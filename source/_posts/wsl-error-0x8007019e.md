---
title: Windows 安装 WSL Ubuntu 出现错误代码：0x8007019e
math: true
hide: false
date: 2022-10-28 20:42:46
updated: 2022-10-28 21:26:29
excerpt: Windows 安装 WSL Ubuntu 出现错误：Installation Failed! Error：0x8007019e
categories: 
- 教程
- 记录
tags:
- Ubuntu
- install
index_img:
banner_img:
sticky:
---

近期为了方便自己重装系统，准备整一个适用自己的系统镜像，想着给它也整个 WSL Ubuntu 省的后面重装后还麻烦。

由于咱选取了 `windows 10 企业版 LTSC`，为了搞 linux 子系统也是要费不少功夫，其他的先不谈，直接到 Ubuntu 的使用。

下载完 Ubuntu 后点击使用，一开始就出现该错误：

```
Installing, this may take a few minutes...
Installation Failed!
Error: 0x8007019e
Press any key to continue...
```

一番搜索后发现 —— **未安装 Windows 子系统支持**

**解决办法**：
+ 必须启用“适用于 Linux 的 Windows 子系统”可选功能并**重启**，然后才能在 Windows 上运行 Linux 发行版。
+ 以管理员身份运行 `PowerShell`，并执行下列命令：
  
  ```pwershell
  Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
  ```

重启完后打开 Ubuntu 等一会就行了。

### 参考
+ [在windows应用商店安装ubuntu系统，报错WslRegisterDistribution failed with error: 0x8007019e](https://www.cnblogs.com/cai1432452416/p/11748610.html)
+ [Windows Server 安装指南](https://learn.microsoft.com/zh-cn/windows/wsl/install-on-server)