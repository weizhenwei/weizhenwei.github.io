---
layout: post
title: "x86-64指令和ABI"
date: 2014-12-25 21:51:09 +0800
comments: true
categories: x86-64 abi
---

&emsp;&emsp;本文是针对x86-64指令和ABI的综述，其内容翻译自参考文献[1]。  

###1 引言
x86-64指令一般有两个操作数：源操作数和目的操作数，目的操作数也作为结果存放地。  
linux下的x86-64指令格式采用AT&T格式，也即源操作数在左边，目的操作数在右边。  
绝大多数x86-64指令采用后缀字母标示操作数的大小，例如q表示64为，b表示8位，w表示16位，l表示32位。  

###2 寄存器
x86-64有16个64位通用寄存器，在AT&T格式中使用%做前缀，其定义和在ABI中的角色如下表所示：  
  
| Register      | Callee Save   |                 Description                 |  
|:-------------:|:-------------:|:--------------------------------------------|  
| %rax          | no            | result register, also used in idiv and imul |  
| %rbx          | yes           | miscellaneous register                      |  
| %rcx          | no            | fourth argument register                    |  
| %rdx          | no            | third argument register, also idiv and imul |  
| %rsp          | no            | stack pointer                               |  
| %rbp          | yes           | frame pointer                               |  
| %rsi          | no            | second argument register                    |  
| %rdi          | no            | first argument register                     |  
| %r8           | no            | fifth argument register                     |  
| %r9           | no            | sixth argument register                     |  
| %r10          | no            | miscellaneous register                      |  
| %r11          | no            | miscellaneous register                      |  
| %r12~%15      | yes           | miscellaneous registers                     |  
  
寄存器%rbp，%rbx和%r12~%r15是callee-save的，也即由被调用函数保存。  

###3 函数调用约定
Mac OS Ｘ和Ｌinux操作系统的函数调用都遵从System V ABI，  
有三个x86-64指令用来实现函数调用和返回：  
&emsp;&emsp;&ensp;call:返回地址(当前下一条指令地址)压栈，控制权转移到操作数所在的地址；  
&emsp;&emsp;leave:设置栈指针%rsp为为帧%rbp，恢复帧指针%rbp为栈上保存的帧指针，  
&emsp;&emsp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;该指针从函数栈上弹出；  
&emsp;&emsp;&ensp;&ensp;ret:返回值从函数栈弹出，并跳转到该地址；  


#####参考文献
[http://www.classes.cs.uchicago.edu/archive/2009/spring/22620-1/docs/handout-03.pdf](http://www.classes.cs.uchicago.edu/archive/2009/spring/22620-1/docs/handout-03.pdf)  

