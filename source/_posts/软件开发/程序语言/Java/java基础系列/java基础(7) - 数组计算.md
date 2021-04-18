---
title: java基础(7) - 数组计算
tags: [java基础,数组]
keywords: 'java基础,数组'
categories: []
abbrlink: a0221u1Eg6EFh
date: 2021-04-16 23:14:50
description:
cover: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
top_img: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
---



## 数组的定义

```java
dataType[] arrayRefVar;   // 首选的方法
dataType[] arrayRefVar = new dataType[arraySize];
dataType[] arrayRefVar = {value0, value1, ..., valuek};
        
dataType arrayRefVar[];  // 效果相同，但不是首选方法
```
:::warning 注意
建议使用 dataType[] arrayRefVar 的声明风格声明数组变量。 dataType arrayRefVar[] 风格是来自 C/C++ 语言 ，在Java中采用是为了让 C/C++ 程序员能够快速理解java语言。
:::

## 数组遍历

```java

double[] myList = {1.9, 2.9, 3.4, 3.5};
 
// 打印所有数组元素
for (int i = 0; i < myList.length; i++) {
    System.out.println(myList[i] + " ");
}
// 或者
for(type element: array) {
   System.out.println(element);
}
```

## Arrays 类

java.util.Arrays 类能方便地操作数组，它提供的所有方法都是静态的。具有以下功能：

- 给数组赋值：通过 fill 方法。
- 对数组排序：通过 sort 方法,按升序。
- 比较数组：通过 equals 方法比较数组中元素值是否相等。
- 查找数组元素：通过 binarySearch 方法能对排序好的数组进行二分查找法操作。

