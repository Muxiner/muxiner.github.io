---
title: 好东西就记录下来.jpg
date: 2022-07-12 16:38:19
updated: 2023-06-12 20:29:38
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

{% note primary %}
**2023-03-29** 更新
{% endnote %}

### Linux Shell 获取系统时间

Linux `date` 命令可以显示或者设定系统的日期和时间。


**语法**
```zsh
date [OPTION]... [+FORMAT]
date [-u] [-d datestr] [-s datestr] [--utc] [--universal] [--date=datestr] [--set=datestr] [--help] [--version] [+FORMAT] [MMDDhhmm[[CC]YY][.ss]]
```
**可选参数：**
+ `-d, --date=STRING`：
  通过字符串显示时间格式，字符串不能是'now'。
+ `-f, --file=DATEFILE`：
  类似于--date; 一次从DATEFILE处理一行。
+ `-I[FMT], --iso-8601[=FMT]`：
  按照 ISO 8601 格式输出时间，FMT 可以为'date'(默认)，'hours'，'minutes'，'seconds'，'ns'。 可用于设置日期和时间的精度，例如：2006-08-14T02:34:56-0600。
+ `-R, --rfc-2822`： 
  按照 RFC 5322 格式输出时间和日期，例如: Mon, 14 Aug 2006 02:34:56 -0600。
+ `--rfc-3339=FMT`：
  按照 RFC 3339 格式输出，FMT 可以为'date', 'seconds','ns'中的一个，可用于设置日期和时间的精度， 例如：2006-08-14 02:34:56-06:00。
+ `-r, --reference=FILE`：
  显示文件的上次修改时间。
+ `-s, --set=STRING`：
  根据字符串设置系统时间。
+ `-u, --utc, --universal`：
  显示或设置协调世界时(UTC)。
+ `--help`：
  显示帮助信息。
+ `--version`：
  输出版本信息。

**FORMAT 参数:**
在显示方面，使用者可以设定欲显示的格式 ，格式设定为一个加号后接数个标记，其中可用的标记列表如下：
```txt
%%     输出字符 %
%a     星期几的缩写 (Sun..Sat)
%A     星期的完整名称(Sunday..Saturday)。 
%b     缩写的月份名称（例如，Jan）
%B     完整的月份名称（例如，January）
%c     本地日期和时间（例如，Thu Mar  3 23:05:25 2005）
%C     世纪，和%Y类似，但是省略后两位（例如，20）
%d     日 (01..31)
%D     日期，等价于%m/%d/%y
%e     一月中的一天，格式使用空格填充，等价于%_d
%F     完整的日期；等价于 %Y-%m-%d
%g     ISO 标准计数周的年份的最后两位数字
%G     ISO 标准计数周的年份，通常只对%V有用
%h     等价于 %b
%H     小时 (00..23)
%I     小时 (01..12)
%j     一年中的第几天 (001..366)
%k     小时，使用空格填充 ( 0..23); 等价于 %_H
%l     小时, 使用空格填充 ( 1..12); 等价于 %_I
%m     月份 (01..12)
%M     分钟 (00..59)
%n     新的一行，换行符
%N     纳秒 (000000000..999999999)
%p     用于表示当地的AM或PM，如果未知则为空白
%P     类似 %p, 但是是小写的
%r     本地的 12 小时制时间(例如 11:11:04 PM)
%R     24 小时制 的小时与分钟; 等价于 %H:%M
%s     自 1970-01-01 00:00:00 UTC 到现在的秒数
%S     秒 (00..60)
%t     插入水平制表符 tab
%T     时间; 等价于 %H:%M:%S
%u     一周中的一天 (1..7); 1 表示星期一
%U     一年中的第几周，周日作为一周的起始 (00..53)
%V     ISO 标准计数周，该方法将周一作为一周的起始 (01..53)
%w     一周中的一天（0..6），0代表星期天
%W     一年中的第几周，周一作为一周的起始（00..53）
%x     本地的日期格式（例如，12/31/99）
%X     本地的日期格式（例如，23:13:48）
%y     年份后两位数字 (00..99)
%Y     年
%z     +hhmm 格式的数值化时区格式（例如，-0400）
%:z    +hh:mm 格式的数值化时区格式（例如，-04:00）
%::z   +hh:mm:ss格式的数值化时区格式（例如，-04:00:00）
%:::z  数值化时区格式，相比上一个格式增加':'以显示必要的精度（例如，-04，+05:30）
%Z     时区缩写 （如 EDT）
```


**一些简单示例：**
```zsh
$ date
2023年03月29日 20:07:46

# 当前年月日
$ date +%F
2023-03-29

# 当前时分
$ date +%R
21:06

# 当前时分秒
$ date +%T
21:06:34

# 当前星期
$ date +%A
星期三

# 组合输出日期，分隔符 /
$ date +%Y/%m/%d
2023/03/29

# 组合输出日期，分隔符 -
$ date +%Y-%m-%d
2023-03-29

# 输出时分秒，分隔符 :
$ date +%H:%M:%S
21:10:11

# 输出年月日时分秒
$ date +%F%n%T
2023-03-29
21:10:22
```
还可以使用 `echo $()` 括号中间加 date 命令。
```zsh
$ echo $(date +%F%n%T)
2023-03-29 21:12:59
```
还可以将需要常用的命令设置别名，以方便简便使用：
```zsh
alias datetime='echo $(date +%F%n%T)'
```
并将其添加到 `~/.zshrc` 或者 `~/.bashrc` 中。
再 `source ~/.zshrc` 或者 `source ~/.bashrc`。
```zsh
$ datetime
2023-03-29 21:40:39
```

### MV 使用

{ % note info % }
2023-06-12 20:29:38 更新。
{ % endnote % }

```bash
# 使用 find 命令查找源目录下的所有文件，并使用 mv 命令移动到目标目录
find "$source_dir" -type f -exec mv {} "$target_dir" \;
```