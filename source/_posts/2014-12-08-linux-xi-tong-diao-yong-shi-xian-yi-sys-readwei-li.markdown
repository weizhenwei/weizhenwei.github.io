---
layout: post
title: "Linux 系统调用实现-以read为例"
date: 2014-12-08 21:52:21 +0800
comments: true
categories: Linux kernel
---


&emsp;&emsp;Linux系统调用是连接用户态和内核态的纽带，弄清楚这个过程对于理解Linux操作系统具有十分重要的意义。下面以read系统调用为例分析这一过程。本文中Linux内核代码版本为3.16，glibc版本为2.20。

###1. sys_read系统调用的定义(在内核文件fs/read_write.c中):  
```c
    SYSCALL_DEFINE3(read, unsigned int, fd, char __user *, buf, size_t, count)  
    {  
        struct fd f = fdget_pos(fd);  
        ssize_t ret = -EBADF;  
  
        if (f.file) {  
            loff_t pos = file_pos_read(f.file);  
            ret = vfs_read(f.file, buf, count, &pos);  
            if (ret >= 0)  
                file_pos_write(f.file, pos);  
            fdput_pos(f);  
        }  
        return ret;  
    }  
```
&emsp;&emsp;sys_read的实现代码比较简单：首先根据文件描述符fd通过fdget_pos(fd)从当前进程结构中得到fd对应的struct fd结构（这个fd结构是struct file结构的进一步封装）；然后调用file_pos_read(f.file)得到当前文件读位置；最后调用vsf_read()进行文件读取操作；如果读取成功，则调用file_pos_write函数更新文件的读当前位置；最后调用fdput_pos函数更新文件的引用计数；最终sys_read返回读取的字节数。  
&emsp;&emsp;sys_read系统调用实现的核心是vfs_read函数，这涉及到Linux的VFS虚拟文件系统机制，这是另外一个主题，在此就不深入展开了。





