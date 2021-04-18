---
title: java基础(5) - 时间工具
tags: [java基础,时间工具]
keywords: 'java基础,时间'
categories: []
abbrlink: ab31u1Eg6EFh
date: 2021-04-16 23:14:50
description:
cover: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
top_img: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
---



LocalDateTime工具使用

## Unable to obtain LocalDateTime from TemporalAccessor: {},ISO resolved to 2018-04-30 of type java.tim

> 原因日期格式的时间不能转化为LocalDateTime

可采用如下方法解决：

```java
   public static LocalDateTime parseDate(String dateStr) {
        DateTimeFormatter baseDateTimeFormatter = DateTimeFormatter.ofPattern("yyyy-MM-dd");

        DateTimeFormatter dateTimeFormatter = new DateTimeFormatterBuilder().append(baseDateTimeFormatter)
                .parseDefaulting(ChronoField.HOUR_OF_DAY, 0)
                .parseDefaulting(ChronoField.MINUTE_OF_HOUR, 0)
                .parseDefaulting(ChronoField.SECOND_OF_MINUTE, 0)
                .toFormatter();
        return LocalDateTime.parse(dateStr, dateTimeFormatter);
    }
```
