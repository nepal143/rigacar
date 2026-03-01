# Rigacar — Blender 4.x / 5.x Compatibility Fix

> *"Rigacar was broken in Blender 4+ due to removal of the legacy action/fcurve API. This version fully migrates it to Blender's layered animation system (action slots, channelbags) while maintaining backward compatibility with Blender 4.0–4.3 via runtime version detection."*

**Original Author:** David Gayerie
**Fix By:** Nepal Singh
**Supported Blender Versions:** 4.0, 4.1, 4.2, 4.3, 4.4, 5.0+

---

## What Is Rigacar?

A Blender addon that generates a deformation rig for vehicles, with automatic wheel rotation and steering animation baking.

## Why This Fork?

The original Rigacar addon was written for Blender 2.83. Blender 4.0+ introduced breaking changes to the animation API:

- **Blender 4.0–4.1:** `nla.bake` replaced by `bpy_extras.anim_utils.bake_action()` with keyword arguments
- **Blender 4.2+:** `bake_action()` requires a `BakeOptions` dataclass
- **Blender 4.4+:** Action slots, layers, strips, and channelbags for F-Curve access
- **Blender 5.0:** `action.fcurves` legacy API removed entirely

This fork adds **runtime version detection** so the same code works across all 4.x+ versions.

## What Was Changed

### `bake_operators.py`

| Change | Details |
|---|---|
| **Version detection** | `HAS_ACTION_SLOTS` and `HAS_BAKE_OPTIONS` flags for runtime API branching |
| **FCurve access** | 4.0–4.3: `action.fcurves`; 4.4+/5.0: `channelbag.fcurves` via action slots |
| **FCurve creation** | 4.0–4.3: `action_group=`; 4.4+: `group_name=` |
| **Action slots** | Only created on Blender 4.4+ |
| **`bake_action()`** | `BakeOptions` (4.2+) or keyword args (4.0–4.1) |

### `__init__.py`

- Minimum Blender version set to `(4, 0, 0)`
- Updated addon name and author credit

## Installation

1. Download or clone this repo
2. Zip the root folder
3. In Blender: **Edit → Preferences → Add-ons → Install from Disk** → select the zip
4. Enable "Rigacar (Blender 4/5 Fix)"

## License

GPL v3 (same as the original Rigacar addon)
