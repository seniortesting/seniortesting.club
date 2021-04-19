---
title: python基础系列(2)-文件操作
tags: [python]
keywords: 'python,file'
categories: []
abbrlink: PxA45H5dQg
date: 2021-04-16 09:52:55
description:
cover: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210419092310.png
top_img: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210419092310.png
---



## 产生一个zip文件，generate a zip file?

```python
        os.chdir(os.path.join(current_dir, 'data'))
        cls.verify_equals(os.getcwd(), os.path.join(current_dir, 'data'), subject='getcwd Check')
        ret = os.system(f"gzip -c {file_name} > {file_name}.zip")
        cls.verify_equals(ret, 0, subject='gzip command return code')
     
```

## 如何获取文件大小， file folder size？

```python
import os
from os.path import join, getsize

# 获取指定路径 path 下的文件的大小，以字节为单位
# 计算机中的单位换算：字节→1024-K→1024-M→1024-G→1024-T…
# 文件大小： 
fsize = os.path.getsize('d:/svn/bin/SciLexer.dll')
f_kb = fsize/float(1024)

# 文件夹大小
def getdirsize(dir):
    size = 0
    for root, dirs, files in os.walk(dir):
        size += sum([getsize(join(root, name)) for name in files])
    return size

# 个性化大小
def StrOfSize(size):
    '''
    example：StrOfSize(11923)
    递归实现，精确为最大单位值 + 小数点后三位
    '''
    def strofsize(integer, remainder, level):
        if integer >= 1024:
            remainder = integer % 1024
            integer //= 1024
            level += 1
            return strofsize(integer, remainder, level)
        else:
            return integer, remainder, level

    units = ['B', 'KB', 'MB', 'GB', 'TB', 'PB']
    integer, remainder, level = strofsize(size, 0, 0)
    if level+1 > len(units):
        level = -1
    return ( '{}.{:>03d} {}'.format(integer, remainder, units[level]) )


```