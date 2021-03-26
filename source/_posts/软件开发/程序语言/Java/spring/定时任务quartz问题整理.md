---
title: 定时任务quartz问题整理
tags: []
keywords: ''
categories: []
abbrlink: 7670b080
date: 2021-03-26 20:41:06
description:
cover:
top_img:
---

{% note blue 'fas fa-bullhorn' %}

整理常用的quart技术问题

{% endnote %}


## `extends QuartzJobBean` 和 `implements Job `  difference

在spring-boot-quartz中使用提供的接口创建job的时候有两种方式：

- 实现接口`Job` 

如果采用的是implements job接口的形式创建job，name我们如何获取任务传递过来的外部参数呢？

```java
 @Override
    public void execute(JobExecutionContext context) {
        try {
            // 通过访问 JobExecutionContext 获取JobDataMap 对象，从而访问对应的参数
            JobDataMap jobDataMap = context.getJobDetail().getJobDataMap();
            Object jobName = jobDataMap.get("name");
        }
    }

```
有没有一种更方便的形式进行访问获取`JobDataMap`中的参数和值呢？是的，这个就是`QuartzJobBean`类做得

- 继承抽象类`QuartzJobBean`

官方的说明是： 更优雅采用java对象思想来访问传过来的参数。

```java
public class MyJob extends QuartzJobBean {
    private String parameter1;


    public void setParameter1(String parameter1) {
        this.parameter1 = parameter1;
    }

    @Override
    public void execute(JobExecutionContext context) throws JobExecutionException {
        System.out.println("My job is running with "+parameter1);
    }
}
```

## @DisallowConcurrentExecution 配置quartz并发执行

> 可能有多个触发器使用该job，所以避免并发执行这个任务

@DisallowConcurrentExecution
@PersistJobDataAfterExecution



## 常用基本quartz cron表达式

```xml
            每隔5秒执行一次：*/5 * * * * ?

             每隔1分钟执行一次：0 */1 * * * ?

             每天23点执行一次：0 0 23 * * ?

             每天凌晨1点执行一次：0 0 1 * * ?

             每月1号凌晨1点执行一次：0 0 1 1 * ?

             每月最后一天23点执行一次：0 0 23 L * ?

             每周星期天凌晨1点实行一次：0 0 1 ? * L

             在26分、29分、33分执行一次：0 26,29,33 * * * ?

             每天的0点、13点、18点、21点都执行一次：0 0 0,13,18,21 * * ?

```

## quartz state

see [org/quartz-scheduler/quartz/2.3.0/quartz-2.3.0-sources.jar!/org/quartz/impl/jdbcjobstore/Constants.java:142](/org/quartz-scheduler/quartz/2.3.0/quartz-2.3.0-sources.jar!/org/quartz/impl/jdbcjobstore/Constants.java:142)

```java

   // STATES
    String STATE_WAITING = "WAITING";

    String STATE_ACQUIRED = "ACQUIRED";

    String STATE_EXECUTING = "EXECUTING";

    String STATE_COMPLETE = "COMPLETE";

    String STATE_BLOCKED = "BLOCKED";

    String STATE_ERROR = "ERROR";

    String STATE_PAUSED = "PAUSED";

    String STATE_PAUSED_BLOCKED = "PAUSED_BLOCKED";

    String STATE_DELETED = "DELETED";

```


## quartz修改 `JobDetail`的相关属性

在实际运用中可能需要修改`JobDetail`中的描述或者名称或者`JobDataMap`,查了好久发现了一个隐藏很深的方法，如下：

```java
// 先获取jobDetail实例（注意转换成: JobDetailImpl ,否则个别属性不能修改，例如Description)
            JobDetailImpl jobDetail = (JobDetailImpl) scheduler.getJobDetail(jobKey);
            CronTrigger cronTrigger = (CronTrigger) scheduler.getTrigger(triggerKey);
            if (jobDetail != null && cronTrigger != null) {
                if (StrUtil.isNotEmpty(description)) {
                    jobDetail.setDescription(description);
                }
                if (null != jobData && !jobData.isEmpty()) {
                    String trimJobData = jobData.trim();
                    Map<String, String> updateParams = Splitter.on("\n").withKeyValueSeparator("=").split(trimJobData);
                    jobDetail.getJobDataMap().putAll(updateParams);
                }
                // 重點： 重新保存内容更新, 注意第二，三個參數
                // 第二個參數replace表示如果存在，替換掉
                // 第三個參數storeNonDurableWhileAwaitingScheduling表示，參見下方說明,所以此處需要設置被true
                scheduler.addJob(jobDetail, true, true);
            }

```

另外，如果需要每次執行完任務后都保存任務的相關配置參數，需要聲明任務是: StatefulJob,但是此方法已經過時，推薦的使用方法是直接添加兩個註解到`Job`上：`@DisallowConcurrentExecution`和
`@PersistJobDataAfterExecution`

``` java
@Component
@DisallowConcurrentExecution
@PersistJobDataAfterExecution
@Slf4j
public class RuleCrawlerJob implements Job {

}
```

::: warning  JobDetail中的 durable requestRecovery屬性

>  如果一个任务durable=false，那么当没有Trigger关联它的时候，它就会被自动删除 ，默認是false
>  如果一个任务是"requestRecovery"，那么当任务运行过程非正常退出时（比如进程崩溃，机器断电，但不包括抛出异常这种情况），Quartz再次启动时，会重新运行一次这个任务实例。
:::