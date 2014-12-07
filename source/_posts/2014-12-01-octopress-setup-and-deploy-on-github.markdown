---
layout: post
title: "Octopress setup and deploy on Github"
date: 2014-12-01 22:49:57 +0800
comments: true
categories: Octopress
---

经过充分调研，选定Octopress作为技术博客系统框架。
下面是在Linux mint 13操作系统上安装Octopress和在Github上部署的过程。

##安装
###1.安装git, ruby和nodejs
    apt-get install git
    apt-get install libruby1.9.1
    apt-get install ruby1.9.1
    apt-get install ruby1.9.1-dev
    apt-get install nodejs
###2.下载Octopress
    git clone git://github.com/imathis/octopress.git octopress
    cd octopress
###3.安装依赖
    gem install bundler
    rbenv rehash
    bundle install
###4.安装默认Octopress主题
    rake install

##在Github上部署Octopress
###1.在Github个人帐号上创建仓库
我的Github个人帐号为weizhenwei，创建仓库weizhenwei.github.io.git
###2.部署Octopress到Github
    1.rake setup_github_pages    #关联仓库weizhenwei.github.io.git的完整路径；
    2.rake generate              #内容生成；
    3.rake preview               #内容预览，在本地浏览器localhost:4000预览；
    4.rake deploy                #内容部署，上传到github仓库上的master分支；
###3.Octopress源代码保存
    git add .
    git commit -m "my comment"
    git push origin source       # 源代码保存到source分支；
###4.Octopress配置
主要是修改_config.yml文件。

##博客内容撰写：
    rake new_post["title“]       # 创建博客文件，该文件在sorce/_post目录下；
    然后编辑这个博客文件；
    rake generate;
    rake preview;
    rake deploy;
    git add .
    git commit -m "my comment"
    git push origin source

##添加新页面：
    1. rake new_page["aboutme"], 该命令自动生成source/aboutme目录以及其下的index.markdown文件;  
    2. 编辑source/aboutme/index.markdown文件, 添加内容;  
    3. 修改souce/_includes/custom/navigation.html文件，将1.中新建文件路径添加到该文件中。
    4. rake generate; rake preview; rake deploy;  
    5. git add .; git commit -m "comment"; git push origin source;  

##注意事项：
    1.在新的地方git clone代码之后，需要checkout到source分支，
      然后再运行rake setup_github_pages命令连接上仓库url。
    2. master分支是内容分支，全部是由rake deploy命令提交；
       source分支是源代码分支，用git命令进行提交；
       两个分支不可搞混。
       

-----
##参考文献：
[http://octopress.org/docs/setup/](http://octopress.org/docs/setup/)  
[http://octopress.org/docs/deploying/github/](http://octopress.org/docs/deploying/github/)  
[http://octopress.org/docs/blogging/](http://octopress.org/docs/blogging/)  
[http://stackoverflow.com/questions/21356212/failed-to-deploy-to-github-pages-using-octopress](http://stackoverflow.com/questions/21356212/failed-to-deploy-to-github-pages-using-octopress)  

