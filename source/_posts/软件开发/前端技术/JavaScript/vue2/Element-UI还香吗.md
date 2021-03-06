---
title:  Element-UI还香吗，是否真的已死？
keywords: ''
categories: []
abbrlink: GM88B1kH7H
date: 2021-03-25 23:16:38
description:
cover:
top_img:
---


## 前言

Element-Ul是国内饿了么前端团队推出的一款基于Vue.js 2.0 的桌面端UI框架，一套为开发者、设计师和产品经理准备的基于 Vue 2.0 的桌面端组件库，他们也推出了对应的手机端框架Mint UI （已经早早的停止维护了，如果感兴趣看看隔壁的Vant框架）

GitHub代码仓库地址：[https://github.com/ElemeFE/element](https://github.com/ElemeFE/element)
官方框架学习帮助文档：[http://element-cn.eleme.io/#/zh-CN](http://element-cn.eleme.io/#/zh-CN)

 ![](http://p3-tt.byteimg.com/large/pgc-image/8c3979ca0f4143c0ba3c7f4aa610a0bf?from=pc)

## Element-UI到底有多火？

可以说这是目**前Vue生态圈最火的桌面UI组件库**，没有之一。基本你使用Vue没有不知道这个组件库的。
![](http://p1-tt.byteimg.com/large/pgc-image/622c5c2d0eb64c4a849d77b078faf4cc?from=pc)

别跟我说Ant Design和iView什么的？前者是相对于React生态圈的，而Vue版本的Ant Design Vue一直都是唐金州个人在主要维护，加上一些社区的中国开发者在维护。你真的不敢保证这个也会是个为了KPI而开源的项目，而且也有网友反应Ant Design Vue代码仓库中有Element代码抄袭的影子，作者反应是为了保证接口跟Element的一致性，这是欲盖弥彰，还是实锤抄袭？而对于后者iView则直接把Element代码拿过来复制黏贴，莫名投来一个鄙视的表情包~~~
![](http://p6-tt.byteimg.com/large/pgc-image/7b50ecff6ed9476785148e114c179641?from=pc)

其实在Vue刚出来不久前，尤雨溪（Vuejs的创建者）也很大推荐了这套UI框架。Element的视觉设计更符合国人的观赏体验，不同于一直不温不火的国外Material Design(vue生态中代表框架是：**Vuetify**，**Quasar**), 这个是谷歌一直推了好多年的UI设计标准，现在几乎所有的谷歌产品都迁移到Material Desgin的风格，包括官网。
![](http://p6-tt.byteimg.com/large/pgc-image/204549db770f455a8cb8c2619af80569?from=pc)
之前我也陆陆续续使用Vuetify和Quasar Framework制作一些个人网站的页面，领导或产品经理对于移动端的部分没什么意见，主要是Android界面已经被谷歌设计的基于Material Design风格的了，所以大家也还算能接受。但在桌面端网页上使用Material Design 的风格，在视觉习惯上国内基本都不太能接受，这怕是国内普遍的情况。其实要说质量、更新频率和文档完整程度，上述的两个国外UI库都要略优于国内的库，但在国内普及不开来，也是无奈！

![](http://p1-tt.byteimg.com/large/pgc-image/3baf4f2bc99f402ea39615c5a6f1bc5a?from=pc)

而对于Element的界面设计标准，他的细节设计则更能打动国人。看看这个全世界范围内几大Vue框架的对比，你就知道Element的普及率和使用率了：

![](http://p3-tt.byteimg.com/large/dfic-imagehandler/2fdde97b-1e66-449a-8780-bf54d5c1d1cc?from=pc)
element大约在去年年初开始下滑，在此之前的使用率一直碾压其他主流框架

![](http://p1-tt.byteimg.com/large/dfic-imagehandler/83d7c469-32dc-47ef-ab06-43e8a2da01dd?from=pc)
再看看这star数，还是蛮多的，毕竟很大一部分也是国人在使用

其实判断一个框架的好坏主要看你配置的生态和开发团队实力。就像这两年嚷嚷着的华为的鸿蒙操作系统，没有对应的生态谈何去对抗安卓和苹果？而反观我们的Element在国内使用的普及率，覆盖率，**认知度是相当高的**，生态已经基本全覆盖。例如很多在Element上进行二次开发的框架，比如最有名的一些Element上层生态产品：

* Avuejs: [https://avuejs.com/](https://avuejs.com/)
* Vue Admin Beautiful: [https://github.com/chuzhixin/vue-admin-beautiful](https://github.com/chuzhixin/vue-admin-beautiful)
* PanJiaChen/vue-element-admin: [https://github.com/PanJiaChen/vue-element-admin](https://github.com/PanJiaChen/vue-element-admin)
* Vue Form Generator: [https://github.com/JakHuang/form-generator](https://github.com/JakHuang/form-generator)
* RuoYi: [https://gitee.com/sushengbuyu/RuoYi](https://gitee.com/sushengbuyu/RuoYi)
* JEECG开源社区/jeecg-boot: [https://gitee.com/jeecg/jeecg-boot](https://gitee.com/jeecg/jeecg-boot)

还有其他更多实际的运作中的项目,这里就不一一赘述了。

另外Element 也提供了对**Sketch **和 **Axure **等原型工具的支持。对设计人员，产品经理快速设计网页很友好，像国内的优秀原型设计工具墨刀，Mockplus等也都同步封装了大量Element的界面组件。这些都进一步的降低了Element的开发封装成本。构建了Element强大的生态。

可以说这是**国内目前唯一一个真正推向国际的Vue生态UI框架**。就像国内科技公司一直在做种种尝试突破国外市场，尝试打破各种国外垄断，但是真正打入国外市场的科技公司这些年却也只有抖音（国外版TikTok)。

![](http://p1-tt.byteimg.com/large/pgc-image/d47ff61cb04e4cc7aea0fec1670b5348?from=pc)

如果以此类比Vue的生态圈，那么Element无疑就是那个最耀眼的TikTok。当然国内也有其他一些框架在前赴后继的维护和更新，可最后也只在国内大放异彩，国外使用度仍屈指可数！

## 当前仓库状态

是的，Element确实有很多先发的优势，随着它的发展历程，也在逐步扩大相关的生态，版本更新迭代也是很频繁。可是大约从2019年9月份左右Element 的代码提交开始放缓，基本停滞了，最近的一次提交是在2020年5月份的更新，也就是更新了下版本号和微小改动。

![](http://p6-tt.byteimg.com/large/pgc-image/983571198e834fbcb4389bf2b2a853b0?from=pc)
这可真是快一年代码基本没有更新了

代码仓库提交量最多的两个大佬也已经按兵不动了。。。

![](http://p1-tt.byteimg.com/large/pgc-image/b9973f694bbe4243a1cf071a3266a1ab?from=pc)
据说两个大佬Leopoldthecoder和QingWei-Li已经跳槽到了石墨

![](http://p3-tt.byteimg.com/large/pgc-image/ef636acaa3f6444492bcc0cb6fe1b4d4?from=pc)
突然发现仓库以前的几个维护人员已经没有了

## 收购+离职风起云涌

大家都知道阿里已经收购了饿了么，难道真的是 阿里收购饿了么，要干掉Element扶植自己的亲儿子Ant Design吗？**饿了么被阿里收购后原团队已经被肢解？？？**

要知道我也是一名忠实且重度使用Element的用户，看到最近一年Element的更新状态很是忧伤和焦虑哎！

![](http://p3-tt.byteimg.com/large/pgc-image/9eec02461edc46a28b4a4db419bd8415?from=pc)
网友也开始急了，这么大的项目

![](http://p3-tt.byteimg.com/large/dfic-imagehandler/c394e2a3-5994-4613-a5ac-7016b86385ce?from=pc)
一颗受伤的小心脏啊

带着满脸的惊叹号，我开始搜寻Element目前到底什么情况了？为什么好好的框架不维护了呢？

![](http://p3-tt.byteimg.com/large/pgc-image/b17ab84b0d5045debe608435136587ef?from=pc)
一开始有人反映这是个KPI项目，起初饿了么内部团队做的时候确实没有想到发展这么好。但是后来的发展势头确实已经超出了他们的预期。。。现在加上收购后并入阿里，自然一山不容二虎。。。

![](http://p3-tt.byteimg.com/large/pgc-image/13f59bd66b63444c998f0399da88b1cb?from=pc)
大部分ant-design-vue代码是直接从element改过去的

但后来有相关知情人透露并没有所谓的并入，而且据说Ant Desgin其核心开发人员也就才五六个人，也不是全职在做。所以并不存在谁轻谁重问题。**但是饿了么公司是否重新维护这个项目，那真的是决策的问题。**

![](http://p6-tt.byteimg.com/large/pgc-image/1e1dbc2853df4a0bb9efb45b72c5a50f?from=pc)
现在饿了么前端核心维护人员变动几乎是肯定的，据听说几个大佬纷纷跳槽离开饿了么，有的到了字节跳动，有的到了石墨。。。但从commit历史来看也不是第一次这样了，至于后续动态真的不敢妄加猜测

这里还有一群Element的忠实粉丝在角落里瑟瑟发抖。。。

![](http://p3-tt.byteimg.com/large/pgc-image/6e794b8b8fb54e92b03fbeb0d0183e0c?from=pc)
相对于隔壁Reat生态最强框架，element瑟瑟发抖

![](http://p6-tt.byteimg.com/large/pgc-image/6382f9bc7409455b9735c698f9a64b44?from=pc)
vue-element-admin作者表示很受伤

所以有人提议捐钱帮助Element发展，毕竟是个开源项目，没点钱怎么坚持下去？安排。。。

![](http://p1-tt.byteimg.com/large/pgc-image/d6978f60ca0340b2b70cc8fd86bf7ca6?from=pc)
网友群献策支持element

可惜Element现在状态真的让你爱莫能助，连捐款的通道它都关闭了！

![](http://p1-tt.byteimg.com/large/pgc-image/a32eab3a93544de294975eb47c6d9c42?from=pc)
可惜的是element已经关闭了所有的捐钱通道，爱莫能助

![](http://p6-tt.byteimg.com/large/pgc-image/d6d5684533684e2b82e47f2fc5a91f09?from=pc)

峰回路转，就在我快要绝望的时候，又有一位前Element的维护大佬说到**Element将来不会停止维护**。

> “还在维护，踩一下说“KPI 项目，积重难返”的童鞋，即使它是KPI项目，也远远远远超出了当时定立KPI的期望，何况不是 ”

![](http://p6-tt.byteimg.com/large/pgc-image/c1739631afc041189012858dd629f063?from=pc)
大佬出来声明element接下来状态

![](http://p6-tt.byteimg.com/large/pgc-image/07388536c236439bac45c47353a52b77?from=pc)
即使是KPI项目，我们也爱你

Element团队真的要上点心了，如果今年继续这样半死不活，只会失去更多的用户，让大家更寒心。**难道国内的开源都是真的面向KPI开源吗？**

趁着Element半死不活的, 对面的**iView**和**Vuetify**也已经开始蠢蠢欲动，一波波广告好不热闹。。。

![](http://p1-tt.byteimg.com/large/pgc-image/6c0cfa9a87594dcfbe5e929e60961fa4?from=pc)
iview也来打个广告吗

![](http://p6-tt.byteimg.com/large/pgc-image/741de109734141e78bc2e084bcec2c37?from=pc)
对面的vuetify也来凑热闹，无情嘲讽

![](http://p1-tt.byteimg.com/large/pgc-image/134ef10bbc764728b91aa0e87c5387e3?from=pc)

## 何不换个框架？

说到这里，你可能会反问为什么不换个框架呢，市场面毕竟还有那么多框架可以选择？干嘛一棵树上吊死！

其实我也想换个框架，无奈可选的空间太小，就个人使用体验来说，Element还是感觉最上手，是我最喜欢的UI框架。这可不是我一个人有这样的感觉。。。。看看下面网友对Element的一众打CALL

这里主要针对的是Ant Design，毕竟在国内市场这两个是平级关系，仅作参考！

> Ant Design Vue没有 element 舒服，element ui算是彻底贯彻了vue的思想，优先用template，但是antd vue，iview之类的，很多地方都在用render函数，本质上就是想用jsx。本身vue易用就易用在这个template上，element ui确实提炼出一套基于template做到直观、易用的方法，因此吸引了很大一批人。但是讲到可定制化，就远不如jsx了。个人还是比较喜欢template和代码分离，看起来清晰一点。

> antd-vue总觉得还是react那味。搞得太复杂，导致使用上收起来不是很快，而且问题也不少。而element即使不维护也基本没有严重的bug存在。

![](http://p6-tt.byteimg.com/large/pgc-image/2ab2772da8824397b95d04d7b92a67bc?from=pc)
Element接口封装的确实很干净

![](http://p6-tt.byteimg.com/large/pgc-image/bc84f7408dd14ebe85ab0a1890616e69?from=pc)
打动网友的Element框架

其实上面也提到了，Ant Design Vue的接口设计也在慢慢靠拢Element，借鉴它的设计，一来方便使用者可以快速上手Ant Design,另外也省的再造轮子。

互联网的技术总是在更新换代，我们无法保证自己熟悉的一个框架技术可以永葆青春，谁都有谢幕的那一天！如果真到了Element要谢幕的那一天，我们也只能无奈欢送！

## 接下来我们怎么办？

说了这么多Element的前途叵测，Element项目未来也不明朗，那我们这些伸手党能做些什么呢？我这里可以给大家一些建议。

- **Element至于凉不凉主要看Vue3出来后它的动作**，目前的Element代码库支持Vue2.0绰绰有余，平时的开发工作完全可以应付，代码致命性的错误基本为零。毕竟经历了多年的洗礼和打磨，已经很成熟了。况且虽然现在的Element停止了新功能的开发工作，但是修复补丁工作还在继续，每天仍然还有大量的开发者参与进来修复网友反馈的问题。但是修复的问题现在不会merge和发布到新版。WTF 你只能静待Element的回归了。。。
![](http://p3-tt.byteimg.com/large/pgc-image/1bea567925fd468792f443b2fb6c3215?from=pc)
虽然代码停止更新，但是版本的修复工作还是有在正常进行

- 如果我们还是离不开Element,还是对它情怀满满，你不妨自己尝试着将代码fork一份，自己在代码基础上造轮子，修修补补，岂不乐哉！
![](http://p1-tt.byteimg.com/large/pgc-image/3bb59f6840ef4d5a8a5e5d3eb4d754be?from=pc)

- 其实上面也提到了Element生态很火，所以即使出现最糟的情况，我们还有一堆的第三方依赖库和网友定制版可以替代，目前社区出现了好些个人修改版的Element，也有的在做vue3.0 的兼容，但个人感觉不是很乐观，持续维护一个组件库的成本是非常高的，人力和精力的投入都没法计量。不管怎样，这也侧面说明你的选型是对的，选择Element是正确的。Element的生态如此强大，你也只需要做些前人栽树后人乘凉的事。
![](http://p3-tt.byteimg.com/large/pgc-image/3c4f8ec4ce42419b9eb8bd2f4f468b10?from=pc)
最后真心希望接下来的日子里，我们的Element可以度过难关，继续蓬勃发展！

![](http://p1-tt.byteimg.com/large/pgc-image/b21bc3f63a3d41ea989a049602abc8e0?from=pc)
爱你喔，Element

![](http://p3-tt.byteimg.com/large/pgc-image/bad89231d22846a2ba7d3f8d2ffe927f?from=pc)
再爱！

![](http://p6-tt.byteimg.com/large/pgc-image/1bb0cbe335214ea4b16fb098d47eb70f?from=pc)
三连击爱！


### 附录几个现在活跃维护定制版的Element-UI参考

* 网友版（这是针对vue3的版本）： [https://github.com/a631807682/ele-next](https://github.com/a631807682/ele-next)
* 算是官方版（据说这是饿了么内部发行版会支持vue3）： 

   - [ https://github.com/EOITek/element/commits/dev]( https://github.com/EOITek/element/commits/dev)
   - [https://www.npmjs.com/package/element-ui-eoi?activeTab=versions](https://www.npmjs.com/package/element-ui-eoi?activeTab=versions)

* 网友版think-vuele(主要做了增强和修复）： [https://github.com/chfree/think-vuele](https://github.com/chfree/think-vuele)

