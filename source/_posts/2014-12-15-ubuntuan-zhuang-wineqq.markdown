---
layout: post
title: "Ubuntu安装WineQQ"
date: 2014-12-15 21:13:03 +0800
comments: true
categories: linux
---

&emsp;&emsp;如果以Ubuntu(或者其变种Mint)作为日常工作环境的话，那么类似于字处理，挂QQ等将成为不可避免的需求。关于在Ubuntu上挂QQ，之前的解决方案是使用VirtualBox安装windows,然后在windows里安装QQ；最近也使用Qemu安装过Win7。很明显为了挂个QQ而安装个虚拟机太笨重了，非常耗费系统资源。最近发现了一种新的办法，就是WineQQ解决方案，亲测好用，记录之。  
###1. 安装依赖库  
    sudo apt-get install libgtk2.0-0  
    sudo apt-get install ia32-libs  
    sudo apt-get install lib32ncurses5  
    sudo apt-get install liblcms2-2  

###2. 下载并解压缩wineqq  
&emsp;&emsp;下载地址：[http://www.ubuntukylin.com/applications/showimg.php?lang=cn&id=23](http://www.ubuntukylin.com/applications/showimg.php?lang=cn&id=23)  
&emsp;&emsp;然后用unzip命令解压缩。  

###3. 安装wineqq  
    sudo dpkg -i wine-qqintl_0.1.3-2_i386.deb  
    sudo dpkg -i ttf-wqy-microhei_0.2.0-beta-2_all.deb  
    sudo dpkg -i fonts-wqy-microhei_0.2.0-beta-2_all.deb  
&emsp;&emsp;然后在系统菜单的互联网子菜单里就可以发现刚安装的WineQQ，开启用之！  

###参考文献  
[http://bubuko.com/infodetail-343048.html](http://bubuko.com/infodetail-343048.html)  

