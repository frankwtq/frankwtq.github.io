---
layout: post
title: Github Pages 学习笔记
category : Intro
tags: [github_pages]
stickie: true
---

# 记录学习github pages的笔记
学习过程来源于 [读立书生](http://www.cnfeat.com/) 微博的博文 [如何搭建一个独立博客——简明 Github Pages与 jekyll 教程](http://www.cnfeat.com/blog/2014/05/10/how-to-build-a-blog/)  

简单博客的管理在这个网址：[https://github.com/isnowfy/simple](https://github.com/isnowfy/simple)
## 参考博文
* [一步步在GitHub上创建博客主页-最新版](http://www.pchou.info/ssgithubPage/2014-07-04-build-github-blog-page-08.html)
* [使用Github Pages建独立博客](http://beiyuu.com/github-pages)
* [如何搭建一个独立博客——简明 Github Pages与 jekyll 教程](http://www.cnfeat.com/blog/2014/05/10/how-to-build-a-blog/)

## github pages介绍
> github-page是一个免费的静态网站托管平台，由github提供，它具有以下特点：
>* 免空间费，免流量费
>* 具有项目主页和个人主页两种选择
>* 支持页面生成，可以使用jekyll来布局页面，使用markdown来书写正文
>* 可以自定义域名

其中提到的jekyll：
> [jekyll](http://baike.baidu.com/link?url=OlwBCB7vKyxh7m25bZtt4GN2nngQY7RGY1NDLR0C9CGUcS3Vyoj6aSyUF9Cra2M0jiNxDDKRtDzpf60wzW89-q)是一个简单的免费的Blog生成工具，类似WordPress。但是和WordPress又有很大的不同，原因是jekyll只是一个生成静态网页的工具，不需要数据库支持。但是可以配合第三方服务,例如Disqus。最关键的是jekyll可以免费部署在Github上，而且可以绑定自己的域名。

## 个人主页
> 每个帐号只能有一个仓库来存放个人主页，而且仓库的名字必须是**username/username.github.io**，这是特殊的命名约定。你可以通过**http://username.github.io**来访问你的个人主页。
通过向导很容易创建一个仓库，并测试成功。不过，同样的，没有博客的结构。需要注意的个人主页的网站内容是在**master**分支下的。

## 本地环境搭建
> 这一步不是必须的，但是强烈建议完成。因为在博客发布之前，通常都是需要在本地先检验一下的。github有一个对应的gem，可以”一键”配置环境，具体可以参考[Using Jekyll with Pages](https://help.github.com/articles/using-jekyll-as-a-static-site-generator-with-github-pages/)。
* 确保系统下有gem,因为Jekyll是基于Ruby的
* `gem install Jekyll`
* 在[Jekyll Themes](http://jekyllthemes.org/)上下载模板
* 在模板文件中运行`Jekyll server`运行Jekyll的本地开发服务器，此时就可以到http://localhost:4000上查看博客了

## Jekyll模板系统
> GitHub Pages为了提供对HTML内容的支持，选择了Jekyll作为模板系统，Jekyll是一个强大的静态模板系统，作为个人博客使用，基本上可以满足要求，也能保持管理的方便，你可以查看Jekyll官方文档。

### Jekyll基本结构
> Jekyll的核心其实就是一个文本的转换引擎，用你最喜欢的标记语言写文档，可以是Markdown、Textile或者HTML等等，再通过layout将文档拼装起来，根据你设置的URL规则来展现，这些都是通过严格的配置文件来定义，最终的产出就是web页面。

基本的Jekyll结构如下：  
├── _config.yml  
├── _drafts  
|&emsp;&emsp;├── begin-with-the-crazy-ideas.textile  
|&emsp;&emsp;└── on-simplicity-in-technology.markdown  
├── _includes  
|&emsp;&emsp;├── footer.html  
|&emsp;&emsp;└── header.html  
├── _layouts  
|&emsp;&emsp;├── default.html  
|&emsp;&emsp;└── post.html  
├── _posts  
|&emsp;&emsp;├── 2007-10-29-why-every-programmer-should-play-nethack.textile  
|&emsp;&emsp;└── 2009-04-26-barcamp-boston-4-roundup.textile  
├── _data  
|&emsp;&emsp;└── members.yml  
├── _site  
└── index.html  

* _config.yml
保存配置数据。很多配置选项都会直接从命令行中进行设置，但是如果你把那些配置写在这儿，你就不用非要去记住那些命令了。 
* _drafts
drafts 是未发布的文章。这些文件的格式中都没有 title.MARKUP 数据。学习如何使用 drafts. 
* _includes
你可以加载这些包含部分到你的布局或者文章中以方便重用。可以用这个标签`{ % include file.ext % }`(实际使用时“{}”前后都没有空格)来把文件 _includes/file.ext 包含进来。

* _layouts
layouts 是包裹在文章外部的模板。布局可以在 YAML 头信息中根据不同文章进行选择。 这将在下一个部分进行介绍。标签`{ { content } }`(实际使用时“{}”前后都没有空格)可以将content插入页面中。 

* _posts
这里放的就是你的文章了。文件格式很重要，必须要符合: YEAR-MONTH-DAY-title.MARKUP。 The permalinks 可以在文章中自己定制，但是数据和标记语言都是根据文件名来确定的。 

* _site
一旦 Jekyll 完成转换，就会将生成的页面放在这里（默认）。最好将这个目录放进你的 .gitignore 文件中。 这个是Jekyll生成的最终的文档，不用去关心。最好把他放在你的.gitignore文件中忽略它。

* 其他文件夹
你可以创建任何的文件夹，在根目录下面也可以创建任何文件，假设你创建了project文件夹，下面有一个github-pages.md的文件，那么你就可以通过yoursite.com/project/github-pages访问的到，如果你是使用一级域名的话。文件后缀可以是.html或者markdown或者textile。这里还有很多的例子：https://github.com/mojombo/jekyll/wiki/Sites

## 部署
在搭建好本地Jekyll环境，并下载好Jekyll Theme后，就可以部署到github pages上了。
* 在github上创建名为**username.github.io**的仓库
* 在Setting中的github pages栏中选择一个Theme
* `git clone https://github.com/username/username.github.io`克隆到本地
* 用之前下载的Jekyll Theme中的文件替换克隆到本地的git仓库
* 在仓库中`jekyll server`检测以下是否能运行本地开发服务器
* 将自己的文章（例如markdown格式的）放到**_posts**文件家中，按格式修改好文件名
* 上传自己的git仓库，等待1到2分钟，就可以到**username.github.io**上查看自己的博客了

*当前使用的jekyll主题:[Project Gaia](http://jekyllthemes.org/themes/project-gaia/)
