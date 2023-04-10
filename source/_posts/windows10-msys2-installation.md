---
title: Windows10 安装 MSYS2
date: 2023-03-12 11:49:09
updated: 2023-04-10 15:08:16
excerpt: MSYS2 —— Windows 的软件分发和构建平台，是一个为 Windows 操作系统提供类似于 Unix 环境的软件开发环境的软件。
categories: Linux
tags: MSYS2
index_img:
banner_img:
sticky:
---

## 1. MSYS2 是什么 

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

## 2. MSYS2 的安装

就直接下载文件 —— [msys2-x86_64-20230127.exe](https://github.com/msys2/msys2-installer/releases/download/2023-01-27/msys2-x86_64-20230127.exe)。

> 上面链接可能不是最新的，建议去 MSYS2 官网下载 —— 指个路 —— [MSYS2 Installation](https://www.msys2.org/#installation)
>
> 建议使用魔法下载，不然容易出问题 —— 指下不下来。

下载完成后，点击运行，然后一路点击，需要修改设置的话，自行注意界面就行了。

安装完成后，启动 `MSYS2` 会是一个单独的 `terminal`，我们可以将其使用 `Windows Terminal` 打开 `MSYS2`。


## 3. pacman 更换源

一般的，pacman 的镜像源文件位置位于 `/etc/pacman.d/`，所以咱直接去看：
```bash
$ ls /etc/pacman.d
gnupg               mirrorlist.clang64  mirrorlist.mingw32  mirrorlist.msys
mirrorlist.clang32  mirrorlist.mingw    mirrorlist.mingw64  mirrorlist.ucrt64
```
哈哈，镜像源文件还挺多，对应着不同的环境。

以 `mirrorlist.ucrt64` 为例，进行修改，**咱主要使用清华源和科大源，主要是网速问题，那个快哪个好**：
```bash
$ cat /etc/pacman.d/mirrorlist.ucrt64
# See https://www.msys2.org/dev/mirrors

## Primary
Server = https://mirror.msys2.org/mingw/ucrt64/
Server = https://repo.msys2.org/mingw/ucrt64/

## Tier 1
Server = https://mirror.umd.edu/msys2/mingw/ucrt64/
Server = https://mirror.yandex.ru/mirrors/msys2/mingw/ucrt64/
Server = https://download.nus.edu.sg/mirror/msys2/mingw/ucrt64/
Server = https://ftp.acc.umu.se/mirror/msys2.org/mingw/ucrt64/
Server = https://ftp.nluug.nl/pub/os/windows/msys2/builds/mingw/ucrt64/
Server = https://ftp.osuosl.org/pub/msys2/mingw/ucrt64/
Server = https://mirror.internet.asn.au/pub/msys2/mingw/ucrt64/
Server = https://mirror.selfnet.de/msys2/mingw/ucrt64/
Server = https://mirror.ufro.cl/msys2/mingw/ucrt64/
Server = https://mirrors.dotsrc.org/msys2/mingw/ucrt64/
Server = https://mirrors.bfsu.edu.cn/msys2/mingw/ucrt64/
Server = https://mirrors.tuna.tsinghua.edu.cn/msys2/mingw/ucrt64/
Server = https://mirrors.ustc.edu.cn/msys2/mingw/ucrt64/
Server = https://mirror.nju.edu.cn/msys2/mingw/ucrt64/
Server = https://repo.extreme-ix.org/msys2/mingw/ucrt64/
Server = https://mirrors.hit.edu.cn/msys2/mingw/ucrt64/
Server = https://mirror.clarkson.edu/msys2/mingw/ucrt64/
Server = https://quantum-mirror.hu/mirrors/pub/msys2/mingw/ucrt64/
Server = https://mirror2.sandyriver.net/pub/software/msys2/mingw/ucrt64/
Server = https://mirror.archlinux.tw/MSYS2/mingw/ucrt64/

## Tier 2
Server = https://fastmirror.pp.ua/msys2/mingw/ucrt64/
Server = https://ftp.cc.uoc.gr/mirrors/msys2/mingw/ucrt64/
Server = https://mirror.jmu.edu/pub/msys2/mingw/ucrt64/
Server = https://mirrors.piconets.webwerks.in/msys2-mirror/mingw/ucrt64/
Server = https://www2.futureware.at/~nickoe/msys2-mirror/mingw/ucrt64/
Server = https://mirrors.sjtug.sjtu.edu.cn/msys2/mingw/ucrt64/
Server = https://mirrors.bit.edu.cn/msys2/mingw/ucrt64/
Server = https://repo.casualgamer.ca/mingw/ucrt64/
Server = https://mirrors.aliyun.com/msys2/mingw/ucrt64/
Server = https://mirror.iscas.ac.cn/msys2/mingw/ucrt64/
Server = https://mirrors.tencent.com/msys2/mingw/ucrt64/
```
基本上所有镜像源都有，不过弱水三千咱只取一瓢，就选**科大源**吧，原因呀。就是快：

把除科大源的都给注释掉就行：
```bash
# See https://www.msys2.org/dev/mirrors

## Primary
# Server = https://mirror.msys2.org/mingw/ucrt64/
# Server = https://repo.msys2.org/mingw/ucrt64/

## Tier 1
# # Server = https://mirror.umd.edu/msys2/mingw/ucrt64/
# Server = https://mirror.yandex.ru/mirrors/msys2/mingw/ucrt64/
# Server = https://download.nus.edu.sg/mirror/msys2/mingw/ucrt64/
# Server = https://ftp.acc.umu.se/mirror/msys2.org/mingw/ucrt64/
# Server = https://ftp.nluug.nl/pub/os/windows/msys2/builds/mingw/ucrt64/
# Server = https://ftp.osuosl.org/pub/msys2/mingw/ucrt64/
# Server = https://mirror.internet.asn.au/pub/msys2/mingw/ucrt64/
# Server = https://mirror.selfnet.de/msys2/mingw/ucrt64/
# Server = https://mirror.ufro.cl/msys2/mingw/ucrt64/
# Server = https://mirrors.dotsrc.org/msys2/mingw/ucrt64/
# Server = https://mirrors.bfsu.edu.cn/msys2/mingw/ucrt64/
# Server = https://mirrors.tuna.tsinghua.edu.cn/msys2/mingw/ucrt64/
Server = https://mirrors.ustc.edu.cn/msys2/mingw/ucrt64/
# Server = https://mirror.nju.edu.cn/msys2/mingw/ucrt64/
# Server = https://repo.extreme-ix.org/msys2/mingw/ucrt64/
# Server = https://mirrors.hit.edu.cn/msys2/mingw/ucrt64/
# Server = https://mirror.clarkson.edu/msys2/mingw/ucrt64/
# Server = https://quantum-mirror.hu/mirrors/pub/msys2/mingw/ucrt64/
# Server = https://mirror2.sandyriver.net/pub/software/msys2/mingw/ucrt64/
# Server = https://mirror.archlinux.tw/MSYS2/mingw/ucrt64/

## Tier 2
# Server = https://fastmirror.pp.ua/msys2/mingw/ucrt64/
# Server = https://ftp.cc.uoc.gr/mirrors/msys2/mingw/ucrt64/
# Server = https://mirror.jmu.edu/pub/msys2/mingw/ucrt64/
# Server = https://mirrors.piconets.webwerks.in/msys2-mirror/mingw/ucrt64/
# Server = https://www2.futureware.at/~nickoe/msys2-mirror/mingw/ucrt64/
# Server = https://mirrors.sjtug.sjtu.edu.cn/msys2/mingw/ucrt64/
# Server = https://mirrors.bit.edu.cn/msys2/mingw/ucrt64/
# Server = https://repo.casualgamer.ca/mingw/ucrt64/
# Server = https://mirrors.aliyun.com/msys2/mingw/ucrt64/
# Server = https://mirror.iscas.ac.cn/msys2/mingw/ucrt64/
# Server = https://mirrors.tencent.com/msys2/mingw/ucrt64/
```

其他的镜像源文件以此重复上述注释就行，因为无论在哪个环境模式下执行 `pacman -Syyu` 等等之类的命令都是同步更新所有环境的软件包数据库。

所以所以，统统换源。

然后：
```bash
pacman -Syyu
```


## 4. MSYS2 中的环境

当咱们安装完 MSYS2 后就发现好几个应用，MSYS2 带有不同的后缀如 `CLANG64`、`CLANG32`、`CLANGARM64`、`MINGW32`、`MINGW64`、`MSYS`、`UCRT64`等。

都是些啥，区别是什么。

MSYS2 提供了不同的**环境/子系统**，首先用户需要决定要使用哪个环境。

这些环境之间的区别主要在于**环境变量**、**默认编译器**/**链接器**、**架构**、使用的**系统库**等方面。
+ `environment variables`：环境变量
+ `default compilers/linkers`：默认编译器/链接器
+ `architecture`：架构
+ `system libraries used etc`：使用的系统库

**如果不确定，建议选择 `UCRT64` 环境。**

MSYS 环境包含基于类 `Unix/cygwin` 的工具，存储在 `/usr` 目录下，并且它是特殊的，因为它始终处于活动状态。

所有其他环境都继承自 `MSYS` 环境并在其基础上添加各种功能。

例如，在 `UCRT64` 环境中，`$PATH` 变量以 `/ucrt64/bin:/usr/bin` 开头，因此可以使用所有 `ucrt64` 和 `msys` 工具。

**各环境及其细节的简单展示**：
|                                                                           |    Name    |    Prefix     | Toolchain | Architecture | C Library | C++ Library |
| :-----------------------------------------------------------------------: | :--------: | :-----------: | :-------: | :----------: | :-------: | :---------: |
|  <img src="https://www.msys2.org/docs/msys.png" width="30" height="30">   |    MSYS    |    `/usr`     |    gcc    |    x86_64    |  cygwin   |  libstdc++  |
| <img src="https://www.msys2.org/docs/ucrt64.png" width="30" height="30">  |   UCRT64   |   `/ucrt64`   |    gcc    |    x86_64    |   ucrt    |  libstdc++  |
| <img src="https://www.msys2.org/docs/clang64.png" width="30" height="30"> |  CLANG64   |  `/clang64`   |   llvm    |    x86_64    |   ucrt    |   libc++    |
| <img src="https://www.msys2.org/docs/clang64.png" width="30" height="30"> | CLANGARM64 | `/clangarm64` |   llvm    |   aarch64    |   ucrt    |   libc++    |
| <img src="https://www.msys2.org/docs/clang32.png" width="30" height="30"> |  CLANG32   |  `/clang32`   |   llvm    |     i686     |   ucrt    |   libc++    |
| <img src="https://www.msys2.org/docs/mingw64.png" width="30" height="30"> |  MINGW64   |  `/mingw64`   |    gcc    |    x86_64    |  msvcrt   |  libstdc++  |
| <img src="https://www.msys2.org/docs/mingw32.png" width="30" height="30"> |  MINGW32   |  `/mingw32`   |    gcc    |     i686     |  msvcrt   |  libstdc++  |

活动环境是通过 `MSYSTEM` **环境变量**选择的。

#### GCC vs LLVM/Clang

GCC、LLVM/Clang 都是是默认的编译器/工具链，用于在各自的存储库中构建所有软件包。

+ 基于 GCC 的环境：
  + 目前被广泛测试和使用
  + 支持 `Fortran`
  + 虽然 `MINGW` 环境中也存在 `Clang` 软件包，但该软件包仍使用 `GNU` 链接器和 `GNU C++` 库。在某些情况下，例如上游开发者更喜欢 `Clang` 而不是 `GCC`，也会使用 `Clang` 来构建软件包。
+ 基于 LLVM/Clang 的环境：
  + 仅使用 `LLVM` 工具，`LLD` 作为链接器，`LIBC++` 作为 `C++` 标准库
  + `Clang` 提供 `ASAN` 支持
  + 本地支持 `TLS` —— 线程本地存储（Thread-local storage）
  + `LLD` 比 `LD` 更快，但不支持 `LD` 支持的所有功能
  + 某些工具缺乏与等效的 `GNU` 工具相同的功能
  + Microsoft Windows 10 支持 `ARM64/AArch64` 架构

#### MSVCRT vs UCRT

MSVCRT 和 UCRT 是在 Microsoft Windows 上的 C 标准库变体。

+ **MSVCRT（Microsoft Visual C++ Runtime）** 在所有 Microsoft Windows 版本上默认可用，但由于向后兼容性问题而停留在过去，不兼容 `C99`，并且缺少一些功能：
  + 例如，它不兼容 `C99` 的 `printf()` 函数族，但是...
  + `mingw-w64` 提供了替代函数，在许多情况下使事情兼容 `C99`
  + 不支持 `UTF-8` 区域设置
  + 使用 `MSVCRT` 链接的二进制文件不应与使用 `UCRT` 的二进制文件混合使用，因为内部结构和数据类型不同。（更严格地说，针对不同目标构建的对象文件或静态库不应混合使用。构建为不同 CRT 的 DLL 可以混合使用，只要它们不跨 DLL 边界共享 CRT 对象，例如 FILE*。）同样的规则适用于 `MSVC` 编译的二进制文件，因为 `MSVC` 默认使用 `UCRT`（如果未更改）。
  + 在每个 Microsoft Windows 版本上开箱即用。

+ **UCRT（Universal C Runtime）** 是一个较新版本，也是 Microsoft Visual Studio 默认使用的版本。它应该像使用 `MSVC` 编译代码一样工作和运行。
  + 在构建时和运行时与 `MSVC` 的兼容性更好。
  + 它仅默认在 Windows 10 上提供，对于旧版本，您必须自己提供或取决于安装它的用户。

### MSYS2 切换环境

{% note info %}

想要直接看切换的命令，[点击一下，直接跳转](#env-change)。

{% endnote %}

经过一番简单的研究，如果想要在终端直接切换 MSYS2 的**环境**，使用 `export MSYSTEM=UCRT64` 之类的命令，就只能忽悠自己，该命令只是改变了终端的**提示符(prompt)**处的环境名称：
```bash
Username@Hostname CLANG64 ~
$ export MSYSTEM=UCRT64

Username@Hostname UCRT64 ~
$ echo $PATH | tr ':' '\n'
/clang64/bin
/usr/local/bin
...
```
你使用 `echo $PATH | tr ':' '\n'` 命令查看环境变量，你就发现，这还是 `CLANG64` 的环境变量，说明完全没有切换成功，上述的命令就只是欺骗了你。

{% note indo %}

`echo $PATH | tr ':' '\n'` 命令是将 `echo $PATH` 输出的内容碰到 ":" 替换为 "\n".

`tr` 命令的**第一个参数**是要替换的字符，**第二个参数**是替换成的字符。

就是实现了**每个路径一行输出的效果**。

不然就是：
```bash
Username@Hostname CLANG64 ~
$ echo $PATH
/clang64/bin:/usr/local/bin:/usr/bin:/bin:/c/Windows/System32:/c/Windows:/c/Windows/System32/Wbem:/c/Windows/System32/WindowsPowerShell/v1.0/:/usr/bin/site_perl:/usr/bin/vendor_perl:/usr/bin/core_perl
```

{% endnote %}

回归正题，上述命令效果不明显，咱就去 MSYS2 那找，找到个：
> If you need to start a shell correctly, but none of the ways above suit you, devise your own way based on this knowledge:
> + set `MSYSTEM=...` into the environment, with the value of either `MSYS`, `MINGW32`, or `MINGW64`
> + then run a login shell
> 
> The typical one-liner if your options are limited is `C:\\msys64\\usr\\bin\\env MSYSTEM=MSYS /usr/bin/bash -li`.
>
> 如果以上提到的方法都不适用于你，你可以根据以下知识自己设计启动 shell 的方法：
> + 将 `MSYSTEM=...` 设置为环境变量，并将值设为 `MSYS`、`MINGW32` 或 `MINGW64`
> + 然后启动一个登录 shell
> 
> 如果你的选择受限，一种常见的方法是运行以下一行命令：`C:\\msys64\\usr\\bin\\env MSYSTEM=MSYS /usr/bin/bash -li`

简单介绍一下原理，如何自行设计启动 shell —— **先设置 `MSYSTEM=...` 环境变量，再启动一个登录 shell。**

所以咱们就执行 `env MSYSTEM=UCRT64 /usr/bin/bash -li`...再 `echo $PATH | tr ':' '\n'`：
```bash
Username@Hostname CLANG64 ~
$ env MSYSTEM=UCRT64 /usr/bin/bash -li

Username@Hostname UCRT64 ~
$ echo $PATH | tr ':' '\n'
/ucrt64/bin
/usr/local/bin
...
```
显然，环境切换成功。

等等，咱再试试 `export MSYSTEM=CLANG64`，再执行 `/usr/bin/bash -li`，最后检查成功否 `echo $PATH | tr ':' '\n'`：
```bash
Username@Hostname UCRT64 ~
$ export MSYSTEM=CLANG64

Username@Hostname CLANG64 ~
$ /usr/bin/bash -li

Username@Hostname CLANG64 ~
$ echo $PATH | tr ':' '\n'
/clang64/bin
/usr/local/bin
```
😯 woc，傻逼竟是我自己。

**先设置 `MSYSTEM=...` 环境变量，再启动一个登录 shell。**

咱没有重新启动 bash。没有使用命令重新启动 bash。

结束结束，不多BB。

{% note info %}

再多 BB 一声：

`/usr/bin/bash -li` 是启动一个 Bash shell 的命令。其中 `-l` 选项代表要启动一个 **login shell**，这将读取登录 shell 的启动文件（如 `/etc/profile` 和 `~/.bash_profile`），并在其后面加上 `-i` 选项，表示这是一个交互式的 shell，可以接受来自用户的输入。`-i` 选项通常用于设置别名和环境变量。

加上 `/usr/bin/` 是 bash 的路径，其在环境变量里的话，直接 `bash -li` 就可以。

{% endnote %}

<scan id="env-change" style="font-weight: bold;">更换环境的话直接使用：</scan>

+ `MSYS`
  ```bash
  env MSYSTEM=MSYS /usr/bin/bash -li
  ```
+ `UCRT64`
  ```bash
  env MSYSTEM=UCRT64 /usr/bin/bash -li
  ```
+ `CLANG64`
  ```bash
  env MSYSTEM=CLANG64 /usr/bin/bash -li
  ```
+ `CLANGARM64`
  ```bash
  env MSYSTEM=CLANGARM64 /usr/bin/bash -li
  ```
+ `CLANG32`
  ```bash
  env MSYSTEM=CLANG32 /usr/bin/bash -li
  ```
+ `MINGW64`
  ```bash
  env MSYSTEM=MINGW64 /usr/bin/bash -li
  ```
+ `MINGW32`
  ```bash
  env MSYSTEM=MINGW32 /usr/bin/bash -li
  ```



## 5. MSYS2 terminal 的设置

### Mintty

`MSYS2` 中**默认的终端应用程序**是 [Mintty](https://mintty.github.io/)，并包含在安装程序中。

`MSYS2` 还通过提供相应的 `.ini` 配置文件和分别对应的启动器（msys2{.exe,.ini}/ucrt64{.exe,.ini}/...）提供了一些自定义的 `Mintty` 集成，因此用户可以轻松地配置的环境并将启动器固定到 `Windows` 任务栏。

有关更多详细信息，请参见 [https://github.com/msys2/msys2-launcher](https://github.com/msys2/msys2-launcher) 和 [https://mintty.github.io](https://mintty.github.io)。

### Windows Terminal

`Windows Terminal` 默认支持 `cmd`、`PowerShell` 和 `WSL`，还可以扩展支持 `MSYS2 shell`。

> Windows Terminal 支持美化，可以让终端更加的好看。

Windows Terminal 的安装，Windows11 是默认安装了的，Windows10 的话可以去 Microsoft Store 进行安装。

在 Windows Terminal 中添加 MSYS2 有两种方法：

{% note danger %}

咱先默认 MSYS2 的安装路径是 `C:\msys64`

{% endnote %}

1. **通过图形化界面点点点**：
   
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

2. **通过在 JSON 配置文件敲敲敲**：
   
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

## 6. MSYS2 各环境编译工具的安装

不同的 MSYS 环境需要的编译器等等工具不经相同，所需要安装的包也不经相同，看了让人头大。现简单列举一下各环境所需要的包，嗯，应该说是最基础的包，具体需要哪些包取决于要编译的代码和程序所依赖的库。

以下表格根据各自的环境列出了包名，安装时，通常会使用下面列出的包前缀加完整包名：
|                                                                   |  Name[^1]  |     Package prefix[^2]     |
| :---------------------------------------------------------------: | :--------: | :------------------------: |
|    <img src="https://www.msys2.org/docs/msys.png" width="30"/>    |    MSYS    |            None            |
|  <img src="https://www.msys2.org/docs/mingw64.png" width="30"/>   |  MINGW64   |    `mingw-w64-x86_64-`     |
|   <img src="https://www.msys2.org/docs/ucrt64.png" width="30"/>   |   UCRT64   |  `mingw-w64-ucrt-x86_64-`  |
|  <img src="https://www.msys2.org/docs/clang64.png" width="30"/>   |  CLANG64   | `mingw-w64-clang-x86_64-`  |
|  <img src="https://www.msys2.org/docs/mingw32.png" width="30"/>   |  MINGW32   |     `mingw-w64-i686-`      |
|  <img src="https://www.msys2.org/docs/clang32.png" width="30"/>   |  CLANG32   |  `mingw-w64-clang-i686-`   |
| <img src="https://www.msys2.org/docs/clangarm64.png" width="30"/> | CLANGARM64 | `mingw-w64-clang-aarch64-` |

[^1]: 环境变量 `MSYSTEM`
[^2]: 环境变量 `MINGW_PACKAGE_PREFIX`

然后就是结合之前**环境**信息的表，上述表，以及 `pacman -Ss` 和搜索，给出各环境安装相应的**编译工具链**需要的**包名**：

+ `MSYS`：`None`
+ `MINGW64`：

  `mingw-w64-x86_64-toolchain`，一般直接安装 `mingw-w64-x86_64-gcc`，包管理器就会自动分析其需要的依赖，并进行安装：
  ```bash
  Username@Hostname MINGW64 ~
  $ pacman -S mingw-w64-x86_64-gcc
  正在解析依赖关系...
  正在查找软件包冲突...

  软件包 (15) mingw-w64-x86_64-binutils-2.40-2  mingw-w64-x86_64-crt-git-10.0.0.r234.g283e5b23a-1
              mingw-w64-x86_64-gcc-libs-12.2.0-10  mingw-w64-x86_64-gmp-6.2.1-5
              mingw-w64-x86_64-headers-git-10.0.0.r234.g283e5b23a-1  mingw-w64-x86_64-isl-0.25-1
              mingw-w64-x86_64-libiconv-1.17-3  mingw-w64-x86_64-libwinpthread-git-10.0.0.r234.g283e5b23a-1
              mingw-w64-x86_64-mpc-1.3.1-1  mingw-w64-x86_64-mpfr-4.2.0-1
              mingw-w64-x86_64-windows-default-manifest-6.4-4
              mingw-w64-x86_64-winpthreads-git-10.0.0.r234.g283e5b23a-1  mingw-w64-x86_64-zlib-1.2.13-3
              mingw-w64-x86_64-zstd-1.5.4-1  mingw-w64-x86_64-gcc-12.2.0-10

  全部安装大小：  402.29 MiB
  ```
  还可以根据需要安装如，`mingw-w64-x86_64-make`、 `mingw-w64-x86_64-gdb`、 `mingw-w64-x86_64-cmake`、 `mingw-w64-x86_64-pkg-config` 等包。

+ `MINGW32`：

  `mingw-w64-i686-toolchain`，
  ```bash
  Username@Hostname MINGW32 ~
  $ pacman -S mingw-w64-i686-gcc
  正在解析依赖关系...
  正在查找软件包冲突...

  软件包 (15) mingw-w64-i686-binutils-2.40-2  mingw-w64-i686-crt-git-10.0.0.r234.g283e5b23a-1
              mingw-w64-i686-gcc-libs-12.2.0-10  mingw-w64-i686-gmp-6.2.1-5
              mingw-w64-i686-headers-git-10.0.0.r234.g283e5b23a-1  mingw-w64-i686-isl-0.25-1
              mingw-w64-i686-libiconv-1.17-3  mingw-w64-i686-libwinpthread-git-10.0.0.r234.g283e5b23a-1
              mingw-w64-i686-mpc-1.3.1-1  mingw-w64-i686-mpfr-4.2.0-1
              mingw-w64-i686-windows-default-manifest-6.4-4
              mingw-w64-i686-winpthreads-git-10.0.0.r234.g283e5b23a-1  mingw-w64-i686-zlib-1.2.13-3
              mingw-w64-i686-zstd-1.5.4-1  mingw-w64-i686-gcc-12.2.0-10

  下载大小：       55.12 MiB
  全部安装大小：  392.16 MiB
  ```
  还可以根据需要安装如，`mingw-w64-i686-pkgconf`，`mingw-w64-i686-gdb`，`mingw-w64-i686-make`，`mingw-w64-i686-cmake` 等包。

+ `UCRT64`：
  
  `mingw-w64-ucrt-x86_64-toolchain`，一般直接安装 `mingw-w64-ucrt-x86_64-gcc`，包管理器就会自动分析其需要的依赖，并进行安装：
  ```bash
  Username@Hostname UCRT64 ~
  $ pacman -S mingw-w64-ucrt-x86_64-gcc
  正在解析依赖关系...
  正在查找软件包冲突...

  软件包 (10) mingw-w64-ucrt-x86_64-binutils-2.40-2  mingw-w64-ucrt-x86_64-crt-git-10.0.0.r234.g283e5b23a-1
              mingw-w64-ucrt-x86_64-gmp-6.2.1-5  mingw-w64-ucrt-x86_64-headers-git-10.0.0.r234.g283e5b23a-1
              mingw-w64-ucrt-x86_64-isl-0.25-1  mingw-w64-ucrt-x86_64-mpc-1.3.1-1
              mingw-w64-ucrt-x86_64-mpfr-4.2.0-1  mingw-w64-ucrt-x86_64-windows-default-manifest-6.4-4
              mingw-w64-ucrt-x86_64-winpthreads-git-10.0.0.r234.g283e5b23a-1
              mingw-w64-ucrt-x86_64-gcc-12.2.0-10

  全部安装大小：  393.62 MiB
  ```
  还可以根据需要安装如，`mingw-w64-ucrt-x86_64-make`，`mingw-w64-ucrt-x86_64-gdb`，`mingw-w64-ucrt-x86_64-cmake`，`mingw-w64-ucrt-x86_64-pkgconf` 等包。

+ `CLANG32`：

  `mingw-w64-clang-i686-toolchain`，一般直接安装 `mingw-w64-i686-clang`，包管理器就会自动分析其需要的依赖，并进行安装：
  ```bash
  Username@Hostname CLANG32 ~
  $ pacman -S mingw-w64-clang-i686-clang
  正在解析依赖关系...
  正在查找软件包冲突...

  软件包 (18) mingw-w64-clang-i686-compiler-rt-15.0.7-3  mingw-w64-clang-i686-crt-git-10.0.0.r234.g283e5b23a-1
              mingw-w64-clang-i686-expat-2.5.0-1  mingw-w64-clang-i686-gettext-0.21.1-1
              mingw-w64-clang-i686-headers-git-10.0.0.r234.g283e5b23a-1  mingw-w64-clang-i686-libc++-15.0.7-3
              mingw-w64-clang-i686-libffi-3.4.4-1  mingw-w64-clang-i686-libiconv-1.17-3
              mingw-w64-clang-i686-libunwind-15.0.7-3
              mingw-w64-clang-i686-libwinpthread-git-10.0.0.r234.g283e5b23a-1
              mingw-w64-clang-i686-libxml2-2.10.3-1  mingw-w64-clang-i686-lld-15.0.7-3
              mingw-w64-clang-i686-llvm-15.0.7-3  mingw-w64-clang-i686-winpthreads-git-10.0.0.r234.g283e5b23a-1
              mingw-w64-clang-i686-xz-5.4.1-1  mingw-w64-clang-i686-zlib-1.2.13-3
              mingw-w64-clang-i686-zstd-1.5.4-1  mingw-w64-clang-i686-clang-15.0.7-3

  下载大小：      128.94 MiB
  全部安装大小：  882.98 MiB
  ```
  还可以根据需要安装如，`mingw-w64-clang-i686-pkgconf`，`mingw-w64-clang-i686-make`，`mingw-w64-clang-i686-lldb`，`mingw-w64-clang-i686-cmake` 等包。

+ `CLANG64`：

  `mingw-w64-clang-x86_64-toolchain`，一般直接安装 `mingw-w64-clang-x86_64-clang`，包管理器就会自动分析其需要的依赖，并进行安装：
  ```bash
  Username@Hostname CLANG64 ~
  $ pacman -S mingw-w64-clang-x86_64-clang
  正在解析依赖关系...
  正在查找软件包冲突...

  软件包 (7) mingw-w64-clang-x86_64-compiler-rt-15.0.7-3
            mingw-w64-clang-x86_64-crt-git-10.0.0.r234.g283e5b23a-1
            mingw-w64-clang-x86_64-headers-git-10.0.0.r234.g283e5b23a-1
            mingw-w64-clang-x86_64-libwinpthread-git-10.0.0.r234.g283e5b23a-1
            mingw-w64-clang-x86_64-lld-15.0.7-3
            mingw-w64-clang-x86_64-winpthreads-git-10.0.0.r234.g283e5b23a-1
            mingw-w64-clang-x86_64-clang-15.0.7-3

  全部安装大小：  478.21 MiB
  ```
  还可以根据需要安装如，`mingw-w64-clang-x86_64-make`，`mingw-w64-clang-x86_64-pkgconf`，`mingw-w64-clang-x86_64-lldb`，`mingw-w64-clang-x86_64-cmake` 等包。

+ `CLANGARM64`：
  
  `mingw-w64-clang-aarch64-toolchain`，一般直接安装 `mingw-w64-clang-aarch64-clang`，包管理器就会自动分析其需要的依赖，并进行安装：
  ```bash
  Username@Hostname CLANGARM64 ~
  $ pacman -S mingw-w64-clang-aarch64-clang
  正在解析依赖关系...
  正在查找软件包冲突...

  软件包 (18) mingw-w64-clang-aarch64-compiler-rt-15.0.7-3
              mingw-w64-clang-aarch64-crt-git-10.0.0.r234.g283e5b23a-1  mingw-w64-clang-aarch64-expat-2.5.0-1
              mingw-w64-clang-aarch64-gettext-0.21.1-1
              mingw-w64-clang-aarch64-headers-git-10.0.0.r234.g283e5b23a-1
              mingw-w64-clang-aarch64-libc++-15.0.7-3  mingw-w64-clang-aarch64-libffi-3.4.4-1
              mingw-w64-clang-aarch64-libiconv-1.17-3  mingw-w64-clang-aarch64-libunwind-15.0.7-3
              mingw-w64-clang-aarch64-libwinpthread-git-10.0.0.r234.g283e5b23a-1
              mingw-w64-clang-aarch64-libxml2-2.10.3-1  mingw-w64-clang-aarch64-lld-15.0.7-3
              mingw-w64-clang-aarch64-llvm-15.0.7-3
              mingw-w64-clang-aarch64-winpthreads-git-10.0.0.r234.g283e5b23a-1
              mingw-w64-clang-aarch64-xz-5.4.1-1  mingw-w64-clang-aarch64-zlib-1.2.13-3
              mingw-w64-clang-aarch64-zstd-1.5.4-1  mingw-w64-clang-aarch64-clang-15.0.7-3

  下载大小：      125.33 MiB
  全部安装大小：  861.81 MiB
  ```
  还可以根据需要安装如，`mingw-w64-clang-aarch64-make`，`mingw-w64-clang-aarch64-pkgconf`，`mingw-w64-clang-aarch64-lldb`，`mingw-w64-clang-aarch64-cmake` 等包。

{% note info %}

在 MSYS 环境下，一般需要安装以下工具来支持 **C 语言**的编译：
+ **`gcc` 编译器**：用于编译 C 语言代码。
+ **`make` 工具**：用于自动化构建和编译程序，通常需要根据 `Makefile` 文件来执行构建和编译操作。
+ **`gdb` 调试器**：用于调试程序，可以在程序运行过程中对变量和内存进行查看和修改。
+ **`pkg-config`** 工具：用于检测和获取已安装的库的信息，通常在编译程序时需要指定库的路径和编译选项。

`CMake` 是一款跨平台的开源构建工具，用于管理和构建软件项目。它可以自动生成与操作系统、编译器和库相关的 `Makefile` 或者 `Project` 文件，从而简化了项目的构建和移植。

`CMake` 不直接构建软件，而是通过生成 `Makefile` 或者项目文件来让构建工具完成具体的构建过程。

`CMake` 支持的平台非常广泛，包括 `Windows`、`Linux`、`macOS`、`Android` 等。

{% endnote %}

## 7. 个人 Windows Terminal 的 MSYS2 配置

### 1）安装 zsh

```bash
pacman -S zsh
```

### 2）安装 oh my zsh

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

编辑 oh my zsh 配置文件 `nano ~/.zshrc`：
+ 修改 `ZSH_THEME=ys`
+ 修改插件：
  ```
  plugins=( 
      git
      zsh-autosuggestions
      zsh-syntax-highlighting
      history-substring-search
  )
  ```
  并下载相关代码：
  ```zsh
  git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
  git clone https://github.com/zsh-users/zsh-history-substring-search.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/history-substring-search
  git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
  ```
  下载完成后，执行下一步。
+ 使配置生效：`source ~/.zshrc`
  
### 3）安装 lsd

一个 Rust 编写的 ls 替代品，支持彩色输出、图标显示、Git 状态显示等。

搜索 lsd：
```zsh
$ pacman -Ss lsd
mingw32/mingw-w64-i686-lsd 0.23.1-1
    The next gen ls command (mingw-w64)
mingw64/mingw-w64-x86_64-lsd 0.23.1-1
    The next gen ls command (mingw-w64)
ucrt64/mingw-w64-ucrt-x86_64-lsd 0.23.1-1
    The next gen ls command (mingw-w64)
clang32/mingw-w64-clang-i686-lsd 0.23.1-1
    The next gen ls command (mingw-w64)
clang64/mingw-w64-clang-x86_64-lsd 0.23.1-1
    The next gen ls command (mingw-w64)
```

有不同版本的 lsd。不过还是推荐使用 rust 安装或者直接编译：

安装 rust (ucrt 环境)：
```zsh
pacman -S mingw-w64-ucrt-x86_64-rust
```
使用 cargo 命令安装 lsd：
```zsh
cargo install lsd
```
如果想安装最新的 lsd：
```
cargo install --git https://github.com/Peltoche/lsd.git --branch master
```
如果不出意外的话，这样应该就能直接使用 lsd。

如果出现问题，就自行解决吧。
同时也可以自行编译：
```zsh
git clone https://github.com/lsd-rs/lsd.git
## 上述克隆不了，可使用下述命令
## git clone https://ghproxy.com/github.com/lsd-rs/lsd.git
```
开始编译：
```zsh
cd lsd
cargo build
```

更多信息详见：[lsd | github](https://github.com/lsd-rs/lsd)

{% note info %}

如果提示添加 cargo 路径到环境变量，那就添加 cargo 路径到环境变量：
```zsh
export PATH="$PATH:/c/Users/USERNAME/.cargo/bin"
```
添加在 `.bashrc` 或者 `.zshrc` 文件中。

{% endnote %}

### 3）使用 Visual Studio Code 打开文件或文件夹

直接让 MSYS 使用 Windows 安装的 Visual Studio Code 就行，将 VS code 的路径添加到环境变量中：
```zsh
export PATH="$PATH:/c/Program Files (x86)/Microsoft VS Code/bin"
```
或者是：
```zsh
export PATH="$PATH:/c/Users/$USER/AppData/Local/Programs/Microsoft VS Code/bin"
```
根据自身情况进行修改。

将上述加入 `~/.zshrc` 中。
最后再生效：
```zsh
source ~/.zshrc
```

### 4）安装 node.js、 npm、 yarn 

先更新软件源：
```zsh
pacman -Syu
```
然后根据自己 Msys2 的环境安装 node.js，比如安装 UCRT64 环境的：
```zsh
pacman -S mingw-w64-ucrt-x86_64-nodejs
```
> 如果是其他环境的 node.js 安装，就先搜索都有什么 node.js 可以安装：
> ```zsh
> pacman -Ss nodejs
> ```
> 然后选择需要的 node.js 进行安装。

npm 会和 node.js 一起安装，当安装完 node.js 时，npm 也会安装完，可以使用 `npm -v` 检测是否安装完成。

使用 `node -v` 检测 node.js 是否安装成功。

安装 yarn 的话使用：
```zsh
npm install -g yarn
```
检测 yarn 是否安装成功 `yarn -v`。

好家伙，结果给我返回一个：**zsh: command not found: yarn**，仔细一看发现应该是 npm 的安装路路径并不在 PATH 中，看来还需要小小设置一下，然后经查询可以使用下述命令查询 npm 安装路径：
```zsh
npm root -g
```
返回给我 `C:\msys64\ucrt64\lib\node_modules`，那咱就在 ~/.zshrc 文件中添加一行:
```.zshrc
export PATH="$PATH:/ucrt64/lib/node_modules"
```
再使文件生效。`yarn -v` 继续检测，好家伙还有问题 —— zsh: permission denied: yarn，咱知道这是没有 yarn 的可执行权限，一般都是加上 `sudo` 命令就好了，不过咱们 msys2 中没有 `sudo` 命令，害，咋回事呢。先不管这个吧，咱先去 npm 安装路径里看看：
```zsh
$ ls /ucrt64/lib/node_modules/                 
 corepack   hexo-cli   npm   yarn
```
> 咱的 ls 是给 lsd 加上别名了。`alias ls="lsd"`

说明咱是安装了 yarn 的，我还安装了 hexo-cil 呢，再进去看看：
```zsh
$ ls /ucrt64/lib/node_modules/yarn    
 bin   lib   LICENSE   package.json   preinstall.js   README.md
```
还有个可执行文件的文件夹，再进去看看：
```zsh
$ ls /ucrt64/lib/node_modules/yarn/bin
 yarn   yarn.cmd   yarn.js   yarnpkg   yarnpkg.cmd
```
有个 yarn 文件呀，看看文件类型：
```zsh
$ file /ucrt64/lib/node_modules/yarn/bin/yarn
/ucrt64/lib/node_modules/yarn/bin/yarn: POSIX shell script, ASCII text executable
```
这是一个 ASCII 码编写的 POSIX shell 脚本文件，其中包含了一些 Linux/Unix 系统下可执行的 shell 命令。

执行一下看看：
```zsh
$ /ucrt64/lib/node_modules/yarn/bin/yarn -v
1.22.19
```

是可以的哦。难道说是因为可执行文件太深了？
将 `/ucrt64/lib/node_modules/yarn/bin` 加入环境变量试试，在 `~/.zshrc` 文件加入下面内容，并生效：
```zsh
export PATH="$PATH:/ucrt64/lib/node_modules/yarn/bin"
```
看看能使用 yarn 了没：
```zsh
$ yarn -v
1.22.19
```
好家伙，成了，但是这也太麻烦了吧，我是用 npm 安装应用后，还得添加路径到环境变量，这也太麻烦了。

stackoverflow 里有多个回答，其中有一个就是要使用 Windows 安装的 node.js 和 npm 然后并添加 node.js 和 npm 的安装路径，二者默认的路径是：
+ `node.js`: `C:\Program Files\nodejs`，包含 `node`、`npm`。
+ `npm`: `C:\Users\<USERNAME>\AppData\Roaming\npm`，这是使用 `npm install xxxx` 后所安装应用的安装位置。

我查看自己 Windows 10 中的上述路径的文件，差不多就如我所说了，有 npm 以及使用 npm 安装的应用。咱是用 msys2 查看一下都有啥：
```zsh
$ ls /c/Program\ Files/nodejs
 node_modules   corepack   corepack.cmd   install_tools.bat   node.exe   node_etw_provider.man   nodevars.bat   npm   npm.cmd   npx   npx.cmd

$ ls /c/Program\ Files/nodejs/node_modules
 corepack   npm

$ ls /c/Program\ Files/nodejs/node_modules/npm
 bin   docs   lib   man   node_modules   index.js   LICENSE   npmrc   package.json   README.md

$ ls /c/Program\ Files/nodejs/node_modules/npm/bin
 node-gyp-bin   npm   npm-cli.js   npm.cmd   npx   npx-cli.js   npx.cmd
```
尝试执行一下 `npm -v` 命令，执行的是上述 Windows 中的 npm:
```zsh
$ /c/Program\ Files/nodejs/node_modules/npm/bin/npm -v
node:internal/modules/cjs/loader:1078
  throw err;
  ^

Error: Cannot find module 'C:\msys64\ucrt64\bin\node_modules\npm\bin\npm-cli.js'
    at Module._resolveFilename (node:internal/modules/cjs/loader:1075:15)
    at Module._load (node:internal/modules/cjs/loader:920:27)
    at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:81:12)
    at node:internal/main/run_main_module:23:47 {
  code: 'MODULE_NOT_FOUND',
  requireStack: []
}

Node.js v18.15.0
Could not determine Node.js install directory
```
看来是之前安装的 node.js 和 Windows 下的冲突了，把已经安装的卸载：`pacman -Rns mingw-w64-ucrt-x86_64-nodejs` 连同依赖也都删除了，再把之前所添加的和 npm 相关的环境变量也删除，并使 `.zshrc` 文件生效，再执行 `/c/Program\ Files/nodejs/node_modules/npm/bin/npm -v`:
```zsh
$ /c/Program\ Files/nodejs/node_modules/npm/bin/npm -v
9.3.1
```
OK，看来是冲突解决了，那再将上述所说的 Windows 的 node.js 和 npm 路径添加到 msys2 的环境变量：
```zsh
export PATH="$PATH:/c/Program Files/nodejs"
export PATH="$PATH:/c/Users/<USERNAME>/AppData/Roaming/npm"
```
> <USERNAME> 是自己 Windows 的用户名哦，注意一下。

然后再试 `.zshrc` 文件生效。

```zsh
$ node -v
v18.14.0

$ npm -v 
9.3.1

$ yarn -v
1.22.19

$ hexo -v
INFO  Validating config
hexo: 6.3.0
hexo-cli: 4.3.0
os: win32 10.0.19044
node: 18.14.0
v8: 10.2.154.23-node.22
uv: 1.44.2
zlib: 1.2.13
brotli: 1.0.9
ares: 1.18.1
modules: 108
nghttp2: 1.51.0
napi: 8
llhttp: 6.0.10
uvwasi: 0.0.14
acorn: 8.8.1
simdutf: 3.1.0
undici: 5.14.0
openssl: 3.0.7+quic
cldr: 42.0
icu: 72.1
tz: 2022g
unicode: 15.0
ngtcp2: 0.8.1
nghttp3: 0.7.0
```
好哦，显而易见的，这养的方法比之前使用包管理器 `pacman` 安装的方便多了，只需要一次性添加两条环境变量就好了，不像之前 npm 安装一次就需要添加一次环境变量。

哦，再看一下 npm 安装路径里都有什么：
```zsh
$ ls /c/Users/<USERNAME>/AppData/Roaming/npm
 etc   node_modules   hexo   hexo.cmd   hexo.ps1   vue   vue.cmd   vue.ps1   yarn   yarn.cmd   yarn.ps1   yarnpkg   yarnpkg.cmd   yarnpkg.ps1
```

#### （1）Node.js 和 npm 安装步骤

不错不错，特别的好使。现在综上所述一下，将 Windows 安装 Node.js 和 npm 以及添加环境变量的方法总结一下：

{% note danger %}

~~TMD，先不写了，有空再写，TMD。~~

~~我 TMD 本来是想再 MSYS UCRT64 环境使用 hexo 新生成一篇 post 的，结果发现没有 hexo、npm、nodejs，🍀，然后就写了上述内容 —— 关于 MSYS 中 nodejs 的安装。TMD，一下子直接花了好多时间，😭😭😭😭😭😭。~~


{% endnote %}


### 5）Visual Studio Code 使用 MSYS2 作为默认终端

{% note info %}

该部分的编写时间是：**2023-04-05 15:31:10**，注意时效性，可能不是那么适用。

官方文档有专门关于终端的内容，可以自行查看：[Terminal Basics - TERMINAL | Visual Studio Code Docs](https://code.visualstudio.com/docs/terminal/basics)。

{% endnote %}

主要是修改 VS code 的设置文件 —— `settings.json`，以及该文件中 `terminal.integrated.profiles.windows` 字段的内容，记录时所参照的系统是 Windows 10。

啊吧啊吧，我 TM 直接贴出我的 `settings.json` 文件的 `terminal.integrated.profiles.windows` 字段内容，不继续多讲了，懒了懒了：
```json
    "terminal.integrated.profiles.windows": {
        "PowerShell": {
            "source": "PowerShell",
            "icon": "terminal-powershell"
        },
        "Command Prompt": {
            "path": [
                "${env:windir}\\Sysnative\\cmd.exe",
                "${env:windir}\\System32\\cmd.exe"
            ],
            "args": [],
            "icon": "terminal-cmd"
        },
        "Git Bash": {
            "source": "Git Bash"
        },
        "MSYS2(URCT64)": {
            "path": [
                "${env:windir}\\Sysnative\\cmd.exe",
                "${env:windir}\\System32\\cmd.exe"
            ],
            "args": [
                "/c",
                "C:/msys64/msys2_shell.cmd -defterm -here -no-start -ucrt64"
            ],
            "icon": "terminal-bash",
            "color": "terminal.ansiRed"
        }
    }
```
咱使用 UCRT64 环境，同时为了显示出某些 icons 啥的，需要使用 nerdfonts 字体，所以咱设置一下终端所使用的字体：
```json
"terminal.integrated.fontFamily": "'mononoki NFM', '微软雅黑'"
```

同时也方便直接对 VS code 所打开项目进行某些命令行操作呢，还需要**设置一下终端打开时所处于的路径**：
```json
"terminal.integrated.defaultLocation": "editor"
```
哦。还需要设置一下默认终端：
```json
"terminal.integrated.defaultProfile.windows": "MSYS2(URCT64)"
```

暂且这样。

### 6）.zshrc 文件配置

主要记录一下环境变量的设置，以及命令别名设置，直接上文件：
```.zshrc
# Environment Variable
# export ALL_PROXY=http://127.0.0.1:10809
# export PATH="$PATH:/home/{UserName}/.local/share/gem/ruby/3.1.0/bin"
export PATH="$PATH:/c/Users/{UserName}/.cargo/bin"
export PATH="$PATH:/c/Program Files (x86)/Microsoft VS Code/bin"
export PATH="$PATH:/c/Android/platform-tools"
export PATH="$PATH:/c/Users/{UserName}/scoop/apps/scrcpy/current"
export PATH="$PATH:/c/Program Files/nodejs"
export PATH="$PATH:/c/Users/{UserName}/AppData/Roaming/npm"
# export PATH="$PATH:/ucrt64/lib/node_modules"
# export PATH="$PATH:/ucrt64/lib/node_modules/yarn/bin"

# Aliases
alias ls="lsd --config-file /home/{UserName}/.config/lsd/config.yaml"
alias datetime='echo $(date +%F%n%T)'
alias path='echo $PATH | tr ":" "\n" | sort -u'
alias msysenv='echo $MSYSTEM'
alias zshconfig='echo "sourcing ~/.zshrc..." && source ~/.zshrc'
alias all_proxy='ALL_PROXY=http://127.0.0.1:10809'
```
添加了一些常用的环境变量：
+ VS code
+ adb
+ scrcpy
+ nodejs
+ npm

等等，这个都在本文中有所描述，基本上就是在自己使用 msys2 的过程中，将觉得有用的东西使用上，并进行记录。

## 继续摸鱼

## 参考
+ [MSYS2](https://www.msys2.org/)
+ [Package Naming | MSYS2](https://www.msys2.org/docs/package-naming/)
+ [Environments | MSYS2](https://www.msys2.org/docs/environments/)
+ [Installing nodejs and npm on MSYS2 | stack**overflow**](https://stackoverflow.com/questions/46473196/installing-nodejs-and-npm-on-msys2)
