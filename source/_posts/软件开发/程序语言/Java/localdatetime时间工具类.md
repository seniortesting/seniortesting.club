---
title: localdatetime时间工具类
tags: []
keywords: ''
categories: []
abbrlink: 7670b080
date: 2021-03-26 20:44:19
description:
cover:
top_img:
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
