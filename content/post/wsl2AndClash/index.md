---
title: "Wsl2 配置 Clash 代理"
date: 2022-07-29T21:45:07+08:00
draft: false
image: "pic/clash.jpg"
categories:
    - Linux
tags:
    - clash
    - wsl
    - proxy
    - command
---

不是直接在虚拟机里安装["Clash for linux"](https://github.com/Dreamacro/clash)而是直接使用宿主机的clash代理，也就是只在Windows上打开代理。

# clash设置

允许局域网连接，并记下端口号`7890`。
![允许局域网连接](pic/allowLan.png)

## 开启系统代理
一般配置系统代理都是使用回环地址 `127.0.0.1` 但是WSL不行，需要改成WSL的IP地址。

```bash
# 设置clash代理
# 自动获取IP地址
host_ip=$(cat /etc/resolv.conf |grep "nameserver" |cut -d " " -f 2)
export ALL_PROXY="http://$host_ip:7890"
```

是个环境变量，所以写进`.bashrc`即可自动添加。
## 自动获取IP地址

`cat /etc/resolv.conf |grep "nameserver" |cut -d " " -f 2`
![获取IP](pic/reslov.png)

## 注意

`ping`命令不会使用代理，所以`ping google.com`此时也是`ping`不通的。可以使用`curl`命令来测试。
![curl](pic/curl.png)
