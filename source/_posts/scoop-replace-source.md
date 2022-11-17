---
title: Windows 包管理工具 Scoop 更换国内可用源
hide: false
date: 2022-11-17 19:17:24
updated: 2022-11-17 19:25:45
excerpt: 你好
categories:
- 记录
tags:
- Scoop
index_img:
banner_img:
sticky:
---

## 为什么要更换源

Windows 的命令行包管理器 Scoop 使用起来就非常的好用，但是，但是，但是，由于 github 被一道神秘力量阻挡在外，而 Scoop 的安装、安装和更新软件都依赖于 github 上的仓库，于是乎 Scoop 就变得不太好用了起来，当然这不是 Scoop 的问题。

这神秘的力量导致咱更新或安装软件经常性出现网络问题，即使是使用魔法，依然会存在问题，以至于就想更新一下软件，不是网络问题就是更新或下载的速度太慢。

非常的无奈，不过解决办法还是特别的多，一番简单的搜索过后，锁定解决方案 —— 使用国内镜像源/代理加速。

## 代理~~网站~~法器

{% note info %}
+ 简单列举几个站点，不定时检查下来站点的可用性。
+ 站点排序不根据可靠性，随意排的。
个站点详细的使用方式需自行进入官方进行查看。
{% endnote %}

### 镜像网站

暂无。

### 文件加速
3. **ghdl.feizhuqwq.cf** Github 文件加速
    
    地址：[https://ghdl.feizhuqwq.cf/](https://ghdl.feizhuqwq.cf/)
4. **ghproxy.qystudio.ml** Github 文件加速
    
    地址：[https://ghproxy.qystudio.ml/](https://ghproxy.qystudio.ml/)
8. GitHub 文件加速

    地址：[GitHub 文件加速](https://gh.api.99988866.xyz/)

### 加速下载
1. **Github Proxy**
   
   地址：[Github Proxy](https://ghproxy.com/)
   `GitHub` 文件 , `Releases` , `archive` , `gist` , `raw.githubusercontent.com` 文件代理加速下载服务.

2. GitClone

    地址：[GitClone](https://gitclone.com/)
    ​`gitclone.com` 是一个 `github.com` 缓存加速网站，通过对经常访问的 github 的代码库的缓存，加速从 github 的 `git clone` 操作。

3. FastGit UK Document

    地址：[FastGit UK Document](https://doc.fastgit.org/)
    `FastGit` 是一个对于 `GitHub.com` 的镜像加速器。

7. GitHub 加速下载

    地址：[GitHub 加速下载](http://toolwa.com/github/)
2. **pd.zwc365.com** Github 文件加速下载服务
    
    地址：[pd.zwc365.com](https://pd.zwc365.com/)
6. 加速你的 Github

    地址：[加速你的Github](https://github.zhlh6.cn/)

1. FAST-GitHub
   
   地址：[FAST-GitHub](https://fhefh2015.github.io/Fast-GitHub/)

## Scoop 更换源

使用 [Github Proxy](https://ghproxy.com/) 对 Scoop 仓库进行代理加速下载。

> 亲测，使用后效果起飞。Scoop 使用起来都舒服多了。

使用方法很简单，仅需在原 url 前加入 `https://ghproxy.com/` 即可，如 `gie clone`
```bash
# 原：git clone https://github.com/your_name/your_repo
# 使用 github proxy
git clone https://ghproxy.com/https://github.com/your_name/your_repo
```

因而对 Scoop 仓库等等 url 做如下修改：
### Scoop 源

```bash
scoop config SCOOP_REPO 'https://ghproxy.com/ScoopInstaller/Scoop'
```

### bucket 源

先 rm 掉原有的 bucket，然后再添加新的。

**main**
```bash
scoop bucket add main 'https://ghproxy.com/https://github.com/ScoopInstaller/Main'
```

**extras**
```bash
scoop bucket add extras 'https://ghproxy.com/https://github.com/ScoopInstaller/Extras'
```

**versions**
```bash
scoop bucket add versions 'https://ghproxy.com/https://github.com/ScoopInstaller/Versions'
```

**java**
```bash
scoop bucket add java 'https://ghproxy.com/https://github.com/ScoopInstaller/Java'
```

**nirsoft**
```bash
scoop bucket add nirsoft 'https://ghproxy.com/https://github.com/kodybrown/scoop-nirsoft'
```

**nerd-fonts**
```bash
scoop bucket add nerd-fonts 'https://ghproxy.com/https://github.com/matthewjberger/scoop-nerd-fonts'
```

添加其他 bucket 方法同上。

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/posts/scoop-bucket-proxy.png)

## xxxx

有啥问题解决什么问题，问题解决不了，那就解决提出问题的人（doge）。
