---
title: Windows10 安装 MSYS2
date: 2023-03-12 11:49:09
updated: 2023-03-13 10:57:01
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


## 4. 环境

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

GCC、LLVM、Clang 都是是默认的编译器/工具链，用于在各自的存储库中构建所有软件包。

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



## 6. MSYS2 各环境编译工具的安装
