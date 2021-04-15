---
title: autojs常用脚本片段整理
tags: [autojs, 脚本]
keywords: 'autojs,外挂,网赚'
categories: [autojs,外挂,网赚]
abbrlink: AVOOZOBZ1v
date: 2021-03-31 23:30:04
description:
cover:
top_img:
---


> 此处整理一些常用的autojs脚本片段,便于查询.

## 1. 如何优雅的开启"无障碍服务" ?

```js
"ui";

// 误区一：使用线程开启无障碍
// 浪费CPU和内存资源，不必要的线程
// threads.start(function() {
//      auto.waitFor();
// });


// 误区二：直接使用auto()
// 对用户不友好
// auto();

// 正确示范：
// 通过一个开关表示无障碍权限是否开启
// 如果用户没有开启直接运行则提示

ui.layout(
    <vertical>
        <appbar>
            <toolbar title="UI脚本使用无障碍服务的最佳实践"/>
        </appbar>
        <Switch id="autoService" text="开启无障碍服务" checked="{{auto.service != null}}" padding="8 8 8 8" textSize="15sp"/>
        <Switch id="switchEnbleFloating" text="开启悬浮窗" checked="false" padding="8 8 8 8" textSize="15sp" textColor="red" />
        <button id="start" text="开始运行"/>
    </vertical>
);

ui.autoService.on("check", function(checked) {
    // 用户勾选无障碍服务的选项时，跳转到页面让用户去开启
    if(checked && auto.service == null) {
        app.startActivity({
            action: "android.settings.ACCESSIBILITY_SETTINGS"
        });
    }
    if(!checked && auto.service != null){
        auto.service.disableSelf();
    }
});

// 当用户回到本界面时，resume事件会被触发
ui.emitter.on("resume", function() {
    // 此时根据无障碍服务的开启情况，同步开关的状态
    ui.autoService.setChecked(auto.service != null);
    // ui.autoService.checked = auto.service != null;
});


// 用户勾选悬浮窗的选项时，跳转到页面让用户去开启 
ui.switchEnbleFloating.on("check", function (checked) {
    if (checked) { //  && auto.service == null
        app.startActivity({
            action: "android.settings.action.MANAGE_OVERLAY_PERMISSION"
        });
    }
    if (!checked && auto.service != null) {
        // auto.service.disableSelf();
    }
});

// 点击启动线程
ui.start.on("click", function(){
    //程序开始运行之前判断无障碍服务
    if(auto.service == null) {
        toast("请先开启无障碍服务！");
        return;
    }
    main();
});


function main() {
    // 这里写脚本的主逻辑
    threads.start(function () {
        log("开始运行");
        sleep(2000);
        log("运行结束");
    });
}

```

## 2. UI编程的一些注意事项

- 1. 不管你的代码多么少, `"ui";` 这个字符串,必须放在第一行,在它之上,不能有任何的代码和注释.

- 2. UI线程中除函数和公用变量外不要写任何流程性质的代码,如果要写流程,必须使用线程

```js
threads.start(function() {
    //这里写你的流程代码
});
```

- 3. 使用线程时,如果要对UI中的数据进行修改,最好使用下面的方法来执行:

```js
threads.start(function() {
    //流程代码
    ui.run(()=>{
        //这里写针对UI的操作
    });
});
```

- 4. 为了方便管理,所有开的线程,根据不同功能,最好都定义各个线程的变量名

```js
const Thread = threads.start(function() {});

```

- 5. 线程函数,不能简写 观察上面的代码,你会发现:

```js
ui.run(()=>{});
```
而在线程 threads.start();中,我的写法是:

```js
threads.start(function() {});

```

- 6. 使用`setVisibility()`方法时,一定要 `importClass(android.view.View);`
括号中的属性包括:

```js
View.GONE //完全隐藏控件
View.INVISIBLE //隐藏控件,但保留控件的位置
View.VISIBLE //默认属性, 显示控件
```

- 7. 针对text控件的对齐 gravity 要在 linear 布局中进行设置,例如

```xml
<linear gravity="right|center" w="80" h="*">
    <text text="当前速度: "
        textColor="#FFFFFF"
        textSize="16sp" />
</linear>
```

## 3. Intent列表,打开对应的Intent页面

```js
var intent = new Intent();
// vpnIntent.setAction("android.net.vpn.SETTINGS");
intent.setAction("android.settings.ACCESSIBILITY_SETTINGS"); //辅助功能
intent.setAction("android.settings.ADD_ACCOUNT_SETTINGS"); //添加账户
intent.setAction("android.settings.AIRPLANE_MODE_SETTINGS"); //系统设置首页
intent.setAction("android.settings.APN_SETTINGS"); //APN设置
intent.setAction("android.settings.APPLICATION_SETTINGS"); //应用管理
intent.setAction("android.settings.BATTERY_SAVER_SETTINGS"); //节电助手
intent.setAction("android.settings.BLUETOOTH_SETTINGS"); //蓝牙
intent.setAction("android.settings.CAPTIONING_SETTINGS"); //字幕
intent.setAction("android.settings.CAST_SETTINGS"); //无线显示
intent.setAction("android.settings.DATA_ROAMING_SETTINGS"); //移动网络
intent.setAction("android.settings.DATE_SETTINGS"); //日期和时间设置
intent.setAction("android.settings.DEVICE_INFO_SETTINGS"); //关于手机
intent.setAction("android.settings.DISPLAY_SETTINGS"); //显示设置
intent.setAction("android.settings.DREAM_SETTINGS"); //互动屏保设置
intent.setAction("android.settings.HARD_KEYBOARD_SETTINGS"); //实体键盘
intent.setAction("android.settings.HOME_SETTINGS"); //应用权限,默认应用设置,特殊权限
intent.setAction("android.settings.IGNORE_BATTERY_OPTIMIZATION_SETTINGS"); //忽略电池优化设置
intent.setAction("android.settings.INPUT_METHOD_SETTINGS"); //可用虚拟键盘设置
intent.setAction("android.settings.INPUT_METHOD_SUBTYPE_SETTINGS"); //安卓键盘语言设置(AOSP)
intent.setAction("android.settings.INTERNAL_STORAGE_SETTINGS"); //内存和存储
intent.setAction("android.settings.LOCALE_SETTINGS"); //语言偏好设置
intent.setAction("android.settings.LOCATION_SOURCE_SETTINGS"); //定位服务设置
intent.setAction("android.settings.MANAGE_ALL_APPLICATIONS_SETTINGS"); //所有应用
intent.setAction("android.settings.MANAGE_APPLICATIONS_SETTINGS"); //应用管理
intent.setAction("android.settings.MANAGE_DEFAULT_APPS_SETTINGS"); //与ACTION_HOME_SETTINGS相同
intent.setAction("android.settings.action.MANAGE_OVERLAY_PERMISSION"); //在其他应用上层显示,悬浮窗
intent.setAction("android.settings.MANAGE_UNKNOWN_APP_SOURCES"); //安装未知应用 安卓8.0
intent.setAction("android.settings.action.MANAGE_WRITE_SETTINGS"); //可修改系统设置 权限
intent.setAction("android.settings.MEMORY_CARD_SETTINGS"); //内存与存储
intent.setAction("android.settings.NETWORK_OPERATOR_SETTINGS"); //可用网络选择
intent.setAction("android.settings.NFCSHARING_SETTINGS"); //NFC设置
intent.setAction("android.settings.NFC_SETTINGS"); //网络中的 更多设置
intent.setAction("android.settings.ACTION_NOTIFICATION_LISTENER_SETTINGS"); //通知权限设置
intent.setAction("android.settings.NOTIFICATION_POLICY_ACCESS_SETTINGS"); //勿扰权限设置
intent.setAction("android.settings.ACTION_PRINT_SETTINGS"); //打印服务设置
intent.setAction("android.settings.PRIVACY_SETTINGS"); //备份和重置
intent.setAction("android.settings.SECURITY_SETTINGS"); //安全设置
intent.setAction("android.settings.SHOW_REGULATORY_INFO"); //监管信息
intent.setAction("android.settings.SOUND_SETTINGS"); //声音设置
intent.setAction("android.settings.SYNC_SETTINGS"); //添加账户设置
intent.setAction("android.settings.USAGE_ACCESS_SETTINGS"); //有权查看使用情况的应用
intent.setAction("android.settings.USER_DICTIONARY_SETTINGS"); //个人词典
intent.setAction("android.settings.VOICE_INPUT_SETTINGS"); //辅助应用和语音输入
intent.setAction("android.settings.VPN_SETTINGS"); //VPN设置
intent.setAction("android.settings.VR_LISTENER_SETTINGS"); //VR助手
intent.setAction("android.settings.WEBVIEW_SETTINGS"); //选择webview
intent.setAction("android.settings.WIFI_IP_SETTINGS"); //高级WLAN设置
intent.setAction("android.settings.WIFI_SETTINGS"); //选择WIFI,连接WIFI
intent.setAction("com.android.settings.Settings$DevelopmentSettingsActivity");

app.startActivity(intent);

```

Intent查找, 先准备工具：Activity管理器,点击认为是正确的Activity，测试看看是否正确，搜索一般内含Search。找到正确能打开淘宝搜索页的出来。
找到后就是写代码调用了。这里找出来正确的`"com.taobao.search.searchdoor.SearchDoorActivity"`。

```js
app.startActivity({
	action: "View",
	packageName: "com.taobao.taobao",
	className: "com.taobao.search.searchdoor.SearchDoorActivity"
});
```
运行就可以自动打开淘宝app的搜索页面出来了。


## 4. 增强版`toast`,带有时间参数

```js
function toasts(text, time) {
    text = text || null;
    time = time || 2500;
    if (isNaN(time)) return;
    let arr = engines.all(),
        run = false;
    for (i in arr) {
        if (files.getName(arr[i].getSource()) == "toast.js") {
            run = true;
            break;
        }
    }
    if (!run) {
        let tex = "var t = toasts();\nevents.broadcast.on(\"toast\", (arr) => {\nif (arr.length != 2) return;\nlet time = new Number(arr[1][1]),text = arr[1][0];\nif(isNaN(time)) time = 5000;\nif(!text) return;\nt(text, time);});\nsetInterval(() => {}, 10000);\nfunction toasts() {\nvar th = \"\",Y = device.width / 4,X = Y,x = Y * 2;\nvar flo = floaty.rawWindow(\n<frame gravity=\"center\" bg=\"#00000000\">\n<text id=\"message\"  bg=\"#70000000\" textColor=\"#ffffff\" textSize=\"18sp\" gravity=\"center\" w=\"auto\" padding=\"1\"/>\n</frame>);\nflo.setTouchable(false);\nflo.setSize(0, 0);\nreturn doflo;\nfunction doflo(mes, time) {\nmes = \" \" + mes.toString().split(\"\\n\").join(\" \\n \") + \" \";\nif (th != \"\") {\nth.interrupt();\nth = \"\";}\nui.run(function() {\nflo.message.setText(mes);});\nflo.setPosition(X, Y);\nflo.setSize(x, -2);\nth = threads.start(function() {\nsleep(time);\nui.run(function() {\nflo.message.setText(\"\");});\nflo.setSize(0, 0);\nth = \"\";});}}";
        engines.execScript("toast", tex);
        sleep(500);
    }
    events.broadcast.emit("toast", [[engines.myEngine(),[text, time]]]);
}

```

## 5. 获取随机相关函数

参考代码: <https://easydoc.xyz/doc/25791054/uw2FUUiw/QzYbygUV>

```js

//取随机姓名
//此代码由飞云脚本圈整理（www.feiyunjs.com）
function getRndName() {
    //以下字库可自行添加
    var familyNames = new Array(
        "赵", "钱", "孙", "李", "周", "吴", "郑", "王", "冯", "陈",
        "褚", "卫", "蒋", "沈", "韩", "杨", "朱", "秦", "尤", "许",
        "何", "吕", "施", "张", "孔", "曹", "严", "华", "金", "魏",
        "陶", "姜", "戚", "谢", "邹", "喻", "柏", "水", "窦", "章",
        "云", "苏", "潘", "葛", "奚", "范", "彭", "郎", "鲁", "韦",
        "昌", "马", "苗", "凤", "花", "方", "俞", "任", "袁", "柳",
        "酆", "鲍", "史", "唐", "费", "廉", "岑", "薛", "雷", "贺",
        "倪", "汤", "滕", "殷", "罗", "毕", "郝", "邬", "安", "常",
        "乐", "于", "时", "傅", "皮", "卞", "齐", "康", "伍", "余",
        "元", "卜", "顾", "孟", "平", "黄", "和", "穆", "萧", "尹",
        "司马","欧阳","上官","夏侯夏侯","诸葛","西门","南宫","东郭",
        "百里","尉迟","端木","皇甫","钟离","宇文","长孙","慕容","司徒","司空","东方","公孙","令狐"
    );
    var givenNames = new Array(
        "子璇", "淼", "国栋", "夫子", "瑞堂", "甜", "敏", "尚", "国贤", "贺祥", "晨涛",
        "昊轩", "易轩", "益辰", "益帆", "益冉", "瑾春", "瑾昆", "春齐", "杨", "文昊",
        "东东", "雄霖", "浩晨", "熙涵", "溶溶", "冰枫", "欣欣", "宜豪", "欣慧", "建政",
        "美欣", "淑慧", "文轩", "文杰", "欣源", "忠林", "榕润", "欣汝", "慧嘉", "新建",
        "建林", "亦菲", "林", "冰洁", "佳欣", "涵涵", "禹辰", "淳美", "泽惠", "伟洋",
        "涵越", "润丽", "翔", "淑华", "晶莹", "凌晶", "苒溪", "雨涵", "嘉怡", "佳毅",
        "子辰", "佳琪", "紫轩", "瑞辰", "昕蕊", "萌", "明远", "欣宜", "泽远", "欣怡",
        "佳怡", "佳惠", "晨茜", "晨璐", "运昊", "汝鑫", "淑君", "晶滢", "润莎", "榕汕",
        "佳钰", "佳玉", "晓庆", "一鸣", "语晨", "添池", "添昊", "雨泽", "雅晗", "雅涵",
        "清妍", "诗悦", "嘉乐", "晨涵", "天赫", "玥傲", "佳昊", "天昊", "萌萌", "若萌",
        "惠宁","雅欣","奕雯","佳琪","永怡","璐瑶","娟秀","天佳","晓华","妍丽","璇菡",
        "嘉禾","忆辰","妍彤","眉萱","秀辰","怡熹","思琦","弦娇","青淑","宣淑","和静",
        "雪涵","美嘉","佳涵","旭和","丽娇","雨晨","文惠","雅馥","雨嘉","亦婷","秀慧",
        "俊颖","亭清","思涵","珂嘉","蒂莲","秀娟","晋仪","玮菁","慧琳","丽帆","思辰",
        "宇纯","美瑞","蕊清","秀敏","家维","宁致","婷方","燕晨","子琳","雪菲","泓锦",
        "佳妮","初晨","芷菡","奕可","莉姿","杏菏","韵彩","姝慧","雪华","珊娜","秀丽",
        "箫辉","盈初","语楚","青秋","梓菁","宝萱"
    );
    var i = parseInt( * Math.random()) * + parseInt( * Math.random());
    var familyName = familyNames[i];
    var j = parseInt( * Math.random()) * + parseInt( * Math.random());
    var givenName = givenNames[i];
    var name = familyName + givenName;
    var x = document.getElementsByName("client_name");
    for (var i = ; i < x.length; i++) {
        var o = x[i];
        o.value = name;
    };
};

// 取随机手机号
//此代码由飞云脚本圈整理（www.feiyunjs.com）
function getRndMoble() {
    var prefixArray = new Array("130", "131", "132", "133", "134", "135", "137", "138",
        "170", "187", "189", "199", "198", "156", "166", "175", "186", "184", "146", "139", "147",
        "150", "151", "152", "157", "158", "159", "178", "182", "183", "187", "188", "133", "153",
        "149", "173", "177", "180", "181", "189");
    var i = parseInt(10 * Math.random());
    var prefix = prefixArray[i];
    for (var j = 0; j < 8; j++) {
        prefix = prefix + Math.floor(Math.random() * 10);
    };
    var x = document.getElementsByName("mobile_tel");
    for (var i = 0; i < x.length; i++) {
        var o = x[i];
        o.value = prefix;
    };
};

// 取随机身份证号
//此代码由飞云脚本圈整理（www.feiyunjs.com）
function getRndID() {
    var coefficientArray = ["7", "9", "10", "5", "8", "4", "2", "1", "6", "3", "7", "9", "10", "5", "8", "4", "2"];// 加权因子
    var lastNumberArray = ["1", "0", "X", "9", "8", "7", "6", "5", "4", "3", "2"];// 校验码
    var address = "420101"; // 住址
    var birthday = "19810101"; // 生日
    var s = Math.floor(Math.random() * 10).toString() + Math.floor(Math.random() * 10).toString() + Math.floor(Math.random() * 10).toString();
    var array = (address + birthday + s).split("");
    var total = 0;
    for (i in array) {
        total = total + parseInt(array[i]) * parseInt(coefficientArray[i]);
    };
    var lastNumber = lastNumberArray[parseInt(total % 11)];
    var id_no_String = address + birthday + s + lastNumber;
    var x = document.getElementsByName("id_no");
    for (var i = 0; i < x.length; i++) {
        var o = x[i];
        o.value = id_no_String;
    };
};


//取随机字母数字
//此代码由飞云脚本圈整理（www.feiyunjs.com）
//https://www.cnblogs.com/sunshq/p/4171490.html
/*
** randomWord 产生任意长度随机字母数字组合
** randomFlag-是否任意长度 min-任意长度最小位[固定位数] max-任意长度最大位
** xuanfeng 2014-08-28
*/
function getRndLetterNumber(randomFlag, min, max){
    var str = "",
        range = min,
        arr = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z', 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'];
 
    // 随机产生
    if(randomFlag){
        range = Math.round(Math.random() * (max-min)) + min;
    }
    for(var i=0; i<range; i++){
        pos = Math.round(Math.random() * (arr.length-1));
        str += arr[pos];
    }
    return str;
};

//使用方法
//生成3-32位随机串：
getRndLetterNumber(true, 3, 32)
//生成43位随机串：
getRndLetterNumber(false, 43)


//取随机汉字(简体+生僻字)
//此代码由飞云脚本圈整理（www.feiyunjs.com）
function getRndWord() {
    eval("var word=" + '"\\u' + (Math.round(Math.random() * 20901) + 19968).toString(16) + '"')
    return word;
};


```

## 5. 时间戳相关

```js
// 获取时间戳
var timestamp = new Date().getTime()；  //获取时间戳


// 时间戳转时间
//第一种  2010年12月23日 10:53
function getLocalTime(nS) {     
   return new Date(parseInt(nS) * 1000).toLocaleString().replace(/:\d{1,2}$/,' ');     
};    
log(getLocalTime(1293072805));

//第二种    
function getLocalTime(nS) {     
    return new Date(parseInt(nS) * 1000).toLocaleString().substr(0,17)
};    
log(getLocalTime(1293072805));

//第三种  2010-10-20 10:00:00
function getLocalTime(nS) {     
    return new Date(parseInt(nS) * 1000).toLocaleString().replace(/年|月/g, "-").replace(/日/g, " ");      
};     
log(getLocalTime(1177824835));

```

## 6. 飞行模式切换

```js
function 打开飞行模式() {
  // 打开飞行模式
  new Shell().exec("su -c 'settings put global airplane_mode_on 1; am broadcast -a android.intent.action.AIRPLANE_MODE --ez state true'")
};

function 关闭飞行模式() {
  //关闭飞行模式
  new Shell().exec("su -c 'settings put global airplane_mode_on 0; am broadcast -a android.intent.action.AIRPLANE_MODE --ez state false'")
};

```

## 7. 点击指定区域

```js
while (true) {
 click(500, 380);
}
//或者用
for (var i = 0; i < 7; i++) {
click(500, 380);
}

```

## 8. 自动打开网址

```js
"Auto"
app.openUrl("http://chapai.act.qq.com/ph2");

```

## 9. 禁止脚本多次运行

```js
/*
 * Author:TimeOut
 * Date: 2018.12.18
 */

//获取当前所运行的脚本
var list = engines.all();
//双循环比较
for (var i = 0; i < list.length; i++) {
    for (var j = i + 1; j < list.length; j++) {
       //比较是否只有一个运行
        if (list[i].getSource().toString() == list[j].getSource().toString()) {
            //停止二次运行的脚本
            list[j].forceStop();
        };
    };
};
```

## 10. 获取指定应用的版本号

```js
/*
* 获取指定应用的版本号
* @param {string} packageName 应用包名
*/
function getPackageVersion(packageName) {
    importPackage(android.content);
    var pckMan = context.getPackageManager();
    var packageInfo = pckMan.getPackageInfo(packageName, 0);
    return packageInfo.versionName;
};

```

## 11. 停止卸载APP

```js
// 停止APP
function killApp(packageName) {
    shell('am force-stop ' + packageName, true);
};


// 卸载APP
function uninstallApp(packageName) {
    shell("pm uninstall " + packageName, true)
};

// 清除App数据
function clearApp(packageName) {
    shell('pm clear ' + packageName, true);
};

// 卸载最新安装的app
function uninstallAppLast() {
    var pm = context.getPackageManager()
    var appList = pm.getInstalledApplications(0)
    var appInfoList = []
    for (let i = 0; i < appList.size(); i++) {
        var app = appList.get(i)
        var appInfo = {
            appName: app.loadLabel(pm),
            packageName: app.packageName,
            isSystemApp: app.isSystemApp(),
            firstInstallTime: pm.getPackageInfo(app.packageName, 0).firstInstallTime
        }
        appInfoList.push(appInfo)

    }
    appInfoList.sort((a, b) => {
        return b.firstInstallTime - a.firstInstallTime
    })
    log('最新安装的app是=%j', appInfoList[0])

    var packageName = appInfoList[0].packageName
    shell("pm uninstall " + packageName, true)
    return appInfoList[0].appName
};

// 清除最新安装的APP数据
function clearAppLast() {
    var pm = context.getPackageManager()
    var appList = pm.getInstalledApplications(0)
    var appInfoList = []
    for (let i = 0; i < appList.size(); i++) {
        var app = appList.get(i)
        var appInfo = {
            appName: app.loadLabel(pm),
            packageName: app.packageName,
            isSystemApp: app.isSystemApp(),
            firstInstallTime: pm.getPackageInfo(app.packageName, 0).firstInstallTime
        }
        appInfoList.push(appInfo)

    }
    appInfoList.sort((a, b) => {
        return b.firstInstallTime - a.firstInstallTime
    })
    log('最新安装的app是=%j', appInfoList[0])

    var packageName = appInfoList[0].packageName
    shell('pm clear ' + packageName, true);
    return appInfoList[0].appName
};


// 停止最新安装的APP
function killAppLast {
    var pm = context.getPackageManager()
    var appList = pm.getInstalledApplications(0)
    var appInfoList = []
    for (let i = 0; i < appList.size(); i++) {
        var app = appList.get(i)
        var appInfo = {
            appName: app.loadLabel(pm),
            packageName: app.packageName,
            isSystemApp: app.isSystemApp(),
            firstInstallTime: pm.getPackageInfo(app.packageName, 0).firstInstallTime
        }
        appInfoList.push(appInfo)

    }
    appInfoList.sort((a, b) => {
        return b.firstInstallTime - a.firstInstallTime
    })
    log('最新安装的app是=%j', appInfoList[0])

    var packageName = appInfoList[0].packageName
    shell('am force-stop ' + packageName, true);
    return appInfoList[0].appName
};

```

