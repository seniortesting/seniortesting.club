---
title: java基础(9) - 文件操作
tags: [java基础,文件操作]
keywords: 'java基础,文件操作'
categories: []
abbrlink: f5x51Eg6EFh
date: 2021-04-14 23:14:50
description:
cover: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
top_img: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
---

## 得到当前代码运行的根目录路径？

可以参考地址： <https://mkyong.com/java/how-to-get-the-current-working-directory-in-java/#:~:text=In%20Java%2C%20we%20can%20use%20System.getProperty%20%28%22user.dir%22%29%20to,program%20was%20launched%20%2F%2F%20e.g%20%2Fhome%2Fmkyong%2Fprojects%2Fcore-java%2Fjava-io%20System.out.println%20%28dir%29%3B>

代码参考如下：

```java
    // System Property
    private static void printCurrentWorkingDirectory1() {
        String userDirectory = System.getProperty("user.dir");
        System.out.println(userDirectory);
    }

    // Path, Java 7
    private static void printCurrentWorkingDirectory2() {
        String userDirectory = Paths.get("")
                .toAbsolutePath()
                .toString();
        System.out.println(userDirectory);
    }

    // File("")
    private static void printCurrentWorkingDirectory3() {
        String userDirectory = new File("").getAbsolutePath();
        System.out.println(userDirectory);
    }

    // FileSystems
    private static void printCurrentWorkingDirectory4() {
        String userDirectory = FileSystems.getDefault()
                .getPath("")
                .toAbsolutePath()
                .toString();
        System.out.println(userDirectory);
    }
```