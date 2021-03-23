---
title: git常见问题和错误
date: 2021-03-22 22:31:46
tags:
  - git
  - github
  - ssh key
categories: git
keywords: 'git,github,ssh key, git clone'
description: git常见错误整理
abbrlink: git-error
sticky: 100
---

## git错误整理

### 1. Key is invalid. You must supply a key in OpenSSH public key format

Github添加公开秘钥的时候，如果直接粘贴复制往往会收到这样一个报错：

`Key is invalid. You must supply a key in OpenSSH public key format`

这个原因是因为：

直接粘贴复制会破坏.ssh文件的格式
解决办法是：使用cat命令将 `~/.ssh/id_rsa.pub` 内容输出到终端，再拷贝。
`cat ~/.ssh/id_rsa.pub`
