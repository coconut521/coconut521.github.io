---
title: Find Constellation
tags:
  - C++班级内部资料
createTime: 2023/10/20 17:35:05
permalink: /cpp/hfak05id/
---

> 输入日期，输出对应星座 **if else if else**
> 
> 实现方法：OOP 

<!--more-->

标准作业解法：
```C++
#include <iostream>
using namespace std;

int main()
{
    cout << "Hello World!";
    int month, day;

    cout << "请输入月份：";
    cin >> month;
    cout << "请输入日期：";
    cin >> day;

    if ((month == 3 && day >= 21) || (month == 4 && day <= 20))
    {
        cout << "白羊座";
    }
    else if ((month == 4 && day >= 21) || (month == 5 && day <= 21))
    {
        cout << "金牛座";
    }
    else if ((month == 5 && day >= 22) || (month == 6 && day <= 21))
    {
        cout << "双子座";
    }

    return 0;
}

```

---

一种麻烦但看起来很复杂的解法
面向对象式编程解法


::: code-tabs
@tab stdafx.h

```C++
// stdafx.h : 预编译头
#pragma once
#include <iostream>
#include <cstring>
```

@tab Date.h

```C++
// Date.h Date类成员声明

#pragma once
#ifndef DATE
#define DATE
#include "stdafx.h"

class Date
{
private:
    int m_Month, m_Day, m_fDate;

public:
    int FindConsellation();
    Date() = default;
    Date(int M, int D);
    //int m_Consellation = FindConsellation();

};

#endif
```

@tab Date.cpp

```C++
//Date.cpp 用于实现Date类中的构造函数与查找功能

#include "Date.h"

// Date 类的构造函数
Date::Date(int M, int D)
{
    m_Month = M;            // 传入初始数值
    m_Day = D;
    m_fDate = M * 100 + D;  // 转换日期格式
                    // 将日期转换为整数数字如01-25 转换为125
}

// 针对转换后的格式返回星座对应的数字
// 0-11 水瓶座-魔羯座 按日期排列
int Date::FindConsellation()
{
    if (m_fDate >= 120 && m_fDate <= 218)
        return 0;
    else if (m_fDate >= 219 && m_fDate <= 320)
        return 1;
    else if (m_fDate >= 321 && m_fDate <= 419)
        return 2;
    else if (m_fDate >= 420 && m_fDate <= 520)
        return 3;
    else if (m_fDate >= 521 && m_fDate <= 621)
        return 4;
    else if (m_fDate >= 622 && m_fDate <= 722)
        return 5;
    else if (m_fDate >= 723 && m_fDate <= 822)
        return 6;
    else if (m_fDate >= 823 && m_fDate <= 922)
        return 7;
    else if (m_fDate >= 923 && m_fDate <= 1023)
        return 8;
    else if (m_fDate >= 1024 && m_fDate <= 1122)
        return 9;
    else if (m_fDate >= 1123 && m_fDate <= 1221)
        return 10;
    else if ((m_fDate >= 1222 && m_fDate <= 1231) || (m_fDate <= 119 && m_fDate >= 101))
        return 11;
    //else if (m_fDate >= 120 && m_fDate <= 218)
      //  return 0;
    else
        return -1;
}

```

@tab Constellation.cpp

```c++
// Constellation.cpp : 此文件包含 "main" 函数。程序执行将在此处开始并结束。
//

#include "stdafx.h"
#include "Date.h"
using namespace std;

string Constellation[12] = { "水瓶座", "双鱼座", "白羊座", "金牛座", "双子座", "巨蟹座", 
    "狮子座", "处女座", "天秤座", "天蝎座", "射手座", "魔羯座" };

int main()
{
    int mo = 0, day = 0;

    while (mo <= 0 || mo >= 13) 
    {
        cout << "Input month: ";
        while (!(cin >> mo))
        {
            cout << "Invalid input, please input again! " << endl << "Input month: ";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
        }
        if (mo <= 0 || mo >= 13)
            cout << "Invalid input, please input again: " << endl;
    }

    while (day <= 0 || day >= 31)
    {
        cout << "Input day: ";
        while (!(cin >> day))
        {
            cout << "Invalid input, please input again: " << endl << "Input month: ";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
        }
        if (day <= 0 || day >= 31)
            cout << "Invalid input, please input again: " << endl;
    }

    Date date(mo, day);

    // 检验输入数据是否合法
    if (date.FindConsellation() != -1)
        cout << "你的星座是: " << Constellation[date.FindConsellation()] << endl;
    //else

    //system("pause");

    return 0;
}

```


:::
