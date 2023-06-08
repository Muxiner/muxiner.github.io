---
title: 更改终端显示语言
math: true
hide: false
date: 2022-07-26 11:24:36
updated: 2022-07-26 11:24:36
excerpt: 在 linux 显示语言设置为中文后，终端的显示语言设置为 en。
categories:
- Linux
tags:
- console
- 记录
index_img:
banner_img:
sticky:
---

### 问题描述

将 linux (arch) 的语言设置为中文后，不仅是显示语言成功设置为中文，就连终端的显示（提示）语言也是中文，使用起来，总有种奇怪的感觉，觉得奇怪是因为习惯了全英文的终端显示。

所以想要将终端显示设置回英文。

经过多番搜索后，终于找到一个不错的解决方案。

### 解决方案

1. **打开终端**
2. **使用命令 `echo $0` 或是 `echo $SHELL` 查看当前使用的 `Shell`：**
   
    ```bash
    xxxx@xxxxx: ~$ echo $0
    /bin/bash
    ```

    ```bash
    xxxx@xxxxx: ~$ echo $SHELL
    /bin/bash
    ```
    > 一般 `shell` 类型：`bash`、`zsh`。
3. **使用编辑器打开配置文件**
    编辑器可选取：`Vim`、`nano`。
    `bash` 的（用户）配置文件：`.bashrc` 或是 `.bash_profile`
    > 编辑任一即可
    > `zsh` 的（用户）配置文件：`.zshrc`

    输入命令编辑器打开配置文件：

    ```bash
    nano ~/.bashrc
    ```
4. **编辑配置文件**
    在文件中加入下述内容：

    ```txt
    if [ "$TERM"="linux" ] ;then 
    export LANG=en_US.UTF-8 
    export LANGUAGE=en_US 
    fi
    ```
    保存。
5. **使配置文件生效**
   
   ```bash
   source ~/.bashrc
   ```
   > `zsh` 的配置文件生效命令同理。
