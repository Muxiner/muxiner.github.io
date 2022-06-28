---
title: 【水博客】Ubuntu Update 失败：Release file is not valid yet
math: true
date: 2022-05-09 13:59:13
udpated: 2022-06-28 22:05:22
excerpt: 本文所写记录 Ubuntu 使用过程中的问题 —— Ubuntu Update 失败：Release file is not valid yet。
categories: 
 - linux
 - 水博客
tags:
 - Ubuntu
index_img: 
banner_img: https://w.wallhaven.cc/full/md/wallhaven-mdkjl1.jpg
---

ᕕ( ᐛ )ᕗ

(ノﾟ∀ﾟ)ノ举高高

( へ ﾟ∀ﾟ)べ摔低低

(`ヮ´ ) 开摆！

↙(`ヮ´ )↗ 开摆！

### 问题描述
该问题是在 `Windows` 下使用 `Linux` 子系统 `Ubuntu` 时，执行了 `sudo apt update` 命令后，就出现问题：

![](https://s1.ax1x.com/2022/05/09/OGlyCD.png)

```
E: Release file for https://mirrors.tuna.tsinghua.edu.cn/ubuntu/dists/focal-updates/InRelease is not valid yet (invalid for another 5h 35min 12s). Updates for this repository will not be applied.
E: Release file for https://mirrors.tuna.tsinghua.edu.cn/ubuntu/dists/focal-backports/InRelease is not valid yet (invalid for another 5h 36min 30s). Updates for this repository will not be applied.
E: Release file for https://mirrors.tuna.tsinghua.edu.cn/ubuntu/dists/focal-security/InRelease is not valid yet (invalid for another 5h 34min 27s). Updates for this repository will not be applied.
```

意思就是：**发布文件尚未生效（在另一个 5 小时 35 分钟 12 秒内无效）。不会应用此存储库的更新。**


### 问题原因
经过一番搜索后发现了问题 —— 咱 `Ubuntu` 上的时间与清华大学 `TUNA` 的软件源镜像的时间不一致，咱的系统时间比它慢了几个小时。
> 错误的原因是系统上的时间和现实世界的时间不同。

为啥会出现这种问题呢？

咱电脑安装了双系统的，`windows 11` + `manjaro`，上午的时候玩了一会 `manjaro`，整了一会后，回到 `windows 11`，发现咱的时间晚了 8 小时，但是咱没有注意到时间的变化，就安装了咱们的 `ubuntu`，因而该系统的时间也是跟着咱 `windows 11` 的时间一样，慢了 8 小时。但是这会，咱执行 `sudo apt update` 是没问题的哦。后来咱就发现电脑时间不对，就赶紧更新了电脑时间，后重新启动了 `ubuntu`，仍旧执行了 `sudo apt update` 命令，这会就出现问题了。

提示：**发布文件尚未生效（在另一个 5 小时 35 分钟 12 秒内无效）。不会应用此存储库的更新。**

执行 `date` 命令查看时间：
```
date
```
![](https://munner.coding.net/p/blogpicgo/d/blogimages/git/raw/main/posts/20220628221558.png)

### 问题解决

想要解决问题呀，简单的改一下 `ubuntu` 的时间就好，改成和 `windows 11` 时间一样就行。

执行 `sudo date -s xxxxxx` 设置系统时间
```
sudo date -s 12:40:50
```
![](https://munner.coding.net/p/blogpicgo/d/blogimages/git/raw/main/posts/20220628221120.png)

> 我这知识时间不对，因而仅修改了时间。
> 若是日期也不对就需要执行：
> ```
> sudo date -s 2022-5-9 12:40:50
> ```

![](https://munner.coding.net/p/blogpicgo/d/blogimages/git/raw/main/posts/20220628222226.png)

OK! 问题成功解决。

(`ヮ´ ) 开摆！

↙(`ヮ´ )↗ 开摆！
