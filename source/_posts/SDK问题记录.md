---
title: electron接入steam SDK问题记录
date: 2023-06-07 23:13:49
tags:
---
gameoverlayui 无法调用, 在主进程js文件中加入
```
// 解决steam overlay无效的问题
app.commandLine.appendSwitch('--in-process-gpu')
```
