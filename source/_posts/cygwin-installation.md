---
title: Cygwin 的安装与配置
math: true
hide: false
date: 2022-11-13 21:04:57
updated: 2022-11-13 21:09:10
excerpt: 在 Windows 10 系统下安装 Cygwin，并进行一下简单的配置。
categories: 
- 记录
- Windows
tags:
- install
- Cygwin
index_img:
banner_img:
sticky:
---

## 什么是 Cygwin

安装之前先简单地介绍一下 `Cygwin` —— **是一个可原生运行于 Windows 系统上的 POSIX 兼容环境**。

> **维基百科**：
> Cygwin 是许多自由软件的集合，最初由 Cygnus Solutions 开发，用于各种版本的 Microsoft Windows 上，运行类 UNIX 系统。Cygwin 的主要目的是通过重新编译，将 POSIX 系统（例如 Linux、BSD，以及其他 Unix 系统）上的软件移植到 Windows 上。

不多比比，直接开整。

## 安装 cygwin

### 下载 cygwin 安装包

官网指路：[Cygwin - Get the Linux feeling on Windows](https://cygwin.com).

进入官网后，找到下方一 `Installing Cygwin` 的地方，点击下方黑体加粗后的链接 - [setup-x86_64.exe](https://cygwin.com/setup-x86_64.exe).

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/Pixiv/installing-cygwin.png)

> 图省事直接点击咱这个 setup-x86_64.exe 就行。

{% note info %}
Use the setup program to perform a **fresh install** or to **update** an existing installation.

当你安装了 Cygwin 后，还可以使用该安装程序进行**更新**和**重新安装**。非常的好用。
{% endnote %}

### 开始安装 cygwin

点击下载好的 [setup-x86_64.exe](https://cygwin.com/setup-x86_64.exe).

> 没有下载还可以再点击一下上述链接，开始下载，完成后开始点击，进行安装。

进入安装界面后，仔细看界面内容进行修改或者是下一步，如：
+ 选择**根目录**，如 `C:\cygwin64`.
+ 选择**本地包目录**，如 `C:\xxxxx\cygwin_download`，自定义的。
+ 设置**网络连接**，如 `系统代理`。
+ 选择**下载站点**，如 `https://mirrors.ustc.edu.cn`.
+ 选择**需要下载或是更新的包**，自行研究。

然后还是下一步安装或是更新 cygwin，直至完成。


## 配置 Cygwin

### 安装命令行软件包管理器 apt-cyg

#### 简单介绍 apt-cyg

`apt-cyg` 是类似与 `apt-get`、`apt`、`yum`、`pacman` 等著名命令行包管理器的命令行包管理器，在 `Cygwin` 下使用。

Github 上托管了 n 种 shell 语言版的 apt-cyg —— [Search apt-cyg | github](https://github.com/search?l=Shell&q=apt-cyg&type=Repositories).

咱们要使用的是搜索结果排行第一的 [transcode-open/apt-cyg](https://github.com/transcode-open/apt-cyg)。
> 其遵循 MIT 开源协议发布，2016 年发布 v1 版本后便再未更新过。
> 它其实就是一个 Shell 脚本，帮助用户查找、安装、卸载软件包，还可以根据文件名称反向查找所属的软件包。

#### 安装 apt-cyg

项目推荐的安装步骤：
1. 下载安装包

    ```bash
    lynx -source rawgit.com/transcode-open/apt-cyg/master/apt-cyg > apt-cyg
    ```
    {% note warning %}
    如果上述命令无法完成下载，则直接使用 `git clone` 进行拉去项目：
    ```bash
    git clone https://github.com/transcode-open/apt-cyg.git apt-cyg
    ```
    {% endnote %}
2. 安装

    ```bash
    install apt-cyg /bin
    ```
    {% note warning %}
    如果使用 `git clone` 下载，则需要先进入 `apt-cyg` 文件夹在进行安装：
    ```bash
    cd apt-cyg
    install apt-cyg /bin
    ```
    {% endnote %}


{% note success %}
使用 [Cygwin系列（八）：命令行软件包管理器apt-cyg | silaoa.github.io](https://silaoa.github.io/2019/2019-05-25-Cygwin%E7%B3%BB%E5%88%97%EF%BC%88%E5%85%AB%EF%BC%89%EF%BC%9A%E5%91%BD%E4%BB%A4%E8%A1%8C%E8%BD%AF%E4%BB%B6%E5%8C%85%E7%AE%A1%E7%90%86%E5%99%A8apt-cyg.html#0x01-%E5%AE%89%E8%A3%85apt-cyg) 内容解释上述命令：

第 1 行是使用 `lynx` 命令将 `apt-cyg` 脚本从网站下载保存至当前目录的 `apt-cyg` 文件。
第 2 行是使用 `install` 命令将 `apt-cyg` 文件安装至 `/bin` 目录下，这一步其实包含了两个动作：
+ 将 `apt-cyg` 文件复制到 `/bin` 目录
+ 增加 `/bin/apt-cyg` 文件可执行权限，这样用户可以在任意位置使用 `apt-cyg` 命令

也可以手工的方式用浏览器下载 `apt-cyg` 脚本至本地，通过 `cp` 命令复制到 `/bin` 目录，再通过 `chmod` 命令增加 `/bin/apt-cyg` 文件可执行权限。

`apt-cyg` 运行过程中依赖 `bash`、`tar`、`wget`、`bzip2`、`gawk`、`xz` 软件包中的命令来完成文件下载、文本分析、压缩/解压等基本功能，需要先在 `Cygwin` 中安装好这些软件包。

其中，`bash`、`tar`、`wget`、`gawk` 属于 `Base` 类，在安装最小系统时已包含；`bzip2`、`xz` 属于 `Archive`类，需要通过 `setup` 先装上，确保后续运行 `apt-cyg` 不出错。

> 突然发现了盲点，我光安装了 `apt-cyg` 没有安装 `bzip2`、`xz`，不过问题不大，再走一遍 `setup-x86_64.exe` 就行了。

> 突然又发现了盲点，上述的几个包都已经安装了，不需要再额外安装。
{% endnote %}

安装后可以使用 `apt-cyg install nano` 命令安装一个 `nano` 编辑器检测 apt-cyg 是否安装成功：
![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/Pixiv/apt-cyg-install-nano.png)

{% note info %}
关于 apt-cyg 的使用可见大佬 **silaoA** 的一篇博客，嗯，还是上述那篇 —— [Cygwin系列（八）：命令行软件包管理器apt-cyg | silaoa.github.io](https://silaoa.github.io/2019/2019-05-25-Cygwin%E7%B3%BB%E5%88%97%EF%BC%88%E5%85%AB%EF%BC%89%EF%BC%9A%E5%91%BD%E4%BB%A4%E8%A1%8C%E8%BD%AF%E4%BB%B6%E5%8C%85%E7%AE%A1%E7%90%86%E5%99%A8apt-cyg.html#0x02-%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8).
{% endnote %}

### 添加环境变量

**为能够在 Windows 环境下的命令行工具直接使用 linux 命令行命令，需在在系统环境变量的 `path` 中添加三条路径：**
1. `C:\cygwin64\bin`
   
   `bin` 为 `binary` 的简写，包含基本的用户命令，可被所有用户使用。包含能够同时被用户和系统管理员使用的命令（二进制程序），并且可以在不挂载任何其它文件系统的情况下使用。
2. `C:\cygwin64\sbin`
   
   存放系统管理员以及其他需要 `root` 权限来运行的工具。
3. `C:\cygwin64\usr\local\bin`
   
   本地站点用户使用的二进制程序文件。

结果如图：

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/Pixiv/cygwin-env-path.png)

{% note info %}
就是将 cygwin 中的**用户可执行文件的目录**以及**系统可执行文件的目录**加入到 Windows 系统环境变量中，以便于 Windows 下的命令行工具调用 cygwin 中的可执行文件，从而在 Windows 下使用 linux 一部分的命令行命令。

+ 用户可执行文件：`/bin`、`/usr/bin`、`/usr/local/bin`.
+ 系统可执行文件：`/sbin`、`/usr/sbin`、`/usr/local/sbin`.
{% endnote %}

{% note primary %}
快捷打开 Windows 环境变量设置的方法：
1. `Win + R` 打开**运行**
2. 输入 `systempropertiesadvanced`，进入**系统属性**界面
3. 点击下方**环境变量**，进入环境变量设置

怎么说，就很快。
{% endnote %}


## 使用 zsh 和 oh my zsh 进行美化

方法与[Ubuntu 安装 zsh + oh my zsh 美化终端](https://muxiner.github.io/2022/11/01/ubuntu-zsh-ohmyzsh/)殊途同归:

### 安装 zsh

```bash
apt-cyg install zsh
```

### 安装 oh my zsh

两个命令二选一：
```bash
sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"

sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
### 修改配置文件 
```bash
nano ~/.bashrc
```
在最后加入 `exec zsh`。

### 修改 oh my zsh 主题
```bash
nano ~/.zshrc
```
找到 `ZSH_THEME` 字段，修改引号内内容为 `robbyrussell`.

### 生效配置

输入命令使配置生效：
```bash
exec zsh
```

{% note default %}
如果还需要安装 zsh 插件，可见 [Ubuntu 安装 zsh + oh my zsh 美化终端](https://muxiner.github.io/2022/11/01/ubuntu-zsh-ohmyzsh/#%E5%AE%89%E8%A3%85-zsh-%E6%8F%92%E4%BB%B6).
{% endnote %}

## 添加 Cygwin 到 Windows Terminal

+ 打开 Windows Terminal；
+ 然后 `设置 > 配置文件 > 添加新配置文件`；
+ 再者 `新建空配置文件`；
+ 对空配置文件进行修改（基础修改）：
  + 名称：`Cygwin`
  + 命令行：`C:\cygwin64\bin\bash.exe -i -l`
  + 启动目录：`C:\cygwin64\home\xxxxxx`
  + 图标：`C:\cygwin64\Cygwin.ico`

{% note info %}
关于命令行的一点点解释，使用大佬 leo3418 [在 Windows Terminal 中使用 Cygwin 命令行或 Git Bash](https://leo3418.github.io/zh/2020/05/24/cygwin-git-bash-in-wt.html) 的部分内容：

首先确定 Cygwin 的安装路径。如果您装的是 64 位版本，那么默认的安装路径是 `C:\cygwin64`。Bash 的可执行文件 `bash.exe` 存在 Cygwin 安装路径下的 `bin` 文件夹中，因此在默认的情况下，该文件的绝对路径是 `C:\cygwin64\bin\bash.exe`。

此处需要注意的一点是，Cygwin 中的 Bash 需要以交互式登录 shell（interactive login shell）的形式启动，否则的话，在运行一些包括 `ls` 在内的基本指令的时候会出 “command not found” 的消息。这个的原因是只有登录 shell 会在启动的时候运行 `/etc/profile`，然后 Cygwin 中的 `/etc/profile` 会把 `/usr/bin` 和 `/usr/local/bin` 加到 `PATH` 环境变量当中。如果开启的不是登录 shell，那么 `/etc/profile` 不会被运行，环境变量也就不会被设置。**启动交互式登录 shell 的方法是使用 -i -l 选项**。如果您想使用别的 shell，那么请自行确认下让 `/usr/bin` 和 `/usr/local/bin` 被添加到 PATH 下的方法。
{% endnote %}

## 最终效果

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/Pixiv/cygwin-installation-final.png)

大功告成。


