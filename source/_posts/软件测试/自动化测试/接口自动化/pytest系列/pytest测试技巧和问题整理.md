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



## pytest如何实时打印日志？

Q: I cannot see the print and logger output until the test is over. In practice, I need to see all of them in real time

A: 按照官方的一个解释说明 [pytest live log](https://docs.pytest.org/en/latest/how-to/logging.html?highlight=live%20log),可以使用如下解决方案：
Pytest captures your output and your logging to display it only when your test fails. It's not a bug, it's a feature (although an unwanted one as far as I'm concerned)

You can disable the stdout/stderr capture with `-s` and disable the logs capture with `-p no:logging`. Then you will see the test output and the test logs in real time.

You can add `-s -p no:logging` to "**Additional Arguments**" in your Run Configuration or Run Configuration Template for pytest.

## 参考资料

- [Show logging output when using pytest](https://intellij-support.jetbrains.com/hc/en-us/community/posts/360007644040-Show-logging-output-when-using-pytest)




