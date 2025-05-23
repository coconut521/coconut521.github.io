---
title: Conditional Operator
date: 2022-06-07T19:11:29.000Z
tags:
  - C++
createTime: 2022/06/07 19:11:29
permalink: /cpp/de3sd59v/
---

> 讲真，这段是知识盲点\[捂脸\]

<!--more-->

```c++
#include <iostream> 
using namespace std;

int main()
{
    int a = 1;
    int b = 2;
    int c = 0;
    
    
    //exp1 ? exp2 : exp3
    //exp1 真 则执行exp2 返回exp2
    //exp2 假 则执行exp3 返回exp3
    //返回值如果是变量可以继续赋值
    cout << (a>b ? a:b) << endl;
    //max: b 2
    
    (a>b ? a:b) = 3;
    //b 会变成 3
    
    return 0;
}
```
