---
title: User Guide
description: Complete guide to using Amplifier
---

# User Guide

This guide covers everything you need to know to use Amplifier effectively.

## Topics

<div class="grid">

<div class="card">
<h3><a href="cli/">CLI Reference</a></h3>
<p>Complete reference for all Amplifier commands and options.</p>
</div>

<div class="card">
<h3><a href="profiles/">Profiles</a></h3>
<p>Pre-configured capability sets for different use cases.</p>
</div>

<div class="card">
<h3><a href="agents/">Agents</a></h3>
<p>Specialized sub-agents for focused tasks.</p>
</div>

<div class="card">
<h3><a href="sessions/">Sessions</a></h3>
<p>Session management, persistence, and resumption.</p>
</div>

<div class="card">
<h3><a href="collections/">Collections</a></h3>
<p>Shareable bundles of profiles, agents, and context.</p>
</div>

</div>

## Quick Reference

### Most Common Commands

```bash
# Run a single command
amplifier run "Your prompt"

# Interactive mode
amplifier

# Resume last session
amplifier continue

# List sessions
amplifier session list
```

### Configuration Commands

```bash
# Profiles
amplifier profile list
amplifier profile use dev

# Providers
amplifier provider list
amplifier provider use anthropic

# Modules
amplifier module list
amplifier module add tool-web
```

### Getting Help

```bash
# General help
amplifier --help

# Command-specific help
amplifier run --help
amplifier session --help
```
