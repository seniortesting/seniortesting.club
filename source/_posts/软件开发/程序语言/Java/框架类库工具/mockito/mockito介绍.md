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


## 配置

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

```java
import org.mockito.junit.jupiter.MockitoExtension;

// @RunWith(MockitoJUnitRunner.class)  
@ExtendWith(MockitoExtension.class)
public class FileProcessorTest {

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

