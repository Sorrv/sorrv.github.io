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

<script src="https://unpkg.com/vanilla-back-to-top@7.2.1/dist/vanilla-back-to-top.min.js"></script>
<script>addBackToTop({
        backgroundColor: '#fff',
        innerHTML: 'Back to Top',
        textColor: '#333'
      })</script>
<div id="back-to-top" class="">Back to Top</div>
<style>
        #back-to-top {
          border: 1px solid #ccc;
          border-radius: 0;
          font-family: sans-serif;
          font-size: 14px;
          width: 100px;
          text-align: center;
          line-height: 30px;
          height: 30px;
        }
      </style>

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

## 7.3 Transposing a bit matrix

*转置 8X8 的位矩阵*

```c
void transpose8(unsigned char A[8], int m, int n, unsigned charB[8]) {
    unsigned long long x;
    int i;
    
    for (i = 0; i <= 7; i++)    // Load 8 bytes from the
        x = x << 8 | A[m*i];    // input array and pack
                                // them into x.
    
    x = x & 0xAA55AA55AA55AA55LL        |
       (x & 0x00AA00AA00AA00AALL) << 7  |
       (x >> 7) & 0x00AA00AA00AA00AALL;
    x = x & 0xCCCC3333CCCC3333LL        |
       (x & 0x0000CCCC0000CCCCLL) << 14 |
       (x >> 14) & 0x0000CCCC0000CCCCLL;
    x = x & 0xF0F0F0F00F0F0F0FLL        |
       (x & 0x00000000F0F0F0F0LL) << 28 |
       (x >> 28) & 0x00000000F0F0F0F0LL;
  
    for (i = 7; i >= 0; i--) {
        B[n*i] = x;        // Store result into
        x = x >> 8;        // output array B.
    }
}
```



*Compact code for transposing a 32X32-bit matrix.*

```c
void transpose32(unsigned A[32]) {
    int j, k;
    unsigned m, t;
    
    m = 0x0000FFFF;
    for (j = 16; j != 0; j = j >> 1, m = m ^ (m << j)) {
        for (k = 0; k < 32; k = (k + j + 1) & ~j) {
            t = (A[k] ^ (A[k+j] >> j)) & m;
            A[k] = A[k] ^ t;
            a[k+j] = A[k+j] ^ (t << j);
        }
    }
}
```



```c
void transpose32_optimized(uint32_t A[32]) {
    int j, k;
    unsigned m, t;
    
    j = 16;
    m = 0x0000FFFF;
    for (k = 0; k < 32; k = (k + j + 1) & ~j) { swap(A[k], A[k + j], j, m); }
 
    j = 8;
    m = 0x00ff00ff;
    for (k = 0; k < 32; k = (k + j + 1) & ~j) { swap(A[k], A[k + j], j, m); }
 
    j = 4;
    m = 0x0f0f0f0f;
    for (k = 0; k < 32; k = (k + j + 1) & ~j) { swap(A[k], A[k + j], j, m); }
 
    j = 2;
    m = 0x33333333;
    for (k = 0; k < 32; k = (k + j + 1) & ~j) { swap(A[k], A[k + j], j, m); }
 
    j = 1;
    m = 0x55555555;
    for (k = 0; k < 32; k = (k + j + 1) & ~j) { swap(A[k], A[k + j], j, m); }
```



*Straight-line code for transposing a 32X32-bit matrix.*

```c
#define swap(a0, a1, j, m) t = (a0 ^(a1 >> j)) & m; \
                           a0 = a0 ^ t; \
                           a1 = a1 ^ (t << j);
void transpose32(unsigned A[32], unsigned B[32]) {
    unsigned m, t;
    unsigned a0, a1, a2, a3, a4, a5, a6, a7,
           a8, a9, a10, a11, a12, a13, a14, a15,
           a16, a17, a18, a19, a20, a21, a22, a23,
           a24, a25, a26, a27, a28, a29, a30, a31;
    
    a0  = A[ 0]; a1  = A[ 1]; a2  = A[ 2]; a3  = A[ 3];
    a4  = A[ 4]; a5  = A[ 5]; a6  = A[ 6]; a7  = A[ 7];
    a8  = A[ 8]; a9  = A[ 9]; a10 = A[10]; a11 = A[11];
    a12 = A[12]; a13 = A[13]; a14 = A[14]; a15 = A[15];
    a16 = A[16]; a17 = A[17]; a18 = A[18]; a19 = A[19];
    a20 = A[20]; a21 = A[21]; a22 = A[22]; a23 = A[23];
    a24 = A[24]; a25 = A[25]; a26 = A[26]; a27 = A[27];
    a28 = A[28]; a29 = A[29]; a30 = A[30]; a31 = A[31];
    
    m = 0x0000FFFF;
    swap(a0,  a16, 16, m);
    swap(a1,  a17, 16, m);
    swap(a2,  a18, 16, m);
    swap(a3,  a19, 16, m);
    swap(a4,  a20, 16, m);
    swap(a5,  a21, 16, m);
    swap(a6,  a22, 16, m);
    swap(a7,  a23, 16, m);
    swap(a8,  a24, 16, m);
    swap(a9,  a25, 16, m);
    swap(a10, a26, 16, m);
    swap(a11, a27, 16, m);
    swap(a12, a28, 16, m);
    swap(a13, a29, 16, m);
    swap(a14, a30, 16, m);
    swap(a15, a31, 16, m);
    m = 0x00FF00FF;
    swap(a0,  a8,   8, m);
    swap(a1,  a9,   8, m);
    swap(a2,  a10,  8, m);
    swap(a3,  a11,  8, m);
    swap(a4,  a12,  8, m);
    swap(a5,  a13,  8, m);
    swap(a6,  a14,  8, m);
    swap(a7,  a15,  8, m);
    swap(a16, a24,  8, m);
    swap(a17, a25,  8, m);
    swap(a18, a26,  8, m);
    swap(a19, a27,  8, m);
    swap(a20, a28,  8, m);
    swap(a21, a29,  8, m);
    swap(a22, a30,  8, m);
    swap(a23, a31,  8, m);
    m = 0x0F0F0F0F;
    swap(a0,  a4,   4, m);
    swap(a1,  a5,   4, m);
    swap(a2,  a6,   4, m);
    swap(a3,  a7,   4, m);
    swap(a8,  a12,  4, m);
    swap(a9,  a13,  4, m);
    swap(a10, a14,  4, m);
    swap(a11, a15,  4, m);
    swap(a16, a20,  4, m);
    swap(a17, a21,  4, m);
    swap(a18, a22,  4, m);
    swap(a19, a23,  4, m);
    swap(a24, a28,  4, m);
    swap(a25, a29,  4, m);
    swap(a26, a30,  4, m);
    swap(a27, a31,  4, m);
    m = 0x33333333;
    swap(a0,  a2,   2, m);
    swap(a1,  a3,   2, m);
    swap(a4,  a6,   2, m);
    swap(a5,  a7,   2, m);
    swap(a8,  a10,  2, m);
    swap(a9,  a11,  2, m);
    swap(a12, a14,  2, m);
    swap(a13, a15,  2, m);
    swap(a16, a18,  2, m);
    swap(a17, a19,  2, m);
    swap(a20, a22,  2, m);
    swap(a21, a23,  2, m);
    swap(a24, a26,  2, m);
    swap(a25, a27,  2, m);
    swap(a28, a30,  2, m);
    swap(a29, a31,  2, m);
    m = 0x55555555;
    swap(a0,  a1,   1, m);
    swap(a2,  a3,   1, m);
    swap(a4,  a5,   1, m);
    swap(a6,  a7,   1, m);
    swap(a8,  a9,   1, m);
    swap(a10, a11,  1, m);
    swap(a12, a13,  1, m);
    swap(a14, a15,  1, m);
    swap(a16, a17,  1, m);
    swap(a18, a19,  1, m);
    swap(a20, a21,  1, m);
    swap(a22, a23,  1, m);
    swap(a24, a25,  1, m);
    swap(a26, a27,  1, m);
    swap(a28, a29,  1, m);
    swap(a30, a31,  1, m);
    
    B[ 0] = a0;  B[ 1] = a1;  B[ 2] = a2;  B[ 3] = a3;
    B[ 4] = a4;  B[ 5] = a5;  B[ 6] = a6;  B[ 7] = a7;
    B[ 8] = a8;  B[ 9] = a9;  B[10] = a10; B[11] = a11;
    B[12] = a12; B[13] = a13; B[14] = a14; B[15] = a15;
    B[16] = a16; B[17] = a17; B[18] = a18; B[19] = a19;
    B[20] = a20; B[21] = a21; B[22] = a22; B[23] = a23;
    B[24] = a24; B[25] = a25; B[26] = a26; B[27] = a27;
    B[28] = a28; B[29] = a29; B[30] = a30; B[31] = a31;
}
```

[back](../../)
