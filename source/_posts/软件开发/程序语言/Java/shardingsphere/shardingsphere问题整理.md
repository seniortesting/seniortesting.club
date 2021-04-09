---
title: shardingsphere问题整理
tags: [分库分表,shardingsphere]
keywords: '分库分表,shardingsphere'
categories: []
abbrlink: 7670b080
date: 2021-04-09 09:23:45
description:
cover:
top_img:
---

## java.sql.SQLFeatureNotSupportedException: getObject with type

- 问题描述

Using MyBatis to return a LocalDateTime type field gives an error.

java.sql.SQLFeatureNotSupportedException: getObject with type
at org.apache.shardingsphere.shardingjdbc.jdbc.unsupported.AbstractUnsupportedOperationResultSet.getObject(AbstractUnsupportedOperationResultSet.java:221) ~[sharding-jdbc-core-4.1.0.jar:4.1.0]
at org.apache.ibatis.type.LocalDateTimeTypeHandler.getNullableResult(LocalDateTimeTypeHandler.java:38) ~[mybatis-3.5.2.jar:3.5.2]

The sharding-jdbc version used is 4.1.1

- 解决方案

这是因为`shardingsphere`暂时不支持LOcalDateTime类型


