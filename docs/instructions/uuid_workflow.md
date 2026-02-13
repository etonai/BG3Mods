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
306c7fbf-d3b2-4e20-8a7b-e5dc624e8320

a3312d41-5d26-47de-bb55-61d4af60550b

6b470875-b3f0-4bca-8b6e-ea29e5f9a696

185e7558-6b60-4193-97d1-c7d26f8a858b

783035f2-a754-4cb9-851d-a16e8c8ebef2

52ffb86f-a7f7-4de6-ad51-1a2c33b9c779

8054ad1d-1aea-4b70-b63f-eabb5fb10181

b514d87a-f785-4f45-8c93-4827fb5d7f3f
623f3f43-c3e3-4811-866d-2c78072bc69a

81c15d59-c758-4b66-96c9-ded4998d6a9f

ed73d5c7-1c7c-4ed2-bc7e-ed6b4d454460

41f5f4a4-c036-4db2-9763-51e01ba28887

57a21a18-4d37-4935-926c-8ea8169f84f6

7eec854f-b997-466f-8a74-59e5d6e6e978

80380ea8-80a2-4a71-8269-3c7d26dd91a5

3e018fbc-f4a3-440e-b169-c938dfde49f5

6b3e5669-8780-4a36-8e55-f59f22b5ebfa

ad00001a-a204-4af5-9f9c-2703b9654ec0

c56fc6eb-7b46-4739-96e5-4f896829c10c

aaf7657a-cc38-445c-b1e8-8c8a93d1f648

49fe5773-5cde-4791-9668-7f67f1bb9d1c

06b70227-4bcb-4ed6-a3b9-a458a9bf9e31

023d53c4-351d-47ec-b7eb-32765783d8d3

bc94a0be-96af-4c71-a16d-86741886005e

2971301f-d552-4a72-8d84-126e51811bc4

0da4a14f-00f4-40a0-b0a2-826e58cf044e

1857d276-b362-40b6-a438-9205fdf6c3af

e9685b00-394d-4b9c-bbc9-1868de4de69e

25732722-7c75-47db-8a2a-306ae673986a

aa3e541c-165a-4c18-aad1-175c59940bbb

4797d32e-9395-43f8-b4a6-6469c8b648c3

5d33db34-eba9-4c17-8436-c76452fc20d8

93382d3f-a487-49b8-b76b-3763201a26b7

8512e061-f4d9-49f0-8aa0-e737813db4e4

4c27b41f-25f6-4b48-a058-98882385ec98

6aa8219c-bdb5-4b2c-a6bd-75aa4061f5b9

ff9236c4-c084-4bb9-b8cd-4ee2ceed5e44

e2f43c4c-37f4-419b-b7d8-6a99ba882b59

b0fd95eb-c3b4-4c56-84e0-5b9be483da78

db16b2de-0467-4c28-b2d3-68d9241d9fbf

d5def39d-9a39-4020-8633-8baa0346f142

bd0d1779-1e07-4aba-94b1-837b1f5bf081

f0d41c3b-a028-4c40-9974-48a782f2611b

f3d99799-77ff-4983-bbc0-2c7c6a098a0c

db7516dd-bdfc-4f8e-b30f-7e97d64fb985

84278d2e-299c-4166-9d49-a2ef0b6a4f6b

131d0df9-fc13-40b3-93f5-f712e0859489

b00b74cf-334b-4279-88de-a41c002d7a49
****

```

**Note:** Phase 037 used 17 UUIDs (1 RootTemplate + 16 handles) for Ring of Spectral Power and its custom spells.
**Note:** Phase 038 used 32 UUIDs (9 RootTemplates + 3 spell handles + 20 localization handles) for 4 weapons, 5 body armor pieces, and Spirit Guardians Tyr spell variant.

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
