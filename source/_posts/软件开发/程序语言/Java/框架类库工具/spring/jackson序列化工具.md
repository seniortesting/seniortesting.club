---
title: jackson序列化工具
tags: []
keywords: ''
categories: []
abbrlink: IgPZNxpwqG
date: 2021-03-26 20:43:09
description:
cover: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
top_img: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
---



反序列化工具jackson使用

## jackson反序列化myql的datetime类型为LocalDateTime时间错误

> 在jackson反序列化mysql中的datetime类型的数据的时候，发现时间总是不一致，发现是mysql的分区和当前运行程序的分区不一致导致的

- 检查mysql的时区：

```bash

show variables like "%time_zone%";

```

+------------------+--------+
| Variable_name  | Value |
+------------------+--------+
| system_time_zone | CST  |
| time_zone    | SYSTEM |
+------------------+--------+
2 rows in set (0.00 sec)
  #time_zone说明mysql使用system的时区，system_time_zone说明system使用CST时区

- 修改mysql的时区：

```bash
第一种方法
> set global time_zone = '+08:00'; ##修改mysql全局时区为北京时间，即我们所在的东8区
> set time_zone = '+08:00'; ##修改当前会话时区
> flush privileges; #立即生效
第二种方法
# vim /etc/my.cnf ##在[mysqld]区域中加上
default-time_zone = '+08:00'
# /etc/init.d/mysqld restart ##重启mysql使新时区生效
```

## jackson 反序列化报错 `InvalidDefinitionException: Cannot construct instance of`com.xxx`, problem:`java.lang.NullPointerException`

> jackson 反序列化的时候，对象需要有一个默认方法，否则无法构建对象
