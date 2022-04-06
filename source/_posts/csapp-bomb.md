---
title: CSAPP：BOMB实验
date: 2020-12-9 20:08:50
categories: 实验记录
tags:
- 计算机基础
- Csapp

---

-------
### 实验开始
炸弹实验是`CSAPP`的第二个实验，涉及到了`反汇编`、`读懂汇编语言`、`Linux下GDB的使用`及`C语言`，其中的读懂汇编语言是重难点，完整的看懂了一个函数的汇编语言时，炸弹也迎刃而解。

每个人得到的BOMB都是不一样的，大体上是每种类型的炸弹都有不同的题目，共六个`PHASE` + 一个`SECRET_PHASE`, 也就是七个炸弹。具体内容后面再说。每个人的BOMB都不一样，但是大体就那么几个在哪排列组合，所以花时间使用BAIDU GOOGLE的话还是可以找到原题的，但是并没有什么卵用，直接抄的话。按我们老师说就是学术剽窃，就是学术作弊。当然可以借鉴一下，毕竟不认真研究一下汇编，是真的不怎么好做这BOMB实验。最好还是自己慢慢看懂汇编，翻译成原来的C语言代码，再得到密码解除炸弹，这样子的收获才是最大的。

实验的资料自己都有哦，懂得都懂。  

### 实验过程
#### 实验概述

+ 逆向工程拆除“二进制炸弹”程序  
+ 增强对程序机器级表示、汇编语言、调试器和逆向工程等理解。  
+ 一个“Binary Bombs”（二进制炸弹，简称炸弹）是一个Linux可执行C程序，包含phase1~phase6共6个阶段。  
+ 炸弹运行各阶段要求输入一个字符串，若输入符合程序预期，该阶段炸弹被“拆除”，否则“爆炸” 。  
+ 你需要拆除尽可能多的炸弹。  

#### 实验介绍  
每个炸弹阶段考察机器级语言程序不同方面，难度递增  
+ 阶段1：字符串比较
+ 阶段2：循环
+ 阶段3：条件/分支：含switch语句
+ 阶段4：递归调用和栈
+ 阶段5：指针
+ 阶段6：链表/指针/结构
+ 隐藏阶段：第4阶段之后附加特定字符串后出现

好家伙，老师提供的PPT里就直接说明了，以上内容，尤其是隐藏阶段，即SECRET_PHASE，在哪出现和出现的条件。 = =  

#### 实验技能
+ 拆弹装备：
  + 熟练使用gdb调试器和objdump；
  + 单步跟踪调试每一阶段的机器代码；
  + 理解汇编语言代码的行为或作用；
  + “推断”拆除炸弹所需的目标字符串。
  + 在各阶段的开始代码前和引爆炸弹函数前设置断点，便于调试。
+ 实验语言：C语言，at&t汇编语言
+ 实验环境：32位 linux  

#### 实验文件说明
+ 炸弹文件包：（每个人的不一样）
+ $tar vxf bomb_2017.tar
  + bomb：   bomb的可执行程序。
  + bomb.c：bomb程序的main函数。
  + README
+ bomb：是一个linux下可执行程序，需要0或1个命令行参数
  + 不带参数运行，输出欢迎信息后，期待你按行输入                拆弹字符串，错误炸弹引爆退出，正确提示进入下一关。
  + 带参数运行，从拆弹者的密码文件中读取用户密码
+ bomb.c：bomb主程序，帮助拆弹者了解代码框架，没有细节

#### 拆弹方式
+ 方法1：$./bomb 
  + 根据提示，逐阶段手工输入拆弹字符串（见演示）
  + 较为繁琐，重复工作多

[![qveCUf.md.png](https://s1.ax1x.com/2022/04/06/qveCUf.md.png)](https://imgtu.com/i/qveCUf)
+ 方法2：$./bomb ans.txt     （推荐）
  + ans.txt为拆弹密码文本文件，名字可以自定义
    + 文本文件，每个拆弹字符串一行，回车结束，最多7行
    + 除此之外不要包含任何其它字符
  + 程序会检查每一阶段的拆弹密码字符串来决定炸弹拆除成败。

[![qveSbt.md.png](https://s1.ax1x.com/2022/04/06/qveSbt.md.png)](https://imgtu.com/i/qveSbt)

这样子是真的快！ 
```terminal
$ ./bomb ans.txt
```

### 开始拆弹  
首先反汇编`bomb`
```ter
$ objdump –d bomb > asm.txt
```
对bomb进行反汇编并将汇编代码输出到asm.txt中。  

然后查看汇编文件`asm.txt`。寻找`phase`所在的汇编代码段。 

#### Phase_1

在`asm.txt`的`main`函数中找到如下语句
这里为`phase1`函数在`main()`函数中被调用的位置：

```text
 8048a9a:	c7 04 24 01 00 00 00 	movl   $0x1,(%esp)
 8048aa1:	e8 ea fd ff ff       	call   8048890 <__printf_chk@plt>
 8048aa6:	c7 04 24 08 00 00 00 	movl   $0x8,(%esp)
 8048aad:	e8 7e fd ff ff       	call   8048830 <exit@plt>
 8048ab2:	e8 7c 06 00 00       	call   8049133 <initialize_bomb>
 8048ab7:	c7 04 24 cc a1 04 08 	movl   $0x804a1cc,(%esp)
 8048abe:	e8 2d fd ff ff       	call   80487f0 <puts@plt>
 8048ac3:	c7 04 24 08 a2 04 08 	movl   $0x804a208,(%esp)
 8048aca:	e8 21 fd ff ff       	call   80487f0 <puts@plt>
 8048acf:	e8 7d 07 00 00       	call   8049251 <read_line>
 8048ad4:	89 04 24             	mov    %eax,(%esp)
 8048ad7:	e8 b4 00 00 00       	call   8048b90 <phase_1>
                                                   //phase_1的位置，往下翻找即可
 8048adc:	e8 6e 08 00 00       	call   804934f <phase_defused>
 8048ae1:	c7 04 24 34 a2 04 08 	movl   $0x804a234,(%esp)
```
然后再就是`phase_1`:  
```text
08048b90 <phase_1>:
 8048b90:	55                   	push   %ebp
 8048b91:	89 e5                	mov    %esp,%ebp
 8048b93:	83 ec 18             	sub    $0x18,%esp //开栈
 8048b96:	c7 44 24 04 84 a2 04 	movl   $0x804a284,0x4(%esp) 
                                           //将0x804a284的内容存放到esp+4的位置
 8048b9d:	08 
 8048b9e:	8b 45 08             	mov    0x8(%ebp),%eax
                                           //esp+8，从调用函数处取第一个参数放到eax寄中
 8048ba1:	89 04 24             	mov    %eax,(%esp)
                                           //传送到esp寄存器
 8048ba4:	e8 19 05 00 00       	call   80490c2 <strings_not_equal>
                                           //入口函数， 判断字符串是否相等（判断esp+4和esp+8的字符串是否相等）
 8048ba9:	85 c0                	test   %eax,%eax
                                           //当两个字符串相等时返回eax=0
 8048bab:	74 05                	je     8048bb2 <phase_1+0x22>
                                           //是否引爆炸弹的条件（eax=0跳到leave，否则引爆炸弹，因此通关的条件是eax=0）
 8048bad:	e8 25 06 00 00       	call   80491d7 <explode_bomb>
 8048bb2:	c9                   	leave  
 8048bb3:	c3                   	ret    
```

根据以上分析可知，程序先将输入的参数存放到`ebp+8`的位置，接着传送到`esp`中，然后函数在`0x804a284`这个地址取值，放到`esp+8`中。最后传送到`eax`进行比较，如果相等，返回`eax = 0`，跳到`leave`结束，不相等则返回`1`，同时调用引爆炸弹的函数。因此只要查看`0x804a284`这个地址的内容就能找到密码！用`GDB调试工具`进行查看：
[![qvZLCD.md.png](https://s1.ax1x.com/2022/04/06/qvZLCD.md.png)](https://imgtu.com/i/qvZLCD)

还可以使用方法二：
```
Objdump --start-address=0x804a0fc –s bomb   #方法2
```
建议慎用 T T
[![qvZHUK.md.png](https://s1.ax1x.com/2022/04/06/qvZHUK.md.png)](https://imgtu.com/i/qvZHUK)
密码是出来了，但是多了一长串的后面地址的内容。

`phase_1`的密码：  
> Public speaking is very easy.  

将其放入`ans.txt`中再`./bomb ans.txt`可得：
[![qvZ7E6.md.png](https://s1.ax1x.com/2022/04/06/qvZ7E6.md.png)](https://imgtu.com/i/qvZ7E6)


一下简要介绍GBD在本次拆炸弹中的使用：

##### GDB工具的使用
terminal输入gdb bomb，即是调试bomb这个程序，显示如下：
```text
b xxx   //在XX处设置断点
ni      //单步执行机器指令
x/2s    //查看地址中的两个字符串
x/d     //查看地址中的整数
```
```text
GNU gdb (GDB) 7.2-ubuntu
Copyright (C) 2010 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
and "show warranty" for details.
This GDB was configured as "i686-linux-gnu".
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>...
./bomb/bomblab/src/bomb...done.
gdb) b main        #在main函数的开始处设置断点   
Breakpoint 1 at 0x80489a5: file bomb.c, line 45.
(gdb) r                  #从gdb里运行bomb程序
Starting program:./bomb/bomblab/src/bomb 
                              # 运行后，暂停在断点1处
Breakpoint 1, main (argc=1, argv=0xbffff3f4) at bomb.c:45
45	    if (argc == 1) { 
(gdb) ni                #单步执行机器指令
0x080489a8	45	    if (argc == 1) {  
(gdb) ni
46		infile = stdin;   #这里可以看到执行到哪一条C语句
(gdb) ni
73	    input = read_line();             /* Get input                   */
(gdb) ni                /*如果是命令行输入，这里输入你的拆弹字符串*/
74	    phase_1(input);                  /* Run the phase               */
(gdb) x/2s 0x804a284       #查看地址0x804a0fc处两个字符串：
0x804a284:	"Public speaking is very easy."
0x804a2a2:	"%d %c %d" 
(gdb) q                          #退出gdb               
```  




#### Phase_2
可知此次是关于循环的，不多BB直接上汇编：

```text
08048bb4 <phase_2>:
 8048bb4:	55                   	push   %ebp
 8048bb5:	89 e5                	mov    %esp,%ebp
 8048bb7:	56                   	push   %esi
 8048bb8:	53                   	push   %ebx
                                           //esi和ebx为调用者保存寄存器，因为后面的循环用到了者两个寄存器，因此要压栈保存
 8048bb9:	83 ec 30             	sub    $0x30,%esp 
                                           //esp - 48开栈
 8048bbc:	8d 45 e0             	lea    -0x20(%ebp),%eax
 8048bbf:	89 44 24 04          	mov    %eax,0x4(%esp)
                                           //以上两句将ebp-32处的地址借助eax传给esp+4处
 8048bc3:	8b 45 08             	mov    0x8(%ebp),%eax
 8048bc6:	89 04 24             	mov    %eax,(%esp)
                                           //以上两句将ebp+8处的地址传给esp
 8048bc9:	e8 33 06 00 00       	call   8049201 <read_six_numbers>
                                           //输入6个数
 8048bce:	83 7d e0 01          	cmpl   $0x1,-0x20(%ebp)
                                           //(ebp - 32)- 1 = 0
 8048bd2:	74 1e                	je     8048bf2 <phase_2+0x3e>
                                           //引爆炸弹的条件，不为1则引爆炸弹。因此ebp-32处要为1，从前面看，这是存放输入参数的位置
 8048bd4:	e8 fe 05 00 00       	call   80491d7 <explode_bomb>
 8048bd9:	eb 17                	jmp    8048bf2 <phase_2+0x3e>

 8048bdb:	8b 43 fc             	mov    -0x4(%ebx),%eax
 8048bde:	01 c0                	add    %eax,%eax
 8048be0:	39 03                	cmp    %eax,(%ebx)
                                           //以上三句将(ebx-4)传给eax，eax = eax*2 
                                           eax - ebx = 0就跳转，反之不为0，引爆炸弹
 8048be2:	74 05                	je     8048be9 <phase_2+0x35>
 8048be4:	e8 ee 05 00 00       	call   80491d7 <explode_bomb>

 8048be9:	83 c3 04             	add    $0x4,%ebx
                                           //ebx上移4，ebx+4
 8048bec:	39 f3                	cmp    %esi,%ebx
                                           // esi - ebx ！= 0
 8048bee:	75 eb                	jne    8048bdb <phase_2+0x27>
 8048bf0:	eb 08                	jmp    8048bfa <phase_2+0x46>
                                           //当esi=ebx时跳出循环，反之继续循环。
 8048bf2:	8d 5d e4             	lea    -0x1c(%ebp),%ebx
                                           //ebp - 28传给ebx(调用者帧保存)
 8048bf5:	8d 75 f8             	lea    -0x8(%ebp),%esi
                                           //ebp - 8 传给esi(调用者帧保存)
 8048bf8:	eb e1                	jmp    8048bdb <phase_2+0x27>

 8048bfa:	83 c4 30             	add    $0x30,%esp
 8048bfd:	5b                   	pop    %ebx
 8048bfe:	5e                   	pop    %esi
 8048bff:	5d                   	pop    %ebp
 8048c00:	c3                   	ret    
 ```

栈图如下：
[![qvZd3Q.png](https://s1.ax1x.com/2022/04/06/qvZd3Q.png)](https://imgtu.com/i/qvZd3Q)
分析：  
显然是一个首项为1，公比为2的等比数列。

第二关密码：
> 1 2 4 8 16 32

#### Phase_3
可知本关与switch有关，有分支，故而代码较长，解题选一种情况即可（看了才知道的）。
继续上汇编代码：
```text
08048c01 <phase_3>:
 8048c01:	55                   	push   %ebp
 8048c02:	89 e5                	mov    %esp,%ebp
 8048c04:	83 ec 38             	sub    $0x38,%esp
                                           // esp-56开栈
 8048c07:	8d 45 f4             	lea    -0xc(%ebp),%eax
 8048c0a:	89 44 24 10          	mov    %eax,0x10(%esp)
                                           //ebp-12 借助eax传给esp + 16
 8048c0e:	8d 45 ef             	lea    -0x11(%ebp),%eax
 8048c11:	89 44 24 0c          	mov    %eax,0xc(%esp)
                                           //ebp-17借助eax传给esp+12
 8048c15:	8d 45 f0             	lea    -0x10(%ebp),%eax
 8048c18:	89 44 24 08          	mov    %eax,0x8(%esp)
                                           //ebp-16借助eax传给esp+8
 8048c1c:	c7 44 24 04 a2 a2 04 	movl   $0x804a2a2,0x4(%esp)
                                           //将0x804a2a2的内容传给esp+8
                                           //GDB查看发现是%d%c%d
 8048c23:	08 
```

0x804a2a2这个地址有点熟悉哦，感觉在哪见过——
[![qvZd3Q.png](https://s1.ax1x.com/2022/04/06/qvZd3Q.png)](https://imgtu.com/i/qvZd3Q)
好家伙，查0x804a284的时候就出现0x804a2a2了，还是进入GDB再看看。
[![qvZa9g.png](https://s1.ax1x.com/2022/04/06/qvZa9g.png)](https://imgtu.com/i/qvZa9g)
好家伙，确实是这样，需要我们输入`%d %c %d`,两个整数，一个字符。（所以这也是这个的原因）
> lea    -0x11(%ebp),%eax
> mov    %eax,0xc(%esp) 
> //ebp-17借助eax传给esp+12

第二个参数只占一个一个字节。（这里之前想了好久。。。。。。）
继续看汇编：
```text
 8048c24:	8b 45 08             	mov    0x8(%ebp),%eax
 8048c27:	89 04 24             	mov    %eax,(%esp)
                                           // ebp-8借助eax传给esp
 8048c2a:	e8 31 fc ff ff       	call   8048860 <__isoc99_sscanf@plt>
                                           //读入函数，将你输入的参数按指定格式读到相应的地址
 8048c2f:	83 f8 02             	cmp    $0x2,%eax
                                           //eax接受ssacnf函数的返回值，说明sscanf函数的返回值是参数个数，如果大于2跳过炸弹，否则引爆炸弹。
 8048c32:	7f 05                	jg     8048c39 <phase_3+0x38>
 8048c34:	e8 9e 05 00 00       	call   80491d7 <explode_bomb>

 8048c39:	83 7d f0 07          	cmpl   $0x7,-0x10(%ebp)
 8048c3d:	0f 87 e9 00 00 00    	ja     8048d2c <phase_3+0x12b>
                                           //以上两句说明ebp-16不能超过7，否则就引爆炸弹。
 8048c43:	8b 45 f0             	mov    -0x10(%ebp),%eax
                                           //ebp-16赋给eax
 8048c46:	ff 24 85 c0 a2 04 08 	jmp    *0x804a2c0(,%eax,4)
                                           //间接跳转，跳到*0x804a2c0这个地址，这是第三关的核心代码！
```
详细分析：
ja : 无符号大于则跳转; 代表ebp-16中的内容只能小于等于7，大于等于0，再看上面的代码易知ebp-16是第一个参数，故设第一个参数为i，再往下看可知：
> i = 0, 1, 2, 3, 4, 5, 6, 7

所以就会有8个不同的密码！
> -0x10(%ebp),%eax //ebp-16赋给eax

即第一个参数赋给eax。
> jmp    *0x804a2c0(,%eax,4)

用GDB查看*0x804a2c0,可知这个指针指向0x8048c4d。即使当i=1的情况。
仔细一看发现后面的汇编大体相似，应该就是i取值不同时的不同情况。
```text
 8048c4d:	b8 6d 00 00 00       	mov    $0x6d,%eax
                                           // eax = 0x6d
 8048c52:	81 7d f4 f0 01 00 00 	cmpl   $0x1f0,-0xc(%ebp)
 8048c59:	0f 84 d7 00 00 00    	je     8048d36 <phase_3+0x135>
                                           // ebp-12 = 0x1f0 跳转，反之爆炸。
 8048c5f:	e8 73 05 00 00       	call   80491d7 <explode_bomb>
 8048c64:	b8 6d 00 00 00       	mov    $0x6d,%eax
                                           // eax = 0x6d
 8048c69:	e9 c8 00 00 00       	jmp    8048d36 <phase_3+0x135>
                                           
```
edp-12是第三个参数，为496
```
 8048d2c:	e8 a6 04 00 00       	call   80491d7 <explode_bomb>
 8048d31:	b8 77 00 00 00       	mov    $0x77,%eax
 8048d36:	3a 45 ef             	cmp    -0x11(%ebp),%al
                                           // 比较ebp-17 和 al寄存器中的值，相等结束，反之爆炸。
 8048d39:	74 05                	je     8048d40 <phase_3+0x13f>
 8048d3b:	e8 97 04 00 00       	call   80491d7 <explode_bomb>
 8048d40:	c9                   	leave  
 8048d41:	c3                   	ret
 ```
al寄存器是eax的低8位，举例
> mov eax 12345678h
> mov al 78h
> AX是EAX的低16位
> AH是ax的高8位，而AL是ax的低8位  

差不多这个意思。
> cmp    -0x11(%ebp),%al
> je     8048d40 <phase_3+0x13f>

就是第二个参数等于al中的内容，即上面eax的内容（eax = 0x6d）  
定义 char B;    
B是第二个参数，B = 0x6d。
查ASCII码表知   B = m。
[![qvZYAf.md.png](https://s1.ax1x.com/2022/04/06/qvZYAf.md.png)](https://imgtu.com/i/qvZYAf)

所以其中一个密码为  
0 m 496


以下分析方法同上，就不做重复的分析：
```text
 8048c6e:	b8 6f 00 00 00       	mov    $0x6f,%eax
 8048c73:	81 7d f4 5a 01 00 00 	cmpl   $0x15a,-0xc(%ebp)
 8048c7a:	0f 84 b6 00 00 00    	je     8048d36 <phase_3+0x135>
 8048c80:	e8 52 05 00 00       	call   80491d7 <explode_bomb>
 8048c85:	b8 6f 00 00 00       	mov    $0x6f,%eax
 8048c8a:	e9 a7 00 00 00       	jmp    8048d36 <phase_3+0x135>

 8048c8f:	b8 70 00 00 00       	mov    $0x70,%eax
 8048c94:	83 7d f4 64          	cmpl   $0x64,-0xc(%ebp)
 8048c98:	0f 84 98 00 00 00    	je     8048d36 <phase_3+0x135>
 8048c9e:	e8 34 05 00 00       	call   80491d7 <explode_bomb>
 8048ca3:	b8 70 00 00 00       	mov    $0x70,%eax
 8048ca8:	e9 89 00 00 00       	jmp    8048d36 <phase_3+0x135>

 8048cad:	b8 68 00 00 00       	mov    $0x68,%eax
 8048cb2:	83 7d f4 3d          	cmpl   $0x3d,-0xc(%ebp)
 8048cb6:	74 7e                	je     8048d36 <phase_3+0x135>
 8048cb8:	e8 1a 05 00 00       	call   80491d7 <explode_bomb>
 8048cbd:	b8 68 00 00 00       	mov    $0x68,%eax
 8048cc2:	eb 72                	jmp    8048d36 <phase_3+0x135>

 8048cc4:	b8 6f 00 00 00       	mov    $0x6f,%eax
 8048cc9:	81 7d f4 02 02 00 00 	cmpl   $0x202,-0xc(%ebp)
 8048cd0:	74 64                	je     8048d36 <phase_3+0x135>
 8048cd2:	e8 00 05 00 00       	call   80491d7 <explode_bomb>
 8048cd7:	b8 6f 00 00 00       	mov    $0x6f,%eax
 8048cdc:	eb 58                	jmp    8048d36 <phase_3+0x135>

 8048cde:	b8 6e 00 00 00       	mov    $0x6e,%eax
 8048ce3:	81 7d f4 d5 00 00 00 	cmpl   $0xd5,-0xc(%ebp)
 8048cea:	74 4a                	je     8048d36 <phase_3+0x135>
 8048cec:	e8 e6 04 00 00       	call   80491d7 <explode_bomb>
 8048cf1:	b8 6e 00 00 00       	mov    $0x6e,%eax
 8048cf6:	eb 3e                	jmp    8048d36 <phase_3+0x135>

 8048cf8:	b8 74 00 00 00       	mov    $0x74,%eax
 8048cfd:	81 7d f4 97 01 00 00 	cmpl   $0x197,-0xc(%ebp)
 8048d04:	74 30                	je     8048d36 <phase_3+0x135>
 8048d06:	e8 cc 04 00 00       	call   80491d7 <explode_bomb>
 8048d0b:	b8 74 00 00 00       	mov    $0x74,%eax
 8048d10:	eb 24                	jmp    8048d36 <phase_3+0x135>

8048d12:	b8 74 00 00 00       	mov    $0x74,%eax
8048d17:	81 7d f4 9b 01 00 00 	cmpl   $0x19b,-0xc(%ebp)8048d1e:	74 16                	je     8048d36 <phase_3+0x135>
8048d20:	e8 b2 04 00 00       	call   80491d7 <explode_bomb>
8048d25:	b8 74 00 00 00       	mov    $0x74,%eax
8048d2a:	eb 0a                	jmp    8048d36 <phase_3+0x135>
```

所以第三关密码为：  
0 m 496  
1 o 346  
2 p 100  
3 h 61  
4 o 514  
5 n 213  
6 t 407
7 t 411   
任选一组即可过关。  

#### phase_4
我们可知phase_4与递归的调用有关，不看不知道，一看吓一跳，递归在汇编里看着就是真的恶心啊。（主要还是自己看不明白（主要还是汇编学的不是很透彻））。  
不多比比继续直接看代码：
```text
08048da4 <phase_4>:
 8048da4:	55                   	push   %ebp
 8048da5:	89 e5                	mov    %esp,%ebp
 8048da7:	83 ec 28             	sub    $0x28,%esp
                                           //esp-40开栈
 8048daa:	8d 45 f4             	lea    -0xc(%ebp),%eax
 8048dad:	89 44 24 0c          	mov    %eax,0xc(%esp)
                                           //ebp-12借助eax传给esp+12
 8048db1:	8d 45 f0             	lea    -0x10(%ebp),%eax
 8048db4:	89 44 24 08          	mov    %eax,0x8(%esp)
                                           //ebp-16借助eax传给esp+8
 8048db8:	c7 44 24 04 57 a4 04 	movl   $0x804a457,0x4(%esp)
                                           //使用GDB查看知需要输入两个整型 %d %d
 8048dbf:	08 
 8048dc0:	8b 45 08             	mov    0x8(%ebp),%eax
 8048dc3:	89 04 24             	mov    %eax,(%esp)
                                           //ebp+8借助eax传给esp
 8048dc6:	e8 95 fa ff ff       	call   8048860 <__isoc99_sscanf@plt>
                                          
 8048dcb:	83 f8 02             	cmp    $0x2,%eax
                                           //判断参数个数是否为2，不为2，爆炸
 8048dce:	75 06                	jne    8048dd6 <phase_4+0x32>

 8048dd0:	83 7d f0 0e          	cmpl   $0xe,-0x10(%ebp)
                                           //(ebp-16)-14 <= 0 跳转，反之爆炸
                                           //可知参数一是一个小于等于14的无符号型整数
 8048dd4:	76 05                	jbe    8048ddb <phase_4+0x37>
 8048dd6:	e8 fc 03 00 00       	call   80491d7 <explode_bomb>
```
设参数一为A， 所以0 <= A <= 14  
```text
 8048ddb:	c7 44 24 08 0e 00 00 	movl   $0xe,0x8(%esp)
                                           //exp+8 = 14
 8048de2:	00 
 8048de3:	c7 44 24 04 00 00 00 	movl   $0x0,0x4(%esp)
                                           //esp+4 = 0
 8048dea:	00 
 8048deb:	8b 45 f0             	mov    -0x10(%ebp),%eax
 8048dee:	89 04 24             	mov    %eax,(%esp)
                                           // ebp-16赋值给esp(参数1赋给esp)
 8048df1:	e8 4c ff ff ff       	call   8048d42 <func4>//进入递归
 ```
进入递归Func4函数时传入了三个参数，即14，0，A（参数1）。  
 ```text
 8048df6:	83 f8 06             	cmp    $0x6,%eax
                                           //eax是递归函数的返回值且为6，不为6，爆炸。
 8048df9:	75 06                	jne    8048e01 <phase_4+0x5d>
 8048dfb:	83 7d f4 06          	cmpl   $0x6,-0xc(%ebp)
                                           //(ebp-12) - 6 = 0
                                           // ebp-12是参数2，即参数2为6。
                                           // 参数2为6时，结束，反之爆炸。
 8048dff:	74 05                	je     8048e06 <phase_4+0x62>
 8048e01:	e8 d1 03 00 00       	call   80491d7 <explode_bomb>
 8048e06:	c9                   	leave  
 8048e07:	c3                   	ret   
 ```
 分析到这里时，我们已经知道了`参数1`的范围`[0, 14]`, `参数2`为`6`。  
 其实我们擦不多就可以结束phase4的分析了，差不多可以知道密码了。  
 我们可以一个一个地带进去试验  即输入`i 6`,其中`i = 0, 1, 2, ..., 14`。
 最后我们可以得到第四关地密码：  
 `6 6  `

 但是投机取巧并不好，万一有人问道——递归函数（func4）时怎么样的呢  
 那么你就回答不上来了。  所以我们还要继续分析，知道全部熟络于心。  
 但是下面的递归是真的难，真的花时间。  

 现在我们开始func4的分析：  
 ```text
08048d42 <func4>:
 8048d42:	55                   	push   %ebp
 8048d43:	89 e5                	mov    %esp,%ebp
 8048d45:	56                   	push   %esi
 8048d46:	53                   	push   %ebx
 8048d47:	83 ec 10             	sub    $0x10,%esp
                                           //esp-16开栈
 8048d4a:	8b 55 08             	mov    0x8(%ebp),%edx //ebp+8赋给edx，记为参数A
 8048d4d:	8b 45 0c             	mov    0xc(%ebp),%eax //ebp+12赋给eax，记为参数B
 8048d50:	8b 5d 10             	mov    0x10(%ebp),%ebx //ebp+16赋给ebx，记为参数C
                                           
 8048d53:	89 d9                	mov    %ebx,%ecx //ebx赋给ecx
 8048d55:	29 c1                	sub    %eax,%ecx //ecx=ecx-eax=C-B
 8048d57:	89 ce                	mov    %ecx,%esi //ecx赋给esi
 8048d59:	c1 ee 1f             	shr    $0x1f,%esi //esi逻辑右移31位
 8048d5c:	01 f1                	add    %esi,%ecx //ecx=ecx+esi
 8048d5e:	d1 f9                	sar    %ecx //ecx算术右移1位，就是C/2。
 8048d60:	01 c1                	add    %eax,%ecx //ecx=ecx+eax
```
上述汇编是对参数进行了算术运算。  
```text
 8048d62:	39 d1                	cmp    %edx,%ecx
                                           //if(edx <= ecx) 跳转到 8048d7d，否则顺序执行。
 8048d64:	7e 17                	jle    8048d7d <func4+0x3b>

 8048d66:	83 e9 01             	sub    $0x1,%ecx
                                           // ecx=ecx-1
 8048d69:	89 4c 24 08          	mov    %ecx,0x8(%esp)
 8048d6d:	89 44 24 04          	mov    %eax,0x4(%esp)
 8048d71:	89 14 24             	mov    %edx,(%esp)
                                           //构造func4的参数
 8048d74:	e8 c9 ff ff ff       	call   8048d42 <func4>
                                           //进入递归

 8048d79:	01 c0                	add    %eax,%eax
                                           //eax=eax+eax
                                           //递归返回值加倍
 8048d7b:	eb 20                	jmp    8048d9d <func4+0x5b>

 8048d7d:	b8 00 00 00 00       	mov    $0x0,%eax
                                           //eax=0
 8048d82:	39 d1                	cmp    %edx,%ecx
                                           if(edx >= ecx) 递归终止，否则顺序执行。
 8048d84:	7d 17                	jge    8048d9d <func4+0x5b>
 
 8048d86:	89 5c 24 08          	mov    %ebx,0x8(%esp)
 8048d8a:	83 c1 01             	add    $0x1,%ecx
                                           //ecx=ecx+1
 8048d8d:	89 4c 24 04          	mov    %ecx,0x4(%esp)
 8048d91:	89 14 24             	mov    %edx,(%esp)
                                           //构造func4的参数
 8048d94:	e8 a9 ff ff ff       	call   8048d42 <func4>
                                           //进入递归
 8048d99:	8d 44 00 01          	lea    0x1(%eax,%eax,1),%eax
                                           //eax=eax*2+1
                                           //递归返回值加倍后加一
 8048d9d:	83 c4 10             	add    $0x10,%esp
 8048da0:	5b                   	pop    %ebx
 8048da1:	5e                   	pop    %esi
 8048da2:	5d                   	pop    %ebp
 8048da3:	c3                   	ret    
 ```
最终可得C语言函数func4：  
```c
int func4(int ebx, int eax, int edx)
{
    int esi = (ebx - eax) >> 31;
    int ecx = (ebx - eax + esi) >> 1;
    ecx = ecx + eax;

    if (edx == ecx)
        return 0;
    if (edx > ecx)
        return func4(ebx, ecx + 1, edx) * 2 + 1;

    else
        return func4(ecx - 1, eax, edx) * 2;
}
```
```c
int main()
{
    for (int i = 0; i <= 14; i++)
    {
        if (func4(14, 0, i) == 6)
        {
            printf("%d\n", i);
            getchar();
            return 0;
        }
    }
    getchar();
    return 0;
}
```
于是可得需要输入的第一个参数为`6`。  
故phase_4的密码为：  
6 6  


#### phase_5
```text
08048e08 <phase_5>:
 8048e08:	55                   	push   %ebp
 8048e09:	89 e5                	mov    %esp,%ebp
 8048e0b:	83 ec 28             	sub    $0x28,%esp
                                       //esp-40开栈

 8048e0e:	8d 45 f4             	lea    -0xc(%ebp),%eax
 8048e11:	89 44 24 0c          	mov    %eax,0xc(%esp)
 8048e15:	8d 45 f0             	lea    -0x10(%ebp),%eax
 8048e18:	89 44 24 08          	mov    %eax,0x8(%esp)
                                       //两个参数的赋值，分别为参数1，参数2，可知本关需要输入两个参数
 8048e1c:	c7 44 24 04 57 a4 04 	movl   $0x804a457,0x4(%esp)
                                       //使用GDB可知为%d %d，故需要输入两个整型参数
 8048e23:	08 

 8048e24:	8b 45 08             	mov    0x8(%ebp),%eax
 8048e27:	89 04 24             	mov    %eax,(%esp)
 8048e2a:	e8 31 fa ff ff       	call   8048860 <__isoc99_sscanf@plt>
 8048e2f:	83 f8 01             	cmp    $0x1,%eax
 8048e32:	7f 05                	jg     8048e39 <phase_5+0x31>
 8048e34:	e8 9e 03 00 00       	call   80491d7 <explode_bomb>
                                       //这一段的意思就是（前几关说过）
                                       //需要输入大于一个的参数个数，否则爆炸
 8048e39:	8b 45 f0             	mov    -0x10(%ebp),%eax
                                       //参数1赋给eax
 8048e3c:	83 e0 0f             	and    $0xf,%eax
                                       //按位与操作，即eax = eax & 0xf
                                       //按位与后eax 必然小于等于 0x0000 000f
 8048e3f:	89 45 f0             	mov    %eax,-0x10(%ebp)
                                       //eax 赋给ebp-16
 8048e42:	83 f8 0f             	cmp    $0xf,%eax
                                       //if ((ebp-16) - 15 == 0) 爆炸，否则顺序执行。
                                       //故经过按位与和比较后可知参数1小于15
                                       
 8048e45:	74 28                	je     8048e6f <phase_5+0x67>

 8048e47:	b9 00 00 00 00       	mov    $0x0,%ecx
 8048e4c:	ba 00 00 00 00       	mov    $0x0,%edx
 8048e51:	83 c2 01             	add    $0x1,%edx
                                       //令ecx = 0; edx = 0;
                                       // edx += 1;循环的次数
 8048e54:	8b 04 85 e0 a2 04 08 	mov    0x804a2e0(,%eax,4),%eax
                                       //使用GDB知0x804a2e0为一维数组的首地址
                                       //操作为 eax = array[eax]
                                       //首次的eax = 输入的参数一
```
经GDB得数组为`array[16]={10,2,14,7,8,12,15,11,0,4,1,13,3,9,6,5}`。
```text
 8048e5b:	01 c1                	add    %eax,%ecx
                                       //ecx = ecx + array[eax]
 8048e5d:	83 f8 0f             	cmp    $0xf,%eax
                                       //当eax!=15时继续循环，否则跳出循环。
                                       //跳出循环时eax=15
 8048e60:	75 ef                	jne    8048e51 <phase_5+0x49>

 8048e62:	89 45 f0             	mov    %eax,-0x10(%ebp)
                                       //(ebp-16)=eax
 8048e65:	83 fa 0f             	cmp    $0xf,%edx
                                       //当循环次数小于15次时顺序执行，否则爆炸。
 8048e68:	75 05                	jne    8048e6f <phase_5+0x67>
 8048e6a:	3b 4d f4             	cmp    -0xc(%ebp),%ecx
                                       //if (参数2 == ecx) 结束，否则爆炸。
 8048e6d:	74 05                	je     8048e74 <phase_5+0x6c>
 8048e6f:	e8 63 03 00 00       	call   80491d7 <explode_bomb>
 8048e74:	c9                   	leave  
 8048e75:	c3                   	ret 
 ```
 分析：  
 分析得参数2 = 循环时数组元素的和，即sum += array[eax]，开始进行循环时 eax = array[参数1]，循环时eax的取值为 0 - 14，循环结束时 eax = 15，15是读取数组得来的。想要知道参数1的值就需要逆向推理求sum的过程，由`0x804a2e0(,%eax,4),%eax`可得也就是`eax=array[eax]`，所以就是当eax=15是逆向运算，直到eax为参数1即可结束，参数2也是循环过程中所得array[eax]的和。  
 逆向过程：
 > array[6] = 15;
 > array[14] = 6;
 > array[2] = 14;
 > array[1] = 2;
 > array[10] = 1;
 > array[0] = 10;
 > array[8] = 0;
 > array[4] = 8;
 > array[9] = 4;
 > array[13] = 9;
 > array[11] = 13;
 > array[7] = 11;
 > array[3] = 7;
 > array[12] = 3;
 > 以上时循环时的变化
 > array[参数1] = 12;
> 看数组知array[5] = 12 所以参数1 = 5

所以参数2为上述数组元素之和 = 115，参数1 = 5。
phase_5密码：  
5 115  


#### phase_6
phase_6是一个关于链表的关卡，需要输入6个数字。
```text
08048e76 <phase_6>:
 8048e76:	55                   	push   %ebp
 8048e77:	89 e5                	mov    %esp,%ebp
 8048e79:	56                   	push   %esi
 8048e7a:	53                   	push   %ebx
                                       ////以上两个为调用者保存寄存器，后面的循环用到，故压栈保存(寄存器数量有限，要将原来的状态保存，因为要复原）
 8048e7b:	83 ec 40             	sub    $0x40,%esp
                                       //esp-64开栈
 8048e7e:	8d 45 c8             	lea    -0x38(%ebp),%eax
 8048e81:	89 44 24 04          	mov    %eax,0x4(%esp)
                                       //ebp-56借助eax传给esp+4
 8048e85:	8b 45 08             	mov    0x8(%ebp),%eax
 8048e88:	89 04 24             	mov    %eax,(%esp)
                                       //ebp+8 借助eax传给esp
 8048e8b:	e8 71 03 00 00       	call   8049201 <read_six_numbers>
                                       ////读入6个数

 8048e90:	be 00 00 00 00       	mov    $0x0,%esi //清零
 8048e95:	8b 44 b5 c8          	mov    -0x38(%ebp,%esi,4),%eax
                                       // eax = (ebp-64) + 4*esi
                                       //当前esi=0，亦即把ebp-64赋给eax，对于不同的esi，就是从ebp-64向上找第esi个数赋给eax。
 8048e99:	83 e8 01             	sub    $0x1,%eax //eax -= 1
 8048e9c:	83 f8 05             	cmp    $0x5,%eax  
                                       //if (5 >= eax-1) 跳转，否则爆炸
                                       //jbe是无符号数操作，故推知eax的范围为1-6
 8048e9f:	76 05                	jbe    8048ea6 <phase_6+0x30>
 8048ea1:	e8 31 03 00 00       	call   80491d7 <explode_bomb>

 8048ea6:	83 c6 01             	add    $0x1,%esi 
                                       //esi += 1;
                                       //(取第二个数）
 8048ea9:	83 fe 06             	cmp    $0x6,%esi 
                                       //if (esi - 6 != 0) 跳转，否则顺序执行 
                                       //判断取的数是否超过6个，若大于6个引爆炸弹。从而推知循环结束的条件是esi=6。
 8048eac:	75 07                	jne    8048eb5 <phase_6+0x3f>
 8048eae:	bb 00 00 00 00       	mov    $0x0,%ebx //ebx = 0
 8048eb3:	eb 3a                	jmp    8048eef <phase_6+0x79>

 8048eb5:	89 f3                	mov    %esi,%ebx // ebx = esi
 8048eb7:	8b 44 9d c8          	mov    -0x38(%ebp,%ebx,4),%eax
                                       //eax = (ebp-64) + 4*ebx
 8048ebb:	39 44 b5 c4          	cmp    %eax,-0x3c(%ebp,%esi,4)
                                       // if (eax - ((ebx-64) + 4*esi)!=0)跳转，否则爆炸
 8048ebf:	75 05                	jne    8048ec6 <phase_6+0x50>
 8048ec1:	e8 11 03 00 00       	call   80491d7 <explode_bomb>

 8048ec6:	83 c3 01             	add    $0x1,%ebx //ebx+=1
 8048ec9:	83 fb 05             	cmp    $0x5,%ebx //if (5 <= ebx) 跳转，否则顺序执行
 8048ecc:	7e e9                	jle    8048eb7 <phase_6+0x41>

 8048ece:	66 90                	xchg   %ax,%ax //交换16位寄存器中的内容
 8048ed0:	eb c3                	jmp    8048e95 <phase_6+0x1f>

 8048ed2:	8b 52 08             	mov    0x8(%edx),%edx // edx+8赋给edx
 8048ed5:	83 c0 01             	add    $0x1,%eax //eax += 1
 8048ed8:	39 c8             p->  	cmp    %ecx,%eax //if (ecx - eax != 0) 跳转，否则顺序执行
 8048eda:	75 f6                	jne    8048ed2 <phase_6+0x5c>
 8048edc:	eb 05                	jmp    8048ee3 <phase_6+0x6d>

 8048ede:	ba 3c c1 04 08       	mov    $0x804c13c,%edx
                                       //0x804c13c中的内容赋给edx
                                       //用GDB查看发现它是链表表头的首地址，推知第六关是对链表进行操作
 8048ee3:	89 54 b5 e0          	mov    %edx,-0x20(%ebp,%esi,4)
                                       //（ebp-32）+ sei*4 = edx
 8048ee7:	83 c3 01             	add    $0x1,%ebx //ebx+=1
 8048eea:	83 fb 06             	cmp    $0x6,%ebx //ebx = 6跳转，否则顺序执行
 8048eed:	74 17                	je     8048f06 <phase_6+0x90>

 8048eef:	89 de                	mov    %ebx,%esi //ebx赋给esi
 8048ef1:	8b 4c 9d c8          	mov    -0x38(%ebp,%ebx,4),%ecx 
                                       //ecx=(ebp-64)+4*ebx
 8048ef5:	83 f9 01             	cmp    $0x1,%ecx
                                       //if(1<=ecx)跳转，否则顺序执行
 8048ef8:	7e e4                	jle    8048ede <phase_6+0x68>

 8048efa:	b8 01 00 00 00       	mov    $0x1,%eax // eax=1
 8048eff:	ba 3c c1 04 08       	mov    $0x804c13c,%edx 
                                       //0x804c13c中的值赋给edx
                                       //用GDB查看发现它是链表表头的首地址，推知第六关是对链表进行操作
 8048f04:	eb cc                	jmp    8048ed2 <phase_6+0x5c>

 8048f06:	8b 5d e0             	mov    -0x20(%ebp),%ebx 
                                       //ebp-32赋给ebx
 8048f09:	8d 45 e4             	lea    -0x1c(%ebp),%eax
                                       //ebp-28赋给eax
 8048f0c:	8d 75 f8             	lea    -0x8(%ebp),%esi
                                       //ebp-8赋给esi
 8048f0f:	89 d9                	mov    %ebx,%ecx  
                                       //ebx赋给ecx
 8048f11:	8b 10                	mov    (%eax),%edx
                                       //edx = eax中的内容
 8048f13:	89 51 08             	mov    %edx,0x8(%ecx) 
                                       //edx赋给ecx+8
 8048f16:	83 c0 04             	add    $0x4,%eax //eax += 4
 8048f19:	39 f0                	cmp    %esi,%eax 
                                       // esi = eax跳转，否则顺序执行
 8048f1b:	74 04                	je     8048f21 <phase_6+0xab>

 8048f1d:	89 d1                	mov    %edx,%ecx//edx赋给ecx
 8048f1f:	eb f0                	jmp    8048f11 <phase_6+0x9b>
 8048f21:	c7 42 08 00 00 00 00 	movl   $0x0,0x8(%edx)
                                       //edx+8=0
 8048f28:	be 05 00 00 00       	mov    $0x5,%esi
                                       //esi=5
 8048f2d:	8b 43 08             	mov    0x8(%ebx),%eax
                                       //ebx+8赋给eax
 8048f30:	8b 00                	mov    (%eax),%eax
                                       //eax = eax中的内容
 8048f32:	39 03                	cmp    %eax,(%ebx)
                                       // eax <= ebx中的内容 跳转，否则爆炸
 8048f34:	7e 05                	jle    8048f3b <phase_6+0xc5>
 8048f36:	e8 9c 02 00 00       	call   80491d7 <explode_bomb>

 8048f3b:	8b 5b 08             	mov    0x8(%ebx),%ebx
                                       //ebx+8 赋给ebx
 8048f3e:	83 ee 01             	sub    $0x1,%esi //esi-1 > 0跳回到循环中
 8048f41:	75 ea                	jne    8048f2d <phase_6+0xb7>
 8048f43:	83 c4 40             	add    $0x40,%esp
 8048f46:	5b                   	pop    %ebx
 8048f47:	5e                   	pop    %esi
 8048f48:	5d                   	pop    %ebp
 8048f49:	c3                   	ret    
 ```
 将上面分析得  
 用GDB查看链表中的内容是（链表首地址是0x804c13c,下一个链表地址是上一个链表的地址+12）  
[![qvZ8Bt.png](https://s1.ax1x.com/2022/04/06/qvZ8Bt.png)](https://imgtu.com/i/qvZ8Bt)

> 1 0x146
> 2 0x2dc
> 3 0x2f7
> 4 0x0a3
> 5 0x26c
> 6 0x225

从小到大排序得  
> 4 0x0a3
> 1 0x14f
> 6 0x225
> 5 0x26c
> 2 0x2dc
> 3 0x2fc

故phase_6得密码为  
4 1 6 5 2 3  



#### secret_phase
由于老师、助教提供的实验、资料，他们在介绍实验的PPT里说明了——还有这个`secret_phase`关卡，也说明了——进入第七关需要在第四关后面输入一个字符串。
所以减少了的工作，但是我们还是要明白为什么是这样。  （还是实验前我并没有认真看PPT或者是我忘记了提示过还有个隐藏关卡，所以做到phase_6时，看着对应的汇编代码发现下面还有个`secret_phase`）  

当我们发现了还有个隐藏关卡时，发现了第一个问题——怎么进入`secret_phase`，毕竟输入完前六关的密码时，炸弹就全部解开了，没给我们输入什么的机会。所以该怎么进入呢。  

前六个都是在Main函数中顺序排好的，那我们就去看看main函数对应汇编代码会不会有线索。然而并没有发现与`secret_phase`有关的内容，但是发现每个phase_x后都有一个`phase_defused`。
```text
call   xxxxxxx <phase_x>
call   xxxxxxx <phase_defused>
```
那么能否进入隐藏关卡是否与其有关呢。于是在查看`phase_defused`的汇编代码，发现`80493c9:	e8 cf fb ff ff       	call   8048f9d <secret_phase>`，这不就出现了嘛，那就看看里面是什么意思。
```text
0804934f <phase_defused>:
 804934f:	55                   	push   %ebp
 8049350:	89 e5                	mov    %esp,%ebp
 8049352:	81 ec 88 00 00 00    	sub    $0x88,%esp
                                       //esp-128开栈
 8049358:	65 a1 14 00 00 00    	mov    %gs:0x14,%eax
 ```
 这意味着从地址gs：0x14的内存中读取4个字节到eax。 gs是一个段寄存器。最有可能的是线程本地存储(AKA TLS)通过该寄存器引用。(百度的，我不懂，搜索了很多，还是没怎么看明白%gs的意思，故而找了一个感觉对的)
 ```text
 804935e:	89 45 f4             	mov    %eax,-0xc(%ebp) //ebp-12 = eax
 8049361:	31 c0                	xor    %eax,%eax //eax异或运算
 8049363:	83 3d c8 c3 04 08 06 	cmpl   $0x6,0x804c3c8 
                                       // 0x804c3c8 与 6比较
                                       // 经GDB查看后发现0x804c3c8指向<num_input_strings>:"\005"
                                       // 其中"\005"是调试时处于phase_5得到的值x
                                       // 在不同得phase阶段查此地址会得到不同的"\00x",x取决于第几个
                                       // 所以 这一行是判断密码输入的次数是否 = 6
 804936a:	75 6e                	jne    80493da <phase_defused+0x8b>
 804936c:	8d 45 a4             	lea    -0x5c(%ebp),%eax 
 804936f:	89 44 24 10          	mov    %eax,0x10(%esp) 
                                                       // esp+16 = ebp - 92
 8049373:	8d 45 a0             	lea    -0x60(%ebp),%eax
 8049376:	89 44 24 0c          	mov    %eax,0xc(%esp) 
                                                       // esp+12 = ebp- 96
 804937a:	8d 45 9c             	lea    -0x64(%ebp),%eax
 804937d:	89 44 24 08          	mov    %eax,0x8(%esp) 
                                                      // esp+8 = ebp -100
                                       
 8049381:	c7 44 24 04 b1 a4 04 	movl   $0x804a4b1,0x4(%esp)
                                       // GDB查看得 "%d %d %s"
                                       // 表示需要如此输入，经提示，我们知道了在第四关以这样得格式输入。
 8049388:	08 
 8049389:	c7 04 24 d0 c4 04 08 	movl   $0x804c4d0,(%esp)
                                       // 得 <input_strings + 240> : "6 6" (有点熟悉)
                                       
 8049390:	e8 cb f4 ff ff       	call   8048860 <__isoc99_sscanf@plt>
 8049395:	83 f8 03             	cmp    $0x3,%eax 
                                       // 如果返回的输入个数不等于三跳转至80493ce，否则顺序执行
 8049398:	75 34                	jne    80493ce <phase_defused+0x7f>
 804939a:	c7 44 24 04 ba a4 04 	movl   $0x804a4ba,0x4(%esp)
                                       // 易知地址中为"DrEvil"
                                       // 不会是进入的密码呢，再往下看看
 80493a1:	08 
 80493a2:	8d 45 a4             	lea    -0x5c(%ebp),%eax
 80493a5:	89 04 24             	mov    %eax,(%esp) //esp=ebp-92
 80493a8:	e8 15 fd ff ff       	call   80490c2 <strings_not_equal>
                                       // 字符比较
 80493ad:	85 c0                	test   %eax,%eax //应该是判断输入的字符是否为"DrEvil"
 80493af:	75 1d                	jne    80493ce <phase_defused+0x7f>
 80493b1:	c7 04 24 80 a3 04 08 	movl   $0x804a380,(%esp) 
                                       
 80493b8:	e8 33 f4 ff ff       	call   80487f0 <puts@plt>
 80493bd:	c7 04 24 a8 a3 04 08 	movl   $0x804a3a8,(%esp)

 80493c4:	e8 27 f4 ff ff       	call   80487f0 <puts@plt>
 80493c9:	e8 cf fb ff ff       	call   8048f9d <secret_phase>
                                       //以上就是发现secret_phase需要进行得操作
 80493ce:	c7 04 24 e0 a3 04 08 	movl   $0x804a3e0,(%esp)
 80493d5:	e8 16 f4 ff ff       	call   80487f0 <puts@plt>
 80493da:	8b 45 f4             	mov    -0xc(%ebp),%eax
 80493dd:	65 33 05 14 00 00 00 	xor    %gs:0x14,%eax
 80493e4:	74 05                	je     80493eb <phase_defused+0x9c>
 80493e6:	e8 d5 f3 ff ff       	call   80487c0 <__stack_chk_fail@plt>
 80493eb:	c9                   	leave  
 80493ec:	8d 74 26 00          	lea    0x0(%esi,%eiz,1),%esi
 80493f0:	c3                   	ret    
 80493f1:	66 90                	xchg   %ax,%ax
 80493f3:	66 90                	xchg   %ax,%ax
 80493f5:	66 90                	xchg   %ax,%ax
 80493f7:	66 90                	xchg   %ax,%ax
 80493f9:	66 90                	xchg   %ax,%ax
 80493fb:	66 90                	xchg   %ax,%ax
 80493fd:	66 90                	xchg   %ax,%ax
 80493ff:	90                   	nop
```
上面几个地址中存在的值如图  
[![qvZAn1.png](https://s1.ax1x.com/2022/04/06/qvZAn1.png)](https://imgtu.com/i/qvZAn1)

经分析可知，secret_phase的进入需要我们成功解除了前六个炸弹后并在第四关以"%d %d %s"的格式输入"6 6 DrEvil"。

```text
08048f9d <secret_phase>:
 8048f9d:	55                   	push   %ebp
 8048f9e:	89 e5                	mov    %esp,%ebp
 8048fa0:	53                   	push   %ebx
 8048fa1:	83 ec 14             	sub    $0x14,%esp//开栈
 8048fa4:	e8 a8 02 00 00       	call   8049251 <read_line>
 8048fa9:	c7 44 24 08 0a 00 00 	movl   $0xa,0x8(%esp) //esp+8 = 10
 8048fb0:	00 
 8048fb1:	c7 44 24 04 00 00 00 	movl   $0x0,0x4(%esp) //esp+4=0
 8048fb8:	00 
 8048fb9:	89 04 24             	mov    %eax,(%esp) 
 8048fbc:	e8 0f f9 ff ff       	call   80488d0 <strtol@plt>
 8048fc1:	89 c3                	mov    %eax,%ebx
 8048fc3:	8d 40 ff             	lea    -0x1(%eax),%eax
 8048fc6:	3d e8 03 00 00       	cmp    $0x3e8,%eax //if 0x3e8 <= eax,跳转，否则爆炸
 8048fcb:	76 05                	jbe    8048fd2 <secret_phase+0x35>
 8048fcd:	e8 05 02 00 00       	call   80491d7 <explode_bomb>

 8048fd2:	89 5c 24 04          	mov    %ebx,0x4(%esp)
                                       //ebx中值为输入的参数
 8048fd6:	c7 04 24 88 c0 04 08 	movl   $0x804c088,(%esp)
                                       //进入递归的参数
 8048fdd:	e8 68 ff ff ff       	call   8048f4a <fun7>
 8048fe2:	83 f8 05             	cmp    $0x5,%eax 
 8048fe5:	74 05                	je     8048fec <secret_phase+0x4f>
 8048fe7:	e8 eb 01 00 00       	call   80491d7 <explode_bomb>
                                       //只有当递归的返回值等于5时，不引爆炸弹
 8048fec:	c7 04 24 20 a3 04 08 	movl   $0x804a320,(%esp)
 8048ff3:	e8 f8 f7 ff ff       	call   80487f0 <puts@plt>
 8048ff8:	e8 52 03 00 00       	call   804934f <phase_defused>
 8048ffd:	83 c4 14             	add    $0x14,%esp
 8049000:	5b                   	pop    %ebx
 8049001:	5d                   	pop    %ebp
 8049002:	c3                   	ret    
 8049003:	66 90                	xchg   %ax,%ax
 8049005:	66 90                	xchg   %ax,%ax
 8049007:	66 90                	xchg   %ax,%ax
 8049009:	66 90                	xchg   %ax,%ax
 804900b:	66 90                	xchg   %ax,%ax
 804900d:	66 90                	xchg   %ax,%ax
 804900f:	90                   	nop
 ```
分析得secret_phase需要我们输入一个值，该值与0x804c088中的值一起进入递归函数，需使得递归返回值 = 5。  

分析Func7 ：

 ```text
08048f4a <fun7>:
 8048f4a:	55                   	push   %ebp
 8048f4b:	89 e5                	mov    %esp,%ebp
 8048f4d:	53                   	push   %ebx
 8048f4e:	83 ec 14             	sub    $0x14,%esp
 8048f51:	8b 55 08             	mov    0x8(%ebp),%edx //最开始是0x804c088中的值，记作参数one
 8048f54:	8b 4d 0c             	mov    0xc(%ebp),%ecx //最开始是我们需要的参数，记作参数two
 8048f57:	85 d2                	test   %edx,%edx //edx为0 返回-1
 8048f59:	74 37                	je     8048f92 <fun7+0x48>
------------------
 8048f5b:	8b 1a                	mov    (%edx),%ebx //ebx = *edx
 8048f5d:	39 cb                	cmp    %ecx,%ebx //if ecx <= ebx 跳转
 8048f5f:	7e 13                	jle    8048f74 <fun7+0x2a> 
 8048f61:	89 4c 24 04          	mov    %ecx,0x4(%esp)
 8048f65:	8b 42 04             	mov    0x4(%edx),%eax
 8048f68:	89 04 24             	mov    %eax,(%esp)//(edx+4, ecx)两个参数进入递归
 8048f6b:	e8 da ff ff ff       	call   8048f4a <fun7>
 8048f70:	01 c0                	add    %eax,%eax//返回值=递归返回值*2
 8048f72:	eb 23                	jmp    8048f97 <fun7+0x4d>
 ------------------
 8048f74:	b8 00 00 00 00       	mov    $0x0,%eax //eax = 0
 8048f79:	39 cb                	cmp    %ecx,%ebx 
 8048f7b:	74 1a                	je     8048f97 <fun7+0x4d> 
                                       //if ecx == ebx 结束递归
 8048f7d:	89 4c 24 04          	mov    %ecx,0x4(%esp)
 8048f81:	8b 42 08             	mov    0x8(%edx),%eax
 8048f84:	89 04 24             	mov    %eax,(%esp) //(*(edx+8),ecx)两个参数进入递归
 8048f87:	e8 be ff ff ff       	call   8048f4a <fun7>
 8048f8c:	8d 44 00 01          	lea    0x1(%eax,%eax,1),%eax
                                       // 返回值 = 递归返回值*2 + 1
 8048f90:	eb 05                	jmp    8048f97 <fun7+0x4d>
--------------------
 8048f92:	b8 ff ff ff ff       	mov    $0xffffffff,%eax
 8048f97:	83 c4 14             	add    $0x14,%esp
 8048f9a:	5b                   	pop    %ebx
 8048f9b:	5d                   	pop    %ebp
 8048f9c:	c3                   	ret    
```
进行一波困难的逆向得Func7的C语言代码:  
```c
int func7(int *a, int b)
{
    if (a == NULL)
      return -1;
    
    int result = 0;
    if (*a > b)
    if (*a == b)
        return 0;
      else
      {
        result = func7(*(a + 8), b);
        return 2 * result + 1;
      }

    else 
    {
      result = func7(*(a + 4), b);  
      return 2 * result;
    }
}
```
由于最后的返回值是5，根据函数的结构可以想到这样的结构：
> a \* 2 + 1 = 5 ————> b \* 2 = a ————> c \* 2 + 1 = b ————> c = 0  

即*a、b的关系为  
> \*a < b ————> \*a > b ————> \*a < b————> \*a == b

所以一共递归
> \*a – b > 0
> \*a – b < 0
> \*a – b > 0
> \*a – b == 0


用GDB查看`0x804c088`后得到
1. `0x804c088 = 0x24`，之后在`*a - b < 0 (0x24 – b < 0)`的分支中`*(a + 8)= 0x804c090`，所以`func7(0x804c090, b)`。
2. `*0x804c090 = 0x32`，`*a - b > 0 (0x32 - b > 0)`，递归`fun7(*(0x804c090 + 4) = 0x804c094, b)`。
3. `*0x804c094 = 0x2d`，`*a - b < 0 (0x2d - b < 0)`，`fun7(*(0x804c094 + 8) = 0x804c09c, b)`。
4. `*0x804c09c = 0x2f`，`*a – b == 0 (0x2f – b == 0)`，所以`b = 0x2f`，递归返回。

得到3个不等式和一个等式：

1. `0x24 – 0x2f < 0`
2. `0x32 – 0x2f > 0`
3. `0x2d – 0x2f < 0`
4. `b = 0x2f`
转为十进制 b = 47，故隐藏关卡密码为47。

淦！！！！！！！  

以上是正常情况下应该得出理解答案的结果，但是事实并不如我想象。操作后并没有得到答案。但是答案确实是47。  
通过不断的查找，发现存着47的地址在老后面了，完全不对啊。 淦，问题真多。

### 结果 
[![qvVXmq.md.png](https://s1.ax1x.com/2022/04/06/qvVXmq.md.png)](https://imgtu.com/i/qvVXmq)