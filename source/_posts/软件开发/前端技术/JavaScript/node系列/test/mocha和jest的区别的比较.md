---
title: mocha和jest的区别的比较
tags: [mocha，jest]
keywords: 'mocha,jest'
categories: []
date: 2021-04-19 10:12:37
description:
abbrlink:
cover:
top_img:
---

## 前言

测试框架是测试您努力工作的代码的基础。一个好的测试框架可以测试客户端代码。两个最受欢迎的竞争者是Jest和Mocha。
**Jest**是由Facebook开发的开源测试框架，内置于流行的create-react-app程序包中，可以更快，更流畅地编写惯用的JavaScript测试。在并行运行测试时，它具有内置的Mock和Assertion功能，从而提供了更流畅，更快的测试运行。 Jest的一项独特功能是它提供了Snapshot测试，可以完全控制UI。
**Mocha**为开发人员提供了一个基本的测试框架，以及诸如Assertion，Mock和Spy libraries之类的选项。它是最灵活的JavaScript测试库之一。Mocha的缺点是需要额外的设置和配置。柴，最流行的开源断言库与Mocha一起使用。


二者主要区别在于，前者Jest专注于`Unit Test`类型，可能更底层一些，而`Mocha`支持多种类型测试，比如Unit Testing, Intergration Testing, End-to-End Testing。


## 使用



可以看到我们的测试脚本中，有两个方法describe和it.

1. **describe方法**

describe块称为"测试套件"（test suite），表示一组相关的测试。它是一个函数，第一个参数是测试套件的名称（"加法函数的测试"），第二个参数是一个实际执行的函数

2. **it方法**

it块称为"测试用例"（test case），表示一个单独的测试，是测试的最小单位。它也是一个函数，第一个参数是测试用例的名称（"1 加 1 应该等于 2"），第二个参数是一个实际执行的函数。

## mocha参数配置说明

官方配置介绍： <https://github.com/mochajs/mocha/blob/master/example/config/.mocharc.js>


## 参考文档

- [官方例子教程](https://github.com/mochajs/mocha/blob/master/example)
