# Phase 043: Create Moonguard Plate

**Note:** This armor is part of the Moonguard set, joining other Moonguard items (Blade, Splint, Helm, Circlet, Gloves, Cloak, Shield).

**Status:** PENDING
**Date:** 2026-02-11

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
- Added to Tutorial Chest via TreasureTable
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
- Use L13_Armor_Moonguard.lsf.lsx as structural reference
- ParentTemplateId from vanilla MAG_EndGame_Plate_Armor: fdb8ce53-51dc-4ccb-9e29-d1d99040e60b

### Task 4: Create Armor Stats Entry

**Description:** Add the armor stats entry to Armor.txt.

**Steps:**
1. Open: `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Armor.txt`
2. Add new entry "L13_Plate_Moonguard"
3. Set `using "ARM_Plate_Body"` (or appropriate plate base)
4. Add RootTemplate UUID
5. Set `Rarity "Legendary"`
6. Add `Boosts "AC(5)"` for +5 armor
7. Copy all Boosts from vanilla MAG_EndGame_Plate_Armor
8. Copy all PassivesOnEquip from vanilla item
9. Copy any StatusOnEquip from vanilla item
10. Set `Unique "0"` for TreasureTable delivery

**Implementation (based on vanilla MAG_EndGame_Plate_Armor + L13 enhancements):**
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

**Description:** Add Moonguard Plate to the Tutorial Chest loot table.

**Steps:**
1. Open: `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/TreasureTable.txt`
2. Locate the "L13_Tutorial_Chest" treasure table
3. Add new entry: `new treasuretable "L13_Plate_Moonguard"`
4. Configure with appropriate probability (follow existing pattern)

**Example:**
```
new treasuretable "L13_Plate_Moonguard"
CanMerge 1
new subtable "1,1"
object category "I_L13_Plate_Moonguard",1,0,0,0,0,0,0,0
```

Then add to main chest table:
```
new treasuretable "L13_Tutorial_Chest"
...
object category "L13_Plate_Moonguard",1,0,0,0,0,0,0,0
```

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

**[To be filled in during implementation]**

**L13_Plate_Moonguard:**
- **RootTemplate UUID:** `ed13xxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`
- **DisplayName Handle:** `hed13xxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`
- **Description Handle:** `hed13xxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`

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

- [ ] Moonguard Plate RootTemplate created with proper UUID and handles
- [ ] Armor stats entry added to Armor.txt with +5 AC and vanilla powers
- [ ] DisplayName and Description added to localization
- [ ] Item added to Tutorial Chest TreasureTable
- [ ] Unique flag set to 0 for proper spawning
- [ ] Mod version incremented
- [ ] UUID pool updated (used UUIDs removed)
- [ ] Item spawns correctly in Tutorial Chest
- [ ] Armor provides correct AC bonus (+5)
- [ ] All vanilla powers function correctly
- [ ] Visual displays properly
- [ ] Item catalog updated with new armor
- [ ] Testing completed and verified

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

**[To be filled in after implementation]**

---

## Post-Implementation

- [ ] Test item spawning in Tutorial Chest
- [ ] Test armor equipping and AC calculation
- [ ] Test all vanilla powers from MAG_EndGame_Plate_Armor
- [ ] Test visual appearance
- [ ] Update item catalog documentation
- [ ] User testing required before marking COMPLETE

---

## Phase 043 Status: PENDING

**Planning Complete:**
1. ✓ Found vanilla MAG_EndGame_Plate_Armor stats in VanillaBG3/Gustav/Public/GustavDev/
2. ✓ Documented all vanilla powers, passives, and statuses
3. ✓ Confirmed: No additional powers in this phase
4. ✓ Confirmed: Use vanilla armor visual (ParentTemplateId: fdb8ce53-51dc-4ccb-9e29-d1d99040e60b)
5. ✓ Confirmed: Option A - Keep +7 total AC (AC 25)

**Final Design Summary:**
- **Name:** Moonguard Plate
- **AC:** 25 (18 base + 5 explicit + 2 from magical passive)
- **Powers:** Blade Ward, End Game Resistance, Magical Plate +2
- **Visual:** Vanilla end-game plate armor
- **Rarity:** Legendary
- **Unique:** 0 (for Tutorial Chest delivery)

**Ready for Implementation:**
1. Allocate 3 UUIDs from pool
2. Create RootTemplate, stats entry, localization
3. Add to TreasureTable
4. Test thoroughly
5. Update documentation

---
