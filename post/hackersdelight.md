---
layout: default
title: Hacker's Delight
description: Notes
---

# Brief Introduction

"[Hacker's Delight](https://book.douban.com/subject/10756419/)" is one of the most influential works in the field of algorithms. Together with the Doctor [Donald Knuth](https://www-cs-faculty.stanford.edu/~knuth/index.html)'s "[The Art of Computer Programming](https://www-cs-faculty.stanford.edu/~knuth/books.html)", it is hailed as a computer work worth reading for all programmers. The book summarizes a large number of efficient, elegant and wonderful algorithms, and analyzes the principles behind them from a mathematical perspective. The art of algorithms and the wisdom of mathematics are best embodied in this book.

# Preface to the 1st edition



# Preface written by the author Henry S. Warren, Jr.

*"print itself.c"*

```c
#include <stdio.h>
int main() {
    char * p="#include <stdio.h> int main() {char * p=%c%s%c; printf(13,14,p,20); return 0;}%c";
    printf(13,14,p,20);
    return 0;
}
```



# table of Contents

* Preface to the 1st edition
* Preface written by the author
* Chapter 1 Overview
  * 1.1 Notation
  * 1.2 Instruction set and Execution time model
  * 1.3 Exercises

* Chapter 2 Basic Knowledge
  * 2.1 Operate the rightmost bit
    * 2.1.1 Corollary to De Morgan's Law
    * 2.1.2 Computability test from right to left
    * 2.1.3 New usage of bit manipulation
  * 2.2 Combine addition and subtraction with logical operations
  * 2.3 Inequalities in logic and arithmetic expressions

# Chapter 1 Overview

## 1.1 Notation

假设机器码字长n位，左侧最高1位为符号位，右边剩下的(n-1)位全是数值位。

**这里只讨论带符号的整数(signed integer).**

### 原码

用二进制数来表示真值的绝对值，8位字长的机器数有7位数值位，符号由左边最高1位决定，例如：

*7位的二进制数最大能表示到2^7-1 = 127 = 111 1111，能表示包括0在内共128个数。*

[+122]原 = 0111 1010

[-122]原  = 1111 1010

[-56]原    = 1011 1000

> 零和正数的原码、反码、补码相同

### 反码

正数：和原码同

负数：在原码的基础上（符号位不变）每一数值位取反，例如：

[+122]反 = 0111 1010

[-122]反  = 1000 0101

[-56]反    = 1100 0111

### 补码

正数：和原码同

负数：在反码的基础末位上+1（符号位不变，若进位溢出取余），例如：

[+122]补 = 0111 1010

[-122]补  = 1000 0110

[-56]补    = 1100 1000

> Tips: 如何快速转换原码和补码？
>
> 只需从右往左数，出现第一个'1'后，左边其余所有数值位取反操作即可

### 移码

在补码的基础上（数值位不动）符号位取反，例如：

[+122]移 = 1111 1010

[-122]移  = 0000 0110

[-56]移    = 0100 1000



> 补码表示0只有一种"0000 0000"

[back](../../)
