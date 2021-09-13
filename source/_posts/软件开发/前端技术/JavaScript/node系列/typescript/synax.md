---
title: typescript的入门和学习
keywords: 'typescript, ts,javascript'
categories: [typescript]
abbrlink: p3eRqr6121B
date: 2021-09-08 23:16:38
description:
cover:
top_img:
---

## tsconfig.json文件的配置

## FAQ

### 1. uncaughtException: (0 , express_1.default) is not a function

修改`tsconfig.json`文件中的配置属性` "esModuleInterop": true`.

当我们想要将 CommonJS 模块导入 ES6 模块代码库时会出现问题。解释文档如下: https://stackoverflow.com/questions/56238356/understanding-esmoduleinterop-in-tsconfig-file

if `-esModuleInterop=false` flag,then should be` import * as moment from 'moment' `