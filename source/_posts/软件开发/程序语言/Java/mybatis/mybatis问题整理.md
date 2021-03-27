---
title: mybatis问题整理
tags: []
keywords: ''
categories: []
abbrlink: 7670b080
date: 2021-03-26 20:35:26
description:
cover:
top_img:
---



整理相关mybatis的问题

## 通用MYSQL建表字段模板

```
--
-- Set character set the client will use to send SQL statements to the server
--
SET NAMES 'utf8';

--
--  创建新表的模板，所有的表创建需要已此为模板
-- Create table 新表名称
--
CREATE TABLE 新表名称 (
    -- 必须字段 id, uuid, active,version, gmt_create,gmt_modified, create_by, modified_by
                      id bigint(20) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT '主键',
                      uuid varchar(500) NOT NULL COMMENT '该记录唯一识别码，用于区别主键',
    -- 其他的字段

    -- 以下为必须添加的额外保留字段
                      active tinyint(1) UNSIGNED NOT NULL DEFAULT 1 COMMENT '对应该条记录是否可用，1可用，0不可用',
                      version int(20) UNSIGNED NOT NULL COMMENT '对应乐观锁的版本号',
                      gmt_create datetime NOT NULL COMMENT '对应记录的创建时间',
                      gmt_modified datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '对应记录的修改时间',
                      create_by varchar(250) NOT NULL COMMENT '对应添加记录的人',
                      modified_by varchar(250) NOT NULL COMMENT '对应最后一次修改记录的',
                      PRIMARY KEY (id)
)
    ENGINE = INNODB,
    CHARACTER SET utf8mb4,
    COLLATE utf8mb4_general_ci,
    COMMENT = '新表说明';


```

## `PageHelper` return `PageInfo` total =-1

> Found that the `PageInfo` always return the `total` field as -1, and the select count(*) sql not run

* The reason is as below:

```yml
pagehelper:
  default-count: false
```

* The sql used here is:

```java
    Page<Object> page = PageHelper.startPage(pageNum, pageSize);
    List<PermissionActionResponse> permissionActions = authMapper.getPermissionActions();
    PageInfo<PermissionActionResponse> pageInfo = new PageInfo<>(permissionActions);
```

## mybatis-plus 重要坑记录

* 数据库表的字段为数据库关键字，采用如下声明：

```
1. 关键字数据表： @TableName("[user]")
2. 关键字数据表字段：  @TableField("`desc`")
```

* 配置 MapperScan 注解

> 提到需要写上`@MapperScan("com.baomidou.mybatisplus.samples.quickstart.mapper")`,可以在mapper类上采用注解`@Mapper`达到同样的效果

参考代码： [github 代码段](https://github.com/baomidou/mybatis-plus-samples/blob/master/mybatis-plus-sample-auto-fill-metainfo/src/main/java/com/baomidou/samples/metainfo/mapper/UserMapper.java)

-- 注解 annotation

1. `@TableName`
2. `@TableId`
3. `@TableField`
4. `@Version`

* 分页

```
  // 不进行 count sql 优化，解决 MP 无法自动优化 SQL 问题，这时候你需要自己查询 count 部分
    // page.setOptimizeCountSql(false);
    // 当 total 为非 0 时(默认为 0),分页插件不会进行 count 查询
    // 要点!! 分页返回的对象与传入的对象是同一个

```

* 常见问题整理

[FAQ](https://mybatis.plus/guide/faq.html)

* mybatis plus 详细配置产生实体类及其相关代码

```

import cn.hutool.core.io.FileUtil;
import cn.hutool.core.util.StrUtil;
import com.baomidou.mybatisplus.annotation.DbType;
import com.baomidou.mybatisplus.annotation.FieldFill;
import com.baomidou.mybatisplus.annotation.IdType;
import com.baomidou.mybatisplus.core.exceptions.MybatisPlusException;
import com.baomidou.mybatisplus.generator.AutoGenerator;
import com.baomidou.mybatisplus.generator.config.DataSourceConfig;
import com.baomidou.mybatisplus.generator.config.GlobalConfig;
import com.baomidou.mybatisplus.generator.config.PackageConfig;
import com.baomidou.mybatisplus.generator.config.StrategyConfig;
import com.baomidou.mybatisplus.generator.config.po.TableFill;
import com.baomidou.mybatisplus.generator.config.rules.DateType;
import com.baomidou.mybatisplus.generator.config.rules.NamingStrategy;
import com.baomidou.mybatisplus.generator.engine.FreemarkerTemplateEngine;
import com.google.common.collect.Lists;

import java.util.Scanner;

public class MybatisCodeGenerator {


    public static String scanner(String tip){
        Scanner scanner = new Scanner(System.in);
        StringBuilder help = new StringBuilder();
        help.append("请输入: "+tip+": ");
        System.out.println(help.toString());
        if(scanner.hasNext()){
            String inputTip = scanner.next();
            if(StrUtil.isNotEmpty(inputTip)){
                return inputTip;
            }
        }
        throw new MybatisPlusException("请输入正确的"+tip+"!");
    }


    public static void main(String[] args) {

        // 配置信息
        String url ="jdbc:mysql://192.168.1.108:3306/vrpano?useUnicode=true&useSSL=false&characterEncoding=utf8";
        String username ="yanzhi";
        String passwd="yanzhi123!@#";
        String packageName ="generator";

        // 代码生成器
        AutoGenerator mpg = new AutoGenerator();

        // 数据源配置
        DataSourceConfig dsc = new DataSourceConfig();
        // 必须
        dsc.setDbType(DbType.MYSQL);
        dsc.setUrl(url);
        dsc.setDriverName("com.mysql.cj.jdbc.Driver");
        dsc.setUsername(username);
        dsc.setPassword(passwd);
        mpg.setDataSource(dsc);

        // 全局配置
        GlobalConfig gc = new GlobalConfig();


        String currentFilePath =MybatisCodeGenerator.class.getClassLoader().getResource("").getPath();
        String projectPath = FileUtil.getParent(currentFilePath, 2);
        gc.setOutputDir(projectPath + "/src/main/java");

        gc.setFileOverride(true);
        gc.setOpen(true);
        // 是否在xml中添加二级缓存
        gc.setEnableCache(false);

        gc.setAuthor("Walter Hu");

        gc.setKotlin(false);
        gc.setSwagger2(false);

        gc.setActiveRecord(false);

        // xml中添加返回结果的基本类型
        gc.setBaseResultMap(true);
        // xml中添加基本的数据列
        gc.setBaseColumnList(true);
        // java8 时间映射，所有的时间映射被LocalDate,LocalDateTime类型
        gc.setDateType(DateType.TIME_PACK);

        gc.setEntityName("%sEntity");
        gc.setMapperName("%sMapper");
        gc.setXmlName("%sMapper");
        gc.setIdType(IdType.AUTO);

        mpg.setGlobalConfig(gc);

        //数据库表配置 策略配置
        StrategyConfig strategy = new StrategyConfig();
        // 表名是否大写
        strategy.setCapitalMode(false);
        strategy.setSkipView(true);
        // 表名到实体类的映射关系
        strategy.setNaming(NamingStrategy.underline_to_camel);
//        数据库表字段映射到实体的命名策略, 未指定按照 naming 执行
        strategy.setColumnNaming(NamingStrategy.underline_to_camel);

        String tables = scanner("表名，多个英文逗号分割");
         if(!tables.contains("a")){
             // 全部的表
             String[] parseTables = tables.split(",");
             strategy.setInclude(parseTables);
         }

        // 实体类设置
        // 初始化字段值
        strategy.setEntityColumnConstant(false);
        // lombok类型
        strategy.setEntityLombokModel(true);
        // 将boolean类型的字段去掉前面的is字段
        strategy.setEntityBooleanColumnRemoveIsPrefix(true);
        //
        strategy.setEntitySerialVersionUID(true);
        // 乐观锁字段
        strategy.setVersionFieldName("version");
        // 默认字段
        strategy.setTableFillList(Lists.newArrayList(
                new TableFill("gmt_create", FieldFill.INSERT),
                new TableFill("gmt_modified",FieldFill.INSERT_UPDATE),
                new TableFill("version", FieldFill.INSERT),
                new TableFill("is_active", FieldFill.INSERT)
                ));

        mpg.setStrategy(strategy);
        // 默认是采用velocity 模板的
        mpg.setTemplateEngine(new FreemarkerTemplateEngine());

        // 包配置
        PackageConfig pc = new PackageConfig();
//        pc.setModuleName(scanner("模块名"));
        pc.setParent(packageName);
        mpg.setPackageInfo(pc);


        mpg.execute();
    }
}

```

## 踩坑记录

* 问题描述：

> 单元执行正常，正常service层调用报错，代码很简单：

 1. `sysUserMapper.selectOne(Wrappers.<SysUser>lambdaQuery().eq(SysUser::getUsername,username));`
 2. 报错信息如下：

```
2019-05-15 20:31:58.892 [http-nio-8085-exec-3] DEBUG org.springframework.web.servlet.mvc.method.annotation.ExceptionHandlerExceptionResolver.doResolveHandlerMethodException:403 - Using @ExceptionHandler public com.yanzhi.common.response.WebResponse com.yanzhi.core.vrpanoapp.exception.GlobalExceptionHandler.handleExceptionHandler(java.lang.Exception)
2019-05-15 20:31:58.893 [http-nio-8085-exec-3] ERROR com.yanzhi.core.vrpanoapp.exception.GlobalExceptionHandler.handleExceptionHandler:223 - 未捕获的系统异常：nested exception is org.apache.ibatis.builder.BuilderException: Error evaluating expression 'ew.sqlSegment != null and ew.sqlSegment != '' and ew.nonEmptyOfWhere'. Cause: org.apache.ibatis.ognl.OgnlException: sqlSegment [com.baomidou.mybatisplus.core.exceptions.MybatisPlusException: Your property named "username" cannot find the corresponding database column name!]
org.mybatis.spring.MyBatisSystemException: nested exception is org.apache.ibatis.builder.BuilderException: Error evaluating expression 'ew.sqlSegment != null and ew.sqlSegment != '' and ew.nonEmptyOfWhere'. Cause: org.apache.ibatis.ognl.OgnlException: sqlSegment [com.baomidou.mybatisplus.core.exceptions.MybatisPlusException: Your property named "username" cannot find the corresponding database column name!]
```

* 解决方法：

> 移除 `dev-tools`,参见 [https://github.com/baomidou/mybatis-plus/issues/1137](https://github.com/baomidou/mybatis-plus/issues/1137)

## mybatis中的mapper传参/foreach用法

[参考](https://www.toutiao.com/i6650268183603184141/?tt_from=weixin&utm_campaign=client_share&wxshare_count=1&timestamp=1558061459&app=news_article&utm_source=weixin&utm_medium=toutiao_ios&req_id=201905171050590100290580310951B02&group_id=6650268183603184141)

## 使用mybatis的自定义查询

```
// mapper层

public List<DTO> listResult(@Param(Constants.WRAPPER) Wrapper wrapper)

```

```xml

<select id="getAll" resultType="MysqlData">
 SELECT * FROM mysql_data ${ew.customSqlSegment}
</select>

```

## mybatis plus自定义分页出错

采用mybatis plus的自定义查询报错如下：

```java
Caused by: com.baomidou.mybatisplus.core.exceptions.MybatisPlusException: cannot find column's cache for "com.yanzhi.batch.entity.JobListEntity", so you cannot used "class com.baomidou.mybatisplus.core.conditions.query.LambdaQueryWrapper"!
不支持，不可以使用`LambdaQueryWrapper`来构造自定义查询条件

```

那么该如何优雅的使用mybatis提供的QueryWrapper构造子查询条件呢？避免在xml中写大量的`<if test>`进行判断子查询，生成动态的查询条件，如下是操作步骤：

   1. 首先确定配置了拦截器如下：

 ```java
 /**
     * 分页拦截器
     *
     * @return
     */
    @Bean
    public PaginationInterceptor paginationInterceptor() {
        PaginationInterceptor paginationInterceptor = new PaginationInterceptor();

        List<ISqlParser> sqlParserList = new ArrayList<>();
        // 攻击 SQL 阻断解析器、加入解析链作用！阻止恶意的全表更新删除
        sqlParserList.add(new BlockAttackSqlParser());

        paginationInterceptor.setSqlParserList(sqlParserList);
        return paginationInterceptor;

    }
```

   2. 在mapper中定义对应的接口（主要看对应的两个方法参数`IPage`, `@Param(Constants.WRAPPER) Wrapper`，还有返回类型: `IPage`，其他的根据自己的实体调整）:

```java
     IPage<JobListEntity> getJobs(IPage page, @Param(Constants.WRAPPER) Wrapper entityWrapper);
```

   3. 在mapper的xml对应的查询SQL最后定义如下自定义查询:

```java
        <where>
            ${ew.sqlSegment}
        </where>
```

   4. 在service层调用mapper层的方法代码：

```java
        Page<JobListEntity> page = new Page<>(pageNum, PageSize);
        // 或者QueryWrapper queryWrapper =Wrappers.query();
        QueryWrapper queryWrapper = Wrappers.emptyWrapper(); 
        if(StrUtil.isNotEmpty(name)) {
            // 这里填的字段对应查询条件中的数据字段
            queryWrapper.like("qjd.JOB_NAME", name);
        }
        IPage<JobListEntity> jobListEntityIPage = jobMapper.getJobs(page, queryWrapper);
```

关于 `${ew.sqlSegment}` 使用了 `$` 不要误以为就会被 sql 注入，请放心使用 mp 内部对`wrapper` 进行了字符转义处理！

## mybatis `Blob`字段类型转换

::: warning MYSQL的BLOB /CBLOB 字段
> 经确认mybatis对应的Blob数据库类型不是`java.sql.Blob`类型，否则获取的结果是null，应该对应的是`byte[]`,而`clob`对应的则是 `String`
:::

## mybatis-plus枚举类型

参考例子代码: [https://gitee.com/baomidou/mybatis-plus-samples](https://gitee.com/baomidou/mybatis-plus-samples)

1. 通常的方法进行序列化和反序列化

使用的是`jackson`进行序列化和反序列化

* 将枚举序列化需要的是注解 : `@JsonValue`
* 将枚举反序列化需要的注解 ： `@JsonCreator`

2. 采用mybatis-plus进行枚举的序列化和反序列：

* 设置mybatis-plus进行枚举的转换:

```yaml
# mybatis相关配置
mybatis-plus:
  #  configLocation
  mapper-locations: classpath*:mapper/**/*.xml
  check-config-location: false
  # 该执行器类型会复用预处理语句（PreparedStatement）
  executor-type: reuse
  # 以下的是原生的mybatis的配置信息
  configuration:
    # 列名驼峰转换
    map-underscore-to-camel-case: true
    cache-enabled: true
    aggressive-lazy-loading: true
    auto-mapping-unknown-column-behavior: warning
    # 此处设置序列化的转换器，是需要定义一个方法: getValue
    default-enum-type-handler: com.baomidou.mybatisplus.extension.handlers.EnumTypeHandler

```

* 枚举类举例如下:

```java
@Getter
@AllArgsConstructor
public enum ProductCategory implements IEnum<Long> {
    /**
     * 产品类型
     */
    WOOD(1L, "WOOD", "方木"),
    REBAR(2L, "REBAR", "钢筋"),
    CEMENT(3L, "CEMENT", "水泥"),
    TEMPLATE(4L, "TEMPLATE", "模板"),
    MIXED(5L, "MIXED", "混合版"),
    DIGGING_MACHINE(6L, "DIGGING_MACHINE", "挖机"),
    CRANE(7L, "CRANE", "吊车"),
    FORKLIFT(8L, "FORKLIFT", "铲车"),
    CONCRETE(9L, "CONCRETE", "混凝土");

    private Long id;

    private String name;

    private String description;


    @Override
    public Long getValue() {
        return id;
    }
}
```
