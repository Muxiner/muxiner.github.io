---
title: Visual Studio Code 插件使用记录
date: 2022-07-12 16:35:59
updated: 2022-07-12 16:35:59
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

{% note primary %}
**2022-07-12** 更新：
+ 添加 <span class="label label-info"><a href="#C/C++Plugins" title="vs code C\C++插件">C\C++ Plugins</a></span>：<span class="label label-default"><a href="#C\C++">C\C++</a></span>、<span class="label label-default"><a href="#C/C++Extension-Pack">C/C++ Extension Pack</a></span>
+ 添加 <span class="label label-info"><a href="#beauty-plugins" title="vs code 美化插件">美化</a></span>：
{% endnote %}



### C\C++ Plugins
<a id='C/C++Plugins'></a>
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

<a id='beauty-plugins'></a>

#### 1. Beauty

<a id='Beauty'></a>

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220712191137.png)

Beauty 是 Web 开发中 VSCODE 的代码美化器扩展。
它支持多种语言，如 javascript, css, less, python, jsx, markups(html, swig, nunjucks)...等。

> 不格式化其他的编程语言吗。

#### 2. One Dark Pro

<a id="ondarkpro"></a>

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220712191628.png)

`Atom` 用于 `Visual Studio Code` 的标志性 `One Dark` 主题。

> 很好看的主题呀。


### 汉化

<a id="Sinicization"></a>

#### Chinese (Simplified) (简体中文) Language Pack for Visual Studio

<a id="Chinese-Simplified"></a>

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220712192229.png)

此中文（简体）语言包为 VS Code 提供本地化界面。

> 英文不友好者狂喜插件。

### MarkDown

<a id="markdown"></a>

#### 1. Markdown All in One

<a id="Markdown-All-in-One"></a>

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220712192533.png)

`Visual Studio Code` 的 `Markdown` 支持。

> 将 `vscode` 作为 `markdown` 编辑器的话就需要这个了。

#### 2. Markdown PDF

<a id="markdown-pdf"></a>

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220712192745.png)

此扩展将 `Markdown` 文件转换为 `pdf`、`html`、`png` 或 `jpeg` 文件。

> 导出 `markdown` 文件需要的插件。

{% note info %}
如果导出文件时数学公式不正确，可见：{% btn https://muxiner.github.io/2022/04/18/vscode-markdown-pdf-math-latex-error/, VS code Markdown 导出 PDF 时，数学公式未能正确导出 %}
{% endnote %}

### Python

<a id="python-plugins"></a>

#### 1. Python

<a id="python"></a>

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220712193331.png)

`IntelliSense` (Pylance)、`Linting`、调试（多线程、远程）、`Jupyter Notebooks`、代码格式化、重构、单元测试。

> 编辑 python 的必备插件呀。

#### 2. Pylance

<a id="pylance"></a>

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