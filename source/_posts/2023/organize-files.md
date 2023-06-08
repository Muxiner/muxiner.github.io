---
title: Hexo 文章管理：子文件夹管理 + 保留文章永久链接
comment: giscus
math: true
hide: false
date: 2023-06-08 17:04:15
updated: 2023-06-08 17:04:15
excerpt: 使用年份子文件夹管理 Hexo 文章，并保留文章的永久链接（之前的链接）。
categories: Blog
tags: Blog
index_img:
banner_img:
sticky:
---

最近使用 Mkdocs + Material for Mkdocs 编辑文档网站，一顿实践下来，就习惯干净整洁的项目结构，一个个文件都比较容易找到，看着也不乱。

然后看到许久未更新的博客，就想着过来水一水。结果所有的文章都是堆在 `source/_post` 下面，像是一团乱麻，而且找起之前的文章也是十分的不方便，就想着能不能整理一下，看着清爽一点。

于是一番搜索后，发现大佬们有着不错的想法：
+ [使用子文件夹管理 Hexo 文章且不改变文章永久链接 | PRIN BLOG](https://prinsss.github.io/hexo-posts-in-subfolder/)
+ [如何在 Hexo 中对文章 md 文件分类 | Sea](https://mrseawave.github.io/blogs/articles/2021/06/25/hexo-new-post-path/)

简单查看后，明白了应该怎么实现简单的文章整理 + 保留文章的永久链接。

主要修改的文件是：`_config.yml` —— 主题配置文件。

+ `permalink`：用于设置文章的永久链接格式
+ `new_post_name`：新文章的文件名称

需要修改的位置也只是上述两个字段，对于我而言，只需要修改**新文章的文件名称**，永久链接格式，我之前已经修改了 —— 直接使用 `url/:name/` 的格式，看着直观清爽。

所以修改一下 `new_post_name` 为 `:year/:title.md` ，即，新文章自动创建在年份的文件夹下，如本文 markdown 文件的创建过程：

```bash
$ hexo new post organize-files
INFO  Validating config
INFO  Created: ....\blog\source\_posts\2023\organize-files.md
```

故而 `_config.yml` 文件修改为：

```yml
permalink: :name/
new_post_name: :year/:title.md
```

虽然修改了站点配置文件，但是咱们文章的整理还是 “比较” 麻烦，文章太多，创建时间也不是那么好查看，一个个的移动真的挺麻烦。

不过好在，[使用子文件夹管理 Hexo 文章且不改变文章永久链接 | PRIN BLOG](https://prinsss.github.io/hexo-posts-in-subfolder/) 中给了我答案：使用命令行命令批量整理源文件 - `grep -r "date: '2015-" *.md -l | xargs mv -v -t 2015/`。

我直接照葫芦画瓢：

```bash
$ grep -r "date: 2020-" *.md -l | xargs mv -v -t 2020/
已重命名 'csapp-bomb.md' -> '2020/csapp-bomb.md'
已重命名 'datalab-handout.md' -> '2020/datalab-handout.md'
已重命名 'git-password.md' -> '2020/git-password.md'
已重命名 'hexo-blog-encrypt.md' -> '2020/hexo-blog-encrypt.md'
已重命名 'using-github-actions.md' -> '2020/using-github-actions.md'
已重命名 'vscode-env-c-old.md' -> '2020/vscode-env-c-old.md'

$ grep -r "date: 2021-" *.md -l | xargs mv -v -t 2021/
已重命名 'C-create-link.md' -> '2021/C-create-link.md'
已重命名 'mean-of-life.md' -> '2021/mean-of-life.md'

$ grep -r "date: 2022-" *.md -l | xargs mv -v -t 2022/
已重命名 'cannot-display-pictrue.md' -> '2022/cannot-display-pictrue.md'
已重命名 'cannot-ssh-connect-with-ps.md' -> '2022/cannot-ssh-connect-with-ps.md'
已重命名 'console-lang=en.md' -> '2022/console-lang=en.md'
已重命名 'cygwin-installation.md' -> '2022/cygwin-installation.md'
已重命名 'discrete-mathematics-basic-concept-graph.md' -> '2022/discrete-mathematics-basic-concept-graph.md'
已重命名 'discrete-mathematics-color-graphic.md' -> '2022/discrete-mathematics-color-graphic.md'
已重命名 'discrete-mathematics-elatu-hamilton.md' -> '2022/discrete-mathematics-elatu-hamilton.md'
已重命名 'discrete-mathematics-graph-connectivity.md' -> '2022/discrete-mathematics-graph-connectivity.md'
已重命名 'discrete-mathematics-graph-matrix.md' -> '2022/discrete-mathematics-graph-matrix.md'
已重命名 'discrete-mathematics-path-circuit.md' -> '2022/discrete-mathematics-path-circuit.md'
已重命名 'discrete-mathematics-plane-map.md' -> '2022/discrete-mathematics-plane-map.md'
已重命名 'discrete-mathematics-set-knowledge.md' -> '2022/discrete-mathematics-set-knowledge.md'
已重命名 'discrete-mathematics-tree.md' -> '2022/discrete-mathematics-tree.md'
已重命名 'git-proxy-error.md' -> '2022/git-proxy-error.md'
已重命名 'good-skills-record.md' -> '2022/good-skills-record.md'
已重命名 'install-microsoft-store.md' -> '2022/install-microsoft-store.md'
已重命名 'linux-gurb-beauty.md' -> '2022/linux-gurb-beauty.md'
已重命名 'ml-boston-housing.md' -> '2022/ml-boston-housing.md'
已重命名 'ml-decision-tree.md' -> '2022/ml-decision-tree.md'
已重命名 'ml-lda.md' -> '2022/ml-lda.md'
已重命名 'ml-perceptron.md' -> '2022/ml-perceptron.md'
已重命名 'powershell-beauty.md' -> '2022/powershell-beauty.md'
已重命名 'scoop-replace-source.md' -> '2022/scoop-replace-source.md'
已重命名 'terminal-useing.md' -> '2022/terminal-useing.md'
已重命名 'ubuntu-error-unable-to-mkstemp.md' -> '2022/ubuntu-error-unable-to-mkstemp.md'
已重命名 'ubuntu-install-colorls.md' -> '2022/ubuntu-install-colorls.md'
已重命名 'ubuntu-update-failed.md' -> '2022/ubuntu-update-failed.md'
已重命名 'ubuntu-ustc-sources.md' -> '2022/ubuntu-ustc-sources.md'
已重命名 'ubuntu-zsh-ohmyzsh.md' -> '2022/ubuntu-zsh-ohmyzsh.md'
已重命名 'use-wsl2-ubuntu.md' -> '2022/use-wsl2-ubuntu.md'
已重命名 'using-scoop.md' -> '2022/using-scoop.md'
已重命名 'vscode-env-c-new.md' -> '2022/vscode-env-c-new.md'
已重命名 'vscode-markdown-pdf-math-latex-error.md' -> '2022/vscode-markdown-pdf-math-latex-error.md'
已重命名 'vscode-plugins.md' -> '2022/vscode-plugins.md'
已重命名 'wsl-error-0x8007019e.md' -> '2022/wsl-error-0x8007019e.md'

$ grep -r "date: 2023-" *.md -l | xargs mv -v -t 2023/
已重命名 'adb-learning.md' -> '2023/adb-learning.md'
已重命名 'arch-kde-plasma.md' -> '2023/arch-kde-plasma.md'
已重命名 'archlinux-beauty.md' -> '2023/archlinux-beauty.md'
已重命名 'cannot-find-module-css.md' -> '2023/cannot-find-module-css.md'
已重命名 'git-learning.md' -> '2023/git-learning.md'
已重命名 'git-ssh-authentication.md' -> '2023/git-ssh-authentication.md'
已重命名 'install-uninstall-anaconda.md' -> '2023/install-uninstall-anaconda.md'
已重命名 'install-uninstall-python.md' -> '2023/install-uninstall-python.md'
已重命名 'kex-exchange-identification.md' -> '2023/kex-exchange-identification.md'
已重命名 'rename-by-rust.md' -> '2023/rename-by-rust.md'
已重命名 'rust-learning.md' -> '2023/rust-learning.md'
已重命名 'use-comment-giscus.md' -> '2023/use-comment-giscus.md'
已重命名 'vscode-quick-suggestions.md' -> '2023/vscode-quick-suggestions.md'
已重命名 'windows10-msys2-installation.md' -> '2023/windows10-msys2-installation.md'
已重命名 'yay-instead-pacman.md' -> '2023/yay-instead-pacman.md'
```
{% note info %}

```bash
grep -r "date: 2020-" *.md -l | xargs mv -v -t 2020/
```

这个命令的意思是在当前目录下查找所有扩展名为 .md 的文件中包含 "date: '2020-" 的行，并将这些文件移动到名为 2020 的目录中。

这需要**先创建 2020 目录**。否则：`mv: 访问 '2020/' 失败: No such file or directory`。

其次，要确定好 `grep` 命令查找的文件的内容 —— "date: 2020-"，该部分为每个 md 文件：

```markdown
date: 2023-06-08 17:04:15
```

的内容，这需要根据自己文件的情况敲命令，不要盲目复制啊，不要学我。

仔细一点后就没事了。

{% endnote %}