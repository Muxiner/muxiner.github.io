---
title: Windows PowerShell 美化
math: true
date: 2022-05-06 15:01:55
categories: Terminal
tags:
 - Beauty
 - Terminal
index_img: https://s1.ax1x.com/2022/05/06/OK5y8J.png
banner_img: https://s1.ax1x.com/2022/05/06/OK5y8J.png
---
### 简介
这是属于颜狗的胜利，丑不拉几的都不是咱们颜狗想要的，终端也是可以花里胡哨的，人家 `linux` 可以使用 `oh-my-zsh`，将他们的 terminal 打扮的花里胡哨的，咱们 `windows` 下的 `terminal` 也要站起来。所以大佬们就站出来了，他们做出来了 `oh-my-posh`，让咱们 `windows` 也可以使用漂漂亮亮的终端。
> `windows terminal` 也可以装饰咱们的终端，但是，不够呀，咱们想要做成 `oh-my-zsh` 那样的漂漂亮亮。知道**提示符（Prompt）**也需要烧烧的。

[Oh My Posh](https://ohmyposh.dev/) —— A prompt theme engine for any shell.

[Oh My Posh](https://ohmyposh.dev/) 正是这样一款终端 `Prompt` 个性化工具，虽然肇始于同类工具 `Oh My Zsh`，但当更新到 `5.0` 版本时，重新设计的 `Oh my posh` 已经摆脱平台的桎梏，支持了 `Windows、GNU/Linux（WSL）`、`macOS` 三个系统上的 `PowerShell`、`bash`、`zsh` 等终端。

**需要使用** `WindowsTerminal`。
### 安装 Oh My Posh 
官方文档上写到，`Oh My Posh` 在 `windows` 下有三种安装途径：`winget`、`scoop`、`manual`。本文通过 `scoop` 进行安装。
> 想使用其他方法的可进官方文档查看 —— [Windows Install Oh My Posh](https://ohmyposh.dev/docs/installation/windows)

#### Scoop
在安装 `Oh My Posh` 之前，还需要安装一个 `Windows` 下的包管理工具 —— `Scoop`。
> [Scoop](https://scoop.sh/#/) 是 Windows 下的一款十分强大的包管理器，可以用来下载和管理各种软件包
首次需要打开并运行 `PowerShell terminal` (version 5.1 or later)。

然后使用下列命令进行安装：
```shell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser 
# Optional: Needed to run a remote script the first time
```

```shell
Invoke-WebRequest get.scoop.sh | Invoke-Expression
```

#### Oh My Posh
通过 `scoop` 进行安装：
```shell
scoop install https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/oh-my-posh.json
```
![](https://s1.ax1x.com/2022/05/06/OKHemR.png)
当出现图示内容（绿色）时，说明安装成功。

> 除了使用官方文档提到的方式进行安装。还可以使用 `scoop install oh-my-posh` 进行安装。
> 这是 [scoop apps](https://scoop.sh/#/apps?q=oh-my-posh)中所提到的。
> ![](https://s1.ax1x.com/2022/05/06/OKHWNV.png)
> 使用此种方法时，要跟着文档的方法走哦。
> 安装成功截图：
> ![](https://s1.ax1x.com/2022/05/06/OKbA4f.png)

> 如果想要卸载 Oh My Posh 的话，可以使用命令 `scoop uninstall oh-my-posh`，进行卸载。
> 卸载成功截图：
> ![](https://s1.ax1x.com/2022/05/06/OKbPHI.png)

#### 字体
![](https://s1.ax1x.com/2022/05/07/OKO35t.png)
[Oh My Posh](https://ohmyposh.dev/docs/installation/windows) 提示到** 要显示所有图标，我们建议使用 `Nerd Font`。**

所以咱就下载 [Nerd Font](https://www.nerdfonts.com/font-downloads) 字体吧。

如果不适用 `Nerd Font` 的话，就会出现这种情况：
![](https://s1.ax1x.com/2022/05/07/OKOhZ9.png)
可见 icon 们均没有正常显示，而是显示的方框，这也是为什么要使用 `Nerd Font` 的原因了。
> 人家自己也说了—— “To display all icons, we recommend the use of a Nerd Font.”


![](https://s1.ax1x.com/2022/05/07/OKOxII.png)

进入官网后选择一个中意的字体下载就行。我自己使用的 [Hack Nerd Font](https://github.com/ryanoasis/nerd-fonts/releases/download/v2.1.0/Hack.zip)（点击可直接下载该字体）

然后进行安装啦，打开压缩包，选择喜欢的（细、粗）字体，然后点击安装。
![](https://s1.ax1x.com/2022/05/07/OKXuWV.png)

> 也可以使用 `scoop` 安装 `Nerd Font` 字体：
> ```shell
> scoop bucket add nerd-fonts
> ```
> 再在 [nerd fonts 字体库](https://github.com/matthewjberger/scoop-nerd-fonts/tree/master/bucket) 找到需要安装的字体。
> 然后就执行命令：
> ```shell
> scoop install Hack-NF
> ```
> 安装完成后需要重启 Windows Terminal 才可以设置字体哦，否则会设置失败。

最后，在 `windows terminal` 中将字体选择为 `Hack Nerd Font`，即可。
![](https://s1.ax1x.com/2022/05/07/OKXswd.png)

#### posh-git
[posh-git](https://github.com/dahlbyk/posh-git) 可以在 `PowerShell` 中显示 `Git` 状态的摘要信息并自动补全 `Git` 命令。

通过 `scoop` 来安装，依次执行命令：
```shell
scoop bucket add extras
```
![](https://s1.ax1x.com/2022/05/07/OKjf41.png)
```shell
scoop install posh-git
```
![](https://s1.ax1x.com/2022/05/07/OKjcB4.png)

#### Terminal-Icons
![](https://s1.ax1x.com/2022/05/07/OKjHDe.png)
[Terminal-Icons](https://github.com/devblackops/Terminal-Icons) 可以在 `PowerShell` 中显示项目图标并以颜色区分。让你的 `Powershell` 变得更加的花哨。

通过 `scoop` 来安装，依次执行命令：
```shell
scoop bucket add extras
```
> 前文中已执行过该命令，此次可不在执行。

```shell
scoop install terminal-icons
```
![](https://s1.ax1x.com/2022/05/07/OKvMb4.png)

> 安装完成后，还贴心的提示了如何使用呢。
### 配置 Oh My Posh
完成上述的安装后，启动 `PowerShell` 时并不会默认加载个性化后的配置，因此需要修改 `PowerShell` 配置文件来让每次启动都加载。

执行命令打开配置文件：
```shell
notepad $PROFILE
```
若提示不存在文件，且提示是否创建文件，则直接创建，否则需要手动在 `PowerShell` 目录下创建一个配置文件再进行编辑。

若需手动创建配置文件，则依次执行命令：
```shell
mkdir ~\Documents\WindowsPowerShell
# 创建文件夹
echo "" > ~\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1
# 创建配置文件
```
最后向配置文件中添加：
```ps1
# 使用 oh my posh
oh-my-posh init pwsh | Invoke-Expression
# 使用 Terminal-Icons
Import-Module Terminal-Icons
# 使用 posh-git
Import-Module posh-git
```
最后重新启动 `PowerShell`，或者是输入命令 `powershell` 即可查看美化后的界面。
![](https://s1.ax1x.com/2022/05/07/OKxkLD.png)

### 配置主题
完成全部安装和配置后，使用的是默认主题，如果想要切换成其它主题，可以去 [官方主题目录](https://ohmyposh.dev/docs/themes) 查看各种主题的效果，同时这些主题也被安装在 `Oh My Pos`h 的主题目录下。

通过 `scoop` 安装后的主题目录为：
```shell
~\scoop\apps\oh-my-posh\current\themes
```
所有主题配置文件都放在这里，并以 `.omp.json` 结尾，从其它地方下载的主题配置文件也需要放在这里。

在终端中执行以下命令，就可以查看所有主题在终端中的效果：
```shell
Get-PoshThemes ~\scoop\apps\oh-my-posh\current\themes 
```
![](https://s1.ax1x.com/2022/05/07/OKxrmF.png)

选择一个主题的名字，如 `paradox`，然后编辑 `PowerShell` 的配置文件，执行命令：
```shell
notepad $PROFILE
```
将其中的 `oh-my-posh init pwsh | Invoke-Expression` 加上 `--config [主题路径]` 参数：
```
oh-my-posh init pwsh --config ~\scoop\apps\oh-my-posh\current\themes\paradox.json | Invoke-Expression
```
最后重新启动 `PowerShell`，或者是输入命令 `powershell` 即可查看美化后的界面。

### 配置 VS code
在 `VS code` 中也能打开 `PowerShell` 终端，但是由于没有配置终端字体，因为 icon 们还是没有正常显示，而是显示的方框。

因此需要设置 `VSCode` 的终端字体为 `Hack Nerd Font` 才能正常显示。

首先打开**设置**，搜索 `Terminal > Integrated > Font Family`。
![](https://s1.ax1x.com/2022/05/07/OKxh6K.png)
然后添加 `Hack Nerd Font`。

最后重新打开终端，或是执行 `powershell`，即可查看美化界面。
![](https://s1.ax1x.com/2022/05/07/OKzaAH.png)

### 成品
完成上述配置，以及对 `Windows Terminal` 的配置文件进行修改后，咱就获得了一个花哨的 `PowerShell`:
![](https://s1.ax1x.com/2022/05/07/OMSsi9.png)

### 参考
+ [Oh My Posh | A prompt theme engine for any shell](https://ohmyposh.dev/)
+ [Scoop | A command-line installer for Windows](https://scoop.sh/#/)
+ [Oh My Posh：全平台终端提示符个性化工具](https://sspai.com/post/69911)
+ [使用 Oh My Posh 来个性化终端](https://www.raimis.me/archives/80/)
+ [颜值是第一生产力 - Windows Terminal](https://blog.davidz.cn/beauty-is-productivity-windows-terminal/)
+ [果然颜值才是第一生产力……power-shell美化](https://jishuin.proginn.com/p/763bfbd716f5)
