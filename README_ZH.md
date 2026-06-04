# Lightnix

<div align="center">

# ⚡ Lightnix

### The Operating System That Exists Only For Your Current Task

**一个面向任务的 Linux 发行版构想**

启动一个系统。  
完成一个任务。  
然后让它消失。

---

![Status](https://img.shields.io/badge/status-concept-blue)
![Buildroot](https://img.shields.io/badge/based%20on-Buildroot-green)
![License](https://img.shields.io/badge/license-GPL--2.0-orange)
![Contributions](https://img.shields.io/badge/contributions-welcome-brightgreen)

</div>

---

# Why?

现代操作系统为了满足所有需求而存在。

它们需要：

- 加载大量服务
- 长时间驻留后台
- 维护复杂状态
- 为所有可能的任务做好准备

Lightnix 的想法恰恰相反。

> 如果一个操作系统只为当前任务而存在，会怎样？

当你想：

- 看视频
- 写代码
- 玩游戏
- 浏览网页

系统只加载该任务所需的最小环境。

任务结束。

系统消失。

---

# Vision

我们认为：

操作系统不应该是永远运行的庞然大物。

它应该像工具一样：

- 需要时出现
- 不需要时离开
- 可以随时恢复
- 永远专注于当前任务

---

传统操作系统：

```text
Boot
 ↓
Load Everything
 ↓
Run Everything
 ↓
Keep Everything Alive
```

Lightnix：

```text
Choose Task
 ↓
Compose Environment
 ↓
Do One Thing
 ↓
Disappear
```

---

# Concept

设想这样一个启动菜单：

```text
┌──────────────────────────────┐
│          Lightnix            │
├──────────────────────────────┤
│ ▶ Watch Bilibili             │
│ ▶ Minecraft                  │
│ ▶ Office                     │
│ ▶ Firefox                    │
│ ▶ Terminal                   │
└──────────────────────────────┘
```

选择一个任务。

系统只加载对应环境。

无需等待完整桌面。

无需启动无关服务。

无需携带历史包袱。

---

# Core Ideas

## ⚡ Fast by Design

Lightnix 不追求功能最多。

而追求：

- 最小启动路径
- 最小依赖集合
- 最小资源占用

目标：

- 亚秒级系统准备
- 秒级进入任务环境
- 接近即时恢复

---

## 🧩 Task-Oriented Systems

每个功能都是一个独立环境：

```text
Bilibili OS
Minecraft OS
Office OS
Firefox OS
```

它们拥有：

- 独立 RootFS
- 独立配置
- 独立运行环境

但共享基础运行时。

---

## 🔥 Memory-First Runtime

Lightnix 的理想运行模式：

```text
SquashFS
      ↓
tmpfs
      ↓
Run In Memory
```

整个系统在内存中运行。

获得：

- 更快响应
- 更少磁盘访问
- 更简单状态管理

---

## 📸 Snapshot Everything

每个环境都可以被保存。

```bash
lx snapshot save coding
```

随后：

```bash
lx snapshot restore coding
```

恢复到之前的状态。

如同游戏存档。

---

## 🔒 Minimal Attack Surface

安全性来自于：

- 更少组件
- 更少服务
- 更少后台进程
- 更小 RootFS

而不是更多安全软件。

目标包括：

- Namespace Isolation
- seccomp Filtering
- Read-only RootFS
- dm-verity Verification

---

# Architecture

```text
                       User
                         │
                         ▼

              ┌──────────────────┐
              │  Task Selector   │
              └──────────────────┘
                         │
                         ▼

              ┌──────────────────┐
              │ RootFS Composer  │
              └──────────────────┘
                         │

      ┌──────────────────┼──────────────────┐
      ▼                  ▼                  ▼

 Bilibili FS      Minecraft FS       Office FS

      └──────────────────┼──────────────────┘
                         ▼

                Shared Runtime Pool

                    BusyBox
                    musl libc
                    Wayland

                         ▼

                   Linux Kernel
```

---

# Technology Stack

| Component | Planned Choice |
|------------|----------------|
| Build System | Buildroot |
| Kernel | Linux LTS |
| C Library | musl libc |
| Userland | BusyBox |
| Init System | BusyBox Init / s6 |
| Graphics | Wayland + Cage |
| Isolation | Namespaces + seccomp |
| Filesystem | SquashFS + OverlayFS |
| Runtime | tmpfs |
| Snapshots | Recipe-based Overlay |

---

# Package Manager (Planned)

Lightnix 计划提供声明式包管理器：

```bash
lx install bilibili

lx switch minecraft

lx snapshot save coding

lx snapshot restore gaming

lx remove wechat
```

每个软件实际上都是：

```text
Recipe
   ↓
Buildroot
   ↓
RootFS
   ↓
Task Environment
```

用户无需关心构建细节。

---

# Runtime Layout

```text
/
├── common
├── etc
├── home
├── media
├── mnt
├── opt
└── var
```

说明：

| Directory | Purpose |
|------------|------------|
| common | Shared binaries and libraries |
| etc | Configuration overlays |
| home | Persistent user data |
| media | Device mounts |
| mnt | Mount points |
| opt | Task-specific files |
| var | Runtime data |

---

# Roadmap

## Phase 1 — Foundation

- [ ] Buildroot Prototype
- [ ] Minimal RootFS
- [ ] SquashFS Integration
- [ ] OverlayFS Support

---

## Phase 2 — Task System

- [ ] Task Launcher
- [ ] Environment Composer
- [ ] Shared Runtime Pool

---

## Phase 3 — Snapshots

- [ ] Snapshot Engine
- [ ] Export / Import
- [ ] Version Rollback

---

## Phase 4 — Package Manager

- [ ] Recipe Format
- [ ] Dependency Resolution
- [ ] Automatic Builds

---

## Phase 5 — Hot Switching

- [ ] Runtime Environment Switching
- [ ] Instant Recovery
- [ ] Session Preservation

---

# Inspirations

Lightnix 受到以下项目启发：

- NixOS
- GNU Guix
- Tiny Core Linux
- Alpine Linux
- Fedora Silverblue
- Docker
- Podman
- Unikernel Research
- LiveCD Systems
- Game Console Snapshot Systems

它并不是上述项目的替代品。

而是一次不同方向的探索。

---

# Origin Story

这个项目诞生于一个深夜。

当时我正在折腾 Buildroot。

突然冒出一个问题：

> 为什么操作系统必须永远存在？

如果：

- 看视频有自己的系统
- 写代码有自己的系统
- 玩游戏有自己的系统

会怎样？

我并不是操作系统开发者。

我甚至不了解许多底层实现细节。

但这个想法让我兴奋。

于是我把它记录下来。

这就是 Lightnix 的起点。

---

# Current Status

⚠️ Lightnix 目前仍处于概念设计阶段。

这是一个正在寻找实现路径的系统构想。

许多技术方案仍需验证：

- 热切换是否可行
- RootFS 组合效率如何
- Snapshot 机制如何设计
- 包管理器如何实现

欢迎一起探索。

---

# Contributing

如果你对以下领域感兴趣：

- Buildroot
- Linux Kernel
- OverlayFS
- Namespace
- Container Runtime
- Init Systems
- Operating System Design

欢迎参与讨论。

任何想法、Issue 或 Pull Request 都非常欢迎。

---

# Join Us

许多伟大的系统项目，

最开始都只是一个疯狂的想法。

Lightnix 也是。

如果你觉得：

> “操作系统应该只为当前任务而存在”

那么欢迎加入。

让我们一起看看这个想法最终会走到哪里。

---

# License

Core Code

```text
GPL-2.0-only
```

Recipes

```text
CC0
```

---

<div align="center">

### ⚡ Lightnix

The Operating System That Exists Only For Your Current Task

</div>
