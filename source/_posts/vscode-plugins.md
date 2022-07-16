---
title: Visual Studio Code 插件使用记录
date: 2022-07-12 16:35:59
updated: 2022-07-16 17:30:32
excerpt: 记录一下 vs code 好用的插件，以及开发环境需要的插件。
categories: 
- VS code
tags:
- Plugins
- 记录
index_img:
banner_img:
math: true
---

### 更新情况

{% note primary %}
**2022-07-12** 更新：
+ 添加 <span class="label label-info"><a href="#C-C-Plugins" title="vs code C\C++插件">C\C++ Plugins</a></span>：<span class="label label-default"><a href="#1-C-C">C\C++</a></span>、<span class="label label-default"><a href="#2-C-x2F-C-Extension-Pack">C/C++ Extension Pack</a></span>
+ 添加 <span class="label label-info"><a href="#美化" title="vs code 美化插件">美化</a></span>：<span class="label label-default"><a href="#2-One-Dark-Pro">One Dark Pro</a></span>、<span class="label label-default"><a href="#1-Beauty">Beauty</a></span>
+ 添加 <span class="label label-info"><a href="#汉化" title="vs code 汉化插件">汉化</a></span>：<span class="label label-default"><a href="#Chinese-Simplified-简体中文-Language-Pack-for-Visual-Studio">Chinese (Simplified) (简体中文) Language Pack for Visual Studio</a></span>
+ 添加 <span class="label label-info"><a href="#Markdown" title="vs code 汉化插件">Markdown</a></span>：<span class="label label-default"><a href="#1-Markdown-All-in-One">Markdown All in One</a></span>、<span class="label label-default"><a href="#2-Markdown-PDF">Markdown PDF</a></span>
+ 添加 <span class="label label-info"><a href="#Python" title="vs code python 插件">Python</a></span>：<span class="label label-default"><a href="#1-Python">Python</a></span>、<span class="label label-default"><a href="#2-Pylance">Pylance</a></span>

{% endnote %}


{% note primary %}
**2022-07-16** 更新：
+ <span class="label label-info">美化</span> 添加：<span class="label label-default"><a href="#2-Material-Icon-Theme">Material Icon Theme</a></span>、<span class="label label-default"><a href="#3-vscode-icons">vscode-icons</a></span>
+ 添加 <span class="label label-info"><a href="#前端" title="vs code 前端插件">前端</a></span>：<span class="label label-default"><a href="#1-Live-Server">Live Server</a></span>、<span class="label label-default"><a href="#2-Auto-Complete-Tag">Auto Complete Tag</a></span>、<span class="label label-default"><a href="#3-Auto-Rename-Tag">Auto Rename Tag</a></span>、<span class="label label-default"><a href="#4-Auto-Close-Tag">Auto Close Tag</a></span>、<span class="label label-default"><a href="#5-CSS-Peek">CSS Peek</a></span>、<span class="label label-default"><a href="#6-HTML-CSS-Support">HTML CSS Support</a></span>
+ 添加 <span class="label label-info"><a href="#高效率工具" title="vs code 高效率工具插件">高效率工具</a></span>：<span class="label label-default"><a href="#1-Path-Intellisense">Path Intellisense</a></span>、<span class="label label-default"><a href="#2-Bracket-Pair-Colorization-Toggler">Bracket Pair Colorization Toggler</a></span>
{% endnote %}


### C\C++ Plugins

{% note info %}
关于 windows 下 VS code C\C++ 环境的配置：{% btn https://muxiner.github.io/2022/04/19/vscode-env-c-new/#, Windows 下 VS code 配置 C/C++ 环境 %}
{% endnote %}


#### 1. C\C++
<a id='C\C++'></a>

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220712185147.png)

C/C++ 扩展为 Visual Studio Code 添加了对 C/C++ 的语言支持，包括 IntelliSense 和调试等功能。

> 是在 vs code 上面使用 C\C++ 的必要插件。

#### 2. C/C++ Extension Pack
<a id='C/C++Extension-Pack'></a>

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220712185921.png)

此扩展包包括一组用于 Visual Studio Code 中 C++ 开发的流行扩展。
+ [C/C++](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools)
+ [C/C++ Themes](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools-themes)
+ [CMake](https://marketplace.visualstudio.com/items?itemName=twxs.cmake)
+ [CMake Tools](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cmake-tools)
+ [Doxygen Documentation Generator](https://marketplace.visualstudio.com/items?itemName=cschlosser.doxdocgen)
+ [Better C++ Syntax](https://marketplace.visualstudio.com/items?itemName=jeff-hykin.better-cpp-syntax)
+ [Remote Development Extension Pack](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack)

> 推荐 C\C++ 插件的插件呀。

#### 3. 


### 美化

#### 1. Beauty

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220712191137.png)

Beauty 是 Web 开发中 VSCODE 的代码美化器扩展。
它支持多种语言，如 javascript, css, less, python, jsx, markups(html, swig, nunjucks)...等。

> 不格式化其他的编程语言吗。


#### 2. One Dark Pro

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220712191628.png)

`Atom` 用于 `Visual Studio Code` 的标志性 `One Dark` 主题。

> 很好看的主题呀。

#### 2. Material Icon Theme

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220716174638.png)

Get the Material Design icons into your VS Code.

> 这个图标还挺好看的呢。
> 想看清楚的图标的话，需要去官方的 [MarketPlace](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme) 看一看吧。

#### 3. vscode-icons

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220716181801.png)

vscode 团队设计的图标库，还可以，但是在我看来，没上一个好看哦。

### 汉化

#### Chinese (Simplified) (简体中文) Language Pack for Visual Studio

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220712192229.png)

此中文（简体）语言包为 VS Code 提供本地化界面。

> 英文不友好者狂喜插件。

### Markdown

#### 1. Markdown All in One

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220712192533.png)

`Visual Studio Code` 的 `Markdown` 支持。

> 将 `vscode` 作为 `markdown` 编辑器的话就需要这个了。

#### 2. Markdown PDF


![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220712192745.png)

此扩展将 `Markdown` 文件转换为 `pdf`、`html`、`png` 或 `jpeg` 文件。

> 导出 `markdown` 文件需要的插件。

{% note info %}
如果导出文件时数学公式不正确，可见：{% btn https://muxiner.github.io/2022/04/18/vscode-markdown-pdf-math-latex-error/, VS code Markdown 导出 PDF 时，数学公式未能正确导出 %}
{% endnote %}

### Python


#### 1. Python


![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220712193331.png)

`IntelliSense` (Pylance)、`Linting`、调试（多线程、远程）、`Jupyter Notebooks`、代码格式化、重构、单元测试。

> 编辑 python 的必备插件呀。

#### 2. Pylance


![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220712193550.png)

`VS Code` 中用于 `Python` 的高性能、功能丰富的语言服务器。

`Pylance` 可与 `VScode` 中的 `Python` 插件一起使用的一个插件，以提供高性能的语言支持。 
在后台，`Pylance` 由 `Microsoft` 的静态类型检查工具 `Pyright` 提供支持。 使用 `Pyright`，`Pylance` 可以为 `Python IntelliSense` 体验提供丰富的类型信息，从而帮助您更快地编写更好的代码。

`Pylance` 名称是 `Monty Python` 的 `Lancelot` 的一个小颂歌，`Lancelot` 是第一个在圣杯中回答守门员问题的骑士。

**快速开始**

1. 安装 `Pylance` 扩展。
   1. 打开一个 `Python（.py）`文件，`Pylance` 扩展名将被激活。
2. 当提示您将 `Pylance` 设置为默认语言服务器时，选择“是”。 这将更新您的首选项，也可以通过使用文本编辑器将“python.languageServer”：“ Pylance” 添加到 `settings.json` 文件中来手动进行。

`Pylance` 为 `Python 3` 提供了一些很棒的功能，包括：

+ 字串
+ 签名帮助，带有类型信息
+ 参数建议
+ 代码补全
+ 自动导入（以及添加和删除导入代码操作）
+ 输入代码的时候报告代码错误和警告（诊断）
+ 代码大纲
+ 代码导航
+ 类型检查模式
+ 本地多个工作区支持
+ `IntelliCode` 兼容性
+ `Jupyter Notebooks` 兼容性
+ 语法高亮

### 前端

#### 1. Live Server

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220716182133.png)

模拟本地服务器，编写完网页代码后保存，浏览器的页面情况将自动刷新，就无需在浏览器中刷新。

#### 2. Auto Complete Tag

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220716184131.png)

同时拥有**自动关闭标签**和**自动重命名标签**的功能。

> 就是下面两个插件的功能，要么安装该插件，要么安装下面两个插件。

#### 3. Auto Rename Tag

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220716183614.png)

自动重命名成对的 HTML/XML 标记。

#### 4. Auto Close Tag

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220716183810.png)

自动添加 HTML/XMl 关闭标记。

特征：
+ 键入开始标签的右括号时自动添加结束标签
+ 插入结束标签后，光标在开始和结束标签之间
+ 设置不自动关闭的标签列表
+ 自动关闭自关闭标签
+ 支持 `Sublime Text 3` 的自动关闭标签
+ 使用键盘快捷键或命令面板手动添加关闭标签


#### 5. CSS Peek

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220716184534.png)

快速跳到CSS的定义处预览。

特征：该扩展支持符号定义跟踪的所有正常功能，但它适用于 `css` 选择器（`类`、`ID` 和 `HTML` 标记）。这包括：
+ `Peek`：内联加载 `css` 文件并在此处进行快速编辑。( `Ctrl + Shift + F12` )
+ `转到`：直接跳转到 `css` 文件或在新编辑器中打开它 (`F12`)
+ `悬停`：悬停在符号 (`Ctrl + hover`)上显示定义


#### 6. HTML CSS Support

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220716184901.png)

适用于 `HTML` 的 `Visual Studio Code CSS Intellisense`.

特征: 
+ 完善 HTML `id` 和 `类`属性。
+ 支持链接和嵌入的样式表。
+ 支持模板继承。
+ 支持其他样式表。
+ 支持其他类似 `HTML` 的语言。
+ 按需验证 `CSS` 选择器。

用法: 可以通过 `ctrl + 空格` 查看 `id` 和 `类` 属性建议列表。

### 高效率工具

#### 1. Path Intellisense

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220716173750.png)

该插件支持自动提示文件路径，支持各种文件无脑快速引入。

#### 2. Bracket Pair Colorization Toggler

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220716182853.png)

给不同区域的括号加上不同的颜色，加以区分。

仓库：[Bracket Pair Colorization Toggler](https://github.com/dzhavat/bracket-pair-toggler)