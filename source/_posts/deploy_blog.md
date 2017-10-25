---
title: My First Blog
date: 2017-09-9 16:57:57
tags: [hexo,github]
---

#### 利用Hexo + GitHub Pages搭建私人博客
我弄这个博客源于当时无意中在简书上看到一篇文章[少撸两局教你搭个博客玩
](http://www.jianshu.com/p/1ed6abf9d102)，这篇文章对我来说也是挺坑的，上面讲的都是windows环境下搭建的，作为一个忠实linux用户我果断弃坑，不过我也是因此打算搭个博客玩玩，虽然说我并没有什么明确的目的用它来写些什么，但管它呢，先搭来玩玩(^_^)。    

> 按照hexo 的[官方文档](https://hexo.io)我安装了node.js npm hexo当然事情总是很自然的出现了一些问题,hexo 安装失败！ :-，不过所幸是后面成功了，应该是缺了了些东西，后面加上*sudo apt-get install nodejs-legacy*就成了，十有八九就是它的锅了吧。    

然后经过下面一系列的初始化什么的
```bash
hexo init
hexo g    #生成静态网页
hexo s    #运行本地服务器
```

- 然后设置_config.yml文件的deploy
<!--more-->
```bash
deploy:
  type: git
  repository: git@github.com:Richardcsb/Richardcsb.git
  branch: master
```
- 并且强调设置好deployment后一定要
```bash
npm install hexo-deployer-git --save
```
然而问题又来了到这里后我一直不能成功的把本地push到GitHub上，然后看了另外一篇blog找到了下面办法  

- 部署本地博客到github	

```bash
hexo d
```
我也没想到就这么简单就行了，看来是习惯性用git了，总想着git push .	

看各类blog都说原主题太丑，所以我感觉我是被强烈要求使用一个新的主题，这用的是yilia，这个也是比较多人推崇的。
```bash
git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia
theme: yilia
```

- 为了弄上这个yilia没被累个半死已然不错，出现的毛病是本地正常而在github上却无法显示出css样式。
> 后面更改了_config.yml的url地址为[github上的地址](https://richardcsb.github.io/),当然应该不是这个问题，主要问题出在GitHub上仓库的名字，把我的仓库名字Richardcsb改成Richardcsb.github.io才终于成了，这个终于必须得加上，我得突出我找到这个问题不容易。我只能说网上些乱七八糟教程害人不浅，找十个有九个行不通。	
	

- 顺带copy了一些常用命令在这里	

```bash
hexo c 清除生成的静态网页
hexo g 生成静态网页
hexo d 将本地的静态页面部署到github上
hexo n “acticlename” 新建文章
hexo n page “pagename” 新建页面
hexo s -g 先生成静态页面然后开启本地预览
hexo d -g 生成静态页面然后部署到github
```
