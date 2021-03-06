---
title: scrapy logging模块配置
tags: [leetcode,刷题,算法]
abbrlink: 9INw2VVe9l
tags: []
keywords: ''
categories: []
date: 2021-03-25 23:12:53
description:
cover: 
top_img:
---



## 配置

在`settings.py`中配置对应的字段：

```
log_day=datetime.datetime.now()
log_file_path= "{}-{}-{}.log".format(log_day.year,log_day.month,log_day.day)

LOG_ENABLED = True
LOG_ENCODING = 'utf-8'
LOG_FILE = log_file_path
LOG_FORMAT='%(asctime)s [%(name)s] %(levelname)s: %(message)s'
LOG_STDOUT=False
LOG_LEVEL = 'INFO'
```

## 使用

使用方式有两种,一种是通过`logging`模块引用，一种是通过引用`scrapy`自带的` self.logger.`模块。如下：

1. 方法一：

```python
import logging
logger = logging.getLogger(__name__)
logger.warning("This is a warning")
```

2. 方法二：

```python
import scrapy

class MySpider(scrapy.Spider):

    name = 'myspider'
    start_urls = ['https://scrapinghub.com']

    def parse(self, response):
        self.logger.info('Parse function called on %s', response.url)
```

## 问题

### 1. 设置了`LOG_FILE`参数后控制台将不会产生日志？
官方说明是设置了该参数后会重定向所有的日志到文件，所以控制台没有日志。如果需要控制台有日志，需要配置不同环境设置该参数为`None`或者文件目录。

### 2. 通过`scrapyd`调度的egg执行的爬虫日志文件在哪里?
找到`scrapyd`的配置文件，通过如下命令：
```
find / -name "default_scrapyd.conf"
```
里面有一个配置`logs_dir    = /logs`,这个配置对应的就是存放日志的目录，然后切换到该目录下面会找到对应的scrapyd项目下面的爬虫目录对应的日志文件。