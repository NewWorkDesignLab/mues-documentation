# Installation

MUES is distributed as a Unity package from the
[MUES-Core](https://github.com/j0nes-L/MUES-Core) repository.

## Requirements

Before installing, make sure the following packages are present in your Unity project:

- **Meta All-in-One SDK** *(v.83)*
- **GLTFast** — `com.unity.cloud.gltfast`
- **Photon Fusion**
- **Photon Voice**

Both URP and BRP are supported.

## Install via Git URL (Package Manager)

1. Open **Window → Package Manager** in Unity.
2. Click the **+** button and choose **Add package from git URL…**.
3. Enter:

   ```
   https://github.com/j0nes-l/MUES-Core.git?path=/package
   ```

4. Click **Add**. Unity will download and import the package.

## Post-Install Configuration

### Fusion Network Config

Add `MUES-Core.Runtime` under **Assemblies to Weave** in the **Fusion Network Config**.

### Render While Loading Layer

If you want your avatar or other objects to be visible during loading, assign them the `MUES_RenderWhileLoading` layer.
