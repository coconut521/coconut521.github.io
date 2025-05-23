---
title: Selection Sort of Name and Birthday
tags:
  - C++班级内部资料
createTime: 2023/11/03 16:41:34
permalink: /cpp/tjlyb0pn/
---

> **“结构体”**，然后是解决 **“排序问题”** ,事实上有很多种排序方法,这次作业使用 **“选择排序”** 算法

<!--more-->

---


## 作业解法

剩下就是解决年份排序完姓名如何对应了
且看代码

> 别直接抄哇啊啊!

```C++
#include <iostream>
using namespace std;

struct Celebrity
{
    char name[12];
    int year;
};

int main()
{

    Celebrity clb[3] = { 
        {"Jun Lei", 1969}, 
        {"Steve Jobs", 1955}, 
        {"Tim Cook", 1960} };
    int order[3] = { 0, 1, 2 };

    int i, j, min;
    int swap;
    //int a[6] = { 17, 83, 36, 37, 94, 15 };
    for (i = 0; i < sizeof(clb)/sizeof(Celebrity); i++)
    {
        for (j = i+1; j < 3; j++)
        {
            if (clb[j].year < clb[i].year)
            {
                swap = order[i];
                order[i] = order[j];
                order[j] = swap;
            }
        }
    }

    for (int i = 0; i < sizeof(clb) / sizeof(Celebrity); i++)
    {
        cout << clb[order[i]].name << " is birthed in " << clb[order[i]].year << " " << endl;
    }



    system("pause");
    return 0;
}
```
