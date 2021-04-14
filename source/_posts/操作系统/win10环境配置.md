---
title: Windows10机器新环境配置
---


## 软件列表

### 装机系统软件

* 激活工具
* [Chrome Canary](https://www.google.com/chrome/?extra=canarychannel&standalone=1)
   1. tampermonkey
      * ( 懒人专用，全网VIP视频免费破解去广告、全网音乐直接下载、百度网盘直接下载、知乎视频下载等多合一版。长期更新，放心使用。)
      * JAV老司机
   2. Free Download Manager
   3. Octotree
   4. Vue Devtools
   5. ChroPath
   6. 掘金
   7. 谷歌上网助手
   8. Wappalyzer
   9. Momentum

* [VPN客户端](https://www.shrew.net/download/vpn/vpn-client-2.2.2-release.exe)
* [WPS](https://www.wps.cn/)
* [OneNote](https://www.microsoft.com/en-us/p/onenote/9wzdncrfhvjl)
* [Firefox](https://www.mozilla.org/en-US/firefox/new/)

* [火绒杀毒](https://www.huorong.cn/person5.html)
* [Free Download Manager](https://www.freedownloadmanager.org/download.htm)
* [7Zip](https://www.7-zip.org/download.html)
* [Dism++](https://www.chuyu.me/)

## 开发工具

* [AdoptOpenJDK 11](https://adoptopenjdk.net/?variant=openjdk11&jvmVariant=hotspot)
* [Jetbrains IDEA](https://www.jetbrains.com/idea/download/)
  * 插件
    1. Alibaba Java Coding Guidelines
    2. Lombok
    3. Maven Helper
    4. Mybatis Log Plugin
    5. MybatisCodeHelperPro
    6. Python
    7. Vue.js
    8. Wake Time
    9. Any Rule

* [HBuilderX](https://dcloud.io/)
* [VS Code](https://code.visualstudio.com/download)

  * Markdown相关插件
     1.1 Markdown PDF
     1.2 Markdown Preview Enhanced
     1.3 Markdown Shortcuts
     1.4 markdownlint
     1.5 vscode-pdf
     1.6 PicGo （配置操作: <https://code.seniortesting.club/blog/setup/how-setup-picgo-vscode.html> )
     1.7 Visual Studio IntelliCode
     1.8 Python
     1.9 Impornt Cost
     1.10 Settings Sync, token: 88b53e726d32e7125a784d90a2ba0d2e73678164, gist: 9a957602da106a377142305bcb2f3e65
    1.11 Live Server
    1.12 Debugger for Chrome
    1.13 Live Sass Compiler
    1.14 Lorem ipsum
    1.15 CSS Peek
    1.16 IntelliSense for CSS class names in HTML
    1.17 [Markdown Table](https://marketplace.visualstudio.com/items?itemName=TakumiI.markdowntable)

* [Oracle VirtualBox](https://www.virtualbox.org/wiki/Downloads)
* [Node](https://nodejs.org/en/download/)
* [Python 3.8.2](https://www.python.org/ftp/python/3.8.2/)
* [Apache Tomcat9](http://tomcat.apache.org/)
* [Apache Maven](https://maven.apache.org/download.cgi)

```
 // user/.m2/settings.xml
  <localRepository>E:\MavenRepository</localRepository>
```

* [Gradle-Android开发](https://gradle.org/)
* [Fiddler](https://www.telerik.com/download/fiddler)
* [dbForge Studio for MySQL](https://www.devart.com/dbforge/mysql/studio/download.html)
* [Git](https://git-scm.com/download/win)
* [TortoiseGit](https://tortoisegit.org/download/)
* [Source Tree](https://www.sourcetreeapp.com/)
* [Xshell](https://www.netsarang.com/en/xshell-download/)
* [Redis Desktop Manager](http://docs.redisdesktop.com/en/latest/)
* [Adobe Photoshop CC 2018](https://www.adobe.com/products/photoshop/free-trial-download.html)
* [frp](https://github.com/fatedier/frp)
* [ngrok](https://ngrok.com/download)
* [微信开发者工具](https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html)
* [aliyun OSS Browser](https://github.com/aliyun/oss-browser)
* [Bootstrap Studio](https://bootstrapstudio.io/)
* [MongoDB](https://www.mongodb.com/download-center)
* [artipub-多平台文章发布](https://github.com/crawlab-team/artipub)
* [FastStoneCapturePortable](https://www.faststone.org/FSCaptureDetail.htm)
* [后裔采集器](http://www.houyicaiji.com/?type=download)
* [小飞兔整站下载](https://xft.fzxgj.top/)
* [Advanced IP Scanner](https://www.advanced-ip-scanner.com/index2.php)
* [RealVNC](https://www.realvnc.com/)
* [Win32DiskImager](https://sourceforge.net/projects/win32diskimager/)
* [PhpStudy](https://www.xp.cn/)
* [有道云笔记](http://m.note.youdao.com/)
* [应用宝乐固加固](https://cloud.tencent.com/product/ms)

### 娱乐工具

* [m3u8 downloader-youtube-dl.exe](https://github.com/ytdl-org/youtube-dl)
* [PotPlayer](https://daumpotplayer.com/download/)
* [百度网盘](https://pan.baidu.com/download)
* ~~[PanDownload](https://pandownload.com/)~~
* [QQ](https://im.qq.com/download/)
* [微信桌面版](https://pc.weixin.qq.com/)
* [人人影视](http://www.rrys2019.com/)
* [迅雷](https://www.xunlei.com/)
  [Google Earth](https://www.google.com/earth/versions/)

最新更新： 推荐直接使用 [PowerShell 7](https://github.com/PowerShell/PowerShell/releases)

## 下载安装

1. 官方提示需要先安装： [Desktop Bridge VC++ v14 Redistributable Package](https://www.microsoft.com/en-us/download/details.aspx?id=53175)
2. 在[microsoft/terminal](https://github.com/microsoft/terminal)仓库下载对应的terminal文件，打开`powershell`命令行执行命令如下安装:

```
> Add-AppxPackage .\Microsoft.WindowsTerminalPreview_1.3.2382.0_8wekyb3d8bbwe.msixbundle
```

## 配置使用

WT 好处都有啥？
根据官方介绍，Windows Terminal 是一个**面向命令行用户的全新、现代化、功能丰富的高性能终端应用程序**。它在实现了社区用户热切期望的许多功能的同时（包括多标签页、富文本、全球化、可配置性、对主题与样式的支持等），依然保持快速与高效，不会消耗大量的内存或电量。

安装完成后可以直接在开始菜单中找到，“Window Terminal Preview”.

1. 添加右键菜单

2020年0915日最新更新： 参考此脚本： <https://github.com/lextm/windowsterminal-shell>

不过我还是比较习惯传统的右键菜单「在这里打开终端」的方式。WT 目前还没有内置这一功能，想要手动添加也比较麻烦（下文参考了这个 [issue](https://github.com/microsoft/terminal/issues/1060)中的方法）。

以管理员权限打开 PowerShell，运行以下命令：

```
$basePath = "Registry::HKEY_CLASSES_ROOT\Directory\Background\shell"
New-Item -Path "$basePath\wt" -Force -Value "Windows Terminal here"
New-ItemProperty -Path "$basePath\wt" -Force -Name "Icon" -PropertyType ExpandString -Value "%LOCALAPPDATA%\Microsoft\WindowsApps\terminal.ico"
New-Item -Path "$basePath\wt\command" -Force -Type ExpandString -Value '"%LOCALAPPDATA%\Microsoft\WindowsApps\wt.exe" -p Ubuntu -d "%V"'

```

如果你足够熟练，也可以自行通过其他方式修改注册表，反正就那么些字段，路径正确就行了。Windows Terminal 的图标可以在 [这里](https://raw.githubusercontent.com/microsoft/terminal/master/res/terminal.ico) 获取 。

> 2020/03/14 更新：Windows Terminal 0.9 版本之后添加了 wt.exe 的命令行参数，可以直接指定启动目录，不需要再修改 profiles.json 中的 `startingDirectory` 字段了。

另外 wt.exe 支持通过` -p `参数指定要打开的 Profile，所以除了 WSL，我还添加了一个在当前目录下打开 PowerShell 的菜单项（注册表中添加一个 Extended 项可以让该右键菜单项仅在按住 Shift 右键时才显示）。你甚至可以通过二级菜单的方式实现更多功能，具体可以参考上面给出的 issue 中的讨论。
