---
title: python系列(1)-requirements.txt文件使用介绍
tags: [python]
keywords: 'python,requirements.txt'
categories: []
abbrlink: PqA55H5dQg
date: 2021-04-15 09:52:55
description:
cover: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210419092310.png
top_img: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210419092310.png
---

## requirements.txt介绍

requirements.txt 文件里面记录了当前程序的所有依赖包及其精确版本号。类似于node中的`package.json`,类似于java的`pom.xml`,都是用于管理当前项目的依赖包。一个requirements.txt只是简单的列出来了当前项目使用的包。

它的语法很简单遵循以下几个规则：

| Requirement specifier | Name     | Description                                                                                                                 |
| --------------------- | -------- | --------------------------------------------------------------------------------------------------------------------------- |
| ==                    | 等于     | 需要完全匹配。例如: requests==2.18.4                                                                                        |
| >                     | 大于     | 使用大于指定版本的任何版本。例如:requests>2.18.4                                                                            |
| >=                    | 大于等于 | 使用大于指定版本的任何版本. 例如: requests>=2.18.4                                                                          |
| <                     | 小于     | 使用小于指定版本的任何版本。例如: requests<2.18.4                                                                           |
| <=                    | 小于等于 | 使用小于或等于指定版本的任何版本。例如: requests<=2.18.4                                                                    |
| ~=                    | 兼容版本 | 使用大于或等于指定版本，但不大于当前版本系列的任何版本。例如: ~=1.4.2 匹配 1.4.2 到 1.4.9) 但是不匹配 1.5.0 |

支持的操作符号如下:

**注意此处的`-e`参数使用的比较多,常用于安装本地的python包**

1. -i, --index-url, 默认是:  https://pypi.org/simple

2. --extra-index-url

3. --no-index

4. -c, --constraint

5. -r, --requirement

6. -e, --editable, 从本地项目路径或VCS网址以可编辑模式（比如 setuptools）安装到项目中。

7. -f, --find-links

8. --no-binary

9. --only-binary

10. --prefer-binary

11. --require-hashes

12. --pre

13. --trusted-host

14. --use-feature



## 1. 由安装包生成对应的requirements.txt文件

执行命令：

```shell
python3 -m pip freeze > requirements.txt
```

而对于使用Pycharm或者IDEA工具的小伙伴可以通过更简单的操作使得根据当前项目已经安装的包自动生成对应的`requirements.txt`文件,操作步骤如下：
![](https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210415100512.png)

在弹出的对话框中可以对生成的requirements.txt文件进行相关的配置：
![](https://resources.jetbrains.com/help/img/idea/2021.1/py_sync_requirements.png)

## 2. 通过requirements.txt安装项目依赖包

执行命令：

```shell
pip install -r requirements.txt
```

## 参考链接

- [Use requirements.txt in Pycharm](https://www.jetbrains.com/help/pycharm/managing-dependencies.html)
- [Requirements.Txt Syntax](https://docs.activestate.com/platform/projects/requirements-txt/)
- [Requirements File Format](https://pip.pypa.io/en/stable/reference/pip_install/#requirements-file-format)
