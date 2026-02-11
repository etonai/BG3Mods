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
646889eb-b94d-4729-9f1c-dbb076b89dc2

a97e5b37-c15a-406e-9fae-f9c01e088d4b

979aade8-0894-4a8d-a1a8-43c82c135636

0f477ec9-9c1f-417c-879b-87cc582dd87b

c9de23f1-da91-4f28-b249-fb602de523c3

193f51df-f7ca-4ec9-9c02-8d276688f61d

97c3989d-c40f-408e-a4c5-e5a739766f71

df161560-5883-49f6-9f77-ba85e1313d75

980c1526-fbf8-4d9c-8d2c-1a24302caa4e

feb69a1f-da95-43d2-915b-86d9f7b82c5b

7d1ab663-541e-43be-b79a-d4dcb0353dc0

1b7e50fb-ecd8-40d7-b11b-769e4dbea462

84e7cb49-1619-4aa5-8121-77502416e759

de9049ba-1520-45e8-86f3-eb124533e33a

5b0b73e4-02a6-484c-80eb-69b8ae745ed8

fd322884-3264-4120-b15b-febefc16b6cb

81aa4717-dfb8-47f9-98a5-9ed2fc841e50

a8392513-d5a4-49dd-8346-2f5df0ba2e77

3d0af80d-b40e-4534-a8dc-45a9db336374

61827095-93bb-47e8-9734-f0a85b99a2d8

4569dc14-cd05-4045-b2fc-846210c43d94
****

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
