---
title: mysql基础问题整理
tags: [mysql,数据库]
categories: []
date: 2021-03-25 19:24:34
keywords: ''
description:
top_img:
cover:
---



整理一些常见的高频mysql相关的问题




## 定位查询可以是任意查询SQL 

```sql
WITH CTE_TEMP   --公用表表达式（Common Table Expression)
as(
select * FROM ProvinceCity_Test where value LIKE '%西安%'
union ALL
SELECT a.* FROM ProvinceCity_Test a
INNER JOIN CTE_TEMP b ON a.ID = b.ParentID    --父子级关系,递归,递归部分不允许使用外部联接(不允许使用left join等)
)  
SELECT * FROM CTE_TEMP   -- CTE后面必须直接跟使用CTE的SQL语句（如select、insert、update等），否则，CTE将失效。

```

- 递归查询中查询结果分隔符 

[参考递归查询结果分隔符](https://blog.csdn.net/dufemt/article/details/80773394)

![alter](https://img-blog.csdn.net/20180622145111389?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2R1ZmVtdA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

```sql  
with RECURSIVE cte as
(
select a.id,cast(a.name as varchar(100)) from tb a where id='002'
union all 
select k.id,cast(c.name||'>'||k.name as varchar(100)) as name  from tb k inner join cte c on c.id = k.pid
)select id,name from cte ;
```


## 建表规范参考阿里巴巴手册

1. UNSIGNED属性就是将数字类型无符号化，与C、C++这些程序语言中的unsigned含义相同。例如，INT的类型范围是-2 147 483 648 ～ 2 147 483 647， INT UNSIGNED的范围类型就是0 ～ 4 294 967 295



## mysql单索引和联合索引的区别

> 靠左原则

[参考文档](https://blog.csdn.net/Abysscarry/article/details/80792876)

索引如何建立，及其如何使用，参考： https://www.toutiao.com/i6695892976922526212/