---
title: Junit5测试技巧和问题整理
tags: []
keywords: ''
categories: []
abbrlink: Dux41bh2np
date: 2021-03-25 23:12:53
description:
cover: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210413125328.png
top_img: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210413125328.png
---


## How to repeat the failed test cases?

- [repeat test](https://www.swtestacademy.com/junit-5-how-to-repeat-failed-test/)
- [return-jupiter](https://github.com/artsok/rerunner-jupiter)

## reorder the junit execution order?

<https://blog.csdn.net/jackyrongvip/article/details/89389387>

## how to configure junit concurrent execution?

Create a file named `junit-platform.properties` in the root of the class path that follows the syntax rules for a Java Properties file.

```java

junit.jupiter.testinstance.lifecycle.default = per_method
junit.jupiter.execution.parallel.enabled = true
junit.jupiter.execution.parallel.mode.default = concurrent
junit.jupiter.execution.parallel.mode.classes.default = same_thread
junit.jupiter.execution.parallel.config.strategy = dynamic

```

or via JVM system property:

```shell
-Djunit.jupiter.extensions.autodetection.enabled=true
```

## references

- [Junit5 examples](https://github.com/kolorobot/junit5-samples/tree/master/junit5-basics/src/test/java/pl/codeleak/samples/junit5/basics)
- [junit5 extension](https://github.com/JeffreyFalgout/junit5-extensions)
