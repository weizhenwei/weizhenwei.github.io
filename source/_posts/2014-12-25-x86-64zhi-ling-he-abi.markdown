---
layout: post
title: "x86-64指令和ABI"
date: 2014-12-25 21:51:09 +0800
comments: true
categories: x86-64 abi
---

&emsp;&emsp;本文之针对x86-64指令和ABI的综述，其内容翻译自参考文献[1]。  
#####1 引言
x86-64指令一般有两个操作数：源操作数和目的操作数，目的操作数也作为结果存放地。  
linux下的x86-64指令格式采用AT&T格式，也即源操作数在左边，目的操作数在右边。  
绝大多数x86-64指令采用后缀字母标示操作数的大小，例如q表示64为，b表示8位，w表示16位，l表示32位。  

#####2 寄存器
x86-64有16个64位通用寄存器，在AT&T格式中使用%前缀，其定义和在ABI中的角色如下表所示：  

| Register      | Callee Save   |                 Description                 |
|:-------------:|:-------------:|:--------------------------------------------|
| %rax          | no            | result register, also used in idiv and imul |
| %rbx          | yes           | miscellaneous register                      |
| %rcx          | no            | fourth argument register                    |
| %rdx          | no            | third argument register, also in idiv and imul|
| %rsp          | no            | stack pointer                               |
| %rbp          | yes           | frame pointer                               |
| %rsi          | no            | second argument register                    |
| %rdi          | no            | first argument register                     |
| %r8           | no            | fifth argument register                     |
| %r9           | no            | sixth argument register                     |
| %r10          | no            | miscellaneous register                      |
| %r11          | no            | miscellaneous register                      |
| %r12~%15      | yes           | miscellaneous registers                     |

#####3 函数调用












#####参考文献
[http://www.classes.cs.uchicago.edu/archive/2009/spring/22620-1/docs/handout-03.pdf](http://www.classes.cs.uchicago.edu/archive/2009/spring/22620-1/docs/handout-03.pdf)  
