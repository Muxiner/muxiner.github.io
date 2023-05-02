---
title: Arch Linux 桌面环境的一些设置
date: 2023-03-28 02:27:43
updated: 2023-03-28 02:28:55
excerpt: 简单记录一下 Arch Linux 桌面环境的配置信息。
categories: Linux
tags: 
- Arch Linux
- KDE
- Plasma
index_img:
banner_img:
sticky:
---

### discover

Arch Linux 安装 kde 桌面环境后，Discover 软件商店虽然能够打开应用，但是没有软件信息，无法在其中安装软件，这是因为少了一些软件包。

> Discover 是 KDE 桌面环境中的软件包管理器，可以方便地搜索、安装和卸载软件包。

打开终端，安装包：

```zsh
sudo pacman -S archlinux-appstream-data packagekit-qt5 packagekit flatpak fwupd
# yay -S archlinux-appstream-data packagekit-qt5 packagekit flatpak fwupd
```

`ackagekit-qt5` —— 安装以解决 Discover 不显示任何程序的问题。

KDE Discover 中已实现了新的 fwupd 后端以进行固件更新。

`fwupd` 是一个进行设备固件更新的简单守护程序，虽然是为桌面计算机设计，但是同样也支持手机和服务器。

`flatpak` —— 是一个用来管理应用和应用所使用的运行时的工具。

在 Flatpak 模型中，应用的构建和分发不依赖其主系统，并且它们在运行时一定程度上独立于主系统（'沙箱化'）。Flatpak 使用 OSTree 以分发和部署数据。它使用的仓库是 OSTree 仓库并且可以用 ostree 的工具来操作。已安装的运行时和应用都已经过 OSTree 检出。

### bluetooth

如果安装完 Arch Linux 想听歌，带着自己酷炫的蓝牙耳机听歌，但是仔细一看，蓝牙怎么没有，这时就需要将蓝牙服务安装过来。

首先先安装蓝牙并启动蓝牙服务：

```zsh
sudo pacman -S bluez bluez-utils

# yay -S bluez bluez-utils
```

两个软件包，前者提供蓝牙协议栈，后者提供 `bluetoothctl` 实用程序。

`bluetoothctl` — 在 shell 中配对设备是最简单可靠的方法之一。

启动服务：

```zsh
sudo systemctl start bluetooth
#sudo systemctl start bluetooth.service
```

并设计开机自启：

```zsh
sudo systemctl enable bluetooth
# sudo systemctl enable bluetooth.service
```

检查蓝牙服务状态：

```zsh
systemctl status bluetooth
# systemctl statss bluetooth.service
```

还可以安装蓝牙图形化界面 — `Bluedevil` — KDE 的蓝牙工具。如果 Dolphin 和系统托盘里没有蓝牙图标，就在系统托盘选项里启用，或者添加一个挂件。点击图标或在 KDE 系统设置里都可以配置蓝牙:

```zsh
sudo pacman -S bluedevil
# yay -S bluedevil
```

至此之后，只要是不出问题，就可以直接在系统设置中连接蓝牙，并进行使用。

至于还有其他的问题，我之前遇到过，但是没有及时记录下来，如今想进行记录，但是记不清了。
