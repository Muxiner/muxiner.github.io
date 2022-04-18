title: Windows Terminal 使用实况记录
author: Muxiner
date: 2022-04-06 18:11:19
categories: Termnial
tags:
 - Beauty
 - Termnial
 - Blog
---
### 简介
用来记录使用 Windows Terminal 一路上遇到的问题以及解决的办法、附加解决日期。

### 安装
+ Windows 10
	Windows 10 可以从系统自带的 MicroSoft Store 进行下载安装，搜索 Windows Terminal，点击安装即可。
+ Windows 11
	Windows 11 直接自带 Windows Terminal，并将其作为默认的命令行工具——无论是 PowerShell 还是 CMD，或者是用户自己后续安装的如 Git Bash 等等均会直接使用 Windows Terminal 进行打开，怎么说就，十分舒适。

> 总所周知，Windows Terminal 是可以进行美化的，而这意味着什么？
> 我们可以将不忍直视的 CMD 或者 Git Bash 界面做成让我们自己赏心悦目的样子，可以极大的愉悦我们的心情。

### Windows Terminal 美化
#### 配置文件
简单的说就是，Windows Terminal 通过修改**配置文件**中的内容，获得不一样的视觉效果。

配置文件包含三块部分：
1. 常规
2. 外观 —— 设置字体、窗口样式、配色方案、透明度、背景图片等
3. 高级

外观是咱们 Windows Terminal 美化的主战场，主要就是自定义修改**字体**、**配色方案**、**背景图片**、**亚克力效果**（透明度）。

共有两种修改方式：
1. 使用图形界面的设置 —— 就是进入 Windows Terminal 的设置里一点点的调整
2. 修改配置文件（JSON文件）—— 这个会比第一种复杂不少，因为是需要自己文件中的一点点设置啦

不过两者各有所长，至少配置文件可以用来保存设置好的美化方案，方便分享或是重装系统后的恢复。

通过修改上述的几点设置后，咱们的终端界面就会有很大的不同了，看起来就有那么一点点的赏心悦目。

### PowerShell 命令使用
#### 安装 scoop
在 PowerShell 中输入下述代码进行安装（可能需要科学上网）
```PowerShell
 iex (new-object net.webclient).downloadstring('https://get.scoop.sh')
```
输入下述命令可检查 scoop 是否成功安装
```PowerShell
scoop help
```
#### 安装 colortool
安装 colortool 需要通过 scoop 指令
```PowerShell
scoop install colortool
```

### Oh-My-Posh
这个是在 PowerShell 上使用上类似于 [Oh-My-Zsh](https://ohmyz.sh/) 的 主题引擎 。
[Oh-My-Posh](https://ohmyposh.dev/) 上的主题看起来似乎还要比 zsh 上的好看不少。

#### 安装
```PowerShell
# 绕过 powershell 执行策略，使其可以顺利执行脚本
Set-ExecutionPolicy Bypass
# posh-git将git信息添加到提示中
Install-Module posh-git -Scope CurrentUser
# oh-my-posh提供主题
Install-Module oh-my-posh -Scope CurrentUser

```
#### 更新
```PowerShell
Update-Module oh-my-posh
```

#### 编辑相应文件
```PowerShell
# 如果之前没有配置文件，就新建一个 Powershell 配置文件
if (!(Test-Path -Path $PROFILE )) { New-Item -Type File -Path $PROFILE -Force }
# 打开配置文件，优先使用 vscode ，其次会使用记事本打开
notepad $PROFILE
# 也可用使用 nano，不过需要先安装，使用 scoop install nano 即可完成安装
# 或者直接去文件夹中寻找
# C:/user/xxxxx/Documents/WindowsPowerShell/MicroSoft.PowerShell_profile.ps1
```
在配置文件中写入如下内容（脚本文件），并保存。
```PowerShell
Import-Module posh-git
Import-Module oh-my-posh
Set-PoshPrompt -Theme capr4n

```
**配置完后**，每次打开 Windows Terminal 中的 Powershell 都会执行脚本文件中的三条命令。

#### 安装字体
![](https://s3.bmp.ovh/imgs/2022/04/06/6daae30b63069edd.png)

当出现上图情况时，说明是当前使用的字体并不适合所使用的主题，因而我们需要安装字体。
之前我使用 YYDS 的搜索所得的结果 —— 安装 [JetBrains Mono](https://www.jetbrains.com/zh-cn/lp/mono/) 好看是好看而且也解决了一部分的不显示问题，但是还是会存在一些图标显示的是方框，因而重新找到了 [nerdfonts](https://www.nerdfonts.com/font-downloads) ，并选择了 **Hasklug Nerd Font** 并进行安装。
> 下载下来的是一个字体的压缩包，里面包含了不同样式的该类字体，选取其中的一个进行安装即可。
> 安装方法：
> 双击想要安装的字体可以进行预览，左上角有“安装”按钮，点击即可安装。

在 Windows Terminal 中使用新字体时，需要重新打开 Terminal 才能使的字体库中显示先安装的字体，然后选择新字体，OVER。

[![qvnStf.md.png](https://s1.ax1x.com/2022/04/06/qvnStf.md.png)](https://imgtu.com/i/qvnStf)



### 参考文档
+ [Windows Terminal 官方文档](https://docs.microsoft.com/zh-cn/windows/terminal/)