---
title: Architecture
description: Understanding Amplifier's architecture
---

# Architecture

Amplifier follows a Linux kernel-inspired architecture where a tiny, stable core provides mechanisms while all features live at the edges as replaceable modules.

## Core Principle

> **"The center stays still so the edges can move fast."**

## Topics

<div class="grid">

<div class="card">
<h3><a href="overview.md">Overview</a></h3>
<p>High-level architecture and component relationships.</p>
</div>

<div class="card">
<h3><a href="kernel.md">Kernel Philosophy</a></h3>
<p>Why the kernel is tiny, stable, and boring.</p>
</div>

<div class="card">
<h3><a href="modules.md">Module System</a></h3>
<p>How modules are discovered, loaded, and coordinated.</p>
</div>

<div class="card">
<h3><a href="mount_plans.md">Mount Plans</a></h3>
<p>The configuration contract between apps and kernel.</p>
</div>

<div class="card">
<h3><a href="events.md">Event System</a></h3>
<p>Canonical events and observability.</p>
</div>

</div>

## Quick Architecture Overview

```
┌─────────────────────────────────────────────────────────────┐
│  Application Layer (amplifier-app-cli)                      │
│  • Resolves configuration → Creates Mount Plans             │
│  • Provides approval/display systems                        │
└──────┬──────────────────────────────────────────────────────┘
       │
       ▼
┌─────────────────────────────────────────────────────────────┐
│  Kernel (amplifier-core) - ~2,600 lines                     │
│  • Validates Mount Plans                                    │
│  • Loads modules via entry points                           │
│  • Coordinates session lifecycle                            │
│  • Emits canonical events                                   │
└──────┬──────────────────────────────────────────────────────┘
       │
       ▼
┌─────────────────────────────────────────────────────────────┐
│  Modules (Userspace)                                        │
│  • Providers: LLM backends                                  │
│  • Tools: Agent capabilities                                │
│  • Orchestrators: Execution loops                           │
│  • Contexts: Memory management                              │
│  • Hooks: Observability & control                           │
└─────────────────────────────────────────────────────────────┘
```

## Key Concepts

| Concept | Description |
|---------|-------------|
| **Kernel** | Ultra-thin core providing mechanisms only |
| **Module** | Swappable component implementing a contract |
| **Mount Plan** | Configuration specifying which modules to load |
| **Event** | Observable occurrence in the system |
| **Hook** | Module that observes/controls events |
| **Session** | Single conversation lifecycle |
| **Coordinator** | Infrastructure context for modules |
