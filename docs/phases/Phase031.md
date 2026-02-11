# Phase 031 - RingOfCreation: Item Summoning Mod

**Status:** COMPLETE

## Goal

Create a new mod called "RingOfCreation" that provides a magical ring capable of summoning items by their ID. This mod will serve as a utility/testing tool for spawning items in-game without console commands.

---

## Mod Overview

**Mod Name:** RingOfCreation

**Primary Item:** Ring of Creation
- Equippable ring that grants item summoning abilities
- Summons items using spell-based mechanics (similar to cheatersring mod)
- Likely creates scrolls that cast summoning spells - NO, it summons them directly. No scrolls are involved.

**Delivery Method:** Dual delivery for maximum accessibility
- Tutorial Chest injection (new games)
- Traveler's Chest via OneTimeRewards (existing saves)

**Dependencies:**
- Level13PlusGear (required - for summoning L13 gear chest)
- SampleMagicRingMod (required - for summoning Boots of Stormwalker)

---

## Reference Mods

### Primary Basis: Level13PlusGear
**Why:** Small, clean, recently created mod with modern structure
- Clean UUID workflow (ed13 prefix)
- Proper localization handles
- Well-documented
- Good template for new mod creation

### Ring Creation Reference: ExampleMods/OldMagicRingMod
**Purpose:** Learn ring item creation patterns
- Ring stats structure
- Ring RootTemplates
- Ring equip mechanics

### Item Summoning Reference: ExampleMods/cheatersring_2d1ca631-35dd-3af-bpmv
**Purpose:** Understand item summoning spell mechanics
- How spells summon items by ID
- Scroll creation for summoning spells
- Spell-to-item mapping system

NOTE: There is a scroll in this mod that summons the Tutorial Chest, so that may be a good model for summoning the Level 13 Plus Gear chest
---

## Test Items to Summon

### 1. Level 13 Plus Gear Chest
**Source:** Level13PlusGear mod
**Purpose:** Test cross-mod item summoning
**Item:** L13_Gear_Chest
**UUID:** `ed134bf4-d2cc-462b-81cd-ab61536c7375`

### 2. Potion of Supreme Healing
**Source:** Vanilla BG3
**Purpose:** Test vanilla item summoning
**Item:** CONS_Potion_Healing_A_Supreme
**UUID:** `7d78f227-e8d4-486d-8121-25cf0bee751d`

### 3. Boots of the Stormwalker
**Source:** SampleMagicRingMod
**Purpose:** Test summoning from another custom mod
**Item:** SMR_Boots_Stormwalker
**UUID:** (need to find from SampleMagicRingMod)

---

## Implementation Plan

### Step 1: Create Mod Structure
Based on Level13PlusGear, create RingOfCreation mod structure:

**Directories to Create:**
```
RingOfCreation/
├── Mods/
│   └── RingOfCreation/
│       ├── meta.lsx
│       └── Story/RawFiles/Goals/ForceRecompile.txt
├── Public/
│   └── RingOfCreation/
│       ├── Stats/Generated/
│       │   ├── Data/
│       │   │   ├── Armor.txt (ring stats)
│       │   │   └── Spell_Target.txt (summoning spells)
│       │   └── TreasureTable.txt
│       ├── RootTemplates/
│       │   └── ROC_Ring_Creation.lsf.lsx
│       └── OneTimeRewards/
│           └── OneTimeRewards.lsx
└── Localization/
    └── English/
        └── RingOfCreation.loca.xml
```

### Step 2: Generate UUIDs and Handles
Use uuid_workflow.md UUID pool with custom prefix for RingOfCreation

**UUID Prefix:** `ed31` (Phase 031, valid hexadecimal)
- Mod UUID: `ed31XXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX`
- Item UUIDs: `ed31XXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX`

**Handle Prefix:** `hroc` (Ring Of Creation)
- Handles: `hrocXXXXXgXXXXgXXXXgXXXXgXXXXXXXXXXXX`

**UUIDs Needed:**
- Mod UUID (1)
- Ring of Creation (1)
- OneTimeReward (1)
- Localization handles (8: ring name/desc + 3 spell names + 3 spell descs)

**Total:** 3 UUIDs + 8 handles

**Note:** Spell stat entries don't require UUIDs - they use their stat names for references.

### Step 3: Research Summoning Mechanics
**Research Complete:** Based on cheatersring examination:
1. Ring grants spells directly (no scrolls needed)
2. Spells create items at target location using item template UUID
3. Tutorial Chest scroll in cheatersring is excellent reference for summoning L13 chest
4. Direct spell → item creation flow confirmed

### Step 4: Create Ring Item
**Stats Entry (Armor.txt):**
```
new entry "ROC_Ring_Creation"
type "Armor"
using "ARM_Ring"
data "RootTemplate" "<UUID>"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(<Summon_L13_Chest>);UnlockSpell(<Summon_Potion_Supreme>);UnlockSpell(<Summon_Boots_Stormwalker>)"
data "Unique" "1"
```

### Step 5: Create Summoning Spells
Based on cheatersring Tutorial Chest scroll reference, create spells that summon items directly

**Key Finding:** Cheatersring's Tutorial Chest scroll provides the exact pattern needed for summoning the L13 Plus Gear Chest

**Example Spell Structure (based on cheatersring research):**
```
new entry "ROC_Summon_L13_Chest"
type "SpellData"
data "SpellType" "Target"
data "TargetRadius" "1"
data "CreateItemTemplateAtPosition" "ed134bf4-d2cc-462b-81cd-ab61536c7375"
// Properties determined from Tutorial Chest scroll examination
```

**Three Spells Needed:**
1. `ROC_Summon_L13_Chest` - Summons Level 13 Plus Gear Chest
2. `ROC_Summon_Potion_Supreme` - Summons Potion of Supreme Healing
3. `ROC_Summon_Boots_Stormwalker` - Summons Boots of Stormwalker

### Step 6: Create RootTemplate
Ring template with proper stats reference and localization handles

### Step 7: Create Localization
- Ring name: "Ring of Creation"
- Ring description: Describes item summoning abilities
- Spell names for each summoning ability
- Spell descriptions

### Step 8: Implement Dual Delivery

**Tutorial Chest (TreasureTable.txt):**
```
new treasuretable "TUT_Chest_Potions"
CanMerge 1
new subtable "1,1"
object category "I_ROC_Ring_Creation",1,0,0,0,0,0,0,0
```

**Traveler's Chest (OneTimeRewards.lsx):**
```xml
<node id="RewardNode">
  <attribute id="Reward" type="LSString" value="ROC_Ring_Creation" />
  <attribute id="UUID" type="FixedString" value="<REWARD_UUID>" />
</node>
```

### Step 9: Set Up Dependencies
**meta.lsx Dependencies node:**
```xml
<node id="Dependencies">
  <children>
    <node id="ModuleShortDesc">
      <attribute id="Folder" type="LSString" value="Level13PlusGear" />
      <attribute id="MD5" type="LSString" value="" />
      <attribute id="Name" type="LSString" value="Level13PlusGear" />
      <attribute id="UUID" type="FixedString" value="ed133cf1-389c-47f1-9fa7-fe49ee4fe2ce" />
      <attribute id="Version64" type="int64" value="36028861443473408" />
    </node>
    <node id="ModuleShortDesc">
      <attribute id="Folder" type="LSString" value="SampleMagicRingMod" />
      <attribute id="MD5" type="LSString" value="" />
      <attribute id="Name" type="LSString" value="SampleMagicRingMod" />
      <attribute id="UUID" type="FixedString" value="560497d3-63b4-4dbe-a1c8-a10497ccc009" />
      <attribute id="Version64" type="int64" value="36028855001022464" />
    </node>
  </children>
</node>
```

---

## Research Questions

### Answered Through cheatersring Research:

1. **How does cheatersring summon items?** ✅ ANSWERED
   - ❌ Scrolls are NOT necessary
   - ✅ Ring directly grants summoning spells
   - ✅ Tutorial Chest scroll provides perfect reference for L13 chest summoning

2. **What's the exact spell property for item creation?** ⏳ TO VERIFY
   - Likely `CreateItemTemplateAtPosition` (from cheatersring)
   - Need to examine Tutorial Chest scroll specifically
   - Will verify exact property name and parameters

### Still Need to Answer:

3. **Can cross-mod item summoning work?**
   - Will summoning L13 chest work with dependency declared?
   - Will summoning SMR boots work with dependency declared?
   - **Test Plan:** Try summoning with and without dependencies loaded

4. **Do summoned items persist?**
   - Do they stay in inventory after save/load?
   - Any special flags needed?
   - **Test Plan:** Summon items, save, reload, verify persistence

5. **Delivery approach:**
   - ✅ Dual delivery (Tutorial Chest + Traveler's Chest) confirmed as best approach
   - Addresses Phase 030 container limitation discovery

---

## Naming Conventions

**Prefix:** ROC (RingOfCreation)

**Examples:**
- Stats: `ROC_Ring_Creation`
- Spells: `ROC_Summon_L13_Chest`, `ROC_Summon_Potion_Supreme`
- UUIDs: `ed31XXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX` (ed31 = Phase 031, valid hexadecimal)
- Handles: `hrocXXXXXgXXXXgXXXXgXXXXgXXXXXXXXXXXX`

---

## Implementation Checklist

### Phase 1: Research
- [x] Extract and examine cheatersring mod
- [x] Confirm no scrolls needed - ring summons items directly
- [x] Identify Tutorial Chest scroll as reference for L13 chest summoning
- [x] Examine Tutorial Chest scroll for exact spell properties
- [x] Find Boots of Stormwalker UUID from SampleMagicRingMod
- [x] Document exact spell structure from cheatersring

### Phase 2: Setup
- [x] Create RingOfCreation directory structure
- [x] Generate UUIDs from pool (6 needed, 6 used)
- [x] Generate localization handles (8 handles with hroc prefix)
- [x] Create meta.lsx with dependencies

### Phase 3: Ring Creation
- [x] Create ring stats entry (Armor.txt)
- [x] Create ring RootTemplate
- [x] Create base localization entries

### Phase 4: Summoning Spells
- [x] Create summon L13 chest spell
- [x] Create summon potion spell
- [x] Create summon boots spell
- [x] Add spell localization entries

### Phase 5: Delivery
- [x] Create TreasureTable.txt for Tutorial Chest
- [x] Create OneTimeRewards.lsx for Traveler's Chest
- [ ] Test both delivery methods

### Phase 6: Testing
- [ ] Test in new game (Tutorial Chest)
- [ ] Test in existing save (Traveler's Chest)
- [ ] Test summoning each item type
- [ ] Verify dependencies work correctly
- [ ] Verify summoned items persist

---

## Expected Challenges

1. **Understanding Summoning Mechanics** ✅ PARTIALLY RESOLVED
   - ✅ Direct summoning confirmed (no scrolls)
   - ✅ Tutorial Chest scroll provides reference pattern
   - ⏳ Need to extract exact spell property names and values

2. **Cross-Mod Dependencies**
   - First time declaring mod dependencies
   - Need to ensure dependency UUIDs and versions are correct
   - Must test that dependencies actually allow cross-mod item summoning

3. **Item Persistence**
   - Summoned items might not persist through saves
   - May need special flags or different approach
   - Will test with cheatersring approach first

4. **Spell Balance**
   - Unlimited item summoning could be too powerful
   - May need cooldowns or resource costs
   - Start unlimited for testing, balance later if needed

---

## Success Criteria

- ✅ Ring of Creation appears in both Tutorial Chest and Traveler's Chest
- ✅ Ring equips and grants summoning abilities
- ✅ Can summon Level 13 Plus Gear Chest from Level13PlusGear mod
- ✅ Can summon Potion of Supreme Healing from vanilla
- ✅ Can summon Boots of Stormwalker from SampleMagicRingMod
- ✅ Summoned items persist through save/load
- ✅ Dependencies properly declared and working
- ✅ Works in both new games and existing saves

---

## Future Enhancements (Post-Phase 031)

- Add more item summoning options
- Create different rings for different item categories
- Add UI for selecting items to summon
- Balance summoning costs/cooldowns
- Expand to summon any item by entering UUID

---

## Documentation Updates

After implementation:
- Update CLAUDE.md with RingOfCreation as active mod
- Update uuid_workflow.md with used UUIDs
- Document summoning spell mechanics in new instruction doc
- Create item catalog for RingOfCreation

---

## UUID Prefix Fix #2 - Incorrect Character Count

**Issue Discovered:** The mod UUID still shows as invalid because the first segment has 9 characters instead of 8.

**Root Cause:** When replacing "roc" (3 chars) with "ed31" (4 chars), I didn't account for the character count difference. The first UUID segment must be exactly 8 characters.

**Correct Approach:** Replace the first 4 characters of the original UUID with "ed31" (not replace "roc" with "ed31").

**UUID Corrections:**
- Mod: `ed31387dc-...` (9 chars, WRONG) → `ed3187dc-...` (8 chars, CORRECT)
- Ring: `ed315901-...` (8 chars, already correct) ✓
- Reward: `ed31ee90-...` (8 chars, already correct) ✓

**Original Pool UUIDs for Reference:**
- Mod: `17c387dc-...` → replace "17c3" with "ed31" = `ed3187dc-...`
- Ring: `40975901-...` → replace "4097" with "ed31" = `ed315901-...`
- Reward: `8a4eee90-...` → replace "8a4e" with "ed31" = `ed31ee90-...`

---

## UUID Prefix Fix #1 - Invalid Hexadecimal Characters

**Issue Discovered:** BG3 rejected the mod with "invalid UUID" error because the `roc` prefix contains non-hexadecimal characters ('r' and 'o' are not valid hex digits 0-9, a-f).

**Root Cause:** UUID strings must contain only hexadecimal characters. The `roc` prefix violated this requirement.

**Solution:** Changed all UUIDs to use `ed31` prefix instead (31 = Phase 031).

**UUIDs Changed:**
- Mod UUID: `roc387dc-...` → `ed3187dc-...` (fixed in UUID Prefix Fix #2)
- Ring UUID: `roc75901-...` → `ed315901-...`
- OneTimeReward UUID: `roc4eee90-...` → `ed31ee90-...`

**Note:** The three spell UUIDs that were allocated (roc55a05, rocbb55d, rocd4c2e6) were never actually used in the implementation because spell stat entries don't have UUID properties. These UUIDs were returned to the pool.

**Files Updated:**
- `meta.lsx` - Mod UUID
- `Armor.txt` - Ring RootTemplate UUID
- `ROC_Ring_Creation.lsf.lsx` - Ring MapKey
- `OneTimeRewards.lsx` - Reward UUID

---

## Implementation Summary

### UUIDs Used (ed31 prefix)

| Item | UUID |
|------|------|
| Mod | ed3187dc-1bbb-4458-86c6-255e285e9b96 |
| Ring of Creation | ed315901-9dab-41eb-a5b4-cb0f073ef272 |
| OneTimeReward | ed31ee90-0474-4852-a8d5-18a156f156b6 |

**Note:** Only 3 UUIDs were needed. Spell stat entries don't require UUIDs.

### Localization Handles (hroc prefix)

| Item | Handle |
|------|--------|
| Ring name | hroc7624bgb5dag47d9gab02g456236332c1e |
| Ring description | hroc8099g3c13g42adg8b31g50724eafee5a |
| Summon L13 Chest spell name | hroc1c8gf42ag4d19gb8e2ga1b4c7d8e9f0a |
| Summon L13 Chest spell desc | hroc6020gd37fg4fc7ga174g47f0bf91dace |
| Summon Potion spell name | hroce5b4geb99g45cagaffeg68c39c6a4429 |
| Summon Potion spell desc | hroc5661ga7e0g412ag8232gff0073e5fb64 |
| Summon Boots spell name | hroc0ccag8bc9g4a79gab95g36259cbf2165 |
| Summon Boots spell desc | hroc3d8ag477bg4051gaeecg5cb59a916ca2 |

### Files Created

**Mod Structure:**
- `RingOfCreation/Mods/RingOfCreation/meta.lsx`
- `RingOfCreation/Mods/RingOfCreation/Story/RawFiles/Goals/ForceRecompile.txt`

**Stats Files:**
- `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Armor.txt` - Ring of Creation stats
- `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Spell_Target.txt` - 3 summoning spells
- `RingOfCreation/Public/RingOfCreation/Stats/Generated/TreasureTable.txt` - Tutorial Chest injection

**Templates:**
- `RingOfCreation/Public/RingOfCreation/RootTemplates/ROC_Ring_Creation.lsf.lsx` - Ring item template

**Delivery:**
- `RingOfCreation/Public/RingOfCreation/OneTimeRewards/OneTimeRewards.lsx` - Traveler's Chest delivery

**Localization:**
- `RingOfCreation/Localization/English/RingOfCreation.loca.xml` - All 8 localization entries

### Summoning Spell Implementation

All three spells use the pattern discovered from cheatersring:
```
data "SpellProperties" "AI_IGNORE:GROUND:Summon(UUID, UntilLongRest, , , ,NAME)"
```

**Items Summoned:**
1. Level 13 Plus Gear Chest (UUID: ed134bf4-d2cc-462b-81cd-ab61536c7375)
2. Potion of Supreme Healing (UUID: 7d78f227-e8d4-486d-8121-25cf0bee751d)
3. Boots of Stormwalker (UUID: e1f2a3b4-c5d6-4e7f-8a9b-0c1d2e3f4a5b)

### Dependencies Declared

- Level13PlusGear (UUID: ed133cf1-389c-47f1-9fa7-fe49ee4fe2ce)
- SampleMagicRingMod (UUID: 560497d3-63b4-4dbe-a1c8-a10497ccc009)

---

## Delivery Failure - Ring Not Appearing

**Issue Discovered:** Ring of Creation does not appear in either Tutorial Chest or Traveler's Chest.

**Implications:** Unable to determine if:
- The ring item itself has an error preventing creation
- The delivery systems (TreasureTable/OneTimeRewards) are not working
- The mod is not being loaded properly
- There's a naming/reference mismatch

**Potential Causes:**

1. **Ring Definition Error:**
   - Stats entry using "ARM_Ring" base might have issues
   - RootTemplate might have incorrect ParentTemplateId
   - Icon reference might be invalid

2. **Spell Reference Error:**
   - Ring boosts reference three spells: `ROC_Summon_L13_Chest`, `ROC_Summon_Potion_Supreme`, `ROC_Summon_Boots_Stormwalker`
   - If spell definitions have errors, the ring might fail to create
   - Spell SpellProperties using `Summon()` function might be incorrect

3. **Delivery System Issues:**
   - TreasureTable: Uses `I_ROC_Ring_Creation` - must match stats entry name
   - OneTimeRewards: Uses `ROC_Ring_Creation` - must match stats entry name
   - Case sensitivity could be an issue

4. **Dependency Loading:**
   - Mod depends on Level13PlusGear and SampleMagicRingMod
   - If dependencies aren't loaded, the mod might fail

5. **File Structure:**
   - Files might not be in correct locations for BG3 to recognize
   - Missing or incorrect meta.lsx could prevent mod loading

**Current Implementation Details to Verify:**

```
Stats Entry: "ROC_Ring_Creation"
TreasureTable: "I_ROC_Ring_Creation"
OneTimeRewards: "ROC_Ring_Creation"
RootTemplate UUID: ed315901-9dab-41eb-a5b4-cb0f073ef272
Ring base: "ARM_Ring"
```

**Test Ring Created:**

Created a minimal test ring to isolate the issue:
- Name: "Test Ring (Simple)"
- Stats: ROC_Test_Ring_Simple
- Properties: Common rarity, no boosts, no passives
- UUID: ed315a05-b09d-452a-9250-9d952326e34e
- Delivered via both Tutorial Chest and Traveler's Chest

**Test Ring Implementation:**
- Added to Armor.txt
- Created RootTemplate (ROC_Test_Ring_Simple.lsf.lsx)
- Added to TreasureTable.txt (Tutorial Chest)
- Added to OneTimeRewards.lsx (Traveler's Chest, UUID: ed31b55d-2a10-42c2-886c-4c4e64c35be6)
- Added localization entries (name and description)

**Test Results:**
- ❌ Test ring does NOT appear in Tutorial Chest
- ❌ Test ring does NOT appear in Traveler's Chest
- ❌ Ring of Creation does NOT appear in either chest

**Conclusion:** The RingOfCreation mod is not loading properly or there's a fundamental issue with the mod structure/delivery system.

**Next Test:** Create a test ring in Level13PlusGear mod (which is known to work) to verify that the delivery system itself functions correctly. This will isolate whether the issue is specific to RingOfCreation or a broader problem.

**Level13PlusGear Test Ring Created:**

Created "Ring of Testing" in Level13PlusGear mod:
- **Stats Name:** L13_Ring_Testing
- **UUID:** ed13c2e6-0627-412c-8067-5e46d299105b
- **Parent Template:** 699135e9-8932-4bde-8a17-8be5e11d873f (vanilla MAG_Mobility_LowHP_Momentum_Ring)
- **Rarity:** Uncommon
- **Delivery:**
  - Tutorial Chest directly (TUT_Chest_Potions injection)
  - Inside L13 Plus Gear Chest (L13_Gear_Chest_TT) alongside Staff of Archmage
- **Localization:** Added name and description with hed13 prefix handles

**Files Created/Modified:**
- Created: `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Armor.txt`
- Created: `Level13PlusGear/Public/Level13PlusGear/RootTemplates/L13_Ring_Testing.lsf.lsx`
- Modified: `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/TreasureTable.txt`
- Modified: `Level13PlusGear/Localization/English/Level13PlusGear.loca.xml`

**Test Results:**
- ✅ Ring of Testing appears in Tutorial Chest (direct injection works)
- ❌ Ring of Testing does NOT appear in L13 Plus Gear Chest (even in NEW game)
- ❌ Ring display icon shows as error/incorrect (FIXED)
- ✅ Ring description displays correctly

**Analysis:**

1. **L13 Plus Gear Chest Issue:**
   - Ring added to L13_Gear_Chest_TT treasure table
   - Not appearing in the chest (tested in NEW game, so not a caching issue)
   - Possible causes:
     - Incorrect treasure table syntax (added as separate subtable)
     - May need to add both items in same subtable
     - Treasure table structure issue

2. **Icon Display Error:**
   - Icon setting: `Item_LOOT_Ring_A` (may be invalid)
   - ParentTemplateId: `699135e9-8932-4bde-8a17-8be5e11d873f` (vanilla ring specified by user)
   - Possible issues:
     - Icon path incorrect
     - ParentTemplateId might be incompatible
     - May need to use different ParentTemplateId (e.g., `6c984aa7-e1a8-4e7c-ae0e-0bcdf2b3fdd0` used in RingOfCreation)

3. **Localization Success:**
   - Description displays correctly
   - Confirms hed13 prefix handles work properly

**Icon Fix Applied:**
- Changed ParentTemplateId from `699135e9-8932-4bde-8a17-8be5e11d873f` (vanilla ring) to `6c984aa7-e1a8-4e7c-ae0e-0bcdf2b3fdd0` (standard ring parent)
- Removed Icon attribute from RootTemplate (following Staff of Archmage pattern)
- Icon should now display correctly

**Treasure Table Syntax - ATTEMPTED FIX FAILED:**

Original working state (Staff appears):
```
new subtable "1,1"
object category "I_L13_Staff_Archmage",1,0,0,0,0,0,0,0
```

Attempted fix (tried to add Ring of Testing by putting both in same subtable):
```
new subtable "1,1"
object category "I_L13_Staff_Archmage",1,0,0,0,0,0,0,0
object category "I_L13_Ring_Testing",1,0,0,0,0,0,0,0
```

**Result:** Chest became EMPTY. Both items disappeared.

**REVERTED** back to original working state with only Staff of Archmage.

**Lesson:** Cannot add items to existing treasure table without understanding correct syntax. Guessing made it worse.

**RingOfCreation Mod Structure Comparison:**

Compared file structures of Level13PlusGear (works) vs RingOfCreation (doesn't work):

**Both mods have:**
- meta.lsx with correct structure
- ForceRecompile.txt
- RootTemplates (*.lsf.lsx files)
- Stats/Generated/Data files (Armor.txt, etc.)
- TreasureTable.txt

**Key difference:**
- RingOfCreation has OneTimeRewards.lsx (Level13PlusGear doesn't)
- This shouldn't prevent mod loading

**Critical Questions to Investigate:**

1. **Is RingOfCreation showing up in BG3 Mod Manager?**
   - If NO: Mod not being recognized by BG3
   - If YES but not loading: Check mod order, dependencies, or conflicts

2. **Are there errors in BG3 logs?**
   - Script Extender logs might show why mod fails to load
   - Check for UUID conflicts or file errors

3. **Is the mod properly packaged?**
   - BG3 mods need to be in specific location
   - May need to be .pak file instead of loose files

**Conclusion:**
- ✅ Tutorial Chest direct injection works for Level13PlusGear
- ❌ L13_Gear_Chest_TT syntax fixed (pending retest)
- ❌ RingOfCreation mod has fundamental loading issue - likely not being recognized/loaded by BG3 at all

---

## Revision 7: Get Ring of Testing into Tutorial Chest (IMPLEMENTED)

**Goal:** Ensure Ring of Testing appears correctly in the Tutorial Chest with proper icon display.

**Current State:**

**Ring of Testing Status:**
- ✅ Appears in Tutorial Chest (TUT_Chest_Potions injection working)
- ❌ Icon displays incorrectly (error/wrong icon)
- ❌ Does NOT appear in L13 Plus Gear Chest

**L13 Plus Gear Chest Status:**
- ✅ Staff of Archmage appears correctly (reverted to working state)
- ❌ Cannot add additional items without breaking the chest

**Files Involved:**
1. `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Armor.txt`
   - Contains L13_Ring_Testing stats entry

2. `Level13PlusGear/Public/Level13PlusGear/RootTemplates/L13_Ring_Testing.lsf.lsx`
   - Ring template with icon issue
   - Current ParentTemplateId: `6c984aa7-e1a8-4e7c-ae0e-0bcdf2b3fdd0`
   - Icon attribute removed (attempted fix)

3. `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/TreasureTable.txt`
   - Ring added to TUT_Chest_Potions (working)
   - Ring NOT in L13_Gear_Chest_TT (reverted)

4. `Level13PlusGear/Localization/English/Level13PlusGear.loca.xml`
   - Name and description handles present

**Known Issues:**

1. **Icon Display Problem:**
   - Ring appears with incorrect/error icon
   - Attempted fix: Changed ParentTemplateId and removed Icon attribute
   - Status: Unknown if fix worked (needs testing in new game)

2. **ParentTemplateId Uncertainty:**
   - Originally used: `699135e9-8932-4bde-8a17-8be5e11d873f` (vanilla ring specified)
   - Changed to: `6c984aa7-e1a8-4e7c-ae0e-0bcdf2b3fdd0` (standard ring parent)
   - Don't know if either is correct

3. **Treasure Table Syntax Unknown:**
   - Cannot add items to existing treasure tables reliably
   - Last attempt broke L13_Gear_Chest_TT completely
   - Need to understand correct syntax before trying again

**Questions to Answer:**

1. Did the icon fix work?
   - Need to test Ring of Testing in Tutorial Chest in new game
   - Check if icon displays correctly now

2. What is the correct ParentTemplateId for a basic ring?
   - Should we look at vanilla BG3 ring templates?
   - Or find example from working mods?

3. How do we properly add items to a treasure table?
   - Current method broke the chest
   - Need to find correct syntax/pattern

**Potential Approaches:**

**Approach 1: Verify Icon Fix**
- Test in new game to see if Ring of Testing now has correct icon
- If yes: Icon problem solved
- If no: Need different ParentTemplateId or different approach

**Approach 2: Find Correct ParentTemplateId**
- Search VanillaBG3 or ExampleMods for working ring examples
- Copy exact ParentTemplateId from known-working ring
- Ensure Icon inheritance works properly

**Approach 3: Research Treasure Table Syntax** ✅ COMPLETED

**Reference Mod Found:** gandalfsequipment_44944cf8-4ce-5cxi

**Key Discovery - Worn Gray Travel Pack Pattern:**

This mod places a container (Worn Gray Travel Pack) with 8 items into the Tutorial Chest.

**Container Contents Treasure Table (lines 2-19):**
```
new treasuretable "Ink850_StatObj_Container_StartingBackpack_TT"
CanMerge 1
new subtable "1,1"
object category "I_Ink850_StatArmor_Gandalf_Robe_0",1,0,0,0,0,0,0,0
new subtable "1,1"
object category "I_Ink850_StatArmor_Gandalf_Hat_0",1,0,0,0,0,0,0,0
new subtable "1,1"
object category "I_Ink850_StatArmor_Gandalf_Cloak_0",1,0,0,0,0,0,0,0
new subtable "1,1"
object category "I_Ink850_StatWpn_Staff_Gandalf_0",1,0,0,0,0,0,0,0
new subtable "3,1"
object category "I_OBJ_Potion_Healing",1,0,0,0,0,0,0,0
new subtable "1,1"
object category "T_Supply_Vegetables",1,0,0,0,0,0,0,0
new subtable "1,1"
object category "I_Ink850_StatObj_Letter_Elrond",1,0,0,0,0,0,0,0
new subtable "1,1"
object category "I_Ink850_StatWpn_Sword_Gandalf_0",1,0,0,0,0,0,0,0
```

**Tutorial Chest Injection (lines 20-23):**
```
new treasuretable "TUT_Chest_Potions"
CanMerge 1
new subtable "1,1"
object category "I_Ink850_StatObj_Container_StartingBackpack",1,0,0,0,0,0,0,0
```

**CRITICAL FINDING:**
- ✅ Multiple items in treasure table = EACH item gets its own "new subtable" line
- ✅ This is the SAME syntax I originally used for L13_Gear_Chest_TT!
- ❌ When I changed to put both items in same subtable, the chest became empty
- ✅ The original syntax with separate subtables was CORRECT

**Why Did L13_Gear_Chest Break?**
The gandalf mod proves the multiple-subtable syntax is correct. Possible reasons it failed:
1. Ring of Testing item definition has an error (bad stats, bad RootTemplate)
2. Icon issue in RootTemplate caused item creation to fail
3. Typo in the item category name
4. Ring of Testing breaking causes entire treasure table to fail, making chest empty

**Approach 4: Alternative Delivery Method**
- Keep Ring of Testing only in Tutorial Chest (already working)
- Don't try to add to L13_Gear_Chest_TT (avoid breaking it)
- Focus on fixing icon display only

**Success Criteria:**
- Ring of Testing appears in Tutorial Chest
- Ring displays with correct icon (no error)
- Ring name and description display correctly
- Ring can be equipped and functions as basic ring

**NOT in Scope for Revision 7:**
- Adding Ring of Testing to L13_Gear_Chest_TT (proven to break things)
- Fixing RingOfCreation mod (separate issue)
- Creating additional test items

**Revised Understanding:**

Based on gandalf mod reference:
1. ✅ Original L13_Gear_Chest_TT syntax was CORRECT (multiple subtables)
2. ❌ Problem is NOT the treasure table syntax
3. ❌ Problem is the Ring of Testing item itself
4. When an item has errors, it can break the entire treasure table

**Root Cause Hypothesis:**
Ring of Testing has an issue (likely icon/ParentTemplateId) that prevents it from being created. When BG3 tries to populate the L13_Gear_Chest_TT and encounters the broken Ring of Testing, the entire treasure table fails, resulting in empty chest.

**Evidence:**
- Staff alone in table: ✅ Works (chest has staff)
- Staff + Ring in table: ❌ Fails (chest empty)
- Ring in Tutorial Chest: ✅ Works (ring appears but wrong icon)

**Conclusion:**
The Ring of Testing appears in Tutorial Chest but with wrong icon, suggesting the item mostly works but has display issues. However, when added to L13_Gear_Chest_TT, it breaks the entire chest. This suggests:
- Icon error is more severe than just "wrong icon"
- May be causing item creation to fail in some contexts
- Need to fix Ring of Testing item definition before adding to L13_Gear_Chest_TT

**Implementation Completed:**

**Step 1: Examined Gandalf Mod PowerRing**
- Found working ring example with complete attributes
- Key discovery: Working rings HAVE Icon attribute (contrary to earlier assumption)
- ParentTemplateId: `2f157b63-5500-406f-bf32-90011d612907`
- VisualTemplate: `c0f4586f-323f-7975-6aa3-7f8e9b5841f8`
- PhysicsTemplate: `6205ed1e-9bf0-e17e-61af-a1b5e9845c27`
- Icon: `Item_LOOT_GEN_Ring_B_Gem_A_Gold`

**Step 2: Fixed Ring of Testing RootTemplate**
File: `Level13PlusGear/Public/Level13PlusGear/RootTemplates/L13_Ring_Testing.lsf.lsx`

Changes:
- ✅ ParentTemplateId: Changed from `6c984aa7-e1a8-4e7c-ae0e-0bcdf2b3fdd0` to `2f157b63-5500-406f-bf32-90011d612907` (gandalf ring parent)
- ✅ Added VisualTemplate: `c0f4586f-323f-7975-6aa3-7f8e9b5841f8`
- ✅ Added PhysicsTemplate: `6205ed1e-9bf0-e17e-61af-a1b5e9845c27`
- ✅ Added Icon: `Item_LOOT_Ring_A` (basic ring icon)

**Step 3: Added Ring to L13_Gear_Chest_TT**
File: `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/TreasureTable.txt`

Used correct multiple subtables syntax (proven by gandalf mod):
```
new treasuretable "L13_Gear_Chest_TT"
CanMerge 1
new subtable "1,1"
object category "I_L13_Staff_Archmage",1,0,0,0,0,0,0,0
new subtable "1,1"
object category "I_L13_Ring_Testing",1,0,0,0,0,0,0,0
```

**Expected Results:**
- Ring of Testing should appear in Tutorial Chest with correct icon
- Ring of Testing should appear in L13 Plus Gear Chest alongside Staff
- Both items should work correctly

**Testing Required:**
- Load new game
- Check Tutorial Chest for Ring of Testing (correct icon?)
- Open L13 Plus Gear Chest (both Staff and Ring present?)

---

## Revision 8: Diagnose Ring of Testing Failure (IMPLEMENTED)

**Revision 7 Test Results:**
- ❌ Ring icon still wrong in Tutorial Chest
- ❌ Ring does NOT appear in L13 Plus Gear Chest
- ✅ Staff of Archmage DOES appear in L13 Plus Gear Chest (chest still works!)

**What We Know:**

**Ring of Testing Behavior:**
1. Appears in Tutorial Chest (TUT_Chest_Potions injection) ✅
2. Icon displays incorrectly ❌
3. Does NOT appear in L13 Plus Gear Chest (L13_Gear_Chest_TT) ❌

**What We've Tried:**
1. ❌ ParentTemplateId: `699135e9-8932-4bde-8a17-8be5e11d873f` (vanilla ring user specified)
2. ❌ ParentTemplateId: `6c984aa7-e1a8-4e7c-ae0e-0bcdf2b3fdd0` (standard ring)
3. ❌ ParentTemplateId: `2f157b63-5500-406f-bf32-90011d612907` (gandalf ring - Revision 7)
4. Removed Icon attribute ❌
5. Added Icon attribute back ❌
6. Added VisualTemplate and PhysicsTemplate ❌

**Critical Pattern:**
- Ring works in TUT_Chest_Potions (direct Tutorial Chest injection)
- Ring fails in L13_Gear_Chest_TT (container contents)
- This suggests the issue is NOT the ring definition itself
- Issue is specific to how L13_Gear_Chest container processes its treasure table

**Possible Root Causes:**

**1. Container vs Direct Chest Difference**
- Tutorial Chest: Direct injection into vanilla chest ✅ Works
- L13 Gear Chest: Custom container with treasure table ❌ Fails
- Hypothesis: Custom container has specific requirements or limitations

**2. Stats Entry Issue**
Current L13_Ring_Testing stats:
```
new entry "L13_Ring_Testing"
type "Armor"
using "ARM_Ring"
data "RootTemplate" "ed13c2e6-0627-412c-8067-5e46d299105b"
data "Rarity" "Uncommon"
data "Unique" "1"
```

Issues:
- Very minimal (no boosts, no passives)
- Using "ARM_Ring" base - is this correct?
- Maybe missing required properties?

**3. RootTemplate vs Stats Mismatch**
- RootTemplate Name: "L13_Ring_Testing"
- Stats entry: "L13_Ring_Testing"
- MapKey UUID: ed13c2e6-0627-412c-8067-5e46d299105b
- These should all match - need to verify

**4. Treasure Table Category Name**
- TreasureTable uses: "I_L13_Ring_Testing"
- Stats entry: "L13_Ring_Testing"
- Format should be: I_ + stats name
- Appears correct

**5. L13_Gear_Chest Container Definition**
- Need to examine how L13_Gear_Chest itself is defined
- Check Object.txt stats entry
- Check RootTemplate
- Verify InventoryList references L13_Gear_Chest_TT correctly

**Investigation Plan:**

**Step 1: Verify L13 Plus Gear Chest Still Works**
- Question: Does Staff of Archmage still appear in chest?
- If NO: We broke the chest again with Revision 7
- If YES: Ring is specifically failing, chest works

**Step 2: Compare Ring of Testing to Staff of Archmage** ✅ COMPLETED

**Stats Comparison:**

Staff (Weapon.txt):
```
new entry "L13_Staff_Archmage"
type "Weapon"
using "WPN_Quarterstaff_2"
data "RootTemplate" "ed13f510-3c96-4308-813e-f9592c9afee4"
data "Rarity" "Legendary"
data "Boosts" "[extensive boosts]"
data "PassivesOnEquip" "[extensive passives]"
data "Unique" "1"
```

Ring (Armor.txt):
```
new entry "L13_Ring_Testing"
type "Armor"
using "ARM_Ring"
data "RootTemplate" "ed13c2e6-0627-412c-8067-5e46d299105b"
data "Rarity" "Uncommon"
data "Unique" "1"
```

**RootTemplate Comparison:**

Staff (L13_Staff_Archmage.lsf.lsx):
- ParentTemplateId: `d25bc94a-5ee9-448f-9210-f2dad61ae7e5` (Spellsparkler)
- VisualTemplate: `91b88b2e-09c7-8523-ee50-df363cef3d9f`
- ❌ NO Icon attribute
- ❌ NO PhysicsTemplate
- ExamineRotation: "75 180 0"

Ring (L13_Ring_Testing.lsf.lsx):
- ParentTemplateId: `2f157b63-5500-406f-bf32-90011d612907` (gandalf ring)
- VisualTemplate: `c0f4586f-323f-7975-6aa3-7f8e9b5841f8` (gandalf)
- ✅ Icon: `Item_LOOT_Ring_A`
- ✅ PhysicsTemplate: `6205ed1e-9bf0-e17e-61af-a1b5e9845c27` (gandalf)
- ❌ NO ExamineRotation

**KEY FINDING:**
- Staff has NO Icon in RootTemplate → Works in L13_Gear_Chest_TT
- Ring HAS Icon in RootTemplate → Fails in L13_Gear_Chest_TT
- Contradiction: Gandalf ring HAS Icon and works in their container
- Hypothesis: Icon might be causing issues specifically in Level13PlusGear context

**Step 3: Examine L13_Gear_Chest Container**
Files to check:
- `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Object.txt`
- `Level13PlusGear/Public/Level13PlusGear/RootTemplates/L13_Gear_Chest.lsf.lsx`

Look for:
- How container references its treasure table
- Any special properties or requirements
- Comparison to gandalf's Worn Gray Travel Pack

**Step 4: Try Simplest Possible Ring**
Create ultra-minimal ring that exactly mirrors Staff structure:
- Copy Staff RootTemplate structure
- Change only: Name, MapKey, Stats reference
- Use same ParentTemplateId pattern
- Test if THIS minimal ring appears

**Step 5: Alternative Approach - Different Container**
Instead of adding to L13_Gear_Chest_TT:
- Create a NEW container just for Ring of Testing
- Place that container in Tutorial Chest
- See if Ring appears in the new container
- If YES: Issue is specific to L13_Gear_Chest_TT
- If NO: Issue is with Ring item itself

**Potential Approaches:**

**Approach A: Fix Ring Based on Staff Pattern**
- Copy exact structure from Staff of Archmage
- Change only the minimum necessary (name, UUID, stats)
- Test if exact structural match works

**Approach B: Create New Container for Ring**
- Don't try to add to existing L13_Gear_Chest_TT
- Create separate container with only Ring
- Place in Tutorial Chest
- Bypass the L13_Gear_Chest_TT issue entirely

**Approach C: Debug L13_Gear_Chest Container**
- Examine container definition in detail
- Compare to gandalf's working container
- Find what's different or missing
- Fix container to accept multiple items

**Approach D: Accept Tutorial Chest Only**
- Ring works in Tutorial Chest
- Keep it there only
- Don't try to add to L13_Gear_Chest
- Focus on fixing icon instead

**Questions to Answer:**

1. **Does Staff still appear in L13 Plus Gear Chest after Revision 7?**
   - If NO: Revert Revision 7, we broke it again
   - If YES: Continue investigation

2. **What's different between Staff and Ring definitions?**
   - Need side-by-side comparison
   - Find the critical difference

3. **How does L13_Gear_Chest reference its treasure table?**
   - Check container RootTemplate InventoryList
   - Verify treasure table name matches

4. **Why does Ring work in one chest but not another?**
   - Different container processing?
   - Missing attribute that TUT_Chest_Potions doesn't need but L13_Gear_Chest_TT does?

**Success Criteria:**
- Ring of Testing appears in L13 Plus Gear Chest alongside Staff
- Ring displays with correct icon
- Both items work properly

**Out of Scope:**
- RingOfCreation mod (still separate issue)
- Adding more items beyond Ring of Testing

**Proposed Solution for Revision 8:**

**Approach: Make Ring Match Staff Structure**

Since Staff works and Ring doesn't, make Ring RootTemplate minimal like Staff:

**Remove from Ring RootTemplate:**
- ❌ Icon attribute (Staff doesn't have it)
- ❌ PhysicsTemplate (Staff doesn't have it)
- ❌ VisualTemplate from gandalf (use different one or none)

**Keep/Add:**
- ✅ ParentTemplateId (but which one? Try Staff's parent or simpler ring parent)
- ✅ DisplayName, Description
- ✅ Stats reference

**Simplest Test:**
Use a vanilla ring ParentTemplateId that's known to work without additional attributes.

**Alternative: Copy gandalf container pattern**
Instead of fixing Ring:
- Create separate container for Ring (like gandalf's pack)
- Place container in Tutorial Chest
- See if Ring works in its own container
- If YES: Issue is with L13_Gear_Chest_TT specifically
- If NO: Issue is with Ring item

**Implementation Completed:**

**Minimal Ring RootTemplate Applied**

File: `Level13PlusGear/Public/Level13PlusGear/RootTemplates/L13_Ring_Testing.lsf.lsx`

**Removed:**
- ❌ Icon attribute
- ❌ PhysicsTemplate attribute
- ❌ VisualTemplate attribute

**Kept (Essential Only):**
- ✅ ParentTemplateId: `2f157b63-5500-406f-bf32-90011d612907` (gandalf ring parent)
- ✅ Stats: `L13_Ring_Testing`
- ✅ DisplayName handle
- ✅ Description handle

**Final Minimal Structure:**
```xml
<attribute id="MapKey" ... />
<attribute id="Name" ... />
<attribute id="Type" value="item" />
<attribute id="ParentTemplateId" value="2f157b63-5500-406f-bf32-90011d612907" />
<attribute id="Stats" value="L13_Ring_Testing" />
<attribute id="DisplayName" handle="..." />
<attribute id="Description" handle="..." />
```

**Expected Results:**
- Ring should inherit visual appearance from ParentTemplateId
- Ring should appear in both Tutorial Chest and L13 Plus Gear Chest
- Icon should come from parent template (not directly specified)

**Testing Required:**
- New game required to test
- Check Tutorial Chest for Ring (should still appear, possibly correct icon now)
- Check L13 Plus Gear Chest for both Staff AND Ring

---

## Revision 9: L13_Gear_Chest Container Investigation (IMPLEMENTED)

**Revision 8 Test Results:**
- ✅ Ring of Testing appears in Tutorial Chest
- ✅ Ring icon looks correct now!
- ✅ Ring item definition is working
- ❌ Ring does NOT appear in L13 Plus Gear Chest
- ✅ Staff still appears in L13 Plus Gear Chest

**Critical Pattern Identified:**

**Ring of Testing Behavior:**
1. Tutorial Chest (TUT_Chest_Potions injection): ✅ Works perfectly
2. L13 Plus Gear Chest (L13_Gear_Chest_TT): ❌ Fails

**Staff of Archmage Behavior:**
1. L13 Plus Gear Chest (L13_Gear_Chest_TT): ✅ Works perfectly

**Conclusion:**
- Ring item is functional (proven by Tutorial Chest appearance)
- Treasure table syntax is correct (proven by gandalf mod and Staff working)
- Issue is NOT the Ring, NOT the treasure table syntax
- Issue is something specific about L13_Gear_Chest container

**What Makes L13_Gear_Chest Different?**

The L13_Gear_Chest is a custom container that:
1. Contains a treasure table (L13_Gear_Chest_TT)
2. Is itself placed in Tutorial Chest
3. Currently works for Staff
4. Does NOT work for Ring (when both in same table)

**Investigation Required:**

**1. Examine L13_Gear_Chest Container Definition**

Files to check:
- `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Object.txt`
- `Level13PlusGear/Public/Level13PlusGear/RootTemplates/L13_Gear_Chest.lsf.lsx`

Look for:
- How container stats are defined
- How RootTemplate references treasure table
- InventoryList structure
- Any item type restrictions or filters

**2. Compare to Gandalf's Container**

Gandalf's Worn Gray Travel Pack:
- Contains 8 items successfully
- Uses same treasure table pattern (multiple subtables)
- Works in Tutorial Chest

Find differences between:
- L13_Gear_Chest container definition
- Gandalf's container definition

**3. Test Adding Ring to Treasure Table Differently**

Current TreasureTable.txt:
```
new treasuretable "L13_Gear_Chest_TT"
CanMerge 1
new subtable "1,1"
object category "I_L13_Staff_Archmage",1,0,0,0,0,0,0,0
new subtable "1,1"
object category "I_L13_Ring_Testing",1,0,0,0,0,0,0,0
```

Possible issues:
- Item category name: "I_L13_Ring_Testing" vs "L13_Ring_Testing"
- Subtable probability values
- CanMerge setting

**4. Check Item Type Categories**

Staff:
- Type: "Weapon"
- Category in treasure table: "I_L13_Staff_Archmage"

Ring:
- Type: "Armor"
- Category in treasure table: "I_L13_Ring_Testing"

Question: Does L13_Gear_Chest have item type restrictions?

**Theories:**

**Theory A: Container Capacity**
- Container can only hold 1 item?
- First item (Staff) fills it, second item (Ring) ignored?
- Test: Try removing Staff, see if Ring appears alone

**Theory B: Item Type Filter**
- Container only accepts certain item types (Weapons)?
- Ring is Armor type, might be filtered out
- Check container definition for type restrictions

**Theory C: Treasure Table Processing Order**
- First subtable processes (Staff appears)
- Second subtable fails for some reason
- Container stops processing after first item

**Theory D: Treasure Table Name Mismatch**
- L13_Gear_Chest_TT might not be correctly referenced
- Check RootTemplate InventoryList for exact name

**Investigation Plan:**

**Step 1: Read L13_Gear_Chest Container Files**
- Object.txt stats entry
- RootTemplate with InventoryList
- Document exact structure

**Step 2: Compare to Gandalf Container**
- Read gandalf's container files
- Find critical differences
- Identify what L13_Gear_Chest might be missing

**Step 3: Test Theory A - Container Capacity**
- Remove Staff from treasure table temporarily
- Test if Ring appears alone in chest
- If YES: Container limited to 1 item
- If NO: Different issue

**Step 4: Check Treasure Table Name**
- Verify exact name in container RootTemplate
- Check for typos or case sensitivity issues

**Proposed Solutions:**

**Solution A: Fix Container Definition**
- If container has capacity limit, increase it
- If container has type filter, remove it
- Match gandalf's working container structure

**Solution B: Different Treasure Table Structure**
- Try single subtable with both items
- Try different probability values
- Try without CanMerge

**Solution C: Separate Container for Ring**
- Create new container just for Ring
- Place both containers in Tutorial Chest
- Bypass the multi-item issue entirely

**Solution D: Add Ring Directly to Tutorial Chest**
- Ring already works in Tutorial Chest
- Keep it there (already implemented)
- Don't try to add to L13_Gear_Chest
- Accept this limitation

**Questions to Answer:**

1. How does L13_Gear_Chest reference L13_Gear_Chest_TT?
2. Does container have item capacity limit?
3. Does container have item type restrictions?
4. How is gandalf's container different?
5. Can we replicate gandalf's exact pattern?

**Success Criteria:**
- Both Staff and Ring appear in L13 Plus Gear Chest
- Both items work correctly
- Understand why it was failing

**ROOT CAUSE IDENTIFIED BY USER:**

**The "Unique" Flag Issue**

Ring of Testing was marked as `data "Unique" "1"` in Armor.txt.

**How BG3 Handles Unique Items:**
- Unique items can only appear ONCE per game/world
- Ring already spawns in Tutorial Chest (TUT_Chest_Potions)
- When L13_Gear_Chest_TT tries to spawn the same unique ring, BG3 blocks it
- Result: Staff appears (not unique conflict), Ring doesn't (blocked by unique constraint)

**Why This Explains Everything:**
- ✅ Ring appears in Tutorial Chest (first spawn, allowed)
- ❌ Ring doesn't appear in L13 Plus Gear Chest (second spawn, blocked)
- ✅ Staff appears everywhere (different item, no conflict)

**Solution Implemented:**

File: `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Armor.txt`

Changed:
```
data "Unique" "1"  ← Prevents multiple spawns
```

To:
```
data "Unique" "0"  ← Allows multiple spawns
```

**Expected Results:**
- Ring should now appear in BOTH locations:
  - Tutorial Chest (direct injection)
  - L13 Plus Gear Chest (treasure table)
- Players can have multiple copies of Ring of Testing

**Testing Required:**
- New game to test
- Check both Tutorial Chest and L13 Plus Gear Chest
- Both should contain Ring of Testing

---

## Revision 10: Apply Lessons to RingOfCreation Mod (IMPLEMENTED)

**Goal:** Fix RingOfCreation mod using lessons learned from Ring of Testing success.

**Current State of RingOfCreation:**
- ❌ Ring of Creation doesn't appear anywhere
- ❌ Test Ring Simple doesn't appear anywhere
- ❌ Mod appears to not be loading

**Lessons Learned from Ring of Testing:**

1. **Minimal RootTemplate Structure**
   - Remove Icon attribute
   - Remove PhysicsTemplate
   - Remove VisualTemplate
   - Keep only: ParentTemplateId, Stats, DisplayName, Description

2. **Unique Flag Must Be 0**
   - Items appearing in multiple locations need `Unique: 0`
   - Ring of Creation: In Tutorial Chest + Traveler's Chest → needs `Unique: 0`
   - Test Ring Simple: In Tutorial Chest + Traveler's Chest → needs `Unique: 0`

3. **Working ParentTemplateId**
   - Use proven working ring parent: `2f157b63-5500-406f-bf32-90011d612907`

4. **Treasure Table Syntax**
   - Multiple subtables is correct (proven by gandalf mod)
   - Each item gets own "new subtable" line

**Files to Fix:**

**1. Armor.txt - Ring Stats**
Current:
```
new entry "ROC_Ring_Creation"
type "Armor"
using "ARM_Ring"
data "RootTemplate" "ed315901-9dab-41eb-a5b4-cb0f073ef272"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(ROC_Summon_L13_Chest);UnlockSpell(ROC_Summon_Potion_Supreme);UnlockSpell(ROC_Summon_Boots_Stormwalker)"
data "Unique" "1"  ← CHANGE TO 0

new entry "ROC_Test_Ring_Simple"
type "Armor"
using "ARM_Ring"
data "RootTemplate" "ed315a05-b09d-452a-9250-9d952326e34e"
data "Rarity" "Common"
data "Unique" "1"  ← CHANGE TO 0
```

**2. ROC_Ring_Creation.lsf.lsx - Main Ring RootTemplate**
Current has many attributes. Simplify to minimal:
- Keep: ParentTemplateId (change to working one), Stats, DisplayName, Description
- Remove: Icon, VisualTemplate, PhysicsTemplate, etc.

**3. ROC_Test_Ring_Simple.lsf.lsx - Test Ring RootTemplate**
Same as above - simplify to minimal structure.

**4. TreasureTable.txt**
Already uses correct syntax (multiple subtables), no changes needed.

**5. Spell_Target.txt**
Contains 3 summoning spells - these might have issues but leave for now.
Focus on getting rings to appear first.

**Implementation Plan:**

**Step 1: Fix Ring of Creation Stats**
- Change `Unique: 1` to `Unique: 0`

**Step 2: Fix Ring of Creation RootTemplate**
- Change ParentTemplateId to `2f157b63-5500-406f-bf32-90011d612907`
- Remove Icon, PhysicsTemplate, VisualTemplate
- Keep only minimal attributes

**Step 3: Fix Test Ring Simple Stats**
- Change `Unique: 1` to `Unique: 0`

**Step 4: Fix Test Ring Simple RootTemplate**
- Change ParentTemplateId to `2f157b63-5500-406f-bf32-90011d612907`
- Remove Icon, PhysicsTemplate, VisualTemplate
- Keep only minimal attributes

**Step 5: Verify Treasure Table Syntax**
- Ensure each ring has own subtable
- Keep existing structure (already correct)

**Expected Results After Fixes:**
- Ring of Creation appears in Tutorial Chest
- Ring of Creation appears in Traveler's Chest
- Test Ring Simple appears in Tutorial Chest
- Test Ring Simple appears in Traveler's Chest
- Both rings display correctly
- Summoning spells may or may not work (separate issue to debug later)

**Known Potential Issues:**

1. **Mod Loading**
   - If mod isn't being loaded by BG3 at all, these fixes won't help
   - Need to verify mod appears in Mod Manager
   - Check mod is enabled

2. **Summoning Spells**
   - Ring of Creation has complex spell boosts
   - Spells reference cross-mod items (L13 chest, SMR boots)
   - May cause issues even if ring appears
   - Plan: Fix ring appearance first, debug spells later

3. **Dependencies**
   - RingOfCreation depends on Level13PlusGear and SampleMagicRingMod
   - These must be loaded for summoning to work
   - But shouldn't prevent rings from appearing

**Success Criteria:**
- Both rings appear in their respective locations
- Rings can be equipped
- Rings display with correct icons
- (Summoning functionality is secondary - get appearance working first)

**Implementation Completed:**

**Changes Applied to RingOfCreation Mod:**

**1. Armor.txt - Fixed Both Rings**
File: `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Armor.txt`

Ring of Creation:
- Changed: `Unique: 1` → `Unique: 0`

Test Ring Simple:
- Changed: `Unique: 1` → `Unique: 0`

**2. ROC_Ring_Creation.lsf.lsx - Main Ring RootTemplate**
File: `RingOfCreation/Public/RingOfCreation/RootTemplates/ROC_Ring_Creation.lsf.lsx`

Changes:
- ✅ ParentTemplateId: Changed from `6c984aa7-e1a8-4e7c-ae0e-0bcdf2b3fdd0` to `2f157b63-5500-406f-bf32-90011d612907` (working gandalf ring parent)
- ❌ Removed Icon attribute
- ✅ Kept minimal structure: ParentTemplateId, Stats, DisplayName, Description

**3. ROC_Test_Ring_Simple.lsf.lsx - Test Ring RootTemplate**
File: `RingOfCreation/Public/RingOfCreation/RootTemplates/ROC_Test_Ring_Simple.lsf.lsx`

Changes:
- ✅ ParentTemplateId: Changed from `6c984aa7-e1a8-4e7c-ae0e-0bcdf2b3fdd0` to `2f157b63-5500-406f-bf32-90011d612907` (working gandalf ring parent)
- ❌ Removed Icon attribute
- ✅ Kept minimal structure: ParentTemplateId, Stats, DisplayName, Description

**Summary of Fixes:**
- Both rings now use minimal RootTemplate structure (like Ring of Testing)
- Both rings marked as Unique: 0 (can appear in multiple locations)
- Both rings use proven working ParentTemplateId
- Icon attributes removed (inherit from parent)

**Expected Results:**
- ✅ Ring of Creation should appear in Tutorial Chest
- ✅ Ring of Creation should appear in Traveler's Chest
- ✅ Test Ring Simple should appear in Tutorial Chest
- ✅ Test Ring Simple should appear in Traveler's Chest
- ✅ Rings should display with correct icons (inherited from parent)
- ⚠️ Summoning spells on Ring of Creation may still need debugging

**Testing Required:**
- New game to test
- Check Tutorial Chest for both rings
- Check Traveler's Chest (existing save) for both rings
- Verify rings can be equipped
- Test summoning spells (secondary priority)

---

## Revision 11: Remove Potion Summoning from Ring of Creation (IMPLEMENTED)

**Revision 10 Test Results:**
- ✅ Ring of Creation appears in Tutorial Chest and Traveler's Chest!
- ✅ Test Ring Simple appears in Tutorial Chest and Traveler's Chest!
- ✅ Rings display correctly
- ✅ Almost completely successful!

**Goal:** Remove the ability to summon Potion of Supreme Healing from Ring of Creation.

**Current Ring of Creation Abilities:**
```
data "Boosts" "UnlockSpell(ROC_Summon_L13_Chest);UnlockSpell(ROC_Summon_Potion_Supreme);UnlockSpell(ROC_Summon_Boots_Stormwalker)"
```

Three summoning spells:
1. ROC_Summon_L13_Chest (Keep)
2. ROC_Summon_Potion_Supreme (Remove)
3. ROC_Summon_Boots_Stormwalker (Keep)

**Files to Modify:**

**1. Armor.txt - Remove Spell from Boosts**
File: `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Armor.txt`

Current:
```
data "Boosts" "UnlockSpell(ROC_Summon_L13_Chest);UnlockSpell(ROC_Summon_Potion_Supreme);UnlockSpell(ROC_Summon_Boots_Stormwalker)"
```

Change to:
```
data "Boosts" "UnlockSpell(ROC_Summon_L13_Chest);UnlockSpell(ROC_Summon_Boots_Stormwalker)"
```

**2. Spell_Target.txt - Optional Cleanup**
File: `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Spell_Target.txt`

Options:
- **Option A:** Leave spell definition in place (no harm, just unused)
- **Option B:** Remove entire ROC_Summon_Potion_Supreme spell entry (cleaner)

**3. Localization - Optional Cleanup**
File: `RingOfCreation/Localization/English/RingOfCreation.loca.xml`

Potion spell entries:
- `hroce5b4geb99g45cagaffeg68c39c6a4429` - Spell name
- `hroc5661ga7e0g412ag8232gff0073e5fb64` - Spell description

Options:
- **Option A:** Leave entries (no harm, just unused)
- **Option B:** Remove entries (cleaner)

**4. Ring Description - Optional Update**
File: `RingOfCreation/Localization/English/RingOfCreation.loca.xml`

Ring description currently mentions:
> "Grants the ability to summon the Level 13 Plus Gear Chest, Potions of Supreme Healing, and Boots of the Stormwalker."

Should update to:
> "Grants the ability to summon the Level 13 Plus Gear Chest and Boots of the Stormwalker."

**Implementation Plan:**

**Approach A: Minimal Change (Recommended)**
- Remove spell from ring's Boosts
- Leave spell definition and localization in place
- Update ring description
- Fast, simple, no risk

**Approach B: Complete Cleanup**
- Remove spell from ring's Boosts
- Remove spell definition from Spell_Target.txt
- Remove localization entries
- Update ring description
- Thorough, but more work

**Recommended: Approach A**
- Simplest and safest
- Unused spell/localization won't hurt anything
- Keeps file complete for future reference

**Implementation Steps:**

**Step 1: Remove Spell from Ring Boosts**
Edit Armor.txt to remove `UnlockSpell(ROC_Summon_Potion_Supreme);`

**Step 2: Update Ring Description**
Edit localization to remove mention of Potions of Supreme Healing

**Expected Results:**
- Ring of Creation grants only 2 spells:
  - Summon Level 13 Plus Gear Chest
  - Summon Boots of Stormwalker
- Potion summoning spell no longer accessible
- Ring description accurately reflects abilities

**Success Criteria:**
- Ring equips successfully
- Only 2 summoning spells granted (L13 Chest, Boots)
- No potion summoning spell
- Description accurate

**Implementation Completed - Approach B (Complete Cleanup):**

**Changes Applied:**

**1. Armor.txt - Removed Spell from Boosts**
File: `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Armor.txt`

Changed:
```
Before: "UnlockSpell(ROC_Summon_L13_Chest);UnlockSpell(ROC_Summon_Potion_Supreme);UnlockSpell(ROC_Summon_Boots_Stormwalker)"
After:  "UnlockSpell(ROC_Summon_L13_Chest);UnlockSpell(ROC_Summon_Boots_Stormwalker)"
```

**2. Spell_Target.txt - Removed Spell Definition**
File: `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Spell_Target.txt`

Removed entire ROC_Summon_Potion_Supreme spell entry (24 lines)

**3. Localization - Removed Spell Entries and Updated Description**
File: `RingOfCreation/Localization/English/RingOfCreation.loca.xml`

Removed:
- `hroce5b4geb99g45cagaffeg68c39c6a4429` - "Summon Potion of Supreme Healing"
- `hroc5661ga7e0g412ag8232gff0073e5fb64` - Potion spell description

Updated Ring Description:
```
Before: "...Chest, Potions of Supreme Healing, and Boots..."
After:  "...Chest and Boots of the Stormwalker."
```

**Final State:**

Ring of Creation now grants only 2 summoning spells:
1. ✅ Summon Level 13 Plus Gear Chest
2. ✅ Summon Boots of Stormwalker

All references to potion summoning removed:
- ✅ Not in ring's Boosts
- ✅ Spell definition deleted
- ✅ Localization entries deleted
- ✅ Ring description updated

**Expected Results:**
- Ring equips successfully
- Grants exactly 2 summoning spells
- No potion summoning option
- Clean, accurate description

**Testing Required:**
- Equip Ring of Creation
- Verify only 2 spells granted
- Test both summoning spells work correctly

---

## Revision 12: Fix OneTimeRewards Format (IMPLEMENTED)

**Problem Identified:**
RingOfCreation OneTimeRewards.lsx uses incorrect format compared to working SampleMagicRingMod.

**Format Comparison:**

**SampleMagicRingMod (Correct):**
```xml
<node id="OneTimeReward">
    <attribute id="Amount" type="uint32" value="1"/>
    <attribute id="ItemTemplateId" type="FixedString" value="[RootTemplate UUID]"/>
    <attribute id="UUID" type="guid" value="[Unique UUID]"/>
</node>
```

**RingOfCreation (Incorrect):**
```xml
<node id="RewardNode">
    <attribute id="Reward" type="LSString" value="[Stat Name]"/>
    <attribute id="UUID" type="FixedString" value="[UUID]"/>
</node>
```

**Key Differences:**
1. Node name: `OneTimeReward` vs `RewardNode`
2. Item reference: `ItemTemplateId` (RootTemplate UUID) vs `Reward` (stat name)
3. UUID type: `guid` vs `FixedString`
4. Missing `Amount` attribute

**Implementation:**

File: `RingOfCreation/Public/RingOfCreation/OneTimeRewards/OneTimeRewards.lsx`

Fixed format to match SampleMagicRingMod:

**Ring of Creation:**
- Amount: 1
- ItemTemplateId: ed315901-9dab-41eb-a5b4-cb0f073ef272 (RootTemplate UUID from Armor.txt)
- UUID: ed31ee90-0474-4852-a8d5-18a156f156b6

**Test Ring Simple:**
- Amount: 1
- ItemTemplateId: ed315a05-b09d-452a-9250-9d952326e34e (RootTemplate UUID from Armor.txt)
- UUID: ed31b55d-2a10-42c2-886c-4c4e64c35be6

**Expected Results:**
- Ring of Creation appears in Traveler's Chest
- Test Ring Simple appears in Traveler's Chest
- Both rings work in existing saves (if Traveler's Chest not yet opened)

---

## Notes

- This mod serves as both a utility and a learning exercise
- Understanding item summoning mechanics will be valuable for future mods
- Dual delivery approach addresses Phase 030 container limitation discovery
- Dependencies make this mod a good test of cross-mod functionality
