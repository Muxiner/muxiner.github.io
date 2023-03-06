---
title: Git 学习......
math: true
hide: false
date: 2023-02-22 22:35:06
updated: 2023-03-6 21:50:55
excerpt: Git 学习过程的记录，烂笔头持续记录。
categories: Git
tags: Git
index_img:
banner_img:
sticky: 99
---

### 常用 Git 命令
以下是一些常用的 Git 命令：

+ `git init`：初始化一个 Git 仓库
+ `git clone [url]`：从远程仓库克隆代码到本地
+ `git add [file]`：将文件添加到暂存区
+ `git commit -m "[message]"`：提交暂存区中的文件到版本库，并添加一条提交信息
+ `git status`：查看当前仓库状态
+ `git log`：查看提交日志
+ `git pull`：从远程仓库拉取最新代码
+ `git push`：将本地代码推送到远程仓库
+ `git branch`：查看当前仓库的所有分支
+ `git checkout [branch]`：切换分支
+ `git merge [branch]`：将指定分支合并到当前分支
+ `git diff [file]`：查看文件差异
+ `git stash`：将当前未提交的改动暂存起来
+ `git reset [file]`：将文件从暂存区中移除
+ `git revert [commit]`：撤销指定的提交
+ `git tag [name]`：给当前提交打标签
+ `git remote`：查看远程仓库信息
+ `git config`：配置 Git

以上只是一些常用的 Git 命令，Git 还有很多其他命令和选项，可以通过 `git --help` 查看 Git 的帮助文档来了解更多信息。

-----


### git init

`Git` 使用 `git init` 命令来初始化一个 `Git` 仓库，`Git` 的很多命令都需要在 `Git` 的仓库中运行，所以 `git init` 是使用 `Git` 的第一个命令。

在执行完成 `git init` 命令后，`Git` 仓库会生成一个 `.git` 目录，该目录用于追踪管理版本库，不建议手动修改该文件夹。

{% note info %}

`.git` 目录：
包含所有 git 操作的所需要文件。

`git init` 初始化后的目录结构：
```bash
$ tree
.
└── .git
    ├── HEAD
    ├── branches
    ├── config
    ├── description
    ├── hooks
    │   ├── applypatch-msg.sample
    │   ├── commit-msg.sample
    │   ├── fsmonitor-watchman.sample
    │   ├── post-update.sample
    │   ├── pre-applypatch.sample
    │   ├── pre-commit.sample
    │   ├── pre-merge-commit.sample
    │   ├── pre-push.sample
    │   ├── pre-rebase.sample
    │   ├── pre-receive.sample
    │   ├── prepare-commit-msg.sample
    │   └── update.sample
    ├── info
    │   └── exclude
    ├── objects
    │   ├── info
    │   └── pack
    └── refs
        ├── heads
        └── tags

10 directories, 16 files
```

进行 `git add` + `git commit`，操作后的 `.git` 目录：
```
$ tree
.git
├── COMMIT_EDITMSG
├── HEAD
├── branches
├── config
├── description
├── hooks
│   ├── applypatch-msg.sample
│   ├── commit-msg.sample
│   ├── fsmonitor-watchman.sample
│   ├── post-update.sample
│   ├── pre-applypatch.sample
│   ├── pre-commit.sample
│   ├── pre-merge-commit.sample
│   ├── pre-push.sample
│   ├── pre-rebase.sample
│   ├── pre-receive.sample
│   ├── prepare-commit-msg.sample
│   └── update.sample
├── index
├── info
│   └── exclude
├── logs
│   ├── HEAD
│   └── refs
│       └── heads
│           └── master
├── objects
│   ├── 3d
│   │   └── 6bb1c51730683ab010f472f60eb96f1041eb86
│   ├── 86
│   │   └── 9644542e81a31cd5d0828cdaca22fcb4bf1dce
│   ├── ce
│   │   └── 013625030ba8dba906f756967f9e9ca394464a
│   ├── info
│   └── pack
└── refs
    ├── heads
    │   └── master
    └── tags

15 directories, 24 files
```
可以发现，进行了 `git add` 和 `git commit` 操作后的文件夹多出了：`COMMIT_EDITMSG` 文件、`index` 文件、`logs` 文件夹等等，`logs`、`objects`、`refs` 等文件夹下还会多出了子目录及文件。

简单介绍 .git 文件夹中内容：
- `COMMIT_EDITMSG`：保存有最新一次提交的 `commit message`，`git` 系统不会用上，仅是给用户一个参考。 
- `HEAD`：指向目前被检出的分支或提交记录。
- `branches`：存储本地分支的目录。
- `config`：包含项目特定的配置文件，例如例如用户名、邮箱、远程仓库等。
- `description`：GitWeb 程序使用此文件来获取 Git 仓库的简短描述。
- `hooks`：存储客户端或服务端的 Git 钩子（hooks）脚本的目录。Git 钩子是在 Git 特定的动作发生时自动运行的脚本程序，例如提交前、提交后、合并时等。
- `index`：包含一个暂存区域，用于在提交之前暂存更改。
- `info`：存放一些 Git 的临时信息，例如排除一些不需要版本控制的文件、记录 Git 所有分支的最后一次提交的时间戳等。
- `info/exclude`：指定 Git 忽略文件的规则。
- `logs`：存放 Git 引用日志，记录每个引用的提交历史。
- `logs/HEAD`：存储引用的更改历史。
- `logs/refs/heads`：存储本地分支的更改历史。
- `objects`：存储 Git 数据库中的所有内容。
  - `info`：存储 Git 数据库的一些元数据信息。
  - `pack`：存储 Git 压缩的对象文件。
- `refs/heads`：存储本地分支引用的目录。
- `refs/tags`：存储标签引用的目录。

{% endnote %}

### git clone 

`git clone` 以为**克隆**或**拷贝**，用作从现有的 Git 仓库克隆（下载）项目到本地。

直接克隆仓库：
```
git clone <repo>
```

克隆仓库到指定文件夹：
```
git clone <repo> <dir>
```

克隆**速度过慢**或是**无响应时**，应选择走**代理加速下载**：
```
git clone https://xxxxxx.xxx/<repo>
# e.g:
# git clone https://ghproxy.com/https://github.com/xxxxx/xxxxx.git
```

### git branch

`git branch` 是 Git 中用来管理分支的命令。

以下是常见的 `git branch` 用法：
+ `git branch`: 查看本地分支列表。
+ `git branch <branch_name>`: 创建一个新的分支。
+ `git branch -d <branch_name>`: 删除指定的分支。
+ `git branch -r`: 查看远程分支列表。
+ `git branch -a`: 查看所有分支（本地和远程）的列表。
+ `git branch -m <old_branch_name> <new_branch_name>`: 将分支重命名。
+ `git branch --merged`: 查看已经合并到当前分支的分支。
+ `git branch --no-merged`: 查看尚未合并到当前分支的分支。
+ `git branch -vv`: 查看本地分支的详细信息，包括与远程分支的关联关系和最后一次提交。

{% note info %}

**新建分支时报错：**
```bash
$ git branch xxxxx
fatal: Not a valid object name: 'master'.
```
> 初学 `Git` 时，如果新建一个本地仓库的时候如果没有任何操作的情况下进行分支创建，会遇到该报错信息。

**原因：**
根据提示可以知道，原因是没有一个叫 `master` 的提交对象。你也可以执行一下 `git branch`，会发现没有看到本地分支列表（没有内容）：

其实，要先进行一次 `commit` 操作（进行一次提交操作），才会真正建立 `master` 分支。

这是因为分支的指针要指向提交的，只有进行了提交，才有指针指向该分支，才算是真正的建立了分支，成为一个有效的对象。

{% endnote %}

-----------


