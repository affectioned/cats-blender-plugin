# Changelog

## 0.21.0 — 2026-05-27 (this fork)

- Updater: point release/dev URLs at the affectioned fork
  
## 0.20.0 — 2026-05-27 (this fork)

Compatibility work for Blender 4.0–4.2 LTS. Original upstream targets 2.93.

- Added `.github/workflows/release.yml`: tag pushes (`v0.20.0` or bare `0.20.0`) build a zipped addon and draft a GitHub release with auto-generated notes. The workflow verifies that the tag matches `bl_info['version']` before building.
- Added `tools/common.iter_objects()` that filters None entries from `view_layer.objects`. Converted `unselect_all`, `remove_unused_objects`, and `remove_no_user_objects` to use it. The `select()` None guard stays as defense-in-depth.
- Restructured `tools/bake.py` `swap_links` to fall back to a per-operator `_parked_inputs` dict when the scratch socket is missing on this Blender version (e.g. `"Transmission Roughness"`, removed in 4.0). Without this, the paired forward/reverse swap silently no-ops while the in-between `set_values` still mutates the primary socket, permanently corrupting Metallic/Specular values on every alpha/metallic/smoothness bake.
- Added `'Anisotropic'` to the Principled BSDF candidate map so the bake's anisotropic-rotation parking still resolves on Blender 4.0+ regardless of which naming variant ships.
- Narrowed the `except (TypeError, AttributeError)` in the bake-material default-copy block to `except TypeError` (the AttributeError branch was unreachable after the explicit None check), and added a debug log so type-mismatch skips are visible during debugging.
- Snapshot `pose.bone_groups` via `list()` before the remove loop in Fix Model. Iterating a `bpy_prop_collection` while calling `.remove()` on it skips every other entry; previously up to half the groups were left behind on Blender 2.93–3.x.
- Filter out None emission sockets in autodetect_passes and guard `tree.links.new` when `_get_emission_input` returns None.

- Filter `WindowManager.addon_support` to enum's valid identifiers (`TESTING` removed in 4.2).
- Principled BSDF input renames (4.0): added shared `get_principled_input` / `set_principled_input` helpers in `tools/common.py` covering `Emission` → `Emission Color`, `Specular` → `Specular IOR Level`, `Clearcoat*` → `Coat*`, `Transmission` → `Transmission Weight`, `Sheen Tint` → `Sheen Weight`, `Subsurface` → `Subsurface Weight`. Routed `bake.py` `swap_links` / `set_values` / `_get_emission_input` and `common.py` `combine_mats` / `add_principled_shader` through the helpers. Sites missing on the current Blender version are skipped silently.
- Guarded `Mesh.use_auto_smooth` / `auto_smooth_angle` behind `hasattr` (removed in 4.0; custom split normals are honored unconditionally on 4.0+).
- Guarded `EditBone.layers[0]` assignment behind `hasattr` (4.0 replaced bone layers with bone collections).
- Guarded `pose.bone_groups` iteration behind `hasattr` (removed in 4.0).
- Added missing `hasattr(scene, 'layers')` guard around child-mesh deletion in `Fix Model` (pre-existing 2.80 bug surfaced by 4.x testing).
- Skip `None` entries in `select()` — Blender 4.x's `view_layer.objects` can yield `None` for slots whose object was deleted during the same operation.
- Cached `EditBone` names before leaving edit mode in `eyetracking.py` — references invalidate the moment mode changes and on 4.2 the underlying memory may contain non-UTF-8 bytes that raise `UnicodeDecodeError`.
- Guarded `BakeSettings.use_pass_ambient_occlusion` behind `hasattr` (removed in 4.0; AO is now its own bake type).
- Fixed `bpy.ops.uv.smart_project(angle_limit=66.0)` — 3.0 switched the unit from degrees to radians, so the old value effectively disabled the angle limit.
- Wrapped all `invoke_props_dialog(width=dpi_value * X)` call sites in `int(...)` — 4.x became strict about int vs float for `width`.

## 0.19.0

- **Fully compatible with Blender 2.93**
- **Translations:**
  - **Added Korean translation!**
    - Cats is now translated into Korean by a large portion
    - To use it, simply change your Blender language to Korean and then restart Blender or select it in the Cats Settings
    - Thanks to **Siromori** for contributing the translation! <3
  - Added Cats Ui Language setting
    - This lets you choose in which language Cats should be displayed
    - Setting it to "auto" will choose the current Blender language
  - Added button to download the latest Cats Translations
    - This feature is for translators to test their translations in the plugin
    - If you want to help to translate Cats into any language, please let me (Hotox) know in our Discord
- **Model Options:**
  - Added "Connect Bones" button
  - Added options to keep merged bones and to merge the bones of visible meshes only
- **Custom Model Creation:**
  - Reworked "Attach Mesh" feature, it is much more reliable now
- **General:**
  - Fixed translation errors
  - Updated mmd_tools
- **Bake: (by feilen)**
  - Emission influence baking: fake realtime lighting based on your emissive channel, quest-compatible!
  - 'Manual' reprojection mode for Bake: creating new UV maps called 'Target' will allow you to re-bake to a specific layout.
  - 'Optimize static shapekeys' option
    - Splits your mesh into two skinned meshes, one with all shapekey-influenced geometry,
      one with the rest (and fixes the normals in place). Significantly improves GPU performance, especially when a lot of shapekeys are in effect.
      Needs the lighting anchor point in Unity to be set to the armature Hips on both, or you'll get lighting artifacts.
  - Introduce 'BakeFixer.cs', which is a run-time unity script that hopefully should do the lighting work for you.
  - 'Ignore hidden objects' option
    - When baking, this will ignore any objects you currently have hidden, making it easier to create different versions of your avatar.
  - Apply Current Shapekey Mix option
    - Sets your basis to whatever current mix of shapekeys you have. Always-on shapekeys are terrible for performance,
      so if you have some that are only intended to customize the character without updates, this will help with that.
  - '_bake' shapekeys: any shapekey with '_bake' at the end will be applied and completely removed, allowing the static shapekeys option to work better.
    If you're an avatar creator distributing bases, this is recommended for character customization keys!
  - Misc: Updated defaults to be in line with updated Quest limits.

## 0.18.0

- **Added Bake Panel!**
  - This is a non-destructive way to produce an optimized variant of (almost) any avatar!
  - Full credit goes to **feilen**! Thanks so much for this awesome feature <3
  - Check out the wiki for more information: https://github.com/GiveMeAllYourCats/cats-blender-plugin/wiki/Bake
- **Added Smart Decimation!**
  - This lets you decimate without loosing any shapekeys!
  - Full credit goes to **feilen**! Tons of thanks for this awesome feature as well <3
- **Added Japanese translation!**
  - Cats is now almost fully translated into Japanese
  - To use it simply change your Blender language to Japanese and then restart Blender
  - Full credit goes to **Jordo** and **Ruuubick**! Thank you so much <3
  - If you want to help translating Cats into any language, please us know!
- **General:**
  - Cats is now fully compatible with Blender 2.90 and 2.91
  - Added "Show mmd_tools tabs" option to Settings
    - This allows you show and hide the "MMD" and "Misc" tabs added by the mmd_tools plugin
  - Added button to "Start/Stop Pose Mode" which starts/stops pose mode without resetting the current pose
  - Changed link to a new vrm importer since the old one dropped support
  - Fixed Google Translations no longer working
  - Fixed bug in "Apply as Rest Pose" and "Pose to Shape Key" in Blender 2.90
  - More fixes for Blender 2.90
  - NOTE: Using Cats in Blender 2.90+ on Ubuntu might cause Blender to crash on load (caused by mmd_tools)
    - To fix this use a Blender version prior to 2.90 or try updating your drivers

## 0.17.0

- **Cats is now fully compatible with Blender 2.83!**
  - *It was compatible with 2.82 all long*
- **Fix Model:**
  - Added "Keep Twist Bones" option to Fix Model
    - This will keep any bone containing 'Twist'
  - Added "Fix MMD Twist Bones" option to Fix Model
    - This will apply a fix to make the MMD arm twist bones usable **(Thanks Rokk!)**
    - You do not need to enable "Keep Twist Bones" for this to work
  - Added "Remove Rigidbodies and Joints" option to Fix Model
    - This is solely intended for our non-VRChat users
  - Added compatibility to more models
  - Disabling the option "Remove Zero Weight Bones" now also keeps unused vertex groups
- **Importer:**
  - Imported meshes from VRM files now get automatically parented to their armature
  - Imported armatures now always show their bones in front and in wire mode
  - Fixed export warning being empty
  - Fixed importer error when the FBX importer was not enabled
  - Fixed importer error when a zip file contained another zip file
  - When importing a model, objects of a new scene now only get deleted if all three of them are present
- **Custom Model Creation:**
  - Added "Remove Zero Weight Bones" option to Merge Armatures
- **Decimation:**
  - Added "Remove Doubles" option
- **General:**
  - Fixed some bugs
  - Fixed objects getting unhidden when doing any cats operation in 2.80+
  - Updated mmd_tools

Read the full historical changelog [on the releases page](https://github.com/michaeldegroot/cats-blender-plugin/releases).
