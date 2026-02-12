# Phase 38: Copy Weapons and Body Armor from SampleMagicRingMod

**Status:** PENDING
**Date:** 2026-02-11

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

## Phase 38 Status: PENDING

**Awaiting user decision on scope and UUID generation.**
