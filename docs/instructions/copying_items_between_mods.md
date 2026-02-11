# Copying Items Between Mods

## Overview

This guide documents the process for copying items from one mod to another, using the Staff of the Archmage copy from SampleMagicRingMod to Level13PlusGear as the reference example.

---

## ⚠️ CRITICAL: Handle Generation

**DO NOT make up random hex strings for handles!**

Handles MUST be generated from UUIDs in your UUID pool, not invented from scratch.

**Wrong Approach:**
```
❌ hed13a2b3g4c5dg6e7fg8a9bg0b1c2d3e4f5a6b  (made-up random hex)
```

**Correct Approach:**
```
1. Take UUID from pool: fcd9ca2e-9c68-4012-b265-7801a6f95211
2. Remove hyphens:      fcd9ca2e9c684012b2657801a6f95211
3. Format as handle:    hfcd9gca2eg9c68g4012gb265g7801a6f95211
4. Add mod prefix:      hed13fcd9gca2eg9c68g4012gb265g7801a6f95211 ✓
```

See the "Handle Format Reference" section below for detailed instructions.

---

## The Example: Staff of the Archmage

**Source Mod:** SampleMagicRingMod
**Target Mod:** Level13PlusGear (during Phase 029)
**Item:** Staff of the Archmage

This copy was performed to make Level13PlusGear independent from SampleMagicRingMod.

---

## ID Naming Convention Changes

### Prefix Changes

All identifiers must be updated to use the target mod's prefix:

| ID Type | Source (SampleMagicRingMod) | Target (Level13PlusGear) |
|---------|----------------------------|-------------------------|
| **Stats Name** | `SMR_Staff_Archmage` | `L13_Staff_Archmage` |
| **UUID Prefix** | No specific prefix | `ed13` prefix (Phase 031 convention) |
| **Handle Prefix** | No specific prefix | `hed13` prefix |

### UUID Changes

**Critical:** Every UUID must be unique. Never reuse UUIDs between mods.

**Source UUIDs (SampleMagicRingMod):**
- Staff RootTemplate UUID: `c2d3e4f5-a6b7-4c8d-9e0f-1a2b3c4d5e6f`
- Display Name Handle: `h0a1b2c3dge4f5g6a7bg8c9dg0e1f2a3b4c5d6`
- Description Handle: `ha1b2c3d4gf5e6g7a8bg9c0dg1e2f3a4b5c6d7`

**Target UUIDs (Level13PlusGear):**
- Staff RootTemplate UUID: `ed13f510-3c96-4308-813e-f9592c9afee4` (new, from UUID pool)
- Display Name Handle: `hed137624bgb5dag47d9gab02g456236332c1e` (new, with ed13 prefix)
- Description Handle: `hed138099g3c13g42adg8b31g50724eafee5a` (new, with ed13 prefix)

**UUID Generation Process:**
1. Take UUID from `docs/instructions/uuid_workflow.md` pool
2. Replace first 4 characters with target mod prefix (`ed13`)
3. Delete used UUID from pool
4. Document in phase file

**Handle Generation Process (also uses UUID pool):**
1. Take a different UUID from the pool (don't reuse RootTemplate UUIDs)
2. Remove hyphens and convert to handle format (see Handle Format Reference)
3. Add `h` + mod prefix (e.g., `hed13`)
4. Delete used UUID from pool
5. Document in phase file

**Important:** Both RootTemplates AND handles consume UUIDs from the pool. Budget accordingly.

---

## Files to Copy and Modify

### 1. Stats File

**Source:** `SampleMagicRingMod/Public/SampleMagicRingMod/Stats/Generated/Data/Weapon.txt`
**Target:** `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Weapon.txt`

**Changes Required:**
```
Source:
new entry "SMR_Staff_Archmage"
type "Weapon"
using "WPN_Quarterstaff_2"
data "RootTemplate" "c2d3e4f5-a6b7-4c8d-9e0f-1a2b3c4d5e6f"
[...rest of properties...]

Target:
new entry "L13_Staff_Archmage"              ← Changed prefix
type "Weapon"
using "WPN_Quarterstaff_2"
data "RootTemplate" "ed13f510-3c96-4308-813e-f9592c9afee4"  ← New UUID
[...rest of properties - keep same...]
```

**Key Changes:**
- Stats entry name: `SMR_` → `L13_`
- RootTemplate UUID: Generate new UUID with `ed13` prefix
- All other properties: Keep identical (Boosts, PassivesOnEquip, etc.)

### 2. RootTemplate File

**Source:** `SampleMagicRingMod/Public/SampleMagicRingMod/RootTemplates/[UUID].lsf.lsx`
**Target:** `Level13PlusGear/Public/Level13PlusGear/RootTemplates/L13_Staff_Archmage.lsf.lsx`

**Changes Required:**
```xml
Source:
<attribute id="MapKey" type="FixedString" value="c2d3e4f5-a6b7-4c8d-9e0f-1a2b3c4d5e6f" />
<attribute id="Name" type="LSString" value="SMR_Staff_Archmage" />
<attribute id="Stats" type="FixedString" value="SMR_Staff_Archmage" />
<attribute id="DisplayName" handle="h0a1b2c3dge4f5g6a7bg8c9dg0e1f2a3b4c5d6" />
<attribute id="Description" handle="ha1b2c3d4gf5e6g7a8bg9c0dg1e2f3a4b5c6d7" />

Target:
<attribute id="MapKey" type="FixedString" value="ed13f510-3c96-4308-813e-f9592c9afee4" />
<attribute id="Name" type="LSString" value="L13_Staff_Archmage" />
<attribute id="Stats" type="FixedString" value="L13_Staff_Archmage" />
<attribute id="DisplayName" handle="hed137624bgb5dag47d9gab02g456236332c1e" />
<attribute id="Description" handle="hed138099g3c13g42adg8b31g50724eafee5a" />
```

**Key Changes:**
- MapKey: New UUID (matches Stats RootTemplate)
- Name: `SMR_` → `L13_`
- Stats: `SMR_` → `L13_`
- DisplayName handle: New handle with `hed13` prefix
- Description handle: New handle with `hed13` prefix
- All other attributes: Keep identical (ParentTemplateId, VisualTemplate, etc.)

### 3. Localization File

**Source:** `SampleMagicRingMod/Localization/English/SampleMagicRingMod.loca.xml`
**Target:** `Level13PlusGear/Localization/English/Level13PlusGear.loca.xml`

**Changes Required:**
```xml
Source:
<content contentuid="h0a1b2c3dge4f5g6a7bg8c9dg0e1f2a3b4c5d6" version="1">Staff of the Archmage</content>
<content contentuid="ha1b2c3d4gf5e6g7a8bg9c0dg1e2f3a4b5c6d7" version="1">[Description text]</content>

Target:
<content contentuid="hed137624bgb5dag47d9gab02g456236332c1e" version="1">Staff of the Archmage</content>
<content contentuid="hed138099g3c13g42adg8b31g50724eafee5a" version="1">[Description text]</content>
```

**Key Changes:**
- Handle UIDs: New handles with target mod prefix
- Content text: Keep identical (unless intentionally changing)

### 4. Supporting Files (if applicable)

**Spell Files (Spell_Target.txt, Interrupt.txt, etc.):**
- Follow same naming convention: `SMR_` → `L13_`
- Generate new handles with `hed13` prefix
- Keep spell properties identical

**Passive Files:**
- Usually reference vanilla passives, no changes needed
- If custom passives: Apply same naming convention

---

## Step-by-Step Procedure

### Phase 1: Planning

1. **Identify source item and all related files**
   - Stats entry (Weapon.txt, Armor.txt, Object.txt, etc.)
   - RootTemplate file
   - Localization entries
   - Any custom spells, passives, or interrupts

2. **Determine target mod naming convention**
   - Stats prefix (e.g., `L13_`)
   - UUID prefix (e.g., `ed13`)
   - Handle prefix (e.g., `hed13`)

3. **Count UUIDs needed**
   - 1 for RootTemplate
   - 2+ for localization handles (name, description)
   - Additional for custom spells/abilities
   - Reserve from UUID pool in `uuid_workflow.md`

### Phase 2: Copy Stats Entry

1. Open source stats file
2. Copy entire item entry
3. Paste into target stats file
4. Replace:
   - Entry name: `SMR_` → `L13_`
   - RootTemplate UUID: Use new UUID from pool
5. Verify all properties are present

### Phase 3: Create RootTemplate

1. Copy source RootTemplate file
2. Rename file to match new stats name (e.g., `L13_Staff_Archmage.lsf.lsx`)
3. Replace:
   - MapKey: New RootTemplate UUID
   - Name: New stats name
   - Stats: New stats name
   - DisplayName handle: New handle with prefix
   - Description handle: New handle with prefix
4. Keep all other attributes identical

### Phase 4: Create Localization

1. Copy localization entries from source
2. Replace:
   - Handle UIDs with new prefixed handles
3. Keep content text identical (or modify if needed)
4. Add to target mod's localization file

### Phase 5: Copy Supporting Files (if needed)

For custom spells/abilities:
1. Copy spell entries from source
2. Apply naming convention: `SMR_` → `L13_`
3. Generate new handles for localization
4. Update localization file

### Phase 6: Update UUID Pool

1. Delete used UUIDs from `uuid_workflow.md`
2. Document used UUIDs in phase file
3. Note if pool is getting low (< 10 UUIDs)

### Phase 7: Testing

1. Load mod in new game
2. Verify item appears in delivery location
3. Check item name and description display correctly
4. Equip item and verify functionality
5. Test all abilities/spells work as expected

---

## Common Pitfalls and Solutions

### Issue: Item Doesn't Appear

**Possible Causes:**
- Stats name doesn't match RootTemplate Stats attribute
- RootTemplate UUID doesn't match Stats RootTemplate
- Treasure table references wrong item name (should be `I_[StatsName]`)
- Item marked as `Unique: 1` and already spawned elsewhere

**Solution:**
- Verify all name references match exactly
- Check UUIDs match between files
- Set `Unique: 0` if item appears in multiple locations

### Issue: Item Name/Description Shows as Handle

**Possible Causes:**
- Localization handle in RootTemplate doesn't exist in localization file
- Handle UID typo or mismatch
- Localization file not loaded

**Solution:**
- Verify handle UIDs match exactly between RootTemplate and localization
- Check for typos in handle format (`h` prefix, `g` separators)
- Ensure localization file is in correct location

### Issue: Item Has Wrong Icon/Visuals

**Possible Causes:**
- ParentTemplateId or VisualTemplate changed during copy
- Icon attribute causing issues (Phase 031 lesson)

**Solution:**
- Keep ParentTemplateId and VisualTemplate identical to source
- For rings: Use minimal RootTemplate (no Icon attribute)
- Verify VisualTemplate UUID is correct

### Issue: Item Abilities Don't Work

**Possible Causes:**
- Spell names in Boosts don't exist in target mod
- Custom spells not copied over
- Dependencies on source mod's spells

**Solution:**
- Copy all referenced spells to target mod
- Update spell references to use target mod prefix
- Check PassivesOnEquip reference valid passives

---

## Handle Format Reference

### Standard Handle Format

```
h[prefix][4-5 hex]g[4 hex]g[4 hex]g[4 hex]g[12 hex]
```

**Example with hed13 prefix:**
```
hed137624bgb5dag47d9gab02g456236332c1e
 │   │     │    │    │    │
 │   │     │    │    │    └─ 12 hex characters
 │   │     │    │    └────── 4 hex characters
 │   │     │    └─────────── 4 hex characters
 │   │     └──────────────── 4 hex characters
 │   └────────────────────── 5 hex characters (after prefix)
 └────────────────────────── "h" + prefix (hed13)
```

**CRITICAL: Generating Handles from UUIDs**

**DO NOT** make up random hex strings for handles. Handles must be generated from UUIDs in your UUID pool.

**Correct Process:**
1. Take a UUID from your pool (e.g., `fcd9ca2e-9c68-4012-b265-7801a6f95211`)
2. Remove all hyphens: `fcd9ca2e9c684012b2657801a6f95211`
3. Insert `g` separators in handle format: segments of varying lengths
4. Add `h` prefix + mod prefix (e.g., `ed13` becomes `hed13`)

**Example Conversion:**
```
UUID from pool:    fcd9ca2e-9c68-4012-b265-7801a6f95211
Remove hyphens:    fcd9ca2e9c684012b2657801a6f95211
Format as handle:  hfcd9gca2eg9c68g4012gb265g7801a6f95211
Add mod prefix:    hed13fcd9gca2eg9c68g4012gb265g7801a6f95211
                   │   │    │    │    │    │    │
                   │   │    │    │    │    │    └─ Remaining characters
                   │   │    │    │    │    └────── "g" separator
                   │   │    │    │    └─────────── 4 hex characters
                   │   │    │    └──────────────── "g" separator
                   │   │    └───────────────────── 4 hex characters
                   │   └────────────────────────── "g" separator
                   └────────────────────────────── "h" + prefix (hed13) + first 4 hex
```

**Common Handle Patterns:**
- Pattern 1: `h[prefix][4hex]g[4hex]g[4hex]g[4hex]g[4hex]g[12hex]`
- Pattern 2: `h[prefix][5hex]g[4hex]g[4hex]g[4hex]g[12hex]`

Both patterns are valid. The key is using characters from a real UUID, not inventing random hex.

**After using a UUID for a handle:**
- Delete it from the UUID pool (same as RootTemplates)
- Document it in your phase file
- Never reuse handles between items

---

## UUID Format Reference

### Standard UUID Format

```
xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

**With Target Mod Prefix:**
```
ed13xxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
 │   │
 │   └─ Remaining 4 characters from original UUID
 └───── 4-character mod prefix (ed13)
```

**Example Transformation:**
```
Original UUID:  17c387dc-1bbb-4458-86c6-255e285e9b96
Replace "17c3":  ed31
Result:         ed3187dc-1bbb-4458-86c6-255e285e9b96
                │   │
                │   └─ "87dc" kept from original
                └───── "ed31" replaces "17c3"
```

---

## Quick Reference Checklist

When copying an item, ensure you update:

- [ ] Stats entry name (prefix change)
- [ ] Stats RootTemplate UUID (new UUID)
- [ ] RootTemplate file name (matches stats name)
- [ ] RootTemplate MapKey (matches stats UUID)
- [ ] RootTemplate Name attribute (matches stats name)
- [ ] RootTemplate Stats attribute (matches stats name)
- [ ] RootTemplate DisplayName handle (new handle)
- [ ] RootTemplate Description handle (new handle)
- [ ] Localization entries (new handles, copied text)
- [ ] Custom spell entries (if applicable)
- [ ] Custom spell localization (if applicable)
- [ ] UUID pool updated (used UUIDs deleted)
- [ ] Phase documentation (UUIDs recorded)

---

## Example: Ring Copy Template

For copying a ring item:

**Stats (Armor.txt):**
```
new entry "[TARGET_PREFIX]_[ItemName]"
type "Armor"
using "ARM_Ring"
data "RootTemplate" "[NEW_UUID]"
data "Rarity" "[Same as source]"
data "Boosts" "[Copy boosts, update spell names if needed]"
data "Unique" "0"    ← Set to 0 if appears in multiple locations
```

**RootTemplate (Minimal Structure - Phase 031 Lesson):**
```xml
<attribute id="MapKey" value="[NEW_UUID]" />
<attribute id="Name" value="[TARGET_PREFIX]_[ItemName]" />
<attribute id="ParentTemplateId" value="2f157b63-5500-406f-bf32-90011d612907" />
<attribute id="Stats" value="[TARGET_PREFIX]_[ItemName]" />
<attribute id="DisplayName" handle="[NEW_HANDLE]" />
<attribute id="Description" handle="[NEW_HANDLE]" />
```

**Note:** For rings, use minimal RootTemplate structure (no Icon, no PhysicsTemplate, no VisualTemplate).

---

## Related Documentation

- **uuid_workflow.md** - UUID pool and generation process
- **BG3_Modding_Lessons_Learned.md** - Handle format and file structure
- **Phase029.md** - Staff of Archmage copy implementation details
- **Phase031.md** - Ring creation lessons (minimal RootTemplate, Unique flag)

---

## Notes

- Always use fresh UUIDs from the pool - never copy UUIDs between mods
- Handles must be unique - generate new handles with target mod prefix
- Test in clean save to verify item appears correctly
- Document all UUIDs used in phase file
- Keep source mod as reference, don't delete original item

---

## Version History

- **2026-02-10**: Initial document created based on Phase 029 (Staff of Archmage copy) and Phase 031 lessons
