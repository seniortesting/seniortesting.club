---
title: python系列(1)-requirements.txt文件使用介绍
tags: [python]
keywords: 'python,requirements.txt'
categories: []
date: 2021-04-15 09:52:55
description:
cover:
top_img:
---

## requirements.txt介绍

requirements.txt 文件里面记录了当前程序的所有依赖包及其精确版本号。类似于node中的`package.json`,类似于java的`pom.xml`,都是用于管理当前项目的依赖包。一个requirements.txt只是简单的列出来了当前项目使用的包。

它的语法很简单遵循以下几个规则：



## 1. 由安装包生成对应的requirements.txt文件

执行命令：

```shell
$ python3 -m pip freeze > requirements.txt
```

而对于使用Pycharm或者IDEA工具的小伙伴可以通过更简单的操作使得根据当前项目已经安装的包自动生成对应的`requirements.txt`文件,操作步骤如下：
![](https://cdn.jsdelivr.net/gh/alterhu2020/CDN%20/img/blog/20210415100512.png)

在弹出的对话框中可以对生成的requirements.txt文件进行相关的配置：
![](https://resources.jetbrains.com/help/img/idea/2021.1/py_sync_requirements.png)

## 2. 通过requirements.txt安装项目依赖包

执行命令：

```shell
$ pip install -r requirements.txt
```

## 参考链接

- [Use requirements.txt in Pycharm](https://www.jetbrains.com/help/pycharm/managing-dependencies.html)
-  [Requirements.Txt Syntax](https://docs.activestate.com/platform/projects/requirements-txt/)