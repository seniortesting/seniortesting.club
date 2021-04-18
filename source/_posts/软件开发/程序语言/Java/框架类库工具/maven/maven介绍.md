---
title: maven介绍
tags: []
keywords: ''
categories: []
abbrlink: nr51gAG3oBtK
date: 2021-04-18 20:44:19
description:
cover:
top_img:
---

## maven的三种scope的区别

参考文档： <https://blog.csdn.net/lishuoboy/article/details/100554751>

maven的执行生命周期：

```java
public enum LifecyclePhase
{
    // 三个部分的phase

    // 第一部分的phase, clean相关
    PRE_CLEAN( "pre-clean" ),
    CLEAN( "clean" ),
    POST_CLEAN( "post-clean" ),

   // 第二部分的默认phase
    VALIDATE( "validate" ),  // 
    INITIALIZE( "initialize" ),
    GENERATE_SOURCES( "generate-sources" ),
    PROCESS_SOURCES( "process-sources" ),
    GENERATE_RESOURCES( "generate-resources" ),
    PROCESS_RESOURCES( "process-resources" ),
    COMPILE( "compile" ),
    PROCESS_CLASSES( "process-classes" ),
    GENERATE_TEST_SOURCES( "generate-test-sources" ),
    PROCESS_TEST_SOURCES( "process-test-sources" ),
    GENERATE_TEST_RESOURCES( "generate-test-resources" ),
    PROCESS_TEST_RESOURCES( "process-test-resources" ),
    TEST_COMPILE( "test-compile" ),
    PROCESS_TEST_CLASSES( "process-test-classes" ),
    TEST( "test" ),
    PREPARE_PACKAGE( "prepare-package" ),
    PACKAGE( "package" ),
    PRE_INTEGRATION_TEST( "pre-integration-test" ),
    INTEGRATION_TEST( "integration-test" ),
    POST_INTEGRATION_TEST( "post-integration-test" ),
    VERIFY( "verify" ),
    INSTALL( "install" ),
    DEPLOY( "deploy" ),

    // 第三部分默认的phase操作
    PRE_SITE( "pre-site" ),
    SITE( "site" ),
    POST_SITE( "post-site" ),
    SITE_DEPLOY( "site-deploy" ),

    NONE( "" );

    private final String id;

    LifecyclePhase( String id )
    {
        this.id = id;
    }

    public String id()
    {
        return this.id;
    }

}

```

生命周期(lifecycle)由多个阶段(phase)组成,每个阶段(phase)会挂接一到多个goal。goal是maven里定义任务的最小单元，goal分为两类，一类是绑定phase的，就是执行到某个phase，那么这个goal就会触发，另外一类不绑定，就是单独任务，这就相当于ant里的target。

注意： **执行某个phase，那么它前面所有phase绑定的目标(goal)都会执行**， 每个phase都会邦定maven默认的goal或者没有goal， 或者自定义的goal。

对应maven插件中的声明的`execution`选项：

```xml
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>compile</goal>
                            <goal>compile-custom</goal>
                        </goals>
                    </execution>
                </executions>
```

例如此处的 `package`,  如果执行命令：`mvn package`,那么会执行之前所有的`clean compile test`,不会执行`install`下面的操作。

```java
@Mojo(
        name = "compile",
        defaultPhase = LifecyclePhase.GENERATE_SOURCES,
        requiresDependencyResolution = ResolutionScope.COMPILE,
        threadSafe = true
)
```

上面定义的插件的name就是对应的`goal`

## maven插件的开发和调试

此处假设我们**maven插件源码项目是A**， **使用插件的项目是B**，进行调试的步骤如下：

1. 首先在**项目B**中设置`mvndebug`进行调试监听操作：

```bash
# 该步骤必须操作将当前的工程包安装到本地仓库中，否则mvndebug会找不到包错误
$ mvn clean install -DskipTests
$ mvndebug plugin-groudid:plugin-artifactid:plugin-version:plugin-phase
# 例如： mvndebug  org.xolstice.maven.plugins:protobuf-maven-plugin:0.7.0-SNAPSHOT:compile
```

然后会打印如下类似信息：

```bash

pu@LM--24502820 karate-grpc-helper % mvndebug org.xolstice.maven.plugins:protobuf-maven-plugin:0.7.0-SNAPSHOT:compile
Preparing to execute Maven in debug mode
Listening for transport dt_socket at address: 8000

```

从上面可以看到对应的监听端口默认是：`8000`,后面插件工程A将会使用到这个端口号。

2. 回到**插件源码项目A**，在对应的phase的mojo代码中加入相关的断点，并在插件源码工程A中配置`java Remote debug`运行配置，
使用工具IDEA的时候只需要在JVM参数添加如下参数：

```bash
-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=8000
```

3. 然后就是等待项目B执行对应的maven操作，然后就会在插件源码项目A中看到源码会在对应的断点处暂停，此时就可以进行相关的debug操作了。

## maven仓库包发布配置

操作步骤参考： <https://www.cnblogs.com/exmyth/p/11567579.html>

按照上面的操作进入地址： <https://issues.sonatype.org/secure/CreateIssue.jspa?issuetype=21&pid=10134> 提交一个issue

参考一个发布github仓库到对应的oss nuxus仓库的代码：
http://bjansen.github.io/java/2021/02/03/deploying-to-maven-central-using-github-actions.html
