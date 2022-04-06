title: 解决Github + hexo网页无法显示图片问题
author: Muxiner
date: 2022-04-06 13:34:24
tags:
---

### 问题描述
md文件中加入图片链接后，在网页上无法显示图片。  
<!--more-->

### 解决方案

1.修改站点配置文件(博客目录下的)`_config.yml`  

+ 改`post_asset_folder: false`为`true`。
```yml
#启动 Asset 文件夹 （用来存放相对路径图片或文件）
post_asset_folder: true
```
2.安装插件，在命令窗口输入  
```git
npm install https://github.com/CodeFalling/hexo-asset-image -- save
```

3.在markdown编辑时引入图片  
例如：  

首先创建博客及其文件夹  
```git
hexo new XXXXXX
# XXXXX 为 文件名
```
或者您手动”新建文件夹“  

结果如下  
![文件目录](cannot-display-pictrue/menu.png)

然后md文件中再合适的位置插入图片链接  
```md
![result](datalab-handout/datalab-handout.png) 
```
> result 为 图片描述  
> datalab-handout/datalab-handout.png为图片保存路径  

4.解决后的效果  
![](cannot-display-pictrue/display.png)  
就成功显示了。

### 紫薯布丁
不保证方法百分百解决您的问题，仅仅提供一个方案（能解决我的问题的方案），无法解决的话，请您继续百度以查看他人的方法。  

参考：  
[github+hexo博客无法显示图片解决办法](https://www.dazhuanlan.com/2019/10/16/5da647c849379/)