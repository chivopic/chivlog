---
layout: ../../layouts/PostLayout.astro
title: "Tailscale：把所有设备连成一个私人局域网"
description: "一个几乎不用折腾配置的 WireGuard 虚拟局域网，适合多设备开发、远程 SSH 和 Home Lab。"
date: 2026-09-06
type: tool
source: https://tailscale.com
note: "把所有设备拉进一个私人虚拟局域网，很适合多设备开发、远程 SSH 和 Home Lab。"
categories:
  - inbox
  - tools
  - networking
---

Tailscale 可以简单理解成：

> **给你所有设备建立一个跨互联网的私人局域网。**

它底层基于 WireGuard，把 Mac、Windows、Linux、手机、NAS、云服务器等设备拉进同一个虚拟网络。哪怕这些设备分别在宿舍、学校、公司或云端，也可以像处在同一个 Wi-Fi 下一样互相访问。

## 为什么有意思

传统远程访问经常要处理：

- 公网 IP
- 端口转发
- DDNS
- NAT
- 防火墙
- SSH 端口暴露

Tailscale 会把这些麻烦大幅隐藏掉。设备加入同一个 tailnet 后，会获得稳定的虚拟地址，也可以配合 MagicDNS 直接通过设备名访问。

例如：

```bash
ssh chiv@omarchy
```

而不是先去查公网 IP、做端口映射，再把 SSH 暴露到公网。

## 一个很适合我的场景

```text
MacBook Air
   │
   ├── SSH → Omarchy / Windows / WSL
   ├──访问 → 本地开发服务
   └──访问 → 云服务器 / NAS / Home Lab
```

这样在图书馆、宿舍或者外面，只要设备联网，就可以继续访问自己的开发环境。

## 本地开发也很好用

比如 Omarchy 上运行：

```bash
npm run dev
```

本来只能通过：

```text
localhost:3000
```

访问。

接入 Tailscale 后，可以直接从 Mac、手机或平板访问这台机器对应的 Tailscale 地址，不需要为了测试一个页面就先部署到 Vercel。

## Home Lab

以后如果自己搭：

- PostgreSQL
- Redis
- Grafana
- Docker
- Kubernetes
- Ollama / vLLM
- AI Agent Server
- NAS

这些服务完全可以只开放给 Tailscale 网络，而不是暴露到公网。

例如数据库更理想的状态是：

```text
公网：
❌ 1.2.3.4:5432

Tailscale：
✅ postgres-server:5432
```

## Exit Node

Tailscale 还可以让某台设备成为 Exit Node：

```text
Mac
 ↓
Tailscale
 ↓
家里的电脑
 ↓
Internet
```

这时 Mac 的网络流量可以从那台机器出去，行为会更接近传统 VPN。

## Tailnet

Tailscale 里有一个核心概念：**tailnet**。

它就是属于自己的 Tailscale 私有网络：

```text
my tailnet

MacBook Air       100.x.x.1
Omarchy PC        100.x.x.2
Phone             100.x.x.3
Server            100.x.x.4
NAS               100.x.x.5
```

这些地址不是公网 IP，而是设备之间使用的稳定虚拟地址。

## 和其他工具的区别

| 工具 | 主要用途 |
| --- | --- |
| WireGuard | VPN 协议本身 |
| Tailscale | 自动化 WireGuard + 身份 + NAT 穿透 + 访问控制 |
| Cloudflare Tunnel | 把 Web 服务安全暴露给外部访问 |
| ngrok | 临时暴露 localhost |
| ZeroTier | 类似的虚拟网络方案 |
| 普通 VPN | 主要让流量经过 VPN Server 出口 |

## 一句话记忆

> **Tailscale = 给自己的所有设备创建一个跨互联网、加密、几乎零配置的私人局域网。**

最值得先尝试的一步，就是把 MacBook 和 Omarchy 主机加入同一个 tailnet，然后直接从 Mac：

```bash
ssh omarchy
```

如果这个体验顺手，之后再逐步把云服务器、NAS、开发服务和 Home Lab 都接进来。
