---
layout: post
title: cloudflare tunnels status down
date: 2024-04-14 15:22:34
---
查看错误日志
```
'ERR Failed to create new quic connection error="failed to dial to edge with quic: timeout: no recent network activity"'
```
网上搜索发现是cloudflare使用了quic协议，需要切换到http2协议<br>
将docker的启动命令修改如下：
```
tunnel --no-autoupdate run --protocol http2 --token [token]
```
使用http2进行连接后发现还是存在问题，错误日志如下：
```
024-04-13T14:08:37Z ERR Unable to establish connection with Cloudflare edge error="TLS handshake with edge error: read tcp 172.17.0.5:35708->198.41.192.27:7844: i/o timeout" connIndex=1 event=0 ip=198.41.192.27
2024-04-13T14:08:37Z ERR Serve tunnel error error="TLS handshake with edge error: read tcp 172.17.0.5:35708->198.41.192.27:7844: i/o timeout" connIndex=1 event=0 ip=198.41.192.27
2024-04-13T14:08:37Z ERR Unable to establish connection with Cloudflare edge error="TLS handshake with edge error: read tcp 172.17.0.5:48800->198.41.192.77:7844: i/o timeout" connIndex=2 event=0 ip=198.41.192.77
2024-04-13T14:08:37Z INF Retrying connection in up to 1m4s connIndex=1 event=0 ip=198.41.192.27
2024-04-13T14:08:37Z ERR Unable to establish connection with Cloudflare edge error="TLS handshake with edge error: read tcp 172.17.0.5:34444->198.41.200.193:7844: i/o timeout" connIndex=0 event=0 ip=198.41.200.193
2024-04-13T14:08:37Z ERR Serve tunnel error error="TLS handshake with edge error: read tcp 172.17.0.5:48800->198.41.192.77:7844: i/o timeout" connIndex=2 event=0 ip=198.41.192.77
2024-04-13T14:08:37Z INF Retrying connection in up to 1m4s connIndex=2 event=0 ip=198.41.192.77
2024-04-13T14:08:37Z ERR Serve tunnel error error="TLS handshake with edge error: read tcp 172.17.0.5:34444->198.41.200.193:7844: i/o timeout" connIndex=0 event=0 ip=198.41.200.193
2024-04-13T14:08:37Z INF Retrying connection in up to 1m4s connIndex=0 event=0 ip=198.41.200.193
2024-04-13T14:08:43Z ERR Connection terminated error="TLS handshake with edge error: read tcp 172.17.0.5:48800->198.41.192.77:7844: i/o timeout" connIndex=2
2024-04-13T14:08:47Z ERR Connection terminated error="TLS handshake with edge error: read tcp 172.17.0.5:34444->198.41.200.193:7844: i/o timeout" connIndex=0
2024-04-13T14:08:55Z ERR Connection terminated error="TLS handshake with edge error: read tcp 172.17.0.5:35708->198.41.192.27:7844: i/o timeout" connIndex=1
```
从日志来看，网络连不上。怀疑被墙了，ping了一下对应的ip地址也能ping通，通过open clash日志也能看到是走的代理。但是一直连不上<br>
试了下将这个docker的访问全部走直连，居然成功连上了。