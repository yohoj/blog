---
title: electron 配置说明
date: 2023-04-07 22:53:27
tags: electron
---
```json
{
    "name": "installFile",//安装目录
    "version": "1.0.0",//版本号
    "description": "",
    "main": "bin/main.js",
    "scripts": {
        "start": "tsc -p ./ && electron ./bin/main.js",
        "dist": "tsc -p ./ && electron-builder",
        "test": "echo \"Error: no test specified\" && exit 1"
    },
    "build": {
        "appId": "com.test.app",//appid
        "copyright": "Copyright © 2023 yohoj",
        "productName": "appName",//安装包名称
        "asar": true, //是否使用asar加密
        "files": [
            "./bin/**/*"
        ],//打包目录
        "extraResources": [
            "./bin/res/**"
        ],//额外资源
        "compression": "maximum",//压缩级别 “store” | “normal” | “maximum” | “undefined”
        "directories": {
            "output": "dist"//输出目录
        },
        "publish": [//自动更新地址
        {
            "provider": "generic",
            "url":    "http://10.225.136.154/electron/update/static/official"
        }
        ],
        "nsis": {
            "oneClick": false,//是否一键安装
            "allowToChangeInstallationDirectory": true,//允许改变安装目录ß
            "createDesktopShortcut": "always",//创建桌面快捷方式
            "createStartMenuShortcut": true,//创建开始目录
            "language": "2052"//语言
        },
        "mac": {
            "category": "your.app.category.type"
        },
        "win": {
            "icon": "bin/res/logo/logo.ico",//安装包图标
            "target": [
                "nsis"
            ]
        }
  }
}

```