---
title: vue3系列(1)-vue3入门介绍
keywords: 'vue, vue3'
categories: [vue,vue3]
abbrlink: p3eRqr61UtB
date: 2021-04-18 23:16:38
description:
cover:
top_img:
---

## vu3入门介绍

Vue (读音 /vjuː/，类似于 view) 是一套用于构建用户界面的渐进式框架。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与现代化的工具链以及各种支持类库结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。


## vite的使用介绍

```
yarn create @vitejs/app

```
可能会出现错误: `文件名、目录名或卷标语法不正确。`,解决方法如下: 如何解决vite安装时报错:`文件名、目录名或卷标语法不正确。`



## 错误问题

### 如何解决vite安装时报错:`文件名、目录名或卷标语法不正确。`?

解决方法,重新设置yarn的相关配置路径: 
参考: <https://www.jianshu.com/p/576acc489293>

```shell
 
yarn config set prefix "E:\nodejs\node_global"
yarn config  set global-folder "E:\nodejs\node_global"
yarn config set cache-folder "E:\nodejs\node_cache"
yarn config set link-folder "E:\nodejs\node_link"

yarn create @vitejs/app my-vue-app --template vue

```

## 参考学习文档

[](https://www.vue3js.cn/docs/zh/)