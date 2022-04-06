---
title: 使用Github Actions实现Hexo博客在Github上的自动部署
date: 2020-11-30 16:55:45
categories: Blogs
tags: 
- Github
  
cover: /Images/14.jpg
---

使用自动部署之前，我都是用的`hexo deploy`把每次生成的`public`文件夹上传到github上去，使用自动部署之后，就省略掉了这一步骤，但是多了这三步
> git add -A
> git commit -m "imformaion"
> git push

看似并没有简化自己的操作，实际上好处很多  
+ 博客源码托管在Github的仓库，避免源码丢失的风险
+ Github会记录每一次`commit`，方便回溯
+ 高逼格
+ ......  
  
### 关于自动化部署
百度词条中的[<u>自动化部署</u>](https://baike.baidu.com/item/%E8%87%AA%E5%8A%A8%E5%8C%96%E9%83%A8%E7%BD%B2/18750522)


以及`CI\CD`——CI/CD 是一种通过在应用开发阶段引入自动化来频繁向客户交付应用的方法。CI/CD 的核心概念是持续集成、持续交付和持续部署。  

[`github Actions`](https://github.com/features/actions) 是 [`GitHub`](https://github.com) 的持续集成服务，于2018年10月推出。

还有一个类似的是[`TravisCI`](https://travis-ci.org/)。  

我之前使用的就是`TravisCI`，然后出了点小小的问题，其无法使用，然后一直配置不好，我就开始使用`GitHub Actions`，而且有大佬说`觉得它非常强大，有创意，比 Travis CI 玩法更多。`

不多介绍，就推荐几个大佬的文章
+ [GitHub Actions 入门教程](https://www.ruanyifeng.com/blog/2019/09/getting-started-with-github-actions.html)
+ [基于Github actions自动部署Hexo博客](https://blog.kaygb.com/210.html)
+ [使用 GitHub Actions 自动构建 Hexo 博客](https://xirikm.net/2020/313-1)
  
不多介绍了，直接说我怎么使用`github actions`的，主要chao了大佬的东西。


### 准备工作
需要一个`GitHub`帐号、一个 `GitHub Pages`仓库、一个`Hexo`博客备份仓库/分支。另外我们还需要获取一个`GitHub Personal Access Token`用来推送构建好的文件到我们的`GitHub Pages`仓库。具体的操作这里不再重复叙述，有需要了解的可以去看之前的文章。

点开博客备份仓库上方的`Settings`，点到左侧的`Secrets`项，添加两个秘密环境变量`GH_REF `、`GH_TOKEN`，值分别填写自己的`GitHub Pages` 仓库地址（不包含 https:// ）和刚刚申请到的`GitHub Personal Access Token`。

![secrets](using-gitActions/secret.png)
### 配置过程
准备工作做好后就可以开始编写`GitHub Actions`配置文件了，这里对 Hexo 博客编译部署的步骤进行拆分讲解。

配置文件的目录——在站点目录下新建`.github`文件夹，再在其中新建文件夹`workflows`，在创建`×××××××.yml`文件，命名随意。

![创建结果](using-gitActions/address.png)

### 触发条件和运行环境
我们设置在`master`分支上发生`push`操作时触发构建，使用最新的`Ubuntu`系统作为编译部署的环境，同时设置一个全局环境变量将时区修改为`Asia/Shanghai`(修改原因见 https://xirikm.net/2020/215-1.html)，具体的配置内容如下：
```yml
name: Blog CI/CD

on:
  push:
    branches: 
      - master

env:
  TZ: Asia/Shanghai

jobs:
  blog-cicd:
    name: Hexo blog build & deploy
    runs-on: ubuntu-latest

    steps:
```

### 建立工作环境
上面的大前提确定后就可以来开始建立我们的工作环境了（注： 后续所有步骤的配置都是接在上面`steps`块下的，不要弄混了层级关系）。

首先检出代码，设置一下`node`环境，我们这里使用`12.x`版本的`node.js`：
```yml
    steps:
    - name: Checkout codes
      uses: actions/checkout@v2

    - name: Setup node
      uses: actions/setup-node@v1
      with:
        node-version: '12.x'
```
然后设置一下缓存目录以避免每次都要重新下载，从而加快构建速度（官方不建议直接缓存`node_modules`目录，所以这里设置的是`npm`的下载缓存目录`~/.npm`，这样后面仍需要使用`npm install`来安装依赖）。这里使用的是`package-lock.json`文件的`hash`值来标识缓存是否可以命中：
```yml
    - name: Cache node modules
      uses: actions/cache@v1
      with:
        path: ~/.npm
        key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
```

最后就是安装依赖了，这个根据自己的需要操作就行，由于我使用了`gulp`任务来压缩`Hexo`生成的文件，所以我这里除了`hexo-cli`还全局安装了`gulp`：
```yml
    - name: Install dependencies
      run: |
        npm install hexo-cli gulp -g
        npm install
```
### 生成部署文件
这一步简单点`hexo g`就行了，我这里多加了一步执行 gulp 任务的操作（将其放在两个`step`中而不是一次性执行是为了方便在日志中看到每个操作消耗的时间）：
```yml
    - name: Generate files
      run: hexo generate

    - name: Execute gulp task
      run: gulp
```
### 部署博客
我们先将`GitHub Pages`仓库克隆过来，将其中的`.git`目录移到存放部署文件的`public`目录中（为了保留`GitHub Pages`仓库的提交历史），然后进入`public`目录设置一下提交用户名和邮箱，`add`所有文件并提交，最后利用保存在秘密环境变量中的`GitHub Personal Access Token`推送到`GitHub Pages`仓库中就可以了：
```yml
- name: Deploy blog
  run: |
    git clone "https://${{ secrets.GH_REF }}" deploy_git
    mv ./deploy_git/.git ./public/
    cd ./public
    git config user.name "yourname"
    git config user.email "youremail"
    git add .
    git commit -m "GitHub Actions Auto Builder at $(date +'%Y-%m-%d %H:%M:%S')"
    git push --force --quiet "https://${{ secrets.GH_TOKEN }}@${{ secrets.GH_REF }}" master:master
```

### 完整配置文件
```yml
name: Blog CI/CD

on:
  push:
    branches: 
      - master

env:
  TZ: Asia/Shanghai

jobs:
  blog-cicd:
    name: Hexo blog build & deploy
    runs-on: ubuntu-latest

    steps:
    - name: Checkout codes
      uses: actions/checkout@v2

    - name: Setup node
      uses: actions/setup-node@v1
      with:
        node-version: '12.x'

    - name: Cache node modules
      uses: actions/cache@v1
      with:
        path: ~/.npm
        key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}

    - name: Install dependencies
      run: |
        npm install hexo-cli gulp -g
        npm install

    - name: Generate files
      run: hexo generate

    - name: Execute gulp task
      run: gulp

    - name: Deploy blog
      run: |
        git clone "https://${{ secrets.GH_REF }}" deploy_git
        mv ./deploy_git/.git ./public/
        cd ./public
        git config user.name "yourname"
        git config user.email "youremail"
        git add .
        git commit -m "GitHub Actions Auto Builder at $(date +'%Y-%m-%d %H:%M:%S')"
        git push --force --quiet "https://${{ secrets.GH_TOKEN }}@${{ secrets.GH_REF }}" master:master
```

### 参考
[<u>使用 GitHub Actions 自动构建 Hexo 博客</u>](https://xirikm.net/2020/313-1)

**持续更新中**  
**暂时这么样**