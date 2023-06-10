---
title: Shell 学习
comment: giscus
math: true
hide: false
date: 2023-06-10 15:43:35
updated: 2023-06-10 15:43:35
excerpt: 指的是 Shell 脚本编程的学习记录。
categories: Learning
tags: Shell
index_img:
banner_img:
sticky: 96
---

### 前言

最近一直在做某些重复性的操作，太多机械性的操作，非常的浪费时间，作为一个懒汉，必须得想办法偷懒。

之前整理博客文章的时候，刚好看到大佬给予的命令：

```bash
grep -r "date: 2020-" *.md -l | xargs mv -v -t 2020/
```

之类的。可以快速的、批量的操作文件，比手动点点点的快多了。心想着，我那些机械性重复性操作是不是也可以想办法偷懒，使用某种命令一次性完成所有的操作。于是就询问的神奇海螺看看有没有什么建议，进而发现**可以使用 shell 脚本 —— shell script** 进行批量操作。

话不多说直接开干。


## 实践

一番实践下来，效果显著，偷懒ing。

下面的实践都是所说的机械性操作。

### 读取文件内容批量创建 markdown 文件和文件夹

```sh
#!/bin/bash

# 读取目录
read -r directory < input.txt

directory=$(echo "$directory" | tr -d '\r')


# 读取文件名并处理回车符
tail -n +2 input.txt | tr -d '\r' | while IFS= read -r file
do
    # 创建文件夹和文件
    file="${line// /_}"
    mkdir -p "$directory/images/$file"
    touch "$directory/$file.md"

done
```

### 读取两个文件以创建 markdown 文件和文件夹，并输出指定格式内容到文件中

```sh
#!/bin/bash
if [ $# -eq 0 ]; then
  echo "未提供路径参数"
  exit 1
fi

# 使用命令行参数作为路径
target_path="path/$1"

mkdir -p "$target_path"

>links.yml

# 指定相对路径的基准路径
base_path="path"

touch "$target_path/index.md"
printf "%c $1/index.md\n" "-" | tee -a links.yml

# 逐行读取两个文件的内容，直到文件结束
paste chinese.txt english.txt | while IFS=$'\t' read -r name path; do
  # 在这里对行内容进行处理
  # 将 \r 替换为空格
  name="${name//$'\r'/}"
  path="${path//$'\r'/}"
  path="${path// /_}"
  # 创建文件和文件夹
  mkdir -p "$target_path/images/$path"
  touch "$target_path/$path.md"
  # printf "$target_path/$path.md & $target_path/images/$path 都已创建~\n"
  # yml 链接
  printf "%c $name: $1/$path.md\n" "-" | tee -a links.yml
done

>chinese.txt
>english.txt
```

### 查找目标路径中的所有 Markdown 文件，并输出相对路径到 output.txt

```sh
#!/bin/bash

# 检查是否提供了命令行参数
if [ $# -eq 0 ]; then
  echo "未提供路径参数"
  exit 1
fi

# 使用命令行参数作为路径
target_path="docs/$1"

# 指定相对路径的基准路径
base_path="docs"

> output.txt

# 查找目标路径中的所有 Markdown 文件，并输出相对路径到 output.txt
find "$target_path" -type f -name "*.md" | while IFS= read -r file
do
    relative_path=$(realpath --relative-to="$base_path" "$file")
    echo "$relative_path" >> output.txt
done
```

### 遍历目标路径中的所有文件夹，并输出相对路径

```sh
#!/bin/bash

# 指定要列出文件夹的目录
target_path="docs"

# 指定相对路径的基准路径
base_path="docs"

# 清空输出文件
> all_path.txt

# 遍历目标路径中的所有文件夹，并输出相对路径
find "$target_path" -type d | while IFS= read -r dir
do
    relative_path=$(realpath --relative-to="$base_path" "$dir")
    echo "$relative_path" >> all_path.txt
done
```

### 格式化输出 html 的图片链接

```sh
#!/bin/bash

#!/bin/bash

if [ $# -ne 3 ]; then
    echo "需要提供 3 个输入参数"
    exit 1
fi

# 在这里执行操作，使用 $1 和 $2 引用输入参数
images_name=$2
num=$3
fmt=$1

if [ $fmt -eq 1 ]; then
    fmt=".jpg"
elif [ $fmt -eq 2 ]; then
    fmt=".png"
else
    echo "输入1表示图片格式为jpg，输入2表示图片格式为png，其他输入无效"
    exit 1
fi

> images.txt
printf "<div class=\"gallery\"><div class=\"column\">\n" | tee -a images.txt
count=0

for ((i = 1; i <= num; i += 2)); do
    printf "<img src=\"./images/%s_%04d$fmt\">" "$images_name" "$i" | tee -a images.txt
    ((count++))
    if [ $count -eq 2 ]; then
        count=0
        printf "\n" | tee -a images.txt
    fi
done
if [ $count -eq 1 ]; then
    printf "\n" | tee -a images.txt
fi
printf "</div><div class=\"column\">\n" | tee -a images.txt
count=0

for ((i = 2; i <= num; i += 2)); do
    printf "<img src=\"./images/%s_%04d$fmt\">" "$images_name" "$i" | tee -a images.txt
    ((count++))
    if [ $count -eq 2 ]; then
        count=0
        printf "\n" | tee -a images.txt
    fi
done
if [ $count -eq 1 ]; then
    printf "\n" | tee -a images.txt
fi
printf "</div></div>\n" | tee -a images.txt

```
