---
title: sequelize系列(1)-学习介绍
tags: [sequelize,orm]
keywords: 'sequelize,orm'
categories: []
date: 2021-04-18 15:26:05
description:
abbrlink: zgt94265w4
cover:
top_img:
---

## sequelize介绍

Sequelize是基于Node.js语言的ORM框架，用于Postgres，MySQL，MariaDB，SQLite和Microsoft SQL Server。它具有可靠的事务支持，关系，快速和延迟加载，读取复制等功能。

## 安装

可以通过npm（或yarn）获得`Sequelize`:

```shell
npm install --save sequelize

```

您还必须为所选的数据库手动安装驱动程序：

```shell
# One of the following:
$ npm install --save pg pg-hstore # Postgres
$ npm install --save mysql2
$ npm install --save mariadb
$ npm install --save sqlite3
$ npm install --save tedious # Microsoft SQL Server
```



## 参考链接

- [廖雪峰的简单介绍](https://www.liaoxuefeng.com/wiki/1022910821149312/1101571555324224)
- [官方文档](https://sequelize.org/master/manual/migrations.html)
