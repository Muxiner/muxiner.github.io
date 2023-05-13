---
title: kex_exchange_identification：远程主机关闭连接
comment: giscus
math: true
hide: false
date: 2023-05-13 21:40:29
updated: 2023-05-13 21:40:29
excerpt: git push 向 GitHub 推送内容时，提示kex_exchange_identification：远程主机关闭连接。
categories: Git
tags: Git
index_img:
banner_img:
sticky:
---

### 问题描述

```zsh
$ git push
kex_exchange_identification: Connection closed by remote host
Connection closed by xx.xxx.xxx.xxx port 22
致命错误：无法读取远程仓库。

请确认您有正确的访问权限并且仓库存在。
```

心血来潮写了点东西到博客，好不容易写完了，推送到 GitHub 时竟然直接报错：`kex_exchange_identification: Connection closed by remote host`，咱也没有干什么呀，怎么就远程主机关闭连接了。

### 问题解决

搜索了许久之后，也是发现了不少的方法，试来试去还是不太行，不少人都提到 —— 关闭科学上网，虽然我试了，但是还是没有卵用。

就这般试了好几次，还是不太行，最后还是看到有人的说到与科学上网有关。

于是乎，就直接操作，最后还是关闭科学上网解决了问题。

### 瞎逼逼

瞎记录点内容，不过好在又让我知道，遇到和 git、GitHub 相关的问题可以去 [GitHub 文档 | 中文](https://docs.github.com/zh) 进行查阅。

### 参考

+ [连接GitHub提示远程主机关闭连接](https://blog.csdn.net/qq_43431735/article/details/106031021)
+ [身份验证 | GitHub 文档](https://docs.github.com/zh/authentication)
