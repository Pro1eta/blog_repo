---
title: C++中的顶层const与底层const
published: 2024-06-25
description:
tags: [C/C++]
categories: 技术笔记
---

# 指针与 const

与引用一样, 也可以令指针指向常量或者非常量. 在C语言的学习中我们已经遇到:

- **常量指针(pointer to const)**
  **不能通过该指针的解引用去改变所指对象的值**, 但是允许从其它途径去改变指针指向的对象的值. 对该指针而言, 它所指向的对象如同常量.
- **指针常量(const pointer)**
  即把指针(变量)本身定义为常量. 显然不能更改它存储的地址, 并且, **必须初始化**. 但是可以通过该指针去修改指向的值.

这两个概念不难, 但是, 一旦混用(包括和引用混用)起来, 难免让人费解, 因此引入以下的概念:

# 顶层 const 和 底层 const

指针本身是否为常量, 和指针指向常量否, 是两个独立的问题. 我们说**顶层 const** 表示指针(或者引用)自身是常量, 用**底层 const** 表示指针指向的对象是一个常量. 显然, 指针类型和引用类型既可以是顶层 const, 也可以是底层 const. 更一般地说来, 顶层 const 也可以表示任意的对象是常量, 包括算术类型, 类, 指针等等.

```cpp
int i = 0;
int *const pl = 6i; 	 // 不能改变 pl 的值, 这是一个顶层 const
const int ci = 42; 		 // 不能改变 ci 的值, 这是一个顶层 const
const int *p2 = &ci;	 // 允许改变 p2 的值, 但这是一个底层 const
const int *const p3 = p2;// 靠右的 const 是顶层 const, 靠左的是底层 const
const int &r = ci; 		 // 底层 const
```

执行拷贝操作的时候, 常量如果仅是顶层 const(对于指针, 要求指向的东西是一致的), 只要符合基本的语法(比如const变量不能再改变), 则这个常量可以成为被拷贝的那个. 

```cpp
i = ci;					// 正确, ci 是顶层 const
p2 = p3;				// 正确, p2, p3 都指向 const int, p3 是顶层 const
```

对于底层 const 要更复杂一点. 要求两个对象具有相同的底层 const 资格, 或者数据类型可以转换.

人话: 非常量可以转换为常量, 反之不行.

```cpp
int *p= p3;				// 错误：p3包含底层 const 的定义, 但是p却没有.
p2 = p3;				// 正确：p2和p3都是底层 const
p2 = &i;				// 正确：int*能转换成 const int*
int &r = ci;			// 错误：普通的int&不能绑定到int常量上
const int &r2 = i;		// 正确：const int 是可以绑定到一个善通int上的
```

# 关于 const 成员函数

在一个类中, 其成员函数有一个**看不见的参数** `this`, 它是一个指向调用这个函数的**对象**的**指针**. 比如

```cpp
class example {
public:
    void example_func();
};

int main()
{
    example myclass;
}

void example::example_func(void) {
    /* Definition... */
}
```

调用 `myclass.example_func()` 的时候, 相当于会多一个参数, 被编译器重写成了 `example::example_func(&myclass)`. 调用 example 的 example_func() 成员时传入了 myclass 的地址. 在成员函数内部则可以用 `this` 来表示这个地址.

C++ 允许把 const 关键字放在成员函数的参数列表之后(**比如在声明时**), 此时, 紧跟在参数列表后面的 const 表示 `this` 是一个**指向常量的指针**. 这样使用 const 的成员函数称为**常量成员函数**.

```cpp
class Circle {
public:
    // 构造函数，初始化半径
    Circle(double radius) : m_radius(radius) {}
    // 常量成员函数，获取半径
    double getRadius() const {
        return m_radius;
    }
    // 常量成员函数，计算并返回圆的面积
    double getArea() const {
        return M_PI * std::pow(m_radius, 2);
    }
private:
    double m_radius; // 圆的半径
};
```

能够发现, 由于 `this` 具有了底层 cosnt 的资格, 对应的常量成员函数不能够改变调用它的对象的内容. 此时 `this` 指向的对象, 可以是常量, 也可以是非常量. 

那么, 如果对象是一个常量, 而被调用的成员函数不是 const 呢? 

比如对一个类 `example`. 非常量成员函数的 `this` 是 `example*` 类型, 但传入的指针(指向对象)却是 `const example*` 类型. 在传参的过程中, 我们会把传入的值赋给形参, 相当于:

```cpp
example* this = &Object;
// Object 是 const example 类型
```

显然, 两者的底层 const 资格不一致, 且无法转换. 根据上文, 这是不允许的, 因此

>常量对象, 以及常量对象的引用或者指针都**只能**调用常量成员函数.

非常量函数对常量对象是不可用的, 无法通过编译.
