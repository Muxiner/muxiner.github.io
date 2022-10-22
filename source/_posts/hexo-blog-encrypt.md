---
title: hexo 文章加密
math: true
hide: false
date: 2022-10-22 14:32:45
updated: 2022-10-22 14:32:45
excerpt: 使用 hexo-blog-encrypt 使用 hexo 的文章加密。
categories: 教程
tags: Hexo
index_img:
banner_img:
sticky:
---

### 丑话在先
本来是没有什么文章内容需要加密的，不过现在突然发现我可以使用博客文章记录一下咱喜欢的 [Pixiv](pixiv.net) 画师，如果是正常的插画，就不需要加密，不过嘛，我喜欢的多少需要一点科学观看，所以还是使用加密，就自己看看吧。

本是记得 hexo 的文章信息头可以加入 `password` 的字段，不过搜索后发现还需要安装一个 hexo 扩展：`hexo-blog-encrypt`。

于是记录一下。

### 特性
+ 一旦你输入了正确的密码，它就会被存储在本地浏览器的 `localStorage` 中。按个按钮，密码将会被清空。若博客中有脚本，它将被正确地执行。
+ 支持按标签加密。
+ 所有的核心功能都是由原生的 `API` 所提供的。在 `Node.js` 中，我们使用 `Crypto`。在浏览器中，我们使用 `Web Crypto API`。
+ `PBKDF2`，`SHA256` 被用作复制密钥，`AES256-CBC` 被用作加解密，我们还使用 `HMAC` 来验证密文的来源，并确保其纠正。
+ 广泛地使用 `Promise` 来进行异步操作，从而确保线程不被杜塞。
+ 过时的浏览器将无法正常显示，因此，请升级您的浏览器。

### 安装

```powershell
npm install --save hexo-blog-encrypt
```

### 快速使用

将 `password` 添加到文章信息头：
```
title: Hello World
date: 2020-03-13 21:12:21
password: muyiio
---
```
### 按照标签加密

#### 1. 修改文章信息头
   
    ```
    title: Hello World
    tags:
    - 加密文章tag
    date: 2020-03-13 21:12:21
    password: muyiio
    abstract: 这里有东西被加密了，需要输入密码查看哦。
    message: 您好，这里需要密码。
    wrong_pass_message: 抱歉，这个密码看着不太对，请再试试。
    wrong_hash_message: 抱歉，这个文章不能被纠正，不过您还是能看看解密后的内容。
    ---
    ```
#### 2. 修改博客本目录 `_config.yml`。添加如下字段

    ```
    # 安全
    encrypt: # hexo-blog-encrypt
        abstract: 这里有东西被加密了，需要输入密码查看哦。
        message: 您好, 这里需要密码.
        tags:
        - {name: tagName, password: 密码A}
        - {name: tagName, password: 密码B}
        template: <div id="hexo-blog-encrypt" data-wpm="{{hbeWrongPassMessage}}" data-whm="{{hbeWrongHashMessage}}"><div class="hbe-input-container"><input type="password" id="hbePass" placeholder="{{hbeMessage}}" /><label>{{hbeMessage}}</label><div class="bottom-line"></div></div><script id="hbeData" type="hbeData" data-hmacdigest="{{hbeHmacDigest}}">{{hbeEncryptedData}}</script></div>
        wrong_pass_message: 抱歉, 这个密码看着不太对, 请再试试.
        wrong_hash_message: 抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.
    ```

### DLC

记录下咱没有用到的内容。

**对 TOC 文章进行加密**

如果有一篇文章使用了 `TOC`，需要修改模板的部分代码。这里以 `matery` 主题作为示例：

在 `hexo/themes/matery/layout/_partial/article.ejs` 找到 `article.ejs`。
然后找到 `<％post.content％>` 这段代码，通常在 30 行左右。
使用如下的代码来替代它：
```
<% if(post.toc == true){ %>
  <div id="toc-div" class="toc-article" <% if (post.encrypt == true) { %>style="display:none" <% } %>>
    <strong class="toc-title">Index</strong>
      <% if (post.encrypt == true) { %>
        <%- toc(post.origin, {list_number: true}) %>
      <% } else { %>
        <%- toc(post.content, {list_number: true}) %>
      <% } %>
  </div>
<% } %>
<%- post.content %>
```

### 参考
+ [hexo-blog-encrypt](https://github.com/D0n9X1n/hexo-blog-encrypt)
+ [hexo-blog-encrypt | 中文](https://github.com/D0n9X1n/hexo-blog-encrypt/blob/master/ReadMe.zh.md)
+ [对 Hexo 博客文章进行加密](https://zhuanlan.zhihu.com/p/113235573)