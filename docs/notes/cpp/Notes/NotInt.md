---
title: Check Input if not int
date: 2023-10-24T18:43:24.000Z
tags:
  - C++
createTime: 2023/10/24 18:43:24
permalink: /cpp/w7adxgq3/
---

> 为了防止向 int 类型输入字母等非法内容，可以使用以下方式输入：

<!--more-->
> 某些情况下需要 `#include <limit>`

```c++
while (!(cin >> i))
{
    cout << "Invalid input, please input again: " ;
    cin.clear();
    cin.ignore(numeric_limits<streamsize>::max(), '\n');
}
```