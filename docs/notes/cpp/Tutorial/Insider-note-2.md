---
title: For Struct SelectionSort
tags:
  - C++班级内部资料
createTime: 2023/11/03 22:09:05
permalink: /cpp/jxxjuq60/
---
> for循环 结构体 选择排序

<!--more-->

---

## for 循环

```C++
// 把循环有关的判断变量（控制循环的变量）都写在小括号里
// int i; 可以单独写出来 然后括号第一句就可以只写 i = 0
// i < 9 判断语句与while逻辑相同
// i++ 对i进行操作防止死循环
for (int i = 0; i < 9; i++) // 注意使用";"分开
{
    //......
}

// 内容只有一条语句时可以不写大括号
```

---

## 结构体

将多个不同数据类型组合成一种新的类型（或者称呼为“组合结构”）
比如一个人可以把他抽象成一个结构体
包含什么呢？
姓名(字符串)、年龄（int）、身高(int)、体重(int)
可见，结构体是将 **多个类型** 的数据结合
对比数组，同一数组里的所有数据只能是同一类型
具体写法
```C++
struct People
{
    char name[10];
    int age;
    int height;
    int weight;
};
//别忘了结尾有个分号！！！！！！

// 使用这个结构体和定义一个变量类似
People a = {"cst", 18, 180, 70};
// 定义后想要读取其中的数据要这样写 "a.age" 比如：
a.age = 8;
a.height = 185

// 但是 a.name 是字符串 不能直接赋值
// a.name = "yzy" 是错的！a.name[10] = "yzy" 更不对！！！
```

> 别忘了struct大括号结尾有个分号！！！！！！

---
## 排序

> 排序方法有很多种，它们的运行速度和逻辑各不相同，这次讲的是"选择排序"

```C++
#include <iostream>
using namespace std;

int main()
{
    // 假设这个是要排列的数组
    int a[5] = { 17, 83, 49, 11, 26 }; 
    int i, j, swap;

    // 第一个数
    for (i = 0; i < 5; i++)
    {
        // 第二个数
        for (j = i + 1; j < 5; j++)
        {
            // 比较这两个数 如果第二个数小于第一个数
            if (a[j] < a[i])
            {
                // 交换这两个数
                swap = a[j];
                a[j] = a[i];
                a[i] = swap;
            }        
        }
    }

    // 输出结果
    for (int k = 0; k < 5; k++)
        cout << a[k] << " ";
    system("pause");
    return 0;
}
```

程序运行结果

```
11 17 26 49 83 请按任意键继续. . .
```