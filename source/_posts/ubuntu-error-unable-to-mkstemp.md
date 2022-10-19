---
title: Ubuntu 出现 Unable to mkstemp 等问题解决
math: true
hide: false
date: 2022-10-19 09:32:41
updated: 2022-10-19 09:32:41
excerpt: 在 ubuntu 更新软件，下载软件时，出现问题 Unable to mkstemp /tmp/clearsigned.message.r1RilL - GetTempFile 等解决办法（疑似误删了/tmp 文件夹）
categories: Linux
tags: 
- BLog
- Ubuntu
index_img:
banner_img:
sticky:
---

### 问题描述

在使用 WSL Ubuntu 进行软件更新或软件下载时，出现如下问题：
```bash
$ sudo apt install xxx
[sudo] password for xxxxxx:
Reading package lists... Error!
E: Unable to mkstemp /tmp/clearsigned.message.r1RilL - GetTempFile (20: Not a directory)
E: The package lists or status file could not be parsed or opened.
```
```bash
$ sudo apt update
E: Unable to mkstemp /tmp/clearsigned.message.u1lbd8 - GetTempFile (20: Not a directory)
E: The package lists or status file could not be parsed or opened.
```

造成软件更新或下载失败。

### 问题解决

想起之前在这 ubuntu 做使用，看到 `/tmp` 非空，且了解到：
> /tmp/    存储系统和用户的临时信息。
就想着删除 `/tmp` 目录下的内容，于是直接动手。

然而，删除完后， `/tmp` 目录就在是出问题：

```bash
$ cd /tmp
-bash: cd: /tmp: Not a directory

$ mkdir -p /tmp
mkdir: cannot create directory ‘/tmp’: File exists
```
刚开始没当回事，以为重启就没事，也就没在乎。

哪知过几天再来使用 ubuntu 时，更新或下载软件时出现上述问题。

然后开始询问度娘，搜索到“误删 `/tmp` 目录”等等的解决方法。

**思路很简单，就是删除 /tmp 再重新创建 /tmp。**

**命令如下：**
```bash
sudo rm -r /tmp
sudo mkdir /tmp
```

