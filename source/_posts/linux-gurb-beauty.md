---
title: 使用 Gurb 进行多系统引导，并使用主题美化 Grub 界面
math: true
hide: false
date: 2022-07-24 21:48:44
updated: 2022-07-24 22:50:55
excerpt: 本记录用于记录 deepin 系统下对 Grub 启动页面进行美化。
categories:
- Archlinux
tags:
- Deepin
- Grub
- Beauty
index_img:
banner_img:
sticky:
---

咕咕咕，开始。

{% note primary %}
**2022-07-24** 更新：简单记录一下，未能添加前后对比图
{% endnote %}

### 更改 Deepin 的系统引导为 grub

1. `ctrl + alt + T` 打开终端，查看 `efi` 的挂载点
   
    ```bash
    lsblk
    # 查看 /boot/efi 的挂载点 
    ```

    查询到 `/boot/efi` 的挂载点是：`/dev/sda1`
2. 安装 `grub` 到 `efi` 挂载点
   
   ```bash
   sudo grub-install /dev/sda1
   ```
   > 安装成功时会提示下述内容：
   > Installation finished. No error reported.
   > 若是中文界面的终端：
   > 安装完成。没有错错误报告。

### 美化 grub 引导界面

#### 下载个人所喜欢的主题

主题网站：[GMOME-LOOK.ORG | GRUB THEME](https://www.gnome-look.org/browse?cat=109&ord=rating)

个人选择了 `Vimix` 主题。主题路径：[Grub-theme-vimix](https://www.gnome-look.org/p/1009236)

> 部分主题拥有适用于不同分辨率显示屏的版本，鉴于个人机器的硬件水平酌情选择，如：
> `1080p`、`4k`、`2k`。

下载方式：

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220724221058.png)

或是：

点击 `files`，再选择对应分辨率的文件。

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/md_img20220724221532.png)

#### 安装主题

1. 解压主题：
   + 使用命令行解压：
        ```bash
        tar -Jxf Vimix-1080p.tar.xz
        # tar -Jxf Vimix-2k.tar.xz
        # tar -Jxf Vimix-4k.tar.xz
        ```
      选择合适的命令解压。
   + 使用文件系统解压。 

2. 放置主题文件
   将解压出来的主题文件放置到系统的 `grub` 主题文件中去。

   例如：
   ```bash
   sudo cp Vimix /usr/share/grub/themes/Vimix -rf
   ```
   > 上述命令执行时，**所在的路径为 Vimix 文件夹所在路径**。

3. 修改系统配置

    编辑 grub 文件。

    ```bash
    sudo nano /etc/default/grub
    ```
    > 根据个人喜好选择编辑器如，nano、vim。

    然后修改 GRUB_THEME，这是 grub 的主题设置，默认注释掉。
    直接插入一行代码：
    ```
    GRUB_THEME="/usr/share/grub/themes/vimix/theme.txt"
    ```
    > 修改了引号中的路径，指向我们自定的主题文件的 `theme.txt`。

#### 更新 `grub.cfg` 文件

执行命令更新 `grub.cfg` 文件，使我们上述所作的设置生效。

```bash
sudo update-grub
```

### 重启查看效果

执行命令命令重启电脑：
```bash
sudo reboot
```

或是可视化的点点点，重启电脑。