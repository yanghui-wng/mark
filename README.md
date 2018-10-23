# 流水灯实验报告

|   班级   |  姓名  |     学号      |
| :------: | :----: | :-----------: |
| 机设1606 | 王阳辉 | 0121602950110 |

[TOC]

## 问题描述

### 现象

LED灯管依次亮灯

### 如何产生

通过给P1口赋值，以及通过移位函数实现

------

## 8个流水灯

### 原理图

![流水灯](C:\Users\20745\Desktop\流水灯.jpg)



### 程序

```c
#include<reg51.h>
#include<intrins.h>//包含移位函数的头文件
#define unchar unsigned char
#define uint unsigned int
void delay(uint i)//延时函数
{
	unchar t;
	while (i--)
	{
		for (t = 0; t < 120; t++);
	}
}
void main()//主程序
{
	P1 = 0xfe;//向P1口送亮灯程序
	while (1)
	{
		delay(50);//设置50ms的延时
		P1 = _crol_(P1, 1);//把P1中的数据左移一位
	}
```



------

## 16个流水灯

### 原理图

![流水灯.改](C:\Users\20745\Desktop\流水灯.改.jpg)

### 程序

```c
#include<reg51.h>
#include<intrins.h>//包含循环左、右移位置函数的头文件
#define unchar unsigned char
#define uint unsigned int
void delay(uint i)//延时函数
{
	unchar t;
	while (i--)
	{
		for (t = 0; t < 120; t++);
	}
}
void main()//主程序
{
	P1 = 0xfe;//向P1口送亮灯程序
	P3 = 0xff;//向P3口送灭灯程序
	while (1)
	{
		int i;
		for (i = 1; i < 8; i++)
		{
			delay(50);
			P1 = _crol_(P1, 1);//把P1中的数据左移一位
		}
		delay(50);//设置50ms的延时
		P1 = 0xff;//向P1口送灭灯程序
		P3 = 0x7f;//向P3口送亮灯程序
		for (; i < 16; i++)
		{
			delay(50);
			P3 = _cror_(P3, 1);//把P3中的数据右移一位
		}
		i = 1;
		P3 = 0xff;//向P3口送灭灯程序
		P1 = 0xfe;//向P1口送亮灯程序
		delay(50);
	}
}

```



------

## 16个变速流水灯

### 原理图

![流水灯.改](C:\Users\20745\Desktop\流水灯.改.jpg)

### 程序

```c
#include<reg51.h>
#include<intrins.h>//包含循环左、右移位置函数的头文件
#define unchar unsigned char
#define uint unsigned int
void delay(uint i)//延时函数
{
	unchar t;
	while (i--)
	{
		for (t = 0; t < 120; t++);
	}
}
void main()//主程序
{
	P1 = 0xfe;//向P1口送亮灯程序
	P3 = 0xff;//向P3口送灭灯程序
	while (1)
	{
		int i;
		for (i = 1; i < 8; i++)
		{
			delay(50 + 50 * i);
			P1 = _crol_(P1, 1);//把P1中的数据左移一位
		}
		delay(50 + 50 * i);//设置延时
		P1 = 0xff;//向P1口送灭灯程序
		P3 = 0x7f;//向P3口送亮灯程序
		for (; i < 16; i++)
		{
			delay(50 + 50 * i);
			P3 = _cror_(P3, 1);//把P3中的数据右移一位
		}
		i = 1;
		P3 = 0xff;//向P3口送灭灯程序
		P1 = 0xfe;//向P1口送亮灯程序
		delay(50);
	}
}

```



------

## 8个随机流水灯

### 原理图

![流水灯](C:\Users\20745\Desktop\流水灯.jpg)

### 程序

```c
#include<reg51.h>
#include<intrins.h>
#include<stdio.h>
#include<stdlib.h>
#define unchar unsigned char
#define uint unsigned int
void delay(uint i)
{
	unchar t;
	while (i--)
	{
		for (t = 0; t < 120; t++);
	}
}
void main()
{
	P1 = 0xfe;
	while (1)
	{
		delay(50);
		P1 = _crol_(P1, rand() % 7); //随机亮灯
	}
}

```

© 2018 GitHub, Inc.
Terms
Privacy
Security
Status
Help
Contact GitHub
Pricing
API
Training
Blog
About
