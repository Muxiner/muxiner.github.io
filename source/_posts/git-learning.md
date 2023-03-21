---
title: Git 学习......
math: true
hide: false
date: 2023-02-22 22:35:06
updated: 2023-03-21 23:52:23
excerpt: Git 学习过程的记录，烂笔头持续记录。
categories: Git
tags: Git
index_img:
banner_img:
sticky: 99
---

## 常用 Git 命令
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


## git init

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

## git clone 

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

## git branch

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


## git checout

**`git checkout` 是 Git 中的一个重要命令，用于切换分支、回退版本、创建分支等操作。**

以下是 `git checkout` 常见的用法和问题：
+ `git checkout <branch_name>`：用于切换到另一个分支，例如 `git checkout dev` 将当前分支切换到名为 dev 的分支。
+ `git checkout <commit_id>`：用于切换到指定的提交版本，例如 `git checkout abc123` 将当前代码库切换到提交 ID 为 abc123 的版本。这个操作也称为“撤销”或“还原”代码。
+ `git checkout -b <new_branch_name>`：用于创建新的分支并切换到该分支，例如 `git checkout -b feature` 将创建一个名为 feature 的新分支，并将当前分支切换到 feature 分支。
+ `git checkout -- <file>`：用于丢弃本地未提交的更改，例如 `git checkout -- index.html` 将丢弃 index.html 文件中未提交的更改。

{% note info %}

**常见的关于 `git checkout` 的问题：**
+ 报错“error: Your local changes to the following files would be overwritten by checkout”

  如果在切换分支时出现此错误，表示您当前分支上的某些更改将覆盖目标分支上的文件。您可以使用以下命令保存本地更改，并在切换分支后再应用它们：
  ```bash
  git stash
  git checkout <target_branch>
  git stash apply
  ```

+ 报错“error: pathspec 'file_name' did not match any file(s) known to git.”

  如果在切换分支时出现此错误，表示您当前分支上没有名为 file_name 的文件。请检查文件名是否正确拼写，并确保文件已被添加到 Git 仓库中。

{% endnote %}


## git add

`git add` 命令用于将文件或文件夹添加到 Git 的暂存区（也称为索引）中，以便在提交时将其包含在版本控制中。

常见用法：
+ `git add <file_path>`：添加单个文件
+ `git add <folder_path>`：添加整个文件夹
+ `git add .`：添加当前目录下的所有文件和文件夹
+ `git add *.txt`：添加指定类型的文件，例如只添加 .txt 文件
+ `git add <folder_path>/`：添加指定文件夹下的所有文件和文件夹
+ `git add -A`：添加所有已修改的文件，包括删除的文件

在提交前，需要使用 `git status` 命令检查已暂存的文件和未暂存的文件的状态。如果文件已暂存，则它们将包括在下一次提交中。如果文件未暂存，则需要使用 `git add` 命令将其添加到暂存区中。

## git status

`git status` 命令用于显示当前 Git 仓库的状态，包括哪些文件已被修改、哪些文件已被添加到暂存区、哪些文件尚未被跟踪等信息。

常见用法：
+ `git status`：显示当前 Git 仓库的状态
+ `git status -v`：显示当前 Git 仓库的状态，并包括更详细的信息
+ `git status --short`：以简洁的方式显示当前 Git 仓库的状态
+ `git status --untracked-files`：显示未跟踪的文件

`git status` 命令是 Git 中最常用的命令之一，它可以帮助您了解当前仓库的状态，以便您决定是否需要执行其他操作，比如使用 `git add` 添加文件到暂存区或使用 `git commit` 提交更改。


## git commit

`git commit` 命令是 Git 中最常用的命令之一，用于将暂存区中的修改提交到本地仓库中。

常见用法：
+ `git commit -m "commit message"`：提交暂存区中的所有修改，并添加提交说明。
+ `git commit -a -m "commit message"`：直接将所有已跟踪的修改提交到本地仓库中，无需先执行 `git add`。
+ `git commit --amend`：修改最近一次提交的提交说明。
+ `git commit -v`：提交时显示文件的差异。
+ `git commit --no-verify`：提交时跳过 Git 钩子的验证。
+ `git commit --allow-empty`：允许提交空的提交记录。
+ `git commit --signoff`：提交时添加签名，通常用于公开的开源项目。
+ `git commit --fixup <commit>`：创建一个针对指定提交的 fixup 提交，用于后续使用 rebase 进行合并操作。


## git log

`git log` 是 Git 中用于查看提交历史的命令。它可以显示 Git 仓库中提交记录的详细信息，包括提交的 SHA 值、作者、提交时间、提交信息等。

常见的用法：
+ `git log`：显示所有提交记录，最近的提交记录排在最上面。
+ `git log -n`：显示最近的 n 个提交记录。
+ `git log --since=yyyy-mm-dd`：显示从指定日期开始的所有提交记录。
+ `git log --until=yyyy-mm-dd`：显示截止到指定日期为止的所有提交记录。
+ `git log --author=name`：显示指定作者的所有提交记录。
+ `git log --grep=pattern`：显示提交信息中包含指定模式的所有提交记录。
+ `git log --oneline`：以一行的形式显示提交记录，包括 SHA 值和提交信息。
+ `git log --graph`：以图形化的方式显示提交历史，可以更清晰地查看分支合并情况。
+ `git log --pretty=format:"format"`：使用指定的格式显示提交记录。format 是格式化字符串，可以包含各种占位符，如 %h 表示提交的短 SHA 值，%an 表示作者名等。
+ `git log --follow <file>`：显示指定文件的提交历史，包括文件的改名和移动。
+ `git log <branch1>..<branch2>`：显示两个分支之间的提交记录。


## git pull

`git pull` 是 Git 中用于从远程代码仓库中拉取最新代码到本地代码仓库中的命令。它会自动合并远程分支到当前分支，并更新本地代码仓库中的文件。

常见用法：
+ `git pull`：直接拉取并合并远程分支到当前分支。
+ `git pull origin <branch>`：拉取并合并指定远程分支到当前分支。
+ `git pull --rebase`：拉取并将本地未提交的修改变基到拉取的代码之上。
+ `git pull --rebase origin <branch>`：拉取并将本地未提交的修改变基到指定的远程分支之上。

需要注意的是，如果本地分支与远程分支之间存在冲突，则 `git pull` 会失败，并提示用户手动解决冲突后再进行提交。

## git push

`git push` 命令用于将本地仓库的代码推送到远程仓库，以便在多个开发者之间共享代码。

通常情况下，`git push` 命令将本地代码推送到与之关联的远程仓库的默认分支。

常见用法：
+ `git push`: 将当前分支的代码推送到关联的远程仓库的默认分支。
+ `git push <remote> <branch>`: 将本地指定分支的代码推送到关联的远程仓库的指定分支。
+ `git push --all`: 将所有本地分支的代码推送到关联的远程仓库。
+ `git push --force`: 强制推送本地代码到远程仓库。该命令会覆盖远程仓库上的修改，慎用。
+ `git push --tags`: 将本地的标签推送到关联的远程仓库。

## 部分问题

### remote rejected

```zsh
To https://github.com/Muxiner/muxiner.github.io.git
 ! [remote rejected] source -> source (refusing to allow a Personal Access Token to create or update workflow `.github/workflows/acitons.yml` without `workflow` scope)
```
上述是 `git push` 时的报错。

这个错误提示说明在使用 Personal Access Token(PAT) 授权推送代码时，没有为该令牌授予 workflow 权限，导致 GitHub Actions 无法更新或创建 workflows。

解决该问题的办法是，重新为 PAT 添加 workflow 权限：
+ 打开 GitHub Settings 页面。
+ 选择 Developer settings > Personal access tokens。
+ 找到所使用的 PAT，并且点击 Edit 按钮。
+ 在 Scopes 栏中，勾选 workflow 权限。
+ 点击 Update token 保存修改。
+ 现在，再次推送代码，就应该可以成功触发 GitHub Actions 并自动部署了。

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/posts/2023-03-20-gitpush.png)

