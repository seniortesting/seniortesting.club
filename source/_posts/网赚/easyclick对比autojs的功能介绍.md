---
title: easyclick对比autojs的功能介绍
tags: []
keywords: 'easyclick,autojs'
categories: [autojs]
abbrlink: 5670b080
date: 2021-03-29 20:25:48
description:
cover:
top_img:
---

{% note blue 'fas fa-bullhorn' %}

快速对比了下,还是auto.js社区比较活跃,资料最多,唯一的遗憾是不能爬取大厂的app,但是有些人可以破解这个.后面了解下

{% endnote %}

## auto.js的安装配置

1. vscode插件下载,用于开发: 
![](https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210331162416.png)

2. 配置联调环境,启动autojs服务：Ctr + Alt + p，搜索启动命令并执行.

![](https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210331161801.png)

3. 正常启动后vscode可以看到如下界面:

![](https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210331161916.png)


4. 下载安卓模拟器<**雷电模拟器**>,下载apk安装包: [autox.js](https://github.com/kkevsekk1/AutoX/), 并安装在模拟器中

5. 通过模拟器右下角的安装按钮安装，安装成功后打开app，拉开左边的抽屉，**开启无障碍服务**和**悬浮窗**，如图所示:

![](https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210331161412.png)

6. 配置联调环境. 通常是打开模拟设置，WLAN, 高级,查找本地IP地址，在命令行输入ipconfig，找到和模拟器同一网段的IP地址

 打开auto.js app，点击连接电脑，输入电脑的IP地址并确定,连接.

 ![](https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210331162732.png)

 7. 连接成功的话会在visual studio弹出提示

 ![](https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210331162845.png)


## auto.js的开发运行


 