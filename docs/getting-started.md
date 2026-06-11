# Getting Started

This guide walks you through setting up a MUES session after [installing the package](installation.md).

## Overview

A MUES session consists of two roles:

- **Local host** — a physical-space user with a Meta headset who scans the room via MRUK.
- **Remote client** — a user who joins the session and sees a digital twin of the scanned room.

## Setup

1. Complete the [Installation](installation.md) steps, including the Fusion Network Config and layer setup.
2. Add `MUES-Core.Runtime` to the **Assemblies to Weave** list in your Fusion Network Config.
3. Place the MUES session prefab in your scene (see the API Reference for available entry points).
4. Assign any avatar or loading-screen objects the `MUES_RenderWhileLoading` layer so they remain visible during room sync.

## Where to go next

- Read the [Introduction](introduction.md) for the bigger picture.
- Explore the [API Reference](../api/index.md) for every public type and member.
