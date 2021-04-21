---
title: mockito工具介绍
tags: []
keywords: ''
categories: []
abbrlink: 83xt51gAG3oBtK
date: 2021-04-18 20:44:19
description:
cover: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
top_img: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
---


## 配置引入

自带的spring-boot-test已经带了mockito:

```java
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
            <exclusions>
                <exclusion>
                    <groupId>org.junit.vintage</groupId>
                    <artifactId>junit-vintage-engine</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
  
```

常用操作代码如下：

1. 构建一个通用的`Mockito`类。 

```java
import lombok.extern.slf4j.Slf4j;
import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.junit.jupiter.MockitoExtension;


@Slf4j
@ExtendWith({ MockitoExtension.class })
public abstract class LuckyMock {

    @BeforeEach
    public void before() {
        LOGGER.info("<--^^----lucky test start ----^^--->");
    }

    @AfterEach
    public void after() {
        LOGGER.info("<--^^----lucky test end -----^^--->");
    }

}
```

```java
import org.mockito.junit.jupiter.MockitoExtension;


public class FileProcessorTest extends LuckyMock {

    @Mock
    private FileClient fileClient;

    @InjectMocks
    private FileProcessor fileProcessor;


    @Test
    void testUploadFile() {
        FileUploadResponse fileUploadResponse = FileUploadResponse.newBuilder().build();
        Mockito.when(fileClient.uploadFile(anyString(), any(byte[].class))).thenReturn(fileUploadResponse);
        Assert.assertTrue(fileProcessor.uploadFile("test", new byte[1]));
    }

}    

```

## @Mock 和 @InjectMocks 的区别？

- @Mock：可以是interface、class,只是只运行是不进入具体的类中
- @InjectMocks：只能只对class,在JUNIT运行时，可以进入具体的方法中，只是mock的方法，直接返回mock的值。 **简单的说是这个Mock可以调用真实代码的方法，其余用@Mock（或@Spy）注解创建的mock将被注入到用该实例中。**


## 常用的mockit方法有哪些？

