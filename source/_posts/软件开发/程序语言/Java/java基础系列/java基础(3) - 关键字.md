---
title: java基础(3) - 关键字
tags: [java基础,关键字]
keywords: 'java基础,关键字'
categories: []
abbrlink: p91D51Eg6EFh
date: 2021-04-16 23:14:50
description:
cover: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
top_img: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
---


## 泛型

Java泛型中的标记符含义：
 
 - E - Element (在集合中使用，因为集合中存放的是元素)

 - T - Type（Java 类）T代表在调用时的指定类型。会进行类型推断

 - K - Key（键）
 - V - Value（值）
 
 - N - Number（数值类型）
 - R - Result （返回结果，多用于函数式编程）

- ？ -  表示不确定的java类型
- S、U、V  - 2nd、3rd、4th types

 PS: 其实**以上这些对于java编译器来说作用都一样，都是作为一个占位作用**，要在使用时就能确定类型，也就是说A,B,C...Z等大写字母都可以表示泛型，只不过以上泛型的定义，更多是我们程序员间约定俗成的命名方式，一种规范，从而达到“见其名则知其意”的目的，罢了。

