---
title: JDK版本新特性
keywords: ''
categories: []
abbrlink: OFru0C2bVe
date: 2021-03-26 20:38:51
description:
cover: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
top_img: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
---


## jdk的docker镜像的选择？

adoptopenjdk 镜像：

- adoptopenjdk/openjdk8

- adoptopenjdk/openjdk9

- adoptopenjdk/openjdk10

之后是 OpenJ9，也是由 adoptopenjdk 为 8/9 版本所提供的，同时包含为 9 发布的每日构建版：

- adoptopenjdk/openjdk8-openj9

- adoptopenjdk/openjdk9-openj9

- adoptopenjdk/openjdk9-openj9:nightly

而以`adoptopenjdk:8-jdk-openj9`开头的则是官方的镜像包，主要是ubuntu和windows的，镜像比较大。不推荐此处。

# adoptopenjdk/openjdk8:slim对比openjdk

众所周知Oracle JDK商业使用开始收费了，然而Oracle在<http://jdk.java.net/放出的官方版OpenJDK>有下面几点问题：

1、没有32位

2、没有安装程序（初学者会遇到困难，比如设置PATH，运行jar等）

3、旧版不更新（即使LTS版本）

4、没有JRE

因此不推荐从<http://jdk.java.net/下载OpenJDK>。

AdoptOpenJDK是OpenJDK的社区维护版，主要维护8、11两个LTS版本以及最新版本。

AdoptOpenJDK官网：<https://adoptopenjdk.net/>

清华大学镜像：<https://mirrors.tuna.tsinghua.edu.cn/AdoptOpenJDK/>

进行Java开发需要下载JDK，msi版本是安装程序，推荐初学者使用安装程序。

64位Windows的JDK8：<https://mirrors.tuna.tsinghua.edu.cn/AdoptOpenJDK/8/jdk/x64/windows/>

32位Windows的JDK8：<https://mirrors.tuna.tsinghua.edu.cn/AdoptOpenJDK/8/jdk/x32/windows/>

64位Windows的JDK11：<https://mirrors.tuna.tsinghua.edu.cn/AdoptOpenJDK/11/jdk/x64/windows/>

32位Windows的JDK11：<https://mirrors.tuna.tsinghua.edu.cn/AdoptOpenJDK/11/jdk/x32/windows/>

64位有hotspot、openj9两种jvm类型，**hotspot是官方的jvm，兼容性最好，因此一般用途推荐使用hotspot**。

OpenJ9 的前身是IBM的 J9 Java 虚拟机，主要服务于IBM企业级软件产品，是一款高性能的JVM。
在 Web 应用开发中，为了降低内存消耗，你是否尝试过：

去除不必要的组件，减少代码体积

更换 Web 容器，如将 Tomcat 更换为Undertow

优化Docker基础镜像，减少镜像体积

这些效果往往不是很理想。而通过将 HotSpot 更换为 OpenJ9，**内存占用能降低至少 60%**，**而启动时间也能快 40% 以上**，效果立竿见影。

## JDK 11 新特性

> 重要通知，直接从oracle的官方下载的JDK11不再是免费的，若是你一旦不小心使用Java 11进行了具有商业性的行为，那么你很可能将接到Oracle的致电，并要求你提供大量的资金。

1. 删除jre运行库，不在需要配置`JRE_HOME`环境变量
2. 删除Java EE和CORBA模块，JavaFX已经被移除
3. 字符串API增加

- `String#repeat` ，例如`"abc".repeat(3)`
- `String#isBlank`, 例如 `" ".isBlank(); // true`
- `String#strip`， 例如 `" ".strip().isBlank()`
- `String#lines`, 将字符串实例拆分为单独行的`Stream<string>`流, 例如 `"foo\nbar".lines().forEach(System.out::println)`

## JDK 10 新特性

1. 局部变量类型判断
2. GC的优化以及内存管理

## JDK 9

1. 引入了新的HTTPClient操作接口
2. `jshell`交互命令引入,类python的代码块交互平台

## JDK 8

重要: 截止到2020年底不再进行JDK8的更新

1. Lambdas表达式与Functional接口
2. 接口的默认与静态方法
3. 新增方法的调用方式类似php
4. try catch resource
5. 优化了HashMap以及ConcurrentHashMap
