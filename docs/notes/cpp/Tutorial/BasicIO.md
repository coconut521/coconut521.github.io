---
title: Basic IO
tags:
  - C++班级内部资料
createTime: 2023/10/26 18:16:50
permalink: /cpp/tun72xn1/
---

> 本期内容：关于新建解决方案、代码框架、基础输入输出、 if 条件判断、 while 循环、代码框架的解释.

<!--more-->
---

## 新建解决方案
根据使用 Visual Studio 版本不同可以：

::: tabs

@tab Visua Studio 2010 or Older Version

新建解决方案-C++**控制台**应用-勾选**空项目**

@tab Visual Studio 2022

新建解决方案-**空项目**
然后在建好的空项目中，找到“**源文件**”，右键，添加项，输入文件名（可以自己随便写，推荐写为 `main.cpp` ）

或者，可以新建解决方案-**C++控制台应用**，直接出现写好的框架（不完全符合目前习惯）

> 注意此方法不完全符合目前习惯，因为没有写 `using namespace std;` 
> 所以应该将 `using namespace std;` 添加到 `#include <iostream>` **下方**

:::

---

## 代码框架

可以点击代码框右上角符号直接复制.

```C++
#include <iostream>
using namespace std;

int main()
{

    system("pause");
    return 0;
}
```


> 注意，使用新版本 Visual Studio 时（如VS2022）可以不写 `syetem("pause")`.

---

## 基本输入输出

```C++
#include <iostream>
using namespace std;

int main()
{
    cout << "Hello World!" << endl;

    int a = 0;
    cin >> a;
    cout << "您输入的数字是: " << a << endl;

    system("pause");    
    return 0;
}
```

程序运行结果：
```
Hello World!
114514 (这行为用户输入内容)
您输入的数字是: 114514
```

---

## if 判断语句

```C++
if ( 条件1 )
{
    ......
}
else if ( 条件2 )
{
    ......
}
…… // 可以有很多个 else if 
else
{
    //以上条件都不满足 执行此内容
    ......
}

// 如果内容只有一条语句 可以使用简单形式（不写大括号）
if ( 条件1 )
    ...;
// else if / else 同理
```
> 程序按顺序从上往下逐个判断是否满足条件;
> 如果满足则执行该条件对应大括号里的内容，并跳过后面的判断;
> 如果所有的条件都不满足，则执行 `else`;
> 其中 `else if` 和 `else` 可以不写，如果不写且不满足条件则跳过什么都不执行，也不会出现错误.

---

## while 循环语句

```C++
while ( 条件 )
{
    // 如果条件满足，则执行里面的内容
    // 执行完成后重新判断条件是否满足，如果满足再执行一遍
    // 知道不满足条件

    //如果执行到某次想主动跳出循环，而不是靠自动判断条件不满足使用：
    break;
}、

// 或者只有一条语句时
while ( 条件 )
    ...;
```

### 例子
```C++
#include <iostream>
using namespace std;

int main()
{
    int a = 1, b = 0;
    cin >> b;
    cout << "b is " << b << endl;
    while (a < 10)
    {
        cout << a << endl;
        a++; // 其它写法如下：
        // a = a + 1;
        // a += 1;
    }

}
```
运行结果：
```c++
(输入一个数)
b is (刚刚输入的数)
1
2
3
4
5
6
7
8
9
```
### 无限循环

```c++
while (1)
{
    // ……
}
```

> `while` `if` 语句中  `()` 的含义是将 `()` 内的表达式当成一个 `bool` 值来计算，如果表达式为真，即表达式对应的布尔值为1，那么条件成立，所以执行 `while (1)` 就意味着直接告诉计算机这里里面条件已经成立，且运行多少次都是成立的，所以会不断循环。
>
> 由于程序陷入死循环会导致无法正常结束，并占用计算机资源，因此不推荐这样写，如有需要，尽量使用正常的表达式，或添加 `break;` 跳出循环.


## 代码框架解释

```C++
#include <iostream>     // 调用 iostream 这个头文件，在这个头文件里写好了 cout cin endl 等函数
using namespace std;    // 为了防止名字冲突，将 cout cin endl 等写在 std 命名空间里面

int main()              // 一个 C++ 项目可心包含多个函数，而程序从 main 函数开始运行
{

    system("pause");    // 让程序结束前暂停 便于观察输出结果
    return 0;           // 程序在这里结束， 如果前面的代码中有循环或判断或恰当时刻需要提前结束,
                        // 可以前面再写一个，（可以写多个）
                        // 但结尾必须写一个
}
```


