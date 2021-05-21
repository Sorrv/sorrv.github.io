---
layout: default
title: Computer Organization
description: Some Notes
---

# Computer Organization

## Chapter 2 Instructions

### 2.13 Sorting Program

#### 2.13.1 swap process

```c
void swap(long long int v[], size_t k)
{
    long long int temp;
    temp = v[k];
    v[k] = v[k+1];
    v[k+1] = temp;
}
```

**LEGv8**

寄存器X0到X7参数传递

swap两个参数v和k可被分配给寄存器X0和X1，将剩余变量temp分配给寄存器X9（swap是一个叶过程）

按字节编址，双字之间地址相差8

1. 通过左移3位（k*8）获得v[k]的地址
2. 根据X10取出v[k]的值，并将X10+8得到v[k+1]
3. 将X9和X11存储到需要交换数据的地址中
4. 跳转指令返回

```assembly
LSL    X10,  X1, #3      //  reg  X10 = k * 8
ADD    X10,  X0, X10     //  reg  X10 = v + (k * 8)
​                        //  reg  X10 has the address of v[k]
LDUR   X9,  [X10, #0]    //  reg  X9  (temp) = v[k]
LDUR   X11, [X10, #8]    //  reg  X11 = v[k+1]
​                        //  refers to next element of v
STUR   X11, [X10, #0]    //  v[k] = reg  X11
STUR   X9,  [X10, #8]    //  v[k+1] = reg X9  (temp)
​
BR     LR                #   return to calling routine 
```

#### 2.13.2 sort process

```c
void sort (long long int v[], size_t int n)
{
    size_t, j;
    for (i = 0; i < n; i += 1) {
        for (j = i - 1; j >= 0 && v[j] > v[j+1]; j += 1) {
            swap(v, j);
        }
    }
}
```



### 2.14 Array and Pointer

将内存中一串双字清零

```c
clear1(long long int array[], size_t int size)
{
    size_t i;
    for (i = 0; i < size; i += 1)
        array[i] = 0;
}

clear2(long long int *array, size_t int size)
{
    long long int *p;
    for (p = &array[0]; p < &array[size]; p = p + 1)
        *p = 0;
}
```

To be continued....
* * *
Last updated on May 21st at 5:19 p.m. (GMT +8)

[back](../../)
