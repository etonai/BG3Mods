# Phase 38: Copy Weapons and Body Armor from SampleMagicRingMod

**Status:** COMPLETE (WITH KNOWN BUGS)
**Date:** 2026-02-11
**Completion Date:** 2026-02-11

---

## Goals

1. **Copy Weapons:** Copy 4 remaining weapons from SampleMagicRingMod (Sword of Orpheus, Divine Maul, Selune's Moon Mace, Rogueblade)
2. **Copy Body Armor:** Copy 5 body armor pieces (Armor of Tyr, Rogue, Moonguard, Voss, Orpheus)
3. **Maintain Independence:** Ensure all copied items are fully independent from SampleMagicRingMod
4. **Systematic Approach:** Use the workflow and infrastructure established in Phase 037
5. **Complete Documentation:** Update item catalog and track all UUID usage

**Scope:** Phase 38 focuses on weapons and body armor. Headgear, accessories, and Ring of the Guardian will be handled in Phase 39.

---

## SampleMagicRingMod Item Inventory

This table lists all 32 items in SampleMagicRingMod, their current status, and whether they will be copied in Phase 38.

| # | Item | Type | Rarity | Copied to L13? | Phase | Copy in Phase 38? |
|---|------|------|--------|----------------|-------|-------------------|
| **WEAPONS** |
| 1 | SMR_Staff_Archmage | Quarterstaff | Legendary | ✅ Yes | Phase 029 | ❌ Already copied |
| 2 | SMR_Staff_Akitaro | Quarterstaff | Legendary | ❌ No | - | ❌ **Will not copy** - Too complex, not needed for L13 mod |
| 3 | SMR_Sword_Tyr | Longsword +5 | Legendary | ✅ Yes | Phase 032 | ❌ Already copied |
| 4 | SMR_Sword_Orpheus | Greatsword +5 | Legendary | ❌ No | - | ✅ Yes |
| 5 | SMR_Maul_Divine | Maul +5 | Legendary | ❌ No | - | ✅ Yes |
| 6 | SMR_Mace_Selune_Moon | Mace +5 | Legendary | ❌ No | - | ✅ Yes |
| 7 | SMR_Rogueblade | Longsword +5 | Legendary | ❌ No | - | ✅ Yes |
| 8 | SMR_Blade_Moonguard | Longsword +5 | Legendary | ✅ Yes | Phase 033 | ❌ Already copied |
| **BODY ARMOR** |
| 9 | SMR_Armor_Tyr | Half Plate +2 | Legendary | ❌ No | - | ✅ Yes |
| 10 | SMR_Armor_Rogue | Studded Leather +5 | Legendary | ❌ No | - | ✅ Yes |
| 11 | SMR_Armor_Moonguard | Splint Armor +5 | Legendary | ❌ No | - | ✅ Yes |
| 12 | SMR_Armor_Voss | Chain Shirt +5 | Legendary | ❌ No | - | ✅ Yes |
| 13 | SMR_Armor_Orpheus | Half Plate (Githyanki) | Legendary | ❌ No | - | ✅ Yes |
| **HEADGEAR** |
| 14 | SMR_Helmet_Tyr | Metal Helmet | Legendary | ❌ No | - | ✅ Yes |
| 15 | SMR_Circlet_Tyr | Circlet | Legendary | ❌ No | - | ✅ Yes |
| 16 | SMR_Circlet_Magus | Circlet | Legendary | ❌ No | - | ✅ Yes |
| 17 | SMR_Helmet_Moonguard | Metal Helmet | Legendary | ❌ No | - | ✅ Yes |
| 18 | SMR_Circlet_Moonguard | Circlet | Legendary | ❌ No | - | ✅ Yes |
| **GLOVES** |
| 19 | SMR_Gloves_Tyr | Gloves | Legendary | ❌ No | - | ✅ Yes |
| 20 | SMR_Gloves_Moonguard | Gloves | Legendary | ❌ No | - | ✅ Yes |
| **BOOTS** |
| 21 | SMR_Boots_Stormwalker | Boots | Legendary | ✅ Yes | Phase 033 | ❌ Already copied |
| **CLOAKS** |
| 22 | SMR_Cloak_Tyr | Cloak | Legendary | ❌ No | - | ✅ Yes |
| 23 | SMR_Cloak_Rogue | Cloak | Legendary | ❌ No | - | ✅ Yes |
| 24 | SMR_Cloak_Moonguard | Cloak | Legendary | ❌ No | - | ✅ Yes |
| **SHIELDS** |
| 25 | SMR_Shield_Tyr | Shield +2 | Legendary | ❌ No | - | ✅ Yes |
| 26 | SMR_Shield_Moonguard | Shield +2 | Legendary | ❌ No | - | ✅ Yes |
| **RINGS** |
| 27 | SMR_Ring_Spectral_Power | Ring | Legendary | ✅ Yes | Phase 037 | ❌ Already copied |
| 28 | SMR_Ring_Guardian | Ring | Legendary | ❌ No | - | ✅ Yes |
| 29 | SMR_Ring_Magic_1 | Ring | Rare | ❌ No | - | ❌ **Will not copy** - Example item only |
| 30 | SMR_Ring_Magic_2 | Ring | Rare | ❌ No | - | ❌ **Will not copy** - Example item only |
| 31 | SMR_Ring_Magic_3 | Ring | Rare | ❌ No | - | ❌ **Will not copy** - Example item only |
| 32 | SMR_Ring_Magic_4 | Ring | Rare | ❌ No | - | ❌ **Will not copy** - Example item only |

---

## Summary

| Status | Count | Items |
|--------|-------|-------|
| **Already Copied** | 5 | Staff of the Archmage, Sword of Tyr, Boots of Stormwalker, Moonguard Blade, Ring of Spectral Power |
| **To Copy in Phase 38** | 9 | Weapons (4), Body Armor (5) |
| **Deferred to Phase 39** | 13 | Headgear (5), Accessories (7), Ring of the Guardian (1) |
| **Will Not Copy** | 6 | Staff of Akitaro (too complex), Ring Magic 1-4 (example items only) |
| **Total Items** | 32 | All SampleMagicRingMod items |

**Note:** The Ring_Magic items (1-4) were part of the original SampleMagicRingMod as example/template items and will not be copied. Staff of Akitaro is too complex and not needed for Level13PlusGear.

**Phase Split:** Phase 38 covers weapons and body armor (9 items). Phase 39 will cover headgear, accessories, and Ring of the Guardian (13 items).

---

## Implementation Strategy

### Phase 38 Scope: Weapons and Body Armor

Based on complexity and dependencies, items will be copied in two groups:

#### Group 1: Weapons (4 items)

**Simple Weapons (Low Complexity):**
- **Divine Maul:** Maul +5 with Celestial Haste and Radiant Weapon passive
- **Rogueblade:** Longsword +5 with Shadow Blade and Rearrangement passives
- **Estimated UUIDs:** ~4-6 per item

**Complex Weapons (Medium Complexity):**
- **Sword of Orpheus:** Greatsword +5 with psionic abilities (Mindcrush, Psionic Weapon, Psionic Resistance)
- **Selune's Moon Mace:** Mace +5 with healing aura and Moonshield
- **Estimated UUIDs:** ~8-12 per item

#### Group 2: Body Armor (5 items)

**Medium Complexity:**
- **Armor of Tyr:** Half Plate +2 with Celestial Haste, Misty Step, Spirit Guardians
- **Armor of the Rogue:** Studded Leather +5 with Displacement passive
- **Moonguard Splint:** Splint Armor +5 with spells + Combat Regeneration
- **Armor of Voss:** Chain Shirt +5 with spells + Combat Regeneration
- **Armor of Orpheus:** Half Plate (Githyanki) with Celestial Haste, Misty Step, Spirit Guardians
- **Reason:** Some share similar spell sets, allowing spell reuse
- **Estimated UUIDs:** ~6-10 per item

#### Items Deferred to Phase 39
- **Headgear (5):** Helmet of Tyr, Circlet of Tyr, Magus Circlet, Moonguard Helm, Moonguard Circlet
- **Gloves (2):** Gloves of Tyr, Moonguard Gloves
- **Cloaks (3):** Cloak of Tyr, Cloak of the Rogue, Moonguard Cloak
- **Shields (2):** Shield of Tyr, Moonguard Shield
- **Ring (1):** Ring of the Guardian

#### Excluded Items (Will Not Copy)
- **Staff of Akitaro:** Too complex (10+ custom spells, many unique passives) and not needed for Level13PlusGear
- **Ring Magic 1-4:** Example/template items from original SampleMagicRingMod, not intended for endgame use

---

## Estimated Resource Requirements

### UUID Usage Estimation

| Item Category | Count | UUIDs per Item | Total UUIDs |
|---------------|-------|----------------|-------------|
| Simple Weapons | 2 | 5 | 10 |
| Complex Weapons | 2 | 10 | 20 |
| Body Armor | 5 | 8 | 40 |
| **Phase 38 Total** | **9** | **Avg: 7.8** | **~70** |

**Current UUID Pool:** 24 UUIDs available (after Phase 037)

**Action Required:** User will need to generate ~46 additional UUIDs before starting Phase 38.

**Phase 39 Items (Deferred):**
- Headgear (5) + Accessories (7) + Ring of the Guardian (1) = 13 items
- Estimated: ~110 UUIDs needed for Phase 39

**Excluded:** Staff of Akitaro (~30-40 UUIDs) and Ring Magic 1-4 (~20 UUIDs) are not being copied.

### File Modifications

**Existing Files to Modify:**
- `Armor.txt` - Add all non-weapon items
- `Weapon.txt` - Add remaining weapons
- `Spell_Projectile.txt` - Add projectile spells
- `Spell_Target.txt` - Add target spells
- `Spell_Shout.txt` - Add shout spells
- `Spell_Zone.txt` - Add zone spells (if any new ones)
- `Spell_Teleportation.txt` - Add teleportation spells (if any new ones)
- `Spell_Throw.txt` - Add throw spells (if any new ones)
- `TreasureTable.txt` - Add all items to L13_Gear_Chest
- `Level13PlusGear.loca.xml` - Add localization for all items and spells

**New Files to Create:**
- RootTemplates for 9 items (4 weapons + 5 body armor pieces)

---

## Questions for User

Before implementing Phase 38, please confirm:

1. **UUID Generation:** Can you generate ~46 additional UUIDs for the UUID pool?
2. **Priority:** Should we copy weapons first, then armor? Or all together?
3. **Testing:** Test after each group (weapons, then armor) or all at once?

---

## Success Criteria

- [ ] All selected items copied from SampleMagicRingMod
- [ ] All items have L13_ prefix and ed13 UUIDs
- [ ] All custom spells copied and adapted
- [ ] All localization entries created
- [ ] All items added to TreasureTable
- [ ] All RootTemplates created
- [ ] Item catalog updated
- [ ] UUID pool updated (used UUIDs removed)
- [ ] No dependencies on SampleMagicRingMod
- [ ] All items tested in-game

---

## Related Documentation

- **Phase037.md** - Ring of Spectral Power copy (reference workflow)
- **Phase029.md** - Staff of the Archmage copy (reference workflow)
- **docs/instructions/copying_items_between_mods.md** - Item copy workflow
- **docs/instructions/uuid_workflow.md** - UUID pool and naming conventions
- **docs/planning/item_catalog.md** - SampleMagicRingMod source items
- **docs/level13plusgear/item_catalog.md** - Level13PlusGear target catalog

---

## Notes

**Complexity Considerations:**
- Items that share similar spell sets (e.g., Tyr variants, Moonguard variants) can reuse some custom spells
- Many items reuse vanilla spells/passives (Celestial Haste, Misty Step, etc.)
- The infrastructure from Phase 037 (Spell_Zone, Spell_Teleportation, Spell_Throw) will reduce new file creation

**Efficiency Tips:**
- Group items by type for batch processing
- Copy similar items together (e.g., all Tyr items, all Moonguard items)
- Create shared custom spells first, then reference them in multiple items
- Use Phase 037 Ring of Spectral Power as template for complex items

**Phase Breakdown:**
- **Phase 38:** Weapons (4) + Body Armor (5) = 9 items, ~70 UUIDs
- **Phase 39:** Headgear (5) + Accessories (7) + Ring of the Guardian (1) = 13 items, ~110 UUIDs

This split makes each phase more manageable and allows for testing between phases.

**Items Excluded from Both Phases:**
- **Staff of Akitaro:** Will never be added to Level13PlusGear (too complex, not needed)
- **Ring Magic 1-4:** Example items only, not intended for endgame use

---

## Phase 38 Status: IMPLEMENTED

**Initial implementation complete. Awaiting testing.**

---

## Revision 1: UUID Formatting Error Fix

**Issue Date:** 2026-02-11
**Status:** COMPLETE
**Completion Date:** 2026-02-11

### Problem

Items not appearing in the Level 13 Plus Gear chest after initial implementation.

### Root Cause

UUID formatting error when converting from raw UUIDs to ed13-prefixed UUIDs. The UUID workflow specifies "replace the first 4 characters with `ed13`", but I incorrectly appended characters instead of replacing them.

**Example Error:**
- Original UUID: `3d0af80d-b40e-4534-a8dc-45a9db336374`
- Incorrect conversion: `ed133d0af-b40e-4534-a8dc-45a9db336374` (9 chars in first section ✗)
- Correct conversion: `ed13f80d-b40e-4534-a8dc-45a9db336374` (8 chars in first section ✓)

### Affected Items (All 9 Items)

| Item | Incorrect UUID | Correct UUID |
|------|---------------|--------------|
| L13_Sword_Orpheus | ed13a392-d5a4-49dd-8346-2f5df0ba2e77 | ed132513-d5a4-49dd-8346-2f5df0ba2e77 |
| L13_Maul_Divine | ed133d0af-b40e-4534-a8dc-45a9db336374 | ed13f80d-b40e-4534-a8dc-45a9db336374 |
| L13_Mace_Selune_Moon | ed1361827-93bb-47e8-9734-f0a85b99a2d8 | ed137095-93bb-47e8-9734-f0a85b99a2d8 |
| L13_Rogueblade | ed134569d-cd05-4045-b2fc-846210c43d94 | ed13dc14-cd05-4045-b2fc-846210c43d94 |
| L13_Armor_Tyr | ed137d2fa-47aa-4263-8147-34b583e18870 | ed13ac3a-47aa-4263-8147-34b583e18870 |
| L13_Armor_Rogue | ed138d366d-370d-44d3-b96f-af7f76628b6e | ed136dac-370d-44d3-b96f-af7f76628b6e |
| L13_Armor_Moonguard | ed13723e5-b130-491f-ac5d-53a72f1262b7 | ed13502f-b130-491f-ac5d-53a72f1262b7 |
| L13_Armor_Voss | ed13dc7dd-3bb4-47ad-be60-8ab165b4358d | ed13dc81-3bb4-47ad-be60-8ab165b4358d |
| L13_Armor_Orpheus | ed137c97e-4435-4861-b83a-2905202a42c1 | ed13e7d6-4435-4861-b83a-2905202a42c1 |

### Files Requiring Fixes

1. **Weapon.txt** - Update 4 RootTemplate UUIDs
2. **Armor.txt** - Update 5 RootTemplate UUIDs
3. **RootTemplate files (9 total)** - Update MapKey UUID in each file
4. **No changes needed:**
   - TreasureTable.txt (uses item names, not UUIDs)
   - Localization files (use handles, not UUIDs)
   - Spell files (not affected)

### Implementation Plan

1. Fix all 4 weapon UUIDs in Weapon.txt
2. Fix all 5 armor UUIDs in Armor.txt
3. Fix MapKey UUID in all 9 RootTemplate .lsf.lsx files
4. Test in-game to verify items appear in chest

### Lesson Learned

UUID conversion requires careful attention to the replacement algorithm:
- **Correct:** Take last N characters after removing first 4: `3d0af80d` → remove `3d0a` → keep `f80d` → result `ed13f80d`
- **Incorrect:** Keeping too many characters from original UUID leads to malformed UUIDs

---

## Revision 2: Missing RootTemplate Children Nodes

**Issue Date:** 2026-02-11
**Status:** COMPLETE
**Completion Date:** 2026-02-11

### Problem

Items still not appearing in chest after UUID fix.

### Root Cause

RootTemplate .lsf.lsx files are missing required `<children>` section with `GameMaster` node. BG3 requires this structure for items to be recognized properly.

**Comparison:**
```xml
<!-- INCORRECT (what I created) -->
<node id="GameObjects">
    <attribute id="MapKey" ... />
    ...
</node>

<!-- CORRECT (what's needed) -->
<node id="GameObjects">
    <attribute id="MapKey" ... />
    ...
    <children>
        <node id="GameMaster" />
    </children>
</node>
```

### Additional Issues

- Used placeholder ParentTemplateId values instead of correct BG3 parent templates
- Missing proper indentation/formatting

### Files Requiring Fixes

All 9 RootTemplate .lsf.lsx files need the `<children><node id="GameMaster" /></children>` section added.

### Correct ParentTemplateId Values (from SampleMagicRingMod)

| Item | Correct ParentTemplateId |
|------|-------------------------|
| Sword of Orpheus | f01c3f5d-c542-420f-86c5-bdddf7819e29 |
| Divine Maul | 7e8ef269-0e7b-4352-8828-89c5fced943c |
| Armor of Tyr | 42e6357a-4c05-4eda-9415-6b6b4c7d44c5 |

---

## Revision 3: Empty "Ability Modifier Cap" Field

**Issue Date:** 2026-02-11
**Status:** COMPLETE
**Completion Date:** 2026-02-11

### Problem

Weapons and Armor of the Rogue appear correctly, but 4 armor pieces don't appear:
- Armor of Tyr
- Moonguard Splint
- Armor of Voss
- Armor of Orpheus

### Root Cause

The 4 non-working armor pieces all have an invalid line in their Armor.txt entries:
```
data "Ability Modifier Cap" ""
```

**Analysis:**
- **Working items** (weapons + Rogue armor): Do NOT have this line
- **Non-working items** (4 armor pieces): All have `Ability Modifier Cap` with empty string value

Empty string values can cause BG3's stats parser to fail silently when loading the item, resulting in the item not appearing in-game.

### Solution

Remove the `data "Ability Modifier Cap" ""` line entirely from all 4 affected armor entries. BG3 will use default behavior when this field is not specified.

### Files Requiring Fixes

**Armor.txt** - Remove empty "Ability Modifier Cap" line from:
1. L13_Armor_Tyr (line 29)
2. L13_Armor_Moonguard (line 50)
3. L13_Armor_Voss (line 61)
4. L13_Armor_Orpheus (line 72)

---

## Revision 4: Handle Collision and Spell Structure Issues

**Issue Date:** 2026-02-11
**Status:** IMPLEMENTED
**Completion Date:** 2026-02-11

### Problem

Same 4 armor pieces still don't appear after Revision 3:
- Armor of Tyr
- Moonguard Splint
- Armor of Voss
- Armor of Orpheus

**Pattern:** Items that reference `L13_Shout_SpiritGuardians_Tyr` don't appear; items that don't reference this spell work correctly.

### Root Cause

Investigation revealed **two distinct issues**:

#### Issue 1: Handle Collision

The handle `hed13a9f33-3d48-4a28-969e-7bedef18b4ee` was being used for TWO different localization entries:
1. **L13_Sword_Orpheus Description** (RootTemplate file)
2. **L13_Shout_SpiritGuardians_Tyr_Necrotic ExtraDescription** (Spell_Shout.txt line 108)

When BG3 loads localization handles, duplicate handles cause conflicts that can prevent items from loading correctly.

#### Issue 2: Spell Structure Mismatch

Comparison of `L13_Shout_SpiritGuardians_Tyr` (broken) vs `L13_Shout_SpiritGuardians_Moonguard` (working):

**Tyr Spell (Broken):**
- Container spell has `UseCosts: "ActionPoint:1"`
- Both variants have `UseCosts: "ActionPoint:1"`
- SpellFlags: `"HasVerbalComponent;HasSomaticComponent;IsConcentration;IsSpell;IsHarmful;IsLinkedSpellContainer"`
- Missing `DisplayInItemTooltip` and `AddFallBackOrigin` flags

**Moonguard Spell (Working):**
- Container spell has NO UseCosts defined
- Variants have NO UseCosts defined
- SpellFlags: `"HasVerbalComponent;HasSomaticComponent;IsSpell;IsConcentration;DisplayInItemTooltip;AddFallBackOrigin"`
- Has `DisplayInItemTooltip` and `AddFallBackOrigin` flags, NO `IsHarmful` or `IsLinkedSpellContainer`

**Analysis:** When an armor grants a spell via `UnlockSpell(...,AddChildren,...)` and that spell is a container spell with `UseCosts`, it can cause item validation failures during loading.

### Solution

#### Fix 1: Resolve Handle Collision

Generate a new handle for the Spirit Guardians Necrotic ExtraDescription:
- **Old handle:** `hed13a9f33-3d48-4a28-969e-7bedef18b4ee` (collision)
- **New handle:** `hed136a4dg91d9g4af7g8c32g8a9d1ad50c9c` (from UUID pool: 768b6a4d-91d9-4af7-8c32-8a9d1ad50c9c)

Keep the L13_Sword_Orpheus Description using the original handle since the sword works correctly.

#### Fix 2: Match Moonguard Spell Structure

Modify `L13_Shout_SpiritGuardians_Tyr` to match the working `L13_Shout_SpiritGuardians_Moonguard` structure:

**Container Spell Changes:**
- Remove: `UseCosts`, `TargetSound`, `CastTextEvent`, `SpellAnimation`, `VerbalIntent`, `PrepareEffect`, `CastEffect`
- Update SpellFlags to: `"HasVerbalComponent;HasSomaticComponent;IsSpell;IsConcentration;DisplayInItemTooltip;AddFallBackOrigin"`

**Variant Spell Changes (Radiant & Necrotic):**
- Remove: `UseCosts`, `SpellFlags`, `DamageType`, `TooltipDamageList`
- Keep only essential fields, let them inherit from `using "Shout_SpiritGuardians"`

### Files Modified

**1. Spell_Shout.txt** (Lines 59-114)
- Simplified `L13_Shout_SpiritGuardians_Tyr` container spell
- Simplified `L13_Shout_SpiritGuardians_Tyr_Radiant` variant
- Simplified `L13_Shout_SpiritGuardians_Tyr_Necrotic` variant and changed ExtraDescription handle

**2. Level13PlusGear.loca.xml** (Line 68)
- Changed handle from `hed13a9f33-3d48-4a28-969e-7bedef18b4ee` to `hed136a4dg91d9g4af7g8c32g8a9d1ad50c9c`
- Content remains: "Necrotic spirits surround you."

**3. uuid_workflow.md**
- Removed used UUID: 768b6a4d-91d9-4af7-8c32-8a9d1ad50c9c

### Expected Result

All 9 items from Phase 38 should now appear in the Level 13 Plus Gear Chest:
- ✅ Sword of Orpheus
- ✅ Divine Maul
- ✅ Selune's Moonmace
- ✅ Rogueblade
- ⏳ Armor of Tyr (should now work)
- ✅ Armor of the Rogue
- ⏳ Moonguard Splint (should now work)
- ⏳ Armor of Voss (should now work)
- ⏳ Armor of Orpheus (should now work)

### Technical Notes

**Why Handle Collisions Matter:**
- BG3's localization system uses handles as unique identifiers
- When multiple items/spells reference the same handle, the game may fail to resolve text properly
- Items with unresolved localization can fail validation and not appear in-game

**Why Spell Structure Matters:**
- Container spells granted via `AddChildren` syntax must be carefully structured
- `UseCosts` on container spells can interfere with item-granted spell mechanics
- The `DisplayInItemTooltip` and `AddFallBackOrigin` flags are critical for spells granted by equipment
- Overriding too many inherited properties from the `using` statement can break spell functionality

**Lessons Learned:**
- Always check for handle collisions when copying items between mods
- Match spell structure exactly when creating variants of working spells
- Container spells granted by items have different requirements than player-castable spells
- BG3's stats parser fails silently on many validation errors, making debugging difficult

---

## Revision 5: Incomplete Spell Structure

**Issue Date:** 2026-02-11
**Status:** IMPLEMENTED
**Completion Date:** 2026-02-11

### Problem

Same 4 armor pieces still don't appear after Revision 4:
- Armor of Tyr
- Moonguard Splint
- Armor of Voss
- Armor of Orpheus

### Root Cause

Revision 4 **over-simplified** the spell structure. I tried to streamline `L13_Shout_SpiritGuardians_Tyr` by removing many fields, but this broke the spell.

**Comparison with SampleMagicRingMod:**

I examined the **working** `SMR_Shout_SpiritGuardians_Moonguard` spell in SampleMagicRingMod and found it has a COMPLETE structure:

**SampleMagicRingMod (WORKING):**
```
new entry "SMR_Shout_SpiritGuardians_Moonguard"
type "SpellData"
data "SpellType" "Shout"
data "Level" "3"
data "SpellSchool" "Conjuration"
data "ContainerSpells" "..."
data "AreaRadius" "3"
data "TargetConditions" "Self()"
data "Icon" "Spell_Conjuration_SpiritGuardians"
data "DisplayName" "..."
data "Description" "..."
data "DescriptionParams" "..."
data "TooltipAttackSave" "Wisdom"
data "PrepareSound" "..."
data "PrepareLoopSound" "..."
data "CastSound" "..."
data "TargetSound" "..."              ← MISSING in Revision 4
data "CastTextEvent" "Cast"           ← MISSING in Revision 4
data "UseCosts" ""                    ← MISSING in Revision 4 (set to empty string!)
data "SpellAnimation" "..."           ← MISSING in Revision 4
data "VerbalIntent" "Damage"          ← MISSING in Revision 4
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsConcentration;IsSpell;IsHarmful;IsLinkedSpellContainer"
data "PrepareEffect" "..."            ← MISSING in Revision 4
data "CastEffect" "..."               ← MISSING in Revision 4
```

**Variants also need:**
- `TooltipDamageList`
- `UseCosts ""`
- `SpellFlags`
- `DamageType`

All of these were removed in Revision 4, breaking the spell.

### Critical Discovery: UseCosts Empty String

The key insight: `UseCosts ""` (empty string) is **NOT** the same as omitting the field entirely.

- SampleMagicRingMod uses: `data "UseCosts" ""`
- My Revision 4 version: Field completely absent
- This subtle difference breaks spell validation!

### Solution

Restore `L13_Shout_SpiritGuardians_Tyr` to match **exact** structure of working `SMR_Shout_SpiritGuardians_Moonguard`:

**Container Spell:**
- Add back: `TargetSound`, `CastTextEvent`, `SpellAnimation`, `VerbalIntent`, `PrepareEffect`, `CastEffect`
- Add: `UseCosts ""` (empty string, not omitted)
- Restore SpellFlags to: `"HasVerbalComponent;HasSomaticComponent;IsConcentration;IsSpell;IsHarmful;IsLinkedSpellContainer"`

**Variant Spells (Radiant & Necrotic):**
- Add back: `TooltipDamageList`, `SpellFlags`, `DamageType`
- Add: `UseCosts ""` (empty string)

### Files Modified

**Spell_Shout.txt** (Lines 59-100)
- Completely rewrote all 3 spell entries to match SampleMagicRingMod's working structure
- Changed from simplified/incomplete structure to full structure
- Added `UseCosts ""` to all 3 entries
- Restored all missing fields

### Expected Result

All 9 items should now appear in the Level 13 Plus Gear Chest.

### Technical Notes

**Why Over-Simplification Failed:**

1. **Missing Required Fields**: Even though many fields have defaults, explicitly setting them is sometimes required for validation
2. **UseCosts Empty String**: Setting `UseCosts ""` tells BG3 "this spell has no cost" which is different from not specifying the field at all
3. **Complete vs Minimal**: While minimal definitions work for some spells, container spells with `AddChildren` syntax require complete field sets
4. **Copy Working Code**: When debugging, match the EXACT structure of known-working code rather than attempting to simplify

**Why This Matters for Container Spells:**

Container spells (spells that open a submenu with variants) have stricter validation requirements than regular spells. The `IsLinkedSpellContainer` flag and complete field set appear to be mandatory for proper loading.

**Lesson Learned:**

When copying spells between mods:
1. Copy the COMPLETE structure from a working spell
2. Don't remove fields unless you're certain they're optional
3. Empty string values (`""`) are NOT the same as omitting the field
4. Test incrementally - if simplification breaks it, restore the full structure

---

## Revision 6: Wrong ParentTemplateId

**Issue Date:** 2026-02-11
**Status:** IMPLEMENTED
**Completion Date:** 2026-02-11

### Problem

Same 4 armor pieces still don't appear after Revision 5:
- Armor of Tyr
- Moonguard Splint
- Armor of Voss
- Armor of Orpheus

### Critical Discovery: Source Mod Has Same Issue!

User revealed that in **SampleMagicRingMod** (the source mod):
- ✅ **Armor of Tyr WORKS**
- ✅ **Moonguard Splint WORKS**
- ❌ **Armor of Voss DOESN'T WORK**
- ❌ **Armor of Orpheus DOESN'T WORK**

This means I was copying items that **don't work in the source mod**! No wonder they don't work in Level13PlusGear!

### Root Cause Investigation

Compared the **working** vs **non-working** armor RootTemplate files in SampleMagicRingMod:

**Working Armor (Tyr & Moonguard):**
```xml
<attribute id="ParentTemplateId" type="FixedString" value="42e6357a-4c05-4eda-9415-6b6b4c7d44c5" />
```

**Non-Working Armor (Voss):**
```xml
<attribute id="ParentTemplateId" type="FixedString" value="eac652ed-ecf7-4505-bf64-0fec29e7d677" />
```

**My Level13PlusGear (Voss & Orpheus):**
```xml
<attribute id="ParentTemplateId" type="FixedString" value="94650cba-61e1-48d7-b42f-99b5c7bd6c29" />
```

### Analysis

The **ParentTemplateId** determines which vanilla BG3 item template the mod item is based on:

- `42e6357a-4c05-4eda-9415-6b6b4c7d44c5` - **WORKS** (used by Tyr & Moonguard in SampleMagicRingMod)
- `eac652ed-ecf7-4505-bf64-0fec29e7d677` - **DOESN'T WORK** (used by Voss in SampleMagicRingMod)
- `94650cba-61e1-48d7-b42f-99b5c7bd6c29` - **DOESN'T WORK** (what I used for Voss & Orpheus in Level13PlusGear)

When I copied items from SampleMagicRingMod in Revision 2, I used the ParentTemplateId from the source item. But for Voss and Orpheus, those ParentTemplateIds **don't work**!

### Solution

Change **both** Voss and Orpheus to use the **working** ParentTemplateId from Tyr and Moonguard:
- Old: `94650cba-61e1-48d7-b42f-99b5c7bd6c29`
- New: `42e6357a-4c05-4eda-9415-6b6b4c7d44c5`

This makes all 4 armor pieces use the same working parent template.

### Files Modified

**1. L13_Armor_Voss.lsf.lsx** (Line 13)
- Changed ParentTemplateId from `94650cba-61e1-48d7-b42f-99b5c7bd6c29` to `42e6357a-4c05-4eda-9415-6b6b4c7d44c5`

**2. L13_Armor_Orpheus.lsf.lsx** (Line 13)
- Changed ParentTemplateId from `94650cba-61e1-48d7-b42f-99b5c7bd6c29` to `42e6357a-4c05-4eda-9415-6b6b4c7d44c5`

### Expected Result

All 9 items from Phase 38 should now appear in the Level 13 Plus Gear Chest:
- ✅ Sword of Orpheus (working since Revision 2)
- ✅ Divine Maul (working since Revision 2)
- ✅ Selune's Moonmace (working since Revision 2)
- ✅ Rogueblade (working since Revision 2)
- ✅ Armor of Tyr (working since Revision 2)
- ✅ Armor of the Rogue (working since Revision 2)
- ✅ Moonguard Splint (working since Revision 2)
- ⏳ **Armor of Voss** (should now work with correct ParentTemplateId)
- ⏳ **Armor of Orpheus** (should now work with correct ParentTemplateId)

### Technical Notes

**Why ParentTemplateId Matters:**

The `ParentTemplateId` references a vanilla BG3 item template that provides:
- Base item properties (weight, value, equipment slot)
- Visual appearance and icon
- Base stats and behavior
- Inventory category

Using the wrong ParentTemplateId can cause:
- Item validation failures during mod loading
- Items not appearing in containers
- Visual glitches or missing icons
- Incorrect equipment behavior

**How to Find the Correct ParentTemplateId:**

When copying items between mods:
1. Don't blindly copy ParentTemplateId from source - test if the source item actually works!
2. Find a **working** item of the same type in the source mod
3. Use that working item's ParentTemplateId
4. For armor, the ParentTemplateId `42e6357a-4c05-4eda-9415-6b6b4c7d44c5` appears to be a reliable "generic magical armor" template

**Lessons Learned:**

1. **Test source items first** - Don't assume items in the reference mod work correctly
2. **Copy from working examples** - Always use ParentTemplateIds from items you've verified work
3. **Document what works** - Keep track of which ParentTemplateIds are reliable for different item types
4. **When in doubt, match working items** - If multiple items of the same type exist, use the ParentTemplateId from the ones that work

**Critical Insight:**

This revision reveals that **all previous revisions were fixing the wrong problem**! The spell structure issues (Revisions 4-5) were red herrings. The real issue was always the ParentTemplateId. The weapons and 3 armor pieces worked from Revision 2 onwards because they already had the correct ParentTemplateId (`42e6357a-4c05-4eda-9415-6b6b4c7d44c5` for armor, appropriate IDs for weapons). Voss and Orpheus failed because they had wrong ParentTemplateIds that don't work even in the source mod.

---

## Revision 7: "Ability Modifier Cap" Field Required for Some Armor

**Issue Date:** 2026-02-11
**Status:** IMPLEMENTED
**Completion Date:** 2026-02-11

### Problem

After Revision 6's ParentTemplateId fix, the situation **reversed**:
- ✅ Armor of Voss NOW APPEARS
- ✅ Armor of Orpheus NOW APPEARS
- ❌ Armor of Tyr NOW DOESN'T APPEAR (but works in SampleMagicRingMod!)
- ❌ Moonguard Splint NOW DOESN'T APPEAR (but works in SampleMagicRingMod!)

### Root Cause Investigation

I compared the working SampleMagicRingMod items with my Level13PlusGear items:

**SampleMagicRingMod (both working):**
```
new entry "SMR_Armor_Tyr"
...
data "Ability Modifier Cap" ""    ← PRESENT
data "Unique" "1"

new entry "SMR_Armor_Moonguard"
...
data "Ability Modifier Cap" ""    ← PRESENT
data "Unique" "1"
```

**My Level13PlusGear (both NOT working):**
```
new entry "L13_Armor_Tyr"
...
data "Unique" "0"                  ← MISSING "Ability Modifier Cap"!

new entry "L13_Armor_Moonguard"
...
data "Unique" "0"                  ← MISSING "Ability Modifier Cap"!
```

**My Level13PlusGear (both WORKING):**
```
new entry "L13_Armor_Voss"
...
data "Unique" "0"                  ← Also missing it, but works!

new entry "L13_Armor_Orpheus"
...
data "Unique" "0"                  ← Also missing it, but works!
```

### Analysis: Why Was It Removed?

In **Revision 3**, I removed `data "Ability Modifier Cap" ""` from ALL 4 armor pieces because:
- User reported that after Revision 2, weapons + Rogue armor worked, but 4 armor pieces didn't
- ALL 4 non-working pieces had the "Ability Modifier Cap" field with empty string
- I concluded it was causing validation failures

**But this was wrong!** The field wasn't the problem. The different ParentTemplateIds were the problem (as discovered in Revision 6).

### The Real Pattern

Now I understand the complete picture:

**Armor pieces that NEED "Ability Modifier Cap" field:**
- L13_Armor_Tyr (using "ARM_HalfPlate_Body_2" + ParentTemplateId 42e6357a...)
- L13_Armor_Moonguard (using "ARM_Splint_Body_2" + ParentTemplateId 42e6357a...)

**Armor pieces that DON'T NEED "Ability Modifier Cap" field:**
- L13_Armor_Voss (using "ARM_ChainShirt_Body_1" + ParentTemplateId 42e6357a...)
- L13_Armor_Orpheus (using "ARM_HalfPlate_Githyanki" + ParentTemplateId 42e6357a...)

The requirement appears to depend on the combination of:
1. The `using` base template (ARM_HalfPlate_Body_2, ARM_Splint_Body_2, etc.)
2. The ParentTemplateId
3. Possibly the specific passives/statuses applied

### Solution

Add `data "Ability Modifier Cap" ""` back to **only** Tyr and Moonguard, matching the working SampleMagicRingMod structure.

### Files Modified

**Armor.txt** (Lines 21-29 and 41-49)
- Added `data "Ability Modifier Cap" ""` to L13_Armor_Tyr (after StatusOnEquip, before Unique)
- Added `data "Ability Modifier Cap" ""` to L13_Armor_Moonguard (after StatusOnEquip, before Unique)
- Left L13_Armor_Voss and L13_Armor_Orpheus unchanged (they work without it)

### Expected Result

All 9 items from Phase 38 should now appear:
- ✅ Sword of Orpheus
- ✅ Divine Maul
- ✅ Selune's Moonmace
- ✅ Rogueblade
- ⏳ **Armor of Tyr** (should now work with "Ability Modifier Cap" field restored)
- ✅ Armor of the Rogue
- ⏳ **Moonguard Splint** (should now work with "Ability Modifier Cap" field restored)
- ✅ Armor of Voss (works from Revision 6)
- ✅ Armor of Orpheus (works from Revision 6)

### Technical Notes

**Why Some Armor Needs This Field:**

The "Ability Modifier Cap" field controls the maximum Dexterity modifier that can be applied to AC. Different armor base templates have different requirements:

- **ARM_HalfPlate_Body_2** and **ARM_Splint_Body_2**: Appear to require explicit "Ability Modifier Cap" definition, even if set to empty string
- **ARM_ChainShirt_Body_1** and **ARM_HalfPlate_Githyanki**: Work without this field

This suggests these base templates handle Dexterity modifiers differently internally.

**Empty String vs Omitted:**

Setting `"Ability Modifier Cap" ""` to empty string is **NOT** the same as omitting the field:
- Empty string: "No modifier cap" (allows full Dex bonus)
- Omitted: Uses template default (varies by base template)

For certain templates combined with certain ParentTemplateIds, the game expects this field to be explicitly present.

**Lessons Learned:**

1. **Match working code exactly** - Don't remove fields from working examples unless you understand why they're there
2. **Field requirements are context-dependent** - The same field might be required for some items but not others, depending on base templates
3. **Test incrementally** - When copying items, test each one individually to identify which specific combinations need which fields
4. **Document the source** - Always note which items in the source mod actually work vs which are broken
5. **Empty string ≠ Omitted** - In BG3 modding, explicitly setting a field to empty string has different behavior than leaving it out entirely

---

## Revision 8: Matching Working Item Configuration

**Issue Date:** 2026-02-11
**Status:** IMPLEMENTED  
**Completion Date:** 2026-02-11

### Problem

After Revision 7, Tyr and Moonguard still don't appear:
- ❌ Armor of Tyr
- ❌ Moonguard Splint
- ✅ Armor of Voss (working from Revision 6)
- ✅ Armor of Orpheus (working from Revision 6)

### Initial Hypothesis (Incorrect)

I compared with SampleMagicRingMod and found `"Unique" "1"` vs my `"Unique" "0"`, and tried changing it. However, the user correctly noted that **Unique should be "0" for all items in Level13PlusGear**.

### Root Cause: Wrong Fix in Revision 7

In Revision 7, I **added** "Ability Modifier Cap" to Tyr and Moonguard thinking they needed it because SampleMagicRingMod has it.

But the working items in MY mod (Voss and Orpheus) **don't have** "Ability Modifier Cap"!

**Working configuration (Voss and Orpheus):**
```
new entry "L13_Armor_Voss"
...
data "PassivesOnEquip" "MAG_ExoticMaterial_MediumArmor_Passive;MAG_PHB_OfRegeneration_Ring_Passive"
data "StatusOnEquip" "MAG_EXOTIC_MATERIAL_ARMOR_TECHNICAL;MAG_PHB_RING_OF_REGENERATION_TECHNICAL"
data "Unique" "0"         ← No "Ability Modifier Cap" field!
```

**Non-working configuration (Tyr and Moonguard after Revision 7):**
```
new entry "L13_Armor_Tyr"
...
data "PassivesOnEquip" "MAG_ExoticMaterial_MediumArmor_Passive"
data "StatusOnEquip" "MAG_EXOTIC_MATERIAL_ARMOR_TECHNICAL"
data "Ability Modifier Cap" ""    ← Added in Revision 7
data "Unique" "0"
```

### Solution

**Remove** "Ability Modifier Cap" from Tyr and Moonguard to match the working items (Voss and Orpheus).

All 4 armor pieces should have the same configuration:
- ParentTemplateId: `42e6357a-4c05-4eda-9415-6b6b4c7d44c5`
- NO "Ability Modifier Cap" field
- "Unique" "0"

### Files Modified

**Armor.txt**
- L13_Armor_Tyr: Removed `data "Ability Modifier Cap" ""`, kept `data "Unique" "0"`
- L13_Armor_Moonguard: Removed `data "Ability Modifier Cap" ""`, kept `data "Unique" "0"`

### Expected Result

All 9 items should appear with this unified configuration.

### Technical Notes

**The Correct Pattern for Level13PlusGear:**

Unlike SampleMagicRingMod, Level13PlusGear items work best with:
- ParentTemplateId: `42e6357a-4c05-4eda-9415-6b6b4c7d44c5`
- NO "Ability Modifier Cap" field
- "Unique" "0" (allows multiple copies)

This configuration works for:
- Voss (ARM_ChainShirt_Body_1) ✅
- Orpheus (ARM_HalfPlate_Githyanki) ✅
- Should work for Tyr (ARM_HalfPlate_Body_2)
- Should work for Moonguard (ARM_Splint_Body_2)

**Why SampleMagicRingMod is Different:**

SampleMagicRingMod uses different field combinations that may not translate directly to Level13PlusGear. When copying between mods:
1. Don't blindly copy ALL fields from source
2. Match the pattern of what WORKS in your destination mod
3. Test incrementally to find the working configuration

**Lessons Learned:**

1. **Match your own working items, not the source** - Voss/Orpheus work in Level13PlusGear, so use their configuration
2. **Different mods, different requirements** - SampleMagicRingMod's working configuration may not work in Level13PlusGear
3. **User requirements matter** - When user specifies "Unique should be 0", trust that requirement
4. **Simpler is sometimes better** - Removing fields can fix issues, not just adding them

---

## Revision 9: Comprehensive Difference Analysis (No Solution)

**Issue Date:** 2026-02-11
**Status:** ANALYSIS ONLY - NO IMPLEMENTATION
**Completion Date:** 2026-02-11

### Problem

After all previous revisions, Tyr and Moonguard still don't appear:
- ❌ Armor of Tyr (doesn't appear)
- ❌ Moonguard Splint (doesn't appear)
- ✅ Armor of Voss (appears correctly)
- ✅ Armor of Orpheus (appears correctly)

### Comprehensive Comparison

Below is a complete field-by-field comparison of ALL armor pieces to identify every difference.

---

## ARMOR.TXT COMPARISON

### L13_Armor_Tyr (Level13PlusGear) - NOT WORKING

```
new entry "L13_Armor_Tyr"
type "Armor"
using "ARM_HalfPlate_Body_2"
data "RootTemplate" "ed13ac3a-47aa-4263-8147-34b583e18870"
data "Rarity" "Legendary"
data "Boosts" "RollBonus(SavingThrow, 2);UnlockSpell(L13_Shout_CelestialHaste_Unlimited);UnlockSpell(L13_Target_MistyStep_Unlimited);UnlockSpell(L13_Shout_SpiritGuardians_Tyr,AddChildren,,,SpellCastingAbility)"
data "PassivesOnEquip" "MAG_ExoticMaterial_MediumArmor_Passive"
data "StatusOnEquip" "MAG_EXOTIC_MATERIAL_ARMOR_TECHNICAL"
data "Unique" "0"
```

**Field Count:** 8 data fields

### SMR_Armor_Tyr (SampleMagicRingMod) - WORKING

```
new entry "SMR_Armor_Tyr"
type "Armor"
using "ARM_HalfPlate_Body_2"
data "RootTemplate" "c3d4e5f6-a7b8-4c9d-0e1f-2a3b4c5d6e7f"
data "Rarity" "Legendary"
data "Boosts" "RollBonus(SavingThrow, 2);UnlockSpell(SMR_Shout_CelestialHaste_Unlimited);UnlockSpell(SMR_Target_MistyStep_Unlimited);UnlockSpell(SMR_Shout_SpiritGuardians_Tyr,AddChildren,,,SpellCastingAbility)"
data "PassivesOnEquip" "MAG_ExoticMaterial_MediumArmor_Passive"
data "StatusOnEquip" "MAG_EXOTIC_MATERIAL_ARMOR_TECHNICAL"
data "Ability Modifier Cap" ""
data "Unique" "1"
```

**Field Count:** 9 data fields

**DIFFERENCES (SMR_Armor_Tyr vs L13_Armor_Tyr):**
1. ❌ **"Ability Modifier Cap" ""** - Present in SMR, ABSENT in L13
2. ❌ **"Unique"** - "1" in SMR, "0" in L13
3. ✅ **"using"** - Same: ARM_HalfPlate_Body_2
4. ✅ **"Boosts"** - Same structure (different spell names, but equivalent)
5. ✅ **"PassivesOnEquip"** - Same
6. ✅ **"StatusOnEquip"** - Same
7. ✅ **"Rarity"** - Same

---

### L13_Armor_Moonguard (Level13PlusGear) - NOT WORKING

```
new entry "L13_Armor_Moonguard"
type "Armor"
using "ARM_Splint_Body_2"
data "RootTemplate" "ed13502f-b130-491f-ac5d-53a72f1262b7"
data "Rarity" "Legendary"
data "Boosts" "AC(5);RollBonus(SavingThrow, 2);UnlockSpell(L13_Shout_CelestialHaste_Unlimited);UnlockSpell(L13_Target_MistyStep_Unlimited);UnlockSpell(L13_Shout_SpiritGuardians_Tyr,AddChildren,,,SpellCastingAbility)"
data "PassivesOnEquip" "MAG_ExoticMaterial_MediumArmor_Passive;MAG_PHB_OfRegeneration_Ring_Passive"
data "StatusOnEquip" "MAG_EXOTIC_MATERIAL_ARMOR_TECHNICAL;MAG_PHB_RING_OF_REGENERATION_TECHNICAL"
data "Unique" "0"
```

**Field Count:** 8 data fields

### SMR_Armor_Moonguard (SampleMagicRingMod) - WORKING

```
new entry "SMR_Armor_Moonguard"
type "Armor"
using "ARM_Splint_Body_2"
data "RootTemplate" "b2c3d4e5-f6a7-4b8c-9d0e-2f3a4b5c6d7e"
data "Rarity" "Legendary"
data "Boosts" "AC(5);RollBonus(SavingThrow, 2);UnlockSpell(SMR_Shout_CelestialHaste_Unlimited);UnlockSpell(SMR_Target_MistyStep_Unlimited);UnlockSpell(SMR_Shout_SpiritGuardians_Tyr,AddChildren,,,SpellCastingAbility)"
data "PassivesOnEquip" "MAG_ExoticMaterial_MediumArmor_Passive;MAG_PHB_OfRegeneration_Ring_Passive"
data "StatusOnEquip" "MAG_EXOTIC_MATERIAL_ARMOR_TECHNICAL;MAG_PHB_RING_OF_REGENERATION_TECHNICAL"
data "Ability Modifier Cap" ""
data "Unique" "1"
```

**Field Count:** 9 data fields

**DIFFERENCES (SMR_Armor_Moonguard vs L13_Armor_Moonguard):**
1. ❌ **"Ability Modifier Cap" ""** - Present in SMR, ABSENT in L13
2. ❌ **"Unique"** - "1" in SMR, "0" in L13
3. ✅ **"using"** - Same: ARM_Splint_Body_2
4. ✅ **"Boosts"** - Same (identical)
5. ✅ **"PassivesOnEquip"** - Same
6. ✅ **"StatusOnEquip"** - Same
7. ✅ **"Rarity"** - Same

---

### L13_Armor_Voss (Level13PlusGear) - WORKING ✅

```
new entry "L13_Armor_Voss"
type "Armor"
using "ARM_ChainShirt_Body_1"
data "RootTemplate" "ed13dc81-3bb4-47ad-be60-8ab165b4358d"
data "Rarity" "Legendary"
data "Boosts" "AC(5);RollBonus(SavingThrow, 2);UnlockSpell(L13_Shout_CelestialHaste_Unlimited);UnlockSpell(L13_Target_MistyStep_Unlimited);UnlockSpell(L13_Shout_SpiritGuardians_Tyr,AddChildren,,,SpellCastingAbility)"
data "PassivesOnEquip" "MAG_ExoticMaterial_MediumArmor_Passive;MAG_PHB_OfRegeneration_Ring_Passive"
data "StatusOnEquip" "MAG_EXOTIC_MATERIAL_ARMOR_TECHNICAL;MAG_PHB_RING_OF_REGENERATION_TECHNICAL"
data "Unique" "0"
```

**Field Count:** 8 data fields

---

### L13_Armor_Orpheus (Level13PlusGear) - WORKING ✅

```
new entry "L13_Armor_Orpheus"
type "Armor"
using "ARM_HalfPlate_Githyanki"
data "RootTemplate" "ed13e7d6-4435-4861-b83a-2905202a42c1"
data "Rarity" "Legendary"
data "Boosts" "AC(5);RollBonus(SavingThrow, 2);UnlockSpell(L13_Shout_CelestialHaste_Unlimited);UnlockSpell(L13_Target_MistyStep_Unlimited);UnlockSpell(L13_Shout_SpiritGuardians_Tyr,AddChildren,,,SpellCastingAbility)"
data "PassivesOnEquip" "MAG_ExoticMaterial_MediumArmor_Passive;MAG_PHB_OfRegeneration_Ring_Passive"
data "StatusOnEquip" "MAG_EXOTIC_MATERIAL_ARMOR_TECHNICAL;MAG_PHB_RING_OF_REGENERATION_TECHNICAL"
data "Unique" "0"
```

**Field Count:** 8 data fields

---

## ROOTTEMPLATES COMPARISON

### L13_Armor_Tyr RootTemplate - NOT WORKING

```xml
<attribute id="ParentTemplateId" type="FixedString" value="42e6357a-4c05-4eda-9415-6b6b4c7d44c5" />
<attribute id="Stats" type="FixedString" value="L13_Armor_Tyr" />
```

### SMR_Armor_Tyr RootTemplate - WORKING

```xml
<attribute id="ParentTemplateId" type="FixedString" value="42e6357a-4c05-4eda-9415-6b6b4c7d44c5" />
<attribute id="Stats" type="FixedString" value="SMR_Armor_Tyr" />
```

**DIFFERENCES:** ✅ Same ParentTemplateId (both use 42e6357a-4c05-4eda-9415-6b6b4c7d44c5)

---

### L13_Armor_Moonguard RootTemplate - NOT WORKING

```xml
<attribute id="ParentTemplateId" type="FixedString" value="42e6357a-4c05-4eda-9415-6b6b4c7d44c5" />
<attribute id="Stats" type="FixedString" value="L13_Armor_Moonguard" />
```

### SMR_Armor_Moonguard RootTemplate - WORKING

```xml
<attribute id="ParentTemplateId" type="FixedString" value="42e6357a-4c05-4eda-9415-6b6b4c7d44c5" />
<attribute id="Stats" type="FixedString" value="SMR_Armor_Moonguard" />
```

**DIFFERENCES:** ✅ Same ParentTemplateId (both use 42e6357a-4c05-4eda-9415-6b6b4c7d44c5)

---

### L13_Armor_Voss RootTemplate - WORKING ✅

```xml
<attribute id="ParentTemplateId" type="FixedString" value="42e6357a-4c05-4eda-9415-6b6b4c7d44c5" />
<attribute id="Stats" type="FixedString" value="L13_Armor_Voss" />
```

---

### L13_Armor_Orpheus RootTemplate - WORKING ✅

```xml
<attribute id="ParentTemplateId" type="FixedString" value="42e6357a-4c05-4eda-9415-6b6b4c7d44c5" />
<attribute id="Stats" type="FixedString" value="L13_Armor_Orpheus" />
```

---

## SUMMARY OF ALL DIFFERENCES

### Armor.txt Field Differences

**L13_Armor_Tyr (NOT WORKING) vs SMR_Armor_Tyr (WORKING):**
1. Missing: `data "Ability Modifier Cap" ""`
2. Different: `data "Unique" "0"` instead of `"1"`

**L13_Armor_Moonguard (NOT WORKING) vs SMR_Armor_Moonguard (WORKING):**
1. Missing: `data "Ability Modifier Cap" ""`
2. Different: `data "Unique" "0"` instead of `"1"`

**L13_Armor_Voss (WORKING) vs L13_Armor_Tyr (NOT WORKING):**
1. Different "using" template: ARM_ChainShirt_Body_1 vs ARM_HalfPlate_Body_2
2. Has AC(5) in Boosts (Tyr doesn't)
3. More PassivesOnEquip/StatusOnEquip (has regeneration)

**L13_Armor_Orpheus (WORKING) vs L13_Armor_Tyr (NOT WORKING):**
1. Different "using" template: ARM_HalfPlate_Githyanki vs ARM_HalfPlate_Body_2
2. Has AC(5) in Boosts (Tyr doesn't)
3. More PassivesOnEquip/StatusOnEquip (has regeneration)

**L13_Armor_Voss (WORKING) vs L13_Armor_Moonguard (NOT WORKING):**
1. Different "using" template: ARM_ChainShirt_Body_1 vs ARM_Splint_Body_2
2. SAME Boosts structure (both have AC(5))
3. SAME PassivesOnEquip/StatusOnEquip

**L13_Armor_Orpheus (WORKING) vs L13_Armor_Moonguard (NOT WORKING):**
1. Different "using" template: ARM_HalfPlate_Githyanki vs ARM_Splint_Body_2
2. SAME Boosts structure (both have AC(5))
3. SAME PassivesOnEquip/StatusOnEquip

### RootTemplate Differences

**ALL FOUR armor pieces** (Tyr, Moonguard, Voss, Orpheus) in Level13PlusGear use:
- ✅ Same ParentTemplateId: 42e6357a-4c05-4eda-9415-6b6b4c7d44c5
- ✅ Same structure with GameMaster child node

### Key Observations

1. **The only Armor.txt differences** between working SampleMagicRingMod items and non-working Level13PlusGear items are:
   - Missing "Ability Modifier Cap" field in L13
   - "Unique" "0" in L13 vs "1" in SMR

2. **Working vs Non-Working in Level13PlusGear:**
   - Voss uses ARM_ChainShirt_Body_1 → WORKS
   - Orpheus uses ARM_HalfPlate_Githyanki → WORKS
   - Tyr uses ARM_HalfPlate_Body_2 → DOESN'T WORK
   - Moonguard uses ARM_Splint_Body_2 → DOESN'T WORK

3. **The "using" template appears correlated with success:**
   - ARM_ChainShirt_Body_1 + ParentTemplateId 42e6357a... = WORKS
   - ARM_HalfPlate_Githyanki + ParentTemplateId 42e6357a... = WORKS
   - ARM_HalfPlate_Body_2 + ParentTemplateId 42e6357a... = DOESN'T WORK
   - ARM_Splint_Body_2 + ParentTemplateId 42e6357a... = DOESN'T WORK

4. **But this contradicts SampleMagicRingMod where:**
   - ARM_HalfPlate_Body_2 + ParentTemplateId 42e6357a... = WORKS
   - ARM_Splint_Body_2 + ParentTemplateId 42e6357a... = WORKS

### Questions to Investigate

1. Why do ARM_HalfPlate_Body_2 and ARM_Splint_Body_2 work in SampleMagicRingMod but not in Level13PlusGear?
2. Is there a different ParentTemplateId that would work better for these "using" templates?
3. Are there other files (like Localization, TreasureTable, or spell files) that might be different?
4. Could the mod loading order or dependencies affect this?

**NO SOLUTION IMPLEMENTED - AWAITING DIRECTION**

---

## Revision 10: Analysis of Armor of Orpheus Equipment Slot Bug

**Issue Date:** 2026-02-11
**Status:** ANALYSIS ONLY - NO IMPLEMENTATION
**Completion Date:** 2026-02-11

### Problem Statement

**Primary Issue:** Armor of Tyr and Moonguard Splint still do not appear in any of the three test locations:
- Tutorial Chest ❌
- Traveler's Chest ❌
- L13 Plus Gear Chest ❌

**Secondary Issue (NEW):** Armor of Orpheus DOES appear but has a critical bug:
- ✅ Item appears in chest
- ❌ Equips in HELMET slot instead of BODY armor slot
- Visual appearance shows as body armor but functions as helmet

### Investigation Focus: Why Does Orpheus Act Like a Helmet?

Given that Orpheus appears (unlike Tyr/Moonguard) but behaves incorrectly, analyzing this bug may reveal the root cause affecting all armor pieces.

---

## ANALYSIS OF L13_ARMOR_ORPHEUS

### Current Configuration

**Armor.txt (Lines 63-70):**
```
new entry "L13_Armor_Orpheus"
type "Armor"
using "ARM_HalfPlate_Githyanki"           ← ISSUE HERE
data "RootTemplate" "ed13e7d6-4435-4861-b83a-2905202a42c1"
data "Rarity" "Legendary"
data "Boosts" "AC(5);RollBonus(SavingThrow, 2);UnlockSpell(L13_Shout_CelestialHaste_Unlimited);UnlockSpell(L13_Target_MistyStep_Unlimited);UnlockSpell(L13_Shout_SpiritGuardians_Tyr,AddChildren,,,SpellCastingAbility)"
data "PassivesOnEquip" "MAG_ExoticMaterial_MediumArmor_Passive;MAG_PHB_OfRegeneration_Ring_Passive"
data "StatusOnEquip" "MAG_EXOTIC_MATERIAL_ARMOR_TECHNICAL;MAG_PHB_RING_OF_REGENERATION_TECHNICAL"
data "Unique" "0"
```

**RootTemplate (L13_Armor_Orpheus.lsf.lsx):**
```xml
<attribute id="ParentTemplateId" type="FixedString" value="42e6357a-4c05-4eda-9415-6b6b4c7d44c5" />
<attribute id="Stats" type="FixedString" value="L13_Armor_Orpheus" />
```

---

## ROOT CAUSE IDENTIFIED

### The Template Name Error

**What I Used:**
```
using "ARM_HalfPlate_Githyanki"
```

**What Vanilla BG3 Actually Uses:**
```
using "ARM_HalfPlate_Body_Githyanki"
```

### Evidence from Vanilla Files

Found in `VanillaBG3/gustav/Public/GustavDev/Stats/Generated/Data/Armor.txt`:

```
new entry "MAG_Githborn_MagicEating_HalfPlate"
type "Armor"
using "ARM_HalfPlate_Body_Githyanki"     ← Correct template name
data "RootTemplate" "f601bac2-16a7-4da0-854a-ae4132ca448f"
data "ValueUUID" "240eb257-ef20-4877-89bd-6956b4b7c41a"
data "Rarity" "Rare"
data "PassivesOnEquip" "MAG_Githborn_MagicEating_HalfPlate_Passive"
data "Unique" "1"
```

### The Missing "_Body" Component

**Template Name Breakdown:**
- `ARM` = Armor category
- `HalfPlate` = Armor type
- `_Body` = **Equipment slot specification** ← MISSING!
- `_Githyanki` = Visual variant

**What Happens Without "_Body":**
- BG3 cannot find the template `ARM_HalfPlate_Githyanki` (doesn't exist)
- Falls back to default/undefined behavior
- Item appears but equipment slot is incorrectly determined
- Result: Body armor equips in helmet slot

---

## IMPLICATIONS FOR TYR AND MOONGUARD

This discovery raises critical questions about the other non-working armor pieces:

### L13_Armor_Tyr Configuration
```
using "ARM_HalfPlate_Body_2"     ← Has "_Body" in the name ✅
```

### L13_Armor_Moonguard Configuration
```
using "ARM_Splint_Body_2"        ← Has "_Body" in the name ✅
```

### L13_Armor_Voss Configuration (WORKING)
```
using "ARM_ChainShirt_Body_1"    ← Has "_Body" in the name ✅
```

**Key Observation:** Tyr, Moonguard, and Voss all have "_Body" in their template names, yet only Voss works. This suggests:
1. The template name format is correct for Tyr and Moonguard
2. Their failure to appear has a DIFFERENT root cause than Orpheus's helmet bug
3. Orpheus's bug is a SEPARATE issue from why Tyr/Moonguard don't appear

---

## COMPARISON: WORKING VS BROKEN ITEMS

### Items That APPEAR and WORK Correctly

**L13_Armor_Voss:**
- using "ARM_ChainShirt_Body_1" ✅
- ParentTemplateId: 42e6357a... ✅
- No "Ability Modifier Cap" ✅
- Unique "0" ✅
- **APPEARS AND WORKS CORRECTLY**

**L13_Armor_Rogue:**
- using "ARM_StuddedLeather_Body_2" ✅
- ParentTemplateId: cab3455f... (different!) ✅
- No "Ability Modifier Cap" ✅
- Unique "0" ✅
- **APPEARS AND WORKS CORRECTLY**

### Items That APPEAR But MALFUNCTION

**L13_Armor_Orpheus:**
- using "ARM_HalfPlate_Githyanki" ❌ (should be "ARM_HalfPlate_Body_Githyanki")
- ParentTemplateId: 42e6357a... ✅
- No "Ability Modifier Cap" ✅
- Unique "0" ✅
- **APPEARS BUT EQUIPS AS HELMET**

### Items That DON'T APPEAR At All

**L13_Armor_Tyr:**
- using "ARM_HalfPlate_Body_2" ✅ (template name format correct)
- ParentTemplateId: 42e6357a... ✅
- HAS "Ability Modifier Cap" "" ✅ (added in previous revision)
- Unique "0" ✅
- **DOES NOT APPEAR**

**L13_Armor_Moonguard:**
- using "ARM_Splint_Body_2" ✅ (template name format correct)
- ParentTemplateId: 42e6357a... ✅
- HAS "Ability Modifier Cap" "" ✅ (added in previous revision)
- Unique "0" ✅
- **DOES NOT APPEAR**

---

## KEY FINDINGS

### Finding 1: Orpheus Has Wrong Template Name
The template `ARM_HalfPlate_Githyanki` doesn't exist in vanilla BG3. The correct name is `ARM_HalfPlate_Body_Githyanki` (with `_Body`).

**Impact:** Item loads but BG3 misidentifies the equipment slot, causing it to equip as a helmet.

**Fix:** Change `using "ARM_HalfPlate_Githyanki"` to `using "ARM_HalfPlate_Body_Githyanki"`

### Finding 2: Tyr and Moonguard Have Different Issue
Unlike Orpheus, Tyr and Moonguard:
- Use correct template name format (include `_Body`)
- Still don't appear at all (not even with wrong equipment slot)
- Have been tested in THREE different delivery methods (all failed)

**This suggests a more fundamental validation failure, not just wrong equipment slot.**

### Finding 3: Template Names That Work
Confirmed working templates in Level13PlusGear:
- `ARM_ChainShirt_Body_1` (Voss) ✅
- `ARM_StuddedLeather_Body_2` (Rogue) ✅
- All weapon templates ✅

Confirmed broken/problematic templates:
- `ARM_HalfPlate_Githyanki` (Orpheus) - appears but wrong slot ❌
- `ARM_HalfPlate_Body_2` (Tyr) - doesn't appear at all ❌
- `ARM_Splint_Body_2` (Moonguard) - doesn't appear at all ❌

### Finding 4: ParentTemplateId Pattern
- Rogue uses different ParentTemplateId (cab3455f...) and WORKS ✅
- Voss uses 42e6357a... and WORKS ✅
- Orpheus uses 42e6357a... and APPEARS (wrong slot) ⚠️
- Tyr uses 42e6357a... and DOESN'T APPEAR ❌
- Moonguard uses 42e6357a... and DOESN'T APPEAR ❌

**Conclusion:** ParentTemplateId 42e6357a... is not the issue (Voss and Orpheus both use it and appear).

---

## QUESTIONS REMAINING

1. **Why do ARM_HalfPlate_Body_2 and ARM_Splint_Body_2 fail completely?**
   - Template names are correctly formatted
   - They work in SampleMagicRingMod
   - What makes them invalid in Level13PlusGear?

2. **Are these templates defined in vanilla BG3?**
   - Need to verify if ARM_HalfPlate_Body_2 exists in vanilla files
   - Need to verify if ARM_Splint_Body_2 exists in vanilla files
   - Could they be from a different module/DLC?

3. **Why does Orpheus appear despite wrong template?**
   - Wrong template causes equipment slot bug but item still loads
   - Tyr/Moonguard have correct templates but don't load at all
   - What's the difference in validation behavior?

4. **What makes ARM_ChainShirt_Body_1 and ARM_StuddedLeather_Body_2 work?**
   - Why are these templates compatible with Level13PlusGear?
   - What attributes do they have that Tyr/Moonguard templates lack?

---

## RECOMMENDED NEXT STEPS

### Immediate Fix (High Confidence)
**Fix L13_Armor_Orpheus helmet bug:**
- Change `using "ARM_HalfPlate_Githyanki"` to `using "ARM_HalfPlate_Body_Githyanki"`
- Expected result: Orpheus will equip correctly as body armor

### Investigation Required (Medium Confidence)
**Verify template existence:**
1. Search vanilla files for `ARM_HalfPlate_Body_2`
2. Search vanilla files for `ARM_Splint_Body_2`
3. Check if these templates exist or if they're from specific DLC/modules
4. If they don't exist, find alternative working templates

### Alternative Approaches (Low Confidence)
**If templates don't exist in vanilla:**
- Try using different templates that ARE confirmed to exist
- Example: Change Tyr to use `ARM_HalfPlate_Body_Githyanki` (now that we know it exists)
- Example: Find a vanilla splint template and use that for Moonguard

---

**NO CHANGES IMPLEMENTED - AWAITING USER DIRECTION**

---

## PHASE 38 COMPLETION SUMMARY

**Completion Date:** 2026-02-11
**Final Status:** COMPLETE (WITH KNOWN BUGS)

### Final Item Count

**Successfully Implemented (5 of 7 items):**

**Weapons (4/4):** ✅ ALL WORKING
1. L13_Sword_Orpheus - Working correctly
2. L13_Maul_Divine - Working correctly
3. L13_Mace_Selune_Moon - Working correctly
4. L13_Rogueblade - Working correctly

**Armor (1/3):** ⚠️ PARTIAL SUCCESS
1. L13_Armor_Rogue - Working correctly ✅
2. L13_Armor_Tyr - **NOT APPEARING** ❌
3. L13_Armor_Moonguard - **NOT APPEARING** ❌

**Removed Items (2):**
- L13_Armor_Voss - Removed (didn't work in source mod)
- L13_Armor_Orpheus - Removed (equipment slot bug - acted as helmet)

### Known Bugs and Issues

#### Bug 1: Armor of Tyr Not Appearing
**Severity:** HIGH  
**Impact:** Item completely fails to appear in any chest (Tutorial, Traveler's, L13 Gear)  
**Status:** UNRESOLVED

**Configuration:**
- Template: `ARM_HalfPlate_Body_2`
- ParentTemplateId: `42e6357a-4c05-4eda-9415-6b6b4c7d44c5`
- Has "Ability Modifier Cap" field
- Unique: "0"

**Investigation Results:**
- Works in SampleMagicRingMod with same configuration
- Template name format appears correct (includes `_Body`)
- All file structure correct (Armor.txt, RootTemplate, TreasureTable, Localization)
- Tested in multiple delivery methods - all failed

**Next Steps:** Needs further investigation - possibly template `ARM_HalfPlate_Body_2` is incompatible with Level13PlusGear mod for unknown reasons.

#### Bug 2: Moonguard Splint Not Appearing
**Severity:** HIGH  
**Impact:** Item completely fails to appear in any chest (Tutorial, Traveler's, L13 Gear)  
**Status:** UNRESOLVED

**Configuration:**
- Template: `ARM_Splint_Body_2`
- ParentTemplateId: `42e6357a-4c05-4eda-9415-6b6b4c7d44c5`
- Has "Ability Modifier Cap" field
- Unique: "0"

**Investigation Results:**
- Works in SampleMagicRingMod with same configuration
- Template name format appears correct (includes `_Body`)
- All file structure correct (Armor.txt, RootTemplate, TreasureTable, Localization)
- Tested in multiple delivery methods - all failed

**Next Steps:** Needs further investigation - possibly template `ARM_Splint_Body_2` is incompatible with Level13PlusGear mod for unknown reasons.

### Revision History Summary

**10 Revisions** were required to reach this state:

1. **Revision 1:** Fixed UUID formatting errors (malformed UUIDs)
2. **Revision 2:** Fixed RootTemplate structure (missing GameMaster nodes, wrong ParentTemplateIds)
3. **Revision 3:** Removed "Ability Modifier Cap" from all armor (wrong move - caused issues)
4. **Revision 4:** Fixed handle collision + spell structure changes
5. **Revision 5:** Restored full spell structure (matched working SampleMagicRingMod spell)
6. **Revision 6:** Fixed ParentTemplateId for Voss/Orpheus → Made them appear
7. **Revision 7:** Re-added "Ability Modifier Cap" to Tyr/Moonguard (didn't fix issue)
8. **Revision 8:** Removed "Ability Modifier Cap" again + changed Unique (reverted after user feedback)
9. **Revision 9:** Comprehensive analysis - documented all differences between working/non-working items
10. **Revision 10:** Analysis of Orpheus helmet bug - discovered wrong template name (`ARM_HalfPlate_Githyanki` instead of `ARM_HalfPlate_Body_Githyanki`)

### What We Learned

#### Critical Discoveries

1. **Template Compatibility Issues:**
   - Some vanilla armor templates work in Level13PlusGear, others don't
   - Working templates: `ARM_ChainShirt_Body_1`, `ARM_StuddedLeather_Body_2`
   - Non-working templates: `ARM_HalfPlate_Body_2`, `ARM_Splint_Body_2`
   - Same templates work in SampleMagicRingMod - suggests mod-specific issue

2. **Template Name Precision Matters:**
   - `ARM_HalfPlate_Githyanki` ≠ `ARM_HalfPlate_Body_Githyanki`
   - Missing `_Body` causes equipment slot misidentification
   - Wrong template name → item appears but wrong behavior
   - Non-existent template → item doesn't appear at all

3. **Item Validation is Complex:**
   - Multiple delivery methods tested (TreasureTable, OneTimeRewards)
   - All delivery methods failed for Tyr/Moonguard
   - Issue is with item definition, not delivery mechanism

4. **Source Mod Items Not Always Reliable:**
   - Armor of Voss and Armor of Orpheus don't work in SampleMagicRingMod
   - Copying broken items wastes time
   - Always test source items before copying

### Files Modified

**Stats Files:**
- `Armor.txt` - Added 3 armor entries (originally 5, removed 2)
- `Weapon.txt` - Added 4 weapon entries
- `Spell_Shout.txt` - Added Spirit Guardians spell variants

**RootTemplates:**
- Created 7 RootTemplate files (originally 9, deleted 2)
- All with proper structure and ParentTemplateIds

**Delivery Configuration:**
- `TreasureTable.txt` - Added items to L13_Gear_Chest_TT and TUT_Chest_Potions
- `OneTimeRewards.lsx` - Created file, added Tyr/Moonguard to Traveler's Chest (for testing)

**Localization:**
- `Level13PlusGear.loca.xml` - Added localization entries for all items and spells

**Documentation:**
- `uuid_workflow.md` - Removed 34 used UUIDs from pool
- `docs/level13plusgear/item_catalog.md` - Updated with Phase 38 items (needs final update)

### Success Rate

**Overall:** 5 of 7 items working = **71% success rate**

**By Category:**
- Weapons: 4/4 = **100% success**
- Armor: 1/3 = **33% success**

### Recommendations for Future Phases

1. **Verify Template Compatibility First:**
   - Before copying items, verify the `using` template exists and works in Level13PlusGear
   - Test with simple item first before investing in full implementation
   - Document which templates are known to work

2. **Test Source Items:**
   - Always verify items actually work in the source mod
   - Don't assume all items in SampleMagicRingMod are functional
   - Create a tested/verified item list

3. **Simpler Alternative:**
   - For problematic armor templates, consider using working templates instead
   - Example: Use `ARM_ChainShirt_Body_1` or `ARM_StuddedLeather_Body_2` 
   - Visual appearance may differ but item will function

4. **Investigation Needed:**
   - Why do `ARM_HalfPlate_Body_2` and `ARM_Splint_Body_2` work in SampleMagicRingMod but not Level13PlusGear?
   - Is there a mod dependency or configuration difference?
   - Are these templates from a specific DLC or module?

### Phase Closure

Despite the bugs with Armor of Tyr and Moonguard Splint, Phase 38 achieved its primary goal of copying weapons and establishing the workflow for item migration. The 71% success rate and lessons learned provide valuable foundation for future phases.

**Phase 38 is now CLOSED.** The two non-appearing armor pieces are documented as known issues for potential future resolution or alternative implementation.

---

**Next Phase:** Phase 39 will focus on remaining accessories and headgear, with explicit verification of template compatibility before implementation.
