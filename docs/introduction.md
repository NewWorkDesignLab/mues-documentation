# Introduction

**MUES-Core** is a modular Unity package that enables seamless mixed-reality sessions between on-site and remote teams. It synchronizes physical and virtual spaces to create a shared spatial context.

> [!NOTE]
> This project is still a Work in Progress. If you encounter bugs, feel free to open an issue!

## How it Works

1. **Scan:** The local host scans their physical room using the **Meta MR Utility Kit (MRUK)**.
2. **Sync:** Geometry data is serialized and distributed at runtime to remote clients via **Photon Fusion**.
3. **Interact:** Remote users appear in an abstract digital twin of the real room. This ensures precise alignment between the remote user's virtual position and the local user's physical Passthrough view.

## Tech Stack

| Layer | Technology |
|---|---|
| Networking | Photon Fusion (State Transfer) |
| Audio | Photon Voice (VoIP) |
| Spatial Computing | Meta MR Utility Kit (MRUK) |

> Future plans include implementing AI-based reconstruction for photorealistic environment sharing.

## Next steps

- [Install the package](installation.md)
- [Get started](getting-started.md)
- [Browse the API Reference](../api/index.md)
