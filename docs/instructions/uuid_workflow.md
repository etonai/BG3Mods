# Level13Gear UUID and Naming Conventions

## Overview
This document establishes the UUID generation and naming conventions for the Level13Gear mod.

---

## Naming Conventions

### Item Prefixes
All items in Level13Gear should use the `L13` prefix for handles and names.

**Examples:**
- `L13_Armor_Medium_ArmorOfTyr`
- `L13_Weapon_Longsword_HolyAvenger`
- `L13_Ring_Protection`

**Comparison:**
- SampleMagicRingMod uses `SMR` prefix
- Level13Gear uses `L13` prefix

---

## UUID Workflow

### UUID Generation Rules

1. Ed generates UUIDs in bulk using a UUID v4 generator and adds them to this document
2. When using a UUID, replace the first 4 characters with `ed13` for easy identification
   - Example: `550e8400-e29b-41d4-a716-446655440000` becomes `ed13e400-e29b-41d4-a716-446655440000`
3. **Delete the UUID from this list** after using it

### Benefits of Custom Prefix
- Easy to identify Level13Gear UUIDs in logs and files
- Helps avoid UUID collisions between mods
- Makes debugging easier

---

## Available UUIDs

### UUID Pool
The following UUIDs are available for Level13Gear mod use. **Delete the UUID from this list when you use it.**

```
258fabe5-df58-4ba4-915f-dafaee1f7906
fcd9ca2e-9c68-4012-b265-7801a6f95211
d0bcc374-2d7b-48e7-8622-8d9c06085de5
bfaecc93-90c1-45d0-b17d-306ef3119412
4c0d95ce-a6eb-4b08-9498-60b32e4e8e09
```

### When Running Low

Ask Ed to generate more UUIDs when the pool gets below 10. Ed will use an online UUID v4 generator to create new UUIDs and add them to this list.

---

## Quick Reference

| Convention | Value |
|------------|-------|
| Item Prefix | `L13` |
| UUID Custom Prefix | `ed13` |
| UUID Format | `ed13xxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx` |
| UUID Management | Delete from list when used |

---

## Notes

- Delete UUIDs from the Available UUIDs list when you assign them to items
- Generate more UUIDs when pool gets below 10
- Use clear, descriptive item handles following BG3 conventions (e.g., `L13_Armor_Medium_ArmorOfTyr`)
