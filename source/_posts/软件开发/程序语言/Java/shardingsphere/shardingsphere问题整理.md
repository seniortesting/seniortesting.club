---
title: shardingsphere问题整理
tags: [分库分表,shardingsphere]
keywords: '分库分表,shardingsphere'
categories: []
abbrlink: y9670b080
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

这是因为`shardingsphere`暂时不支持LocalDateTime类型,截至到目前<2021-04-09> 唯一的办法就是等待**5.0.0**版本修复,对应的这个issue的跟踪链接是:<https://github.com/apache/shardingsphere/issues/5420>


