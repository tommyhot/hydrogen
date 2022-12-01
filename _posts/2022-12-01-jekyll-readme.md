---
layout: post
title: jekyll blog 入门
tags: jekyll blog ruby
---

这里是使用jekyll搭建个人博客的入门方法。注意，并不是从头开始而是，下载别人已经构建好的模板，稍微修改其中的配置以后，就可以自己使用了。
这里以 [hydrogen：https://github.com/link9596/hydrogen](https://github.com/link9596/hydrogen)主题为例。


* 首先从github上clone别人的代码

* 准备本地开发测试

```shell
sudo apt-get install ruby-full build-essential zlib1g-dev

gem install jekyll -v 3.3.1

gem build Hydrogen-blog.gemspec

gem install Material_Theme_For_Jekyll-1.0.gem

```

* 上传的github上并设置自己的主页。


