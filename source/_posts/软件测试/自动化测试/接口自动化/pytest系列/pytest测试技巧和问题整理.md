---
title: Pytest测试技巧和问题整理
tags: [python, pytest]
keywords: 'python,pytest'
categories: []
abbrlink: WSHjL5hXZo
date: 2021-04-14 23:12:02
description:
cover: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414092451.png
top_img: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414092451.png
---

## pytest如何重新运行失败的test case？

有两种方式：

第一种使用flaky装饰器：

```shell
@flaky(max_runs=3, min_passes=2)
def test_lookup_all_request(self, request_type, status):
```

第二种方式使用pytest的内置参数：

```shell
pytest --lf, --last-failed   rerun only the tests that failed at the last run (or all if none failed)
pytest --ff, --failed-first  run all tests but run the last failures first. This may re-order tests and thus lead to repeated fixture setup/teardown
pytest --nf, --new-first     run tests from new files first, then the rest of the tests sorted by file mtime
```
如果是通过docker来运行脚本，需要在`Dockerfile`中如下配置pytest的参数：

```shell
ENTRYPOINT ["pytest", "-s", "-p", "no:logging", "-p", "no:warnings", "--last-failed", "--showlocals"]
```



## cx_oracle提示错误Oracle Database error: DPI-1047: cannot locate a 64-bit Oracle Client library

Q：Oracle Database error：DPI-1047: cannot locate a 64-bit Oracle Client library
![](https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210422180415.png)

A: 解决方案，重复一下的步骤：

```shell
$ python -m pip install cx_Oracle --upgrade
$ mkdir ~/lib
$ ln -s ~/instantclient_19_8/libclntsh.dylib ~/lib/

or

$ cp ~/instantclient_19_8/{libclntsh.dylib.19.1,libclntshcore.dylib.19.1,libnnz19.dylib,libociei.dylib} ~/lib/
```

## cx_oracle报错“libociicus.dylib” cannot be opened because the developer cannot be verified

Q：运行报错： “libociicus.dylib” cannot be opened because the developer cannot be verified. 
![](https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210422181124.png)

A：打开mac的控制台执行命令： `sudo spctl --master-disable`, 这样可以允许高权限运行脚本。

## pytest如何实时打印日志？

Q: I cannot see the print and logger output until the test is over. In practice, I need to see all of them in real time

A: 按照官方的一个解释说明 [pytest live log](https://docs.pytest.org/en/latest/how-to/logging.html?highlight=live%20log),可以使用如下解决方案：
Pytest captures your output and your logging to display it only when your test fails. It's not a bug, it's a feature (although an unwanted one as far as I'm concerned)

You can disable the stdout/stderr capture with `-s` and disable the logs capture with `-p no:logging`. Then you will see the test output and the test logs in real time.

You can add `-s -p no:logging` to "**Additional Arguments**" in your Run Configuration or Run Configuration Template for pytest.

## 如何产生本地的allure报告？

1. 运行pytest脚本的时候加上对应的参数： `pytest --alluredir=allure-results`
2. 切换到上面设置的对应的`allure-results`目录，执行如下命令启动allure server：

```shell
allure serve allure-results 
```

上面会输出对应的日志：

```
(pytest21) alter@% allure serve allure-results 
 
Generating report to temp directory...
 
Report successfully generated to /var/folders/np/323232323/T/31022eeee3098582518/allure-report
 
Starting web server...
 
2020-09-21 15:07:51.870:INFO::main: Logging initialized @6746ms to org.eclipse.jetty.util.log.StdErrLog
 
Server started at <http://192.168.1.4:52268/>. Press <Ctrl+C> to exit
```


## 参考资料

- [Show logging output when using pytest](https://intellij-support.jetbrains.com/hc/en-us/community/posts/360007644040-Show-logging-output-when-using-pytest)




