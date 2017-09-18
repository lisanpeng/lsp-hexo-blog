---
title:  "欢迎来到我的github page"
categories: [github blog]
tags: [github pages]
---
对于一个忘性大的人来说，简单记录下折腾了一天，一切从零开始的主页。

<!--more-->

```环境：Ubuntu 16.04```

挑了一个*jekyll* 主题 [jekyll-uno](https://github.com/joshgerdes/jekyll-uno)。下载并部署到本地开始折腾。
安装Ruby：由于墙的原因，可能需要淘宝镜像

```
$ gem sources --add https://gems.ruby-china.org/ --remove https://rubygems.org/
$ gem sources -l
*** CURRENT SOURCES ***
```

安装bundler：
```
gem install jekyll bundler
```

运行：
```
bundle exec jekyll serve
```

```上传到github pages```


生成ssh key并添加到github
```
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
上传到github pages
```
$ git remote add origin git://github.com/yourname/yourproject.git
$ git add --all
$ git commit -m "first commit"
$ git push -u origin master
```
