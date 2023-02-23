---
title: 好东西就记录下来.jpg
date: 2022-07-12 16:38:19
updated: 2023-02-24 02:36:06
excerpt: The palest ink is better than the best memory. 好记性不如烂笔头。记不住那就记录下来。
categories: 
- 记录
tags:
- Skills
index_img:
banner_img:
math: true
sticky: 100
---

{% note primary %}
**2022-07-12** 更新
{% endnote %}
### PowerShell 获取系统时间

> 人懒不想每次写博文、更新博文时手敲日期和时间，就想偷懒，使用命令行格式化输出想要的时间。

> 较多使用 Windows 系统，因为使用 PowerShell 获取时间。

**基础命令**：
+ `Get-Date`: 获取当前**时间**
+ `Get-Date -Format 'yyyy'`: 获取当前**年份**
+ `Get-Date -Format 'MM'`: 获取当前**月份**
+ `Get-Date -Format 'dd'`: 获取当前**日**
+ `Get-Date -Format 'HH'`: 获取当前**时**（24 小时制）
+ `Get-Date -Format 'hh'`: 获取当前**时**（12 小时制）
+ `Get-Date -Format 'mm'`: 获取当前**分**
+ `Get-Date -Format 'ss'`: 获取当前**秒**

<span style="color: #02b2ff; ">自由组合一下获得格式化的日期或者时间：</span>

```powershell
Get-Date -Format 'yyyy-MM-dd'
# 2022-07-12

Get-Date
# 2022年7月12日 17:47:14

Get-Date -Format 'HH:mm:ss'
# 17:47:56

Get-Date -Format 'yyyy-MM-dd HH:mm:ss'
# 2022-07-12 17:48:25

Get-Date -Format 'yyyy年M月dd日 HH时mm分ss秒'
# 2022年7月12日 17时52分42秒
```
但是每次获取格式化时间时都需要输入这么多字符也很麻烦，那就使用 alias：
```powershell
echo 'Function now {get-date -format "yyyy-MM-d HH:mm:ss"}' >> $profile
```
> 意思就是，将 `Function now {get-date -format "yyyy-MM-d HH:mm:ss"}` 追加到 `$PROFILE` 文件里。
> 上述命令含义是：`now` 代替 `get-date -format "yyyy-MM-d HH:mm:ss"`。
> 二者效果相同。

然后： 
```powershell
now
# 2022-07-12 18:01:15
```
----------------------------------

{% note primary %}
**2023-02-21** 更新
{% endnote %}

### Windows 下的 Redis 安装及简单使用

平台：**Windows**

#### 安装 Redis

Redis 下载地址：[https://github.com/tporadowski/redis/releases](https://github.com/tporadowski/redis/releases)

选择 `Redis-x64-x.x.xxx.msi` 下载，安装。

使用 msi 安装可自行添加**系统环境变量**。

#### Redis 使用

未添加 Redis 的路径到系统环境变量，需要在 Redis 的安装路径启动 CMD/Powershell 等等。

添加了环境变量可直接使用下述指令：
+ 启动 redis：
  ```
  redis-server.exe redis.windows.conf
  # 或 redis-server redis.windows.conf
  # 或 redis-server
  ```
+ 关闭 redis：
  任选一：
  + 关掉命令行窗口
  + `Ctrl + C`
+ 访问 redis 服务端：
  ```
  redis-cli.exe -h 127.0.0.1 -p 6379
  或 redis-cli -h 127.0.0.1 -p 6379
  ```

+ redis 作为 windows 服务启动方式
  ```
  redis-server --service-install redis.windows.conf
  ```
  启动服务：`redis-server --service-start`
  停止服务：`redis-server --service-stop`

+ 移除 redis 的 Windows 服务
  ```
  redis-server.exe --service-uninstall
  # 或 redis-server --service-uninstall
  ```
