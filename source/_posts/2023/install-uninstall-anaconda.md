---
title: Anaconda 安装、使用和卸载
comment: giscus
math: true
hide: false
date: 2023-04-10 20:48:40
updated: 2023-04-10 20:48:52
excerpt: Windows 10 系统下 Anaconda 的安装、使用以及卸载教程。
categories: Python
tags: [Anaconda, conda]
index_img:
banner_img:
sticky:
---

## Installation

先进入 [DownLoad | Anaconda](https://www.anaconda.com/products/distribution#Downloads) 下载界面，选择 Windows 版的 Installer 文件。

或者直接点击：[Anaconda3-2023.03-Windows-x86_64.exe](https://repo.anaconda.com/archive/Anaconda3-2023.03-Windows-x86_64.exe)
> 版本可能不是最新的。

Over，有空再写。

## Use

~~我 TM 的直接开幕雷击，直接先卸载 Anaconda。~~

## Uninstallation

首先，按下 `Win + R` 打开`运行`窗口，输入: 
```
appwiz.cpl
```
按下回车直接打开 `控制面板 > 所有控制面板项 > 程序和功能`。

选择 `Anaconda3` 右键进行卸载。然后根据 Anaconda 卸载窗口的提示一步步操作即可。

待卸载完成后，Anaconda3 目录就已经被删除了，接下来需要检查一下是否存在残留：
+ 环境变量：
  
  按下 `Win + R` 键入：
  ```
  systempropertiesadvanced
  ```
  就会打开**系统属性**，再选择**环境变量**，再选择**用户变量**和**系统变量**中的 `path`，删除与 `Anaconda` 相关的所有条目。

  然后一路点击**确定**。

+ 用户数据：
  
  Anaconda 还可能是用户主目录的一部分。在该目录（例如，`C:\Users\<your username>`）中搜索名为 `.anaconda` 或 `.conda` 的目录并删除。

如此 Anaconda 的卸载基本上就已经完成了。

