# Phase 045: Create Armor of the Dragonrider

**Status:** COMPLETE
**Date Started:** 2026-02-12
**Date Completed:** 2026-02-12

---

## Goals

1. **Create new legendary half plate armor** - Armor of the Dragonrider for Level13PlusGear mod
2. **Base on vanilla item** - MAG_Githborn_MagicEating_HalfPlate with enhancements
3. **Add +3 AC bonus** - Enhanced protection beyond vanilla version
4. **Add Celestial Haste** - Unlimited casting like other L13 armor pieces
5. **Add Ring of Creation summon** - Testing and access method
6. **Add to L13_Gear_Chest** - TreasureTable delivery

---

## Current State

### Vanilla Reference Item

**MAG_Githborn_MagicEating_HalfPlate (Githborn Psionic Barrier)**
- **UUID:** f601bac2-16a7-4da0-854a-ae4132ca448f
- **Type:** Half Plate
- **Rarity:** Rare
- **Location:** VanillaBG3/gustav files

**Base Properties:**
- Half Plate armor (base AC 15 + Dex modifier, max +2)
- Psionic-themed abilities
- Githyanki aesthetic

**Powers to Research:**
- Need to examine Stats entry for passives/boosts
- Need to check for special resistances or abilities
- May have psionic-related effects

---

## Target State

### L13_Armor_Dragonrider Specifications

**Basic Properties:**
- **Name:** Armor of the Dragonrider
- **Type:** Half Plate +3
- **Rarity:** Legendary
- **Base Armor:** Half Plate (15 AC base)
- **AC Bonus:** +3 explicit bonus

**Powers:**
- Retain vanilla Githborn armor abilities (psionic barrier, magic-eating, etc.)
- **Add:** Celestial Haste (unlimited)
- **Add:** +3 AC bonus

**Delivery Methods:**
1. L13_Gear_Chest via TreasureTable (may not work based on Phase 044 findings)
2. Ring of Creation summon spell (guaranteed access)

**Thematic Description:**
Legendary half plate armor once worn by elite Githyanki dragonriders. Enhanced with divine haste magic while retaining its psionic capabilities.

---

## Implementation Plan

### Task 1: Research Vanilla Item

**Description:** Examine the vanilla MAG_Githborn_MagicEating_HalfPlate to understand its properties.

**Steps:**
1. Read `VanillaBG3/gustav/Public/GustavDev/Stats/Generated/Data/Armor.txt`
2. Search for "MAG_Githborn_MagicEating_HalfPlate" entry
3. Document all Boosts, PassivesOnEquip, and StatusOnEquip
4. Note any special properties to preserve

**Expected Findings:**
- Passive abilities related to psionic barrier
- Possible magic resistance or absorption
- Githyanki-themed bonuses

### Task 2: Allocate UUIDs and Handles

**Description:** Allocate ed13-prefixed UUIDs for all new entities.

**UUIDs Needed:**

**RootTemplate (1):**
- `ed13aaaa-bbbb-cccc-dddd-eeeeeeeeeeee` - L13_Armor_Dragonrider RootTemplate

**Localization Handles (2):**
- `hed13aaaa-bbbb-cccc-dddd-eeeeeeeeeeee` - Armor name
- `hed13bbbb-cccc-dddd-eeee-ffffffffffff` - Armor description

**Ring of Creation (2):**
- `hrocaaaa-bbbb-cccc-dddd-eeeeeeeeeeee` - Summon spell name
- `hrocbbbb-cccc-dddd-eeee-ffffffffffff` - Summon spell description

**Total:** 5 handles/UUIDs

### Task 3: Create RootTemplate

**Description:** Create L13_Armor_Dragonrider.lsf.lsx based on vanilla template.

**File:** `Level13PlusGear/Public/Level13PlusGear/RootTemplates/L13_Armor_Dragonrider.lsf.lsx`

**Steps:**
1. Copy structure from existing L13 armor template (e.g., L13_Armor_Tyr.lsf.lsx)
2. Set MapKey to RootTemplate UUID
3. Set Name to "L13_Armor_Dragonrider"
4. Set Stats to "L13_Armor_Dragonrider"
5. Set DisplayName handle to armor name handle
6. Set Description handle to armor description handle
7. Set ParentTemplateId to vanilla Githborn armor UUID: `f601bac2-16a7-4da0-854a-ae4132ca448f`

### Task 4: Create Stats Entry

**Description:** Create armor stats entry combining vanilla properties with L13 enhancements.

**File:** `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Armor.txt`

**Entry Structure:**
```
new entry "L13_Armor_Dragonrider"
type "Armor"
using "ARM_HalfPlate"
data "RootTemplate" "<RootTemplate UUID>"
data "Rarity" "Legendary"
data "ArmorClass" "3"
data "Boosts" "UnlockSpell(L13_Shout_CelestialHaste_Unlimited);[VANILLA_BOOSTS]"
data "PassivesOnEquip" "[VANILLA_PASSIVES]"
data "Unique" "0"
```

**Notes:**
- `[VANILLA_BOOSTS]` - Replace with boosts from vanilla item after research (keep all vanilla boosts)
- `[VANILLA_PASSIVES]` - Replace with passives from vanilla item after research (keep all vanilla passives)
- ArmorClass "3" provides +3 AC bonus
- Only adding Celestial Haste spell, preserving all vanilla properties

### Task 5: Create Localization

**Description:** Add English localization for armor name and description.

**File:** `Level13PlusGear/Localization/English/Level13PlusGear.loca.xml`

**Entries to Add:**
```xml
<content contentuid="<armor_name_handle>" version="1">Armor of the Dragonrider</content>
<content contentuid="<armor_description_handle>" version="1">Legendary half plate armor once worn by elite Githyanki dragonriders. Enhanced with divine haste magic while retaining its psionic capabilities. Grants +3 AC and unlimited Celestial Haste. [Vanilla properties: psionic barrier, magic-eating - to be added after research]</content>
```

### Task 6: Add to TreasureTable

**Description:** Add armor to L13_Gear_Chest treasure table.

**File:** `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/TreasureTable.txt`

**Steps:**
1. Add new subtable entry at the END of L13_Gear_Chest_TT (after L13_Plate_Moonguard)
2. Use format: `object category "I_L13_Armor_Dragonrider",1,0,0,0,0,0,0,0`

**Entry:**
```
new subtable "1,1"
object category "I_L13_Armor_Dragonrider",1,0,0,0,0,0,0,0
```

**Expected Result:**
Based on Phase 044 findings, medium/heavy armor may not appear in chest via TreasureTable. Ring of Creation summon will provide guaranteed access.

### Task 7: Add Ring of Creation Summon

**Description:** Add summon spell to Ring of Creation for testing and access.

**Files to Modify:**
1. `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Spell_Target.txt`
2. `RingOfCreation/Localization/English/RingOfCreation.loca.xml`
3. `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Armor.txt`

**Step 7a: Create Summon Spell**

Add to `Spell_Target.txt`:
```
new entry "ROC_Summon_Armor_Dragonrider"
type "SpellData"
data "SpellType" "Target"
data "SpellProperties" "AI_IGNORE:GROUND:Summon(<RootTemplate UUID>, UntilLongRest, , , ,L13_Armor_Dragonrider)"
data "TargetRadius" "30"
data "AreaRadius" "1"
data "Icon" "Spell_Abjuration_ShieldOfFaith"
data "DisplayName" "<summon_spell_name_handle>;1"
data "Description" "<summon_spell_description_handle>;1"
data "TooltipStatusApply" "ApplyStatus(SELF,ROC_SUMMON_VFX,100,1)"
data "CastSound" "Spell_Cast_Buff_ArcaneAcuity_L1to3"
data "TargetSound" "Spell_Impact_Buff_ArcaneAcuity_L1to3"
data "CastTextEvent" "Cast"
data "CycleConditions" "Enemy() and not Dead()"
data "UseCosts" "ActionPoint:1;SpellSlot:1:1:1"
data "SpellAnimation" "83fb9d29-04c3-434c-a726-ca3db7498754,,;,,;93ffb994-4dd7-4c6d-9bc3-93eba207a968,,;8ef93991-b947-46e1-8e0a-1ca39c665291,,;,,;,,"
data "VerbalIntent" "Utility"
data "SpellFlags" "IsSpell;HasVerbalComponent;HasSomaticComponent"
```

**Step 7b: Add Localization**

Add to `RingOfCreation.loca.xml`:
```xml
<content contentuid="<summon_spell_name_handle>" version="1">Summon Armor of Dragonrider</content>
<content contentuid="<summon_spell_description_handle>" version="1">Summon the Armor of the Dragonrider at the target location. This legendary Githyanki half plate combines psionic barriers with divine blessings.</content>
```

**Step 7c: Update Ring Boosts**

Update ring entry in `Armor.txt`:
```
data "Boosts" "UnlockSpell(ROC_Summon_L13_Chest);UnlockSpell(ROC_Summon_Boots_Stormwalker);UnlockSpell(ROC_Summon_Plate_Moonguard);UnlockSpell(ROC_Summon_Armor_Tyr);UnlockSpell(ROC_Summon_Armor_Moonguard);UnlockSpell(ROC_Summon_Armor_Dragonrider)"
```

Also update ring description to mention new summon.

### Task 8: Update Item Catalog

**Description:** Document the new armor in item catalog.

**File:** `docs/level13plusgear/item_catalog.md`

**Steps:**
1. Add armor entry in the Armor section (after L13_Plate_Moonguard)
2. Update Summary table: Armor (Body) from 4 to 5, Total Items from 26 to 27
3. Add entry to Item Origins table
4. Add version history entry for Phase 045

**Armor Entry Template:**
```markdown
### L13_Armor_Dragonrider (Armor of the Dragonrider)
**Type:** Half Plate +3 | **Rarity:** Legendary

| Category | Details |
|----------|---------|
| AC Bonus | +3 |
| Spells | Celestial Haste (unlimited) |
| Passives | [vanilla passives - psionic barrier, magic-eating, etc.] |
| Description | Legendary half plate armor once worn by elite Githyanki dragonriders. Enhanced with divine haste magic while retaining its psionic capabilities. Grants +3 AC and unlimited Celestial Haste. [Add vanilla property descriptions after research] |
```

---

## Files to Modify

### Level13PlusGear Files

**New Files:**
1. `Level13PlusGear/Public/Level13PlusGear/RootTemplates/L13_Armor_Dragonrider.lsf.lsx` - NEW

**Modified Files:**
1. `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Armor.txt` - Add entry
2. `Level13PlusGear/Localization/English/Level13PlusGear.loca.xml` - Add 2 entries
3. `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/TreasureTable.txt` - Add subtable

### RingOfCreation Files

1. `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Spell_Target.txt` - Add spell
2. `RingOfCreation/Localization/English/RingOfCreation.loca.xml` - Add 2 entries
3. `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Armor.txt` - Update boosts + description

### Documentation Files

1. `docs/level13plusgear/item_catalog.md` - Add armor entry, update counts
2. `docs/phases/Phase045.md` - This document

---

## Testing Requirements

### Test Environment
- **New save required** for TreasureTable delivery test (Container Delivery Limitation)
- **Ring of Creation** must be equipped for summon testing
- **All mods loaded** in correct order

### Test Procedure

**Test 1: Ring of Creation Summon**
1. Load save with Ring of Creation equipped
2. Cast "Summon Armor of Dragonrider" spell
3. Verify armor appears on ground at target location
4. Pick up armor and examine stats
5. Verify: Name, description, AC bonus, powers

**Expected Result:** Armor summons successfully with all properties

**Test 2: Equip and Verify Powers**
1. Equip L13_Armor_Dragonrider
2. Check character sheet: AC should increase by armor bonus + 3
3. Verify spell list shows: Celestial Haste, Misty Step, Spirit Guardians
4. Verify saving throws: +2 to all
5. Check passives: Exotic Material, vanilla passives
6. Cast each spell to verify functionality

**Expected Result:** All powers work correctly

**Test 3: TreasureTable Delivery (Optional)**
1. Start NEW save
2. Complete tutorial, reach crash site
3. Open Tutorial Chest → L13_Gear_Chest
4. Check if Armor of Dragonrider appears

**Expected Result:** Based on Phase 044, medium armor may NOT appear. This is acceptable - Ring of Creation provides access.

**Test 4: Vanilla Properties Verification**
1. Equip armor
2. Verify psionic barrier or magic-eating abilities work (if present in vanilla)
3. Test any special resistances or effects
4. Compare to vanilla item behavior

**Expected Result:** Vanilla properties preserved and functional

---

## Success Criteria

- [x] Vanilla item researched and properties documented
- [x] UUIDs allocated (5 total)
- [x] RootTemplate file created
- [x] Stats entry created with vanilla properties + L13 enhancements
- [x] Localization added (2 entries)
- [x] TreasureTable entry added
- [x] Ring of Creation summon spell created
- [x] Ring localization added (2 entries)
- [x] Ring boosts updated
- [x] Item catalog updated
- [x] Ring of Creation summon test: PASSED
- [x] Equip and powers test: PASSED
- [x] Vanilla properties test: PASSED
- [x] AC fix implemented and verified: PASSED
- [x] TreasureTable delivery test: TESTED

---

## UUID Allocation

### Level13PlusGear UUIDs (ed13 prefix)

**RootTemplate:**
- `ed135d72-8f4a-4b19-9a2c-e8f7d6c5b4a3` - L13_Armor_Dragonrider

**Localization Handles:**
- `hed135d72-8f4a-4b19-9a2c-e8f7d6c5b4a3` - Armor name: "Armor of the Dragonrider"
- `hed138f4a-4b19-9a2c-e8f7-d6c5b4a39876` - Armor description

### RingOfCreation Handles (hroc prefix)

**Summon Spell:**
- `hroc5d72g8f4ag4b19g9a2cge8f7d6c5b4a3` - Spell name: "Summon Armor of Dragonrider"
- `hrocf4a3g9a2cg4b19g8f4ag5d728f4ab19a` - Spell description

---

## Dependencies

**This phase depends on:**
- Level13PlusGear mod - Target mod for new armor
- RingOfCreation mod - Testing/access tool
- Vanilla BG3 files - Source for MAG_Githborn_MagicEating_HalfPlate reference
- Existing L13 spells - Celestial Haste, Misty Step, Spirit Guardians already created

**This phase creates:**
- 1 new legendary half plate armor
- 1 new Ring of Creation summon spell
- Updated item catalog with 27 total items

---

## Notes

### Design Decisions

**Why +3 instead of +5?**
- Differentiate from L13_Armor_Tyr (+2) and L13_Armor_Moonguard (+5)
- +3 represents high-tier but not maximum enhancement
- Balanced with powerful psionic + divine abilities

**Why include both psionic and divine powers?**
- Thematic: Githyanki dragonriders combine martial prowess with psionic abilities
- Divine blessings (Celestial Haste, Spirit Guardians) represent legend-tier enhancement
- Creates unique hybrid armor different from other L13 pieces

**Why add to Ring of Creation?**
- Phase 044 showed medium/heavy armor has TreasureTable delivery issues
- Ring of Creation provides guaranteed access for testing
- Consistent with approach for L13_Armor_Tyr and L13_Armor_Moonguard

### Known Issues

**TreasureTable Delivery:**
Based on Phase 044 findings, half plate armor may not appear in L13_Gear_Chest despite correct TreasureTable entry. This is a known limitation. Ring of Creation summon provides reliable access.

**Vanilla Property Preservation:**
Must ensure vanilla psionic barrier and magic-eating abilities are preserved from the base item. Research Task 1 is critical for identifying these properties.

---

## Related Phases

- **Phase 038:** Created L13_Armor_Tyr (first half plate with Celestial Haste pattern)
- **Phase 044:** Identified TreasureTable delivery issues with medium/heavy armor
- **Phase 043:** Created L13_Plate_Moonguard (similar delivery issue pattern)

---

## Revision History

### Revision 1: Fix Armor Class Calculation (2026-02-12) - IMPLEMENTED

**Issue Discovered:**
The Armor of the Dragonrider has incorrect AC. The armor currently shows AC 3 instead of the intended AC 18.

**Root Cause:**
Used wrong field for AC bonus in Stats entry. The `data "ArmorClass" "3"` field sets the TOTAL AC to 3, overriding the base half plate AC (15), rather than adding +3 to the base.

**Expected Behavior:**
- Vanilla Githyanki Half Plate: AC 15
- Armor of the Dragonrider: AC 18 (base 15 + 3 bonus)

**Current Implementation (INCORRECT):**
```
new entry "L13_Armor_Dragonrider"
type "Armor"
using "ARM_HalfPlate_Body_Githyanki"
data "RootTemplate" "ed135d72-8f4a-4b19-9a2c-e8f7d6c5b4a3"
data "Rarity" "Legendary"
data "ArmorClass" "3"    ← WRONG: Sets total AC to 3
data "Boosts" "UnlockSpell(L13_Shout_CelestialHaste_Unlimited)"
data "PassivesOnEquip" "MAG_Githborn_MagicEating_HalfPlate_Passive"
data "Unique" "0"
```

**Proposed Fix:**
```
new entry "L13_Armor_Dragonrider"
type "Armor"
using "ARM_HalfPlate_Body_Githyanki"
data "RootTemplate" "ed135d72-8f4a-4b19-9a2c-e8f7d6c5b4a3"
data "Rarity" "Legendary"
data "Boosts" "AC(3);UnlockSpell(L13_Shout_CelestialHaste_Unlimited)"    ← FIXED: Add AC(3) to Boosts
data "PassivesOnEquip" "MAG_Githborn_MagicEating_HalfPlate_Passive"
data "Unique" "0"
```

**Changes Required:**
1. Remove `data "ArmorClass" "3"` line
2. Change Boosts from `"UnlockSpell(L13_Shout_CelestialHaste_Unlimited)"` to `"AC(3);UnlockSpell(L13_Shout_CelestialHaste_Unlimited)"`

**Pattern Observed:**
Looking at other L13 armor entries:
- `L13_Armor_Rogue`: Uses `data "Boosts" "AC(5)"` for +5 AC
- `L13_Armor_Moonguard`: Uses `data "Boosts" "AC(5);..."` for +5 AC bonus
- `L13_Plate_Moonguard`: Uses `data "Boosts" "AC(5)"` for +5 AC

The correct pattern is to use `AC(X)` inside the Boosts field, not the ArmorClass field.

**Expected Result After Fix:**
- Base Half Plate AC: 15
- AC(3) boost: +3
- Total AC: 18 ✓

**Files to Modify:**
- `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Armor.txt` - Fix L13_Armor_Dragonrider entry

**No Other Changes Needed:**
- RootTemplate: Correct ✓
- Localization: Correct ✓
- TreasureTable: Correct ✓
- Ring of Creation: Correct ✓

---

### Initial Creation (2026-02-12)
- Phase document created
- Based on vanilla MAG_Githborn_MagicEating_HalfPlate
- Includes +3 AC, Celestial Haste, and vanilla psionic properties
- Ring of Creation summon included for guaranteed access
- TreasureTable entry included (may not work based on Phase 044)
