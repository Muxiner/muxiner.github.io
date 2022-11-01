---
title: Ubuntu 安装 zsh + oh my zsh 美化终端
math: true
hide: false
date: 2022-11-01 13:58:52
updated: 2022-11-1 14:01:34
excerpt: Ubuntu 上安装“终极”终端 —— ZSH，并安装 oh my zsh + powerlevel10k 进行美化。
categories: 
- 记录
- Ubuntu
tags:
- Ubuntu
- install
index_img:
banner_img:
sticky:
---

关于 zsh 的一些简单介绍，查看权威介绍：

+ [Z shell | 中文维基百科](https://zh.wikipedia.org/wiki/Z_shell)
+ [Zsh | archlinux](https://wiki.archlinux.org/title/Zsh_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))

### install zsh

Ubuntu 安装 zsh 十分简单，只是执行命令即可：
```bash
sudo apt install zsh
```

> 又看到别人教程说还需要切换 zsh 为默认 shell，目前来看是没有必要的。
> 因为安装完 oh my zsh 后，其会自动设置 zsh 为默认终端。

{% note info %}

如果手动设置默认 shell：
```
chsh -s `which zsh`
```
再输入密码，并重启就行。
{% endnote %}

### install oh-my-zsh

> Oh My Zsh 是一个令人愉快的、开源的、社区驱动的框架，用于管理咱们的 Zsh 配置。
> 它捆绑了数千个有用的功能、助手、插件、主题，以及一些让咱们兴奋的东西......

+ 官网：[oh my zsh](https://ohmyz.sh/)
+ 文档：[oh my zsh | github wiki](https://github.com/ohmyzsh/ohmyzsh/wiki)

**安装**：
> install oh-my-zsh via curl
```bash
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

> install oh-my-zsh via wget
```bash
sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

> 上述命令会将 oh my zsh 安装在用户目录中，即 `/home/username/.oh-my-zsh`。是个隐藏文件。

### powerlevel10k

接下来主要是配置 oh my zsh 的主题，其自带的主题还是比较多的，比如：
{% note default %}
在我看来，也就 `agnoster` 最好看了。所以我将其放在第一位。

后面的只是我粗看一看，还过得去的。

罗卜白菜，各有所爱啦。
{% endnote %}
+ `agnoster`
  
  ![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/posts/20221101150411-agnoster.png)
+ `half-life`
  
  ![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/posts/20221101150655-half-life.png)
+ `jtriley`
  
  ![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/posts/20221101150823-jtriley.png)
+ `mortalscumbag`
  
  ![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/posts/20221101150956-mortalscumbag.png)
+ `steeef`
  
  ![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/posts/20221101151132-steeef.png)
+ `terminalparty`
  
  ![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/posts/20221101151412-terminalparty.png)
+ `tjkirch`
  
  ![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/posts/20221101151526-tjkirch.png)  
+ `ys`
  
  ![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/posts/20221101151728-ys.png)

更多主题情况请详见：
+ [oh my zsh themes | github wiki](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes)
+ [oh my zsh External themes | github wiki](https://github.com/ohmyzsh/ohmyzsh/wiki/External-themes)

除了上述主题外，还有一种非常 freedom 的一种主题 ——  `powerlevel10k`。

> 它强调速度、灵活性和开箱即用的体验。
> It emphasizes speed, flexibility and out-of-the-box experience.

该主题可以自行选择你所喜欢的样式来美化你的 prompt，也就是主题所改变的部分。

先看看咱的：

![](https://raw.githubusercontent.com/Muxiner/BlogImages/main/posts/20221101152215-powerlevel10k.png)

{% note info %}
就只是简单的选择了自己喜欢的样式。

该主题还可以添加更多有意思的部分，这个详见：[powerlevel10k | github](https://github.com/romkatv/powerlevel10k)
{% endnote %}

### install powerlevel10k

下载仓库：
```zsh
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

{% note success %}
中国大陆用户可以使用 gitee.com 上的官方镜像加速下载.
```zsh
git clone --depth=1 https://gitee.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/theme
```
{% endnote%}

然后修改 `.zshrc` 文件：
```zsh
nano ~/.zshrc
```
注释 `ZSH_THEME` 字段，并在下方添加 `ZSH_THEME="powerlevel10k/powerlevel10k"`。

最后执行命令进行设置，仔细阅读选项进行选择即可：
```zsh
p10k configure
```

### 安装 zsh 插件

> 看到别人推荐，自己试了确实不错。
> zsh 插件确实挺多，可以去 wiki 看看：[zsh Plugins | github wiki](https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins)

这里咱就只说俩，**自动补全** + **代码高亮**。

安装自动补全 —— `zsh-autosuggestions`
先下载到 oh my zsh 插件中
```zsh
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```
然后在配置文件 `.zshrc` 相关位置如下添加：
```txt
plugins=( 
    # other plugins...
    zsh-autosuggestions
)
```

安装代码高亮 —— `zsh-syntax-highlighting`
还是先下载到 oh my zsh 的插件中
```zsh
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```
然后还是在配置文件 `.zshrc` 对应位置：
```txt
plugins=( [plugins...] zsh-syntax-highlighting)
```

结束。

### 参考
+ [oh my zsh | github](https://github.com/ohmyzsh/ohmyzsh/)
+ [oh my zsh](https://ohmyz.sh/)
+ [oh my zsh Plugins| github wiki](https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins)
+ [powerlevel10k | github](https://github.com/romkatv/powerlevel10k)
+ [zsh-autosuggestions | github](https://github.com/zsh-users/zsh-autosuggestions)
+ [zsh-autosuggestions install](https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md#oh-my-zsh)
+ [zsh-syntax-highlighting | github](https://github.com/zsh-users/zsh-syntax-highlighting)
+ [zsh-syntax-highlighting install](https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md)
+ [Ubuntu 安装 Zsh ，配置最强终端](https://matnoble.me/tech/ubuntu/install-zsh/)
