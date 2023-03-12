---
title: Windows10 安装 MSYS2
date: 2023-03-12 11:49:09
updated: 2023-03-12 11:54:11
excerpt: MSYS2 —— Windows 的软件分发和构建平台，是一个为 Windows 操作系统提供类似于 Unix 环境的软件开发环境的软件。
categories: Linux
tags: MSYS2
index_img:
banner_img:
sticky:
---

### MSYS2 是什么

**[MSYS2](https://www.msys2.org/)** 是一个工具和库的集合，为用户提供一个易于使用的环境来构建、安装和运行本机 Windows 软件。

它包括一个名为 [mintty](https://mintty.github.io/) 的`命令行终端`、`bash`、`版本控制系统`如 `git` 和 `subversion`、`工具`如 `tar` 和 `awk`，甚至构建系统如 `autotools`，都是基于修改版的 [Cygwin](https://cygwin.com/) 实现的。尽管其中一些核心部分基于 `Cygwin`，但 `MSYS2` 的主要重点是为本机 `Windows` 软件提供构建环境，`Cygwin` 使用的部分被保持在最小限度。

为了提供易于安装软件包的方式以及保持其更新，MSYS2 提供了一个的包管理系统 —— [Pacman](https://wiki.archlinux.org/index.php/pacman)。

**[MSYS2](https://www.msys2.org/)** 提供了最新的 `GCC`、`mingw-w64`、`CPython`、`CMake`、`Meson`、`OpenSSL`、`FFmpeg`、`Rust`、`Ruby` 等本地构建工具。

{% note info %}

**MSYS2 官方网站介绍**：

**[MSYS2](https://www.msys2.org/)** is a collection of tools and libraries providing you with an easy-to-use environment for building, installing and running native Windows software.

It consists of a command line terminal called [mintty](https://mintty.github.io/), bash, version control systems like git and subversion, tools like tar and awk and even build systems like autotools, all based on a modified version of Cygwin. Despite some of these central parts being based on [Cygwin](https://cygwin.com/), the main focus of MSYS2 is to provide a build environment for native Windows software and the Cygwin-using parts are kept at a minimum. MSYS2 provides up-to-date native builds for GCC, mingw-w64, CPython, CMake, Meson, OpenSSL, FFmpeg, Rust, Ruby, just to name a few.

To provide easy installation of packages and a way to keep them updated it features a package management system called [Pacman](https://wiki.archlinux.org/index.php/pacman), which should be familiar to Arch Linux users. It brings many powerful features such as dependency resolution and simple complete system upgrades, as well as straight-forward and reproducible package building. Our package repository contains [more than 2800 pre-built packages](https://packages.msys2.org/base) ready to install.

For more details see '[What is MSYS2?](https://www.msys2.org/docs/what-is-msys2/)' which also compares MSYS2 to other software distributions and development environments like [Cygwin](https://cygwin.com/), [WSL](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux), [Chocolatey](https://chocolatey.org/), [Scoop](https://scoop.sh/), ... and '[Who Is Using MSYS2?](https://www.msys2.org/docs/who-is-using-msys2/)' to see which projects are using MSYS2 and what for.

{% endnote %}

### MSYS2 的安装

就直接下载文件 —— [msys2-x86_64-20230127.exe](https://github.com/msys2/msys2-installer/releases/download/2023-01-27/msys2-x86_64-20230127.exe)。

> 上面链接可能不是最新的，建议去 MSYS2 官网下载 —— 指个路 —— [MSYS2 Installation](https://www.msys2.org/#installation)
>
> 建议使用魔法下载，不然容易出问题 —— 指下不下来。

下载完成后，点击运行，然后一路点击，需要修改设置的话，自行注意界面就行了。

安装完成后，启动 `MSYS2` 会是一个单独的 `terminal`，我们可以将其使用 `Windows Terminal` 打开 `MSYS2`。


### MSYS2 terminal 的设置

#### Mintty

`MSYS2` 中**默认的终端应用程序**是 [Mintty](https://mintty.github.io/)，并包含在安装程序中。

`MSYS2` 还通过提供相应的 `.ini` 配置文件和分别对应的启动器（msys2{.exe,.ini}/ucrt64{.exe,.ini}/...）提供了一些自定义的 `Mintty` 集成，因此用户可以轻松地配置的环境并将启动器固定到 `Windows` 任务栏。

有关更多详细信息，请参见 [https://github.com/msys2/msys2-launcher](https://github.com/msys2/msys2-launcher) 和 [https://mintty.github.io](https://mintty.github.io)。

#### Windows Terminal

`Windows Terminal` 默认支持 `cmd`、`PowerShell` 和 `WSL`，还可以扩展支持 `MSYS2 shell`。

> Windows Terminal 支持美化，可以让终端更加的好看。

Windows Terminal 的安装，Windows11 是默认安装了的，Windows10 的话可以去 Microsoft Store 进行安装。

在 Windows Terminal 中添加 MSYS2 有两种方法：

{% note danger %}

咱先默认 MSYS2 的安装路径是 `C:\msys64`

{% endnote %}

1. 通过图形化界面点点点：
   
   `设置 > 添加新配置文件 > 新建空的配置文件`，然后就是根据每一行的字段输入内容就行了。

   咱这给予一个示例：
   + **名称**：`UCRT64 | MSYS2`，下拉列表中配置文件显示的名称。
   + **命令行**：`C:/msys64/msys2_shell.cmd -defterm -here -no-start -ucrt64`，在配置文件中所使用的可执行文件。各参数的含义：
     + `C:/msys64/msys2_shell.cmd`: 这是要运行的 `MSYS2 shell` 脚本的路径。
     + `-defterm`: 使用 **Windows 默认终端**作为 shell 的终端，而不是使用 `mintty` 终端。
     + `-here`: 将当前目录设置为 shell 的起始目录。
     + `-no-start`: 不启动 shell 窗口。
     + `-ucrt64`: 使用 `ucrt64.dll` 作为 `C/C++` 运行时库，而不是使用默认的 `msvcrt.dll`。这可以解决一些兼容性问题。

   + **启动目录**：`C:/msys64/home/%USERNAME%`，加载配置文件时启动的目录。
   + **图标**：`C:/msys64/ucrt64.ico`，配置文件中所使用图标的表情符号或者图像文件位置，可自行更换，选择所喜欢的图标。
   
   以上是必要的配置，还有如**选项卡标题**、**以管理员身份运行此配置文件**、**从下拉菜单中隐藏**，可根据自身需要选择。

   **外观**和**高级**属于终端美化，暂不介绍。

2. 通过在 JSON 配置文件敲敲敲：
   
   进入 `设置`，点击 `打开 JSON 文件`，然后找到 `"profiles"` 下面的 `"list"`，仿照其他的 `{}` 的内容进行修改或添加就行了。

   咱继续给个例子：
   ```json
    // defaultProfile: 默认 shell 的 guid，这使 UCRT64 成为默认 shell
    "defaultProfile": "{17da3cac-b318-431e-8a3e-7fcdefe6d114}",
    "profiles": {
    "list":
    [
        // ...
        {
        "guid": "{17da3cac-b318-431e-8a3e-7fcdefe6d114}",
        "name": "UCRT64 / MSYS2",
        "commandline": "C:/msys64/msys2_shell.cmd -defterm -here -no-start -ucrt64",
        "startingDirectory": "C:/msys64/home/%USERNAME%",
        "icon": "C:/msys64/ucrt64.ico",
        },
        {
        "guid": "{71160544-14d8-4194-af25-d05feeac7233}",
        "name": "MSYS / MSYS2",
        "commandline": "C:/msys64/msys2_shell.cmd -defterm -here -no-start -msys",
        "startingDirectory": "C:/msys64/home/%USERNAME%",
        "icon": "C:/msys64/msys2.ico",
        },
        // ...
    ]
    }
   ```
   上述各字段分别是，**全局唯一标识符** —— `guid`、**名称** —— `name`、**命令行** —— `commandline`、**启动目录** —— `startingDirectory`、**图标** —— `icon`。

   {% note info %}
   
   **该配置文件中的命令行默认会启动 `bash shell`。**
   
   要更改默认的登录 shell，请安装相应的 shell 包，并在命令行中附加 -shell 选项。例如，
   + 要将 `fish shell` 设置为默认 shell：
     ```json
     "commandline": "C:/msys64/msys2_shell.cmd -defterm -here -no-start -ucrt64 -shell fish"
     ```
   + 要将 `zsh shell` 设置为默认 shell：
     ```json
     "commandline": "C:/msys64/msys2_shell.cmd -defterm -here -no-start -ucrt64 -shell zsh"
     ```
    {% endnote %}

{% note info %}

有关不同配置文件设置的更多信息，请参见 [Windows Termial 自定义设置](https://learn.microsoft.com/zh-cn/windows/terminal/customize-settings/startup)。

{% endnote %}
