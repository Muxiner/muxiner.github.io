---
title: Ubuntu 更换中科大软件源
math: true
hide: false
date: 2022-10-31 20:02:09
updated: 2022-10-31 20:02:56
excerpt: 为加快 Ubuntu 更新或者下载软件的速度，更换使用中科大软件源。
categories: 
- 记录
- Ubuntu
tags:
- Ubuntu
index_img:
banner_img:
sticky:
---

{% note success %}
为加快 Ubuntu 更新或者下载软件的速度，更换使用中科大软件源。

还可以使用其他的软件源，如清华源、阿里源等等。

需要根据自身网络情况选择合适的软件源，以寻求最快的下载速度。

> 目前咱这边使用中科大源优于清华源。
{% endnote %}

### 更换步骤

> Ubuntu 系统中，软件源文件地址：`/etc/apt/sources.list`

1. （选用）备份软件源
   ```bash
    sudo cp /etc/apt/sources.list /etc/apt/sources.list.backup
   ```
   > 方便以后可以使用原来的软件源
2. **添加中科大软件源**
   + **有备份软件源情况**
      ```bash
      sudo nano /etc/apt/sources.list
      ```
      将之前的所有内容全部删除，然后添加如下内容。
      > 滚包的时候似乎更快。
    
   + **无备份软件源**
     直接复制内容，粘贴到文件最前面。

    {% note secondary %}
    不同的 Ubuntu 发行版有不同的软件源，不同的地方只有字符中的 **jammy** 字样。这个是 `Ubuntu Codename` (别名)。可以执行 `lsb_release -a` 命令进行查看：
    ```bash
    muxiner@DESKTOP-ATVFS68:~$ lsb_release -a
    No LSB modules are available.
    Distributor ID: Ubuntu
    Description:    Ubuntu 22.04.1 LTS
    Release:        22.04
    Codename:       jammy
    ```
    下方内容中的 `jammy` 字段需要根据自身 Ubuntu 版本情况进行更改。
    {% endnote %}
    ```txt
       deb https://mirrors.ustc.edu.cn/ubuntu/ jammy main restricted universe multiverse
       # deb-src https://mirrors.ustc.edu.cn/ubuntu/ jammy main restricted universe multiverse
       deb https://mirrors.ustc.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse
       # deb-src https://mirrors.ustc.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse
       deb https://mirrors.ustc.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse
       # deb-src https://mirrors.ustc.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse
       deb https://mirrors.ustc.edu.cn/ubuntu/ jammy-security main restricted universe multiverse
       # deb-src https://mirrors.ustc.edu.cn/ubuntu/ jammy-security main restricted universe multiverse multiverse
      ```
    
    完成编辑后要保存。

3. **更新**
   + 更新源：
     ```bash
     sudo apt update
     ```
   + 如出现依赖问题，解决方式如下：
     ```bash
     sudo apt -f insatll
     ```
   + 更新软件：
     ```bash
     sudo apt upgrade
     ```

### 参考
+ [Ubuntu 镜像使用帮助](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/)
  > 这个真好，可以自己选择版本，然后直接复制。

  > 也可以更换成科大源，替换字符：`tuna.tsinghua` $\rightarrow$ `lstc`，就行。
  
+ [Ubuntu20.04软件源更换](https://zhuanlan.zhihu.com/p/142014944)