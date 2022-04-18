title: 【水博客】VS code Markdown 导出 PDF 时，数学公式未能正确导出
date: 2022-04-18 11:41:36
categories:
 - 水博客
tags:
 - Markdown
 - VS code
---
## 问题描述

本次出现的是问题是在写作业时发现的。

虽然已经用 `MarkDown` 很久了，也时常将 MD 文件导出成 PDF，但是之前使用的都是实时渲染的软件，如 `Typora` 等，来完成上述的工作，所以就没有出现本文博客需要解决的问题。

后续由于 `Typora` 收费 ~~（当然你还可以去官网找 `1.0` 版本之前的版本，是不收费）~~，以及其导出的 PDF 并不是很合我的审美~~（颜狗去死吧）~~，，我就放弃使用 `Typora`，经过几天的查找后，还是发现 `VS code` + 插件导出的 PDF 最好看，也非常符合我的审美。所以就开始使用 VS code 导出 PDF。

每次都是使用实时渲染的软件写好文档，然后保存 MD 文件，再用 `VS code` 打开 + 导出，就很棒。

但是今天就翻车了，因为在 MD 中使用了**数学公式**，再使用相同的方法导出时，就出了问题 —— 数学公式未能正确导出，还是 MD 语法的表示形式。如图：


[![LazgxA.md.png](https://s1.ax1x.com/2022/04/18/LazgxA.md.png)](https://imgtu.com/i/LazgxA)
  
就挺懵逼的。

## 问题解决


然后就求助于万能的搜索引擎。开始查找解决办法。

先讲述一个失败的方法，不不不，也不是失败的方法，就是导出来的文件不符合我的审美，我就直接拒绝了它。

### 方法一（不喜欢）

+ 安装两个插件：
    + `Markdown Preview Enhance`：预览插件
    + `Markdown + Math`：支持数学公式插件

+ 然后使用上述插件预览
+ 预览页面鼠标右键，选择导出为 html 文件
+ 浏览器打开 html 文件，右键选择打印

问题是可以解决，但是过程复杂了，而且排版和界面不好看呀。

( ᑭ`д´)ᓀ))д´)ᑫ

### 方法二（完美）

所以就去寻找另外的方法。

ᕕ( ᐛ )ᕗ

还是需要两个插件哈，不过都是之前用着的插件，用于 VS code 使用 `Markdown`。

+ `Markdown All in One`
  
  该插件提供了一些 `Markdown` 书写过程中非常便捷性的一些操作，同时支持了 `latex` 公式，能够让你的 `VS code markdown Preview` 识别你所书写的公式。

+ `Markdown PDF`
  
   该插件提供了将 `Markdown` 文件输出为可预览的不同格式文件，包括 `html`， `pdf` 等。

   [![LdSqYD.md.png](https://s1.ax1x.com/2022/04/18/LdSqYD.md.png)](https://imgtu.com/i/LdSqYD)


光安装两插件还不足及解决问题，接下来就需要给加点小动作了。

ᕕ( ᐛ )ᕗ

找到 `Markdown PDF` 插件中的一个文件 —— `template.html`。

文件路径：`C://Users/<username>/.vscode/extensions/yzane.markdown-pdf-1.4.1/template/template.html`

> 实在找不到可以使用 `everything` 搜索一下。
> + [everything](https://www.voidtools.com/zh-cn/)

然后使用编辑器，如 `VS code` 打开该文件，在如图位置加入两行代码。
```html
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>
<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: {inlineMath: [['$', '$']]}, messageStyle: "none" });</script>
```

[![LdpN0x.md.png](https://s1.ax1x.com/2022/04/18/LdpN0x.md.png)](https://imgtu.com/i/LdpN0x)

最后再重新导出 PDF 就可以啦。

[![Ldpr1H.md.png](https://s1.ax1x.com/2022/04/18/Ldpr1H.md.png)](https://imgtu.com/i/Ldpr1H)

可见问题完美解决。

好耶。又水了一篇。

ᕕ( ᐛ )ᕗ

## 参考

+ 法一：[vscode下markdown转PDF](https://blog.csdn.net/weijifen000/article/details/84257434)
+ 法二：[VScode中Markdown PDF无法正确输出包含公式的pdf解决方案](https://blog.csdn.net/qq_18506419/article/details/103461825)