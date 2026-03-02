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
d4ee2c7b-af67-40c3-812c-3e5c1cbcb644
3a199b4e-e7de-4ebe-af3c-fa415f54f699
de7b7f2f-7ef5-41ec-a1bb-e37659b3df8a
34214625-1c0a-44c7-834c-37776c49cc0b
9a3134cd-b04c-4273-a1bf-cc37eef43c1e
df8a9720-94bd-4dfe-ab74-412485ec8cf3
dc345087-1933-4259-8c0a-ed729dae680e
d1dc7ae4-012a-4537-87d8-925cf4ad3211
6ff26e91-f5bf-40b6-8459-14eca7c6389f
575d872c-0381-4698-a0d9-5ff9975572fe
85f0d700-fcb6-4df9-8d11-a7d2217c1ccb
da7b238a-540f-4aec-8232-0cf85183412e
38227ab6-aaba-4c22-acd2-b785ecd60e6f
40388269-35e4-4b68-bfd4-a18ad10b0e74
be1d7abb-2f97-4d03-ba49-9f31cf6b7e72
5a1b39ec-9fad-424f-8ea9-7a46df066bec
0cc6b454-caf8-4204-983b-05b99b1c8a92
42a9166a-157c-467c-b278-7626885635cb
bfdcdb7f-ff0a-4ba8-9b22-b710f6f46b43
9c13a380-3669-48f6-9b17-093260e639ad
1e2e6526-1c14-4115-8419-05b3f2b2cf1d
36c356a5-aa5c-4b33-b839-6084fc0e9672
57f2c865-f166-4417-8756-9c36f3e7671b
7227fac9-17db-44a4-852e-039746ab36bf
abfe8072-1e8c-4ac2-95e4-07887f202003
6109f57b-8cc6-4aa0-a835-ab0fb2ddc217
****

```

**Note:** Phase 037 used 17 UUIDs (1 RootTemplate + 16 handles) for Ring of Spectral Power and its custom spells.
**Note:** Phase 038 used 32 UUIDs (9 RootTemplates + 3 spell handles + 20 localization handles) for 4 weapons, 5 body armor pieces, and Spirit Guardians Tyr spell variant.
**Note:** Phase 054 Revision 1 used 18 UUIDs (18 handles) for Staff of Gimeitaro and its custom spells in Level21Gear mod.
**Note:** Phase 054 Revision 2 used 5 UUIDs (5 handles) for Spirit Guardians Gimeitaro spell variants.
**Note:** Phase 056 used 4 UUIDs (1 RootTemplate UUID, 1 OneTimeReward UUID, 2 handles) for L21_Gear_Chest.
**Note:** Phase 057 used 18 UUIDs (2 RootTemplate UUIDs + 16 handles) for L21_Sword_Silverlight, its spells/passives, and the Silvered Bulwark scroll in Level21Gear.
**Note:** Phase 057 Revision 2 used 2 UUIDs (2 handles, roc1 prefix) for ROC_Summon_L21_Chest spell in RingOfCreation.
**Note:** Phase 058 used 6 UUIDs (1 mod UUID + 1 RootTemplate UUID + 4 handles, ed58 prefix) for the SilveredBulwarkScroll mod.
**Note:** Phase 059 used 3 UUIDs (1 RootTemplate UUID + 2 handles, ed58 prefix) for FBS_Scroll_HellfireOrb in the ForbiddenScrolls mod (renamed from SilveredBulwarkScroll).

### When Running Low

Ask Ed to generate more UUIDs when the pool gets below 20. Ed will use an online UUID v4 generator to create new UUIDs and add them to this list.

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
- Ask Ed to generate more UUIDs when pool gets below 10
- Use clear, descriptive item handles following BG3 conventions (e.g., `L13_Armor_Medium_ArmorOfTyr`)
