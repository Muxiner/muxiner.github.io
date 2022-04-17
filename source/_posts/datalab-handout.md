---
title: 计算机系统基础实验之datalab-handout
date: 2020-11-10 20:13:04
categories: 实验记录
tags: 
- 计算机系统
- 位计算
- Csapp
- Blog
---

## 实验开始
下载 `lab1-handout.tar`
>(可由老师提供，或者在 `http://csapp.cs.cmu.edu/3e/labs.html` [csapp](http://csapp.cs.cmu.edu/3e/labs.html)下载,获取方法是点击实验后面的 `Self-Study Handout`)，存放在下载目录
<!--more-->
点击左侧 `dock` 图标，键入 `term` ，打开终端
+ `cd ~`    进入主目录      键入 
+ `ls` 查看是否有下载文件
+ `tar vxf lab1-handout.tar`   解压代码框架  
+ `cd lab1-handout`
+ `ls`    显示当前目录文件
+ `make`   编译生成可执行文件
+ `ls`  看看多了几个文件
+ `./btest` 试试运行   

本实验是默认在 32 位机上进行测试。

## 实验分析
### 1. bitBor函数
```c
/* 
 * bitXor - x^y using only ~ and & 
 *   Example: bitXor(4, 5) = 1
 *   Legal ops: ~ &
 *   Max ops: 14
 *   Rating: 1
 */
int bitXor(int x, int y) {
  return 2;
}
```
+ 使用 `~` 和 `&` 实现 `x^y` 

法1：  
+ 题意：用 `~` 和 `&` 运算符实现 `Xor` 运算符
+ 思路：我们知道 `Xor` 运算符是对每一个位，相同的话返回 `0` ，不同的话返回 `1` ，即 `((~x)&y)|(x&(~y))` 。但不能使用 `|` 运算，故采用德摩根律将或运算转为与运算。


法2：

+ 利用《数字逻辑》的知识：异或运算 德摩根律
> x ^ y = (x & \~y) | (\~x & y)  
> = \~((x & \~y) | (\~x & y))  
> = \~(\~(x & \~y) & \~(\~x & y))  D

```c
int bitXor(int x, int y) {
  return ~(~(x & ~y) & ~(~x & y));
}
```

### 2. tmim函数  

```c
/* 
 * tmin - return minimum two's complement integer 
 *   Legal ops: ! ~ & ^ | + << >>
 *   Max ops: 4
 *   Rating: 1
 */
int tmin(void) {
  return 2;
}
```
* 题意：输出反码下的最小值
* 思路：直接由定义得最小值  

```c
int tmin(void) {
  return 1 << 31;
}
```
### 3. isTmax函数  
```c
/*
 * isTmax - returns 1 if x is the maximum, two's complement number,
 *     and 0 otherwise 
 *   Legal ops: ! ~ & ^ | +
 *   Max ops: 10
 *   Rating: 1
 */
int isTmax(int x) {
  return 2;
}
```
判断一个数是否为有符号数的最大值 `Tmax` ，即  
> 0x7FFFFFFF   16进制  
> 2147483647   10进制  
> 0111 1111 1111 1111 1111 1111 1111 1111    2进制(32位系统)

> Tmax满足:  Tmax = \~(Tmax + 1)    Tmax ^ (\~(Tmax + 1)) = 0  
`0xFFFFFFFF` 也满足上述关系，但 `0xFFFFFFFF + 1` 为 `0`, 所以要排除这种情况。  

```c
int inTmax(int x) {
    return !(x ^ ~(x + 1)) & !!(x + 1); 
}
```

### 4. allOddBits函数  

```c
/* 
 * allOddBits - return 1 if all odd-numbered bits in word set to 1
 *   where bits are numbered from 0 (least significant) to 31 (most significant)
 *   Examples allOddBits(0xFFFFFFFD) = 0, allOddBits(0xAAAAAAAA) = 1
 *   Legal ops: ! ~ & ^ | + << >>
 *   Max ops: 12
 *   Rating: 2
 */
int allOddBits(int x) {
  return 2;
}
```
判断一个二进制数奇数位是否全为 `1`  
思路:  
若 `x` 奇数位全为 `1`，则 `~x` 的奇数位全为 `0` ，则 `~x & 0xaaaaaaaa` 使得全部为 `0`。
```
int allOddBits(int x) {
  return !(~x & 0xaaaaaaaa);
}
```

### 5. negate函数

```c
/* 
 * negate - return -x 
 *   Example: negate(1) = -1.
 *   Legal ops: ! ~ & ^ | + << >>
 *   Max ops: 5
 *   Rating: 2
 */
int negate(int x) {
  return 2;
}
```

求一个数的相反数。
思路: `-x = ~x + 1`  (取反加一)

```c
int negate(int x) {
  return ~x + 1;
}
```

### 6. isAsciiDigit函数

```c
/* 
 * isAsciiDigit - return 1 if 0x30 <= x <= 0x39 (ASCII codes for characters '0' to '9')
 *   Example: isAsciiDigit(0x35) = 1.
 *            isAsciiDigit(0x3a) = 0.
 *            isAsciiDigit(0x05) = 0.
 *   Legal ops: ! ~ & ^ | + << >>
 *   Max ops: 15
 *   Rating: 3
 */
int isAsciiDigit(int x) {
  return 2;
}
```
 
判断一个数字是否在 `0x30` 到 `0x39` 范围之内。  
思路:  
判断差值是否大于等于 `x - y >= 0` 即 `取符号位且取逻辑反`  
> !(x + (~y + 1) >> 31)  
> x + (~y + 1) >> 31   取符号位


```c
int isAsciiDigit(int x) {
  return !(x + (~0x30 + 1) >> 31) & !(0x39 + (~x + 1) >> 31);
}  
```

### 7. conditional函数

```c
/* 
 * conditional - same as x ? y : z 
 *   Example: conditional(2,4,5) = 4
 *   Legal ops: ! ~ & ^ | + << >>
 *   Max ops: 16
 *   Rating: 3
 */
int conditional(int x, int y, int z) {
  return 2;
}
```

题意：实现一个三目运算符 `x ? y : z`  
思路：用 `!` 判断 `x` 的真假；`x ? y : z` 的关系转换为 `(a & y) | (b & z)` ，当 `x` 为 `0` 时，`a` 为 `0x0` ，`b` 为 `0xffffffff` ；当 `x` 非零时，`a` 为`0xffffffff` , `b` 为 `0x0` 。即  
> 0x0 & 0xaaa = 0  
> 0xffffffff & 0xaaa = 0xaaa   

所以得使得 `a = !x + 0xffffffff` , `b = !!x + 0xffffffff` ，这样 `a` `b` 就会要么是 `0x0` `0xffffffff`。  

```c
int conditional(int x, int y, int z) {
  return ((!x + 0xffffffff)& y) | (z & (!!x + 0xffffffff));
}
```

### 8. isLessOrEqual函数

```c
/* 
 * isLessOrEqual - if x <= y  then return 1, else return 0 
 *   Example: isLessOrEqual(4,5) = 1.
 *   Legal ops: ! ~ & ^ | + << >>
 *   Max ops: 24
 *   Rating: 3
 */
int isLessOrEqual(int x, int y) {
  return 2;
}
```

题意：若 `x <= y` ，则返回 `1` ，反之返回 `0`。  
思路：直接用 `y-x` 可能会超出 `int` 的表示范围，故而：

> 1.在x与y同号的情况下转换为p=y-x>=0，然后对p符号位进行(p>>31)&1操作，符号位为0则返回1，符号位1则返回0；  
> 2.x，y异号时，只要x>=0，就要返回0，否则返回1，由(x>>31)&1能达到该效果；  
> 3.c=a+b可作为x，y同号异号的判断。


```c
int isLessOrEqual(int x, int y) {
  int sign_bit_x = x >> 31;
  int sign_bit_y = y >> 31;
  int sign_bit_xy = sign_bit_x + sign_bit_y;
  int sign_bit_subyx = ((y + ~x + 1) >> 31) & 1;
  return (sign_bit_xy & (sign_bit_x & 1)) | ((~sign_bit_xy) & !sign_bit_subyx);
}
```

### 9. logicalNeg函数  

```c
/* 
 * logicalNeg - implement the ! operator, using all of 
 *              the legal operators except !
 *   Examples: logicalNeg(3) = 0, logicalNeg(0) = 1
 *   Legal ops: ~ & ^ | + << >>
 *   Max ops: 12
 *   Rating: 4 
 */
int logicalNeg(int x) {
  return 2;
} 
```

题意：计算 `!x` ：当 `x = 0` 时返回 `1`；当 `x ≠ 0` 时返回 `0`。  
思路：`0`和`Tmin`的补码都是其本身，而其他数的补码则是符号位相反。所以要区别`0`和`Tmin`的区别  
> 0x0000 0000    
> 0x8000 0000    

即最高位不同，故用算数右移取符号位判断。

```c
int logicalNeg(int x) {
  return ((~x & ~(~x + 1)) >> 31) & 1;
}
```

### 10. haoManyBits函数  

```c
/* howManyBits - return the minimum number of bits required to represent x in
 *             two's complement
 *  Examples: howManyBits(12) = 5
 *            howManyBits(298) = 10
 *            howManyBits(-5) = 4
 *            howManyBits(0)  = 1
 *            howManyBits(-1) = 1
 *            howManyBits(0x80000000) = 32
 *  Legal ops: ! ~ & ^ | + << >>
 *  Max ops: 90
 *  Rating: 4
 */
int howManyBits(int x) {
  return 2;
}
```

题意：  给一个数字x,求出要表示出x需要的最少的位数。  

思路：  使用二分法。  

 若`x`是负数，那么对其取反，因为所需要的位数是一样的。  
> 即  x = (((x >> 31) & ~x) | ((~!(x >> 31) + 1) & x)) 

然后是用二分法，先向右位移16位，即`half_x = x >> 16`，再判断`half_x`是否为`0`，即`!!half_x`。若为`0`，则`x`的最高位数为`16`；反之，其最低位数为`16`。依此类推，继续对其右移`8`、`4`、`2`、`1`位，得到`bit8`, `bit4`, `bit2`, `bit1`,分别表示一分为二后其中的一半是否存在，而另一半继续循环直至1，这时还剩下`x`，最后还需要再加上符号位`0`。

```c
int howManyBits(int x) {
  x = (((x >> 31) & ~x) | ((~!(x >> 31) + 1) & x));
  int bit16, bit8, bit4, bit2, bit1;
  int half_x;
  
  half_x = x >> 16;
  bit16 = !!half_x << 4;
  x = x >> bit16;

  half_x = x >> 8;
  bit8 = !!half_x << 3;
  x = x >> bit8;

  half_x = x >> 4;
  bit4 = !!half_x << 2;
  x = x >> bit4;

  half_x = x >> 2;
  bit2 = !!half_x << 1;
  x = x >> bit2;

  half_x = x >> 1;
  bit1 = !!half_x << 0;
  x = x >> bit1;
  
  return bit16 + bit8 + bit4 + bit2 + bit1 + 1 + x;
}
```

### 11. floatScale2函数

```c
//float
/* 
 * floatScale2 - Return bit-level equivalent of expression 2*f for
 *   floating point argument f.
 *   Both the argument and result are passed as unsigned int's, but
 *   they are to be interpreted as the bit-level representation of
 *   single-precision floating point values.
 *   When argument is NaN, return argument
 *   Legal ops: Any integer/unsigned operations incl. ||, &&. also if, while
 *   Max ops: 30
 *   Rating: 4
 */
unsigned floatScale2(unsigned uf) {
  return 2;  
}
```
题意：  给出一个无符号整数`x`，将其看作一个浮点数，返回此数的两倍`x*2`。  
思路： 取出符号`s`、阶码`exp`、尾数`frac`   
> sgn = uf & 0x80000000  
> exp = uf & 0x7F800000  
> frac = uf & 0x007FFFFF  

若`exp`为0，则是非规格，直接左移。  
若`exp`不是`0x7F80 0000`，即有效，则直接阶码加一。 

```c
unsigned floatScale2(unsigned uf) {
  unsigned f = uf;
  unsigned sgn = uf & 0x80000000;//符号位
  unsigned exp = uf & 0x7F800000;//阶码
  unsigned frac = uf & 0x007FFFFF;//位数
  if (exp == 0)  
    f = (frac << 1) | sgn;
  else if (exp != 0x7F800000) 
     f = f + 0x00800000;//阶码+1
  return f;   
}
```

### 12. floatFloat2Int函数

```c
/* 
 * floatFloat2Int - Return bit-level equivalent of expression (int) f
 *   for floating point argument f.
 *   Argument is passed as unsigned int, but
 *   it is to be interpreted as the bit-level representation of a
 *   single-precision floating point value.
 *   Anything out of range (including NaN and infinity) should return
 *   0x80000000u.
 *   Legal ops: Any integer/unsigned operations incl. ||, &&. also if, while
 *   Max ops: 30
 *   Rating: 4
 */
int floatFloat2Int(unsigned uf) {
 return 2;
}
```

题意：给出一个无符号整数x，将其看作一个浮点数，实现一个(int)x的功能。  

思路：

主要是思考上下界溢出的问题。

下界溢出的临界是`bin(x) = 0 0111 1111 0000 0000 0000 0000 0000 000`，此时`s = 0`，`exp = 127`，`frac = 0`。表示的数字刚好是`1.0`。小于这个数直接返回`0`。

上界溢出的条件是`bin(x) = 0 1001 1101 0000 0000 0000 0000 0000 000`，此时`s = 0`，`exp = 127 + 31`，`frac = 0`。表示的数是`1.0*2**32`，也就是`TMax`，大于这个数就直接返回`TMax`。

其他数字考虑`exp = 127 + 23`这个临界。如果大于这个数，需要将`frac`右移。如果小于这个数，需要将`frac`左移。   

法一：

```c
int floatFloat2Int(unsigned uf)
{
  int s = (uf >> 31) & 1;
  int exp = ((uf >> 23) & 0xFF) - 127; //exp的真实值
  int frac = (uf & 0x007FFFFF) | 0x00800000;
  int tar = 0;
  if (s) s = -1;
  else s = 1;
  if (exp > 31)
    return 0x80000000;
  if (exp < 0)
    return 0;
  if (exp > 23)
    tar = s * (frac << (exp - 23));
  else if (exp < 23)
    tar = s * (frac >> (23 - exp));
  return tar;
}
```

法二：  

```c
int floatFloat2Int(unsigned uf) 
{
    unsigned INF = 1<<31;   // INF = MaxInt+1
    int e = (uf>>23) & 0xff;// 阶码
    int s = (uf>>31) & 1;   // 符号位
    if (uf == 0) return 0;
    uf <<= 8;       // 左移保留至阶码最后1位
    uf |= 1<<31;    // 阶码最后一位设为1
    uf >>= 8;       // 高八位全0
    e -= 127;       // 阶数
    if ((uf & 0x7f80000) == 0x7f80000 || e >= 32)
        return INF; // 超过int范围返回INF
    if (e < 0) // 小数返回0
        return 0;
    if (e <= 22) // 位数小于等于22位，尾数位右移
        uf >>= 23-e;
    else 
        uf <<= e-23; // 尾数大于22位，尾数为左移
    if (s) 
        uf = ~uf + 1;// 若原uf为负数，则对此处的正数uf取反加1得其相反数
    return uf;
}
```

### 13. floatPower2函数

```c
/* 
 * floatPower2 - Return bit-level equivalent of the expression 2.0^x
 *   (2.0 raised to the power x) for any 32-bit integer x.
 *
 *   The unsigned value that is returned should have the identical bit
 *   representation as the single-precision floating-point number 2.0^x.
 *   If the result is too small to be represented as a denorm, return
 *   0. If too large, return +INF.
 * 
 *   Legal ops: Any integer/unsigned operations incl. ||, &&. Also if, while 
 *   Max ops: 30 
 *   Rating: 4
 */
unsigned floatPower2(int x) {
return 2;
}
```

题意：  给出一个无符号整数x，将其看作一个浮点数，返回2**x。   

思路：  先得到阶码`exp = x + 127`，然后考虑临界值：  

`bin(x) = 0 00000000 00000000000000000000001`，此数是`2**((-126)+(-23))`,   
即`exp = 0`时情况；  

`bin(x) = 0 00000001 00000000000000000000000`，此数是`2**(-126)`，  
即`exp = 23`时情况；

`bin(x) = 0 11111111 00000000000000000000000` ，此数是`2**(128)`，  
即`exp = 255`时情况。


代码一：

```c
unsigned floatPower2(int x) {
  int exp = x + 0x7f;                          // x + 127

  if (exp < 0) 
  return 0;

  return exp < 0xff ? exp << 23 : 0x7f800000;  //0xff = 255
}
```

代码二：

```c
unsigned floatPower2(int x) {
    unsigned INF = 0xff << 23; // 阶码全1
    int e = 127 + x;    // 得到阶码
    if (exp < 0) // 阶数小于0直接返回0
        return 0;
    if (e >= 255) // 阶码>=255直接返回INF
        return INF;
    return e << 23;
    // 直接将阶码左移23位，尾数全0，规格化时尾数隐藏有1个1作为底数
}
```


### 实验结果  
[![qvVsYD.png](https://s1.ax1x.com/2022/04/06/qvVsYD.png)](https://imgtu.com/i/qvVsYD)

## 实验总结 
不愧是计算机系统的实验，实验内容和系统基础知识紧密联系，所接触到的不再是10进制数的计算，而是二进制及其反码补码，十六进制的计算，也不再仅仅是算术运算而更多的是逻辑、位的运算。由于知识储备的限制，一开始进行试验的时候实在是无从下手，思路上也受到了极大的限制，加之对于反码补码、有符号数无符号数、逻辑运算符、位运算符等等之类掌握的不深切，就觉得实验真的很难，当然本次实验的难度确实很大，实验内容也仅是datalab-handout的一部分，对其研究个八九不离十，十分有利与我对计算机系统学习，同时也要做好学习记录，以便日后回忆。  

tip： 
  这篇博客会在后续继续完善（在自己更加明白时），目前内容仅供参考。