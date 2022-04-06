---
title: git push 不用每次输入用户名和密码
date: 2020-11-24 12:00:23
categories: Blogs
tags:
- Blogs
- Git

---
**本文仅供参考**


#### 问题描述
每次 `git push` 时都要输入用户名和密码，觉得很累。  就想只输入一次将用户名密码保存下来，避免每次都要重新输入。  

#### 方法
```git
git config --global credential.helper store
```
```git
git pull /git push 
# (这里需要输入用户名和密码，以后就不用啦)
```
push你的代码 (git push), 这时会让你输入用户名和密码, 这一步输入的用户名密码会被记住, 下次再push代码时就不用输入用户名密码 ! 这一步会在用户目录下生成文件.`git-credential` 记录用户名密码的信息。

然后就可以了。
#### 结果 
emmm，使用方法之前，我需要输入两次用户名密码，使用后我只需要输入一次啦，这是一次巨大的”成功“。  
[![qvAb4g.jpg](https://s1.ax1x.com/2022/04/06/qvAb4g.jpg)](https://imgtu.com/i/qvAb4g)
#### 参考
[git不用每次输入用户名和密码](https://blog.csdn.net/LosingCarryJie/article/details/73801554)