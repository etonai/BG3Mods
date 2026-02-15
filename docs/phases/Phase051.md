# Phase 051: Streamline Ring of Creation - Remove Item Summoning Spells

**Status:** COMPLETE
**Date:** 2026-02-14

---

## Goals

1. **Simplify Ring of Creation** - Remove individual armor summoning spells to reduce clutter
2. **Keep Essential Spells** - Retain chest summons, Stormwalker Boots, and Circlet of Willpower
3. **Clean Up Spell Files** - Remove spell definitions that are no longer needed
4. **Update Documentation** - Reflect simplified Ring of Creation functionality

---

## Summary of Changes

| Change | From | To |
|--------|------|-----|
| **Ring of Creation Spells** | 9 summoning spells | 4 summoning spells |
| **Spell_Target.txt** | 9 spell definitions | 4 spell definitions |
| **Functionality** | Summon individual armor + items + chests | Summon chests + key utility items only |

**Result:** Ring of Creation becomes a simpler utility focused on summoning chests and key utility items (Stormwalker Boots, Circlet of Willpower), rather than individual armor pieces.

---

## Current State

### Ring of Creation (ROC_Ring_Creation)

**File:** `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Armor.txt`

**Current Boosts (Line 17):**
```
data "Boosts" "UnlockSpell(ROC_Summon_L13_Chest);UnlockSpell(ROC_Summon_Boots_Stormwalker);UnlockSpell(ROC_Summon_Plate_Moonguard);UnlockSpell(ROC_Summon_Armor_Tyr);UnlockSpell(ROC_Summon_Armor_Moonguard);UnlockSpell(ROC_Summon_Armor_Dragonrider);UnlockSpell(ROC_Summon_Circlet_Willpower);UnlockSpell(ROC_Summon_Armor_Testing);UnlockSpell(ROC_Summon_L13_Armor_Chest)"
```

**Current Spells:**
1. ROC_Summon_L13_Chest - **KEEP** (summons L13 gear chest)
2. ROC_Summon_Boots_Stormwalker - **KEEP** (summons Stormwalker Boots)
3. ROC_Summon_Plate_Moonguard - **REMOVE**
4. ROC_Summon_Armor_Tyr - **REMOVE**
5. ROC_Summon_Armor_Moonguard - **REMOVE**
6. ROC_Summon_Armor_Dragonrider - **REMOVE**
7. ROC_Summon_Circlet_Willpower - **KEEP** (summons Circlet of Willpower)
8. ROC_Summon_Armor_Testing - **REMOVE**
9. ROC_Summon_L13_Armor_Chest - **KEEP** (summons L13 armor chest)

**Problem:** Too many individual armor summoning spells clutter the Ring of Creation's spell list. Users can summon chests to get armor pieces, making individual armor summons redundant.

---

## Target State

### Ring of Creation (Simplified)

**New Boosts:**
```
data "Boosts" "UnlockSpell(ROC_Summon_L13_Chest);UnlockSpell(ROC_Summon_Boots_Stormwalker);UnlockSpell(ROC_Summon_Circlet_Willpower);UnlockSpell(ROC_Summon_L13_Armor_Chest)"
```

**Retained Spells:**
1. ROC_Summon_L13_Chest - Summons L13 gear chest (main item container)
2. ROC_Summon_Boots_Stormwalker - Summons Stormwalker Boots (utility item)
3. ROC_Summon_Circlet_Willpower - Summons Circlet of Willpower (utility headgear)
4. ROC_Summon_L13_Armor_Chest - Summons L13 armor chest (armor container)

**Removed Spells:**
- ROC_Summon_Plate_Moonguard
- ROC_Summon_Armor_Tyr
- ROC_Summon_Armor_Moonguard
- ROC_Summon_Armor_Dragonrider
- ROC_Summon_Armor_Testing

**Result:** Cleaner, more focused Ring of Creation that serves its core purpose: summoning item chests and key utility items (Stormwalker Boots, Circlet of Willpower).

---

## Rationale

### Why Keep These Spells?

**ROC_Summon_L13_Chest:**
- Primary function of Ring of Creation
- Summons container with all L13 gear items
- Essential for mod functionality

**ROC_Summon_L13_Armor_Chest:**
- Secondary container for armor items
- Complements main gear chest
- Provides organized access to armor pieces

**ROC_Summon_Boots_Stormwalker:**
- Unique utility item with movement benefits
- Frequently needed item that benefits from quick summoning
- Different use case than armor/weapons in chests

**ROC_Summon_Circlet_Willpower:**
- Powerful utility headgear with mental ability benefits
- Frequently swapped item that benefits from quick summoning
- Not available in chests, requires individual summon

### Why Remove Individual Armor Summons?

**Redundancy:**
- All individual armor pieces can be obtained from the armor chest
- No benefit to summoning individual armor vs opening chest

**Clutter:**
- 5 individual armor summons create a crowded spell list
- Makes it harder to find the useful spells (chest summons, utility items)

**Simplicity:**
- Ring of Creation should be simple and focused
- Core purpose is summoning chests and key utility items, not individual armor pieces

---

## Implementation Plan

### Task 1: Update Ring of Creation Stats

**Description:** Remove individual armor summoning spells from Ring of Creation's Boosts

**Steps:**
1. Open `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Armor.txt`
2. Locate ROC_Ring_Creation entry (line 12-18)
3. Update Boosts to only include four spells (chests + Stormwalker + Circlet)
4. Save file

**Files to modify:**
- `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Armor.txt` - Update Boosts line

### Task 2: Clean Up Spell Definitions

**Description:** Remove spell definitions for armor pieces that are no longer summoned

**Steps:**
1. Open `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Spell_Target.txt`
2. Remove spell blocks for individual armor pieces
3. Keep chest summons, Stormwalker Boots, and Circlet of Willpower spells
4. Save file

**Files to modify:**
- `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Spell_Target.txt` - Remove spell entries

### Task 3: Update Version

**Description:** Increment mod version for new build

**Steps:**
1. Open `RingOfCreation/Mods/RingOfCreation/meta.lsx`
2. Increment Version64
3. Save file

**Files to modify:**
- `RingOfCreation/Mods/RingOfCreation/meta.lsx` - Increment version

---

## Detailed Implementation

### Step 1: Update ROC_Ring_Creation Boosts

**File:** `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Armor.txt`

**Current (Line 17):**
```
data "Boosts" "UnlockSpell(ROC_Summon_L13_Chest);UnlockSpell(ROC_Summon_Boots_Stormwalker);UnlockSpell(ROC_Summon_Plate_Moonguard);UnlockSpell(ROC_Summon_Armor_Tyr);UnlockSpell(ROC_Summon_Armor_Moonguard);UnlockSpell(ROC_Summon_Armor_Dragonrider);UnlockSpell(ROC_Summon_Circlet_Willpower);UnlockSpell(ROC_Summon_Armor_Testing);UnlockSpell(ROC_Summon_L13_Armor_Chest)"
```

**New:**
```
data "Boosts" "UnlockSpell(ROC_Summon_L13_Chest);UnlockSpell(ROC_Summon_Boots_Stormwalker);UnlockSpell(ROC_Summon_Circlet_Willpower);UnlockSpell(ROC_Summon_L13_Armor_Chest)"
```

**Purpose:** Remove 5 individual armor summons, keeping only the 4 essential spells (chests + key utility items)

### Step 2: Remove Individual Armor Spell Definitions

**File:** `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Spell_Target.txt`

**Remove these spell blocks:**
- Lines 49-71: ROC_Summon_Plate_Moonguard
- Lines 73-95: ROC_Summon_Armor_Tyr
- Lines 97-119: ROC_Summon_Armor_Moonguard
- Lines 120-142: ROC_Summon_Armor_Dragonrider
- Lines 168-190: ROC_Summon_Armor_Testing

**Keep these spell blocks:**
- Lines 1-23: ROC_Summon_L13_Chest
- Lines 25-47: ROC_Summon_Boots_Stormwalker
- Lines 144-166: ROC_Summon_Circlet_Willpower
- Lines 192-214: ROC_Summon_L13_Armor_Chest

**Purpose:** Clean up file by removing unused armor summon spell definitions, reducing file size and maintaining only active spells

### Step 3: Increment Version

**File:** `RingOfCreation/Mods/RingOfCreation/meta.lsx`

Increment Version64 value for new mod build.

**Purpose:** Track mod version for release management

---

## Files to Modify

| File | Action | Description |
|------|--------|-------------|
| `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Armor.txt` | Edit | Remove 5 UnlockSpell entries from ROC_Ring_Creation Boosts (keep 4 spells) |
| `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Spell_Target.txt` | Edit | Remove 5 spell definition blocks for individual armor pieces |
| `RingOfCreation/Mods/RingOfCreation/meta.lsx` | Edit | Increment version number |

---

## UUID/Handle Requirements

**None** - This phase only removes existing functionality, no new UUIDs or handles needed.

---

## Testing Plan

### Test 1: Ring of Creation Spell List

1. Load save with Ring of Creation equipped
2. Open character sheet and check spells
3. **Verify:** Only 4 summoning spells appear:
   - Summon L13 Chest
   - Summon Stormwalker Boots
   - Summon Circlet of Willpower
   - Summon L13 Armor Chest
4. **Verify:** Individual armor summons no longer appear:
   - No Summon Plate of Moonguard
   - No Summon Armor of Tyr
   - No Summon Armor of Moonguard
   - No Summon Dragonrider Armor
   - No Summon Testing Armor

### Test 2: Chest Summoning Functionality

1. Use "Summon L13 Chest" spell
2. **Verify:** L13 gear chest appears
3. **Verify:** Chest contains all expected items
4. **Verify:** Items can be taken from chest normally
5. Use "Summon L13 Armor Chest" spell
6. **Verify:** L13 armor chest appears
7. **Verify:** Armor chest contains expected armor pieces

### Test 3: Stormwalker Boots Summoning

1. Use "Summon Stormwalker Boots" spell
2. **Verify:** Stormwalker Boots appear on ground
3. **Verify:** Boots can be picked up and equipped
4. **Verify:** Boots function normally with all powers

### Test 4: Circlet of Willpower Summoning

1. Use "Summon Circlet of Willpower" spell
2. **Verify:** Circlet of Willpower appears on ground
3. **Verify:** Circlet can be picked up and equipped
4. **Verify:** Circlet functions normally with all powers

### Test 5: Ring of Creation Acquisition

1. Start new game or load early save without Ring of Creation
2. Obtain Ring of Creation (console command or mod delivery method)
3. **Verify:** Ring equips normally
4. **Verify:** Only 4 summoning spells are granted
5. **Verify:** No individual armor summons appear

---

## Success Criteria

- [ ] Ring of Creation Boosts updated to only include 4 spells
- [ ] Spell_Target.txt cleaned up with 5 armor spell blocks removed
- [ ] Only 4 summoning spells appear on Ring of Creation:
  - ROC_Summon_L13_Chest
  - ROC_Summon_Boots_Stormwalker
  - ROC_Summon_Circlet_Willpower
  - ROC_Summon_L13_Armor_Chest
- [ ] All 4 retained spells function correctly
- [ ] No individual armor summons appear in spell list
- [ ] Chests summon correctly with all items
- [ ] Stormwalker Boots summon correctly
- [ ] Circlet of Willpower summons correctly
- [ ] Version incremented correctly
- [ ] Testing completed and verified
- [ ] Documentation updated if needed

---

## Technical Notes

### File Cleanup Benefits

**Reduced File Size:**
- Spell_Target.txt: ~140 lines → ~90 lines (removing 5 armor spell blocks)
- Cleaner, more maintainable code

**Improved Performance:**
- Fewer spells to load and process
- Cleaner spell list UI for players

**Better User Experience:**
- Easier to find the spells that matter
- Less clutter in spellbook
- Clear, focused functionality

### Backward Compatibility

**No Breaking Changes:**
- Existing saves with Ring of Creation will continue to work
- Players who previously had individual armor summons will simply see fewer spells
- No items are removed, just the individual armor summon spells
- All armor pieces remain accessible via armor chest
- Key utility items (Stormwalker Boots, Circlet of Willpower) still individually summonable

---

## Dependencies

**This phase depends on:**
- RingOfCreation mod (existing)
- Level13PlusGear mod (for summoned items)

**This phase affects:**
- Ring of Creation functionality
- Player spell lists when Ring of Creation is equipped
- Ring of Creation mod file structure

---

## Related Documentation

- **CLAUDE.md** - Active mods and project structure
- **Ring of Creation implementation phases** - Original creation of summoning system
- **Level13PlusGear phases** - Items that are summoned via chests

---

## Notes

- This is a cleanup/simplification phase, not new functionality
- Low risk - only removing features, not adding new ones
- Improves usability by reducing clutter
- Maintains core functionality (chest summoning + key utility items)
- Stormwalker Boots retained due to unique movement utility use case
- Circlet of Willpower retained due to frequent swapping and not being in chests
- No localization changes needed (removing spells, not changing text)

---

## Phase 051 Status: COMPLETE

Ring of Creation streamlining has been completed and tested.

**Completed Changes:**
- ✅ Removed 5 individual armor summoning spells from ROC_Ring_Creation Boosts
- ✅ Kept 4 essential spells (chests + Stormwalker Boots + Circlet of Willpower)
- ✅ Cleaned up Spell_Target.txt file (reduced from ~216 lines to ~97 lines)
- ✅ Incremented Version64 from 36028900098179075 to 36028900098179076
- ✅ Simplified Ring of Creation functionality
- ✅ User tested and confirmed working

**Implementation Notes:**
- All 5 armor spell definitions successfully removed from Spell_Target.txt
- Ring of Creation now only grants 4 spells instead of 9
- File size significantly reduced for cleaner code
- All 4 retained spells function correctly in-game
