---
title: 用hexo和github快速搭建博客
date: 2018-03-03 10:07:02
tags:
---

以前用hexo和github搭建过博客，今天在动手实践一边也算是复习了。

本篇默认已在本机(windows)安装好git、node， 且有github账号

是的， 这篇只适用于windows用户， mac我没有，所以。。。
<!-- more -->

以下是步骤

# hexo
安装hexo并进行初始化
```
npm install -g hexo-cli
```

我们的hexo已经安装好了， 执行下列命令用于创建博客：
```
hexo init <folder> #<floder>是你将要创建的博客文件夹，如果你在电脑上已创建好了，那么进入文件夹执行行hexo init即可 我创建的是myBlog， 下同
cd <folder> #进入文件夹
npm install #安装博客所需信息
```
执行完以上步骤后会在myBlog看到大致如下结构：

```
.
├── _config.yml #网站的配置信息, 标题， 时间等
├── package.json #应用程序的信息
├── scaffolds #模板文件夹， 包含新建博客时默认填充的内容
├── source #资源文件夹
|   ├── _drafts #存放的是草稿文章
|   └── _posts  
|       └──hello-world.md 
└── themes #存放hexo博客的主题
```

执行下面的命令在http://localhost:4000/访问博客：
```
hexo server
```
默认访问端口是4000， 也可以通过下面的命令用新端口**临时**打开：
```
hexo server -p 2222
```
在浏览器输出http://localhost:2222/就可以了

下面让我们写一篇博客并发布吧！
```
hexo new 开博大吉
```
会在source/_posts 下看到<开博大吉.md>的文件

生成静态文件
```
hexo generate
```

博客在本地就搭建好了， 注意是本地！本地！本地！

# github
如何部署到github上呢？先大概了解下流程

首先， 我们需要创建一个库用来存放我们的博客， 并配置相关信息
然后， 使用`hexo deploy`命令即可部署。
最后， 在浏览器中输入网址就可以看到了

创建一个空库， 库的名字为： [用户名.github.io]
下面这张图片都应该能看懂！
![github创建hexo库](/用hexo和github快速搭建博客/github创建hexo库.png)

在git bash运行下列命令
```
cd path/myBlog #进入你博客的位置
start _config.yml
```

在_congig.yml中的最后一行修改为：
`type: git` , 注意冒号和git之间有空格
再添加一行：
`repo: git@github.com:helloyongwei/helloyongwei.github.io.git`

repo后面的一串是怎么来的？打开刚创建好的库，单击clone or download， 复制ssh key到repo即可。如图
![sshkey](/用hexo和github快速搭建博客/sshkey.png)

使用hexo命令部署：
`hexo deploy`
打开GitHub Pages 功能。
进入helloyongwei.github.io库， 最右边单击Setting， 向下找， 找到Github Page后按图设置就可以了。
![githubPage](/用hexo和github快速搭建博客/githubPage.png)
设置好后出现地址，
![helloyongwei.github.io](/用hexo和github快速搭建博客/helloyongwei.github.io.png)
在浏览器中输入`https://helloyongwei.github.io` 就可一看到自己的博客了

# 建立源代码库
在github上建立空仓库， 取名为blog-generate
运行如下命令：
```
echo "#blog-generator" >> README.md
git init
git add REMADE.md
git commit -m "first commit"
git remote add origin git@github.com:helloyongwei/blog-generate.git
git push -u origin master
```

blog-generate用来存放博客源代码， helloyongwei.github.io则用来存放博客

每次部署博客后（即`hexo deploy`)，也需要执行下列命令以保证不遗漏博客源代码
```
git add .
git commit -m "xxx"
git push -u origin master
```

参考：
    1.[hexo中文文档][1]


  [1]: https://hexo.io/zh-cn/docs/