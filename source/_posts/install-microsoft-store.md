---
title: 微软商店 Microsoft Store 的安装
math: true
hide: false
date: 2022-10-28 20:43:31
updated: 2022-10-28 20:48:54
excerpt: 当安装了简洁版的 windows 系统时，想要安装微软商店 Microsoft Store 的方法。
categories: 
- 教程
- 记录
tags:
- install
index_img:
banner_img:
sticky:
---

### 问题由来

简单说就是，当安装了比较干净的 windows 系统，如 `Windows 10 LTSC`，系统中没有类似于 Microsoft Store、图片查看器等等工具，但是又迫切的想要使用 Microsoft Store 用来下载或者安装某些软件时，就需要使用到 Microsoft Store。

### 问题解决

啥不会就 Goolge。

一番 Google 下来也看到了不少的方法：
1. 打开 powershell 执行一系列命令——失败
   命令应该是可以的，不过并没有细究失败原因
2. 打开某网站下载 Microsoft Store 软件包 —— 失败
   这个应该也是可以的马，但是看他们说还需要安装一些依赖，有些复杂，咱暂时有些急迫去解决该问题，也就没有细究。
3. github 上有个项目傻瓜式安装
   这个就是真简单了，下载包，根据指示可以一键安装。

咱就简单说明一下方法三。

首先咱先附上该项目的地址：[LTSC-Add-MicrosoftStore](https://github.com/kkkgo/LTSC-Add-MicrosoftStore)

项目名字也是非常直白，针对 LTSC 的 Windows 版本增加 Microsoft Store。

![项目情况](https://raw.githubusercontent.com/Muxiner/BlogImages/main/posts/20221028210543-ltsc-add-ms.png)

项目实现原理也十分明了，就是将 Microsoft Store 安装所需要的包以及依赖给咱准备好，同时还有 App Installer / Purchase App / Xbox 等安装需要的包以及依赖，然后编写一个 CMD 命令脚本，傻瓜式安装。

项目还提醒了：

> 如果您不想安装 App Installer / Purchase App / Xbox，请在运行安装之前删除对应的. appxbundle 后缀的文件。
> 但是，如果您**计划安装游戏，或带有购买选项的应用**，则不要删除。

所以基本上还是不需要删除什么文件的。

### 解决步骤

1. 访问项目地址，下载项目文件
   + [LTSC-Add-MicrosoftStore](https://github.com/kkkgo/LTSC-Add-MicrosoftStore)
   + [下载地址](https://github.com/lixuy/LTSC-Add-MicrosoftStore/archive/2019.zip)：点击直接下载文件。
2. 解压文件
3. 根据自身情况删除部分文件，或是不做修改
4. 以**管理员身份**运行 `Add-Store.cmd`
5. 打开 Microsoft Store 检查安装是否成功

{% note info %}
 + 如果装完之后商店仍然打不开，请先重启试试。
 + 如果仍然不行，请以管理员身份打开命令提示符并运行以下命令之后，然后再重启试试。
    
    ```
    PowerShell -ExecutionPolicy Unrestricted -Command "& {$manifest = (Get-AppxPackage Microsoft.WindowsStore).InstallLocation + '\AppxManifest.xml' ; Add-AppxPackage -DisableDevelopmentMode -Register $manifest}"
    ```
{% endnote %}

{% note default %}
商店修复：
+ `Win+R` 打开运行，输入 `WSReset.exe` 回车。
  该命令会清空并重置 Windows Store 商店的所有缓存。
{% endnote%}

### 写在后面

用此方法安装的 Microsoft Store 以及其他软件版本教旧，可使用 Microsoft Store 进行更新。