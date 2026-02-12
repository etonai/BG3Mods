# Phase 41: Copy Ring of the Guardian

**Status:** COMPLETE
**Date:** 2026-02-11

---

## Goals

1. **Copy Ring of the Guardian:** Copy the most complex healing/support ring from SampleMagicRingMod
2. **Implement All Healing Spells:** Ensure all 11+ spells are properly copied and functional
3. **Maintain Independence:** Ensure the ring is fully independent from SampleMagicRingMod
4. **Complete Documentation:** Update item catalog and track all UUID usage

**Prerequisite:** Phase 40 must be completed (cloaks and shields copied)

---

## Phase 41 Item Inventory

This table lists the single item to be copied in Phase 41.

| # | Item | Type | Rarity | Complexity | Est. UUIDs |
|---|------|------|--------|------------|------------|
| **RING (1 item)** |
| 1 | SMR_Ring_Guardian | Ring | Legendary | Very High | ~18-20 |
| **TOTAL** | **1 item** | | | | **~18-20** |

---

## Implementation Strategy

### The Ring of the Guardian

**Description:**
The Ring of the Guardian is one of the most complex items in SampleMagicRingMod, featuring 11+ healing and support spells with various cooldowns and power levels.

**Spell List:**
1. **Superior Healing Word** - 2d20 healing (custom spell)
2. **Bless** - Unlimited
3. **Create Water** - Unlimited
4. **Lesser Restoration** - Short rest
5. **Greater Restoration** - Long rest
6. **Freedom of Movement** - Short rest
7. **Heroes' Feast** - Long rest
8. **Remove Curse** - Long rest
9. **Revivify** - Long rest
10. **Mass Healing Word** - Unlimited
11. **Counterspell** - Short rest (interrupt)

**Complexity Factors:**
- 11 different spells to implement
- Mix of vanilla and custom spell variants
- Multiple cooldown types (unlimited, short rest, long rest)
- Interrupt spell (Counterspell)
- Custom healing spell with non-standard dice (2d20)
- Support role focus (healing, buffing, debuff removal)

**Why Separate Phase:**
- High complexity justifies dedicated focus
- Many custom spell variants needed
- Different from Phase 39 (headgear/gloves) and Phase 40 (cloaks/shields)
- Allows thorough testing of healing/support mechanics
- Reference: Ring of Spectral Power (Phase 37) was similarly complex

---

## Estimated Resource Requirements

### UUID Usage

| Component | Count | UUIDs Needed |
|-----------|-------|--------------|
| RootTemplate | 1 | 1 |
| Item Localization | 2 | 2 (name + description) |
| Custom Spells | 3-5 | 9-15 (spell + localization) |
| **Total** | **1 item** | **~18-20** |

**Breakdown:**
- Superior Healing Word (custom): ~3 UUIDs (spell + 2 localization)
- Possible unlimited variants: ~2-3 spells × 3 UUIDs = 6-9 UUIDs
- RootTemplate + item localization: 3 UUIDs

**Action Required:** ~18-20 UUIDs needed for Phase 41

### File Modifications

**Existing Files to Modify:**
- `Armor.txt` - Add ring entry
- `Spell_Target.txt` - Add custom target healing spells
- `Spell_Shout.txt` - Add custom shout healing spells (if any)
- `Interrupt.txt` - Add Counterspell variant (if custom)
- `TreasureTable.txt` - Add ring to L13_Gear_Chest
- `Level13PlusGear.loca.xml` - Add localization for ring and all custom spells

**New Files to Create:**
- RootTemplate for Ring of the Guardian (1 .lsf.lsx file)

**Potential New Spell Files:**
- Custom Superior Healing Word variant
- Unlimited variants of vanilla healing spells
- Short rest/long rest variants as needed

---

## Spell Implementation Details

### Vanilla Spells to Reuse

These spells likely exist in vanilla BG3 and can be referenced directly:
- Bless
- Create Water
- Lesser Restoration
- Greater Restoration
- Freedom of Movement
- Heroes' Feast
- Remove Curse
- Revivify
- Mass Healing Word
- Counterspell

### Custom Spells Needed

**Superior Healing Word:**
- Likely needs custom implementation
- 2d20 healing (non-standard dice)
- May need custom spell entry or modify existing Healing Word

**Unlimited Variants:**
May need unlimited (no cooldown) variants of:
- Bless (if vanilla has cooldown)
- Create Water (if vanilla has cooldown)
- Mass Healing Word (if vanilla has cooldown)

**Cooldown Variants:**
May need short rest/long rest variants of:
- Lesser Restoration
- Greater Restoration
- Freedom of Movement
- Heroes' Feast
- Remove Curse
- Revivify
- Counterspell

### Reference: Ring of Spectral Power (Phase 37)

Phase 37's Ring of Spectral Power implementation provides a template:
- Used 17 UUIDs total
- 16 custom spell handles
- 1 RootTemplate
- Successfully implemented multiple spell variants

Ring of the Guardian will likely be similar in complexity.

---

## Success Criteria

- [ ] Ring of the Guardian copied from SampleMagicRingMod
- [ ] Ring has L13_ prefix and ed13 UUIDs
- [ ] All 11 spells implemented and functional
- [ ] Superior Healing Word custom spell working (2d20 healing)
- [ ] All cooldowns correct (unlimited, short rest, long rest)
- [ ] Counterspell interrupt functioning
- [ ] All localization entries created
- [ ] Ring added to TreasureTable
- [ ] RootTemplate created
- [ ] Item catalog updated
- [ ] UUID pool updated (used UUIDs removed)
- [ ] No dependencies on SampleMagicRingMod
- [ ] Ring tested in-game
- [ ] All healing spells tested
- [ ] All support spells tested

---

## Testing Plan

### Basic Functionality
1. Ring appears in Tutorial Chest
2. Ring can be equipped
3. Ring displays all 11 spells in tooltip

### Healing Spell Testing
1. Superior Healing Word heals 2d20 HP
2. Mass Healing Word affects multiple targets
3. Lesser/Greater Restoration remove conditions
4. Revivify resurrects fallen allies

### Support Spell Testing
1. Bless grants bonuses
2. Create Water creates water surface
3. Freedom of Movement removes movement restrictions
4. Heroes' Feast grants buffs
5. Remove Curse removes curses

### Cooldown Testing
1. Unlimited spells have no cooldown
2. Short rest spells recharge on short rest
3. Long rest spells recharge on long rest

### Interrupt Testing
1. Counterspell triggers on enemy spellcast
2. Counterspell consumes short rest charge

---

## Questions for User

Before implementing Phase 41, please confirm:

1. **Prerequisite:** Is Phase 40 complete and tested?
2. **UUID Pool:** Are sufficient UUIDs available (~18-20 needed)?
3. **Approach:** Any specific spell to prioritize or test first?
4. **Custom Spells:** Should Superior Healing Word use 2d20 exactly, or can it be adjusted?

---

## Related Documentation

- **Phase037.md** - Ring of Spectral Power copy (similar complexity reference)
- **Phase040.md** - Cloaks and shields copy (prerequisite phase)
- **docs/instructions/copying_items_between_mods.md** - Item copy workflow
- **docs/instructions/uuid_workflow.md** - UUID pool and naming conventions
- **docs/planning/item_catalog.md** - SampleMagicRingMod source items
- **docs/level13plusgear/item_catalog.md** - Level13PlusGear target catalog

---

## Notes

**Complexity Considerations:**
- Ring of the Guardian is the most complex single item in Phase 39-41 split
- 11 different spells require careful implementation
- Mix of vanilla and custom spells
- Multiple cooldown types to manage
- Interrupt mechanics (Counterspell)

**Why This Ring Matters:**
- Completes the healer/support role for Level13PlusGear
- Provides comprehensive healing and support capabilities
- Complements combat-focused items from earlier phases
- Makes Level13PlusGear suitable for support/healer builds

**Efficiency Tips:**
- Copy vanilla spells by reference (don't recreate)
- Only create custom variants when necessary (unlimited, cooldown changes)
- Use Ring of Spectral Power (Phase 37) as implementation template
- Test healing spells incrementally (don't wait until all 11 are implemented)

**After Phase 41:**
With all phases 38-41 complete, Level13PlusGear will contain:
- **Weapons:** 7 total
- **Body Armor:** 6 total
- **Headgear:** 5 total
- **Gloves:** 2 total
- **Cloaks:** 3 total
- **Shields:** 2 total
- **Rings:** 2 total (Spectral Power, Guardian)
- **Total Items:** 27 legendary items

This completes the migration of all useful items from SampleMagicRingMod to Level13PlusGear, making it a comprehensive endgame gear mod fully independent from SampleMagicRingMod.

---

## Phase 41 Status: COMPLETE

**Implementation Date:** 2026-02-11
**Testing Completed:** 2026-02-11

All items and spells have been successfully copied from SampleMagicRingMod to Level13PlusGear with L13 prefixes and custom UUIDs. Ring of the Guardian tested and confirmed working in-game.

---

## Revision 1

**Date:** 2026-02-11
**Issue:** Ring of the Guardian not appearing in L13 chest
**Root Cause:** RootTemplate UUID in Armor.txt had incorrect prefix "hed13..." instead of "ed13..."
**Fix:** Updated Armor.txt line 24 to use correct UUID prefix "ed13348b7-827b-43b8-9d6c-b3cbd88f5ad7"
**Note:** The 'h' prefix is only for localization handles (TranslatedString), not for RootTemplate UUIDs or MapKeys
