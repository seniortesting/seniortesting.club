---
title: logback使用技巧问题整理
keywords: ''
categories: []
abbrlink: b53t235nOPVFCy6D
date: 2021-04-16 20:37:44
description:
cover:
top_img:
---

## how to disable logback startup load message in console?

```xml
    <!-- Stop output INFO at start -->
    <statusListener class="ch.qos.logback.core.status.NopStatusListener"/>

```

## sample configuration file

if the loback configuration met some exception, we can set the `debug="true"` to view the logback detail information to get the reason.

`logback.xml` file

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration scan="true" debug="false">
    <!-- Stop output INFO at start -->
    <statusListener class="ch.qos.logback.core.status.NopStatusListener"/>
    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <charset>UTF-8</charset>
            <Pattern>%d %-4relative [%thread] %-5level %logger{35} - %msg%n</Pattern>
        </encoder>
    </appender>
    <appender name="FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>logs/application.log</file>
        <rollingPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedRollingPolicy">
            <!-- daily rollover. Make sure the path matches the one in the file element or else
             the rollover logs are placed in the working directory. -->
            <fileNamePattern>logs/application_%d{yyyy-MM-dd}.%i.log</fileNamePattern>
            <maxFileSize>10MB</maxFileSize>
            <!-- keep 15 days' worth of history -->
            <maxHistory>15</maxHistory>
            <totalSizeCap>3GB</totalSizeCap>
        </rollingPolicy>
        <encoder>
            <charset>UTF-8</charset>
            <pattern>%d %-4relative [%thread] %-5level %logger{35} - %msg%n</pattern>
        </encoder>
    </appender>
    <root level="DEBUG">
        <appender-ref ref="CONSOLE"/>
        <appender-ref ref="FILE"/>
    </root>
</configuration>
```