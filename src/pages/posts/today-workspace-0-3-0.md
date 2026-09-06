---
layout: ../../layouts/PostLayout.astro
title: "Today Workspace 0.3.0：从想法到第一个 Android Beta"
description: "第一次完整走通产品设计、本地优先、云同步、认证、Android 和 CI/CD。"
date: 2026-09-05
categories:
  - building
  - engineering
  - project
---

这次开发最值得记录的，不是某一个功能，而是第一次完整走通了一个产品从想法到正式发布包的全过程：

```text
产品设计
→ 本地数据
→ 云同步
→ 用户认证
→ PWA
→ Android
→ CI/CD
→ 正式签名
→ APK / AAB
```

Today Workspace 0.3.0 最终变成了一个真正可以安装、登录、同步数据，并且能够持续升级的 Android Beta。

## 从一个很小的想法开始

我想做的并不是另一个复杂的 Notion，而是一个足够轻量的个人工作台：Today、Notes、Tasks。

产品原则逐渐收束成：

```text
Capture first
Today first
Local first
Mobile first
```

重点不是功能数量，而是让记录和处理当天事情足够自然。

## 第一次真正理解 Local-first

一开始数据主要存在 IndexedDB。后来为了支持多设备同步，数据开始拥有 `updatedAt`、`version`、`userId`、`deviceId`、`deletedAt` 和 `syncStatus` 等字段。

这里我第一次真正从业务问题理解 Soft Delete / Tombstone。

如果设备 A 删除一条 Note 后服务器直接彻底删掉，设备 B 下一次同步时并不知道“发生过删除”。保留 `deletedAt` 后，删除本身也可以成为一次可同步的状态变化。

Outbox 也是类似的体验。

用户操作不会等待服务器：

```text
用户操作
↓
先写 IndexedDB
↓
界面立即更新
↓
写入 Outbox
↓
后台同步云端
```

网络暂时断开时，应用仍然可用。

这让我开始真正理解一句话：本地数据库才是用户交互的第一现场，云端负责同步，而不是阻塞用户操作。

## 接入 Supabase 之后，软件第一次拥有了“云”

接入 Supabase 后，架构变成：

```text
设备 A
  ↓
IndexedDB
  ↓
Outbox
  ↓
Supabase
  ↑
同步
  ↑
设备 B
```

最有感觉的一刻其实很普通：设备 A 新建一条 Note，上传云端，另一台设备登录以后它出现了。

这意味着项目第一次从“只存在于这台浏览器里的网页”，变成了“拥有账户和云端数据的软件”。

同时，RLS 也让我重新确认：前端隐藏按钮不是权限控制，真正的权限必须落在后端、数据库或服务端。

## 从 PWA 到 Android

Web 版本之后，我又把 Vite、PWA、Capacitor、Android SDK 和 Gradle 串了起来：

```text
JavaScript / HTML / CSS
↓
Vite Build
↓
dist/
↓
Capacitor
↓
Android Project
↓
Gradle
↓
APK
```

这里也踩到一个很典型的认知坑：PWA 的 IndexedDB 和 Android WebView 的 IndexedDB 并不是同一个存储容器。

真正让 PWA 与 APK 数据互通的，不是“数据库名字一样”，而是 Cloud Sync。

## CI/CD 让发布第一次变得可重复

Android 构建最终进入 GitHub Actions：

```text
Push / Release
↓
GitHub Runner
↓
npm install
↓
Vite Build
↓
Capacitor Android
↓
Gradle Build
↓
APK / AAB
```

这让我第一次强烈感受到“我的电脑能编译”和“任何一次 Release 都能按相同流程重新构建”之间的差别。

后者才更接近真正的软件工程。

## 技术开始从术语变成解决问题的方法

这次项目把很多以前孤立的概念连接了起来：Local-first、Offline-first、Outbox、Soft Delete、RLS、Auth、Capacitor、Gradle、App Signing、GitHub Actions、Vercel。

以前我会问：Outbox 是什么？为什么需要 RLS？为什么 APK 要签名？

现在这些问题都曾经真实地出现在开发过程中。

技术知识开始从“我知道这个词”，变成“我知道它为什么存在”。

0.3.0 不是终点。

它更像是 Today Workspace 真正意义上的第一个起点。