---
title: shadowsocks
date: 2017-11-11 20:37:35
tags:
---
### shadowsocks
> vsp 部署(我这里是ubuntu17.10)

```
sudo apt-get update
sudo apt-get install shadowsocks-libev
```
> 配置文件/etc/shadowsocks-libev/config.json  
<!--more-->
```
{
	"server":"example.com or X.X.X.X",
	"server_port":443,
	"password":"password",
	"method":"aes-128-gcm",
	"timeout":60
}   
#server：主机域名或者IP地址，尽量填IP
#server_port：服务器监听端口
#password：密码
#method：加密方式 所有支持的加密方式请参照官方文档。这里本人推荐只使用支持AEAD的加密方式，包括以下五种：
#aes-128-gcm/aes-192-gcm/aes-256-gcm/chacha20-ietf-poly1305/xchacha20-ietf-poly1305
```
> start  

```
service shadowsocks-libev restart
```
[upstring](https://cokebar.info/archives/767)
---

> local config(archlinux)  

```
sudo pacman -S shadowsocks-libev
sudo nano /etc/shadowsocks/config.json
ss-local -c /etc/shadowsocks/config.json
```
> config.json  

```
{
    "server":"45.63.121.6",
    "server_port":8388,
    "local_address":"127.0.0.1",
    "local_port":1081,
    "password":"MuptOghi",
    "timeout":60,
    "method":"chacha20-ietf-poly1305"
}
```
