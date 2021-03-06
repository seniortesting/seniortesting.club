---
title: zookeeper学习知识点整理
tags: []
keywords: ''
categories: []
abbrlink: 5GThz4fICO
date: 2021-03-26 20:54:54
description:
cover: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
top_img: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
---


zookeeper配置中心

### zookeeper 单机安装配置

> 参考文章: <https://blog.csdn.net/pucao_cug/article/details/71240246>

- 下载安装 `wget http://mirror.bit.edu.cn/apache/zookeeper/current/apache-zookeeper-3.5.5-bin.tar.gz`
- 解压缩tar.gz到目录： `/opt/apache-zookeeper-3.5.5`
- 创建用户，通用方式：

```shell
# 创建用户和创建组，用户systemctl启动用
# sudo groupadd zookeeper
# sudo useradd -d /opt/apache-zookeeper-3.5.5-bin -s /bin/false -g zookeeper zookeeper
# 列出所有的用户组： cut -d: -f1 /etc/group | sort
# 列出所有的用户: sudo cat /etc/passwd
# 对应目录赋予权限： chown -R zookeeper:zookeeper /opt/apache-zookeeper-3.5.5-bin
```

- 进入`cnf`目录复制一份配置文件： `sudo cp zoo_sample.cfg zoo.cfg`
- 创建日志目录： `sudo mkdir /logs/zookeeper && chmod 777 -R /logs`
- 修改`zoo.cfg`配置信息：

```python
# The number of milliseconds of each tick
# 它用来控制心跳和超时，默认情况下最小的会话超时时间为两倍的 tickTime ，就是minSessionTimeout=
tickTime=2000
# The number of ticks that the initial 
# synchronization phase can take
# 集群配置，此配置表示，允许 follower （相对于 leader 而言的“客户端”）连接并同步到 leader 的初始化连接时间，它以 tickTime 的倍数来表示。当超过设置倍数的 tickTime 时间，则连接失败。
initLimit=10
# The number of ticks that can pass between 
# sending a request and getting an acknowledgement
# 集群配置，此配置表示， leader 与 follower 之间发送消息，请求和应答时间长度。如果 follower 在设置的时间内不能与leader 进行通信，那么此 follower 将被丢弃。
syncLimit=5
# the directory where the snapshot is stored.
# do not use /tmp for storage, /tmp here is just 
# example sakes.
# 存储内存中数据库快照的位置
dataDir=/opt/apache-zookeeper-3.5.5-bin/data
# 这个操作将管理机器把事务日志写入到“ dataLogDir ”所指定的目录，而不是“ dataDir ”所指定的目录。这将允许使用一个专用的日志设备并且帮助我们避免日志和快照之间的竞争
dataLogDir=/logs/zookeeper
# the port at which the clients will connect
# 客户端连接的端口
clientPort=2181
# the maximum number of client connections.
# increase this if you need to handle more clients
# 这个操作将限制连接到 ZooKeeper 的客户端的数量，限制并发连接的数量，它通过 IP 来区分不同的客户端。此配置选项可以用来阻止某些类别的 Dos 攻击。将它设置为 0 或者忽略而不进行设置将会取消对并发连接的限制。
maxClientCnxns=60
#
# Be sure to read the maintenance section of the 
# administrator guide before turning on autopurge.
#
# http://zookeeper.apache.org/doc/current/zookeeperAdmin.html#sc_maintenance
#
# The number of snapshots to retain in dataDir
#autopurge.snapRetainCount=3
# Purge task interval in hours
# Set to "0" to disable auto purge feature
#autopurge.purgeInterval=1

```

-- 配置环境变量：`sudo nano /etc/profile`:
> 配置环境变量的目的是为了直接只用zookeeper中bin目录下的命令，如果不配置zookeeper的home路径，并不影响zookeeper启动

```
export ZOOKEEPER_HOME=/opt/apache-zookeeper-3.5.5-bin
export PATH=$ZOOKEEPER_HOME/bin:$PATH
```

-- 启动服务后台运行：`/opt/apache-zookeeper-3.5.5-bin/bin/zkServer.sh start`
-- 启动服务前台运行：`/opt/apache-zookeeper-3.5.5-bin/bin/zkServer.sh start-foreground`
-- 查看服务是否启动: `/opt/apache-zookeeper-3.5.5-bin/bin/zkServer.sh status`

-- 制作启动开机自启动: `sudo nano /lib/systemd/system/zookeeper.service`
-- 设置开机启动: `sudo systemctl daemon-reload && systemctl enable zookeeper.service`

```
[Unit]
Description=zookeeper
After=network.target remote-fs.target nss-lookup.target

[Service]
Type=forking

User=zookeeper
Group=zookeeper

ExecStart=/opt/apache-zookeeper-3.5.5-bin/bin/zkServer.sh start
ExecReload=/opt/apache-zookeeper-3.5.5-bin/bin/zkServer.sh restart
ExecStop=/opt/apache-zookeeper-3.5.5-bin/bin/zkServer.sh stop

[Install]
WantedBy=multi-user.target

```

### zookeeper启动问题

1. 执行`/zkServer.sh start`，看到启动正常，但是执行`zkServer.sh status`确报：

```
Error contacting service. It is probably not running
```

这说明并没有启动成功.我们可以通过bin目录下面的`bin/zookeeper.out`来查看问题原因,但是没有找到这个文件,后来看到执行这个命令让命令在前台运行:
`sudo ./zkServer.sh start-foreground` :

```
/usr/bin/java
ZooKeeper JMX enabled by default
Using config: /opt/apache-zookeeper-3.5.5/bin/../conf/zoo.cfg
错误: 找不到或无法加载主类 org.apache.zookeeper.server.quorum.QuorumPeerMain
```

发现原来是自己下载的zookeeper版本是源码版本，正确的版本应该是: [http://mirror.bit.edu.cn/apache/zookeeper/current/apache-zookeeper-3.5.5-bin.tar.gz](http://mirror.bit.edu.cn/apache/zookeeper/current/apache-zookeeper-3.5.5-bin.tar.gz)

2. 执行`systemctl start zookeeper`报错: `zkServer.sh[985]: Error: JAVA_HOME is not set and java could not be found in PATH.`

> 尽管配置了JAVA_HOME在`/etc/profile`中，但是还是需要下面的命令执行：

```
# update-alternatives --install /usr/bin/java java /opt/jdk1.8.0_211/bin/java 1
# update-alternatives --install /usr/bin/javac javac /opt/jdk1.8.0_211/bin/javac 1
```
