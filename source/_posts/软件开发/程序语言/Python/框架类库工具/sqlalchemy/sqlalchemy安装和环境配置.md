---
title: Python SQLAlchemy Linux安装及其环境配置
categories: []
abbrlink: ITwraDciAW
date: 2021-04-05 09:52:55
description:
cover: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210419092310.png
top_img: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210419092310.png
---


## SQLAlchemy model code generator[更新到2019年8月10日]

Python环境下执行如下命令全局安装`sqlacodegen`

```shell script

pip install pymysql sqlacodegen
sqlacodegen --noviews --noindexes --nojoined --outfile models.py  mysql+pymysql://syscorer:s6s@#@!L0ngh@192.168.1.7:3306/heapstack 
sqlacodegen --noviews --noindexes --nojoined --noinflect --noclasses --outfile models.py  mysql+pymysql://syscorer:s6s@#@!L0ngh@192.168.1.7:3306/heapstack 
sqlacodegen --tables abc --noviews --noindexes --nojoined --noinflect --noclasses --outfile models.py  mysql+pymysql://syscorer:s6s@#@!L0ngh@192.168.1.7:3306/heapstack 

```
