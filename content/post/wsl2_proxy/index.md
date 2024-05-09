---
title: "WSL2 配置代理"
date: 2024-04-22T09:43:46+08:00
draft: false
categories:
    - Linux
tags:
    - clash
    - wsl
    - proxy
    - command
---

# wsl2使用主机的代理

更新后的WSL2在启动时会有这样的提示"NAT 模式下的 WSL 不支持 localhost 代理。", 原因是现在的wsl2支持修改代理模式, 修改成自动代理模式就可以直接使用主机的代理, 具体修改方式参考下面的链接。

> 参考: [github issues](https://github.com/microsoft/WSL/issues/10753#issuecomment-1814839310)

在`文件资源管理器`中输入`%UserProfile%`, 在该目录中的`.wslconfig`文件里添加以下内容(如果没有这个文件就新建一个)。


``` .wslconfig
[wsl2]
networkingMode=mirrored
dnsTunneling=true
firewall=true
autoProxy=true

[experimental]
# requires dnsTunneling but are also OPTIONAL
bestEffortDnsParsing=true
useWindowsDnsCache=true
```

设置完后, 重启wsl2, 提示消失, 并且可以直接使用主机的clash代理。
