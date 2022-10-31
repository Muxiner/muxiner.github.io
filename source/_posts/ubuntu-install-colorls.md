---
title: Ubuntu 安装 Colorls 美化命令行命令 ls
math: true
hide: false
date: 2022-10-31 19:23:03
updated: 2022-10-31 21:02:51
excerpt: Ubuntu 安装 Colorls 美化命令行命令 ls，让 ls 命令输出更加的可观。
categories: 
- 记录
- Ubuntu
tags:
- Ubuntu
- install
index_img:
banner_img:
sticky:
---

先上效果图。
{% note success %}
查看博客站点文件情况。
1. 使用 colorls 查看 站点根目录以及 posts 目录
2. 未使用 colorls，即原 ls 查看 站点根目录以及 posts 目录
{% endnote %}

![使用 colorls 的效果](https://raw.githubusercontent.com/Muxiner/BlogImages/main/posts/20221031210934-use-colorls.png)

![没有使用 colorls 的效果](https://raw.githubusercontent.com/Muxiner/BlogImages/main/posts/20221031211106-not-colorls.png)

可见使用后，结果更加的好看，主要是有不同的**字体颜色**以及显示**文件类型的图标**。

### 项目介绍 —— colorls

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/posts/20221031211723-Color-Ls-github.png)

`Color Ls` 是一个基于 `Ruby` 开发的脚本，能够添加颜色以及图标对 `ls` 结果输出进行着色。

### 安装 colorls

一共三步。

#### 安装 Ruby 以及相关依赖

```bash
sudo apt install ruby ruby-dev ruby-colorize
```
![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/posts/20221031212518-install-ruby.png)

#### 安装并使用 Nerd Fonts

[Nerd Fonts Download](https://www.nerdfonts.com/font-downloads)
<iframe src="https://www.nerdfonts.com/font-downloads" width="100%" height="320" name="topFrame" scrolling="yes"  noresize="noresize" frameborder="0" id="topFrame"></iframe>

选择合适的字体并下载安装。

推荐几个：
+ Cascadia Cove Nerd Font
+ Hack Nerd Font
+ JetBrainsMono Nerd Font

{% note success %}
Windows Terminal 中自带的 `Cascadia Mono` 字体也能用。
{% endnote %}

#### 安装 colorls

```bash
sudo gem install colorls
```
正常情况下，成功安装：
![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/posts/20221031213155-install-colorls-success.png)

那就还有不正常情况：
![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/posts/20221031213856-install-colorls-error.png)

经过一番验证后，初步了解到，这是因为缺少编译程序必须的软件包 —— `build-essential`。

其作用是：**提供编译程序必须软件包的列表信息。**
> 也就是说编译程序有了这个软件包，它才知道，头文件在哪，才知道库函数在哪，还会下载依赖的软件包，最后才组成一个开发环境。

一般来说 Ubuntu 都是自带该包的：
```bash
muxiner@xxxxxxxxxxxxx:~$ sudo apt install build-essential
[sudo] password for muxiner:
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
build-essential is already the newest version (12.9ubuntu3).
0 upgraded, 0 newly installed, 0 to remove and 82 not upgraded.
```

没有的话也可以使用 `sudo apt install build-essential` 进行安装，同时还会安装 C 语言编译器。

然后就可以快乐的安装 colorls 了。

### Colorls 的使用

这个详见 [https://github.com/athityakumar/colorls](https://github.com/athityakumar/colorls)

### 参考
+ [colorls | github](https://github.com/athityakumar/colorls)
+ [Add Bling to the ‘ls’ Bash Command with Colorls](https://www.omgubuntu.co.uk/2017/07/add-bling-ls-bash-command-colorls)
+ [build-essential 的作用](https://www.cnblogs.com/bing-yu12/p/6384447.html)

