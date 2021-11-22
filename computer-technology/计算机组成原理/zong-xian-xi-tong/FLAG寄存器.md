---

title: PSW寄存器分析
date: 2021-06-01 07:51:22
categories: 计算机组成原理
tags:
- CS

sticky: 
pic:
comments: true
toc: true
only:
- home
- category
- tag

---

# FLAG寄存器

> 存储**程序状态字（PSW，program status word）**，存储相关指令的执行结果，为相关指令提供行为依据，用来控制CPU的相关工作方式。**flag寄存器是按位起作用的**，**每一位都有专门的含义记录特定信息**。


> 在32位CPU中称为为**EFLAGS寄存器**，64为CPU中称为**RFLAGS寄存器**，它们扩展出的高位地址都不使用。现代计算机中一般也叫做**PSW寄存器**。下面以8086为基础处理器分析该寄存器的功能

![flag寄存器](https://i.loli.net/2021/06/01/UlwYT5fQjx3gNsM.png)




#### ZF（Zero Flag）

> 第6位标志位，零标志位。计算指令执行后，若结果为0，则zf=1，否则zf=0


#### PF（Parity Flag）

> 第2位标志位，奇偶标志位。指令执行后，若所有bit位中1的个数为偶数，则pf=1，否则pf=0


   ```C
   mov al 1
   add al，al
   al=00000010   //1的个数为1，所以pf=0 
   若改为
   add al，10H
   al=00000011  //1的个数为2，所以pf=1 
   ```


#### SF（Symbol Flag）

> 第7位标志位，符号标志位。指令执行后，若结果为负，则sf=1，否则sf=0


#### CF（Carry Flag）

> 第0位标志位，进位标志位。**无符号运算中指令执行后，若产生进位**，则cf=1，否则cf=0，同时也可以用作表示借位。若其值被add设置则表示进位，被sub设置则表示借位


#### OF（Overflow Flag）

> 第11位标志位，溢出标志位。**有符号运算**时，若产生溢出，则of=1，否则of=0


#### AF（Auxiliary Flag）

> 第4位标志位，辅助进位标志位。若操作中发生了进位或借位，则af=1，否则af=0
mov al，0Fh
add al，1
计算过程
00001111
00000001
——————
00010000   位3中发生了进位，af=1


#### IF（Interrupt-Enable Flag）

> 第9位标志位，中断允许标志位。决定CPU是否能够响应外部可屏蔽中断请求，若响应则if=1，否则if=0


#### DF（Direction Flag）

> 第10位标志位，方向标志位。控制SI和DI自增还是自减。若自减，则df=1，否则df=0


#### TF（Trap Flag）

> 第8位标志位，追踪标志位。若CPU进入单步调试，则tf=1，否则tf=0
