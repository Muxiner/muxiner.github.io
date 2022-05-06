title: Windows Terminal 使用及美化记录
author: Muxiner
date: 2022-04-06 18:11:19
categories: Terminal
tags:
 - Beauty
 - Terminal
---
## 简介
用来记录使用 Windows Terminal 一路上遇到的问题以及解决的办法。

写本文时，运行 Windows Terminal 的环境：
+ Windows 11
+ 自带的 Windows Terminal

## 安装
+ Windows 10
	Windows 10 可以从系统自带的 MicroSoft Store 进行下载安装，搜索 Windows Terminal，点击安装即可。
+ Windows 11
	Windows 11 直接自带 Windows Terminal，并将其作为默认的命令行工具——无论是 PowerShell 还是 CMD，或者是用户自己后续安装的如 Git Bash 等等均会直接使用 Windows Terminal 进行打开，怎么说就，十分舒适。


总所周知，Windows Terminal 是可以进行美化的，而这意味着什么？

我们可以将不忍直视的 CMD 或者 Git Bash 界面做成让我们自己赏心悦目的样子，可以极大的愉悦我们的心情。


## Windows Terminal 美化
### 配置文件
简单的说就是，Windows Terminal 通过修改**配置文件**中的内容，获得不一样的视觉效果。

配置文件包含三块部分：
1. 常规
2. 外观 —— 设置字体、窗口样式、配色方案、透明度、背景图片等
3. 高级

### 常规
> Windows 10、早期的 Windows 11 的 Terminal 的配置文件还是分为上述的三部分
> 不过，在 22 年 4 月份的时候，Terminal 的配置文件部分就发生了一点变化。
> 首先就是界面部分变得和 Windows 11 设置一样的 UI 风格
> 其次，常规部分变成了如图所示样子：
> [![OnwlJe.png](https://s1.ax1x.com/2022/05/06/OnwlJe.png)](https://imgtu.com/i/OnwlJe)
> 外观 + 高级则隶属于其他设置（内容大致没有变化）。

> 本文根据当前样式进行介绍。

该部分共有 6 个字段：
+ 名称：下拉列表中显示的配置文件名称。
   
  [![OnBa8g.png](https://s1.ax1x.com/2022/05/06/OnBa8g.png)](https://imgtu.com/i/OnBa8g)
+ 命令行：在配置文件中所使用的可执行文件。
   
   简单说就是，需要用到的命令行的可执行文件（路径），如：
   + `cmd`：就是 `cmd.exe`
   + `git`：就是 `git.exe`
   
   等等。
+ 启动目录：加载配置文件时启动的目录。
  
  > 用人话说就是：打开该命令行后，所在的文件路径。
  默认值：`"%USERPROFILE%"`，该值是用户名的文件夹，即：
  [![Onyii6.png](https://s1.ax1x.com/2022/05/06/Onyii6.png)](https://imgtu.com/i/Onyii6)

  > 备注：
  > 反斜杠需要转义。 例如，应以 `C:\\Users\\USERNAME\\Documents` 的形式输入 `C:\Users\USERNAME\Documents`。

+ 图标：配置文件中所使用的图标的表情符号或图像文件位置。
  > 这将设置在选项卡、下拉菜单、跳转列表和选项卡切换器中显示的图标。
  由此就可以将图标设置成喜欢的样子，例如：
  [![OnyISO.png](https://s1.ax1x.com/2022/05/06/OnyISO.png)](https://imgtu.com/i/OnyISO)
  将 powershell 的图标设置成这个样子了。

+ 选项卡标题：将配置文件名称替换为标题，以在启动时传递给外壳。
  >设置后就会如图所示，标题一直是`cmd`、`powershell`。

  [![On6Akq.png](https://s1.ax1x.com/2022/05/06/On6Akq.png)](https://imgtu.com/i/On6Akq)
  ~~似乎没有那么好看了，不过这是看情况的~~

+ 从下拉菜单中隐藏：如果启用，配置文件将不会显示在配置文件列表中。
	> 这可用于**隐藏** `默认配置文件` 和 `动态生成的配置文件`，同时将他们保留在设置文件中。

	[![OnBxsA.png](https://s1.ax1x.com/2022/05/06/OnBxsA.png)](https://imgtu.com/i/OnBxsA)

更多关于该部分的信息，请详见 [**Windows 终端中的常规配置文件设置**](https://docs.microsoft.com/zh-cn/windows/terminal/customize-settings/profile-general)。
### 外观
外观是咱们 Windows Terminal 美化的主战场，主要就是自定义修改**字体**、**配色方案**、**背景图片**、**亚克力效果**（透明度）等等。

共有两种修改方式：
1. 使用图形界面的设置 —— 就是进入 Windows Terminal 的设置里一点点的调整
2. 修改配置文件（JSON文件）—— 这个会比第一种复杂不少，因为是需要自己文件中的一点点设置啦

不过两者各有所长，至少配置文件可以用来保存设置好的美化方案，方便分享或是重装系统后的恢复。

通过修改上述的几点设置后，咱们的终端界面就会有很大的不同了，看起来就有那么一点点的赏心悦目。

现在从配色方案、字体、背景图片、亚克力效果进行说明。

更多关于该部分的信息，请详见 [**Windows 终端中的外观配置文件设置**](https://docs.microsoft.com/zh-cn/windows/terminal/customize-settings/profile-appearance)。

> 注意：
> 可设置选项请以所使用的 Windows Terminal 显示的为主。
#### 配色方案

配色方案就好比一个主题，有着不同的风格（颜色），可以使得咱们的 Terminal 看起来具有别样的美感，同时也可以根据个人的喜好，获取自己别样的美学享受。~~瞎扯ing~~

但是，使用、获取一个配色方案很简单，使用、获取一个合适的配色方案就不是那么简单了。
> 一个合适的配色方案需要考虑到多种因素，如背景图片、亚克力效果等等。
> 他们有机组合在一起才可以获取一个美观、清楚、清晰的美化效果。
> 不然呀，就会发现，某某地方怎么不清楚、看不到了呢？整体看着那么别扭呢？
> 不过，俺也就在这简单的说一说，具体怎么实现美观、清楚、清晰的效果，俺还不知道，后续更新去了。

Windows Terminal 中有几个默认的配色方案可供使用：
+ `Campbell`
  [![OnIeaD.png](https://s1.ax1x.com/2022/05/06/OnIeaD.png)](https://imgtu.com/i/OnIeaD)
+ `Campbell Powershell`
  [![OnIEqK.png](https://s1.ax1x.com/2022/05/06/OnIEqK.png)](https://imgtu.com/i/OnIEqK)
+ `One Half Dark`
  [![OnzeXD.png](https://s1.ax1x.com/2022/05/06/OnzeXD.png)](https://imgtu.com/i/OnzeXD)
+ `One Half Light`
  [![OnzK7d.png](https://s1.ax1x.com/2022/05/06/OnzK7d.png)](https://imgtu.com/i/OnzK7d)
+ `Solarized Dark`
  [![OuSFbQ.png](https://s1.ax1x.com/2022/05/06/OuSFbQ.png)](https://imgtu.com/i/OuSFbQ)
+ `Solarized Light`
  [![OuS0qe.png](https://s1.ax1x.com/2022/05/06/OuS0qe.png)](https://imgtu.com/i/OuS0qe)
+ `Tango Dark`
  [![OupCJ1.png](https://s1.ax1x.com/2022/05/06/OupCJ1.png)](https://imgtu.com/i/OupCJ1)
+ `Tango Light`
  [![OupcTJ.png](https://s1.ax1x.com/2022/05/06/OupcTJ.png)](https://imgtu.com/i/OupcTJ)
+ `Vintage`
  [![OupIOO.png](https://s1.ax1x.com/2022/05/06/OupIOO.png)](https://imgtu.com/i/OupIOO)


如果默认的配色方案没法满足你的需求，还可以自己设置想要的配色方案哦（有时候可能会有一点点困难）。

[![Ou9ikj.png](https://s1.ax1x.com/2022/05/06/Ou9ikj.png)](https://imgtu.com/i/Ou9ikj)

选择合适的终端颜色、系统颜色，再保存，就拥有自己喜欢的配色方案了。

不过具体的效果就不知道如何了。

如果自己设置的配色方案还是没法满足自己的需要，咋办？

没事，有大佬们设计了很多很多种华丽的配色方案: [Windows Terminal Themes](https://windowsterminalthemes.dev/)

[![OuCm8I.png](https://s1.ax1x.com/2022/05/06/OuCm8I.png)](https://imgtu.com/i/OuCm8I)

一共有几十共不同的配色方案，一种配色方案还有 `Dark`，`Light` 两种选择，共有一款会是你喜欢的，或者是适合你的。

#### 字体
字体，字体选择也会对终端的界面有很大的改变。

这里没有太多好说的，主要是需要使用**等宽字体**，不要使用中文字体，如宋体、幼圆、黑体。

这是使用了**黑体**的结果，就一个字——丑。
[![OuPzX6.png](https://s1.ax1x.com/2022/05/06/OuPzX6.png)](https://imgtu.com/i/OuPzX6)

不过 terminal 也提供了很多不错的字体，如 `Cascadia Code`、`Cascadia Mono`、`Consolas` 等等。

当然你还可以自己安装你喜欢的字体，如 [JetBrains Mono](https://www.jetbrains.com/zh-cn/lp/mono/)。
> 该字体有很多种系列，如细体、特细、细、正常、中等、半粗体、粗体、超粗体，同时还有对应的斜体。
> 怎么说，就很丰富。

而我自己使用的字体，是 [Nerd Font](https://www.nerdfonts.com/font-downloads) 字体系列中的 [Hack Nerd Font](https://github.com/ryanoasis/nerd-fonts/releases/download/v2.1.0/Hack.zip)。（点击后会直接下载该字体哦)
> 该系列的字体会比 JetBrains 的字体好一点，因为他们有图标，可以显示某些主题的一下图标。

可以自己找到喜欢的字体，然后安装，就可以设置该字体作为终端的字体了。

#### 背景图片
背景图片可以让你的终端看起来更加的花里胡哨。

你可以选择自己想要的图片，或者是桌面壁纸。
[![OuEtG4.png](https://s1.ax1x.com/2022/05/06/OuEtG4.png)](https://imgtu.com/i/OuEtG4)
选择使用背景图片后，还可以设置图片的一些属性：
+ 背景图像拉升模式
+ 背景图像对齐
+ 背景图像不透明度
  
可自行调试上述的属性。

> 注意：
> 使用背景图片使用时，要注意与配色方案的协调性——就是避免背景图片的某些部分影响了文字的可读性，就如上图中，是灰色的字体，部分地方因为背景图片而看的不甚清楚。
> 当图片会影响到文字的阅读时，可能需要更换其他合适的图片，或者是调整**背景图像不透明度**，这一属性，使得终端看起来舒服些。

#### 亚克力效果、透明效果
设置该配置文件的窗口透明度。效果如下：

[![OuZT2Q.png](https://s1.ax1x.com/2022/05/06/OuZT2Q.png)](https://imgtu.com/i/OuZT2Q)
> 可以看见窗口下层关于 `Windows Terminal Themes` 的内容。
> 透明度也是需要适当设置的，不然也会影响文字的阅读。
> 这一点也是需要和配色方案协调起来，比如某些颜色的字更容易看清楚。
> 不过更多的是与 terminal 下层的窗口有关系，它的颜色很容易影响文字的阅读。
> 所以，最好还是合理的hi用该透明的效果。

不过还有**亚克力效果**可以缓解上述问题：当启用亚克力效果时，终端会创建一个模糊的背景——应用一个半透明的纹理。
[![OumEOs.png](https://s1.ax1x.com/2022/05/06/OumEOs.png)](https://imgtu.com/i/OumEOs)
> 如图，窗口下层依然是关于 `Windows Terminal Themes` 的内容，但是仅能隐约的看到相关内容。
### 高级
看了一下，似乎没有什么和美化有关的内容，所以就不在此叙述。

更多关于该部分的信息，请详见 [**Windows 终端中的高级配置文件设置**](https://docs.microsoft.com/zh-cn/windows/terminal/customize-settings/profile-advanced)。

### 其他

本篇文章仅仅只是介绍了 Windows Terminal 对于终端的美化，设置图片、字体、配色方案、透明度之类的。

或许你也发现，文中配图的 powershell 不太一样，这是因为我使用了 [oh my posh](https://ohmyposh.dev/)(A prompt theme engine for any shell.)

会在下篇文章介绍 oh my posh 的使用。

## 参考文档
+ [Windows Terminal 官方文档](https://docs.microsoft.com/zh-cn/windows/terminal/)