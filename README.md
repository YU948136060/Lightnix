# Lightnix

<div align="center">

# ⚡ Lightnix

### The Operating System That Exists Only For Your Current Task

A task-oriented Linux distribution concept.

Boot a task.
Do one thing.
Then let the system disappear.

---

![Status](https://img.shields.io/badge/status-concept-blue)
![Buildroot](https://img.shields.io/badge/based%20on-Buildroot-green)
![License](https://img.shields.io/badge/license-GPL--2.0-orange)
![Contributions](https://img.shields.io/badge/contributions-welcome-brightgreen)

</div>

---

# Why?

Modern operating systems are designed to be ready for everything.

They load:

* countless services
* background processes
* desktop environments
* features you may never use

Lightnix explores the opposite idea.

> What if an operating system only existed for the task you are performing right now?

When you want to:

* watch videos
* write code
* play games
* browse the web

the system loads only the environment required for that task.

Nothing more.

---

# Vision

Operating systems should not be permanent.

They should behave like tools:

* appear when needed
* disappear when finished
* be instantly recoverable
* remain focused on a single purpose

Traditional systems:

```text
Boot
 ↓
Load Everything
 ↓
Run Everything
 ↓
Keep Everything Alive
```

Lightnix:

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

Imagine a boot menu like this:

```text
┌──────────────────────────────┐
│          Lightnix            │
├──────────────────────────────┤
│ ▶ Watch Videos               │
│ ▶ Minecraft                  │
│ ▶ Office                     │
│ ▶ Firefox                    │
│ ▶ Terminal                   │
└──────────────────────────────┘
```

Each entry launches a dedicated environment.

No full desktop startup.

No unnecessary services.

No historical baggage.

---

# Core Ideas

## ⚡ Fast by Design

Lightnix focuses on:

* minimal boot paths
* minimal dependencies
* minimal runtime overhead

Goals:

* near-instant startup
* task-oriented environments
* rapid recovery

---

## 🧩 Task-Oriented Systems

Each task owns its own environment:

```text
Video OS
Gaming OS
Coding OS
Office OS
```

Each environment has:

* dedicated root filesystem
* dedicated configuration
* dedicated software stack

while sharing a common runtime layer.

---

## 🔥 Memory-First Runtime

Ideal execution model:

```text
SquashFS
      ↓
tmpfs
      ↓
Run Entirely In Memory
```

Benefits:

* faster response
* fewer disk operations
* simplified runtime state

---

## 📸 Snapshot Everything

Save a working environment:

```bash
lx snapshot save coding
```

Restore it later:

```bash
lx snapshot restore coding
```

Like game save states for operating systems.

---

## 🔒 Minimal Attack Surface

Security through simplicity.

Planned technologies:

* Namespace Isolation
* seccomp Filtering
* Read-Only RootFS
* dm-verity Verification

Smaller systems naturally expose fewer attack surfaces.

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

   Video FS         Gaming FS         Office FS

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

# Planned Technology Stack

| Component    | Choice               |
| ------------ | -------------------- |
| Build System | Buildroot            |
| Kernel       | Linux LTS            |
| C Library    | musl libc            |
| Userland     | BusyBox              |
| Init System  | BusyBox Init / s6    |
| Graphics     | Wayland + Cage       |
| Isolation    | Namespaces + seccomp |
| Filesystem   | SquashFS + OverlayFS |
| Runtime      | tmpfs                |
| Snapshots    | Recipe-Based Overlay |

---

# Package Manager (Planned)

Lightnix intends to provide a declarative package manager:

```bash
lx install firefox

lx switch gaming

lx snapshot save coding

lx snapshot restore gaming

lx remove application
```

Conceptually:

```text
Recipe
   ↓
Buildroot
   ↓
RootFS
   ↓
Task Environment
```

---

# Roadmap

## Phase 1 — Foundation

* [ ] Buildroot prototype
* [ ] Minimal root filesystem
* [ ] SquashFS support
* [ ] OverlayFS integration

## Phase 2 — Task Environments

* [ ] Task launcher
* [ ] RootFS composer
* [ ] Shared runtime pool

## Phase 3 — Snapshots

* [ ] Snapshot engine
* [ ] Export and import
* [ ] Rollback support

## Phase 4 — Package Manager

* [ ] Recipe format
* [ ] Dependency resolution
* [ ] Automated builds

## Phase 5 — Hot Switching

* [ ] Runtime switching
* [ ] Session preservation
* [ ] Instant recovery

---

# Inspirations

Lightnix draws inspiration from:

* NixOS
* GNU Guix
* Tiny Core Linux
* Alpine Linux
* Fedora Silverblue
* Docker
* Podman
* Unikernel research
* LiveCD systems
* Game console snapshot systems

This project is not intended to replace them.

Instead, it explores a different direction.

---

# Origin Story

This project started late one night while experimenting with Buildroot.

A simple question appeared:

> Why must an operating system always exist?

What if:

* watching videos had its own OS
* coding had its own OS
* gaming had its own OS

I am not an operating system developer.

I do not claim to know all the implementation details.

But the idea felt exciting enough to write down.

Lightnix is the result of that thought experiment.

---

# Current Status

⚠️ Concept Stage

Lightnix is currently an idea and design proposal.

Many technical challenges remain unsolved:

* runtime switching
* filesystem composition
* snapshot architecture
* package management

The goal is to explore and discuss these possibilities.

---

# Contributing

Interested in:

* Buildroot
* Linux Kernel
* OverlayFS
* Namespaces
* Container runtimes
* Operating system design

Contributions, discussions, and ideas are welcome.

---

# Join Us

Many great systems started as crazy ideas.

Lightnix is one of them.

If you believe operating systems should be focused, disposable, and task-oriented—

join the discussion.

Let's see where this idea leads.

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
