---
title: Windows 上安装 Linux 发行版 —— Ubuntu
math: true
hide: false
date: 2022-10-31 19:20:40
updated: 2022-10-31 19:20:56
excerpt: Windows 安装适用于 Linux 的 Windows 子系统 —— Ubuntu —— 的简单教程。
categories:
- 教程
- Linux
- WSL
tags:
- Ubuntu
- wsl2
index_img:
banner_img:
sticky:
---

没啥好说的，直接开始安装教程。

{% note primary %}

简单的介绍一下 **WSL**：

+ 适用于 Linux 的 Windows 子系统 —— 可让开发人员按原样运行 GNU/Linux 环境 - 包括大多数命令行工具、实用工具和应用程序 - 且不会产生传统虚拟机或双启动设置开销。

更多的信息可详见官方文档：
+ [适用于 Linux 的 Windows 子系统文档](https://learn.microsoft.com/zh-cn/windows/wsl/)
  + [什么是适用于 Linux 的 Windows 子系统 (WSL)？](https://learn.microsoft.com/zh-cn/windows/wsl/about)
  + [WSL 2 的新增功能](https://learn.microsoft.com/zh-cn/windows/wsl/compare-versions#whats-new-in-wsl-2)
  + [比较 WSL 1 和 WSL 2](https://learn.microsoft.com/zh-cn/windows/wsl/compare-versions)
{% endnote %}


### 安装 WSL

{% note default %}
**`WSL` 有 `Windows` 版本要求**：
必须运行 Windows 10 版本 2004 及更高版本（内部版本 19041 及更高版本）或 Windows 11。
{% endnote %}

1. 以**管理员身份**运行 PowerShell
2. 安装 WSL
   ```powershell
   wsl --install
   ```
    此命令将启用所需的可选组件，下载最新的 Linux 内核，将 WSL 2 设置为默认值，并安装 Linux 发行版（默认安装 Ubuntu）。

   > 执行完成后，需要重启计算机来安装在 Windows Server 2022 上运行 WSL 所需的全部内容。**稍后再重启计算机。**
3. 启用适用于 Linux 的 Windows 子系统
   ```powershell
    Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
   ```
    {% note warning %}
    + 必须启用“适用于 Linux 的 Windows 子系统”可选功能并重启，然后才能在 Windows 上运行 Linux 发行版。
    + 依然以管理员身份运行 PowerShell。
    {% endnote %}

4. 安装 Linux 分发版 —— Ubuntu
   + 打开 Microsoft Store，搜索 Ubuntu，下载。

5. 打开 Ubuntu，输入 username 和 password。

结束。

{% note primary %}

如果在安装过程中出现其他的问题，请自行搜索问题进行解决。

{%  endnote%}

### 参考

+ [使用 WSL 在 Windows 上安装 Linux](https://learn.microsoft.com/zh-cn/windows/wsl/install)
+ [安装WSL2并下载配置Ubuntu](https://zhuanlan.zhihu.com/p/348813745)
