---
title: gradle工具整理
tags: []
keywords: ''
categories: []
abbrlink: kQQ2Y4m9In
date: 2021-03-26 20:53:09
description:
cover: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
top_img: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
---



gradle包管理工具

## gradle 离线下载

gradle工程没有会找文件 gradle/wrapper/gradle-wrapper.properties 里面的相关配置，下载对应的gradle包从如下配置：
`distributionUrl=https\://services.gradle.org/distributions/gradle-5.4.1-all.zip`, 所以每个gradle工程记得配置这个参数。
一次下载后后面就不会再下载了。记得配置`GRADLE_USER_HOME`环境变量。

### com.android.builder.internal.aapt.v2.Aapt2Exception: Android resource linking failed

1. 在Android studio中打开toggle view进行查看详细的信息发现如下：

```
> Task :capacitor-android:compileDebugJavaWithJavac FAILED
D:\GitRepository\yitieyilu.com\yanzhi-web\material-sharing\node_modules\@capacitor\android\capacitor\src\main\java\com\getcapacitor\AndroidProtocolHandler.java:56: 错误: -source 1.6 中不支持 multi-catch 语句
    } catch (ClassNotFoundException | IllegalAccessException | NoSuchFieldException e) {
                                    ^
  (请使用 -source 7 或更高版本以启用 multi-catch 语句)
D:\GitRepository\yitieyilu.com\yanzhi-web\material-sharing\node_modules\@capacitor\android\capacitor\src\main\java\com\getcapacitor\Bridge.java:117: 错误: -source 1.6 中不支持 diamond 运算符
  private Map<String, PluginHandle> plugins = new HashMap<>();
                                                          ^
  (请使用 -source 7 或更高版本以启用 diamond 运算符)
D:\GitRepository\yitieyilu.com\yanzhi-web\material-sharing\node_modules\@capacitor\android\capacitor\src\main\java\com\getcapacitor\Bridge.java:461: 错误: -source 1.6 中不支持 multi-catch 语句
          } catch(PluginLoadException | InvalidPluginMethodException | PluginInvocationException ex) {
                                      ^
  (请使用 -source 7 或更高版本以启用 multi-catch 语句)
D:\GitRepository\yitieyilu.com\yanzhi-web\material-sharing\node_modules\@capacitor\android\capacitor\src\main\java\com\getcapacitor\BridgeActivity.java:39: 错误: -source 1.6 中不支持 diamond 运算符
  private List<Class<? extends Plugin>> initialPlugins = new ArrayList<>();
                                                                       ^
  (请使用 -source 7 或更高版本以启用 diamond 运算符)
D:\GitRepository\yitieyilu.com\yanzhi-web\material-sharing\node_modules\@capacitor\android\capacitor\src\main\java\com\getcapacitor\JSArray.java:21: 错误: -source 1.6 中不支持 diamond 运算符
    List<E> items = new ArrayList<>();
                                  ^
  (请使用 -source 7 或更高版本以启用 diamond 运算符)
D:\GitRepository\yitieyilu.com\yanzhi-web\material-sharing\node_modules\@capacitor\android\capacitor\src\main\java\com\getcapacitor\JSObject.java:34: 错误: -source 1.6 中不支持 diamond 运算符
    List<String> keys = new ArrayList<>();
                                      ^
  (请使用 -source 7 或更高版本以启用 diamond 运算符)
D:\GitRepository\yitieyilu.com\yanzhi-web\material-sharing\node_modules\@capacitor\android\capacitor\src\main\java\com\getcapacitor\plugin\Filesystem.java:264: 错误: -source 1.6 中不支持 try-with-resources
      try (BufferedWriter writer = new BufferedWriter(new OutputStreamWriter(
          ^
  (请使用 -source 7 或更高版本以启用 try-with-resources)
D:\GitRepository\yitieyilu.com\yanzhi-web\material-sharing\node_modules\@capacitor\android\capacitor\src\main\java\com\getcapacitor\plugin\Geolocation.java:40: 错误: -source 1.6 中不支持 diamond 运算符
  Map<String, PluginCall> watchingCalls = new HashMap<>();
                                                      ^
  (请使用 -source 7 或更高版本以启用 diamond 运算符)
D:\GitRepository\yitieyilu.com\yanzhi-web\material-sharing\node_modules\@capacitor\android\capacitor\src\main\java\com\getcapacitor\plugin\notification\LocalNotification.java:110: 错误: -source 1.6 中不支持 diamond 运算符
    List<LocalNotification> resultLocalNotifications = new ArrayList<>(notificationArray.length());
                                                                     ^
  (请使用 -source 7 或更高版本以启用 diamond 运算符)
D:\GitRepository\yitieyilu.com\yanzhi-web\material-sharing\node_modules\@capacitor\android\capacitor\src\main\java\com\getcapacitor\plugin\notification\LocalNotificationAttachment.java:42: 错误: -source 1.6 中不支持 diamond 运算符
    List<LocalNotificationAttachment> attachmentsList = new ArrayList<>();
                                                                      ^
  (请使用 -source 7 或更高版本以启用 diamond 运算符)
D:\GitRepository\yitieyilu.com\yanzhi-web\material-sharing\node_modules\@capacitor\android\capacitor\src\main\java\com\getcapacitor\plugin\notification\NotificationAction.java:37: 错误: -source 1.6 中不支持 diamond 运算符
    Map<String, NotificationAction[]> actionTypeMap = new HashMap<>();
                                                                  ^
  (请使用 -source 7 或更高版本以启用 diamond 运算符)
D:\GitRepository\yitieyilu.com\yanzhi-web\material-sharing\node_modules\@capacitor\android\capacitor\src\main\java\com\getcapacitor\plugin\notification\NotificationStorage.java:49: 错误: -source 1.6 中不支持 diamond 运算符
      return new ArrayList<>(all.keySet());
                           ^
  (请使用 -source 7 或更高版本以启用 diamond 运算符)
D:\GitRepository\yitieyilu.com\yanzhi-web\material-sharing\node_modules\@capacitor\android\capacitor\src\main\java\com\getcapacitor\Plugin.java:53: 错误: -source 1.6 中不支持 diamond 运算符
    eventListeners = new HashMap<>();
                                 ^
  (请使用 -source 7 或更高版本以启用 diamond 运算符)
D:\GitRepository\yitieyilu.com\yanzhi-web\material-sharing\node_modules\@capacitor\android\capacitor\src\main\java\com\getcapacitor\PluginCall.java:234: 错误: -source 1.6 中不支持 diamond 运算符
        List<Object> items = new ArrayList<>();
                                           ^
  (请使用 -source 7 或更高版本以启用 diamond 运算符)
D:\GitRepository\yitieyilu.com\yanzhi-web\material-sharing\node_modules\@capacitor\android\capacitor\src\main\java\com\getcapacitor\PluginHandle.java:17: 错误: -source 1.6 中不支持 diamond 运算符
  private Map<String, PluginMethodHandle> pluginMethods = new HashMap<>();
                                                                      ^
  (请使用 -source 7 或更高版本以启用 diamond 运算符)
D:\GitRepository\yitieyilu.com\yanzhi-web\material-sharing\node_modules\@capacitor\android\capacitor\src\main\java\com\getcapacitor\PluginHandle.java:74: 错误: -source 1.6 中不支持 multi-catch 语句
    } catch(InstantiationException | IllegalAccessException ex) {
                                   ^
  (请使用 -source 7 或更高版本以启用 multi-catch 语句)
D:\GitRepository\yitieyilu.com\yanzhi-web\material-sharing\node_modules\@capacitor\android\capacitor\src\main\java\com\getcapacitor\util\HostMask.java:87: 错误: -source 1.6 中不支持 diamond 运算符
            List<HostMask.Simple> masks = new ArrayList<>();
                                                        ^
  (请使用 -source 7 或更高版本以启用 diamond 运算符)
D:\GitRepository\yitieyilu.com\yanzhi-web\material-sharing\node_modules\@capacitor\android\capacitor\src\main\java\com\getcapacitor\WebViewLocalServer.java:96: 错误: -source 1.6 中不支持 diamond 运算符
        tempResponseHeaders = new HashMap<>();
                                          ^
  (请使用 -source 7 或更高版本以启用 diamond 运算符)
18 个错误


```

问题原因，没有正确配置gradle机器对应的Android sdk版本。
配置gradle环境变量：

- GRADLE_HOME =

> gradle会下载相关需要依赖的jar包，默认的本地存放地址是：C:/Users/(用户名)/.gradle/caches/modules-2/files-2.1

- GRADEL_USER_HOME = E:\GradleRepository (但是对于IDEA来说木有用（当然上面的环境变量还是要添加的），在IDEA中使用gradle需要修改Gradle的路径: Service Directory Path)
