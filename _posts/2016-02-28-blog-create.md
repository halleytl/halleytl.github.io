---
layout: post
title: blog 搭建过程
description: ""
category: 
tagline: 心路历程
theme:
  name: twitter
tags: [blog 搭建, 原创]
---
{% include JB/setup %}

[That dog](http://doglooksgood.github.io/)用 org 搭建了一个博客表示很羡慕, 我呢用markdown搭建个。

### 依赖安装 ruby gem jekyll 

rubygems.org 存放在 Amazon S3 上面的资源文件间歇性连接失败,需要修改 [RubyGems 镜像](https://ruby.taobao.org/)

### 开始搭建博客

在你的 [github](https://github.com) 账户下创建一个新的仓库叫 USERNAME.github.io

安装 [Jekyll-Bootstrap](http://jekyllbootstrap.com/usage/jekyll-quick-start.html)

选择主题和添加语法高亮功能

```shell
rake theme:install git="https://github.com/halleytl/theme-twitter.git"
```

添加页面

```shell
rake post title="hello world"
```
执行命令后会在 _post 目录下生成 xxxx-xx-xx-hello-world.md 文件
打开文件,在文件头部添加主题

    theme:
        name: twitter
    tagline: 标语
    tags: [原创]

需要注意以下问题 rake post title="xxx" xxx 不能为中文。

key:<空格>value 我就是因为没有空格导致主题加载失败















