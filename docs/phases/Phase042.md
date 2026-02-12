# Phase 42: Replace Moonguard Splint

**Status:** PENDING
**Date:** 2026-02-11

---

## Goals

1. **Step 1 - Remove Existing:** Remove all references to L13_Armor_Moonguard (Moonguard Splint) from Level13PlusGear mod
2. **Step 2 - Copy Fresh:** Copy Moonguard Splint from SampleMagicRingMod to Level13PlusGear with fresh implementation
3. **Maintain Independence:** Ensure the new implementation is fully independent from SampleMagicRingMod
4. **Complete Documentation:** Update item catalog and track all changes

**Prerequisite:** Phase 41 must be completed (Ring of the Guardian)

---

## Phase 42 Overview

This phase involves a complete replacement of the Moonguard Splint item. The existing L13_Armor_Moonguard will be removed entirely and replaced with a fresh copy from SampleMagicRingMod.

**Why Replace:**
- Potential implementation issues with the current version
- Ensures clean, fresh implementation
- Verifies all components are correctly configured

---

## Step 1: Remove Existing L13_Armor_Moonguard

### Files to Modify (Removal)

| File | Action | Location |
|------|--------|----------|
| Armor.txt | Remove L13_Armor_Moonguard entry | Stats/Generated/Data/Armor.txt |
| TreasureTable.txt | Remove I_L13_Armor_Moonguard entry | Stats/Generated/TreasureTable.txt |
| RootTemplate | Delete L13_Armor_Moonguard.lsf.lsx | RootTemplates/L13_Armor_Moonguard.lsf.lsx |
| Localization | Remove 2 entries (name + description) | Localization/English/Level13PlusGear.loca.xml |

### Current Implementation Details

**From Previous Phase (Phase 038):**
- Item Name: Moonguard Splint (L13_Armor_Moonguard)
- Type: Splint Armor +5
- Rarity: Legendary
- Features: +5 AC, +2 saves, full Dex bonus, Celestial Haste, Misty Step, Spirit Guardians, HP regeneration

**UUIDs Used (will be freed up):**
- RootTemplate MapKey UUID
- DisplayName handle UUID
- Description handle UUID

**Note:** Custom spells used by this item (Celestial Haste, Misty Step, Spirit Guardians) are shared with other items and should NOT be removed.

### Removal Checklist

- [ ] Remove entry from Armor.txt
- [ ] Remove entry from TreasureTable.txt
- [ ] Delete RootTemplate file
- [ ] Remove localization entries (2 total)
- [ ] Verify no other items depend on this specific entry

---

## Step 2: Copy Fresh Moonguard Splint

### Source Item Analysis

**Source:** SampleMagicRingMod - SMR_Armor_Moonguard

**Need to Verify:**
- Base armor type and stats
- Boosts and PassivesOnEquip
- Spell unlocks
- ParentTemplateId for RootTemplate

### Implementation Steps

1. **Read source item** from SampleMagicRingMod/Armor.txt
2. **Create new Armor.txt entry** with L13_ prefix
3. **Create new RootTemplate** with fresh UUIDs
4. **Add to TreasureTable** (L13_Gear_Chest_TT only)
5. **Add localization** for DisplayName and Description
6. **Update UUID pool** (remove newly used UUIDs)
7. **Update item catalog** (replace old entry with new)

### Estimated Resource Requirements

| Component | Count | UUIDs Needed |
|-----------|-------|--------------|
| RootTemplate | 1 | 1 (MapKey) |
| Localization | 2 | 2 (DisplayName + Description) |
| **Total** | **1 item** | **3 UUIDs** |

**Net UUID Change:** 0 (3 freed from removal, 3 used for new implementation)

---

## Success Criteria

### Step 1 - Removal Complete
- [ ] L13_Armor_Moonguard removed from Armor.txt
- [ ] I_L13_Armor_Moonguard removed from TreasureTable.txt
- [ ] L13_Armor_Moonguard.lsf.lsx deleted
- [ ] 2 localization entries removed
- [ ] No broken references remain

### Step 2 - Fresh Copy Complete
- [ ] New L13_Armor_Moonguard entry in Armor.txt
- [ ] New RootTemplate created with fresh UUIDs
- [ ] Item added to L13_Gear_Chest_TT treasure table
- [ ] New localization entries created
- [ ] UUID pool updated
- [ ] Item catalog updated
- [ ] No dependencies on SampleMagicRingMod
- [ ] Item tested in-game
- [ ] Item appears in L13 chest
- [ ] All spells and passives functional

---

## Testing Plan

### Basic Functionality
1. Moonguard Splint appears in L13 Gear Chest
2. Item can be equipped
3. Item displays correct stats and description

### Spell Testing
1. Celestial Haste works (unlimited)
2. Misty Step works (unlimited)
3. Spirit Guardians works (both Radiant and Necrotic variants)
4. All spells have correct cooldowns

### Passive Testing
1. +5 AC bonus applies
2. +2 to all saves applies
3. Full Dexterity bonus to AC applies
4. HP regeneration (1d4 per turn) works in combat
5. Exotic Material passive works

---

## Notes

**Why This Approach:**
- Complete removal ensures no remnants of old implementation
- Fresh copy guarantees all components are correctly configured
- Maintains clean separation from SampleMagicRingMod
- Allows verification that all systems work correctly

**Shared Components:**
The following custom spells are used by multiple items and should NOT be removed:
- L13_Shout_CelestialHaste_Unlimited
- L13_Target_MistyStep_Unlimited
- L13_Shout_SpiritGuardians_Tyr (container + variants)

**Item Delivery:**
- Item will ONLY be added to L13_Gear_Chest_TT (the Level 13 chest)
- Item will NOT be added to TUT_Chest_Potions (tutorial chest injection)
- This ensures the item only appears in the dedicated L13 chest

---

## Related Documentation

- **Phase038.md** - Original Moonguard Splint implementation
- **docs/instructions/copying_items_between_mods.md** - Item copy workflow
- **docs/instructions/uuid_workflow.md** - UUID pool and naming conventions
- **docs/planning/item_catalog.md** - SampleMagicRingMod source items
- **docs/level13plusgear/item_catalog.md** - Level13PlusGear target catalog

---

## Phase 42 Status: PENDING

**Prerequisite:** Phase 41 must be completed first.

**Ready to begin:** Awaiting user confirmation to proceed with implementation.
