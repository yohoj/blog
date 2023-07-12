---
title: electron问题记录
date: 2023-06-07 23:13:49
categories: [electron]
---
### 调用dll错误
1. DLL引用的路径错误，检查下DLL的路径是否正确
    ```
    Uncaught Error: Dynamic Linking Error: Win32 error 126
    ```
2. DLL位数不对,根据系统来确定使用x86还是x64,可通过os进行判断引入相应的DLL
    ```
    Uncaught Error: Dynamic Linking Error: Win32 error 193<br>
    ```

3. DLL没有对应的函数
    ```
    Uncaught Error: Dynamic Linking Error: Win32 error 127
    ```
    可以使用VS 2017的开发人员命令提示符，然后到dll目录下，运行

    ```bash
    dumpbin /exports mylib.dll
    ```
### 接入steam sdk问题
gameoverlayui 无法调用, 在主进程js文件中加入
```javascript
// 解决steam overlay无效的问题
app.commandLine.appendSwitch('--in-process-gpu')
```

### 接入wegame sdk问题
打开一直白屏，需要在主进程js文件中加入
```javascript
app.commandLine.appendSwitch('--no-sandbox');
```

### 调用alert后，input输入框无法聚焦
解决方法：重写alert<br>
在preload.js中增加如下代码
```javascript
const { ipcRenderer } = require('electron')
window.alert = (str) => {
    ipcRenderer.send("alert", str);
}
```
main.js
```javascript
    const { ipcMain, dialog } = require('electron');
    ipcMain.on("alert", (e, str) => {
        var options = {
        type: 'warning',
        buttons: ["Ok"],
        defaultId: 0,
        cancelId:0,
        detail:str,
        message: ''
        }
        dialog.showMessageBoxSync(options)
    });
```
