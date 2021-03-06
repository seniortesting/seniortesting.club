---
title: hbuilderx工具真香定理
tags: []
keywords: ''
categories: []
abbrlink: dqrn4e6WLT
date: 2021-03-26 20:58:52
description:
cover:
top_img:
---



hbuilderx开发工具学习




## 不错的移动端滚动组件`mescroll`

- 官方文档： http://www.mescroll.com/index.html?v=190701
- vue组件地址: node_modules/mescroll.js/mescroll.vue


## 真香系列- HBuilderX入门

配置信息：

```json
{
    "editor.colorScheme" : "Default",
    "editor.saveOnFocusLost" : true,
    "files.autoSaveDelay" : 1,
    "node.path" : "E:/nodejs/node.exe",
    "npm.path" : "E:/nodejs/npm.cmd",
    "terminal.type" : "内置终端",
    "view.remoteDebug.openOnRunDevice" : true,
    "weApp.devTools.path" : "E:/Program Files/Tencent/微信web开发者工具",
    "files.associations.suffixs" : "md,json",
    "files.associations.contextmenu" : true,
    "editor.longLineIndicator" : true,
    "alipayApp.devTools.path" : "E:/Program Files/小程序开发者工具/小程序开发者工具.exe",
    "baiduApp.devTools.path" : "C:\\Users\\Walter\\AppData\\Local\\Programs\\swan-ide-gui\\百度开发者工具.exe",
    "bytedanceApp.devTools.path" : "C:\\Users\\Walter\\AppData\\Local\\Programs\\bytedanceide\\字节跳动开发者工具.exe"
}

```



## IOS开发发布

>  [参考文章](http://ask.dcloud.net.cn/article/152)
1. 在Mac上生成对应的`CertificateSigningRequest.certSigningRequest`文件，
2. 进入苹果开发者中心，生成对应的开发/生产 certification证书，里面会提示需要选择上面的证书请求文件。
3. 在Mac上下载上面生成的证书例如`development.cer`，双击该文件导入到Keychain Access；
4. 在证书列表中选择Export "Developer" ..，导出证书，其中会提示输入证书的密码和确认密码；
5. 保存开发(Production)证书(如“HBuilderCert.p12”)
6. 进入开发者中心，申请描述文件，下载保存开发描述文件（如HBuilderProfileDistribution.mobileprovision）
7. hbuilder生成的是打包的ipa文件


## vue注意事项

1. 建议使用 uni-app 的 onReady代替 vue 的 mounted。
2. 建议使用 uni-app 的 onLoad 代替 vue 的 created。



## truetype 字体

使用：  /* chrome, firefox, opera, Safari, Android, iOS 4.2+ */
TrueType是由AppleComputer公司和Microsoft公司联合提出的一种新型数学字形描述技术。它用数学函数描述字体轮廓外形，含有字形构造、颜色填充、数字描述函数、流程条件控制、栅格处理控制、附加提示控制等指令。TrueType采用几何学中二次B样条曲线及直线来描述字体的外形轮廓，其特点是：TrueType既可以作打印字体，又可以用作屏幕显示；由于它是由指令对字形进行描述，因此它与分辨率无关，输出时总是按照打印机的分辨率输出。无论放大或缩小，字符总是光滑的，不会有锯齿出现。但相对PostScript字体来说，其质量要差一些。特别是在文字太小时，就表现得不是很清楚。
TrueType字体的优势是什么？
答：TrueType字体具有如下优势：①真正的所见即所得字体。由于True-Type字体支持几乎所有输出设备，因而无论在屏幕、激光打印机、激光照排机上，还是在彩色喷墨打印机上，均能以设备的分辨率输出，因而输出很光滑。②支持字体嵌入技术。存盘时可将文件中使用的所有TrueType字体采用嵌入方式一并存入文件之中，使整个文件中所有字体可方便地传递到其它计算机中使用。嵌入技术可保证未安装相应字体的计算机能以原格式使用原字体打印。③操作系统的兼容性。MAC和PC机均支持TrueType字体，都可以在同名软件中直接打开应用文件而不需要替换字体。


其他字体： woff (Web Open Font Format，简称WOFF), 是一种网页所采用的字体格式标准.

字体介绍：https://www.cnblogs.com/sexintercourse/p/9479389.html

.eot，Embedded Open Type，主要用于早期版本的IE，是其专有格式，带有版权保护和压缩。
.ttf，TrueType，在操作系统里更为常见，在web上使用的话，是为了兼容早期仅支持TTF和OTF的浏览器。由于体积比较大，还需要服务器额外压缩。
.woff，Web Open Font Format，可以看作是ttf的再封装，加入了压缩和字体来源信息，通常比ttf小40%。也是当前web字体的主流格式。
.woff2，Web Open Font Format 2.0，相比woff最大的优化应该是加强了字体的压缩比。目前支持的浏览器只有正在互彪版本号的Chrome和Firefox。

woff和woff2的文件，woff2要小25%


> uniapp中不能使用多色图标，而且多色图标兼容性较差，浏览器渲染 SVG 的性能一般，还不如 png。所以我们这里推荐就使用的是ttf的图标，虽然是单色我们可以通过设置对应的背景色达到可以实现双色的效果。 iconfont的class引用图标其实就是采用的unicode的方式使用图标，只是语义化采用class来标记图标更简单了。 在设置对应的tabbar的text的时候还是需要使用unicode的方式。

使用方法：
1. 本地环境：
在iconfont中挑选好图标,切换到`unicode`,然后复制里面的所有内容:
```
@font-face {
  font-family: 'iconfont';  /* project id 1284327 */
  src: url('//at.alicdn.com/t/font_1284327_s5jrvqwkz1b.eot');
  src: url('//at.alicdn.com/t/font_1284327_s5jrvqwkz1b.eot?#iefix') format('embedded-opentype'),
  url('//at.alicdn.com/t/font_1284327_s5jrvqwkz1b.woff2') format('woff2'),
  url('//at.alicdn.com/t/font_1284327_s5jrvqwkz1b.woff') format('woff'),
  url('//at.alicdn.com/t/font_1284327_s5jrvqwkz1b.ttf') format('truetype'),
  url('//at.alicdn.com/t/font_1284327_s5jrvqwkz1b.svg#iconfont') format('svg');
}
```
将上面的所有加上https，如下：
```
@font-face {
  font-family: 'msharing-font';  /* 自定义，避免问题，project id 1284327 */
  src: url('https://at.alicdn.com/t/font_1284327_s5jrvqwkz1b.eot');
  src: url('https://at.alicdn.com/t/font_1284327_s5jrvqwkz1b.eot?#iefix') format('embedded-opentype'),
  url('https://at.alicdn.com/t/font_1284327_s5jrvqwkz1b.woff2') format('woff2'),
  url('https://at.alicdn.com/t/font_1284327_s5jrvqwkz1b.woff') format('woff'),
  url('https://at.alicdn.com/t/font_1284327_s5jrvqwkz1b.ttf') format('truetype'),
  url('https://at.alicdn.com/t/font_1284327_s5jrvqwkz1b.svg#iconfont') format('svg');
}
```
定义一个样式可以通过class的方式直接使用：
```
.iconfont {
    font-family: "msharing-font" !important;
    font-size: 24px;
	font-weight: normal;
	font-style: normal;
	line-height: 1;
	display: inline-block;
	text-decoration: none;
	-webkit-font-smoothing: antialiased;
}
```