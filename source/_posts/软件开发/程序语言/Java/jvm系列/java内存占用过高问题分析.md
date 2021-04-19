---
title: java内存占用过高问题分析
tags: []
keywords: ''
categories: []
abbrlink: GxGWU8kfyb
date: 2021-03-26 20:50:03
description:
cover: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
top_img: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
---



java相关问题错误解决方案

## 生产环境java内存占用很高排查 （尚未解决）

- 命令`top`查看对应的java进程的`pid`,记录下该数值（16066）

- 定位线程问题（通过命令查看16066进程的线程情况），命令：`ps p 16066 -L -o pcpu,pmem,pid,tid,time,tname,cmd`

- 输出堆栈信息,将PID为16066的堆栈信息打印到jstack.log中，命令：`jstack -l 16066 > /logs/jvm/jstack.log`

> jvm运行时会生成一个目录hsperfdata_$USER($USER是启动java进程的用户)，在linux中默认是/tmp。目录下会有些pid文件，存放jvm进程信息。
jps、jstack等工具读取/tmp/hsperfdata_$USER下的pid文件获取连接信息。jstack报错：Unable to open socket file。是因为这个java进程的pid文件删除了。

为什么会被删除呢？这是因为linux操作系统为了防止/tmp目录文件过多，有个删除管理机制：tmpwatch。

查看关键配置`/etc/cron.daily/tmpwatch`：

```shell
flags=-umc /usr/sbin/tmpwatch "$flags" 
-x /tmp/.X11-unix -x /tmp/.XIM-unix \ 
 -x /tmp/.font-unix -x /tmp/.ICE-unix 
-x /tmp/.Test-unix 240 /tmp /usr/sbin/tmpwatch "$flags" 720 /var/tmp 
for d in /var/{cache/man,catman}/{cat?,X11R6/cat?,local/cat?}; 
do if [ -d "$d" ]; then /usr/sbin/tmpwatch "$flags" -f 720 "$d" fi done
```

系统每天会用tmpwatch命令检查并删除 /tmp 下超过240小时未访问过的文件和目录。

### 解决办法

修改tmpwatch设置
排查对应的/tmp/hsperfdata_*的目录，让jvm自己来管理，保证jps,jstat等命令可用。
修改`/etc/cron.daily/tmpwatch`:

```sh
/usr/sbin/tmpwatch "$flags" -x /tmp/hsperfdata_* -x /tmp/.X11-unix -x /tmp/.XIM-unix
 -x /tmp/.font-unix -x /tmp/.ICE-unix -x /tmp/.Test-unix 240 /tmp
```
