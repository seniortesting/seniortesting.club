---
title: python基础系列(3)-logging日志操作
tags: [python,logging]
keywords: 'python,logging'
categories: []
abbrlink: lxA45H2yQg
date: 2021-04-23 09:52:55
description:
cover: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210419092310.png
top_img: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210419092310.png
---


## logging日志介绍

python中操作日志的模块是`logging`.

## 基本设置

```
import logging

logging.basicConfig(
    level=logging.INFO,
    format='[%(asctime)s %(name)s %(levelname)s : %(message)s',
    datefmt='%Y-%m-%d %H:%M:%S')
logging.getLogger("pytest").setLevel(logging.FATAL)
urllib3.disable_warnings()

LOGGER = logging.getLogger(__name__)

```