---
title: java基础(2) - IO流
tags: [java基础,IO流]
keywords: 'java基础,IO流'
categories: []
abbrlink: mD51Eg6EFh
date: 2021-04-14 23:14:50
description:
cover: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
top_img: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
---



## 1. BIO,NIO,AIO 

> When you execute something synchronously, you wait for it to finish before moving on to another task. When you execute something asynchronously, you can move on to another task before it finishes.

> 当你同步执行某项任务时，你需要等待其完成才能继续执行其他任务。当你异步执行某些操作时，你可以在完成另一个任务之前继续进行。

- 同步 ：两个同步任务相互依赖，并且一个任务必须以依赖于另一任务的某种方式执行。 比如在A->B事件模型中，你需要先完成 A 才能执行B。 再换句话说，同步调用中被调用者未处理完请求之前，调用不返回，调用者会一直等待结果的返回。
- 异步： 两个异步的任务是完全独立的，一方的执行不需要等待另外一方的执行。再换句话说，异步调用中一调用就返回结果不需要等待结果返回，当结果返回的时候通过回调函数或者其他方式拿着结果再做相关事情，

阻塞和非阻塞

- 阻塞： 阻塞就是发起一个请求，调用者一直等待请求结果返回，也就是当前线程会被挂起，无法从事其他任务，只有当条件就绪才能继续。
- 非阻塞： 非阻塞就是发起一个请求，调用者不用一直等着结果返回，可以先去干其他事情。


### 1.1  BIO (Blocking I/O)

同步阻塞I/O模式，数据的读取写入必须阻塞在一个线程内等待其完成。

### 1.2 


## 2. listFiles 列出所有的文件

一种是直接采用递归的方式（`new File("").listFiles();`），稍微有一点点复杂。

下面为简化模式java8代码：

```java
        List<String> result = Files.walk(Paths.get("D:\\"))
                .filter(Files::isRegularFile)
                .map(path -> path.getFileName().toString())
                .collect(Collectors.toList());
        
```

## 文件复制/下载的时候报 premature eof异常？

在进行下载的时候偶尔会发现出现错误： `java.io.IOException: Premature EOF`,搜索发现，这个是普遍性的一个问题，解决方法：

<https://stackoverflow.com/questions/13210108/reading-a-web-page-in-java-ioexception-premature-eof>

发生Premature EOF的可能有：
　　1. 在stream到达EOF之前，stream已经结束。( no EOF marker)，显然这种情况下很有可能是响应超时、服务端处理错误、网络问题、防火墙。
　　2. EOF过早地出现了。( EOF marker comes earlier before it shoud be.)

目前，没有找到很好的有效的解决方法。因为，这个问题出现的原因有很多。有些是客户端问题，这种问题可以通过改善良好的代码习惯来杜绝。比如，要记住关闭流以及网络连接，合理使用网络和计算机资源。在读取网络流之前可以试探流是否已经准备好。

　　本人也遇到过Premature EOF的问题，最开始这个问题很令人头疼。当时是一个多线程的程序（而且线程数相对较多，10个），虽然对于一些线程返回的结果正常，然而也有一大部分的Premature EOF异常。为此，我检查了一遍又一遍的代码，上网找了许多潜在的解决方法，但均没有很好地解决问题。

　　考虑到这个异常有可能是服务器端的错误，以及我当时所调用的服务器的资源情况，最后我将线程数设置为2个这种异常便不再出现了。因此，可以猜测到程序的多线程调用造成了服务端程序的资源争抢等问题导致了Premature EOF异常。所以，在开发应用程序的过程中也应该注意到合理使用服务器的资源。



