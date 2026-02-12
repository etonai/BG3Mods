# Phase 40: Copy Cloaks and Shields

**Status:** COMPLETE
**Date:** 2026-02-11

---

## Goals

1. **Copy Cloaks:** Copy 3 cloak items (Cloak of Tyr, Cloak of the Rogue, Moonguard Cloak)
2. **Copy Shields:** Copy 2 shield items (Shield of Tyr, Moonguard Shield)
3. **Maintain Independence:** Ensure all copied items are fully independent from SampleMagicRingMod
4. **Complete Documentation:** Update item catalog and track all UUID usage

**Prerequisite:** Phase 39 must be completed (headgear and gloves copied)

---

## Phase 40 Item Inventory

This table lists all 5 items to be copied in Phase 40.

| # | Item | Type | Rarity | Complexity | Est. UUIDs |
|---|------|------|--------|------------|------------|
| **CLOAKS (3 items)** |
| 1 | SMR_Cloak_Tyr | Cloak | Legendary | Low-Medium | ~6 |
| 2 | SMR_Cloak_Rogue | Cloak | Legendary | Low | ~4 |
| 3 | SMR_Cloak_Moonguard | Cloak | Legendary | Medium | ~8 |
| **SHIELDS (2 items)** |
| 4 | SMR_Shield_Tyr | Shield +2 | Legendary | Low-Medium | ~6 |
| 5 | SMR_Shield_Moonguard | Shield +2 | Legendary | Medium | ~8 |
| **TOTAL** | **5 items** | | | | **~32** |

---

## Implementation Strategy

### Group 1: Cloaks (3 items, ~18 UUIDs)

**Tyr Set:**
- **Cloak of Tyr:** Defensive cloak with Tyr theme
- **Reason:** Part of Tyr equipment set, shares thematic abilities

**Rogue Set:**
- **Cloak of the Rogue:** Stealth/mobility focused
- **Reason:** Part of Rogue equipment set, simpler implementation

**Moonguard Set:**
- **Moonguard Cloak:** Defensive cloak with Moonguard theme
- **Reason:** Part of Moonguard equipment set, shares thematic abilities

### Group 2: Shields (2 items, ~14 UUIDs)

**Tyr Set:**
- **Shield of Tyr:** +2 shield with defensive abilities
- **Reason:** Completes Tyr equipment set

**Moonguard Set:**
- **Moonguard Shield:** +2 shield with Moonguard-themed abilities
- **Reason:** Completes Moonguard equipment set

---

## Estimated Resource Requirements

### UUID Usage

| Item Category | Count | UUIDs per Item | Total UUIDs |
|---------------|-------|----------------|-------------|
| Cloaks | 3 | 6 | 18 |
| Shields | 2 | 7 | 14 |
| **Total** | **5** | **Avg: 6.4** | **~32** |

**Action Required:** ~32 UUIDs needed for Phase 40

### File Modifications

**Existing Files to Modify:**
- `Armor.txt` - Add all cloaks and shields
- `Spell_Target.txt` - Add custom target spells (if any new ones)
- `Spell_Shout.txt` - Add custom shout spells (if any new ones)
- `TreasureTable.txt` - Add all items to L13_Gear_Chest
- `Level13PlusGear.loca.xml` - Add localization for items and custom spells

**New Files to Create:**
- RootTemplates for all 5 items (5 .lsf.lsx files)

**Potential New Spell Files:**
- Most spells will likely reuse existing vanilla spells or spells already in L13 mod

---

## Item Details Preview

### Cloak Abilities

**Cloak of Tyr:**
- Defensive abilities with Tyr theme
- Likely includes resistances or protective bonuses

**Cloak of the Rogue:**
- Stealth/mobility focused
- Likely includes stealth bonuses, movement abilities

**Moonguard Cloak:**
- Defensive abilities with Moonguard theme
- May include resistances or protective bonuses

### Shield Abilities

**Shield of Tyr:**
- +2 shield
- Defensive abilities with Tyr theme
- Likely includes AC bonuses, blocking abilities

**Moonguard Shield:**
- +2 shield
- Defensive abilities with Moonguard theme
- Likely includes AC bonuses, protective abilities

---

## Spell Reuse Opportunities

Many items in Phase 40 will reuse spells already in Level13PlusGear:

**Already Available:**
- Misty Step (unlimited) - L13_Target_MistyStep_Unlimited
- Shield (unlimited) - L13_Interrupt_Shield_Unlimited
- Counterspell (unlimited) - L13_Interrupt_Counterspell_Unlimited

**Vanilla Spells to Reuse:**
- Various defensive and utility spells from vanilla BG3

**May Need Custom Versions:**
- Unlimited or modified cooldown variants
- Set-specific themed abilities

---

## Success Criteria

- [ ] All 5 items copied from SampleMagicRingMod
- [ ] All items have L13_ prefix and ed13 UUIDs
- [ ] All custom spells copied and adapted
- [ ] All localization entries created
- [ ] All items added to TreasureTable
- [ ] All RootTemplates created
- [ ] Item catalog updated with all 5 items
- [ ] UUID pool updated (used UUIDs removed)
- [ ] No dependencies on SampleMagicRingMod
- [ ] All items tested in-game
- [ ] Cloak items grant proper abilities
- [ ] Shield items function correctly

---

## Questions for User

Before implementing Phase 40, please confirm:

1. **Prerequisite:** Is Phase 39 complete and tested?
2. **UUID Pool:** Are sufficient UUIDs available (~32 needed)?
3. **Approach:** Copy all 5 items together, or split cloaks and shields?
4. **Priority:** Any specific item to prioritize (cloaks vs shields)?

---

## Related Documentation

- **Phase039.md** - Headgear and gloves copy (prerequisite phase)
- **Phase041.md** - Ring of the Guardian copy (follow-up phase)
- **docs/instructions/copying_items_between_mods.md** - Item copy workflow
- **docs/instructions/uuid_workflow.md** - UUID pool and naming conventions
- **docs/planning/item_catalog.md** - SampleMagicRingMod source items
- **docs/level13plusgear/item_catalog.md** - Level13PlusGear target catalog

---

## Notes

**Complexity Considerations:**
- Cloaks and shields are generally simpler than headgear (fewer custom spells/passives)
- Tyr variants share thematic abilities with other Tyr set pieces
- Moonguard variants share thematic abilities with other Moonguard set pieces
- Most spells are vanilla or already exist in L13 mod (minimal new spell creation)

**Efficiency Tips:**
- Group Tyr items together for shared spell copying
- Group Moonguard items together for shared spell copying
- Most spells are vanilla or already exist in L13 mod
- Simpler implementation than headgear or rings

**After Phase 40:**
With Phases 38, 39, and 40 complete, Level13PlusGear will contain:
- **Weapons:** 7 total
- **Body Armor:** 6 total
- **Headgear:** 5 total
- **Gloves:** 2 total
- **Cloaks:** 3 total
- **Shields:** 2 total
- **Rings:** 1 total (Spectral Power)
- **Total Items:** 26 legendary items (before Ring of the Guardian in Phase 41)

---

## Phase 40 Status: PENDING

**Prerequisite:** Phase 39 must be completed first.

**Awaiting user decision on UUID availability and implementation approach.**
