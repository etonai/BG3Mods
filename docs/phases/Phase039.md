# Phase 39: Copy Headgear and Gloves

**Status:** COMPLETE
**Date:** 2026-02-11
**Completion Date:** 2026-02-11

---

## Goals

1. **Copy Headgear:** Copy 5 headgear items (Helmet of Tyr, Circlet of Tyr, Magus Circlet, Moonguard Helm, Moonguard Circlet)
2. **Copy Gloves:** Copy 2 glove items (Gloves of Tyr, Moonguard Gloves)
3. **Maintain Independence:** Ensure all copied items are fully independent from SampleMagicRingMod
4. **Complete Documentation:** Update item catalog and track all UUID usage

**Prerequisite:** Phase 38 must be completed (weapons and body armor copied)

**Note:** Cloaks and shields moved to Phase 40. Ring of the Guardian moved to Phase 41.

---

## Phase 39 Item Inventory

This table lists all 7 items to be copied in Phase 39.

| # | Item | Type | Rarity | Complexity | Est. UUIDs |
|---|------|------|--------|------------|------------|
| **HEADGEAR (5 items)** |
| 1 | SMR_Helmet_Tyr | Metal Helmet | Legendary | Medium | ~10 |
| 2 | SMR_Circlet_Tyr | Circlet | Legendary | Medium | ~10 |
| 3 | SMR_Circlet_Magus | Circlet | Legendary | Low-Medium | ~8 |
| 4 | SMR_Helmet_Moonguard | Metal Helmet | Legendary | Medium-High | ~12 |
| 5 | SMR_Circlet_Moonguard | Circlet | Legendary | Medium | ~10 |
| **GLOVES (2 items)** |
| 6 | SMR_Gloves_Tyr | Gloves | Legendary | Low-Medium | ~6 |
| 7 | SMR_Gloves_Moonguard | Gloves | Legendary | Medium | ~8 |
| **TOTAL** | **7 items** | | | | **~64** |

**Items Moved to Phase 40:**
- Cloaks (3 items): Cloak of Tyr, Cloak of the Rogue, Moonguard Cloak
- Shields (2 items): Shield of Tyr, Moonguard Shield

**Items Moved to Phase 41:**
- Ring of the Guardian (1 item)

---

## Implementation Strategy

### Group 1: Headgear (5 items, ~50 UUIDs)

**Tyr Set (2 items):**
- **Helmet of Tyr:** Helmet with regeneration, immunities, utility spells
- **Circlet of Tyr:** Similar to helmet but circlet appearance
- **Reason:** Share similar spell sets (Speak with Dead, See Invisibility, Protection from Evil, Faerie Fire)

**Moonguard Set (2 items):**
- **Moonguard Helm:** Helmet with Smite the Graceless passive, regeneration, immunities
- **Moonguard Circlet:** Circlet variant of Moonguard helmet
- **Reason:** Share Moonguard-themed abilities

**Magus Set (1 item):**
- **Magus Circlet:** Simpler circlet with utility spells, no heavy combat passives

### Group 2: Gloves (2 items, ~14 UUIDs)

- **Gloves of Tyr:** Tyr-themed gloves with defensive/utility abilities
- **Moonguard Gloves:** Moonguard-themed gloves with similar abilities

---

## Estimated Resource Requirements

### UUID Usage by Group

| Group | Items | UUIDs per Item | Total UUIDs |
|-------|-------|----------------|-------------|
| Headgear | 5 | 10 | 50 |
| Gloves | 2 | 7 | 14 |
| **Phase 39 Total** | **7** | **Avg: 9.1** | **~64** |

**Items Moved to Other Phases:**
- Cloaks (3 items, ~18 UUIDs) → Phase 40
- Shields (2 items, ~14 UUIDs) → Phase 40
- Ring of the Guardian (1 item, ~18 UUIDs) → Phase 41

**Current UUID Pool:** 91 UUIDs available

**Action Required:** Current UUID pool is sufficient for Phase 39. May need additional UUIDs for Phases 40-41.

### File Modifications

**Existing Files to Modify:**
- `Armor.txt` - Add all headgear and gloves
- `Spell_Target.txt` - Add custom target spells (if any new ones)
- `Spell_Shout.txt` - Add custom shout spells (if any new ones)
- `TreasureTable.txt` - Add all items to L13_Gear_Chest
- `Level13PlusGear.loca.xml` - Add localization for items and custom spells

**New Files to Create:**
- RootTemplates for all 7 items (7 .lsf.lsx files)

**Potential New Spell Files:**
- Most spells will likely reuse existing vanilla spells or spells already in L13 mod

---

## Item Details Preview

### Headgear Shared Abilities

**Tyr Headgear (Helmet & Circlet):**
- Critical Hit Immunity
- Speak with Dead, Speak with Animals
- See Invisibility (unlimited)
- Protection from Evil and Good (unlimited)
- Faerie Fire (short rest)
- +1 AC, +1 Saves
- Stun/Fear/Blind Immunity
- Darkvision
- Regeneration (2 HP/turn)

**Moonguard Headgear:**
- Similar to Tyr but with Smite the Graceless passive (Moonguard Helm)
- Radiating Orb on enemy miss

**Magus Circlet:**
- Utility spells (Speak with Dead, See Invisibility, Protection, Faerie Fire)
- Fear/Blind Immunity, Darkvision
- No regeneration or AC bonuses (lighter version)

### Ring of the Guardian Abilities

**Complex Healing/Support Ring:**
- Superior Healing Word (2d20 healing)
- Bless (unlimited)
- Create Water (unlimited)
- Lesser Restoration (short rest)
- Greater Restoration (long rest)
- Freedom of Movement (short rest)
- Heroes' Feast (long rest)
- Remove Curse (long rest)
- Revivify (long rest)
- Mass Healing Word (unlimited)
- Counterspell (short rest, interrupt)

**Note:** This is one of the most complex items with many custom spell variants

---

## Implementation Approach

### Option 1: Copy All 7 Items Together
- **Pros:** Single phase completion, all headgear and gloves done at once
- **Cons:** Medium scope (~64 UUIDs), need to track multiple item types

### Option 2: Copy in Two Batches
- **Batch 1:** Headgear (5 items, ~50 UUIDs)
- **Batch 2:** Gloves (2 items, ~14 UUIDs)
- **Pros:** Smaller batches, easier to test each type separately
- **Cons:** Two testing cycles

**Recommendation:** Option 1 (all together) - 7 items is manageable in a single implementation

---

## Spell Reuse Opportunities

Many items in Phase 39 will reuse spells already in Level13PlusGear:

**Already Available:**
- Misty Step (unlimited) - L13_Target_MistyStep_Unlimited
- Shield (unlimited) - L13_Interrupt_Shield_Unlimited
- Counterspell (unlimited) - L13_Interrupt_Counterspell_Unlimited
- Light (unlimited) - L13_Target_Light_Unlimited
- Spirit Guardians variants - L13_Shout_SpiritGuardians_Moonguard

**Vanilla Spells to Reuse:**
- Speak with Dead, Speak with Animals
- See Invisibility, Protection from Evil and Good
- Faerie Fire, Bless, Create Water
- Lesser/Greater Restoration, Freedom of Movement
- Heroes' Feast, Remove Curse, Revivify
- Mass Healing Word, Superior Healing Word

**May Need Custom Versions:**
- Unlimited or modified cooldown variants of healing spells
- Short rest or long rest variants of restoration spells

---

## Success Criteria

- [ ] All 7 items copied from SampleMagicRingMod
- [ ] All items have L13_ prefix and ed13 UUIDs
- [ ] All custom spells copied and adapted
- [ ] All localization entries created
- [ ] All items added to TreasureTable
- [ ] All RootTemplates created
- [ ] Item catalog updated with all 7 items
- [ ] UUID pool updated (used UUIDs removed)
- [ ] No dependencies on SampleMagicRingMod
- [ ] All items tested in-game
- [ ] Headgear items grant proper immunities and passives
- [ ] Glove items grant proper abilities
- [ ] All items function as intended

---

## Questions for User

Before implementing Phase 39, please confirm:

1. **Prerequisite:** Is Phase 38 complete and tested?
2. **UUID Pool:** Current pool has 91 UUIDs (sufficient for Phase 39's ~64 needed). Confirm ready to proceed?
3. **Approach:** Copy all 7 items together, or split into headgear (5) then gloves (2)?
4. **Priority:** Any specific item to prioritize (Tyr set vs Moonguard set vs Magus Circlet)?

---

## Related Documentation

- **Phase038.md** - Weapons and body armor copy (prerequisite phase)
- **Phase040.md** - Cloaks and shields copy (follow-up phase)
- **Phase041.md** - Ring of the Guardian copy (follow-up phase)
- **docs/instructions/copying_items_between_mods.md** - Item copy workflow
- **docs/instructions/uuid_workflow.md** - UUID pool and naming conventions
- **docs/planning/item_catalog.md** - SampleMagicRingMod source items
- **docs/level13plusgear/item_catalog.md** - Level13PlusGear target catalog

---

## Notes

**Complexity Considerations:**
- Headgear items share many common spells (Speak with Dead, See Invisibility, etc.)
- Tyr variants (Helmet, Circlet, Gloves) share thematic abilities
- Moonguard variants (Helmet, Circlet, Gloves) share similar thematic abilities
- Most accessories are simpler than weapons/armor (fewer custom spells)
- Headgear typically has more immunities and passives than other accessories

**Efficiency Tips:**
- Group Tyr items together for shared spell copying
- Group Moonguard items together for shared spell copying
- Most spells are vanilla or already exist in L13 mod (minimal new spell creation)
- Magus Circlet is simpler and can be done quickly

**After Phase 39:**
With Phase 38 and 39 complete, Level13PlusGear will contain:
- **Weapons:** 7 total (Staff, 3 Longswords, 1 Greatsword, 1 Maul, 1 Mace)
- **Body Armor:** 6 total (Boots + 5 chest armors)
- **Headgear:** 5 total
- **Gloves:** 2 total
- **Rings:** 1 total (Spectral Power)
- **Total Items:** 21 legendary items

**Still To Come:**
- Phase 40: Cloaks (3) + Shields (2) = 5 items
- Phase 41: Ring of the Guardian (1 item)
- **Final Total:** 27 legendary items

This phased approach makes implementation more manageable and allows for thorough testing between phases.

---

## Phase 39 Status: COMPLETE

**Prerequisite:** Phase 38 completed.

**UUID Pool:** Used 23 of 91 available UUIDs. 68 UUIDs remaining.

**Scope:** Phase 39 focused on headgear (5) + gloves (2) = 7 items. Cloaks and shields deferred to Phase 40. Ring of the Guardian deferred to Phase 41.

**Implementation Summary:**
- ✅ Created 7 RootTemplate files
- ✅ Added 7 items to Armor.txt
- ✅ Added 4 custom spells (See Invisibility unlimited, Protection unlimited, Faerie Fire short rest, Thunderwave short rest)
- ✅ Added all items to TreasureTable (L13_Gear_Chest_TT)
- ✅ Added 23 localization entries (7 items × 2 + 2 spell descriptions)
- ✅ Updated item catalog with all 7 items
- ✅ Updated UUID pool (removed 23 used UUIDs)

**Files Modified:**
- Armor.txt - Added 7 entries
- Spell_Shout.txt - Added 1 spell
- Spell_Target.txt - Added 1 spell
- Spell_Zone.txt - Added 2 spells
- TreasureTable.txt - Added 7 items
- Level13PlusGear.loca.xml - Added 16 entries
- uuid_workflow.md - Removed 23 UUIDs
- item_catalog.md - Added 7 items + 4 spells

**Files Created:**
- L13_Helmet_Tyr.lsf.lsx
- L13_Circlet_Tyr.lsf.lsx
- L13_Circlet_Magus.lsf.lsx
- L13_Helmet_Moonguard.lsf.lsx
- L13_Circlet_Moonguard.lsf.lsx
- L13_Gloves_Tyr.lsf.lsx
- L13_Gloves_Moonguard.lsf.lsx

**Next Phase:** Phase 40 - Cloaks and Shields (5 items, ~32 UUIDs needed)
