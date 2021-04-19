---
title: spring JPA使用技巧问题整理
keywords: ''
categories: []
abbrlink: 94t235nOPVFCy6D
date: 2021-04-16 20:37:44
description:
cover: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
top_img: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
---

## 如何自动生成一个spring jpa entity？

参考： <https://blog.csdn.net/linmengmeng_1314/article/details/101599559>

1. 新建一个数据源连接
2. 修改对应的groovy脚本，配置生成的脚本
3. 选择对应的表，然后生成对应的entity文件

以上的操作不再使用，可以采用idea的POJO generator插件


## Entity中常量如何转为枚举类型？

对于数据库中某些字段是一些常量值，此时可以考虑转为枚举类型，操作如下：

1.创建枚举文件夹`constant.enums` ，常量文件夹`constant.consist`;


通过code转枚举对象方法：

```
    public static ListingType toEnum(String value) {
        return Stream.of(ListingType.values()).filter(item -> item.getDbMappingKey().equals(value))
                .findFirst().orElse(null);
    }
```

## CrudRepository 和 JpaRepository 区别

使用Spring Data JPA CrudRepository 和JpaRepository 的好处：

继承这些接口，可以使Spring找到自定义的数据库操作接口，并生成代理类，后续可以注入到Spring容器中；
可以不写相关的sql操作，由代理类生成
他们存在继承关系：

PagingAndSortingRepository 继承 CrudRepository
JpaRepository 继承 PagingAndSortingRepository

也就是说， CrudRepository 提供基本的增删改查；
PagingAndSortingRepository 提供分页和排序方法；
JpaRepository 提供JPA需要的方法。


## 常用`JpaRepository`方法代码

### 1. 方法的参数如何在sql中表示？

```java
// 如果参数不加上@param，则可以用索引1，2，3，4代表对应的参数，采用?
@Query(value = "select ACCOUNT_ID, sum(AMOUNT) " +
            "from TRANSACTION t " +
            "where t.TXN_STATUS=?1 " +
            "and t.TXN_TYPE=?2 " +
            "and t.TIME_CREATED>=?3 " +
            "and t.TIME_CREATED<=?4 " +
            "group by t.ACCOUNT_ID "
            , nativeQuery = true)
    List<Object[]> queryAccountAndAmount(String txnStatus, String txnType, Long startTime, Long endTime);

// 如果加上@Param参数可以直接采用关键字进行参数赋值，采用：
// 另外如果查询的结果是一个表，可以直接返回List<entity>，否则返回的是List<Object[]> 类型
@Query(value = "SELECT t FROM PERSON t " +
            "WHERE t.custName=:custName " +
            "AND t.certNoHash=:certNoHash " +
            "AND t.listType=:type " +
            "AND t.certType=:certType " +
            "AND t.isEnabled=true AND (t.expireDate is null OR t.expireDate>=:expireDate)")
    List<Person> findAxxx(@Param("custName") String custName,
                                @Param("certNoHash") String certNoHash,
                                @Param("certType") DocumentTypeEnum certType,
                                @Param("type") ListType type,
                                @Param("expireDate") Date date);
```

### 2. 查询条件的参数如果是对象，对应的sql怎么书写？

传入的参数是个对象,采用#
```java
@Query("select t "
            + " from Threshold t "
            + " where t.stat=:#{#param.comRuleStat}"
            + " and t.type=:#{#param.thresholdType}  "
            + " and t.isRealNameCertify=:#{#param.isRealNameCertify} "
            + " and t.custType=:#{#param.custType} "
            + " and t.payChannel=:#{#param.payChannel} "
            + " and t.TxnCd=:#{#param.intTxnCd} ", nativeQuery = true
)
List<Threshold> queryThreshold(@Param("param") ThresholdQuery thresholdQuery);
```

### 3. 如何查询一个数组或者list的数据？

```java
@Repository
public interface ClientRepository extends CrudRepository<Client, Long>, JpaSpecificationExecutor<Client> {

    @Query(value = "SELECT * FROM Client t WHERE t.id IN (:ids) " , nativeQuery = true)
    List<Client> findByIds(@Param("ids") List<String> ids);
}
// jpa 语句IsIn
Integer countByTimeCreatedGreaterThanEqualAndTimeCreatedLessThanAndBankIdIsInAndTxnStatusIsIn(
        Long startTime, Long endTime,
        List<Long> bankId,
        List<TxnStatus> status);
```

### 4. 查询条件动态sql构建，条件不固定怎么操作？

```java
@Query(value = "select * from LOGIN_LOGS where 1=1 and if(?1 !='',ip=?1,1=1) and if(?2 !='',custId<>?2,1=1)",
            nativeQuery = true)

```

### 5. 如何执行一个自定义的更新和删除的Sql？

同样也是采用查询的annotation= @Query操作，但是需要加上`@Modifying`的注解，同时加上`@Transactional`注解

```java
    @Transactional
    @Modifying
    @Query(value = " update PERSON t "
            + " set t.IS_ENABLED='0', t.TIME_UPDATED=:timeUpdated "
            + " where t.IS_ENABLED='1' and t.id=:id ", nativeQuery = true)
    int softDelete(@Param("id") long id, @Param("timeUpdated") long timeUpdated);

```

### 6. 如何构建分页查询数据？

**注意里面的变量不是表列，而是entity的属性名称**

```java
   @Override
    public Page<HandleRule> queryHandleRule(final RequestRuleVo paramVo, final int pageNum,
            final int pageSize) {
        Specification<HandleRule> spec = (root, query, criteriaBuilder) -> {
            List<Predicate> list = new LinkedList<>();
            list.add(criteriaBuilder.equal(root.get("handleId"), paramVo.getHandleId()));
            if (StringUtils.isNotBlank(paramVo.getType())) {
                list.add(criteriaBuilder.equal(root.get("type"), paramVo.getType()));
            }
            if (StringUtils.isNotBlank(paramVo.getEngine())) {
                list.add(criteriaBuilder.equal(root.get("engine"), paramVo.getEngine()));
            }
            if (StringUtils.isNotBlank(paramVo.getRuleName())) {
                list.add(criteriaBuilder.equal(root.get("ruleName"), paramVo.getRuleName()));
            }
            if (StringUtils.isNotBlank(paramVo.getResult())) {
                list.add(criteriaBuilder.equal(root.get("result"), paramVo.getResult()));
            }
            if (StringUtils.isNotBlank(paramVo.getCode())) {
                list.add(criteriaBuilder.equal(root.get("code"), paramVo.getCode()));
            }
            return criteriaBuilder.and(list.toArray(new Predicate[list.size()]));
        };
        Page<HandleRule> page = handleRuleRepository.findAll(spec, PageRequest.of(pageNum - 1,
                pageSize, Sort.by(Sort.Direction.ASC, "timeOrder")));
        return new PageImpl<>(page.get()
                .collect(Collectors.toList()), page.getPageable(), page.getTotalElements());
    }
```

### 7. 如何采用jpa方式查询单条记录？


```java

Optional<Transaction> queryByTxnId(String encryptTxnId);

Optional<RatingRecord> findByCustIdEquals(String customerId);

```

### 8. 如何采用jpa查询单表是否有记录,存在该记录？

```java
boolean existsByOriginalReqId(String reqId, IntTxnCdEnum transtionEnum, String tenant);
```
### 8. 如何查询返回结果的条数？

```java
 Integer countByTimeCreatedGreaterThanEqualAndTimeCreatedLessThanAndBankIdIsInAndTxnStatusIsIn(
            Long startTime, Long endTime,
            List<Long> bankId,
            List<TxnStatus> status);

```