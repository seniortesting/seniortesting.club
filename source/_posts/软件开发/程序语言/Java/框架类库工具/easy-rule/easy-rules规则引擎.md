---
title: 规则引擎easy-rules
tags: []
keywords: ''
categories: []
abbrlink: 8ou341bh2np
date: 2021-04-18 23:12:53
description:
cover: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
top_img:  https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
---

## 使用场景

在编写代码过程中，我们对于if...else...语句是相当的熟悉了。但是如果条件分支比较多，比如有十几个、几十个、上百个，甚至更多时，如果我们还坚持在业务逻辑代码中使用if...else...语句，那么这个文件中的代码显得十分不协调，并且如果我们以后想再增加或减少规则时，还要来到这块业务逻辑代码中去修改if...else...语句，这给将来的维护带来了一定的不便。
        针对这种情况，我们可以考虑使用规则引擎来解决。规则引擎不只一种，本文介绍的是easy rule规则引擎的使用。对于上面的场景，**easy rule会把if...else...中的逻辑从业务逻辑代码中提取出来，并把这些逻辑存放在其他文件中**。这样做以后，业务逻辑代码看上去就清爽了很多。同时如果将来我们想要修改这些规则时，直接去找这些存放规则的文件就行了。**在easy rule中，存放规则有两种方式，一种是使用 .java 文件，另外一种是使用 .yml 文件，下面我们分别介绍**。
