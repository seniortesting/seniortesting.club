---
title: junit5系列(1) - junit5入门介绍
tags: [junit5,unit test,junit5系列]
keywords: 'junit5,junit5系列'
categories: []
abbrlink: iK3VDSMUo7
date: 2021-04-13 11:47:27
description:
cover: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210413125328.png
top_img: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210413125328.png
---


## 1. springboot项目如何使用junit5进行组件测试？


springboot中如何结合`junit5`进行method的快速测试：

```java
package com.example.service.impl;

import static org.springframework.boot.test.context.SpringBootTest.WebEnvironment.RANDOM_PORT;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit.jupiter.SpringExtension;
import com.example.Application;
import lombok.extern.slf4j.Slf4j;


@Slf4j
@ExtendWith(SpringExtension.class)
@SpringBootTest(classes = { Application.class }, webEnvironment = RANDOM_PORT, properties = {
        "spring.profiles.active=local" })
class BookcontextServiceImplTest {

    @Autowired
    private BookcontextService bookContextService;

    @Test
    void getYearOfCustomerRelationship() {
        String externalAccountId = "RCLAMTG9FN8TW";
        final Bookcontext bookContext = Bookcontext.builder()
                .crrType(CrrTypeEnum.REKYC)
                .externalAccountId(externalAccountId)
                .build();
        final Integer yearOfCustomerRelationship = bookContextService.getYearOfCustomerRelationship(crrContext);
        System.out.println(yearOfCustomerRelationship);

    }
}

```