# Phase 42: Replace Moonguard Splint

**Status:** ABANDONED
**Date:** 2026-02-11
**Abandonment Date:** 2026-02-11

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

## Phase 42 Status: IMPLEMENTED

**Implementation Date:** 2026-02-11

All existing references to L13_Armor_Moonguard removed. Fresh copy from SampleMagicRingMod created with new UUIDs.

---

## Revision 1

**Date:** 2026-02-11
**Issue:** Moonguard Splint not appearing in L13 chest
**Root Cause:** Incorrect UUID conversion - UUID had 9 characters before first dash instead of 8
**Details:**
- Original UUID: `e6a910a5-4fb8-4b8c-a043-6393a5e74ab5`
- Incorrect conversion: `ed13910a5-4fb8-4b8c-a043-6393a5e74ab5` (added "ed13" to beginning = 9 chars)
- Correct conversion: `ed1310a5-4fb8-4b8c-a043-6393a5e74ab5` (replaced first 4 chars with "ed13" = 8 chars)

**Fix:** Updated RootTemplate UUID in both Armor.txt (line 55) and L13_Armor_Moonguard.lsf.lsx (line 11)
**Note:** UUID conversion must REPLACE the first 4 characters with "ed13", not add "ed13" to the beginning

---

## Revision 2

**Date:** 2026-02-11
**Issue:** Cleanup - OneTimeRewards.lsx contained unwanted Moonguard Splint entry
**Root Cause:** Phase 42 goal was to have Moonguard Splint ONLY in L13_Gear_Chest (TreasureTable), but OneTimeRewards.lsx still had an entry from before
**Details:**
- OneTimeRewards.lsx is a direct item delivery system (separate from TreasureTable)
- Phase 42 goal: Moonguard Splint should ONLY be in L13_Gear_Chest via TreasureTable system
- OneTimeRewards.lsx (line 12-16) had a Moonguard Splint entry with old UUID: `ed13502f-b130-491f-ac5d-53a72f1262b7`
- This entry would have caused the item to be delivered via OneTimeRewards (unintended for Phase 42)

**Fix:** REMOVED the Moonguard Splint entry entirely from OneTimeRewards.lsx
**Important Note:** This was cleanup for Phase 42's specific goals, NOT the fix for the chest appearance issue
**Lesson Learned:** When changing item delivery methods, remove entries from unused delivery systems

**Key Insight:** OneTimeRewards and TreasureTable are independent delivery systems that CAN be used together if you want items in multiple locations. For Phase 42, we only wanted TreasureTable delivery.

---

## Revision 3

**Date:** 2026-02-11
**Issue:** Moonguard Splint still not appearing in L13 chest after Revisions 1 and 2
**Investigation:** Verified all components appear structurally correct:
1. ✓ Armor.txt entry exists with correct UUID format: `ed1310a5-4fb8-4b8c-a043-6393a5e74ab5` (8-4-4-4-12 format)
2. ✓ RootTemplate file (L13_Armor_Moonguard.lsf.lsx) exists with matching MapKey
3. ✓ Localization entries exist for both DisplayName and Description handles
4. ✓ TreasureTable entry exists: `I_L13_Armor_Moonguard` in L13_Gear_Chest_TT (line 35)
5. ✓ RootTemplate structure matches working items (compared to L13_Armor_Rogue)
6. ✓ ParentTemplateId matches source: `42e6357a-4c05-4eda-9415-6b6b4c7d44c5`

**Files Verified:**
- Armor.txt (line 52-61): Entry structure correct
- L13_Armor_Moonguard.lsf.lsx: XML structure valid
- TreasureTable.txt (line 35): Category reference correct
- Level13PlusGear.loca.xml (lines 59-60): Handles present

**Status:** All components appear correct. Issue cause unknown.
**Next Steps:** Awaiting additional details about in-game behavior or other symptoms that might indicate the root cause.

---

## Revision 4

**Date:** 2026-02-11
**Issue:** Moonguard Splint still not appearing, but Armor of the Rogue IS appearing correctly
**Diagnostic Approach:** Compared working item (Armor of the Rogue) with non-working item (Moonguard Splint)

**Key Difference Found:**
```
L13_Armor_Rogue:
- Does NOT have "Ability Modifier Cap" line
- 8 data lines total

L13_Armor_Moonguard:
- HAS "Ability Modifier Cap" line with empty value: data "Ability Modifier Cap" ""
- 9 data lines total
```

**Analysis:**
- Both items are in the same TreasureTable (L13_Gear_Chest_TT)
- Armor of the Rogue appears correctly via TreasureTable (confirms TreasureTable system works)
- Only structural difference: the empty "Ability Modifier Cap" line
- This line exists in source SMR_Armor_Moonguard, but may cause issues with empty value

**Fix:** Removed the `data "Ability Modifier Cap" ""` line from L13_Armor_Moonguard entry in Armor.txt (line 60)

**Hypothesis:** Empty "Ability Modifier Cap" value may prevent item from spawning correctly. If attribute is needed, it should have a value; if not needed, line should be omitted entirely.

**Files Modified:**
- Armor.txt: Removed empty "Ability Modifier Cap" line from L13_Armor_Moonguard

**CRITICAL NOTE - Repeating Phase 38:**
This approach (removing "Ability Modifier Cap") was **already extensively tested in Phase 038** during the original Moonguard Splint implementation:
- Phase 038 Revision 3: Removed "Ability Modifier Cap" - didn't fix it
- Phase 038 Revision 7: Re-added "Ability Modifier Cap" - didn't fix it
- Phase 038 Revision 8: Removed "Ability Modifier Cap" again - still didn't fix it

**Phase 038 Final Conclusion:**
The Moonguard Splint NEVER appeared throughout all 10 revisions of Phase 038. The phase was closed with this as an unresolved bug, concluding that template `ARM_Splint_Body_2` is **incompatible with Level13PlusGear mod for unknown reasons**, despite working correctly in SampleMagicRingMod.

**Implication for Phase 42:**
If the root cause is template incompatibility (as Phase 038 concluded), then tweaking the "Ability Modifier Cap" field will not resolve the issue. A more fundamental solution may be required, such as using a different base template.

---

## Phase 42 Status: ABANDONED

**Abandonment Date:** 2026-02-11

### Reason for Abandonment

Phase 42 attempted to fix the Moonguard Splint issue by completely removing all old references and creating a fresh copy with new UUIDs. However, after 4 revisions, the item still does not appear in the L13 chest.

**Critical Discovery:**
- Revision 4 repeated the same "Ability Modifier Cap" removal approach that was already extensively tested in Phase 038 (Revisions 3, 7, 8)
- Phase 038 concluded after 10 revisions that template `ARM_Splint_Body_2` is incompatible with Level13PlusGear mod
- Despite fresh UUIDs, new localization, and new RootTemplate, the fundamental issue persists

### What Was Tried

**Phase 038 (Original Implementation):**
- 10 revisions attempting various fixes
- Tested "Ability Modifier Cap" field: removed, re-added, removed again
- Tested different ParentTemplateId values
- Tested different delivery methods (TreasureTable, OneTimeRewards)
- **Result:** UNRESOLVED - Phase closed with known bug

**Phase 042 (Fresh Copy Attempt):**
- Complete removal of all old references
- Fresh copy with entirely new UUIDs and handles
- Revision 1: Fixed UUID format error (9 chars → 8 chars)
- Revision 2: Cleaned up old OneTimeRewards entry
- Revision 3: Verified all components structurally correct
- Revision 4: Repeated Phase 038's failed "Ability Modifier Cap" removal
- **Result:** ABANDONED - Repeating failed approaches

### Technical Analysis

**Template Investigation:**
- `ARM_Splint_Body_2` EXISTS in vanilla BG3 (confirmed in Shared/Armor.txt)
- NO vanilla items in gustav use this template
- SampleMagicRingMod successfully uses it (confirmed working)
- Level13PlusGear has NEVER been able to make it work

**Known Working Templates in Level13PlusGear:**
- `ARM_StuddedLeather_Body_2` (L13_Armor_Rogue) ✅
- `ARM_ChainShirt_Body_1` (L13_Armor_Voss in Phase 038) ✅

**Known Problematic Templates in Level13PlusGear:**
- `ARM_Splint_Body_2` (L13_Armor_Moonguard) ❌
- `ARM_HalfPlate_Body_2` (L13_Armor_Tyr) ❌

### Conclusion

The issue with Moonguard Splint is not due to:
- UUID formatting errors (fixed in Revision 1)
- Old remnant entries (cleaned in Revision 2)
- RootTemplate structure issues (verified correct in Revision 3)
- "Ability Modifier Cap" field presence/absence (tested extensively in both phases)

**The root cause appears to be an incompatibility between:**
- The `ARM_Splint_Body_2` template
- The Level13PlusGear mod configuration/structure

**Why This Incompatibility Exists:** Unknown. The same template works perfectly in SampleMagicRingMod.

### Alternatives for Future Consideration

If Moonguard Splint functionality is needed in Level13PlusGear:

**Option 1: Different Template**
- Change `using` template to a working one (e.g., `ARM_ChainShirt_Body_1`)
- Item would appear and function correctly
- Visual appearance would differ from intended design

**Option 2: Deep Investigation**
- Compare Level13PlusGear vs SampleMagicRingMod mod structures
- Check for missing dependencies or configurations
- Test load order effects
- Examine mod-specific factors

**Option 3: Accept Limitation**
- Document `ARM_Splint_Body_2` as incompatible with Level13PlusGear
- Do not attempt to add items using this template
- Use alternative templates for similar items

### Files in Final State

**Modified Files (from Phase 42 implementation):**
- Armor.txt: L13_Armor_Moonguard entry exists (lines 52-60) with no "Ability Modifier Cap"
- L13_Armor_Moonguard.lsf.lsx: RootTemplate exists with UUID ed1310a5-4fb8-4b8c-a043-6393a5e74ab5
- TreasureTable.txt: Item listed in L13_Gear_Chest_TT (line 35)
- Level13PlusGear.loca.xml: Fresh localization entries exist (lines 59-60)
- OneTimeRewards.lsx: Moonguard removed (only Armor of Tyr remains)

**Status:** All Phase 42 changes remain in place but item does not appear in-game.

### Lessons Learned

1. **Template compatibility varies by mod** - Same template works in one mod but not another
2. **Fresh start doesn't fix fundamental issues** - New UUIDs/handles don't resolve template incompatibility
3. **Document failed approaches** - Prevents repeating the same failed solutions
4. **Know when to stop** - After 14+ revisions across two phases, accept the limitation
5. **Alternative approaches exist** - Different templates can achieve similar functionality

---

## Related Documentation

- **Phase038.md** - Original 10-revision attempt to implement Moonguard Splint (UNRESOLVED)
- **docs/instructions/copying_items_between_mods.md** - Item copy workflow
- **docs/instructions/uuid_workflow.md** - UUID pool and naming conventions
- **docs/planning/item_catalog.md** - SampleMagicRingMod source items (confirms Moonguard works there)

---

**Phase 42 is now ABANDONED.** The Moonguard Splint remains a documented incompatibility with Level13PlusGear mod.
