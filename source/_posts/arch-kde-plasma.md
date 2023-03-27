---
title: Arch Linux 桌面环境的一些设置
date: 2023-03-28 02:27:43
updated: 2023-03-28 02:28:55
excerpt:暂无
categories: Linux
tags: 
- Arch Linux
- KDE
- Plasma
index_img:
banner_img:
sticky:
---

Arch安装kde后图形软件商店无法使用解决方案
把这组包装上，就不会提示后端未找到了。
```zsh
sudo pacman -S archlinux-appstream-data packagekit-qt5 flatpak fwupd
```
设置Kvantum
首先安装Kvantum Manager。

```
sudo zypper in kvantum-manager kvantum-manager-lang
```
然后需要安装一个Kvantum主题，这边依旧选择McMojave主题，可以从KDE Store下载。

之后将下载下来的tar.xz压缩包解压，然后打开Kvantum Manager，选择这一个文件夹，安装主题。

Discover是KDE桌面环境中的软件包管理器，可以方便地搜索、安装和卸载软件包。以下是在Arch Linux上安装Discover及其相关依赖的步骤：
安装Discover及其相关依赖：
```
sudo pacman -S discover packagekit-qt5 packagekit
```
重新启动Plasma Shell：
```
killall plasmashell
kstart5 plasmashell
```

### bluetooth

要检查您的 Arch Linux 系统是否支持蓝牙，请按照以下步骤进行操作：

确认您的计算机是否具有蓝牙硬件。您可以在终端中运行以下命令来检查：
```
lspci | grep -i bluetooth
```
如果输出结果中包含 Bluetooth 控制器，则表示您的计算机具有蓝牙硬件。

确认您的系统是否已经安装了蓝牙软件。您可以在终端中运行以下命令来检查：

```
pacman -Qs bluez
```
如果输出结果中显示 bluez 软件包，则表示您的系统已经安装了蓝牙软件。

确认 Bluetooth 服务是否已经启动。您可以在终端中运行以下命令来检查：
```
systemctl status bluetooth
```
如果输出结果中显示 Bluetooth 服务已经启动，则表示您的系统支持蓝牙。

如果输出结果中显示 Bluetooth 服务未启动，则可以运行以下命令启动它：

```
sudo systemctl start bluetooth
```
您也可以运行以下命令使 Bluetooth 服务在系统启动时自动启动：

```
sudo systemctl enable bluetooth
```
在 Arch Linux Plasma 中安装蓝牙支持需要执行以下步骤：

确认您的系统已经安装了蓝牙软件包。您可以使用以下命令来检查：

```
pacman -Ss bluez
```
如果输出结果中显示了 bluez 软件包，则表示已经安装了蓝牙软件包。

安装 bluez-utils 和 bluez-firmware 软件包。这些软件包包含了一些必要的工具和固件，以便支持蓝牙硬件：

```
sudo pacman -S bluez-utils bluez-firmware
```
安装 plasma-pa 软件包。这是 KDE 的音频设置工具，可以在蓝牙设备中管理音频输出。

```
sudo pacman -S plasma-pa
```
启动蓝牙服务：

```
sudo systemctl start bluetooth
```
如果您想要系统启动时自动启动蓝牙服务，请运行以下命令：

```
sudo systemctl enable bluetooth
```


在连接蓝牙耳机时，出现 br-connection-profile-unavailable 的错误可能是由于以下原因导致的：

没有安装蓝牙音频支持软件包。请检查是否已经安装了 bluez-alsa 软件包。如果没有安装，请运行以下命令安装它：

```
sudo pacman -S bluez-alsa
```
蓝牙音频协议（A2DP）未能正常连接。您可以尝试重启蓝牙服务并重新连接耳机。执行以下命令：

```
sudo systemctl restart bluetooth
```
蓝牙配置文件不可用。您可以尝试删除 ~/.config/pulse 目录，然后重启蓝牙服务并重新连接耳机。执行以下命令：

```
rm -rf ~/.config/pulse
sudo systemctl restart bluetooth
```
未启用 pulseaudio-bluetooth 模块。请打开 /etc/pulse/default.pa 文件，并确保以下行未被注释掉：

```
load-module module-bluetooth-policy
load-module module-bluetooth-discover
```
如果这些行被注释掉了，请取消注释它们，并保存文件。然后，重启 PulseAudio 服务：

```
pulseaudio -k
pulseaudio --start
```
检查蓝牙服务是否正在运行：
```
systemctl status bluetooth
```
如果蓝牙服务未启动，您可以使用以下命令启动它：
```
sudo systemctl start bluetooth
```

src/service.c:btd_service_connect() a2dp-sink profile connect failed for 64:68:76:46:53:C9: Protocol not available
这个报错可能意味着您的系统没有安装所需的蓝牙协议。您可以尝试安装相应的软件包来解决此问题。例如，在Arch Linux上，您可以使用以下命令安装BlueZ和相关的软件包：
```
sudo pacman -S bluez bluez-utils pulseaudio-bluetooth
```
如果您已经安装了这些软件包，您可以尝试重新启动蓝牙服务以解决问题：
```
sudo systemctl restart bluetooth.service
```
```
Mar 11 15:07:38 happytimes bluetoothd[16905]: profiles/audio/vcp.c:vcp_init() D-Bus experimental not enabled
Mar 11 15:07:38 happytimes bluetoothd[16905]: src/plugin.c:plugin_init() Failed to init vcp plugin
Mar 11 15:07:38 happytimes bluetoothd[16905]: profiles/audio/mcp.c:mcp_init() D-Bus experimental not enabled
Mar 11 15:07:38 happytimes bluetoothd[16905]: src/plugin.c:plugin_init() Failed to init mcp plugin
Mar 11 15:07:38 happytimes bluetoothd[16905]: profiles/audio/bap.c:bap_init() D-Bus experimental not enabled
Mar 11 15:07:38 happytimes bluetoothd[16905]: src/plugin.c:plugin_init() Failed to init bap plugin
```
这些报错信息表明，蓝牙服务加载插件时发生了错误，因为DBus实验性特性没有启用。插件的作用是为蓝牙协议提供支持。要解决这个问题，可以尝试启用DBus实验性特性或者检查是否安装了必要的依赖包。可以尝试执行以下命令来安装和启用DBus实验性特性：
```
sudo pacman -S dbus-x11
sudo nano /etc/dbus-1/system.conf
```
在<config>标签中添加以下内容：
```
<experimental enable="1"/>
```
保存并退出，然后重启系统。如果还是无法解决问题，可以尝试卸载和重新安装bluez和bluez-utils软件包。

要将蓝牙服务设置为开机自启，可以使用systemd。

以下是设置蓝牙服务开机自启的步骤：

创建一个名为bluetooth.service的服务文件。
在终端中输入以下命令，使用nano编辑器创建服务文件：
```
sudo nano /etc/systemd/system/bluetooth.service
```
在终端中输入以下命令，以启用服务：

```
sudo systemctl enable bluetooth.service
```
现在，蓝牙服务将在系统启动时自动启动。


