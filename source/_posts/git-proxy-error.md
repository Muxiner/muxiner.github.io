---
title: 使用 Git 时网络问题（代理）解决
math: true
hide: false
date: 2022-09-06 14:06:54
updated: 2022-09-06 14:06:54
excerpt: git 代理问题解决
categories: 
- 水博客
tags:
- Git
index_img:
banner_img:
sticky:
---

### 问题描述

使用 git 命令执行与 github 相关命令失败的错误提示，如下：

```powershell
## station one
OpenSSL SSL_read: Connection was reset, errno 10054

## station two
Failed to connect to github.com port 443 after 21098 ms: Timed out
```

### 问题原因

简而言之，github 被墙，走代理，然而设置不正确。

修改一下就好。

### 问题解决

执行下述命令（根据自身情况做适当修改）：

```powershell
git config --global --unset socks5.proxy
git config --global socks5.proxy 127.0.0.1:xxxx

### xxxx 为端口号
```

{% note primary %}
没法解决问题的话，就得对症下药，如 DNS 问题就干嘛干嘛之类的。
{% endnote %}