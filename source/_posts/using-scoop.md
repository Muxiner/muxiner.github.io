---
title: Windows 下包管理器 Scoop 的安装与使用
math: true
date: 2022-05-30 23:59:37
categories:
tags:
index_img:
banner_img:
excerpt: 本文所写为 `Windows 11` 下包管理器 `Scoop` 的安装与使用
---


###  🍉 什么是 Scoop

> 😶‍🌫️ 可以去看 [Scoop Github 上的介绍](https://github.com/ScoopInstaller/Scoop)。
>
> 😶‍🌫️ 还有官方文档 [Scoop Wiki](https://github.com/ScoopInstaller/Scoop/wiki)
>
> 😶‍🌫️ 官网 [Scoop.sh](https://scoop.sh/)

`Scoop` 是 `Windows` 上的命令行安装工具。

🙈 可以用来干嘛？

🦥 通过命令行界面，`Scoop` 可以顺畅地安装应用程序。（官方说明）

+ 🌲 没有权限弹出窗口
+ 🌲 隐藏 GUI 向导式安装程序
+ 🌲 防止因而安装大量程序造成 PATH 污染
+ 🌲 避免安装和卸载程序的不当使用
+ 🌲 自动查找并安装依赖项
+ 🌲 自动执行所有额外的设置步骤来获取工作程序

###  🍉 安装 Scoop

####  🍊 准备工作

+ `PowerShell` ：	确保已安装 `PowerShell 5.0` 或更高版本。

  > `Windows 10` 以及更高的版本默认安装的 `PowerShell 5.0`。

+ 确保以允许 `Powershell` 执行本地脚本。

  ```powershell
  set-executionpolicy remotesigned -scope currentuser
  ```

  > `Unrestricted` 也可以，但是安全性较低。
  >
  > 最好使用 `RemoteSigned`。

###  🍉 安装 Scoop

####  🍑 安装在默认位置

默认安装在 `C:\Users\username\scoop` 路径下。

执行命令：

```powershell
Invoke-Expression (New-Object System.Net.WebClient).DownloadString('https://get.scoop.sh')
```

或是执行（更短的）：

```powershell
iwr -useb get.scoop.sh | iex
```

####  🍑 自定义安装目录

例如将 `Scoop` 安装在 `C:\Scoop` 路径下。

需要添加该路径到**用户变量**中：

```powershell
$env:SCOOP='C:\scoop'
```

```powershell
[environment]::setEnvironmentVariable('SCOOP',$env:SCOOP,'User')
```

> 当然也可以添加到**系统变量**中：
>
> 不过此时需要以**管理员身份**运行 `PowerShell` ，或是以**管理员身份**运行 `Windows Terminal`，再打开 `PowerShell` ，否则会报错：
>
> ```powershell
> [environment]::setEnvironmentVariable('SCOOP',$env:SCOOP,'Machine')
> ```

> <span style="color:red;">添加完环境变量后需要重启 PowerShell 或 Terminal 等待变量生效。</span>

然后再执行安装指令：

```powershell
iwr -useb get.scoop.sh | iex
```
![](https://munner.coding.net/p/blogpicgo/d/blogimages/git/raw/main/md_img/20220529150626.png)

> 出现上图所示，且无错误提示，则安装成功。



####  🍑 自定义全局应用安装目录

例如自定义将全局应用安装在 `C:\apps` 路径下：

就需要将该目录添加到系统变量中，步骤同上文相同：

1. 😶‍🌫️ 以管理员身份运行
2. 😶‍🌫️ `$env:SCOOP_GLOBAL='C:\apps'`
3. 😶‍🌫️ `[environment]::setEnvironmentVariable('SCOOP_GLOBAL',$env:SCOOP_GLOBAL,'Machine')`
4. 😶‍🌫️ 安装指令：`scoop install -g <app>`

合起来就是：

```powershell
$env:SCOOP_GLOBAL='C:\apps'
[environment]::setEnvironmentVariable('SCOOP_GLOBAL',$env:SCOOP_GLOBAL,'Machine')
scoop install -g <app>
```

###  🍉 使用 Scoop

查看 scoop 的命令：

```powershell
scoop help
```

查看命令的详细信息：

```powershell
scoop help <command>
# for example: scoop help install 
# For more detailed information on INSTALL
```

执行 `scoop help install `：

```powershell
Usage: scoop install <app> [options]

e.g. The usual way to install an app (uses your local 'buckets'):
     scoop install git

To install an app from a manifest at a URL:
     scoop install https://raw.githubusercontent.com/ScoopInstaller/Main/master/bucket/runat.json

To install an app from a manifest on your computer
     scoop install \path\to\app.json

Options:
  -g, --global              Install the app globally
  -i, --independent         Don't install dependencies automatically
  -k, --no-cache            Don't use the download cache
  -u, --no-update-scoop     Don't update Scoop before installing if it's outdated
  -s, --skip                Skip hash validation (use with caution!)
  -a, --arch <32bit|64bit>  Use the specified architecture, if the app supports it
```



####  🍒 安装应用

分为两种情况：

#####  🫐 为当前用户安装

安装路径：`scoop\apps` 

> `scoop` 路径默认在 `C:\User\username` 。
>
> 若是自定义安装路径，例如上文的位置，则在 `C:\Scoop` 

安装命令：

```powershell
scoop install <app>
# for example:
# scoop install nano
```

#####  🫐 为所有用户安装

默认的安装路径：`C:\ProgramData\scoop`

若是如上文所示，自定义了全局应用安装目录，则安装路径：`C:\apps`

> 需要以**管理员身份**运行。

安装命令：

```powershell
scoop install <app> -g
# for example:
# scoop install nano -g
```

####  🍒 卸载应用

#####  🫐 卸载某一程序

```powershell
scoop uninstall <app>
```

#####  🫐 卸载程序并移除配置文件

```powershell
scoop uninstall <app> -p
```

#####  🫐 卸载全局程序

```powershell
scoop uninstall <app> -g
```

#####  🫐 更多信息

```powershell
scoop help uninstall
```



####  🍒 更新

#####  🫐 更新 scoop 及所有 bucket 但不更新 app

```powershell
scoop update
```

##### 🫐 更新某一 app

```powershell
scoop update <app>
```

##### 🫐 更新 scoop、bucket、app

```powershell
scoop update *
```

##### 🫐 更新全局 app

```powershell
scoop update <app> -g
```

##### 🫐 更多信息

```powershell
scoop help update
```



####  🍒 其他有用操作

##### 🫐 查看已安装 app

```powershell
scoop list
```

##### 🫐 查看可更新 app

```powershell
scoop status
```

##### 🫐 查看某 app 主页

```powershell
scoop home <app>
```

##### 🫐 查看「已知库」

```powershell
scoop bucket known
```

##### 🫐 添加「已知库」

```powershell
scoop bucket add <bucket>
```

##### 🫐 查看已添加的库

```powershell
scoop bucket list
```

##### 🫐 删除已添加的库

```powershell
scoop bucket rm <bucket>
```

##### 🫐 添加第三方库

```powershell
scoop bucket add <bucket> <bucket_url>
```

#####  🫐 删除已安装软件的旧版本

```powershell
scoop cleanup *
```

#####  🫐 清理软件缓存

通常是下载的软件安装包。

以下命令清除所有缓存，即清空 `Scoop` 目录下的 `cache` 文件夹。

```powershell
scoop cache rm *
```

###  🍉 进阶

更多信息请查看 [官方文档](https://github.com/ScoopInstaller/Scoop/wiki)。
