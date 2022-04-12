title: 【水博客】解决 Windows Powershell 中 SSH 远程连接失败问题
author: Muxiner
date: 2022-04-12 23:15:10
categories: 水博客
tags:
 - SSH
 - PowerShell
---

## 问题描述

终端出现：

@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@

如图：

[![LnTJd1.md.png](https://s1.ax1x.com/2022/04/12/LnTJd1.md.png)](https://imgtu.com/i/LnTJd1)

> 上图使用的是他人的问题图片，自己这边忘记截图了。

## 问题原因

WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!

就是：

警告：远程主机标识已更改！

此报错是由于远程的主机的公钥发生了变化导致的。 

ssh 服务是通过公钥和私钥来进行连接的，它会把每个曾经访问过计算机或服务器的公钥（public key），记录在 `~/.ssh/known_hosts` 中，当下次访问曾经访问过的计算机或服务器时，ssh 就会核对公钥，如果和上次记录的不同，`OpenSSH` 会发出警告。


## 问题解决

使用命令清楚所连接的 IP：
```shell
ssh-keygen -R xx.xx.xx.xx
# xx.xx.xx.xx 是需要使用 ssh 连接的 ip
```

[![LnXWAH.md.png](https://s1.ax1x.com/2022/04/12/LnXWAH.md.png)](https://imgtu.com/i/LnXWAH)

然后重新连接：

```shell
ssh name@xx.xx.xx.xx -p 22
# name：用户名
# xx.xx.xx.xx: ip
# -p 22：使用端口 22
```
这是会出现有一局：

Are you sure you want to continue connecting (yes/no)?

输入：yes，并按回车。

[![LupgDP.md.png](https://s1.ax1x.com/2022/04/12/LupgDP.md.png)](https://imgtu.com/i/LupgDP)

然后就能够成功建立远程连接，后续输入 `用户名` + `密码` 登录系统就行。

最后，在终端断开 ssh 连接而不关闭终端的方法：

+ 方法一：`Ctrl + D`
+ 方法二：输入 `logout` (部分情况下需要多次输入) 

## 参考
+ [问题解决——SSH时出现WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!](https://blog.csdn.net/wangguchao/article/details/85614914)
+ [在终端ssh的断开方法](https://blog.csdn.net/weixin_39366112/article/details/78175873)
