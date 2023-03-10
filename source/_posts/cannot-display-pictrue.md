---
title: 【水博客】解决 Github Pages + hexo 网页无法显示图片问题
author: Muxiner
date: 2022-04-06 13:34:24
updated: 2022-06-28 22:39:30
excerpt: 博客网站图床的使用。
categories: 水博客
tags: 
   - Markdown
---
<p class="note note-primary">
2022-06-28 更新：现已不使用该文章提示的方法托管博文图片，而是使用 github + picgo ~~+ coding~~，不过 coding 出了点小问题。
</p>

### 问题描述

md 文件中加入图片链接后，在网页上无法显示图片。  
<!--more-->

### 解决方案

1. 找到一个免费的图床——如 [路过图床](https://imgtu.com/)。
2. 
   ![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/posts/20220628224255.png)

3. 将需要放置在 `MarkDown` 文件中的图片上传到图床中，结果如下：
   ![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/posts/20220628224341.png)
   
4. 选择上述合适的语句，粘贴到 `MarkDown` 文件中合适的位置（要配合使用 MD 语法哦）。
   ![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/posts/20220628224400.png)

5. 解决后的效果  
    ![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/posts/20220628224424.png)
    
    就成功显示了。
    完美~~（暂时）~~解决问题，前提是电脑联网了或者图床没跑路。

### 紫薯布丁

不保证方法百分百解决您的问题，仅仅提供一个方案（能解决我的问题的方案），无法解决的话，请您继续百度以查看他人的方法。  

### 参考

+ [github+hexo博客无法显示图片解决办法](https://www.dazhuanlan.com/2019/10/16/5da647c849379/)