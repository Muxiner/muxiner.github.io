---
title: 使用 Yay 替换 Pacman 作为更加好使的包管理器
math: true
hide: false
date: 2023-03-13 21:31:39
updated: 2023-03-13 21:32:34
excerpt: Yay 是一个基于 Arch Linux 的 AUR (Arch User Repository) 前端，它提供了一些额外的功能和用户友好的界面，使用户可以更方便地管理和安装软件包。与 Arch Linux 的默认包管理器 Pacman 不同，Yay 支持 AUR 软件包的构建和安装，这些软件包通常由社区维护，可以在 Arch Linux 官方软件源之外找到。
categories: Linux
tags:
- Arch Linux
- Yay
- Pacman
index_img:
banner_img:
sticky:
---

## What is Yay

Yay 是一个基于 Arch Linux 的 AUR (Arch User Repository) 前端，它提供了一些额外的功能和用户友好的界面，使用户可以更方便地管理和安装软件包。与 Arch Linux 的默认包管理器 Pacman 不同，Yay 支持 AUR 软件包的构建和安装，这些软件包通常由社区维护，可以在 Arch Linux 官方软件源之外找到。

## Installation

### Install git

```
sudo pacman -S git
```

### Install yay

#### clone yay repo

```
git clone https://aur.archlinux.org/yay.git
```

#### build yay

```
cd yay

makepkg -sri
```

{% note info %}

**可能出现的错误**：
#### 缺少 strip
```bash
$ makepkg -sri
==> 错误： Cannot find the strip binary required for object file stripping.
```

这个错误提示是由于在执行 `makepkg` 编译时缺少 `strip` 命令，`strip` 是一个用于剥离二进制文件中不必要的调试信息的工具，用于减小可执行文件的体积。

要解决这个问题，你需要安装 `binutils` 包，这个包里包含了 `strip` 工具。可以使用以下命令安装：

对于 `Arch Linux` 或者 `Manjaro` 等基于 `Arch Linux` 的发行版：

```
sudo pacman -S binutils
```
安装完成后，重新执行 `makepkg` 命令应该就可以成功了。

#### 没有 go 
```bash
$ makepkg -sri
==> 正在创建软件包：yay 11.3.2-1 (2023年03月13日 21:44:13)
==> 正在检查运行时依赖关系...
==> 正在检查编译时依赖关系
==> 正在安装缺失的依赖关系...
错误：未找到目标：go>=1.17
==> 错误： 'pacman' 无法安装缺失的依赖关系。
==> 缺失依赖关系：
  -> go>=1.17
==> 错误： 无法解决所有的依赖关系。
```
这个错误是提示缺少 go 编译器的版本大于等于 `1.17`。需要先安装 go 编译器，然后再编译 yay。

可以尝试使用 `pacman` 命令安装 go，例如：
```bash
sudo pacman -S go
```
查看 go 版本；
```bash
go version
```
{% endnote %}
