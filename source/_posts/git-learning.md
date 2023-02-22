---
title: Git 学习......
math: true
hide: false
date: 2023-02-22 22:35:06
updated: 2023-02-22 22:35:42
excerpt: Git 学习过程的记录，烂笔头持续记录。
categories: Git
tags: Git
index_img:
banner_img:
sticky: 99
---

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
+ `COMMIT_EDITMSG`：保存有最新一次提交的 `commit message`，`git` 系统不会用上，仅是给用户一个参考。 
+ HEAD
+ branches
+ config
+ description
+ hooks
+ index
+ info
  + exclude
+ logs
  + HEAD
  + refs
    + heads
+ objects
  + info
  + pack
+ refs
  + heads
  + tags


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

