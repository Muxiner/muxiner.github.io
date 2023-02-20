---
title: VScode 自动补全
math: true
hide: false
date: 2023-02-20 13:41:18
updated: 2023-02-20 13:41:18
excerpt: 简单记录：Viusal Studio Code 代码的自动补全。
categories: 
- VS code
tags:
- 记录
- VS code
index_img:
banner_img:
sticky:
---

> 使用 VS code 时没有自动补全的功能，用起来确实十分不适，曾记得之前使用 VS code 时存在着自动补全的功能，一番搜索下来，终是明白如何使用自动补全。

### VS code 文本补全

> VS Code 自动补全，VS Code 当中的自动补全内容，其实是由语言服务来提供的。
> 
> VS Code 为编程语言工作者提供了统一的 API ，即 `Language Server Protocol`，每种语言都能够通过实现这个 API 在 VS Code 上得到类似 IDE 的开发体验，而各个语言根据这个 API 实现的服务，就被称为**语言服务**。
> 
> 语言服务会根据当前的项目、当前的文件，以及光标所在的位置，为我们提供一个建议列表。这个列表包含了在当前光标位置下我们可能会输入的代码。当我们不断地输入字符，VS Code 就会根据当前输入的字符，在这个列表进行过滤。

**使用方法**：
+ 输入字符，出现自动补全的过滤列表窗口；
+ 选择好合适内容，使用 `Tab` 或 `Enter` 进行补全；
+ `Escape` 键关闭（隐藏）自动补全窗口
+ **打字**或 ~~`Ctrl + Space`~~ 重新打开自动补全窗口

#### VS code 自动补全设置

打开 `settings.json`，可以通过设置 `"editor.quickSuggestions"` 来决定在什么语境下自动补全窗口会被唤出。默认设置如下：
```json
 "editor.quickSuggestions": {
    "other": true,
    "comments": false,
    "strings": false
  }
```
+ `other`: 代码;
+ `comments`: 注释；
+ `strings`：字符串。

`true`，启用自动补全窗口；`false` 关闭自动补全窗口。

### 参考

+ [VSCode 自动补全 | 极客教程](https://geek-docs.com/vscode/vscode-tutorials/vs-code-auto-complete.html)