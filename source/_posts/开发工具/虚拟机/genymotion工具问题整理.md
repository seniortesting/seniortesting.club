---
title: genymotion工具问题整理
abbrlink: GDBxruHnFk
tags: []
keywords: ''
categories: []
date: 2021-03-25 23:12:53
description:
cover: 
top_img:
---

## 工作

### Ionic 闲置材料商城

参考：[github ionic源码商城](https://github.com/search?o=desc&q=ionic%E5%95%86%E5%9F%8E&s=updated&type=Repositories)

## 问题

### How to make a transparent(tbm ) header / toolbar?

针对Ionic2可以参考如下链接: [Create a Stylish News Feed Layout in Ionic 2 & 3](https://www.joshmorony.com/create-a-stylish-news-feed-layout-in-ionic-2/)

``` html
<ion-header translucent>
</ion-header>

 <ion-content
      no-padding
      fullscreen
      :scrollEvents="true" @ionScroll="scrollContent">
    
</ion-content>

```

### `mapGetters`,`mapState` 都放在computed里面作为计算属性

```
computed: {
    ...mapState({
        islogged: state=>state.user.islogged
    }),
    ...mapGetters(['islogged'])
}
```

### genymotion的虚拟机不能现在在android studio的device列表中

<https://stackoverflow.com/questions/36142055/genymotion-device-doesnt-appear-on-device-chooser-android-studio>

* click the run button to compile project
* device empty list appear
* start genymotion
* device will appear in the list

### genymotion拖动apk文件出现错误： an error occurred while deploying the file

> 原来是genymotion对应的adb于Android sdk中的adb版本不兼容的问题，换成genymotion内置的adb是没有问题的，所以升级genymotion到3.0，然后升级对应的android sdk到对应的版本即可。

### Genymotion 的android 9.0 可以使用 Android 8.1 的 ARM_Translation_Oreo_android8 ，测试可用。没有找到最新的Android 9.0 的arm translation

### 无法加载webgl

```
IconLoader: Could not find icon drawable from resource
    android.content.res.Resources$NotFoundException: Resource ID #0xffffffff
        at android.content.res.ResourcesImpl.getValueForDensity(ResourcesImpl.java:225)
        at android.content.res.Resources.getDrawableForDensity(Resources.java:887)
        at android.content.res.Resources.getDrawable(Resources.java:827)
        at com.android.systemui.shared.recents.model.IconLoader.createNewIconForTask(IconLoader.java:118)
        at com.android.systemui.shared.recents.model.IconLoader.getAndInvalidateIfModified(IconLoader.java:94)
        at com.android.systemui.shared.recents.model.RecentsTaskLoader.getAndUpdateActivityIcon(RecentsTaskLoader.java:325)
        at com.android.systemui.shared.recents.model.RecentsTaskLoadPlan.executePlan(RecentsTaskLoadPlan.java:202)
        at com.android.systemui.shared.recents.model.RecentsTaskLoader.loadTasks(RecentsTaskLoader.java:173)
        at net.oneplus.quickstep.RecentsModel.onTaskStackChangedBackground(RecentsModel.java:275)
        at com.android.systemui.shared.system.TaskStackChangeListeners.onTaskStackChanged(TaskStackChangeListeners.java:80)
        at android.app.ITaskStackListener$Stub.onTransact(ITaskStackListener.java:50)
        at android.os.Binder.execTransact(Binder.java:752)
        
        
        
         java.util.ConcurrentModificationException
        at java.util.ArrayList$Itr.next(ArrayList.java:860)
        at android.app.ActivityThread.installContentProviders(ActivityThread.java:6106)
        at android.app.ActivityThread.handleBindApplication(ActivityThread.java:6021)
        at android.app.ActivityThread.access$1300(ActivityThread.java:207)
        at android.app.ActivityThread$H.handleMessage(ActivityThread.java:1748)
        at android.os.Handler.dispatchMessage(Handler.java:106)
        at android.os.Looper.loop(Looper.java:193)
        at android.app.ActivityThread.main(ActivityThread.java:6863)
        at java.lang.reflect.Method.invoke(Native Method)
        at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:537)


   --------- beginning of main
2019-05-08 12:02:35.277 366-596/system_process W/AudioTrack: AUDIO_OUTPUT_FLAG_FAST denied by client; transfer 4, track 48000 Hz, output 44100 Hz
2019-05-08 12:02:35.282 1720-1720/? I/zygote: Late-enabling -Xcheck:jni
2019-05-08 12:02:35.290 366-378/system_process I/ActivityManager: Start proc 1720:com.yitieyilu.app/u0a71 for activity com.yitieyilu.app/.MainActivity
2019-05-08 12:02:35.297 1720-1720/? D/houdini: [1720] Initialize library(version: 8.0.0_y.49374 RELEASE)... successfully.
2019-05-08 12:02:35.297 1720-1720/? W/zygote: Unexpected CPU variant for X86 using defaults: x86
2019-05-08 12:02:35.300 1720-1720/? I/JDWP: type=1400 audit(0.0:1007): avc: denied { read write } for path="socket:[31954]" dev="sockfs" ino=31954 scontext=u:r:untrusted_app:s0:c512,c768 tcontext=u:r:init:s0 tclass=unix_stream_socket permissive=1
2019-05-08 12:02:35.312 1720-1727/? E/zygote: Failed writing handshake bytes (-1 of 14): Broken pipe
2019-05-08 12:02:35.312 1720-1727/? I/zygote: Debugger is no longer active
2019-05-08 12:02:35.356 1720-1735/? I/vndksupport: sphal namespace is not configured for this process. Loading /system/lib/egl/libGLES_emulation.so from the current namespace instead.
2019-05-08 12:02:35.360 1720-1720/? E/zygote: No implementation found for void com.tencent.StubShell.TxAppEntry.fixNativeResource(android.content.res.AssetManager, java.lang.String) (tried Java_com_tencent_StubShell_TxAppEntry_fixNativeResource and Java_com_tencent_StubShell_TxAppEntry_fixNativeResource__Landroid_content_res_AssetManager_2Ljava_lang_String_2)
2019-05-08 12:02:35.370 1720-1735/? I/vndksupport: sphal namespace is not configured for this process. Loading /system/lib/egl/libEGL_emulation.so from the current namespace instead.
2019-05-08 12:02:35.374 1720-1720/? E/zygote: No implementation found for void com.tencent.StubShell.TxAppEntry.fixUnityResource(android.content.res.AssetManager, java.lang.String) (tried Java_com_tencent_StubShell_TxAppEntry_fixUnityResource and Java_com_tencent_StubShell_TxAppEntry_fixUnityResource__Landroid_content_res_AssetManager_2Ljava_lang_String_2)
2019-05-08 12:02:35.879 1137-1137/com.android.launcher3 I/Choreographer: Skipped 30 frames!  The application may be doing too much work on its main thread.
2019-05-08 12:02:35.896 1720-1720/? I/BUGLY_THREAD: type=1400 audit(0.0:1014): avc: denied { lock } for path="/data/data/com.yitieyilu.app/databases/bugly_db_legu" dev="sdb3" ino=81969 scontext=u:r:untrusted_app:s0:c512,c768 tcontext=u:object_r:system_data_file:s0:c512,c768 tclass=file permissive=1
2019-05-08 12:02:35.902 1720-1735/? I/vndksupport: sphal namespace is not configured for this process. Loading /system/lib/egl/libGLESv1_CM_emulation.so from the current namespace instead.
2019-05-08 12:02:35.904 1720-1720/? I/m.yitieyilu.app: type=1400 audit(0.0:1016): avc: denied { read } for name="databases" dev="sdb3" ino=81939 scontext=u:r:untrusted_app:s0:c512,c768 tcontext=u:object_r:system_data_file:s0:c512,c768 tclass=dir permissive=1
2019-05-08 12:02:35.904 1720-1720/? I/m.yitieyilu.app: type=1400 audit(0.0:1017): avc: denied { open } for path="/data/data/com.yitieyilu.app/databases" dev="sdb3" ino=81939 scontext=u:r:untrusted_app:s0:c512,c768 tcontext=u:object_r:system_data_file:s0:c512,c768 tclass=dir permissive=1
2019-05-08 12:02:35.919 1720-1735/? I/vndksupport: sphal namespace is not configured for this process. Loading /system/lib/egl/libGLESv2_emulation.so from the current namespace instead.
2019-05-08 12:02:35.965 1720-1720/? D/houdini: [1720] loaded library /data/app/com.yitieyilu.app-UtOPYAJy5psmCStTkjksGA==/lib/arm/libBugly.so via Native Bridge.
2019-05-08 12:02:35.965 1720-1720/? I/CrashReport: native library loaded
2019-05-08 12:02:35.965 1720-1737/? W/System.err: java.io.FileNotFoundException: /system/build.prop (Permission denied)
2019-05-08 12:02:35.966 1720-1720/? I/CrashReport: backup java method success
2019-05-08 12:02:35.966 1720-1737/? W/System.err:     at java.io.FileInputStream.open0(Native Method)
2019-05-08 12:02:35.966 1720-1720/? I/CrashReport: back up java classes success
2019-05-08 12:02:35.967 1720-1737/? W/System.err:     at java.io.FileInputStream.open(FileInputStream.java:200)
2019-05-08 12:02:35.967 1720-1737/? W/System.err:     at java.io.FileInputStream.<init>(FileInputStream.java:150)
2019-05-08 12:02:35.968 1720-1737/? W/System.err:     at java.io.FileInputStream.<init>(FileInputStream.java:103)
2019-05-08 12:02:35.970 1720-1737/? W/System.err:     at java.io.FileReader.<init>(FileReader.java:58)
2019-05-08 12:02:35.970 1720-1737/? W/System.err:     at com.tencent.bugly.legu.proguard.a.p(BUGLY:177)
2019-05-08 12:02:35.970 1720-1737/? W/System.err:     at com.tencent.bugly.legu.proguard.a.e(BUGLY:226)
2019-05-08 12:02:35.970 1720-1737/? W/System.err:     at com.tencent.bugly.legu.crashreport.common.info.a.q(BUGLY:330)
2019-05-08 12:02:35.970 1720-1737/? W/System.err:     at com.tencent.bugly.legu.proguard.a.a(BUGLY:143)
2019-05-08 12:02:35.971 1720-1737/? W/System.err:     at com.tencent.bugly.legu.crashreport.biz.a.b(BUGLY:232)
2019-05-08 12:02:35.971 1720-1737/? W/System.err:     at com.tencent.bugly.legu.crashreport.biz.a$a.run(BUGLY:135)
2019-05-08 12:02:35.971 1720-1737/? W/System.err:     at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:457)
2019-05-08 12:02:35.971 1720-1737/? W/System.err:     at java.util.concurrent.FutureTask.run(FutureTask.java:266)
2019-05-08 12:02:35.972 1720-1737/? W/System.err:     at java.util.concurrent.ScheduledThreadPoolExecutor$ScheduledFutureTask.run(ScheduledThreadPoolExecutor.java:301)
2019-05-08 12:02:35.973 1720-1737/? W/System.err:     at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1162)
2019-05-08 12:02:35.973 1720-1737/? W/System.err:     at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:636)
2019-05-08 12:02:35.973 1720-1737/? W/System.err:     at java.lang.Thread.run(Thread.java:764)
2019-05-08 12:02:35.992 1720-1720/? I/CrashReport: base = 0xd3ec4000
2019-05-08 12:02:35.992 1720-1720/? I/CrashReport: stacksize = 4M
2019-05-08 12:02:35.993 1720-1720/? I/CrashReport: guardsize = 4096
2019-05-08 12:02:35.996 1720-1720/? I/CrashReport: getted buglyline com/tencent/bugly/legu/
2019-05-08 12:02:36.004 1720-1720/? I/CrashReport: it is a channel prefix com/tencent/bugly/legu/
2019-05-08 12:02:36.004 1720-1720/? I/CrashReport: register native log methods success
2019-05-08 12:02:36.005 1720-1720/? I/CrashReport: register native key-value methods success
2019-05-08 12:02:36.005 1720-1720/? I/CrashReport: register native methods success
2019-05-08 12:02:36.005 1720-1720/? I/CrashReport: setLogMode 6 current 4
2019-05-08 12:02:36.028 1720-1720/? D/AndroidRuntime: Shutting down VM
    
    
    --------- beginning of crash
2019-05-08 12:02:36.030 1720-1720/? E/AndroidRuntime: FATAL EXCEPTION: main
    Process: com.yitieyilu.app, PID: 1720
    java.lang.UnsatisfiedLinkError: dlopen failed: "/data/app/com.yitieyilu.app-UtOPYAJy5psmCStTkjksGA==/lib/arm/libshellx-3.0.0.0.so" has unexpected e_machine: 3
        at java.lang.Runtime.loadLibrary0(Runtime.java:1016)
        at java.lang.System.loadLibrary(System.java:1657)
        at com.tencent.StubShell.TxAppEntry.e(Unknown Source:630)
        at com.tencent.StubShell.TxAppEntry.a(Unknown Source:0)
        at com.tencent.StubShell.TxAppEntry.attachBaseContext(Unknown Source:62)
        at android.app.Application.attach(Application.java:189)
        at android.app.Instrumentation.newApplication(Instrumentation.java:1102)
        at android.app.Instrumentation.newApplication(Instrumentation.java:1086)
        at android.app.LoadedApk.makeApplication(LoadedApk.java:965)
        at android.app.ActivityThread.handleBindApplication(ActivityThread.java:5765)
        at android.app.ActivityThread.-wrap1(Unknown Source:0)
        at android.app.ActivityThread$H.handleMessage(ActivityThread.java:1661)
        at android.os.Handler.dispatchMessage(Handler.java:105)
        at android.os.Looper.loop(Looper.java:164)
        at android.app.ActivityThread.main(ActivityThread.java:6541)
        at java.lang.reflect.Method.invoke(Native Method)
        at com.android.internal.os.Zygote$MethodAndArgsCaller.run(Zygote.java:240)
        at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:767)
2019-05-08 12:02:36.119 1008-1511/com.android.dialer I/Dialer: VvmTaskExecutor - executing task com.android.voicemail.impl.ActivationTask@fcbbb3a
2019-05-08 12:02:36.120 1008-1511/com.android.dialer I/Dialer: PreOMigrationHandler - ComponentInfo{com.android.phone/com.android.services.telephony.TelephonyConnectionService}, [e2f7d48dd2b5ca523e7313cf4ba0f6ea830b6281], UserHandle{0} already migrated
2019-05-08 12:02:36.128 1273-1273/android.process.acore I/Binder:1273_2: type=1400 audit(0.0:1018): avc: denied { lock } for path="/data/data/com.android.providers.contacts/databases/calllog.db" dev="sdb3" ino=81864 scontext=u:r:priv_app:s0:c512,c768 tcontext=u:object_r:system_data_file:s0:c512,c768 tclass=file permissive=1
2019-05-08 12:02:36.139 1008-1511/com.android.dialer I/Dialer: VvmActivationTask - VVM content provider configured - vvm_type_cvvm
2019-05-08 12:02:36.139 1008-1511/com.android.dialer I/Dialer: OmtpVvmCarrierCfgHlpr - OmtpEvent:CONFIG_ACTIVATING
2019-05-08 12:02:36.153 1008-1511/com.android.dialer I/Dialer: TelephonyMangerCompat.setVisualVoicemailSmsFilterSettings - using TelephonyManager
2019-05-08 12:02:36.158 1008-1511/com.android.dialer I/Dialer: TelephonyMangerCompat.sendVisualVoicemailSms - using TelephonyManager
2019-05-08 12:02:36.172 688-688/com.android.phone I/Binder:688_2: type=1400 audit(0.0:1023): avc: denied { lock } for path="/data/user_de/0/com.android.providers.telephony/databases/telephony.db" dev="sdb3" ino=81799 scontext=u:r:radio:s0 tcontext=u:object_r:system_data_file:s0 tclass=file permissive=1
2019-05-08 12:02:36.176 438-438/? I/rild: type=1400 audit(0.0:1024): avc: denied { sendto } for path="/dev/socket/logdw" scontext=u:r:rild:s0 tcontext=u:r:init:s0 tclass=unix_dgram_socket permissive=1
2019-05-08 12:02:36.184 449-488/? D/baseband-sms: newsms
2019-05-08 12:02:36.184 449-488/? D/baseband-sms: sender:(N/A)
2019-05-08 12:02:36.184 449-488/? D/baseband-sms: receiver:122
```

乐固加固后出现问题： <https://cloud.tencent.com/developer/ask/197885/answer/308416>

### cordova run android

```
le: not installed
Could not find an installed version of Gradle either in Android Studio,
or on your system to install the gradle wrapper. Please include gradle 
in your path, or install Android Studio


```

```
 https://res.yitieyilu.com/upload/pano/1ba16376e6284cc8af8f41413514242a/index.xml", source: file:///android_asset/www/static/js/61.bundle.js (1)
2019-05-06 12:29:49.153 4087-4146/com.yitieyilu.app E/chromium: [ERROR:context_group.cc(137)] ContextResult::kFatalFailure: WebGL1 blacklisted
2019-05-06 12:29:49.160 4087-4146/com.yitieyilu.app E/chromium: [ERROR:context_group.cc(137)] ContextResult::kFatalFailure: WebGL1 blacklisted
```

## 资源下载

1. All of Genymotion OVAs

[最全Genymotion镜像下载](https://gist.github.com/runo280/e4be3e04c24b463b55ddf012c5cfbdc4),

### 安装genymotion虚拟机

1. 启动genymotion，点击add，等待下载完成，回到目录：
C:\Users\Administrator\AppData\Local\Genymobile\Genymotion\ova，里面是刚刚下载的虚拟机文件。

2. 启动genymotion虚拟机即可.

3. genymotion启动后，对应的`adb.exe`进程也会起来

### ~~使用步骤（不适用直接下载ova的方式)~~

1. 下载上面的地址的ova文件
2. 仅打开oracle vm virtualBox，暂时不要打开Genymotion客户端。管理—-导入虚拟电脑 ，如下：

![genymotion1](./img/genymotion-install1.png)

3. 选择导入下载的.ova镜像—-下一步—–导入。等待其导入成功后关闭即可，不要尝试在virtualBox中打开。打开Genymotion客户端，选中点击Start，就可以使用了。

![genymotion1](./img/genymotion-install2.png)
![genymotion1](./img/genymotion-install3.png)
![genymotion1](./img/genymotion-install4.png)
