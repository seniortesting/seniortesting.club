---
title: autojs的功能介绍
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

1. autojs开发环境的vscode插件下载,用于开发: 
![](https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210331162416.png)

2. 启动vscode代理服务端口,启动autojs服务, vscode中命令: Ctr + Alt + p，搜索启动命令并执行.

![](https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210331161801.png)

3. 正常启动后vscode可以看到如下界面:

![](https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210331161916.png)


4. 下载安卓模拟器<**雷电模拟器**>,下载apk安装包: [autox.js](https://github.com/kkevsekk1/AutoX/), 并安装在模拟器中

5. 通过模拟器右下角的安装按钮安装，安装成功后打开app，拉开左边的抽屉，**开启无障碍服务**和**悬浮窗**，该功能可与真是手机相同.如图所示:

![](https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210331161412.png)

6. 模拟器或者手机连接vscode服务. 通常是打开模拟设置，WLAN, 高级,查找本地IP地址，在命令行输入ipconfig，找到和模拟器同一网段的IP地址, 打开auto.js app，点击连接电脑，输入电脑的IP地址并确定,连接.

 ![](https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210331162732.png)

 7. 连接成功的话会在visual studio弹出提示

 ![](https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210331162845.png)


## auto.js的脚本开发调试

1. 在VS Code中打开"**Developer tools**"视图,方式如下, 点击"help"->"Toggle Developer Tools"选项. 如下截图:
![](https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210331205225.png)

2. 了解工作目录

Auto.js 软件运行后显示的目录即为工作目录
在工作目录下的项目或脚本才会显示在 Auto.js 软件中
工作目录通常包含以下几种可能
- /内部存储/脚本/
- /emulated/storage/0/脚本/
- /internal storage/Scripts/
- /emulated/storage/0/Scripts/
 

 ### 1. 电脑端

1. 安装 vscode， 在左边插件栏搜索安装Auto.js-VSCodeExt插件。
2. 克隆项目 git clone <https://github.com/wpc2333/AutoWatch.git>
3. 使用vscode打开项目。windows下使用快捷键`ctrlshift+P`，选择运行Auto.js:Start Server打开服务，手机端打开Auto.js 选择连接电脑，输入电脑的ip地址（手机电脑需要在同一局域网下）。
4. 待手机连接上后右下角会出现提示，使用快捷键ctrlshift+P，选择运行`Auto.js:Save Project`即可将项目布置导手机上。
运行程序。
5. 电脑端使用快捷键ctrlshift+P，选择运行`Auto.js:Run On Device`,选择自己的手机IP即可运行。
6. 在手机端运行：打开Auto.js，选择AutoWatch，点击开始运行。

### 2. 手机端

使用手机新建一个项目文件，将main.js的代码全部拷贝即可运行。