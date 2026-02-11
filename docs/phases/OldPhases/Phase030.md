# Phase 030 - Rename to Level13PlusGear & Fix Localization Handles

**Status:** COMPLETE

## Goal
1. Rename the mod from "Level13Gear" to "Level13PlusGear" throughout all files and directories
2. Replace patterned/weak localization handles with properly randomized ones to prevent potential mod conflicts

---

## Part 1: Rename Level13Gear → Level13PlusGear

### Scope
**What Changes:**
- All references to "Level13Gear" become "Level13PlusGear"
- Directory names containing "Level13Gear"
- File names containing "Level13Gear"
- Chest display name: "Level 13 Gear Chest" → "Level 13 Plus Gear Chest"

**What Stays the Same:**
- ✅ All "L13_" prefixes remain unchanged (L13_Staff_Archmage, L13_Gear_Chest, etc.)
- ✅ All UUIDs remain unchanged
- ✅ All stats entry names remain unchanged

### Files & Directories to Rename

**Directories:**
1. `Level13Gear/` → `Level13PlusGear/`
2. `Level13Gear/Mods/Level13Gear/` → `Level13PlusGear/Mods/Level13PlusGear/`
3. `Level13Gear/Public/Level13Gear/` → `Level13PlusGear/Public/Level13PlusGear/`

**Files:**
1. `Localization/English/Level13Gear.loca.xml` → `Level13PlusGear.loca.xml`

**Content Updates Required:**
1. `meta.lsx`:
   - Description: "Level 13 character gear mod" → "Level 13+ character gear mod"
   - Folder: "Level13Gear" → "Level13PlusGear"
   - Name: "Level13Gear" → "Level13PlusGear"

2. `Level13PlusGear.loca.xml`:
   - Chest name: "Level 13 Gear Chest" → "Level 13 Plus Gear Chest"
   - Chest description: "A chest containing powerful gear for level 13 characters." → "A chest containing powerful gear for level 13+ characters."

### Rename Checklist
- [x] Rename root directory: Level13Gear/ → Level13PlusGear/
- [x] Rename Mods subdirectory: Mods/Level13Gear/ → Mods/Level13PlusGear/
- [x] Rename Public subdirectory: Public/Level13Gear/ → Public/Level13PlusGear/
- [x] Rename localization file: Level13Gear.loca.xml → Level13PlusGear.loca.xml
- [x] Update meta.lsx with new folder/name/description
- [x] Update chest display text in localization file
- [x] Verify no "Level13Gear" references remain (except in old phase docs)

---

## Part 2: Fix Weak Localization Handles

### Issue Analysis

**Current Handles in Level13PlusGear.loca.xml:**

| Handle | Text | Pattern Analysis |
|--------|------|------------------|
| `h0a1b2c3dge4f5g6a7bg8c9dg0e1f2a3b4c5d6` | Staff of the Archmage | ⚠️ **TOO PATTERNED** - Sequential hex |
| `ha1b2c3d4gf5e6g7a8bg9c0dg1e2f3a4b5c6d7` | Staff description | ⚠️ **TOO PATTERNED** - Sequential hex |
| `hed1371c8gf42ag4d19gb8e2ga1b4c7d8e9f0a` | Level 13 Gear Chest | ✅ Good - Fixed in Phase 29, uses ed13 prefix |
| `h324e8d15ga83ag84b5ge87eg9fab3gd0a604` | Chest description | ⚠️ **WEAK** - Somewhat patterned |

**Risk:** These patterned handles may have been copied from example mods or generated with weak randomization, increasing the chance of conflicts with other mods.

**Solution:** Generate truly random handles using UUIDs from the uuid_workflow.md pool.

### Handle Generation Process

**BG3 Localization Handle Format:**
- Starts with `h`
- Contains lowercase hexadecimal characters (0-9, a-f)
- Separated by `g` characters
- Example: `h223d7c04gf72fg73a4gd76dg8efa2fc09593`

**Generation Method (Level13PlusGear Convention):**
1. Take a UUID from the pool (e.g., `75d7624b-b5da-47d9-ab02-456236332c1e`)
2. **Apply ed13 prefix transformation**: Replace first 4 characters with `ed13`
   - `75d7624b-b5da-47d9-ab02-456236332c1e` → `ed137624b-b5da-47d9-ab02-456236332c1e`
3. Remove hyphens: `ed137624bb5da47d9ab02456236332c1e`
4. Insert `g` separators at intervals and add `h` prefix: `hed137624bgb5dag47d9gab02g456236332c1e`
5. Result: Unique handle with ed13 branding and true randomness

**Example from Phase 029:**
- Chest name handle: `hed1371c8gf42ag4d19gb8e2ga1b4c7d8e9f0a`
- Contains **ed13** prefix: h**ed13**71c8g...
- This follows the same UUID convention used for item UUIDs

**Why ed13 in Handles?**
- Consistency: All Level13PlusGear UUIDs and handles use ed13 branding
- Easy identification: Quickly identify Level13PlusGear handles in logs/files
- Prevents conflicts: Ensures handles are unique to this mod

### Handles to Replace

| Current Handle | Usage | New Handle (TBD) |
|----------------|-------|------------------|
| `h0a1b2c3dge4f5g6a7bg8c9dg0e1f2a3b4c5d6` | Staff of the Archmage (name) | Generate from UUID pool |
| `ha1b2c3d4gf5e6g7a8bg9c0dg1e2f3a4b5c6d7` | Staff of the Archmage (description) | Generate from UUID pool |
| `h324e8d15ga83ag84b5ge87eg9fab3gd0a604` | Chest description | Generate from UUID pool |

**Note:** `hed1371c8gf42ag4d19gb8e2ga1b4c7d8e9f0a` (chest name) is already good - was fixed in Phase 29 with proper ed13 prefix transformation.

### Files Requiring Handle Updates

**For Each Handle Replacement:**

1. **Localization File:**
   - File: `Level13PlusGear/Localization/English/Level13PlusGear.loca.xml`
   - Update: `<content contentuid="OLD_HANDLE">` → `<content contentuid="NEW_HANDLE">`

2. **RootTemplate Files:**
   - File: `Level13PlusGear/Public/Level13PlusGear/RootTemplates/L13_Staff_Archmage.lsf.lsx`
   - Update: `<attribute id="DisplayName" type="TranslatedString" handle="OLD_HANDLE">`
   - Update: `<attribute id="Description" type="TranslatedString" handle="OLD_HANDLE">`

   - File: `Level13PlusGear/Public/Level13PlusGear/RootTemplates/L13_Gear_Chest.lsf.lsx`
   - Update: `<attribute id="Description" type="TranslatedString" handle="OLD_HANDLE">`

### Handle Replacement Checklist
- [x] Generate 3 new handles from UUID pool
- [x] Update Staff name handle in L13_Staff_Archmage.lsf.lsx
- [x] Update Staff description handle in L13_Staff_Archmage.lsf.lsx
- [x] Update Chest description handle in L13_Gear_Chest.lsf.lsx
- [x] Update all 3 handles in Level13PlusGear.loca.xml
- [x] Delete 3 UUIDs from uuid_workflow.md pool
- [x] Document new handles in this phase file

---

## Implementation Plan

### Step 1: Perform Rename (Part 1)
1. Rename directories (root → Mods → Public)
2. Rename localization file
3. Update meta.lsx
4. Update chest text in localization file
5. Verify all "Level13Gear" references replaced

### Step 2: Generate New Handles (Part 2)
1. Take 3 UUIDs from uuid_workflow.md pool
2. Apply ed13 prefix transformation to each UUID (replace first 4 chars with ed13)
3. Convert each to handle format (remove hyphens, add h prefix, insert g separators)
4. Document new handles

### Step 3: Update Handle References (Part 2)
1. Update L13_Staff_Archmage.lsf.lsx (DisplayName, Description)
2. Update L13_Gear_Chest.lsf.lsx (Description)
3. Update Level13PlusGear.loca.xml (all 3 handles)
4. Delete used UUIDs from pool

### Step 4: Verification
1. Search for any remaining "Level13Gear" references (should find none except in old docs)
2. Verify no old patterned handles remain in localization file
3. Test in BG3 mod manager - verify mod loads as "Level13PlusGear"
4. Test in-game - verify chest and staff names display correctly

---

## Expected Changes Summary

### Before Phase 030:
- Mod name: **Level13Gear**
- Chest: "Level 13 Gear Chest"
- Handles: Weak/patterned (3 need replacement)

### After Phase 030:
- Mod name: **Level13PlusGear**
- Chest: "Level 13 Plus Gear Chest"
- Handles: All properly randomized from UUID pool

### What Doesn't Change:
- ✅ L13_ prefixes (stats entries, item names)
- ✅ UUIDs (mod UUID, item UUIDs)
- ✅ Game functionality (all items work the same)

---

## Implementation Summary

**Implementation Date:** February 10, 2026

### Part 1: Rename Complete ✅

**Directories Renamed:**
- `Level13Gear/` → `Level13PlusGear/`
- `Mods/Level13Gear/` → `Mods/Level13PlusGear/`
- `Public/Level13Gear/` → `Public/Level13PlusGear/`

**Files Renamed:**
- `Level13Gear.loca.xml` → `Level13PlusGear.loca.xml`

**meta.lsx Updates:**
- Description: "Level 13 character gear mod" → "Level 13+ character gear mod"
- Folder: "Level13Gear" → "Level13PlusGear"
- Name: "Level13Gear" → "Level13PlusGear"

**Localization Updates:**
- Chest name: "Level 13 Gear Chest" → "Level 13 Plus Gear Chest"
- Chest description: "level 13 characters" → "level 13+ characters"

### Part 2: Localization Handles Fixed ✅

**New Handles Generated (with ed13 prefix):**

| Usage | Old Handle (Weak) | New Handle (ed13) | Source UUID |
|-------|------------------|-------------------|-------------|
| Staff Name | `h0a1b2c3dge4f5g6a7bg8c9dg0e1f2a3b4c5d6` | `hed137624bgb5dag47d9gab02g456236332c1e` | `75d7624b-b5da-47d9-ab02-456236332c1e` |
| Staff Description | `ha1b2c3d4gf5e6g7a8bg9c0dg1e2f3a4b5c6d7` | `hed138099g3c13g42adg8b31g50724eafee5a` | `c41a8099-3c13-42ad-8b31-50724eafee5a` |
| Chest Description | `h324e8d15ga83ag84b5ge87eg9fab3gd0a604` | `hed136020gd37fg4fc7ga174g47f0bf91dace` | `af386020-d37f-4fc7-a174-47f0bf91dace` |

**Files Updated:**
- `L13_Staff_Archmage.lsf.lsx` - DisplayName and Description handles
- `L13_Gear_Chest.lsf.lsx` - Description handle
- `Level13PlusGear.loca.xml` - All 3 new handles

**UUIDs Removed from Pool:**
- `75d7624b-b5da-47d9-ab02-456236332c1e`
- `c41a8099-3c13-42ad-8b31-50724eafee5a`
- `af386020-d37f-4fc7-a174-47f0bf91dace`

### All Handles Now Use ed13 Prefix ✅

**Complete Handle Inventory (8 Total):**

**Staff Handles:**
1. `hed137624bgb5dag47d9gab02g456236332c1e` - Staff of the Archmage (name)
2. `hed138099g3c13g42adg8b31g50724eafee5a` - Staff of the Archmage (description)

**Chest Handles:**
3. `hed1371c8gf42ag4d19gb8e2ga1b4c7d8e9f0a` - Level 13 Plus Gear Chest (name)
4. `hed136020gd37fg4fc7ga174g47f0bf91dace` - Level 13 Plus Gear Chest (description)

**Interrupt Handles (added post-implementation):**
5. `hed13e5b4geb99g45cagaffeg68c39c6a4429` - Shield (Unlimited) (name)
6. `hed135661ga7e0g412ag8232gff0073e5fb64` - Shield (Unlimited) (description)
7. `hed130ccag8bc9g4a79gab95g36259cbf2165` - Counterspell (Unlimited) (name)
8. `hed133d8ag477bg4051gaeecg5cb59a916ca2` - Counterspell (Unlimited) (description)

All 8 handles now follow the ed13 prefix convention, ensuring:
- ✅ Unique identification of Level13PlusGear mod assets
- ✅ True randomness from UUID pool
- ✅ No risk of conflicts with other mods
- ✅ Complete independence from SampleMagicRingMod

---

## Additional Weak Handles Discovered - Interrupt.txt

### Discovery (Post-Implementation)

After Phase 030 completion, additional weak/patterned handles were discovered in `Interrupt.txt`.

**File:** `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Interrupt.txt`

**Handles Found:**

| Entry | Field | Handle | Pattern Analysis |
|-------|-------|--------|------------------|
| L13_Interrupt_Shield_Unlimited | DisplayName | `hf6a7b8c9gd0e1g2f3ag4b5cga0b1c2d3e4f5a6` | ⚠️ Patterned |
| L13_Interrupt_Shield_Unlimited | Description | `h6f7a8b9cg0d1eg3f2ag5b4cg1a0b2c3d4e5f6a7` | ⚠️ Patterned |
| L13_Interrupt_Counterspell_Unlimited | DisplayName | `h4b5c6d7eg8f9ag0b1cg2d3eg5f6a7b8c9d0e1f2` | ⚠️ Patterned |
| L13_Interrupt_Counterspell_Unlimited | Description | `hb5c6d7e8g9f0ag1b2cg3d4eg6f7a8b9c0d1e2f3` | ⚠️ Patterned |

### Origin of These Handles

**Source:** These handles were inherited from SampleMagicRingMod during Phase 029 when the Staff of the Archmage was ported.

**Original Context (SampleMagicRingMod):**
- Entry: `SMR_Interrupt_Shield_Unlimited`
  - DisplayName: `hf6a7b8c9gd0e1g2f3ag4b5cga0b1c2d3e4f5a6` → "Spectral Shield"
  - Description: `h6f7a8b9cg0d1eg3f2ag5b4cg1a0b2c3d4e5f6a7` → "Unlimited Shield as a bonus action."

- Entry: `SMR_Interrupt_Counterspell_Unlimited`
  - DisplayName: `h4b5c6d7eg8f9ag0b1cg2d3eg5f6a7b8c9d0e1f2` → "Spectral Counter"
  - Description: `hb5c6d7e8g9f0ag1b2cg3d4eg6f7a8b9c0d1e2f3` → "Unlimited Counterspell as a bonus action."

**What Happened in Phase 029:**
1. Staff of the Archmage was ported from SampleMagicRingMod → Level13Gear
2. Interrupt.txt was created with L13_ prefix interrupts
3. Handles were copied directly from SampleMagicRingMod without modification
4. Stats entry names changed (SMR_ → L13_) but handles remained the same

### Current State Analysis

**Problem 1: Weak/Patterned Handles**
All 4 handles show obvious sequential patterns similar to the staff/chest handles fixed in Phase 030.

**Problem 2: Missing Localization Entries**
- Level13PlusGear's `Level13PlusGear.loca.xml` does **NOT** contain these 4 handles
- These handles only exist in SampleMagicRingMod's localization files
- Level13PlusGear is currently **dependent on SampleMagicRingMod** for interrupt text display

**Verification:**
```bash
grep "hf6a7b8c9" Level13PlusGear/ -r
# Only found in: Interrupt.txt

grep "hf6a7b8c9" SampleMagicRingMod/Localization/ -r
# Found in: SampleMagicRingMod.loca.xml and SampleMagicRingMod.xml
# Text: "Spectral Shield"
```

### Impact Assessment

**Current Behavior:**
- If SampleMagicRingMod is **loaded**: Interrupts display as "Spectral Shield" and "Spectral Counter" (borrowed text)
- If SampleMagicRingMod is **NOT loaded**: Interrupts likely display with missing/blank text or handle UIDs

**Independence Violation:**
This creates an **unintended dependency** on SampleMagicRingMod, contradicting the goal established in Phase 029 to make Level13PlusGear completely independent.

### Recommended Fix (Future Phase)

**Option 1: Add Localization Entries (Quick Fix)**
Add the 4 handles to `Level13PlusGear.loca.xml` with appropriate text:
```xml
<content contentuid="hf6a7b8c9gd0e1g2f3ag4b5cga0b1c2d3e4f5a6" version="1">Shield (Unlimited)</content>
<content contentuid="h6f7a8b9cg0d1eg3f2ag5b4cg1a0b2c3d4e5f6a7" version="1">Unlimited Shield as a bonus action.</content>
<content contentuid="h4b5c6d7eg8f9ag0b1cg2d3eg5f6a7b8c9d0e1f2" version="1">Counterspell (Unlimited)</content>
<content contentuid="hb5c6d7e8g9f0ag1b2cg3d4eg6f7a8b9c0d1e2f3" version="1">Unlimited Counterspell as a bonus action.</content>
```
**Pros:** Immediate fix, maintains independence
**Cons:** Still uses weak/patterned handles

**Option 2: Generate New Handles with ed13 Prefix (Proper Fix)**
1. Generate 4 new handles from UUID pool with ed13 prefix
2. Update Interrupt.txt with new handles
3. Add localization entries with new handles
4. Delete 4 UUIDs from pool

**Pros:** Complete fix, all handles properly randomized with ed13 branding
**Cons:** Requires more UUIDs from pool

**Recommended:** Option 2 for consistency with Phase 030 approach

### Summary

**Discovered Issues:**
- ✅ 4 additional weak/patterned handles found
- ✅ Handles inherited from SampleMagicRingMod in Phase 029
- ✅ Missing localization entries create hidden dependency
- ✅ Violates mod independence established in Phase 029

**Status:** ✅ **FIXED** (Implemented immediately after discovery)

### Fix Implementation

**Date:** February 10, 2026 (same day as Phase 030)

**New Handles Generated (with ed13 prefix):**

| Usage | Old Handle (Weak) | New Handle (ed13) | Source UUID |
|-------|------------------|-------------------|-------------|
| Shield DisplayName | `hf6a7b8c9gd0e1g2f3ag4b5cga0b1c2d3e4f5a6` | `hed13e5b4geb99g45cagaffeg68c39c6a4429` | `8f93e5b4-eb99-45ca-affe-68c39c6a4429` |
| Shield Description | `h6f7a8b9cg0d1eg3f2ag5b4cg1a0b2c3d4e5f6a7` | `hed135661ga7e0g412ag8232gff0073e5fb64` | `67e15661-a7e0-412a-8232-ff0073e5fb64` |
| Counterspell DisplayName | `h4b5c6d7eg8f9ag0b1cg2d3eg5f6a7b8c9d0e1f2` | `hed130ccag8bc9g4a79gab95g36259cbf2165` | `4cc70cca-8bc9-4a79-ab95-36259cbf2165` |
| Counterspell Description | `hb5c6d7e8g9f0ag1b2cg3d4eg6f7a8b9c0d1e2f3` | `hed133d8ag477bg4051gaeecg5cb59a916ca2` | `a0ef3d8a-477b-4051-aeec-5cb59a916ca2` |

**Files Updated:**
1. `Interrupt.txt` - All 4 handles replaced with ed13-prefixed versions
2. `Level13PlusGear.loca.xml` - Added 4 new localization entries:
   - "Shield (Unlimited)" - "Cast Shield as a bonus action without expending spell slots."
   - "Counterspell (Unlimited)" - "Cast Counterspell as a bonus action without expending spell slots."

**UUIDs Removed from Pool:**
- `8f93e5b4-eb99-45ca-affe-68c39c6a4429`
- `67e15661-a7e0-412a-8232-ff0073e5fb64`
- `4cc70cca-8bc9-4a79-ab95-36259cbf2165`
- `a0ef3d8a-477b-4051-aeec-5cb59a916ca2`

**Result:**
- ✅ All interrupt handles now use ed13 prefix
- ✅ Level13PlusGear now has its own localization entries
- ✅ Complete independence from SampleMagicRingMod achieved
- ✅ No more hidden dependencies

---

## Critical Discovery: Container Delivery Limitation

### Issue Discovered During Testing

**Date:** February 10, 2026

**Observation:**
- In **existing saved games** where tutorial chest was already opened: Level 13 Plus Gear Chest does NOT appear
- Old "Level 13 Gear Chest" is gone (due to rename in Phase 030)
- In **new saves** (before opening tutorial chest): Level 13 Plus Gear Chest appears correctly

### Root Cause Analysis

**How BG3 Treasure Tables Work:**

When a container (like TUT_Chest_Potions) is first generated/opened in a save file:
1. Game evaluates all treasure tables that merge into that container
2. Generates loot based on current mods loaded
3. **Saves the generated loot to the save file**
4. Future loads use the **saved loot**, not re-evaluating treasure tables

**What This Means:**

```
Timeline:
1. Player opens tutorial chest → Game generates loot from treasure tables → Saves to save file
2. Player later installs/updates mod → Chest loot already "locked in" save file
3. New items in treasure table → NOT added to already-opened chests
```

**Why Phase 030 Rename Broke Existing Saves:**

The rename changed the mod identity, so BG3 treats it as a different mod:
- Old mod: "Level13Gear" with chest "Level 13 Gear Chest"
- New mod: "Level13PlusGear" with chest "Level 13 Plus Gear Chest"
- Existing save: Has "Level 13 Gear Chest" from old mod → No longer provided by new mod → Chest disappears

### Impact on Future Development

**The Problem:**
Adding new items to Level13PlusGear via Tutorial Chest will NOT make them available in existing playthroughs where the chest was already opened.

**Example Scenario:**
1. Player starts new game with Level13PlusGear (has Staff of Archmage)
2. Player opens tutorial chest, gets staff, continues playing
3. Modder adds "Ring of Power" to Level13PlusGear chest
4. Player loads save → Ring does NOT appear (chest already opened)

### Delivery System Comparison

| Method | New Games | Existing Saves (Unopened Chest) | Existing Saves (Opened Chest) | Notes |
|--------|-----------|--------------------------------|------------------------------|-------|
| **Container (Current)** | ✅ Works | ✅ Works | ❌ Fails | Loot locked after first open |
| **OneTimeRewards** | ✅ Works | ⚠️ Maybe | ⚠️ Maybe | Delivers to Traveler's Chest - similar limitations |
| **Console Commands** | ✅ Works | ✅ Works | ✅ Works | Requires player manual action |
| **Script Extender** | ✅ Works | ✅ Works | ✅ Works | Advanced, requires SE installed |

### Potential Solutions

**Option 1: Accept Current Limitation**
- Document clearly that Level13PlusGear is "new game friendly"
- Recommend players start new games when updating mod
- Pro: Simple, no changes needed
- Con: Poor user experience for existing saves

**Option 2: Console Command Documentation**
- Provide console commands for each item
- Players manually spawn items in existing saves
- Example: `tz add_item L13_Staff_Archmage`
- Pro: Works for all saves
- Con: Requires player action, less immersive

**Option 3: Multiple Delivery Methods**
- Use different containers for different items
- Some in Tutorial Chest, some in Act 1 camps, some in Act 2, etc.
- Spread items across unopened containers
- Pro: Better chance of working in existing saves
- Con: Complex to manage

**Option 4: Hybrid Approach**
- Core items: Tutorial Chest (for new games)
- New additions: Different containers or console commands
- Document which items work in existing saves
- Pro: Best of both worlds
- Con: More complex implementation

**Option 5: OneTimeRewards with Traveler's Chest**
- Revert to OneTimeRewards.lsx delivery (Phase 029 approach)
- Items appear in Traveler's Chest (camps, etc.)
- Check if this handles updates better than tutorial chest
- Pro: May be more update-friendly
- Con: Need to research if this actually solves the problem

### Recommended Approach for Level13PlusGear

**Short Term:**
1. Document this limitation in README/documentation
2. Advise players to start new games when mod updates with new items
3. Provide console commands for all items as a workaround

**Long Term Research Needed:**
1. Test OneTimeRewards behavior with mod updates
2. Investigate if Traveler's Chest re-evaluates on save load
3. Research Script Extender options for dynamic item delivery
4. Consider container rotation strategy (Act 1, 2, 3 containers)

### Documentation for Users

**Should Include:**
- "This mod is designed for new games"
- "Updating the mod mid-playthrough may not add new items to existing saves"
- "Use console commands to add items to existing characters"
- Provide clear console command list for each item

### Action Items for Future Phases

- [ ] Research OneTimeRewards vs Container delivery for updates
- [ ] Test Traveler's Chest behavior with mod updates
- [ ] Create console command reference for all items
- [ ] Consider delivery system redesign for better update support
- [ ] Document container behavior in CLAUDE.md for future reference

### Key Takeaway

**Container-based delivery has a fundamental limitation:** Once a container is opened, its loot is locked in the save file. This is a **BG3 engine behavior**, not a bug in our implementation.

This is an important consideration for **any mod** that uses container delivery and plans to add items over time.

---

## Test Plan

### Rename Testing:
- [x] Mod manager shows "Level13PlusGear" (not "Level13Gear")
- [x] Chest displays "Level 13 Plus Gear Chest"
- [x] Chest description mentions "level 13+ characters"
- [x] No errors in mod manager or game logs

### Handle Testing:
- [x] Staff name displays "Staff of the Archmage"
- [x] Staff description displays correctly
- [x] Chest description displays correctly
- [x] No localization errors or missing text
- [x] Verify handles don't conflict with other loaded mods

---

## Notes

- This phase is primarily cosmetic/organizational - no gameplay changes
- The rename clarifies this mod is for level 13+ characters
- Fixing handles is a preventative measure against potential future conflicts
- All L13_ prefixes intentionally remain unchanged for consistency
- Documentation in old phase files (Phase029.md etc.) will still reference "Level13Gear" - this is expected and OK

---

## Success Criteria

- ✅ All directories and files renamed to Level13PlusGear
- ✅ meta.lsx reflects new mod identity
- ✅ All weak localization handles replaced with properly randomized ones
- ✅ Mod loads and functions identically to before (just with new name)
- ✅ No "Level13Gear" references in current mod files
- ✅ Documentation updated with new handles used
