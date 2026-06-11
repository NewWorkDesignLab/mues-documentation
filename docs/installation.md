# Installation

MUES is distributed as a Unity package from the
[MUES-Core](https://github.com/j0nes-L/MUES-Core) repository.

## Install via Git URL (Package Manager)

1. Open **Window → Package Manager** in Unity.
2. Click the **+** button and choose **Add package from git URL…**.
3. Enter the repository URL:

   ```
   https://github.com/j0nes-L/MUES-Core.git
   ```

4. Click **Add**. Unity will download and import the package.

## Install via manifest.json

Add the following entry to your project's `Packages/manifest.json`:

```json
{
  "dependencies": {
    "org.nwdl.mues": "https://github.com/j0nes-L/MUES-Core.git"
  }
}
```

> [!TIP]
> Replace `org.nwdl.mues` with the actual package name from the package's
> `package.json`, and pin a specific version or commit with `#<tag-or-commit>`
> for reproducible builds.

## Requirements

- Unity version: _document the minimum supported version here._
- Dependencies: _list any required packages here._
