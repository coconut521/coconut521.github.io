---
title: Q#的安装（VSCode）
createTime: 2020/04/05 21:36:52
permalink: /qsharp/ogl6jclh/
tags:
    - Q#
    - Python
    - IT
---

> **Q#**(*QSharp*)是一种专为量子计算机开发的量子编程语言，官方给出了三种不同的使用方式
> 1.Q#+Python，即在 **.q** (QSharp)文件里编写量子算法，然后在Python中(以Host.py的形式)调用
> 2.Q#+C#，内容同上，改为采用C#作为驱动
> 3.在Visual Studio（2017或2019均可）中安装相关拓展从而直接在VS中编写量子程序。
> **由于我比较倾向第一种，故本教程采用vscode安装并使用Q#**

<!--more-->

# 前期准备

首先，你需要安装一个......电脑！（这可不是废话，你总不能指望用大脑写程序吧。不过说句废话，或许将来真有可能用大脑编写程序！）

然后[VSCode](https://code.visualstudio.com/)。这是算是基本中的基本了，也是微软官方的推荐。当然，你可以选的自己喜欢的代码编辑器。

>如果不知道什么是VSCode或者什么是代码编辑器，又或者不太了解编程，可以看我写的编程基础部分
>都明白的跳过这些直接看后边。
>我会在“基础”部分对电脑、编程等基本知识以及一些属于做一些讲解。

下面的内容很重要，如果没有安装好可能导致代码无法运行或各种错误。
- [Python](https://www.python.org/downloads/) 3.6或更高版本
- [PIP](https://pip.pypa.io/en/stable/installing) Python 包管理器
- [.NET Core SDK 3.1 或更高版本](https://www.microsoft.com/net/download)

## Python的安装

在官网中下载Python最新版本，地址在上面点击Python即可打开，没有找到的...[ここにです! ](https://www.python.org/downloads/)

这个就不过多赘述了，个人认为安装时没有太多问题。

## PIP安装

这个有必要强调一下，安装时需要使用`python3 xxxx/get-pip.py`。注意是**python3**，而不是*python*

剩下的照常安装......

## .Net Core SDK的安装

非常简单，按照官网描述，很快就可以安装。

# QDK（QSharp Development Kit）的安装

安装进行到这步就说明离成功不远了，但是别大意，这里才是最容易出现问题的地方！！！

1. 安装`qsharp`包，这是一个允许在 Q # 和 Python 之间互操作的 Python 包。

```cmd
pip install qsharp
```

2. 安装`iqsharp`，Jupyter 和 Python 使用的内核，提供用于编译和执行 Q # 操作的核心功能。

```
dotnet tool install -g Microsoft.Quantum.IQSharp
dotnet iqsharp install
```

3. [为 VS Code 安装 QDK 扩展](https://marketplace.visualstudio.com/items?itemName=quantum.quantum-devkit-vscode)

这个点击链接查看微软官网的文档

>声明：以上部分内容来自[微软官网关于Q#的文档](https://docs.microsoft.com/zh-cn/quantum/install-guide/pyinstall)，点击查看官方的说明～

# Hello, World! 测试

>什么！？你还不知道什么是Hello,World！来来来，“分类-IT-基础”你可以看看！

- 通过创建名为 Operation.qs 的文件并向其添加以下代码来创建最小 Q# 操作：
```Q#
namespace HelloWorld {
    open Microsoft.Quantum.Intrinsic;
    open Microsoft.Quantum.Canon;

    operation SayHello() : Unit {
        Message("Hello from quantum world!");
    }
}
```

- 创建名为 hello_world.py 的 Python 程序来调用 Q# SayHello() 操作：
```python
import qsharp

from HelloWorld import SayHello

SayHello.simulate()
```

- 运行该程序

***这里需要说明一下，根据官网的文档是***`python hello_world.py`***但我们需要使用***`python3 hello_world.py`

- 如果程序输出如下内容，则表明一切都没问题了！安装成功了！
```bash
Hello from quantum world!
```

# 可能遇到的问题

- 无法在输入命令时总是显示各种失败

可能是你没有给予相应的权限，如果是Windows系统，请右键cmd.exe选择“以管理员身份打开”，Mac/Linux则需要在命令前面添加`sudo `（别忘了空格）以保证该软件有相应的权限去安装。

- pip安装qsharp时显示版本问题

可能的解决方案：回到安装PIP的那一步使用`python3`命令进行安装

# 结束语

如果还有问题或有需要交流的可以评论，我会不定期查看评论并且进行回复，如果您提的问题或建议有帮助，我会及时的更新该文档，以便其他人更好的阅读。

## 谢谢观看！