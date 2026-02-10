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

1. **Generate UUIDs in bulk** using a UUID v4 generator
2. **Mark UUIDs as used** when assigned to an item
3. **Custom prefix**: Replace the first 4 characters with `ed13` for easy identification
   - Example: `550e8400-e29b-41d4-a716-446655440000` becomes `ed13e400-e29b-41d4-a716-446655440000`

### Benefits of Custom Prefix
- Easy to identify Level13Gear UUIDs in logs and files
- Helps avoid UUID collisions between mods
- Makes debugging easier

---

## Available UUIDs

### Reserved UUID Pool
The following UUIDs are reserved for Level13Gear mod use. Mark each as **[USED]** when assigned.

```
ed13a7b0-1234-4567-89ab-111111111111 - [AVAILABLE]
ed13a7b1-1234-4567-89ab-222222222222 - [AVAILABLE]
ed13a7b2-1234-4567-89ab-333333333333 - [AVAILABLE]
ed13a7b3-1234-4567-89ab-444444444444 - [AVAILABLE]
ed13a7b4-1234-4567-89ab-555555555555 - [AVAILABLE]
ed13a7b5-1234-4567-89ab-666666666666 - [AVAILABLE]
ed13a7b6-1234-4567-89ab-777777777777 - [AVAILABLE]
ed13a7b7-1234-4567-89ab-888888888888 - [AVAILABLE]
ed13a7b8-1234-4567-89ab-999999999999 - [AVAILABLE]
ed13a7b9-1234-4567-89ab-aaaaaaaaaaaa - [AVAILABLE]
ed13a7ba-1234-4567-89ab-bbbbbbbbbbbb - [AVAILABLE]
ed13a7bb-1234-4567-89ab-cccccccccccc - [AVAILABLE]
ed13a7bc-1234-4567-89ab-dddddddddddd - [AVAILABLE]
ed13a7bd-1234-4567-89ab-eeeeeeeeeeee - [AVAILABLE]
ed13a7be-1234-4567-89ab-ffffffffffff - [AVAILABLE]
ed13a7bf-1234-4567-89ab-000000000001 - [AVAILABLE]
ed13a7c0-1234-4567-89ab-000000000002 - [AVAILABLE]
ed13a7c1-1234-4567-89ab-000000000003 - [AVAILABLE]
ed13a7c2-1234-4567-89ab-000000000004 - [AVAILABLE]
ed13a7c3-1234-4567-89ab-000000000005 - [AVAILABLE]
ed13a7c4-1234-4567-89ab-000000000006 - [AVAILABLE]
ed13a7c5-1234-4567-89ab-000000000007 - [AVAILABLE]
ed13a7c6-1234-4567-89ab-000000000008 - [AVAILABLE]
ed13a7c7-1234-4567-89ab-000000000009 - [AVAILABLE]
ed13a7c8-1234-4567-89ab-00000000000a - [AVAILABLE]
ed13a7c9-1234-4567-89ab-00000000000b - [AVAILABLE]
ed13a7ca-1234-4567-89ab-00000000000c - [AVAILABLE]
ed13a7cb-1234-4567-89ab-00000000000d - [AVAILABLE]
ed13a7cc-1234-4567-89ab-00000000000e - [AVAILABLE]
ed13a7cd-1234-4567-89ab-00000000000f - [AVAILABLE]
```

### Usage Tracking

When you use a UUID, update the line to include:
1. Mark as **[USED]**
2. Item name
3. Date used

**Example:**
```
ed13a7b0-1234-4567-89ab-111111111111 - [USED] - L13_Armor_Medium_ArmorOfTyr - 2026-02-10
```

---

## Quick Reference

| Convention | Value |
|------------|-------|
| Item Prefix | `L13` |
| UUID Custom Prefix | `ed13` |
| UUID Format | `ed13xxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx` |
| UUID Tracker | This document (uuid_workflow.md) |

---

## Notes

- Generate more UUIDs as needed when pool runs low
- Keep this document updated with UUID usage
- Use clear, descriptive item handles following BG3 conventions
