---
layout: post
category: "windowspe"
title:  "WINDOWS PE 概要"
tags: [二进制,windows pe]
---

### 1.windows pe 总体结构
![](/posts/windowspe_brief1.png)

### 2.windows pe 详细结构
Math.c:
```
__declspec(dllexport) double Add(double a, double b)
{
    return a+b;
}

__declspec(dllexport) double Sub(double a, double b)
{
    return a-b;
}

__declspec(dllexport) double Mul(double a, double b)
{
    return a*b;
}

__declspec(dllexport) double Div(double a, double b)
{
    return a/b;
}
```
TestMath.c:
```
#include <stdio.h>

#if 1
__declspec(dllimport) double Mul(double a, double b);
__declspec(dllimport) double Div(double a, double b);
__declspec(dllimport) double Add(double a, double b);
__declspec(dllimport) double Sub(double a, double b);
#endif

int main(int argc, char **argv)
{
    double result = 0.0;
    result = Add(3.0, 2.0);
    result = Sub(3.0, 2.0);
    result = Mul(3.0, 2.0);
    result = Div(3.0, 2.0);
    printf("result = %f\n", result);
    return 0;
}
```
build:
```
编译环境：vs2008

cl /c /Za /MDd Math.c
link /DLL /out:Math.dll Math.obj

cl /c /Za /MDd TestMath.c
link TestMath.obj Math.lib
```
![](/posts/windowspe_brief2.png)

### 3.windows pe 动态加载
![](/posts/windowspe_brief3.png)
