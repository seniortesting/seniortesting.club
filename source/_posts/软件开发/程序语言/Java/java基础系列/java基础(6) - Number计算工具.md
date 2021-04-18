---
title: java基础(6) - Number计算工具
tags: [java基础,Math]
keywords: 'java基础,Number'
categories: []
abbrlink: m621u1Eg6EFh
date: 2021-04-16 23:14:50
description:
cover: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
top_img: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
---


## 基本数据类型

Java**中**有 8 种基本数据类型，分别为：

1. 6 种数字类型 ：byte、short、int、long、float、double
2. 1 种字符类型：char
3. 1 种布尔型：boolean

这八种基本类型都有对应的包装类分别为：Byte、Short、Integer、Long、Float、Double、Character、Boolean

| 基本类型 | 位数 | 字节 | 默认值  | 最小值 |最大值
| :------- | :--- | :--- |  :---|:---|------- |
| byte     | 8    | 1    | 0    | -128（-2^7） | 127（2^7-1)
| int      | 32   | 4    | 0    | -2,147,483,648（-2^31）| 2,147,483,647（2^31 - 1）
| short    | 16   | 2    | 0    | -32768（-2^15） | 32767（2^15 - 1）
| long     | 64   | 8    | 0L   | -9,223,372,036,854,775,808（-2^63） | 9,223,372,036,854,775,807（2^63 -1）
| float    | 32   | 4    | 0f      |
| double   | 64   | 8    | 0d      |
| char     | 16   | 2    | 'u0000' |
| boolean  | 1    |      | false   |


对于 boolean，官方文档未明确定义，它依赖于 JVM 厂商的具体实现。逻辑上理解是占用 1 位，但是实际中会考虑计算机高效存储因素。

注意：

1. Java 里使用 long 类型的数据一定要在数值后面加上 **L**，否则将作为整型解析：
2. `char a = 'h'`char :单引号，`String a = "hello"` :双引号

## 自动装箱与拆箱

- 装箱：将基本类型用它们对应的引用类型包装起来；
- 拆箱：将包装类型转换为基本数据类型；

