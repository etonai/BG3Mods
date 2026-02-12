# Phase 39: Copy Headgear, Accessories, and Ring of the Guardian

**Status:** PENDING
**Date:** 2026-02-11

---

## Goals

1. **Copy Headgear:** Copy 5 headgear items (Helmet of Tyr, Circlet of Tyr, Magus Circlet, Moonguard Helm, Moonguard Circlet)
2. **Copy Gloves:** Copy 2 glove items (Gloves of Tyr, Moonguard Gloves)
3. **Copy Cloaks:** Copy 3 cloak items (Cloak of Tyr, Cloak of the Rogue, Moonguard Cloak)
4. **Copy Shields:** Copy 2 shield items (Shield of Tyr, Moonguard Shield)
5. **Copy Ring of the Guardian:** Copy the powerful healing/support ring
6. **Maintain Independence:** Ensure all copied items are fully independent from SampleMagicRingMod
7. **Complete Documentation:** Update item catalog and track all UUID usage

**Prerequisite:** Phase 38 must be completed (weapons and body armor copied)

---

## Phase 39 Item Inventory

This table lists all 13 items to be copied in Phase 39.

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
| **CLOAKS (3 items)** |
| 8 | SMR_Cloak_Tyr | Cloak | Legendary | Low-Medium | ~6 |
| 9 | SMR_Cloak_Rogue | Cloak | Legendary | Low | ~4 |
| 10 | SMR_Cloak_Moonguard | Cloak | Legendary | Medium | ~8 |
| **SHIELDS (2 items)** |
| 11 | SMR_Shield_Tyr | Shield +2 | Legendary | Low-Medium | ~6 |
| 12 | SMR_Shield_Moonguard | Shield +2 | Legendary | Medium | ~8 |
| **RINGS (1 item)** |
| 13 | SMR_Ring_Guardian | Ring | Legendary | High | ~18 |
| **TOTAL** | **13 items** | | | | **~110** |

---

## Implementation Strategy

### Group 1: Headgear (5 items, ~50 UUIDs)

**Tyr Set (3 items):**
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

### Group 3: Cloaks (3 items, ~18 UUIDs)

- **Cloak of Tyr:** Defensive cloak with Tyr theme
- **Cloak of the Rogue:** Stealth/mobility focused
- **Moonguard Cloak:** Defensive cloak with Moonguard theme

### Group 4: Shields (2 items, ~14 UUIDs)

- **Shield of Tyr:** +2 shield with defensive abilities
- **Moonguard Shield:** +2 shield with Moonguard-themed abilities

### Group 5: Ring of the Guardian (1 item, ~18 UUIDs)

- **Ring of the Guardian:** Complex ring with 10+ healing and support spells
- **Reason:** Separated due to high complexity (many custom healing spells)
- **Spells:** Superior Healing Word, Bless, Create Water, Lesser Restoration, Greater Restoration, Freedom of Movement, Heroes' Feast, Remove Curse, Revivify, Mass Healing Word, Counterspell

---

## Estimated Resource Requirements

### UUID Usage by Group

| Group | Items | UUIDs per Item | Total UUIDs |
|-------|-------|----------------|-------------|
| Headgear | 5 | 10 | 50 |
| Gloves | 2 | 7 | 14 |
| Cloaks | 3 | 6 | 18 |
| Shields | 2 | 7 | 14 |
| Ring of the Guardian | 1 | 18 | 18 |
| **Total** | **13** | **Avg: 8.8** | **~114** |

**Current UUID Pool (after Phase 38):** Will depend on Phase 38 usage

**Action Required:** Generate ~100-120 additional UUIDs for Phase 39

### File Modifications

**Existing Files to Modify:**
- `Armor.txt` - Add all headgear, gloves, cloaks, shields, and ring
- `Spell_Target.txt` - Add custom target spells (if any new ones)
- `Spell_Shout.txt` - Add custom shout spells (if any new ones)
- `TreasureTable.txt` - Add all items to L13_Gear_Chest
- `Level13PlusGear.loca.xml` - Add localization for items and custom spells
- `Interrupt.txt` - May need for any custom interrupts

**New Files to Create:**
- RootTemplates for all 13 items (13 .lsf.lsx files)

**Potential New Spell Files:**
- Most spells will likely reuse existing vanilla spells or spells already in L13 mod
- Ring of the Guardian may need several custom spell variants for healing spells

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

### Option 1: Copy All 13 Items Together
- **Pros:** Single phase completion, all accessories done at once
- **Cons:** Large scope (~114 UUIDs), harder to track, longer testing cycle

### Option 2: Copy in Two Batches
- **Batch 1:** Headgear + Gloves + Cloaks + Shields (12 items, ~96 UUIDs)
- **Batch 2:** Ring of the Guardian (1 item, ~18 UUIDs)
- **Pros:** Separate complex ring from simpler accessories, manageable batches
- **Cons:** Two testing cycles

### Option 3: Copy by Group (5 groups)
- **Group 1:** Headgear (5 items)
- **Group 2:** Gloves (2 items)
- **Group 3:** Cloaks (3 items)
- **Group 4:** Shields (2 items)
- **Group 5:** Ring of the Guardian (1 item)
- **Pros:** Very granular, easy to test each type
- **Cons:** Many small implementations, more overhead

**Recommendation:** Option 1 (all together) or Option 2 (accessories + ring separately)

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

- [ ] All 13 items copied from SampleMagicRingMod
- [ ] All items have L13_ prefix and ed13 UUIDs
- [ ] All custom spells copied and adapted
- [ ] All localization entries created
- [ ] All items added to TreasureTable
- [ ] All RootTemplates created
- [ ] Item catalog updated with all 13 items
- [ ] UUID pool updated (used UUIDs removed)
- [ ] No dependencies on SampleMagicRingMod
- [ ] All items tested in-game
- [ ] Headgear items grant proper immunities and passives
- [ ] Ring of the Guardian healing spells work correctly
- [ ] All accessory items function as intended

---

## Questions for User

Before implementing Phase 39, please confirm:

1. **Prerequisite:** Is Phase 38 complete and tested?
2. **UUID Generation:** Can you generate ~100-120 additional UUIDs for the UUID pool?
3. **Approach:** Copy all 13 items together, or split into accessories (12) + ring (1)?
4. **Priority:** Any specific item category to prioritize (headgear, gloves, cloaks, shields, ring)?

---

## Related Documentation

- **Phase038.md** - Weapons and body armor copy (prerequisite phase)
- **Phase037.md** - Ring of Spectral Power copy (complex ring reference)
- **docs/instructions/copying_items_between_mods.md** - Item copy workflow
- **docs/instructions/uuid_workflow.md** - UUID pool and naming conventions
- **docs/planning/item_catalog.md** - SampleMagicRingMod source items
- **docs/level13plusgear/item_catalog.md** - Level13PlusGear target catalog

---

## Notes

**Complexity Considerations:**
- Headgear items share many common spells (Speak with Dead, See Invisibility, etc.)
- Tyr variants (Helmet, Circlet, Gloves, Cloak, Shield) share thematic abilities
- Moonguard variants share similar thematic abilities
- Most accessories are simpler than weapons/armor (fewer custom spells)
- Ring of the Guardian is the most complex item in Phase 39 due to many healing spells

**Efficiency Tips:**
- Group Tyr items together for shared spell copying
- Group Moonguard items together for shared spell copying
- Most spells are vanilla or already exist in L13 mod (minimal new spell creation)
- Ring of the Guardian may need dedicated focus due to complexity

**After Phase 39:**
With Phase 38 and 39 complete, Level13PlusGear will contain:
- **Weapons:** 7 total (Staff, 3 Longswords, 1 Greatsword, 1 Maul, 1 Mace)
- **Body Armor:** 6 total (Boots + 5 chest armors)
- **Headgear:** 5 total
- **Gloves:** 2 total
- **Cloaks:** 3 total
- **Shields:** 2 total
- **Rings:** 2 total (Spectral Power, Guardian)
- **Total Items:** 27 legendary items

This will make Level13PlusGear a comprehensive endgame gear mod independent from SampleMagicRingMod.

---

## Phase 39 Status: PENDING

**Prerequisite:** Phase 38 must be completed first.

**Awaiting user decision on UUID generation and implementation approach.**
