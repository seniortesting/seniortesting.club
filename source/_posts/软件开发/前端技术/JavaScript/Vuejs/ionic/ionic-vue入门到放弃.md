---
title: 4月30日整理
---

## 学习Ionic Vue

## capacitor搭建及其踩坑

1. 在`package.json`中加入以下四个必须的依赖，我就是因为稍加了一个`@capacitor/cli`导致`app`模块中的`compileSdkVersion`是27，而其他的模块更新的确实28，注意！！！ 如下配置:

```json
    "@capacitor/android": "^1.0.0",
    "@capacitor/core": "^1.0.0",
    "@capacitor/cli": "^1.0.0",
    "@capacitor/ios": "^1.0.0",

```

2. 配置相应的gradle环境，例如环境变量GRADlE_HOME,GRADLE_USER_HOME，配置idea中的`service directory path`为自定义的gradle路径，配置`capacitor root path/android/app/gradle/wrapper/gradle-wrapper.properties`,设置里面的`distributionUrl=https\://services.gradle.org/distributions/gradle-5.4.1-all.zip` 为自己的设置的目录。

3. 直接编译报错`point to the same directory in the file system.Each module must have a unique path.` ，解决方法: 将项目android文件下的    ***.iml 文件删掉，重新导入编译即可

4. android sdk这里我们使用的`@capacitor/core`=1.0.0， 所以它支持的Androidsdk是28，所以我们记得配置Androidstudio 中sdk只有一个API 28版本的。

5. `npx cap sync`是用户安装了新的cordova插件后更新同步新的插件到工程里面。而`npx cap copy`主要就是每次的web工程build后将对应的dist目录复制到对应的assets目录下面。

6. `Android 9.0 WebView无法加载页面报错net：ERR_CLEARTEXT_NOT_PERMITTED`,从Android 9.0（API级别28）开始，默认情况下禁用明文支持。因此http的url均无法在webview中加载。

> 在`AndroidManifest.xml`文件中的`application`标签添加`android:usesCleartextTraffic="true"`

```
<?xml version="1.0" encoding="utf-8"?>
<manifest ...>
    <uses-permission android:name="android.permission.INTERNET" />
    <application
        ...
        android:usesCleartextTraffic="true"
        ...>
        ...
    </application>
</manifest>

```

7. ionic 切换页面时会添加`ion-page-invisible`,导致页面白屏,参考问题：

8. vue阻止冒泡到父级节点的事件 `@click.stop`：

```
            <div v-for="(image,index) in currentImages"
                 :key="image.src"  @click="previewImage(image, index)">
              <li class="weui-uploader__file"
                  :style="{ backgroundImage: `url(${image.src})`}"
                 >
                <ion-icon name="ios-close-circle" class="weui-close-icon" @click.stop="removeImage(image, index)"></ion-icon>
              </li>
            </div>
```

9. cordova phone call打电话代码: `location.href='tel:13052113519'`或者 `window.open('tel:13052113519')`

10. 离线存储解决方案: `localForage`

11. `promise`, `async`和`await`的讲解

参考： <https://www.cnblogs.com/CandyManPing/p/9384104.html>

1. async 告诉程序这是一个异步，awiat 会暂停执行async中的代码，等待await 表达式后面的结果，跳过async 函数，继续执行后面代码
2. async 函数会返回一个Promise 对象，那么当 async 函数返回一个值时，Promise 的 resolve 方法会负责传递这个值；当 async 函数抛出异常时，Promise 的 reject 方法也会传递这个异常值
3. await  操作符用于等待一个Promise 对象，并且返回 Promise 对象的处理结果（成功把resolve 函数参数作为await 表达式的值），如果等待的不是 Promise 对象，则用 Promise.resolve(xx) 转化

### 例子参考

1. <https://github.com/nklayman/vue-cli-plugin-capacitor/blob/master/index.js>
2. <https://github.com/pietrovieira/Vuejs-Ionic4-Ionic-Capacitor/blob/master/src/App.vue>
3. [sample app using capacitor vuejs and ionicv4 components](https://github.com/aaronksaunders/icon-vue/blob/master/src/components/Login.vue)
4. [Mobile app built with Vue.js, Ionic 4(beta), and wrapped by Capacitor](https://github.com/Balintataw/restaurant-mobile-app)

### 参考链接

- vue-cli-plugin-ionic [cli3-plugin-ionic](https://github.com/ionic-team/vue-cli-plugin-ionic)
- Vue start app [ionic-vue-conference-app](https://github.com/ionic-team/ionic-vue-conference-app/blob/master/src/views/Tabs.vue)
- Vue ionic author's example [beep](https://github.com/ModusCreateOrg/beep)
- 所有的demo代码：[官方网站demo](https://github.com/ionic-team/ionic-docs/blob/master/src/demos/api/item/index.html)
- Ionc start app [ionic-conference-app](https://github.com/ionic-team/ionic-conference-app/blob/master/src/app/pages/account/account.html)

### 集成步骤

1. 引入库：

```json
 "@ionic/core": "latest",
 "@ionic/vue": "^0.0.4",

```

2. 引入`@ionic/vue`相关组件：

```js
import Vue from 'vue'
import Ionic from '@ionic/vue'
// Ionic all bundle css styles
import '@ionic/core/css/ionic.bundle.css'
import '../assets/css/ionic-variables.css'
Vue.use(Ionic)

```

其中的`ionic-variables.css`为自定义主题样式,内容如下：

```css
/* Ionic Variables and Theming. For more info, please see: */
/* http://ionicframework.com/docs/theming/                 */

/** Ionic CSS Variables **/
:root {
    /** primary **/
    --ion-color-primary: #3880ff;
    --ion-color-primary-rgb: 56, 128, 255;
    --ion-color-primary-contrast: #ffffff;
    --ion-color-primary-contrast-rgb: 255, 255, 255;
    --ion-color-primary-shade: #3171e0;
    --ion-color-primary-tint: #4c8dff;

    /** secondary **/
    --ion-color-secondary: #0cd1e8;
    --ion-color-secondary-rgb: 12, 209, 232;
    --ion-color-secondary-contrast: #ffffff;
    --ion-color-secondary-contrast-rgb: 255, 255, 255;
    --ion-color-secondary-shade: #0bb8cc;
    --ion-color-secondary-tint: #24d6ea;

    /** tertiary **/
    --ion-color-tertiary: #7044ff;
    --ion-color-tertiary-rgb: 112, 68, 255;
    --ion-color-tertiary-contrast: #ffffff;
    --ion-color-tertiary-contrast-rgb: 255, 255, 255;
    --ion-color-tertiary-shade: #633ce0;
    --ion-color-tertiary-tint: #7e57ff;

    /** success **/
    --ion-color-success: #10dc60;
    --ion-color-success-rgb: 16, 220, 96;
    --ion-color-success-contrast: #ffffff;
    --ion-color-success-contrast-rgb: 255, 255, 255;
    --ion-color-success-shade: #0ec254;
    --ion-color-success-tint: #28e070;

    /** warning **/
    --ion-color-warning: #ffce00;
    --ion-color-warning-rgb: 255, 206, 0;
    --ion-color-warning-contrast: #ffffff;
    --ion-color-warning-contrast-rgb: 255, 255, 255;
    --ion-color-warning-shade: #e0b500;
    --ion-color-warning-tint: #ffd31a;

    /** danger **/
    --ion-color-danger: #f04141;
    --ion-color-danger-rgb: 245, 61, 61;
    --ion-color-danger-contrast: #ffffff;
    --ion-color-danger-contrast-rgb: 255, 255, 255;
    --ion-color-danger-shade: #d33939;
    --ion-color-danger-tint: #f25454;

    /** dark **/
    --ion-color-dark: #222428;
    --ion-color-dark-rgb: 34, 34, 34;
    --ion-color-dark-contrast: #ffffff;
    --ion-color-dark-contrast-rgb: 255, 255, 255;
    --ion-color-dark-shade: #1e2023;
    --ion-color-dark-tint: #383a3e;

    /** medium **/
    --ion-color-medium: #989aa2;
    --ion-color-medium-rgb: 152, 154, 162;
    --ion-color-medium-contrast: #ffffff;
    --ion-color-medium-contrast-rgb: 255, 255, 255;
    --ion-color-medium-shade: #86888f;
    --ion-color-medium-tint: #a2a4ab;

    /** light **/
    --ion-color-light: #f4f5f8;
    --ion-color-light-rgb: 244, 244, 244;
    --ion-color-light-contrast: #000000;
    --ion-color-light-contrast-rgb: 0, 0, 0;
    --ion-color-light-shade: #d7d8da;
    --ion-color-light-tint: #f5f6f9;
}

```

3. 修改`App.vue`文件，使得`ion-app`为顶级渲染节点，可以识别不同的设备，从而加载不同的主题样式:

```vue
<template>
  <ion-app>
    <ion-vue-router />
  </ion-app>
</template>

<script>

export default {
  name: 'App',
  methods: {
  }
}
</script>
<style>
</style>

```

4. 路由设置,修改路径为`@ionic/vue`中定制的路由，这个路由跟vue-router是一样的，但是功能可能更多：

```js
import Vue from 'vue'
import { IonicVueRouter } from '@ionic/vue'
import routes from './routes'

Vue.use(IonicVueRouter)

const router = new IonicVueRouter({
  mode: 'history',
  base: process.env.BASE_URL,
  routes: routes
})

export default router


```

## 坑/问题

- 在查看`ion-tabs`时发现用到了**命名视图**，这个确实很坑啊，以前都一直都用到的是通过**命名路由**的方式进行导航的.
认真阅读官方文档：[命名视图](https://router.vuejs.org/zh/guide/essentials/named-views.html)

- `<ion-input>`不能使用`v-model`,两种方式解决：

  - 第一种如下的语法糖代码调整：

  ```
  <ion-input
  :value="selectedOption"
    @ionChange="selectedOption= $event.target.value"
    >
  ```

  - vuejs官方提出了这个问题没有解决，web component不支持，参考[ionic 官方issue](https://github.com/ionic-team/ionic/issues/15532)
  和对应的[vuejs官方issue](https://github.com/vuejs/vue/issues/7830)
  对应的需要提到的[问题](https://github.com/vuejs/rfcs/blob/v-model/active-rfcs/0000-v-model-api-change.md#usage-on-custom-elements)

- `type=number`在`vee-validate`中不起作用，使用了`v-validate="{digits: 4}"`,原因是:
  
  - vee-validate作者提到问题： [github issue](https://github.com/baianat/vee-validate/issues/2043):

  > This is caused by vee-validate trying to validate the field based on their HTML attributes, for `number` fields the decimal rule is automatically added.
     You can turn that behavior off like this:
      ```
      Vue.use(VeeValidate, {
        useConstraintAttrs: false
      });
      ```
The problem is that decimal and integer are conflicting rules by definition, so it is advised not to use both at the same time. So Turning the behavior off is the easiest solution for you.

  然后看到官方文档提到，有些html5的内置类型和属性，是不需要在添加`v-validate`进行详细的验证的，只需要添加一个`v-validate`就可以了，参考：[官方指南](https://baianat.github.io/vee-validate/guide/inferred-rules.html#inferred-rules-reference):

## Inferred Rules Reference

This is a table of HTML attributes that is inferred as rules.

| Attribute |   value          | Rule                                                                      |
|-----------|:----------------:|---------------------------------------------------------------------------|
| type      | "email"          |  `email`                                                                  |
| type      | "number"         | `decimal`                                                                 |
| type      | "date"           | `date_format:YYYY-MM-DD`                                                  |
| type      | "datetime-local" | `date_format: YYYY-MM-DDThh:mm`                                           |
| type      | "time"           | `date_format:hh:mm` or `date_format:hh:mm:ss` depending on the step value |
| type      | "week"           | `date_format:YYYY-Www`                                                    |
| type      | "month           | `date_format:YYYY-MM`                                                     |
| min       | val              | `min_value:val`                                                           |
| max       | val              | `max_value:val`                                                           |
| pattern   | rgx              | `regex: rgx`                                                              |
| required  | _none_           | `required`                                                                |
| maxlength | "val"            | `max: val`                                                                |
| minlength | "val"            | `min: val`                                                                |

:::tip
  This feature does not work on custom components, only HTML5 inputs can take advantage from this feature.
  所以还是采用作者的提议，因为我们使用的是`ionic web component`, 所以上面的规则还是不适用
:::

- 同一个页面多表单的校验规则: [multiple form](https://baianat.github.io/vee-validate/examples/scopes.html) ，

> For convenience, you may add the data-vv-scope attribute on the form that owns the inputs, you don't have to add the attribute on every input. You can also pass scope property to the validator expression.  不必每个字段都添加一个scope的属性，这个问题在旧版本中还是需要加上scope的，见问题： [
How to validate two different forms on one page? #1206](https://github.com/baianat/vee-validate/issues/1206)

- ionic 中的`color`自定义： <https://ionicframework.com/docs/theming/advanced#colors>

## ionic常用css工具集

 [参考官方css工具集](https://ionicframework.com/docs/layout/css-utilities)

- 内间距

1. 子元素上下左右间距 padding
1. 子元素无间距 no-padding
2. 子元素上下间距 padding-vertical
3. 子元素左右间距 padding-horizontal

- 外间距

1. 与外元素间距16px margin
2. 与外元素无间距  no-margin
3. 上下元素间距16px margin-vertical
4. 左右元素间距16px margin-horizontal

- 行元素排列顺序 div包裹元素

1. text-left
2. text-right
3. text-start
4. text-end
5. text-center
6. text-justify
7. text-wrap
8. text-nowrap
9. text-uppercase
10. text-lowercase
11. text-capitalize

```
    <ion-col>
      <div class="ion-text-nowrap">
        <h3>text-nowrap</h3>
        Lorem ipsum dolor sit amet, consectetur adipiscing elit.
      </div>
    </ion-col>
```

- 边角间距

1. no-border

- flex布局

## ionic的card组件样式

默认的card的周围有灰色的阴影，采用如下样式将对应的灰色去掉：

```
.card {
  /*border-radius:10px;*/
  /*box-shadow: 1px 8px 11px rgba(131, 131, 131, 0.25), 0 8px 8px rgba(124, 124, 124, 0.22);*/
}

.card, .list-inset {
  overflow: hidden;
  margin: 20px 10px;
  border-radius: 2px;
  background-color: #fff;
}
/** 去掉周围阴影**/
.card {
  padding-top: 1px;
  padding-bottom: 1px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.3);
  /*box-shadow: none !important;*/
  border: none !important;
  border-style: none !important;
}

.card .item {
  border-left: 0;
  border-right: 0;
}

.card .item:first-child {
  border-top: 0;
}

.card .item:last-child {
  border-bottom: 0;
}

.padding .card, .padding .list-inset {
  margin-left: 0;
  margin-right: 0;
}

.card .item:first-child, .list-inset .item:first-child, .padding > .list .item:first-child {
  border-top-left-radius: 2px;
  border-top-right-radius: 2px;
}

.card .item:first-child .item-content, .list-inset .item:first-child .item-content, .padding > .list .item:first-child .item-content {
  border-top-left-radius: 2px;
  border-top-right-radius: 2px;
}

.card .item:last-child, .list-inset .item:last-child, .padding > .list .item:last-child {
  border-bottom-right-radius: 2px;
  border-bottom-left-radius: 2px;
}

.card .item:last-child .item-content, .list-inset .item:last-child .item-content, .padding > .list .item:last-child .item-content {
  border-bottom-right-radius: 2px;
  border-bottom-left-radius: 2px;
}

.card .item:last-child, .list-inset .item:last-child {
  margin-bottom: -1px;
}

.card .item, .list-inset .item, .padding > .list .item, .padding-horizontal > .list .item {
  margin-right: 0;
  margin-left: 0;
}

.card .item.item-input input, .list-inset .item.item-input input, .padding > .list .item.item-input input, .padding-horizontal > .list .item.item-input input {
  padding-right: 44px;
}

.padding-left > .list .item {
  margin-left: 0;
}

.padding-right > .list .item {
  margin-right: 0;
}

```
