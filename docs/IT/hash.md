---
title: 文件哈希值
createTime: 2022/02/08 11:34:05
permalink: /article/0qhwil5l/
tags:
    - hash
    - IT
---

查看文件校验码
<!--more-->
使用 `PowerShell` 或 `cmd` 都可

```
certutil -hashfile [file] [MD5/SHA1/SHA256...]
```