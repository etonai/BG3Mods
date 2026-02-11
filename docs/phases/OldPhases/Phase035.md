# Phase 35: Fix Item Names and Descriptions

**Status:** COMPLETE
**Date:** 2026-02-10
**Implementation Date:** 2026-02-10
**Completion Date:** 2026-02-10

---

## Goal

Improve the quality and consistency of item names, descriptions, and power tooltips in the Level13PlusGear mod by:
1. Adding missing descriptions for passives/abilities
2. Creating custom versions of vanilla passives to allow name/description customization
3. Additional improvements to be researched and added

---

## Issue 1: Moonshield Aura Missing Description

### Current State

**File:** `Passive.txt`
```
new entry "L13_Moonshield_Passive"
type "PassiveData"
data "Properties" "ToggledDefaultOn;ToggledDefaultAddToHotbar;IsToggled"
data "DisplayName" "hed13ab6eg97b6g4155g4ebeg8cb6g634b9ffc1b02;1"
data "ToggleOnFunctors" "ApplyStatus(SCL_MOONSHIELD_AURA, 100, -1)"
data "ToggleOffFunctors" "RemoveStatus(SCL_MOONSHIELD_AURA)"
```

**Problem:** No `Description` field, so tooltip is incomplete.

### Solution

Add a Description field with a new handle:
```
data "Description" "[NEW_HANDLE];1"
```

**Localization to add:**
- Handle: Generate from UUID pool
- Text: "Emanates a protective aura that shields allies from the Shadow Curse."

**Files to modify:**
1. `Passive.txt` - Add Description field
2. `Level13PlusGear.loca.xml` - Add description text
3. `uuid_workflow.md` - Remove 1 UUID from pool
4. `Phase035.md` - Document UUID used

---

## Issue 2: Lathander's Light Passive - Custom Version Needed

### Current State

The Moonguard Blade uses the vanilla passive:
```
data "PassivesOnEquip" "...; CRE_LathandersLight_Passive; ..."
```

**Problem:** Uses vanilla name/description which doesn't match the Moonguard theme.

### Vanilla Passive Location

**File:** `VanillaBG3/gustav/Public/Gustav/Stats/Generated/Data/Passive.txt` (or similar)

**Passive Name:** `CRE_LathandersLight_Passive`

### Research Needed

1. Find the vanilla passive definition in VanillaBG3 files
2. Identify what it does (likely related to Lathander's Light aura)
3. Determine localization handles used
4. Copy to Level13PlusGear as `L13_LathandersLight_Passive`

### Solution Plan

1. **Research:** Locate `CRE_LathandersLight_Passive` in VanillaBG3
2. **Copy:** Create `L13_LathandersLight_Passive` with same functionality
3. **Customize:** Add custom name and description
4. **Update:** Change Moonguard Blade to use `L13_LathandersLight_Passive`

**Suggested Custom Name:** "Moonguard's Radiance" or "Selûne's Light"

**Suggested Description:** Something themed to Selûne instead of Lathander.

**Files to modify:**
1. `Passive.txt` - Add L13_LathandersLight_Passive entry
2. `Weapon.txt` - Update Moonguard Blade reference
3. `Level13PlusGear.loca.xml` - Add custom name/description
4. `uuid_workflow.md` - Remove UUIDs from pool
5. `Phase035.md` - Document UUIDs used

---

## Issue 3: Tyr-Named Powers on Moonguard Blade

### Current State

The Moonguard Blade uses shared spells that reference Tyr:

**From Localization:**
```
L13_Target_BlindingSmite_Unlimited:
  DisplayName: "Tyr's Blinding Smite"
  Description: "Blinding Smite. Unlimited uses."
```

**Problem:** The Moonguard Blade is a weapon of Selûne (the Moonmaiden), not Tyr. The spell names should reflect moon/Selûne themes, not Tyr.

### Items That Share This Spell

**Currently used by:**
1. L13_Sword_Tyr (Longsword of Tyr) - Correct theme ✓
2. L13_Blade_Moonguard (Moonguard Blade) - Wrong theme ❌

### Solution Options

**Option A: Create Separate Moon-Themed Version**
- Create `L13_Target_BlindingSmite_Moonguard` as a separate spell
- Name: "Moonguard's Blinding Smite" or "Selûne's Blinding Smite"
- Description: Moon-themed version
- Only used by Moonguard Blade
- **Pros:** Clean separation, thematically correct
- **Cons:** Duplicates spell functionality

**Option B: Rename Shared Version to Generic**
- Rename to just "Blinding Smite (Unlimited)"
- Works for both weapons
- **Pros:** No duplication
- **Cons:** Less flavorful for Tyr's sword

**Recommendation:** Option A - Create moon-themed version for Moonguard Blade

### Implementation for Option A

1. Copy `L13_Target_BlindingSmite_Unlimited` to `L13_Target_BlindingSmite_Moonguard`
2. Generate 2 new handles (DisplayName, ExtraDescription)
3. Add moon-themed localization
4. Update Moonguard Blade to use new spell version
5. Keep Tyr version for Longsword of Tyr

**Files to modify:**
1. `Spell_Target.txt` - Add new spell entry
2. `Weapon.txt` - Update Moonguard Blade spell reference
3. `Level13PlusGear.loca.xml` - Add moon-themed localization
4. `uuid_workflow.md` - Remove UUIDs from pool
5. `Phase035.md` - Document UUIDs used

**Suggested Names:**
- "Moonguard's Blinding Smite"
- "Selûne's Blinding Smite"
- "Lunar Blinding Smite"

**Suggested Description:**
- "Channel Selûne's radiance to blind your foes. Unlimited uses."
- "Moonlight surges through your blade, blinding enemies. Unlimited uses."

---

## Additional Issues (To Be Researched)

### Placeholder for User Research

Additional items to investigate:

- Other passives/abilities with generic or missing descriptions
- Item descriptions that could be more detailed or thematic
- Spell names that could be more distinctive
- Consistency issues between similar items

---

## UUID Requirements (Updated Estimate)

### Confirmed Needs:

**Issue 1 - Moonshield Description:**
1. **Description:** 1 handle ✓ USED

**Issue 2 - Lathander's Light Custom Passive:**
~~2. **DisplayName:** 1 handle~~
~~3. **Description:** 1 handle~~
**SKIPPED** - Keeping vanilla passive

**Issue 3 - Moon-Themed Blinding Smite:**
2. **DisplayName:** 1 handle
3. **ExtraDescription:** 1 handle

### Additional Items:
- TBD based on further research

**Estimated Total:** 3 UUIDs (1 used, 2 remaining for Blinding Smite)

---

## Implementation Steps (Draft)

### Step 1: Fix Moonshield Aura Description

1. Generate 1 handle from UUID pool
2. Add `Description` field to `L13_Moonshield_Passive` in `Passive.txt`
3. Add localization entry to `Level13PlusGear.loca.xml`
4. Test that tooltip displays correctly in-game

### Step 2: Research Lathander's Light Passive

1. ✓ Search VanillaBG3 files for `CRE_LathandersLight_Passive`
2. ✓ Checked all Passive.txt files in gustav/ and shared/
3. ✓ Searched for MAG_LATHANDERS_LIGHT_TECHNICAL status
4. ✓ Documented findings: Passive not found in reference files
5. ✓ **DECISION:** Keep using vanilla passive (Option A)

### Step 3: Create Custom Lathander's Light Passive

**SKIPPED** - Decision made to keep vanilla `CRE_LathandersLight_Passive` rather than create custom version.

**Rationale:**
- Cannot locate vanilla definition to copy functionality
- Risk of breaking existing feature by guessing at implementation
- Moonguard Blade already has moon-themed name and majority of powers are moon-themed
- One Lathander reference acceptable given constraints

### Step 4: Create Moon-Themed Blinding Smite

1. ✓ Copy `L13_Target_BlindingSmite_Unlimited` to create `L13_Target_BlindingSmite_Moonguard`
2. ✓ Generate 2 handles from UUID pool (DisplayName, ExtraDescription)
3. ✓ Add moon-themed localization:
   - DisplayName: "Selûne's Blinding Smite"
   - ExtraDescription: "Channel Selûne's radiance to blind your foes. Unlimited uses."
4. ✓ Update Moonguard Blade to use `L13_Target_BlindingSmite_Moonguard`
5. ✓ Verify Longsword of Tyr still uses `L13_Target_BlindingSmite_Unlimited`

### Step 5: Additional Fixes (TBD)

Based on user research, implement additional improvements.

### Step 5: Update Documentation

1. Update `item_catalog.md` if any item details changed
2. Document all UUIDs used
3. Mark phase as IMPLEMENTED

---

## Files to Modify

| File | Action | Description |
|------|--------|-------------|
| `Passive.txt` | ✓ Edit | Added Description to Moonshield Passive |
| `Spell_Target.txt` | ✓ Edit | Added L13_Target_BlindingSmite_Moonguard |
| `Weapon.txt` | ✓ Edit | Updated Moonguard Blade to use new Blinding Smite spell |
| `Level13PlusGear.loca.xml` | ✓ Edit | Added 3 new localization entries (Moonshield description, Selûne's Blinding Smite name/description) |
| `uuid_workflow.md` | ✓ Edit | Removed 3 used UUIDs |
| `item_catalog.md` | ✓ Edit | Updated Moonguard Blade entry, added new spell, updated passives, added version history |
| `Phase035.md` | ✓ Edit | Documented research findings, UUIDs, and implementation |

---

## Research Section: Lathander's Light Passive

### Vanilla File Location
**NOT FOUND** - The passive `CRE_LathandersLight_Passive` does not exist in our VanillaBG3 reference files.

**Search Results:**
- Searched all Passive.txt files in VanillaBG3/gustav/
- Searched all Passive.txt files in VanillaBG3/shared/
- Searched all Status files for `MAG_LATHANDERS_LIGHT_TECHNICAL`
- No matches found in any vanilla game files

**Conclusion:** This passive is either:
1. From a DLC/patch not included in our VanillaBG3 reference files
2. A placeholder passive that doesn't actually exist
3. Defined in a game file format we don't have extracted

### Vanilla Definition
**NOT AVAILABLE** - Cannot locate vanilla definition.

### Vanilla Localization
**NOT AVAILABLE** - Cannot locate vanilla localization.

### Analysis

**Current Usage:**
- Used in SampleMagicRingMod on multiple weapons
- Moonguard Blade has both the passive AND `StatusOnEquip: MAG_LATHANDERS_LIGHT_TECHNICAL`
- The status is also not found in VanillaBG3 files

**What It Likely Does:**
Based on the name "Lathander's Light" (Lathander is the god of dawn/light in D&D):
- Probably creates an aura of light that blinds or damages undead/fiends
- Similar to the "Light" cantrip but with combat effects
- The toggled nature suggests it can be turned on/off

**Recommendation:**
Since we cannot find the vanilla definition, we have three options:

**Option A: Keep Using Vanilla Passive (Recommended)**
- Leave `CRE_LathandersLight_Passive` as-is
- Accept that we cannot customize the name/description
- It works in-game even though we can't see the definition
- **Pros:** No risk of breaking functionality
- **Cons:** Can't customize for Selûne theme

**Option B: Remove the Passive**
- Remove both the passive and the status from Moonguard Blade
- **Pros:** Clean, no mystery references
- **Cons:** Loses a potentially useful feature

**Option C: Create New Custom Passive**
- Create a completely new L13 passive based on similar vanilla effects
- Research other light/aura passives to replicate functionality
- **Pros:** Full control, Selûne-themed naming
- **Cons:** Risk of not matching original functionality, more work

**Selected Option: A (Keep Vanilla Passive)**
Given that we cannot verify the exact functionality and the passive works in-game, the safest approach is to keep using the vanilla passive. The Moonguard Blade will have this one Lathander-themed element, but the majority of its powers are already moon-themed.

---

## UUID Allocation (To Be Filled During Implementation)

### Issue 1: Moonshield Aura Description
- **UUID:** `2b99003f-b312-446e-a869-df1a99711655`
- **Description Handle:** `hed132b99g003fgb312g446ega869gdf1a99711655`
- **Text:** "Emanates a protective aura that shields allies from the Shadow Curse."
- **Status:** ✓ IMPLEMENTED

### Issue 2: Lathander's Light Custom Passive
- **Status:** ✗ SKIPPED (Keeping vanilla passive)

### Issue 3: Moon-Themed Blinding Smite
- **DisplayName UUID:** `8183d689-33b1-40c6-9e8d-da543deb74d9`
- **DisplayName Handle:** `hed138183gd689g33b1g40c6g9e8dgda543deb74d9`
- **DisplayName Text:** "Selûne's Blinding Smite"
- **ExtraDescription UUID:** `f88d7b6f-aba8-4bfc-b535-7dbfc723e6e4`
- **ExtraDescription Handle:** `hed13f88dg7b6fgaba8g4bfcgb535g7dbfc723e6e4`
- **ExtraDescription Text:** "Channel Selûne's radiance to blind your foes. Unlimited uses."
- **Status:** ✓ IMPLEMENTED

### Additional Items
- **To be added based on further research**

---

## Testing Plan

### Test 1: Moonshield Aura Tooltip
1. Equip Moonguard Blade
2. Open character sheet
3. Hover over Moonshield Aura passive
4. **Verify:** Description tooltip displays: "Emanates a protective aura that shields allies from the Shadow Curse."

### Test 2: Selûne's Blinding Smite (Moonguard Blade)
1. Equip Moonguard Blade
2. Check spell list/hotbar
3. **Verify:** Blinding Smite shows "Selûne's Blinding Smite" (not "Tyr's Blinding Smite")
4. Hover over spell
5. **Verify:** Description displays: "Channel Selûne's radiance to blind your foes. Unlimited uses."
6. Cast the spell
7. **Verify:** Functionality unchanged (blinds enemies, unlimited uses)

### Test 3: Longsword of Tyr Still Uses Tyr Version
1. Equip Longsword of Tyr
2. Check spell list
3. **Verify:** Shows "Tyr's Blinding Smite" (unchanged)
4. **Verify:** Both weapons have separate, thematically appropriate versions

---

## Implementation Summary

**What Was Implemented:**

1. **Moonshield Aura Description** ✓
   - Added missing description to L13_Moonshield_Passive
   - Text: "Emanates a protective aura that shields allies from the Shadow Curse."
   - Used 1 UUID: `2b99003f-b312-446e-a869-df1a99711655`

2. **Lathander's Light Passive Research** ✓
   - Researched vanilla `CRE_LathandersLight_Passive`
   - **Finding:** Passive not found in VanillaBG3 reference files
   - **Decision:** Keep using vanilla passive (cannot customize without definition)
   - No UUIDs used

3. **Selûne's Blinding Smite** ✓
   - Created `L13_Target_BlindingSmite_Moonguard` (moon-themed variant)
   - Name: "Selûne's Blinding Smite"
   - Description: "Channel Selûne's radiance to blind your foes. Unlimited uses."
   - Updated Moonguard Blade to use new spell
   - Longsword of Tyr still uses original `L13_Target_BlindingSmite_Unlimited` (Tyr's Blinding Smite)
   - Used 2 UUIDs: `8183d689-33b1-40c6-9e8d-da543deb74d9`, `f88d7b6f-aba8-4bfc-b535-7dbfc723e6e4`

**Total UUIDs Used:** 3
**Status:** IMPLEMENTED (awaiting user testing)

---

## Success Criteria

- [x] Moonshield Aura has complete description
- [x] Lathander's Light passive researched (decision: keep vanilla)
- [x] Moon-themed Blinding Smite created (Selûne's Blinding Smite)
- [x] Moonguard Blade updated to use moon-themed Blinding Smite
- [x] All UUIDs documented
- [x] Documentation updated (item_catalog.md, uuid_workflow.md)
- [ ] All new tooltips display correctly (requires user testing)
- [ ] No functionality broken (requires user testing)
- [ ] Additional improvements (awaiting user research)

---

## Related Documentation

- **docs/level13plusgear/item_catalog.md** - Item reference (to be updated)
- **VanillaBG3/gustav/** - Source for vanilla passive research
- **docs/instructions/copying_items_between_mods.md** - Reference for copying process
- **Phase032.md** - Previous passive copying example (RadiantWeapon)

---

## Notes

- This phase focuses on polish and quality of life improvements
- Custom passives allow better thematic consistency
- Missing descriptions can confuse players
- Selûne/Moonguard theme should be emphasized in custom text

---

## Post-Implementation

- [x] Update item_catalog.md with corrected descriptions
- [x] Mark phase as IMPLEMENTED
- [x] User testing completed successfully
- [x] Phase marked as COMPLETE
