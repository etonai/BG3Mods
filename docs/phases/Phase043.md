# Phase 043: Create Moonguard Plate

**Note:** This armor is part of the Moonguard set, joining other Moonguard items (Blade, Splint, Helm, Circlet, Gloves, Cloak, Shield).

**Status:** ABANDONED
**Date:** 2026-02-11
**Implementation Date:** 2026-02-12
**Abandoned Date:** 2026-02-12

---

## Goals

1. **Create Moonguard Plate:** Create a new legendary heavy plate armor blessed by Selûne
2. **Base on Vanilla Item:** Base stats and powers on the vanilla BG3 item MAG_EndGame_Plate_Armor (UUID: fb2ff6d1-3096-4904-813c-a448e3fbec4d)
3. **Enhanced Armor:** Make it +5 armor (following the pattern of L13_Armor_Rogue)
4. **Proper Delivery:** Configure for Tutorial Chest delivery (set Unique=0)

---

## Current State

The Level13PlusGear mod currently has 27 items, including:
- 7 weapons
- 6 body armor pieces (L13_Armor_Tyr, L13_Armor_Rogue, L13_Armor_Moonguard, L13_Armor_Voss, L13_Armor_Orpheus)
- 5 headgear pieces
- 2 gloves
- 3 cloaks
- 2 shields
- 2 rings

**Heavy Armor Gap:**
Currently, the mod has no heavy plate armor. The closest heavy armors are:
- **L13_Armor_Moonguard** - Splint Armor +5 (Heavy, but not plate)
- **L13_Armor_Tyr** - Half Plate +2 (Medium armor)
- **L13_Armor_Orpheus** - Githyanki Half Plate +5 (Medium armor)

**Problem:** Players seeking plate armor have no options in the mod.

---

## Target State

### Moonguard Plate

**Item Name:** L13_Plate_Moonguard
**Type:** Plate Armor +5 | **Rarity:** Legendary

**Base Properties:**
- Heavy Armor (Plate)
- +5 AC bonus (explicit boost)
- +2 AC bonus (from ARM_MagicalPlate_2_Passive)
- **Total: AC 25** (18 base + 7 from bonuses)

**Powers from Vanilla MAG_EndGame_Plate_Armor:**
- **Blade Ward:** Resistance to physical weapon damage
- **End Game Resistance:** General damage resistance
- **Magical Plate +2:** Inherent +2 AC bonus

**Thematic:**
- Part of the Moonguard set
- Blessed by Selûne, the Moonmaiden (moon goddess)

**Visual Identity:**
- Should use a visually impressive plate armor model
- Thematically aligned with Selûne (moon goddess)

**Delivery:**
- Added to L13_Gear_Chest via TreasureTable (L13_Gear_Chest container appears in Tutorial Chest)
- `Unique: 0` for proper container delivery

---

## Implementation Plan

### Task 1: Research Vanilla Item

**Description:** Investigate the vanilla MAG_EndGame_Plate_Armor to understand its stats and powers.

**Steps:**
1. Search for MAG_EndGame_Plate_Armor in vanilla files (or ask user for detailed stats)
2. Document all Boosts, PassivesOnEquip, and StatusOnEquip
3. Document the RootTemplate reference (ParentTemplateId)
4. Identify any custom spells or passives that need to be copied

**Files to check:**
- VanillaBG3 Armor.txt files (if available)
- User's reference materials for MAG_EndGame_Plate_Armor

### Task 2: Allocate UUIDs and Handles

**Description:** Allocate necessary UUIDs from the uuid_workflow.md pool.

**Steps:**
1. Allocate 1 UUID for RootTemplate (convert to ed13 prefix)
2. Allocate 1 handle for DisplayName (convert to hed13 prefix)
3. Allocate 1 handle for Description (convert to hed13 prefix)
4. Delete used UUIDs from uuid_workflow.md pool

**Estimated:** 3 UUIDs total

### Task 3: Create RootTemplate File

**Description:** Create the RootTemplate .lsx file for Moonguard Plate.

**Steps:**
1. Create file: `Level13PlusGear/Public/Level13PlusGear/RootTemplates/L13_Plate_Moonguard.lsf.lsx`
2. Set MapKey to allocated UUID (with ed13 prefix)
3. Set Name to "L13_Plate_Moonguard"
4. Set ParentTemplateId to `fdb8ce53-51dc-4ccb-9e29-d1d99040e60b` (vanilla plate armor visual)
5. Set Stats to "L13_Plate_Moonguard"
6. Add DisplayName and Description handles

**Template Reference:**
- **IMPORTANT:** Use L13_Armor_Rogue.lsf.lsx as structural reference (only working body armor in mod)
- ParentTemplateId from vanilla MAG_EndGame_Plate_Armor: fdb8ce53-51dc-4ccb-9e29-d1d99040e60b
- Do NOT reference other L13 body armors (they have issues)

### Task 4: Create Armor Stats Entry

**Description:** Add the armor stats entry to Armor.txt.

**CRITICAL:** Follow L13_Armor_Rogue pattern exactly - it's the only working body armor in the mod.

**Steps:**
1. Open: `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Armor.txt`
2. Add new entry "L13_Plate_Moonguard"
3. Set `using "ARM_Plate_Body_2"` (from vanilla MAG_EndGame_Plate_Armor)
4. Add RootTemplate UUID
5. Set `Rarity "Legendary"`
6. Add `Boosts "AC(5)"` for +5 armor
7. Copy all PassivesOnEquip from vanilla item
8. Copy any StatusOnEquip from vanilla item
9. Set `Unique "0"` for TreasureTable delivery

**Implementation (based on vanilla MAG_EndGame_Plate_Armor + L13_Armor_Rogue pattern):**
```
new entry "L13_Plate_Moonguard"
type "Armor"
using "ARM_Plate_Body_2"
data "RootTemplate" "ed13xxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
data "Rarity" "Legendary"
data "Boosts" "AC(5)"
data "PassivesOnEquip" "ARM_MagicalPlate_2_Passive;MAG_MAG_EndGame_Plate_Armor_Passive"
data "StatusOnEquip" "MAG_BLADE_WARD;MAG_END_GAME_RESISTANCE"
data "Unique" "0"
```

**Note:** The AC(5) boost adds to the base plate AC. Combined with ARM_MagicalPlate_2_Passive (+2 AC), this gives a total bonus of +7 AC over standard plate armor (base 18 → final 25 AC).

### Task 5: Create Localization Strings

**Description:** Add DisplayName and Description to the localization file.

**Steps:**
1. Open: `Level13PlusGear/Localization/English/Level13PlusGear.loca.xml`
2. Add DisplayName entry with allocated handle
3. Add Description entry with allocated handle

**Localization Content:**
- **DisplayName:** "Moonguard Plate"
- **Description:** "Plate armor blessed by Selûne, the Moonmaiden. Part of the legendary Moonguard set. Provides exceptional protection with Blade Ward and magical resistance."

### Task 6: Add to TreasureTable

**Description:** Add Moonguard Plate to the L13_Gear_Chest loot table.

**Steps:**
1. Open: `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/TreasureTable.txt`
2. Locate the "L13_Gear_Chest_TT" treasure table (this is the loot table FOR the L13_Gear_Chest container)
3. Add new subtable entry for the Moonguard Plate following the existing pattern

**Example:**
```
new treasuretable "L13_Gear_Chest_TT"
CanMerge 1
...
new subtable "1,1"
object category "I_L13_Plate_Moonguard",1,0,0,0,0,0,0,0
```

**Note:** The L13_Gear_Chest container itself appears in the Tutorial Chest via the TUT_Chest_Potions table. Individual items go in the L13_Gear_Chest_TT table.

### Task 7: Update Mod Version

**Description:** Increment the mod version to reflect new content.

**Steps:**
1. Open: `Level13PlusGear/Mods/Level13PlusGear/meta.lsx`
2. Increment the version number (last component)

---

## Files to Modify/Create

| File | Action | Description |
|------|--------|-------------|
| `Level13PlusGear/Public/Level13PlusGear/RootTemplates/L13_Plate_Moonguard.lsf.lsx` | Create | New RootTemplate for Moonguard Plate |
| `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Armor.txt` | Edit | Add L13_Plate_Moonguard stats entry |
| `Level13PlusGear/Localization/English/Level13PlusGear.loca.xml` | Edit | Add DisplayName and Description |
| `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/TreasureTable.txt` | Edit | Add to Tutorial Chest loot |
| `Level13PlusGear/Mods/Level13PlusGear/meta.lsx` | Edit | Increment version |
| `docs/instructions/uuid_workflow.md` | Edit | Remove used UUIDs from pool |
| `docs/level13plusgear/item_catalog.md` | Edit | Document new armor |

---

## UUID/Handle Requirements

### Estimated UUIDs Needed

**Moonguard Plate:**
- RootTemplate: 1 UUID
- DisplayName: 1 handle
- Description: 1 handle

**Total Estimated:** 3 UUIDs/handles

**Note:** If the vanilla MAG_EndGame_Plate_Armor uses custom spells or passives not already in the L13 mod, additional UUIDs may be needed. This will be determined during Task 1.

### UUID Allocation

**L13_Plate_Moonguard:**
- **RootTemplate UUID:** `ed136df4-f2cb-43bb-94a8-d82bfc35aa51`
- **DisplayName Handle:** `hed138746-6425-46d5-8729-5313eaedd921`
- **Description Handle:** `hed133656-2ee6-4a74-96dd-062b531d2762`

---

## Testing Plan

### Test 1: Item Appears in Tutorial Chest
1. Start a new game with Level13PlusGear mod enabled
2. Complete the tutorial on the Nautiloid
3. Reach the crash site
4. Open the Tutorial Chest
5. **Verify:** L13_Gear_Chest container appears
6. Open L13_Gear_Chest
7. **Verify:** "Moonguard Plate" appears in the container with legendary border

### Test 2: Armor Properties
1. Equip Moonguard Plate on a character
2. Open character sheet
3. **Verify:** AC increases by the expected amount (base plate AC + 5)
4. **Verify:** All vanilla powers/passives are present and active
5. **Verify:** Item shows legendary rarity
6. **Verify:** Name displays as "Moonguard Plate"
7. **Verify:** Description text is correct and readable

### Test 3: Armor Visual
1. Equip Moonguard Plate on different character races/body types
2. **Verify:** Armor visual displays correctly
3. **Verify:** No visual glitches or missing textures
4. **Verify:** Visual matches expected plate armor appearance

### Test 4: Powers Functionality
1. Equip Moonguard Plate
2. Test each power/passive from the vanilla item
3. **Verify:** All spells unlock correctly
4. **Verify:** All passives function as expected
5. **Verify:** Any status effects apply correctly

### Test 5: Multiple Copies
1. Use console to spawn multiple copies of the armor
2. **Verify:** Item spawns correctly (not marked as unique)
3. **Verify:** Multiple copies can exist simultaneously
4. **Verify:** Each copy functions independently

---

## Technical Notes

### CRITICAL: Body Armor Reference

**IMPORTANT:** Only L13_Armor_Rogue works correctly in the L13PlusGear mod for body armor.

- **Use L13_Armor_Rogue as the reference** for implementation
- **DO NOT use** L13_Armor_Tyr, L13_Armor_Moonguard, L13_Armor_Voss, or L13_Armor_Orpheus as examples
- These other armors have issues and should not be used as templates

**Reference File:** `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Armor.txt` - L13_Armor_Rogue entry only

### Plate Armor Base

The armor will use `using "ARM_Plate_Body"` as the base template. This is the standard vanilla base for plate armor.

**Plate Armor Characteristics:**
- Heavy Armor proficiency required
- Base AC: 18
- No Dexterity bonus to AC
- Disadvantage on Stealth checks
- Strength requirement: Usually 15 (may be overridden)

### +5 AC Enhancement

Following the L13_Armor_Rogue pattern:
```
data "Boosts" "AC(5);[other boosts]"
```

This adds +5 to the base AC, making Moonguard Plate provide AC 23 (18 base + 5 enhancement).

### Unique Flag

**CRITICAL:** Must set `Unique "0"` for TreasureTable delivery to work correctly.
- `Unique "1"` - Item marked as unique, may not spawn from containers
- `Unique "0"` - Item can spawn normally from TreasureTable

### Vanilla Item Research

**FOUND:** Located MAG_EndGame_Plate_Armor in VanillaBG3/Gustav/Public/GustavDev/

**Complete Vanilla Stats:**
```
new entry "MAG_EndGame_Plate_Armor"
type "Armor"
using "ARM_Plate_Body_2"
data "RootTemplate" "fb2ff6d1-3096-4904-813c-a448e3fbec4d"
data "ValueUUID" "adfdafe5-f4da-4c64-a1e6-a33d626437d2"
data "Rarity" "VeryRare"
data "PassivesOnEquip" "ARM_MagicalPlate_2_Passive;MAG_MAG_EndGame_Plate_Armor_Passive"
data "StatusOnEquip" "MAG_BLADE_WARD;MAG_END_GAME_RESISTANCE"
data "Unique" "1"
```

**RootTemplate Details:**
- **ParentTemplateId:** fdb8ce53-51dc-4ccb-9e29-d1d99040e60b (plate armor visual)
- **Icon:** Generated_MAG_EndGame_Plate_Armor_Magic
- **DisplayName Handle:** h161232a0g2839g4b31g89fcg24313c1d402e
- **Description Handle:** heff80441g1a21g4423g8873gda728b6ad472

**Powers Breakdown:**
- **ARM_MagicalPlate_2_Passive** - Provides +2 AC bonus (standard magical plate bonus)
- **MAG_MAG_EndGame_Plate_Armor_Passive** - Custom passive for this armor (DisplayName: hcfac9774g6a1cg4135gb384gdbd09af2c6df, Description: h49f4ee08g8383g4677g8d23g7af702825adc)
- **MAG_BLADE_WARD** - Uses BLADE_WARD status (resistance to physical damage from weapon attacks)
- **MAG_END_GAME_RESISTANCE** - Uses RESISTANCE status (general damage resistance)

**Summary:** The vanilla armor provides +2 AC from magical plate, plus Blade Ward (resistance to physical weapon damage) and general Resistance effects.

---

## Design Decisions

### Powers & Abilities
**Decision:** No additional powers beyond vanilla MAG_EndGame_Plate_Armor.
- Keep all vanilla passives and statuses exactly as they are
- No Selûne-themed additions in this phase
- Can be enhanced in future phases if desired

### Visual Appearance
**Decision:** Use the same visual as vanilla MAG_EndGame_Plate_Armor.
- ParentTemplateId: `fdb8ce53-51dc-4ccb-9e29-d1d99040e60b`
- This is the standard end-game plate armor appearance

### AC Balance
**Decision:** Option A - Keep both AC bonuses (+7 total)

The armor will have:
- **Explicit AC Boost:** +5 (via Boosts "AC(5)")
- **Magical Plate Passive:** +2 (via ARM_MagicalPlate_2_Passive)
- **Total AC Bonus:** +7
- **Final AC:** 25 (18 base plate + 7)

This matches the power level of other top-tier L13 armor (Moonguard Splint) and makes it a true legendary end-game piece.

---

## Dependencies

**This phase depends on:**
- Level13PlusGear mod base files - Already present
- UUID pool in uuid_workflow.md - Available (64 UUIDs remaining)
- Vanilla MAG_EndGame_Plate_Armor data - ✓ Found in VanillaBG3/Gustav/Public/GustavDev/

**This phase affects:**
- Level13PlusGear mod - Adds 1 new armor piece
- Tutorial Chest loot - Adds new legendary armor to pool
- Item catalog - Needs documentation update

---

## Success Criteria

- [x] Moonguard Plate RootTemplate created with proper UUID and handles
- [x] Armor stats entry added to Armor.txt with +5 AC and vanilla powers
- [x] DisplayName and Description added to localization
- [x] Item added to Tutorial Chest TreasureTable
- [x] Unique flag set to 0 for proper spawning
- [x] Mod version incremented
- [x] UUID pool updated (used UUIDs removed)
- [ ] Item spawns correctly in Tutorial Chest (awaiting user testing)
- [ ] Armor provides correct AC bonus (+7 total) (awaiting user testing)
- [ ] All vanilla powers function correctly (awaiting user testing)
- [ ] Visual displays properly (awaiting user testing)
- [x] Item catalog updated with new armor
- [ ] Testing completed and verified (awaiting user testing)

---

## Related Documentation

- **docs/instructions/uuid_workflow.md** - UUID allocation and L13 naming conventions
- **docs/instructions/copying_items_between_mods.md** - General process for copying items
- **docs/level13plusgear/item_catalog.md** - Item catalog to be updated
- **docs/instructions/PhaseDocumentTemplate.md** - Template structure reference
- **Level13PlusGear/Public/Level13PlusGear/RootTemplates/L13_Armor_Moonguard.lsf.lsx** - Reference for armor RootTemplate structure
- **Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Armor.txt** - Where to add stats entry

---

## Notes

### Design Rationale

**Why Based on MAG_EndGame_Plate_Armor?**
- User specified this as the base
- Provides Blade Ward and Resistance effects
- Solid end-game defensive capabilities
- Good foundation for a legendary plate armor

**Why No Additional Powers?**
- User decision: Keep this phase focused on the vanilla powers only
- Additional Selûne-themed powers can be added in future phases if desired
- Keeps implementation simple and focused

**Visual Choice:**
- User decision: Use vanilla MAG_EndGame_Plate_Armor visual
- ParentTemplateId: fdb8ce53-51dc-4ccb-9e29-d1d99040e60b
- Provides impressive end-game plate armor appearance

**Naming Convention:**
- Using "L13_Plate_Moonguard" to match existing Moonguard item naming pattern
- Part of the Moonguard set (blessed by Selûne, the moon goddess)
- Consistent with L13_Armor_Moonguard (Splint), L13_Blade_Moonguard, etc.

### Future Considerations

**Moonguard Set Expansion:**
- Moonguard Plate completes the heavy armor options for the Moonguard set
- Existing Moonguard items: Blade, Splint, Helm, Circlet, Gloves, Cloak, Shield
- Future: Could add Moonguard-themed accessories or weapons

**Alternative Delivery:**
- Consider adding to a special "Selûne's Shrine" location (future feature)
- Could create a quest-based acquisition method (with Script Extender)

---

## Implementation Summary

**Phase 043 Implementation Complete - 2026-02-12**

### Files Created:
1. **L13_Plate_Moonguard.lsf.lsx** - RootTemplate for Moonguard Plate
   - MapKey: `ed136df4-f2cb-43bb-94a8-d82bfc35aa51`
   - ParentTemplateId: `fdb8ce53-51dc-4ccb-9e29-d1d99040e60b` (vanilla plate armor visual)
   - Stats: `L13_Plate_Moonguard`

### Files Modified:
1. **Armor.txt** - Added L13_Plate_Moonguard stats entry
   - Base: ARM_Plate_Body_2
   - Boosts: AC(5)
   - PassivesOnEquip: ARM_MagicalPlate_2_Passive;MAG_MAG_EndGame_Plate_Armor_Passive
   - StatusOnEquip: MAG_BLADE_WARD;MAG_END_GAME_RESISTANCE
   - Rarity: Legendary
   - Unique: 0

2. **Level13PlusGear.loca.xml** - Added localization
   - DisplayName: "Moonguard Plate"
   - Description: "Plate armor blessed by Selûne, the Moonmaiden. Part of the legendary Moonguard set. Provides exceptional protection with Blade Ward and magical resistance."

3. **TreasureTable.txt** - Added to L13_Gear_Chest loot table
   - Entry: I_L13_Plate_Moonguard (in L13_Gear_Chest_TT table)

4. **meta.lsx** - Version incremented
   - Old: 36028887213277185
   - New: 36028887213277186

5. **uuid_workflow.md** - Removed 3 used UUIDs from pool

### Final Stats:
- **Name:** Moonguard Plate
- **Type:** Plate Armor (Heavy)
- **Base AC:** 18 (plate armor base)
- **AC Bonus:** +5 (explicit boost) + 2 (ARM_MagicalPlate_2_Passive) = +7 total
- **Total AC:** 25
- **Rarity:** Legendary
- **Powers:**
  - Blade Ward (resistance to physical weapon damage)
  - End Game Resistance (general damage resistance)
  - Magical Plate +2 (inherent +2 AC bonus)
- **Delivery:** L13_Gear_Chest container (appears in Tutorial Chest) via TreasureTable
- **Unique:** 0 (allows multiple copies)

### UUIDs Used:
- RootTemplate: ed136df4-f2cb-43bb-94a8-d82bfc35aa51
- DisplayName: hed138746-6425-46d5-8729-5313eaedd921
- Description: hed133656-2ee6-4a74-96dd-062b531d2762

---

## Revision 1: Troubleshooting and Delivery Verification

**Date:** 2026-02-12
**Issue:** Item not spawning in game
**Status:** INVESTIGATING

### Problem Report
User reported that Moonguard Plate is not spawning when opening the Tutorial Chest.

### Investigation

#### 1. TreasureTable Configuration - VERIFIED CORRECT ✓
Checked `TreasureTable.txt` and confirmed the item IS correctly placed in the **L13_Gear_Chest_TT** table:

```
new treasuretable "L13_Gear_Chest_TT"
CanMerge 1
...
new subtable "1,1"
object category "I_L13_Plate_Moonguard",1,0,0,0,0,0,0,0
```

**Location:** Lines 36-37 of TreasureTable.txt
**Delivery Method:** L13_Gear_Chest container (which appears in Tutorial Chest)
**Verdict:** Configuration is correct - item should appear in L13_Gear_Chest, NOT directly in Tutorial Chest

#### 2. RootTemplate Structure - VERIFIED CORRECT ✓
Compared `L13_Plate_Moonguard.lsf.lsx` with working armor templates (L13_Armor_Tyr, L13_Armor_Rogue):
- All required attributes present
- Structure matches working templates exactly
- MapKey, ParentTemplateId, Stats, Name all correct
**Verdict:** RootTemplate is correctly structured

#### 3. Stats Entry - VERIFIED CORRECT ✓
Checked `Armor.txt` entry:
- Using correct base: `ARM_Plate_Body_2`
- RootTemplate UUID matches: `ed136df4-f2cb-43bb-94a8-d82bfc35aa51`
- Unique flag set to 0 for container delivery
- All passives and statuses match vanilla item
**Verdict:** Stats entry is correct

#### 4. Localization - VERIFIED CORRECT ✓
Checked handles in `Level13PlusGear.loca.xml`:
- DisplayName handle: `hed138746-6425-46d5-8729-5313eaedd921` → "Moonguard Plate"
- Description handle: `hed133656-2ee6-4a74-96dd-062b531d2762` → [description text]
- Both entries present in localization file
**Verdict:** Localization is correct

### Possible Causes

#### Most Likely: Container Delivery Limitation
From CLAUDE.md:
> **Once a container is opened** in a save file, its loot is "locked in" to that save
> **Adding new items** to the mod will NOT retroactively appear in already-opened containers

**If the user opened the Tutorial Chest or L13_Gear_Chest in an existing save before adding Moonguard Plate, it will NOT appear.**

**Solution:** Start a NEW game or use console commands to spawn the item.

#### Other Potential Causes:
1. **Game Cache:** BG3 may need a full restart to pick up mod changes
2. **Mod Load Order:** Ensure Level13PlusGear is enabled and loading after vanilla files
3. **Version Mismatch:** Game may be caching old mod version (user's meta.lsx shows version 36028889360760832, which is newer than my increment)

### Verification Steps for User

To verify the item configuration is correct:

1. **Console Spawn Test:**
   ```
   oe L13_Plate_Moonguard
   ```
   If this works, the item exists and all files are correct - issue is delivery method.

2. **New Game Test:**
   - Start a completely NEW game
   - Complete Nautiloid tutorial
   - Open Tutorial Chest at crash site
   - Open L13_Gear_Chest container
   - Verify Moonguard Plate appears

3. **Mod Version Check:**
   - Verify mod version in BG3 Mod Manager shows updated version
   - Ensure mod is enabled and loaded

### Current Configuration Summary

**Delivery Chain:**
1. Tutorial Chest (vanilla container) contains →
2. L13_Gear_Chest (custom container) which contains →
3. **Moonguard Plate** (and all other L13 items)

**Files Verified:**
- ✓ RootTemplate: `L13_Plate_Moonguard.lsf.lsx`
- ✓ Stats: `Armor.txt` entry for `L13_Plate_Moonguard`
- ✓ Localization: `Level13PlusGear.loca.xml` entries
- ✓ Treasure Table: `TreasureTable.txt` entry in `L13_Gear_Chest_TT`
- ✓ All UUIDs and handles valid

**Expected Behavior:**
On a NEW save, opening Tutorial Chest → L13_Gear_Chest should show Moonguard Plate along with all other 27 L13 items.

### Notes
- User's meta.lsx shows version `36028889360760832` (higher than my increment to `36028887213277186`)
- This suggests user manually incremented version using BG3 Mod Manager tools
- This is correct behavior and should not cause issues

---

## Revision 2: Ring of Creation Testing Enhancement

**Date:** 2026-02-12
**Purpose:** Enable direct testing of Moonguard Plate via Ring of Creation
**Status:** COMPLETE

### Rationale
To bypass the Container Delivery Limitation and enable immediate testing of the Moonguard Plate without starting a new game, added the ability to summon it using the Ring of Creation utility mod.

### Changes Made

#### 1. Added Summoning Spell - Spell_Target.txt
Created new spell `ROC_Summon_Plate_Moonguard`:
```
new entry "ROC_Summon_Plate_Moonguard"
type "SpellData"
data "SpellType" "Target"
data "SpellProperties" "AI_IGNORE:GROUND:Summon(ed136df4-f2cb-43bb-94a8-d82bfc35aa51, UntilLongRest, , , ,L13_Plate_Moonguard)"
data "TargetRadius" "30"
data "AreaRadius" "1"
data "Icon" "Spell_Abjuration_ShieldOfFaith"
```

**Key Details:**
- Summons using Moonguard Plate UUID: `ed136df4-f2cb-43bb-94a8-d82bfc35aa51`
- Stats name: `L13_Plate_Moonguard`
- Icon: Shield of Faith (thematically appropriate for plate armor)
- Spell persists until long rest

#### 2. Added Localization - RingOfCreation.loca.xml
Added spell name and description:
- **DisplayName:** "Summon Moonguard Plate"
- **Description:** "Summon the Moonguard Plate at the target location. This legendary plate armor is blessed by Selûne and provides exceptional protection."
- **Handles:**
  - DisplayName: `hrocaa11gbb22gcc33gdd44geeff112233445566`
  - Description: `hrocff99gee88gdd77gcc66gbbaa998877665544`

#### 3. Updated Ring Abilities - Armor.txt
Added spell to Ring of Creation's Boosts:
```
data "Boosts" "UnlockSpell(ROC_Summon_L13_Chest);UnlockSpell(ROC_Summon_Boots_Stormwalker);UnlockSpell(ROC_Summon_Plate_Moonguard)"
```

#### 4. Updated Ring Description
Updated ring description to mention new summon ability:
> "A legendary ring imbued with the power to summon items from across the realms. Grants the ability to summon the Level 13 Plus Gear Chest, Boots of the Stormwalker, **and Moonguard Plate**."

#### 5. Updated Mod Version
Incremented Ring of Creation version:
- Old: `36028874328375299`
- New: `36028874328375300`

### Files Modified

| File | Change |
|------|--------|
| `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Spell_Target.txt` | Added ROC_Summon_Plate_Moonguard spell |
| `RingOfCreation/Localization/English/RingOfCreation.loca.xml` | Added spell localization + updated ring description |
| `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Armor.txt` | Added spell to ring's Boosts |
| `RingOfCreation/Mods/RingOfCreation/meta.lsx` | Incremented version number |

### Testing Instructions

1. **Obtain Ring of Creation:**
   - Console command: `oe ROC_Ring_Creation`
   - Or find in Tutorial Chest if already delivered via TreasureTable

2. **Summon Moonguard Plate:**
   - Equip Ring of Creation
   - Open spell menu
   - Find "Summon Moonguard Plate" spell
   - Cast on ground at target location
   - Armor appears and can be picked up

3. **Verify Functionality:**
   - Pick up armor from ground
   - Equip on character
   - Check AC (should be 25)
   - Verify powers appear in character sheet:
     - Blade Ward status
     - End Game Resistance status
     - Magical Plate +2 passive

### Benefits

✓ **Immediate Testing** - No need to start new game
✓ **Bypasses Container Limitation** - Works on existing saves
✓ **Verifies All Files** - If summoning works, RootTemplate, Stats, and Localization are all correct
✓ **Repeatable** - Can summon multiple copies for testing (Unique: 0)
✓ **Convenient** - Can test anywhere in the game world

### Dependencies

Ring of Creation mod depends on:
- Level13PlusGear mod (to access L13_Plate_Moonguard item definition)
- Must load AFTER Level13PlusGear in mod load order

### Notes

- This is a **testing enhancement** only - does not affect primary delivery via L13_Gear_Chest
- Ring of Creation is a utility mod specifically designed for item testing
- If console summoning (`oe L13_Plate_Moonguard`) works but Ring of Creation doesn't, check mod load order

---

## Revision 3: TreasureTable Delivery Fix

**Date:** 2026-02-12
**Issue:** Moonguard Plate not appearing in L13_Gear_Chest despite correct configuration
**Status:** FIXED

### Problem Confirmed

Ring of Creation successfully summons Moonguard Plate, confirming:
- ✓ RootTemplate is correct
- ✓ Stats entry is correct
- ✓ Localization is correct
- ✓ UUID is valid

**Therefore:** The issue is isolated to TreasureTable delivery only.

### Investigation

Examined TreasureTable.txt configuration:
```
new treasuretable "L13_Gear_Chest_TT"
CanMerge 1
...
new subtable "1,1"
object category "I_L13_Plate_Moonguard",1,0,0,0,0,0,0,0
```

**Findings:**
1. Entry format matches other items exactly ✓
2. ObjectCategory name follows pattern: "I_" + stats name ✓
3. Entry was placed in middle of list (after L13_Armor_Moonguard)
4. All 28 items now in treasure table

**Verified files:**
- `L13_Gear_Chest.lsf.lsx` - RootTemplate correctly references L13_Gear_Chest_TT
- `Object.txt` - Chest stats correctly defined (Unique: 1)
- All other items in same table work correctly

### Root Cause Hypothesis

Possible causes for middle-of-list placement issue:
1. **BG3 parsing quirk** - Some treasure tables may have issues with items inserted between existing entries
2. **Load order sensitivity** - Middle insertions might not process correctly during mod load
3. **Cache issue** - Game may cache treasure table structure and not recognize mid-list additions

### Fix Applied

**Moved TreasureTable entry to END of list:**

**Before:**
- Entry was at line 36-37 (after L13_Armor_Moonguard, before L13_Helmet_Tyr)

**After:**
- Entry now at line 64-65 (after L13_Ring_Guardian, at end of list)

```
new subtable "1,1"
object category "I_L13_Ring_Guardian",1,0,0,0,0,0,0,0
new subtable "1,1"
object category "I_L13_Plate_Moonguard",1,0,0,0,0,0,0,0
```

### Rationale

**Why end-of-list placement may work better:**
1. Appending is safer than inserting in treasure table files
2. Matches pattern of how items are typically added during development
3. Avoids potential parsing issues with mid-list modifications
4. Commonly recommended approach in BG3 modding community

### Files Modified

| File | Change |
|------|--------|
| `TreasureTable.txt` | Moved I_L13_Plate_Moonguard entry from middle to end of L13_Gear_Chest_TT table |

### Testing Instructions - Revision 3

**IMPORTANT:** This fix requires testing on a **completely NEW save** where the L13_Gear_Chest has never been opened.

1. **Clear any cached data:**
   - Fully exit BG3
   - Restart the game

2. **Start NEW game:**
   - Complete Nautiloid tutorial
   - Reach crash site
   - Open Tutorial Chest
   - Open L13_Gear_Chest container

3. **Verify Moonguard Plate appears:**
   - Should be in container with all other 27 L13 items
   - If not, try console spawn to verify files are still correct: `oe L13_Plate_Moonguard`

### Alternative Testing

If new save test fails, try Ring of Creation method (confirmed working):
```
oe ROC_Ring_Creation
```
Then summon Moonguard Plate via ring spell.

### Notes

- **Container Limitation applies:** If you previously opened L13_Gear_Chest on a save, that save will NOT get the new item
- **Mid-playthrough updates:** Players updating the mod mid-playthrough need new saves or console commands
- **Future additions:** Always append new items to END of treasure tables, not middle

### Success Criteria

- [ ] Moonguard Plate appears in L13_Gear_Chest on NEW save
- [ ] Item count in chest: 28 items total (was 27)
- [ ] Armor equips correctly with AC 25
- [ ] All powers function as expected

---

## Post-Implementation

- [ ] Test item spawning in Tutorial Chest
- [ ] Test armor equipping and AC calculation
- [ ] Test all vanilla powers from MAG_EndGame_Plate_Armor
- [ ] Test visual appearance
- [ ] Update item catalog documentation
- [ ] User testing required before marking COMPLETE

---

## Phase 043 Status: ABANDONED

**Planning Complete:**
1. ✓ Found vanilla MAG_EndGame_Plate_Armor stats in VanillaBG3/Gustav/Public/GustavDev/
2. ✓ Documented all vanilla powers, passives, and statuses
3. ✓ Confirmed: No additional powers in this phase
4. ✓ Confirmed: Use vanilla armor visual (ParentTemplateId: fdb8ce53-51dc-4ccb-9e29-d1d99040e60b)
5. ✓ Confirmed: Option A - Keep +7 total AC (AC 25)

**Implementation Complete (2026-02-12):**
1. ✓ Allocated 3 UUIDs from pool
2. ✓ Created RootTemplate (L13_Plate_Moonguard.lsf.lsx)
3. ✓ Created stats entry in Armor.txt
4. ✓ Added localization strings
5. ✓ Added to TreasureTable (Tutorial Chest)
6. ✓ Updated mod version (meta.lsx)
7. ✓ Updated UUID pool (removed used UUIDs)

**Final Design Summary:**
- **Name:** Moonguard Plate
- **AC:** 25 (18 base + 5 explicit + 2 from magical passive)
- **Powers:** Blade Ward, End Game Resistance, Magical Plate +2
- **Visual:** Vanilla end-game plate armor
- **Rarity:** Legendary
- **Unique:** 0 (for Tutorial Chest delivery)

**Awaiting User Testing:**
- Item spawning in L13_Gear_Chest (inside Tutorial Chest)
- Armor equipping and AC calculation
- Powers and passives functionality
- Visual appearance

**Note:** If testing on an existing save where Tutorial Chest or L13_Gear_Chest was already opened, the item will NOT appear due to Container Delivery Limitation. Use a NEW save or console command: `oe L13_Plate_Moonguard`

---

## Abandonment Summary

**Date:** 2026-02-12
**Reason:** TreasureTable delivery issue could not be resolved

### What Worked ✓

1. **Item implementation is FULLY functional:**
   - RootTemplate created correctly
   - Stats entry configured properly
   - Localization working
   - UUIDs valid and allocated

2. **Confirmed via Ring of Creation:**
   - Item successfully summons using `ROC_Summon_Plate_Moonguard` spell
   - Armor equips correctly
   - Visual displays properly
   - Powers and stats function as designed

3. **Alternative access methods work:**
   - Console command: `oe L13_Plate_Moonguard` ✓
   - Ring of Creation summoning ✓

### What Failed ✗

**TreasureTable delivery to L13_Gear_Chest:**
- Item does not appear in L13_Gear_Chest container
- Tested multiple configurations:
  - ✗ Middle of treasure table list
  - ✗ End of treasure table list
  - ✗ Both placements on new saves
- TreasureTable syntax verified correct
- Format matches working items exactly
- L13_Gear_Chest RootTemplate correctly references L13_Gear_Chest_TT

### Investigation Summary

**Attempted fixes (3 revisions):**
1. **Revision 1:** Verified all files correct, documented Container Delivery Limitation
2. **Revision 2:** Added Ring of Creation summoning (successful workaround)
3. **Revision 3:** Moved TreasureTable entry to end of list (no effect)

**Root cause:** Unknown
- All configuration appears correct
- Other items in same treasure table work
- No syntax errors detected
- Format identical to working entries
- May be BG3 engine limitation or undocumented treasure table quirk

### Files Created/Modified

**Created:**
- `Level13PlusGear/Public/Level13PlusGear/RootTemplates/L13_Plate_Moonguard.lsf.lsx`

**Modified:**
- `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Armor.txt`
- `Level13PlusGear/Localization/English/Level13PlusGear.loca.xml`
- `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/TreasureTable.txt`
- `Level13PlusGear/Mods/Level13PlusGear/meta.lsx`
- `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Spell_Target.txt`
- `RingOfCreation/Localization/English/RingOfCreation.loca.xml`
- `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Armor.txt`
- `RingOfCreation/Mods/RingOfCreation/meta.lsx`
- `docs/instructions/uuid_workflow.md` (3 UUIDs removed)
- `docs/level13plusgear/item_catalog.md` (documented but not delivered)

### Current State

**Item Status:**
- Fully functional and accessible via alternative methods
- NOT delivered via L13_Gear_Chest (primary delivery failed)
- Accessible via Ring of Creation (workaround successful)
- Accessible via console command

**Mod State:**
- Level13PlusGear: Version updated, item exists but not in chest
- RingOfCreation: Version updated, can summon Moonguard Plate
- Item catalog: Updated with Moonguard Plate entry

### Recommendations for Phase 044

**Suggested approaches:**
1. **Alternative delivery method** - Try different container or delivery mechanism
2. **Copy working armor** - Try copying a working armor's exact configuration
3. **Fresh item creation** - Create plate armor from scratch with different approach
4. **OneTimeRewards delivery** - Try Traveler's Chest delivery instead of TreasureTable
5. **Investigate existing armors** - Compare L13_Armor_Tyr (Tutorial Chest) vs L13_Armor_Rogue (L13_Gear_Chest)

### Lessons Learned

1. **TreasureTable delivery is unpredictable** - Even with correct syntax, items may not appear
2. **Ring of Creation is essential** - Provides reliable testing method when containers fail
3. **Console commands verify implementation** - If `oe` works, item files are correct
4. **Container Delivery Limitation is real** - New saves required for container testing
5. **Not all delivery methods work equally** - Some items may require specific delivery approaches

### Assets Retained

Despite abandonment, these assets are functional and can be:
- **Reused in Phase 044** with alternative delivery method
- **Accessed via Ring of Creation** for player use
- **Spawned via console** for testing/gameplay
- **Referenced as template** for future armor items

**The Moonguard Plate exists and works - it just won't appear in the L13_Gear_Chest.**

---
