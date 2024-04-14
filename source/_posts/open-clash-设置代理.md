---
title: open clash 代理设置
tags: []
categories: [软路由]
date: 2024-04-14 17:23:43
---
由于cloudflare tunnels的容器走代理一直连不上，需要将其直连。<br>
## 1.clash运行环境
![alt text](./open-clash-设置代理/image.png)
## 2.修改配置文件
覆写设置->规则设置->自定义规则打勾如下图
然后在下面文本框增加
```
- SRC-IP-CIDR,172.17.0.5/32,DIRECT
```
其中172.17.0.5是容器的ip
![alt text](./open-clash-设置代理/image-1.png)
最后点保存配置，应用配置<br>
## 3.最终效果
在clash日志中看到容器都走直连了
```··
[INFO] [TCP] 172.17.0.5:33428 --> 198.41.192.57:7844 match SrcIPCIDR(172.17.0.5/32) using DIRECT
```
