---
layout: post
title: "Linux 系统调用实现-以read为例"
date: 2014-12-08 21:52:21 +0800
comments: true
categories: Linux kernel
---


&emsp;&emsp;Linux系统调用是连接用户态和内核态的纽带，弄清楚这个过程对于理解Linux操作系统具有十分重要的意义。下面以read系统调用为例分析这一过程。本文中Linux内核代码版本为3.16，glibc版本为2.20。

###1. sys_read函数的定义(fs/read_write.c):  
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





