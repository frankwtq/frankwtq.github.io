---
layout: post
title: Github Pages 学习笔记
category : Intro
tags: [github pages, tag1, tag2]
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
> 每个帐号只能有一个仓库来存放个人主页，而且仓库的名字必须是==username/username.github.io==，这是特殊的命名约定。你可以通过==http://username.github.io==来访问你的个人主页。
通过向导很容易创建一个仓库，并测试成功。不过，同样的，没有博客的结构。需要注意的个人主页的网站内容是在==master==分支下的。

## 本地环境搭建
> 这一步不是必须的，但是强烈建议完成。因为在博客发布之前，通常都是需要在本地先检验一下的。github有一个对应的gem，可以”一键”配置环境，具体可以参考[Using Jekyll with Pages](https://help.github.com/articles/using-jekyll-as-a-static-site-generator-with-github-pages/)。

* 现成的模板[Jekyll themes](http://jekyllthemes.org/)
下载下来替换自己的仓库就可以了

## Jekyll模板系统
> GitHub Pages为了提供对HTML内容的支持，选择了Jekyll作为模板系统，Jekyll是一个强大的静态模板系统，作为个人博客使用，基本上可以满足要求，也能保持管理的方便，你可以查看Jekyll官方文档。

### Jekyll基本结构
> Jekyll的核心其实就是一个文本的转换引擎，用你最喜欢的标记语言写文档，可以是Markdown、Textile或者HTML等等，再通过layout将文档拼装起来，根据你设置的URL规则来展现，这些都是通过严格的配置文件来定义，最终的产出就是web页面。

> 基本的Jekyll结构如下：
_config.yml  
_includes  
_layouts  
|-- default.html  
|-- post.html  
_posts  
|-- 2007-10-29-why-every-programmer-should-play-nethack.textile  
|-- 2009-04-26-barcamp-boston-4-roundup.textile  
_site  
index.html  

* _config.yml
配置文件，用来定义你想要的效果，设置之后就不用关心了。

* _includes
可以用来存放一些小的可复用的模块，方便通过{ % include file.ext %}（去掉前两个{中或者{与%中的空格，下同）灵活的调用。这条命令会调用_includes/file.ext文件。

* _layouts
这是模板文件存放的位置。模板需要通过YAML front matter来定义，后面会讲到，{ { content }}标记用来将数据插入到这些模板中来。

* _posts
你的动态内容，一般来说就是你的博客正文存放的文件夹。他的命名有严格的规定，必须是2012-02-22-artical-title.MARKUP这样的形式，MARKUP是你所使用标记语言的文件后缀名，根据_config.yml中设定的链接规则，可以根据你的文件名灵活调整，文章的日期和标记语言后缀与文章的标题的独立的。

* _site
这个是Jekyll生成的最终的文档，不用去关心。最好把他放在你的.gitignore文件中忽略它。

* 其他文件夹
你可以创建任何的文件夹，在根目录下面也可以创建任何文件，假设你创建了project文件夹，下面有一个github-pages.md的文件，那么你就可以通过yoursite.com/project/github-pages访问的到，如果你是使用一级域名的话。文件后缀可以是.html或者markdown或者textile。这里还有很多的例子：https://github.com/mojombo/jekyll/wiki/Sites

*当前使用的jekyll主题:[Project Gaia](http://jekyllthemes.org/themes/project-gaia/)
