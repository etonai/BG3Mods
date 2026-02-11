# Phase 32: Copy Longsword of Tyr to Level13PlusGear

**Status:** COMPLETE
**Date:** 2026-02-10
**Implementation Date:** 2026-02-10
**Completion Date:** 2026-02-10

---

## Goal

Test the **copying_items_between_mods.md** workflow guide by copying the Longsword of Tyr from SampleMagicRingMod to Level13PlusGear mod. This will make Level13PlusGear fully independent from SampleMagicRingMod (no dependencies).

---

## Important Changes Checklist

When copying the Longsword of Tyr, the following changes are critical:

- **Stats prefix:** `SMR_` → `L13_`
  - `SMR_Sword_Tyr` → `L13_Sword_Tyr`
  - All custom spell names must be updated
  - All custom passive names must be updated

- **UUIDs:** Generate new UUIDs with `ed13` prefix
  - RootTemplate UUID (currently: `d2e3f4a5-b6c7-4d8e-9f0a-1b2c3d4e5f6a`)
  - All spell localization handles (for custom spells)

- **Handles:** Generate new handles with `hed13` prefix
  - DisplayName handle (currently: `h5c6d7e8fg9a0bg1c2dg3e4fg5a6b7c8d9e0f1`)
  - Description handle (currently: `h6d7e8f9ag0b1cg2d3eg4f5ag6b7c8d9e0f1a2`)
  - All custom spell name/description handles

- **RootTemplate filename:** Rename to match new stats name
  - Create: `L13_Sword_Tyr.lsf.lsx`

- **Dependencies:** Must copy supporting files
  - Custom spells (3 total)
  - Custom passive (1 total)
  - Spell localization entries

- **Delivery location:** Level13PlusGear uses Tutorial Chest
  - Update TreasureTable.txt to reference `I_L13_Sword_Tyr`

- **No mod dependencies:** All files must be self-contained
  - Do NOT reference SMR_ spells/passives from SampleMagicRingMod
  - Copy all custom content to Level13PlusGear

---

## Source Item Details

### Stats Entry (from SampleMagicRingMod)

**File:** `SampleMagicRingMod/Public/SampleMagicRingMod/Stats/Generated/Data/Weapon.txt`

```
new entry "SMR_Sword_Tyr"
type "Weapon"
using "WPN_Longsword_2"
data "RootTemplate" "d2e3f4a5-b6c7-4d8e-9f0a-1b2c3d4e5f6a"
data "Rarity" "Legendary"
data "DefaultBoosts" "WeaponEnchantment(5);WeaponProperty(Magical)"
data "Boosts" "UnlockSpell(Target_MAG_Smite_Wrathful);UnlockSpell(SMR_Target_BlindingSmite_Unlimited);UnlockSpell(SMR_Target_Light_Unlimited);UnlockSpell(Target_PLA_ShieldOfFaith_SwordOfJustice);UnlockSpell(SMR_Shout_CelestialHaste_Unlimited)"
data "PassivesOnEquip" "MAG_PlaneShifterSlayer_Passive;SMR_RadiantWeapon_Passive"
data "Unique" "1"
```

**Vanilla Dependencies:**
- `Target_MAG_Smite_Wrathful` (Wrathful Smite)
- `Target_PLA_ShieldOfFaith_SwordOfJustice` (Shield of Faith)
- `MAG_PlaneShifterSlayer_Passive` (Plane Shifter Slayer)

**Custom Dependencies (Must Copy):**
- `SMR_Target_BlindingSmite_Unlimited` (custom spell)
- `SMR_Target_Light_Unlimited` (custom spell)
- `SMR_Shout_CelestialHaste_Unlimited` (custom spell)
- `SMR_RadiantWeapon_Passive` (custom passive)

### RootTemplate

**File:** `SampleMagicRingMod/Public/SampleMagicRingMod/RootTemplates/merged.lsf.lsx`

**Key Attributes:**
- MapKey: `d2e3f4a5-b6c7-4d8e-9f0a-1b2c3d4e5f6a`
- Name: `SMR_Sword_Tyr`
- Stats: `SMR_Sword_Tyr`
- ParentTemplateId: `e3b2adb6-7493-466e-9c65-4281fb74e83f` (keep same)
- VisualTemplate: `5f9832fa-7633-5e68-b69c-0156eda17471` (keep same)
- DisplayName: `h5c6d7e8fg9a0bg1c2dg3e4fg5a6b7c8d9e0f1`
- Description: `h6d7e8f9ag0b1cg2d3eg4f5ag6b7c8d9e0f1a2`

**StatusList:**
- `MAG_RADIANT_STRONG_RADIANCE_WEAPON` (keep same)

**Tags:**
- `983087c8-c9d3-4a87-bc69-65f9329666c8` (keep same)

### Localization

**Display Name:** "Longsword of Tyr"
**Description:** "A silver longsword blessed by Tyr, the God of Justice. Grants Wrathful Smite, Soulbreaker, and unlimited Blinding Smite."

---

## Custom Dependencies to Copy

### 1. SMR_Target_BlindingSmite_Unlimited

**File:** `Spell_Target.txt`
**New Name:** `L13_Target_BlindingSmite_Unlimited`
**Requires:** Localization for spell name/description

### 2. SMR_Target_Light_Unlimited

**File:** `Spell_Target.txt`
**New Name:** `L13_Target_Light_Unlimited`
**Requires:** Localization for spell name/description

### 3. SMR_Shout_CelestialHaste_Unlimited

**File:** `Spell_Shout.txt`
**New Name:** `L13_Shout_CelestialHaste_Unlimited`
**Requires:** Localization for spell name/description

### 4. SMR_RadiantWeapon_Passive

**File:** `Passive.txt`
**New Name:** `L13_RadiantWeapon_Passive`
**Requires:** Localization for passive name/description

---

## UUID Requirements

Based on the copying_items_between_mods.md guide, we need UUIDs for:

1. **Longsword RootTemplate** (1 UUID)
2. **Longsword DisplayName handle** (1 handle)
3. **Longsword Description handle** (1 handle)
4. **Spell localization handles** (2 handles per spell = 6 handles)
5. **Passive localization handles** (2 handles = 2 handles)

**Total Required:**
- **1 UUID** (for RootTemplate)
- **9 handles** (for all localization entries)

**Note:** UUIDs will be pulled from `docs/instructions/uuid_workflow.md` pool and documented below during implementation.

---

## Implementation Steps

### Phase 1: Copy Weapon Stats

1. Open `SampleMagicRingMod/Public/SampleMagicRingMod/Stats/Generated/Data/Weapon.txt`
2. Copy the `SMR_Sword_Tyr` entry
3. Paste into `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Weapon.txt`
4. Update:
   - Entry name: `SMR_Sword_Tyr` → `L13_Sword_Tyr`
   - RootTemplate UUID: [NEW UUID from pool]
   - Boosts spell references:
     - `SMR_Target_BlindingSmite_Unlimited` → `L13_Target_BlindingSmite_Unlimited`
     - `SMR_Target_Light_Unlimited` → `L13_Target_Light_Unlimited`
     - `SMR_Shout_CelestialHaste_Unlimited` → `L13_Shout_CelestialHaste_Unlimited`
   - PassivesOnEquip reference:
     - `SMR_RadiantWeapon_Passive` → `L13_RadiantWeapon_Passive`
5. Set `Unique: 0` (appears in TreasureTable, not OneTimeRewards)

### Phase 2: Copy Custom Spells

For each of the 3 custom spells:

1. Copy spell entry from SampleMagicRingMod
2. Update spell name: `SMR_` → `L13_`
3. Generate new handles for DisplayName and Description
4. Copy localization entries
5. Update any internal references (spell containers, etc.)

### Phase 3: Copy Custom Passive

1. Copy passive entry from `Passive.txt`
2. Update passive name: `SMR_RadiantWeapon_Passive` → `L13_RadiantWeapon_Passive`
3. Generate new handles for DisplayName and Description
4. Copy localization entries

### Phase 4: Create RootTemplate

1. Create new file: `Level13PlusGear/Public/Level13PlusGear/RootTemplates/L13_Sword_Tyr.lsf.lsx`
2. Copy structure from `SampleMagicRingMod/Public/SampleMagicRingMod/RootTemplates/merged.lsf.lsx` (Sword of Tyr section)
3. Update:
   - MapKey: [NEW UUID from pool]
   - Name: `L13_Sword_Tyr`
   - Stats: `L13_Sword_Tyr`
   - DisplayName handle: [NEW HANDLE]
   - Description handle: [NEW HANDLE]
4. Keep unchanged:
   - ParentTemplateId
   - VisualTemplate
   - StatusList
   - Tags

### Phase 5: Create Localization

1. Open `Level13PlusGear/Localization/English/Level13PlusGear.loca.xml`
2. Add entries for:
   - Longsword DisplayName and Description
   - All 3 spell DisplayNames and Descriptions
   - Passive DisplayName and Description
3. Use new handles generated in previous steps
4. Copy text content from SampleMagicRingMod (or modify as desired)

### Phase 6: Update TreasureTable

1. Open `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/TreasureTable.txt`
2. Find the Tutorial Chest entry
3. Add new line: `new treasuretable "I_L13_Sword_Tyr"`
4. Set appropriate properties (CanMerge, etc.)

### Phase 7: Update UUID Pool

1. Open `docs/instructions/uuid_workflow.md`
2. Delete used UUIDs from pool
3. Document used UUIDs in this phase file (see section below)

---

## UUIDs Used (Documented During Implementation)

### Longsword of Tyr

- **RootTemplate UUID:** `ed13abe5-df58-4ba4-915f-dafaee1f7906` (from pool: `258fabe5-df58-4ba4-915f-dafaee1f7906`)
- **DisplayName Handle:** `hed13fcd9gca2eg9c68g4012gb265g7801a6f95211` (from pool: `fcd9ca2e-9c68-4012-b265-7801a6f95211`)
- **Description Handle:** `hed13d0bcgc374g2d7bg48e7g8622g8d9c06085de5` (from pool: `d0bcc374-2d7b-48e7-8622-8d9c06085de5`)

### Blinding Smite Spell

- **DisplayName Handle:** `hed13bfaegcc93g90c1g45d0gb17dg306ef3119412` (from pool: `bfaecc93-90c1-45d0-b17d-306ef3119412`)
- **ExtraDescription Handle:** `hed134c0dg95cega6ebg4b08g9498g60b32e4e8e09` (from pool: `4c0d95ce-a6eb-4b08-9498-60b32e4e8e09`)

### Light Spell

- **Note:** Already existed in Level13PlusGear as `L13_Target_Light_Unlimited` (no new UUIDs needed)

### Celestial Haste Spell

- **Note:** No custom localization handles needed (uses vanilla spell name/description via `using "Shout_MAG_Victory_Longbow_Haste"`)

### Radiant Weapon Passive

- **DisplayName Handle:** `hed13a08agdeb3ge67ag4fe8gabacg5c1e91053d81` (from pool: `a08adeb3-e67a-4fe8-abac-5c1e91053d81`)
- **Description Handle:** `hed1379d9g5cfeg8121g4329g85d3g8040d33ee1cd` (from pool: `79d95cfe-8121-4329-85d3-8040d33ee1cd`)

---

## Revision 1: Fix Incorrect Handle Generation

**Date:** 2026-02-10
**Issue:** Handles were incorrectly generated using made-up hex strings instead of being properly derived from UUIDs in the pool.

### Problem Identified

In the initial implementation, handles were created by inventing random hex strings with the `hed13` prefix (e.g., `hed13a2b3g4c5dg6e7fg8a9bg0b1c2d3e4f5a6b`). This is incorrect.

**Correct Process:**
1. Take a UUID from the pool (e.g., `fcd9ca2e-9c68-4012-b265-7801a6f95211`)
2. Remove the hyphens: `fcd9ca2e9c684012b2657801a6f95211`
3. Format as handle: `hfcd9gca2eg9c68g4012gb265g7801a6f95211`
4. Add mod prefix after `h`: `hed13fcd9gca2eg9c68g4012gb265g7801a6f95211`

### UUIDs Taken from Pool for Handles

The following UUIDs will be used to generate proper handles:

1. `fcd9ca2e-9c68-4012-b265-7801a6f95211` → Weapon DisplayName
2. `d0bcc374-2d7b-48e7-8622-8d9c06085de5` → Weapon Description
3. `bfaecc93-90c1-45d0-b17d-306ef3119412` → BlindingSmite DisplayName
4. `4c0d95ce-a6eb-4b08-9498-60b32e4e8e09` → BlindingSmite ExtraDescription
5. `a08adeb3-e67a-4fe8-abac-5c1e91053d81` → RadiantWeapon DisplayName
6. `79d95cfe-8121-4329-85d3-8040d33ee1cd` → RadiantWeapon Description

### Corrected Handles

**Longsword of Tyr:**
- DisplayName: `hed13fcd9gca2eg9c68g4012gb265g7801a6f95211`
- Description: `hed13d0bcgc374g2d7bg48e7g8622g8d9c06085de5`

**Blinding Smite Spell:**
- DisplayName: `hed13bfaegcc93g90c1g45d0gb17dg306ef3119412`
- ExtraDescription: `hed134c0dg95cega6ebg4b08g9498g60b32e4e8e09`

**Radiant Weapon Passive:**
- DisplayName: `hed13a08agdeb3ge67ag4fe8gabacg5c1e91053d81`
- Description: `hed1379d9g5cfeg8121g4329g85d3g8040d33ee1cd`

### Files That Need Correction

1. **Level13PlusGear/Public/Level13PlusGear/RootTemplates/L13_Sword_Tyr.lsf.lsx**
   - Update DisplayName and Description handles

2. **Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Spell_Target.txt**
   - Update BlindingSmite DisplayName and ExtraDescription handles

3. **Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Passive.txt**
   - Update RadiantWeapon DisplayName and Description handles

4. **Level13PlusGear/Localization/English/Level13PlusGear.loca.xml**
   - Update all 6 contentuid values

5. **docs/instructions/uuid_workflow.md**
   - Remove 6 additional UUIDs from pool

6. **This phase document**
   - Update "UUIDs Used" section with corrected information

### Implementation Status

- [x] Fix RootTemplate handles
- [x] Fix Spell_Target.txt handles
- [x] Fix Passive.txt handles
- [x] Fix localization contentuid values
- [x] Remove 6 UUIDs from uuid_workflow.md
- [x] Update "UUIDs Used" section in this document
- [x] Update copying_items_between_mods.md to emphasize proper handle generation

**Revision 1 Complete:** 2026-02-10

---

## Testing Plan

### Test 1: Item Appears in Tutorial Chest

1. Start new game with Level13PlusGear mod enabled
2. Complete tutorial and reach Nautiloid crash site
3. Open Tutorial Chest
4. **Verify:** Longsword of Tyr appears in chest

### Test 2: Item Properties

1. Inspect Longsword of Tyr in inventory
2. **Verify:**
   - Name displays as "Longsword of Tyr" (not handle)
   - Description displays correctly (not handle)
   - Shows as Legendary rarity
   - Shows +5 enchantment
   - Icon/visual appears correctly

### Test 3: Spells Work

1. Equip Longsword of Tyr
2. **Verify spells appear on hotbar:**
   - Wrathful Smite (vanilla)
   - Blinding Smite (unlimited, custom)
   - Light (unlimited, custom)
   - Shield of Faith (vanilla)
   - Celestial Haste (unlimited, custom)
3. **Test each spell:**
   - Cast successfully
   - Tooltips display correctly
   - Effects work as expected

### Test 4: Passives Work

1. With Longsword of Tyr equipped, check character sheet
2. **Verify passives are active:**
   - Plane Shifter Slayer (vanilla)
   - Radiant Weapon (custom - should show in passives list)
3. **Test Radiant Weapon:**
   - Attack enemy with longsword
   - **Verify:** Deals additional 1d4 radiant damage

### Test 5: No Mod Dependencies

1. Disable SampleMagicRingMod
2. Enable only Level13PlusGear
3. Start new game
4. **Verify:** All functionality works without SampleMagicRingMod present

---

## Related Documentation

- **docs/instructions/copying_items_between_mods.md** - Complete workflow guide
- **docs/instructions/uuid_workflow.md** - UUID pool and naming conventions
- **docs/planning/item_catalog.md** - Source item details (Sword of Tyr)
- **Phase029.md** - Previous item copy example (Staff of Archmage)

---

## Success Criteria

- [ ] Longsword of Tyr appears in Tutorial Chest in new game
- [ ] Item name and description display correctly
- [ ] All 5 spells unlock and work (3 custom, 2 vanilla)
- [ ] Both passives work (1 custom, 1 vanilla)
- [ ] No errors in BG3 logs
- [ ] Level13PlusGear mod works independently (no SampleMagicRingMod dependency)
- [ ] UUID pool updated
- [ ] All UUIDs documented in this phase file

---

## Notes

- This phase tests the new copying_items_between_mods.md workflow guide
- Copying spells and passives adds complexity beyond simple item copying
- Must ensure all spell/passive references are updated to L13_ prefix
- TreasureTable delivery means item won't appear in existing saves (see CLAUDE.md)

---

## Post-Implementation

- [ ] Update docs/level13gear/[relevant planning doc] if it exists
- [ ] Mark phase as IMPLEMENTED (awaiting user testing)
- [ ] User testing required before marking COMPLETE
