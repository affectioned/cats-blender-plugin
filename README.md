# Cats Blender Plugin (0.20.0)

A tool designed to shorten steps needed to import and optimize models into VRChat.
Compatible models are: MMD, XNALara, Mixamo, Source Engine, Unreal Engine, DAZ/Poser, Blender Rigify, Sims 2, Motion Builder, 3DS Max and potentially more.

With Cats it takes only a few minutes to upload your model into VRChat. All the hours long processes of fixing your models are compressed into a few functions!

[![](https://i.imgur.com/BFIald5.png)](https://www.patreon.com/catsblenderplugin)

#### Download: [Cats Blender Plugin](https://github.com/michaeldegroot/cats-blender-plugin/archive/master.zip)

---

## Blender compatibility

This fork is being updated to support the modern Blender LTS series. Upstream Cats was last updated for **Blender 2.93**; on newer Blender versions many features hit removed/renamed APIs and crash.

| Blender version | Status in this fork |
|---|---|
| **4.2 LTS** | Active development — load, import, Fix Model, decimation, eye tracking, visemes, combine materials confirmed; bake & atlas in progress |
| 3.6 LTS | Not yet retested (expected to work once 4.2 is solid) |
| 3.3 LTS | Not yet retested |
| 2.93 LTS | Last upstream-supported version; should still work |

See [`docs/changelog.md`](docs/changelog.md) for the per-fix list of fork-specific changes.

## Features

- Optimizing model with one click
- Creating lip syncing
- Creating eye tracking
- Automatic decimation (while keeping shape keys)
- Creating custom models easily
- Creating texture atlas
- Creating root bones for Dynamic Bones
- Optimizing materials
- Translating shape keys, bones, materials and meshes
- Merging bone groups to reduce overall bone count
- Auto updater

Full feature reference: [`docs/features.md`](docs/features.md).

## Requirements

- Blender **2.93 LTS or newer** (see compatibility table above). Running Blender as administrator is recommended on Windows.
- `mmd_tools` is **not required** — Cats ships with a vendored copy.
- If you use a system Python that Blender picks up, make sure `numpy` is installed there.

## Installation

1. Download the plugin zip: **[cats-blender-plugin](https://github.com/michaeldegroot/cats-blender-plugin/archive/master.zip)** — do **not** extract it.
2. Open Blender → `Edit → Preferences → Add-ons`.
3. Click `Install from Disk…` (on Blender 4.2 this is in the dropdown menu at the top-right of the Add-ons panel) and pick the zip.
4. Tick the checkbox next to "Cats Blender Plugin" in the add-ons list.
5. Open the 3D viewport's right sidebar (press `N`) and look for the **CATS** tab.

If you previously installed the upstream Cats and want to upgrade, remove the old version first from `Edit → Preferences → Add-ons` to avoid a stale-files conflict.

## Discord

Join the original Cats Discord for community help and bug reports: **https://discord.gg/f8yZGnv**

## Contributors

Original authors: GiveMeAllYourCats, Hotox. Code contributors: Shotariya, Neitri, Kiraver, Jordo, Ruubick, feilen.

## Feedback

Do you love this plugin or have you found a bug? Post a response in the Cats Discord and look for people with the developer role.

## Support upstream

If this plugin saves you countless hours of work, consider supporting the original authors on Patreon:

[![](https://i.imgur.com/BFIald5.png)](https://www.patreon.com/catsblenderplugin)
