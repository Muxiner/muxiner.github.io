---
title: hexo 主题 fluid：Error：Cannot find module 'css'
comment: giscus
math: true
hide: false
date: 2023-06-08 15:05:25
updated: 2023-06-08 15:05:25
excerpt: ERROR Script load failed：themes\fluid\scripts\events\lib\highlight.js Error：Cannot find module 'css'
categories: Blog
tags: [Blog, Fluid]
index_img:
banner_img:
sticky:
---

### 问题描述

许久没有更新博客，心血来潮，再来一次。先去 github 看了看，发现有依赖更新了，于是一顿操作后更新了。

结果跑持续集成时报错，报错情况如下：

```bash
INFO  Validating config
ERROR Script load failed: themes\fluid\scripts\events\lib\highlight.js
Error: Cannot find module 'css'
Require stack:
......
```
更新了的依赖为：
+ hexo-renderer-stylus
+ hexo-blog-encrypt
+ hexo-renderer-marked

查看错误位置：

```js
'use strict';

const fs = require('fs');
const css = require('css');
const objUtil = require('../../utils/object');
const resolveModule = require('../../utils/resolve');
```

确实有一部分为 `css`，不过怎么会找不到涅。不是很明白。

### 解决

经过一番操作，如更新依赖，更新主题啥啥啥的，还是无法解决。

最终在搜索引擎的帮助下，找到了，fluid 主题 github 仓库的 `issues`，发现有人遇到了同样的问题。

[ERROR Script load failed: themes\fluid\scripts\events\lib\highlight.js](https://github.com/fluid-dev/hexo-theme-fluid/issues/952)

在此中，主题作者[zkqiang](https://github.com/zkqiang)解释道：

```txt
This is because the new version of hexo-renderer-stylus no longer includes css module (stylus/stylus@043d404)
```

即，**新版本的 hexo-renderer-stylus 不再包含 css 模块。**，详见：[stylus/stylus@`043d404`](https://github.com/stylus/stylus/commit/043d4047031579bf8d1383116cf8f9a38d113d43)。

有人就提出了解决办法，安装 `css`：

```bash
npm install css --save
```

尝试后，成功解决问题，Nice。


### 碎碎念


作者在 `develop` 分支中进行了修改：

+ 修改文件：`scripts/events/lib/highlight.js`
+ 删除代码：`const css = require('css');`
+ 添加代码：
    ```js
    let css;
    try {
        css = require('css');
    } catch (error) {
        if (error.code === 'MODULE_NOT_FOUND') {
            css = require('@adobe/css-tools');
        } else {
            throw error;
        }
    }
    ```

没升级 hexo-renderer-stylus 就使用 `css = require('css');`，反之，`css = require('@adobe/css-tools');`。

不过咱这就还是自己安装 css 吧。