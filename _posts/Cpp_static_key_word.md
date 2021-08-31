---
layout: post
title: C++ static关键字
---
C++ static关键字有三种完全不同的用途：

1. 表示一个静态存储器的变量，且具有internal linkage，即static变量
2. 表示一个静态存储器的变量，但是只在一个局部作用域可见，保证仅初始化一次，即static local变量
3. 表示一个class的静态成员，整个class共享一份，不绑定任何instance，即static member变量

## static变量

static变量由`static`修饰，具有静态存储器。通常在main函数之前初始化，存活到main函数结束。

```c++
static int a;
```

## static local变量

在一个函数体内部（严格的说是block scope），用static变量就是static local变量。如：

```c++
void func(){
    static int a;
}
```

这类变量一般在第一次运行到这段代码的时候进行初始化。但是相应的代价就是，每次运行到这个地方都要检查是否初始化。

要注意的是，这个初始化是多线程安全的，可以用来做线程安全的单例（Meyers单例模型）

## static member变量

声明一个静态成员变量很简单：

```c++
class A{
    static int a;
}
```

但是问题是：当这段头文件被多个文件include的时候，这个符号a放在哪个文件里成了一个问题。

C++设计者的方案是再加一条语句专门用来生成符号，顺便可以初始化：

```c++
// A.h 可以被多次包含
class A{
    static int a;
}

// A.cpp 只翻译一次
#include "A.h"
int A::a; // 生成一个符号
```

但是如果我们只想读取`A::a`的值，那完全可以不把`A::a`放进内存，这样就不需要这个符号了，也就不需要把这个符号放进内存了

```c++
// A.h
class A{
    static const int a = 0;
    // 不生成符号，但是可以编译时读a的值
}
```

所以按照C++的设计，只有const的static member变量支持类内初始化，如果不在类外提供一个符号，那么对`A::a`取地址的时候，链接器会提示没有符号

```c++
undefined reference to A::a
```



inline的static member变量

C++17引入了inline的static member变量，即每个翻译单元生成一个符号，然后链接器选其中一个实现。加了inline之后就不需要专门在`A.cpp`内生成一个符号了

```c++
// A.h 可以被多次包含
class A{
    static inline int a;
    // 生成符号，可以取地址
    // 且支持类内初始化
}
```

C++17之后，`constexpr`的static member变量默认`inline`，所以我们可以写出这样的代码

```c++
// A.h 可以被多次包含
class A{
    static constexpr int a = 0;
    // 生成符号，可以取地址
    // 且支持类内初始化
}
```





