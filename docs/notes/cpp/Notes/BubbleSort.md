---
title: Bubble Sort
date: 2022-06-07T19:19:51.000Z
tags:
  - C++
  - Sort
createTime: 2022/06/07 19:51:00
permalink: /cpp/lfhr03b0/
---

> 外循环 `i` 一共循环 `数组总数` 次
> 内循环 `j` 内逐个比对 `总数-i-1` 次

<!--more-->

```c++
#include <iostream> 
using namespace std;

int main()
{
    //创建数组 print
    int arr[9] = { 0 };
    
    for (int i=0; i<9; i++) 
        cin >> arr[i];
        
    cout << "您输入的是: " ;
    
    for (int i=0; i<9; i++) 
        cout << arr[i] << " ";
    cout << endl;
    
    cout << "下面开始排序：" << endl;
    
    //冒泡排序 操作9-1次（总数-1)
    for (int i=0; i<8; i++)
    {
        //对比i-1次
        for (int j=0; j<8-i; j++)
        {
            if(arr[j] > arr[j+1])
            {
                int temp = arr[j];
                arr[j]=arr[j+1];
                arr[j+1]=temp;
            }
        }
        
        for (int k=0; k<9; k++) 
            cout << arr[k] << " ";
        cout << endl;        
    }
    
    return 0;
}
```
