---
title: 使用 SSH 密钥对 git push 进行身份验证
date: 2023-03-09 00:33:07
updated: 2023-03-09 00:33:31
excerpt: 简单介绍一下使用 SSH 密钥对 git push 进行身份验证，避免每次输入用户名及验证内容，或者是使用 git 凭证。
categories: Git
tags: [Git, SSH]
index_img:
banner_img:
sticky:
---

### 简单介绍

当咱首次使用 `git push` 命令时，会要求咱输入 GitHub 账户的 username 和 password，这中**基本身份验证**在 **2021.8.13** 以前还是可以的，之后的话，就会报错啦：
```
remote: Support for password authentication was removed on August 13, 2021.
remote: Please see https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories#cloning-with-https-urls for information on currently recommended modes of authentication.
```
要进行身份验证的话就得使用其他的办法，先咱已知两种：
1. **SSH 密钥身份验证**
2. **Personal Access Token（PAT）身份验证**：
   Personal Access Token 是一种令牌，可用于代替密码进行身份验证。可以在 GitHub、GitLab 或 Bitbucket 等 Git 托管服务中生成 PAT ，并在进行远程操作时使用它。生成 PAT 的过程可能因服务而异，但通常都可以在帐户设置中找到相关选项。

第二种方法较为复杂，就暂且不适用，简单介绍一下第一种的使用方法。

### SSH 身份验证

**推荐使用的操作系统：Linux**

#### 生成 SSH 密钥

如果您已经有 SSH 密钥对，可以跳过这一步。否则，您可以在终端中输入以下命令来生成新的 SSH 密钥：
```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
在提示符下，按照默认设置一路回车即可。

这将在 `~/.ssh` 目录下生成 `id_rsa` 和 `id_rsa.pub` 两个文件，其中 `id_rsa` 是私钥，`id_rsa.pub` 是公钥。
> 按照提示操作，生成一个 SSH 密钥对。
> 提示中显示 SSH 密钥对存放的路径。一般默认位置 `~/.ssh`。

#### 添加公钥到 Git 账户

将 `id_rsa.pub` 文件的内容复制到 Git 账户的 SSH 密钥设置中。

#### 在本地 Git 仓库中配置 SSH 协议

在终端中进入您的git仓库，输入以下命令：
```bash
git remote set-url origin git@github.com:user/repo.git
```
将 `user/repo.git` 替换为 `git` 仓库的 `URL`。这将把 `git` 仓库的 `URL` 从 `HTTPS` 协议改为 `SSH` 协议。

#### 添加私钥到 ssh-agent

将 SSH 私钥（默认为 `~/.ssh/id_rsa`）添加到 ssh-agent 中，以便在进行 SSH 连接时无需每次都输入私钥密码。

> 当您尝试连接到需要身份验证的远程服务器时，ssh-agent 会自动使用保存在其中的私钥进行身份验证。如果您没有使用 ssh-add 命令将私钥添加到 ssh-agent 中，则需要在每次尝试连接时手动输入私钥密码。

执行命令：
```bash
ssh-add ~/.ssh/id_rsa
```

#### git push

然后就可以 Git push 了，根据提示仔细应对就行。

#### 问题

执行 命令 `ssh-add ~/.ssh/id_rsa`，shell 报错：
```bash
Could not open a connection to your authentication agent.
```

这个错误提示通常表示 ssh-agent 没有启动或者没有在当前 shell 中正确地配置。需要进行以下操作：

1. 确保已经安装了 `ssh-agent`。
   如果使用的是 Linux 或 Mac 系统，通常它已经默认安装了。可以在终端中输入以下命令检查：
   ```bash
   ssh-agent -h
   ```
   如果系统已经安装了 `ssh-agent`，它会输出 `ssh-agent` 的帮助信息。否则，可以使用系统包管理器来安装它。

2. `ssh-agent`已经启动，请使用以下命令检查它的进程 `ID`：
   ```bash
   echo $SSH_AGENT_PID
   ```
   如果没有输出任何内容，说明 `ssh-agent` 没有在当前 `shell` 中正确地配置。
   
   可以使用以下命令启动 `ssh-agent`，并将其添加到当前 `shell`中：
   ```bash
    eval "$(ssh-agent -s)"
    ```
3. 添加私钥：
    一旦 `ssh-agent` 已经启动并添加到了当前 `shell` 中，请使用以下命令添加私钥到 `ssh-agent` 中：
    ```bash
    ssh-add ~/.ssh/id_rsa
    ```
    
    如果还是出现 "Could not open a connection to your authentication agent." 错误，请尝试重启 `ssh-agent`：
    ```bash
    ssh-agent -k
    eval "$(ssh-agent -s)"
    ssh-add ~/.ssh/id_rsa
    ```
以上步骤应该能够解决这个问题。


### 参考

**神奇海螺**
