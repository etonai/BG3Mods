# Phase 055: Remove Concentration from Staff of Gimeitaro Buffs

**Status:** COMPLETE
**Date:** 2026-02-15

---

## Goals

1. **Remove Concentration from Gimeitaro's Shield** - Allow Silvered Bulwark to persist without concentration
2. **Remove Concentration from Celestial Haste** - Allow Haste buff to persist without concentration
3. **Remove Concentration from Spirit Guardians** - Allow Spirit Guardians to persist without concentration
4. **Update Documentation** - Update item_catalog.md to reflect non-concentration buffs

**Result:** All three powerful buffs can be active simultaneously without concentration management, significantly increasing the staff's power.

---

## Summary of Changes

| Spell | Current State | Target State |
|-------|---------------|--------------|
| **Gimeitaro's Shield** | Requires concentration | No concentration required |
| **Celestial Haste** | Requires concentration | No concentration required |
| **Spirit Guardians** | Requires concentration | No concentration required |

**Result:** The Staff of Gimeitaro becomes even more powerful by allowing all three major buffs to stack without concentration conflicts.

---

## Current State

### Gimeitaro's Shield (Silvered Bulwark)

**File:** `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Target.txt`

**Current Implementation:**
```
new entry "L21_Target_GimeitarosShield_Unlimited"
type "SpellData"
data "SpellType" "Target"
using "Target_GlobeOfInvulnerability"
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsConcentration;IsSpell"
```

**Current Behavior:**
- Grants Silvered Bulwark (mobile invulnerability)
- Unlimited uses as bonus action
- **Requires concentration** (prevents using other concentration spells)

---

### Celestial Haste

**File:** `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Shout.txt`

**Current Implementation:**
```
new entry "L21_Shout_CelestialHaste_Unlimited"
type "SpellData"
data "SpellType" "Shout"
using "Shout_MAG_Victory_Longbow_Haste"
data "UseCosts" ""
data "Cooldown" ""
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsSpell"
```

**Note:** The base spell `Shout_MAG_Victory_Longbow_Haste` inherits from vanilla Haste, which requires concentration.

**Current Behavior:**
- Grants Haste buff (extra action, doubled movement, +2 AC, advantage on DEX saves)
- Free action cast
- Unlimited uses
- **Requires concentration** (inherited from base spell)

---

### Gimeitaro's Spirit Guardians

**File:** `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Shout.txt`

**Current Implementation:**
```
new entry "L21_Shout_SpiritGuardians_Gimeitaro"
type "SpellData"
data "SpellType" "Shout"
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsConcentration;IsSpell;IsHarmful;IsLinkedSpellContainer"
```

**Current Behavior:**
- Creates 3m aura dealing 3d8 Radiant or Necrotic damage
- Free action cast
- Unlimited uses
- **Requires concentration**

---

## Target State

### Gimeitaro's Shield - No Concentration

**File:** `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Target.txt`

**Target Implementation:**
```
new entry "L21_Target_GimeitarosShield_Unlimited"
type "SpellData"
data "SpellType" "Target"
using "Target_GlobeOfInvulnerability"
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsSpell"
```

**Changes:**
- Remove `IsConcentration` flag from SpellFlags

**Result:** Silvered Bulwark persists without concentration, allowing other concentration spells to be active.

---

### Celestial Haste - No Concentration

**File:** `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Shout.txt`

**Investigation Required:**
The spell uses `using "Shout_MAG_Victory_Longbow_Haste"` which may inherit concentration from the base spell. Need to check if this spell has explicit SpellFlags or if we need to override them.

**Current entry:**
```
new entry "L21_Shout_CelestialHaste_Unlimited"
type "SpellData"
data "SpellType" "Shout"
using "Shout_MAG_Victory_Longbow_Haste"
data "UseCosts" ""
data "Cooldown" ""
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsSpell"
```

**Observation:** The SpellFlags already lacks `IsConcentration` - but the base spell may still enforce it.

**Possible Solutions:**
1. If concentration is inherited, explicitly set `SpellFlags` without `IsConcentration`
2. If that doesn't work, may need to copy the full spell definition instead of using `using`
3. Check if vanilla Haste spell can be referenced with modified flags

**Target Implementation (if explicit override needed):**
```
new entry "L21_Shout_CelestialHaste_Unlimited"
type "SpellData"
data "SpellType" "Shout"
using "Shout_MAG_Victory_Longbow_Haste"
data "UseCosts" ""
data "Cooldown" ""
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsSpell"
data "SpellProperties" "" // Override to ensure no concentration status
```

**Result:** Haste buff persists without concentration.

---

### Spirit Guardians - No Concentration

**File:** `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Shout.txt`

**Target Implementation (Main Container):**
```
new entry "L21_Shout_SpiritGuardians_Gimeitaro"
type "SpellData"
data "SpellType" "Shout"
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsSpell;IsHarmful;IsLinkedSpellContainer"
```

**Target Implementation (Radiant Variant):**
```
new entry "L21_Shout_SpiritGuardians_Gimeitaro_Radiant"
type "SpellData"
data "SpellType" "Shout"
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsSpell;IsHarmful"
```

**Target Implementation (Necrotic Variant):**
```
new entry "L21_Shout_SpiritGuardians_Gimeitaro_Necrotic"
type "SpellData"
data "SpellType" "Shout"
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsSpell;IsHarmful"
```

**Changes:**
- Remove `IsConcentration` flag from all three Spirit Guardians spell entries

**Result:** Spirit Guardians aura persists without concentration, allowing other concentration spells.

---

## Implementation Plan

### Task 1: Remove Concentration from Gimeitaro's Shield

**Description:** Modify Spell_Target.txt to remove IsConcentration flag

**Steps:**
1. Read current `Spell_Target.txt` file
2. Locate `L21_Target_GimeitarosShield_Unlimited` entry
3. Find SpellFlags line
4. Remove `IsConcentration;` from the flags
5. Save file

**Files to modify:**
- `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Target.txt` - Remove concentration flag

---

### Task 2: Remove Concentration from Celestial Haste

**Description:** Modify Spell_Shout.txt to ensure no concentration on Haste

**Steps:**
1. Read current `Spell_Shout.txt` file
2. Locate `L21_Shout_CelestialHaste_Unlimited` entry
3. Verify SpellFlags doesn't include `IsConcentration`
4. If inherited from base spell, may need to explicitly override SpellProperties
5. Test in-game to confirm concentration is removed

**Files to modify:**
- `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Shout.txt` - Ensure no concentration

**Note:** May require testing to verify the base spell doesn't enforce concentration.

---

### Task 3: Remove Concentration from Spirit Guardians

**Description:** Modify Spell_Shout.txt to remove IsConcentration from all Spirit Guardians variants

**Steps:**
1. Read current `Spell_Shout.txt` file
2. Locate all three Spirit Guardians entries:
   - `L21_Shout_SpiritGuardians_Gimeitaro`
   - `L21_Shout_SpiritGuardians_Gimeitaro_Radiant`
   - `L21_Shout_SpiritGuardians_Gimeitaro_Necrotic`
3. Remove `IsConcentration;` from SpellFlags in all three entries
4. Save file

**Files to modify:**
- `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Shout.txt` - Remove concentration from all 3 Spirit Guardians entries

---

### Task 4: Update Documentation

**Description:** Update item catalog to reflect non-concentration buffs

**Steps:**
1. Read `docs/level21gear/item_catalog.md`
2. Update Staff of Gimeitaro entry
3. Note that all three buffs no longer require concentration
4. Update descriptions to emphasize this powerful capability

**Files to modify:**
- `docs/level21gear/item_catalog.md` - Update staff description

---

### Task 5: Update Phase Document with Results

**Description:** Document implementation results and mark phase as IMPLEMENTED

**Steps:**
1. After implementation, update this phase document
2. Add "Implementation Complete" section
3. Document any issues encountered
4. List all modified files with changes
5. Mark status as IMPLEMENTED

**Files to modify:**
- `docs/phases/Phase055.md` - Add implementation section

---

## Detailed Implementation

### Step 1: Modify Gimeitaro's Shield

**File:** `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Target.txt`

**Find:**
```
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsConcentration;IsSpell"
```

**Replace with:**
```
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsSpell"
```

**Purpose:** Removes concentration requirement from Silvered Bulwark, allowing it to persist alongside other concentration spells.

---

### Step 2: Verify Celestial Haste

**File:** `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Shout.txt`

**Current SpellFlags:**
```
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsSpell"
```

**Action:**
1. Verify this line is present and doesn't include `IsConcentration`
2. Test in-game to confirm the base spell `Shout_MAG_Victory_Longbow_Haste` doesn't enforce concentration
3. If concentration still applies, investigate base spell behavior

**Note:** May already be correct, but needs testing to confirm.

---

### Step 3: Modify Spirit Guardians (All 3 Entries)

**File:** `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Shout.txt`

**Entry 1 - Main Container:**

**Find:**
```
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsConcentration;IsSpell;IsHarmful;IsLinkedSpellContainer"
```

**Replace with:**
```
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsSpell;IsHarmful;IsLinkedSpellContainer"
```

**Entry 2 - Radiant Variant:**

**Find:**
```
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsConcentration;IsSpell;IsHarmful"
```

**Replace with:**
```
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsSpell;IsHarmful"
```

**Entry 3 - Necrotic Variant:**

**Find:**
```
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsConcentration;IsSpell;IsHarmful"
```

**Replace with:**
```
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsSpell;IsHarmful"
```

**Purpose:** Removes concentration requirement from all Spirit Guardians variants, allowing the aura to persist alongside other buffs.

---

### Step 4: Update Item Catalog

**File:** `docs/level21gear/item_catalog.md`

**Current Description Excerpt:**
```markdown
**Spells Granted:**
- **Gimeitaro's Shield** - Silvered Bulwark (unlimited, bonus action)
- **Celestial Haste** - Haste (unlimited, free action)
- **Gimeitaro's Spirit Guardians** - Spirit Guardians (unlimited, free action)
```

**Update to:**
```markdown
**Spells Granted:**
- **Gimeitaro's Shield** - Silvered Bulwark (unlimited, bonus action, **no concentration**)
- **Celestial Haste** - Haste (unlimited, free action, **no concentration**)
- **Gimeitaro's Spirit Guardians** - Spirit Guardians (unlimited, free action, **no concentration**)

**Power Enhancement:** All three major buffs can be active simultaneously without concentration conflicts, allowing unprecedented defensive and offensive power stacking.
```

**Purpose:** Clearly document this powerful capability in the item catalog.

---

## Files to Modify

| File | Action | Description |
|------|--------|-------------|
| `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Target.txt` | Edit | Remove `IsConcentration` from Gimeitaro's Shield SpellFlags |
| `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Shout.txt` | Edit | Verify/remove `IsConcentration` from Celestial Haste (if needed) |
| `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Shout.txt` | Edit | Remove `IsConcentration` from all 3 Spirit Guardians entries |
| `docs/level21gear/item_catalog.md` | Edit | Update staff description to note non-concentration buffs |
| `docs/phases/Phase055.md` | Edit | Add implementation section when complete |

---

## UUID/Handle Requirements

**No new UUIDs or handles required** - This phase only modifies existing spell flags.

---

## Testing Plan

### Test 1: Gimeitaro's Shield (No Concentration)

**Steps:**
1. Load save with Staff of Gimeitaro equipped
2. Cast Gimeitaro's Shield (bonus action)
3. Verify Silvered Bulwark buff is active
4. Cast another concentration spell (e.g., vanilla Haste on an ally)
5. **Verify:** Silvered Bulwark remains active (no concentration broken message)
6. **Verify:** Both buffs are active simultaneously

**Expected Result:** Silvered Bulwark persists while casting other concentration spells.

---

### Test 2: Celestial Haste (No Concentration)

**Steps:**
1. Load save with Staff of Gimeitaro equipped
2. Cast Celestial Haste (free action)
3. Verify Haste buff is active (extra action, movement, AC bonus)
4. Cast another concentration spell
5. **Verify:** Haste buff remains active
6. **Verify:** Both buffs are active simultaneously

**Expected Result:** Haste persists while casting other concentration spells.

---

### Test 3: Spirit Guardians (No Concentration)

**Steps:**
1. Load save with Staff of Gimeitaro equipped
2. Cast Gimeitaro's Spirit Guardians (free action, choose Radiant or Necrotic)
3. Verify Spirit Guardians aura is active (visual effect, damage to nearby enemies)
4. Cast another concentration spell
5. **Verify:** Spirit Guardians remains active
6. **Verify:** Both effects are active simultaneously

**Expected Result:** Spirit Guardians persists while casting other concentration spells.

---

### Test 4: Stack All Three Buffs

**Steps:**
1. Load save with Staff of Gimeitaro equipped
2. Cast Celestial Haste (free action)
3. Cast Gimeitaro's Spirit Guardians (free action)
4. Cast Gimeitaro's Shield (bonus action)
5. **Verify:** All three buffs are active simultaneously:
   - Haste icon visible (extra action available)
   - Spirit Guardians aura visible (damage to nearby enemies)
   - Silvered Bulwark buff visible (invulnerability active)
6. Engage in combat to verify all effects function correctly
7. **Verify:** No concentration management required

**Expected Result:** All three powerful buffs stack without any concentration conflicts, creating an extremely powerful combat state.

---

### Test 5: Duration and Re-casting

**Steps:**
1. With all three buffs active, wait for durations to expire (if any)
2. Re-cast any expired buffs
3. **Verify:** Can maintain all three buffs indefinitely with unlimited casts
4. **Verify:** No action economy issues (free actions for Haste/Guardians, bonus for Shield)

**Expected Result:** Player can easily maintain all three buffs throughout entire combats.

---

## Technical Notes

### Concentration Mechanics in BG3

**SpellFlags:** The `IsConcentration` flag in SpellFlags determines if a spell requires concentration.

**Vanilla Behavior:**
- Concentration spells have a blue glowing icon
- Casting a new concentration spell breaks the previous one
- Taking damage requires a Constitution save to maintain concentration

**Removing Concentration:**
- Simply remove `IsConcentration` from SpellFlags
- The spell behaves normally but doesn't occupy the concentration slot
- Duration still applies (if specified)

### Power Level Considerations

**This change is EXTREMELY POWERFUL:**
- Silvered Bulwark = Invulnerability to spells level 5 and below
- Haste = Extra action + doubled movement + +2 AC + advantage on DEX saves
- Spirit Guardians = 3d8 AoE damage per turn

**Combined Effect:**
- Near-invulnerable character (Shield)
- Doubled actions (Haste)
- Massive AoE damage (Spirit Guardians)
- All active simultaneously with no management required

**Balance Note:** This is appropriate for a level 21+ legendary item. The Staff of Gimeitaro becomes one of the most powerful items in the game, which fits its legendary status and level requirement.

---

## Dependencies

**This phase depends on:**
- Phase 054 (Complete) - Staff of Gimeitaro implementation with all three spells

**This phase affects:**
- Staff of Gimeitaro power level (significant increase)
- Player combat tactics (enables new strategies)
- Documentation (item catalog update)

---

## Success Criteria

- [x] Gimeitaro's Shield concentration restored (Revision 1)
- [x] Celestial Haste no longer requires concentration
- [x] Gimeitaro's Spirit Guardians no longer requires concentration
- [x] Haste and Spirit Guardians can be active simultaneously without conflicts
- [x] No errors or issues in-game (user tested)
- [x] Documentation updated to reflect changes
- [x] Phase document updated with implementation results

---

## Implementation Complete

**Date:** 2026-02-15

### Files Modified

**1. Spell_Target.txt**
- Removed `IsConcentration` from `L21_Target_GimeitarosShield_Unlimited`
- Changed: `data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsConcentration;IsSpell"`
- To: `data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsSpell"`

**2. Spell_Shout.txt (3 entries modified)**
- Removed `IsConcentration` from `L21_Shout_SpiritGuardians_Gimeitaro` (main container)
- Removed `IsConcentration` from `L21_Shout_SpiritGuardians_Gimeitaro_Radiant`
- Removed `IsConcentration` from `L21_Shout_SpiritGuardians_Gimeitaro_Necrotic`

**3. Spell_Shout.txt (verification)**
- Verified `L21_Shout_CelestialHaste_Unlimited` already has correct SpellFlags without `IsConcentration`
- No changes needed for Celestial Haste

**4. docs/level21gear/item_catalog.md**
- Updated spell list to note "NO CONCENTRATION" for three major buffs
- Added "Power Stacking" note explaining simultaneous buff capability
- Updated Implementation Status table
- Updated source notes and last updated date

### Summary of Changes

| Spell | Change Made | Result |
|-------|-------------|--------|
| Gimeitaro's Shield | Removed `IsConcentration` flag | No concentration required |
| Celestial Haste | Already correct (verified) | No concentration required |
| Spirit Guardians (all 3 variants) | Removed `IsConcentration` flag from all entries | No concentration required |

### Implementation Notes

1. **Celestial Haste** - Already had correct SpellFlags without concentration. The spell was inheriting from `Shout_MAG_Victory_Longbow_Haste` but our explicit SpellFlags override prevented concentration from being required.

2. **Spirit Guardians** - All three entries (main container, Radiant variant, Necrotic variant) required the flag removal to ensure no concentration at any level.

3. **Gimeitaro's Shield** - Single entry change removed concentration requirement.

**Result:** All three powerful buffs can now be stacked simultaneously:
- **Silvered Bulwark** - Invulnerability to low-level spells
- **Haste** - Extra action, doubled movement, +2 AC, advantage on DEX saves
- **Spirit Guardians** - 3d8 AoE damage per turn to nearby enemies

This creates an extremely powerful combat state appropriate for level 21+ characters.

### Status

**Implementation:** COMPLETE
**Testing:** Awaiting user confirmation

---

## Revision 1: Restore Concentration to Silvered Bulwark

**Issue:** User reconsidered - Silvered Bulwark should require concentration to maintain balance.

**Reasoning:**
- Silvered Bulwark provides invulnerability, which is extremely powerful
- Having invulnerability without concentration is too powerful even for level 21+
- Better balance to allow Haste + Spirit Guardians to stack (both powerful but not invulnerability)
- Maintains tactical decision-making: use Shield for temporary invulnerability, or other concentration spells

**Target State:**
- **Gimeitaro's Shield (Silvered Bulwark)** - REQUIRES concentration
- **Celestial Haste** - NO concentration
- **Spirit Guardians** - NO concentration

**Result:** Haste and Spirit Guardians can stack for offensive/mobility power, but invulnerability requires concentration management.

### Implementation

**File:** `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Target.txt`

**Change Required:**

**Find:**
```
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsSpell"
```

**Replace with:**
```
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsConcentration;IsSpell"
```

**Purpose:** Restores concentration requirement to Silvered Bulwark for better game balance.

### Files to Modify

| File | Action | Description |
|------|--------|-------------|
| `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Target.txt` | Edit | Add `IsConcentration` back to Gimeitaro's Shield |
| `docs/level21gear/item_catalog.md` | Edit | Update to show Shield requires concentration, Haste/Guardians don't |
| `docs/phases/Phase055.md` | Edit | Add Revision 1 section |

### Updated Power Stacking

**Concentration Spell:**
- Gimeitaro's Shield (Silvered Bulwark) - Requires concentration

**Non-Concentration Buffs (can stack with anything):**
- Celestial Haste - No concentration
- Spirit Guardians - No concentration

**Best Stacking Combinations:**
1. **Haste + Spirit Guardians** - Maximum offense (extra actions + AoE damage)
2. **Haste + Shield** - Maximum defense/mobility (extra actions + invulnerability)
3. **Spirit Guardians + Shield** - Tank mode (AoE damage + invulnerability)

**Status:** COMPLETE

### Revision 1 Implementation Complete

**Files Modified:**

1. **Spell_Target.txt**
   - Restored `IsConcentration` to `L21_Target_GimeitarosShield_Unlimited`
   - Changed: `data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsSpell"`
   - To: `data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsConcentration;IsSpell"`

2. **docs/level21gear/item_catalog.md**
   - Updated to show Shield requires concentration
   - Updated Power Stacking note to reflect Haste + Spirit Guardians can stack
   - Updated Implementation Status table

**Final State:**
- ✓ Gimeitaro's Shield - REQUIRES concentration
- ✓ Celestial Haste - NO concentration
- ✓ Spirit Guardians - NO concentration

**Result:** Better game balance - invulnerability requires concentration management, but offensive/mobility buffs (Haste + Spirit Guardians) can stack freely.

---

## Related Documentation

- **Phase 054** - Staff of Gimeitaro creation and implementation
- **Phase 054 Revision 2** - Addition of Silvered Bulwark, free action Haste, and Spirit Guardians
- **docs/level21gear/item_catalog.md** - Staff of Gimeitaro documentation

---

## Notes

### Design Rationale

The Staff of Gimeitaro is intended for level 21+ characters - well beyond the normal level cap. At this power level, concentration management becomes less interesting and more of an annoyance. Removing concentration from these three signature buffs:

1. **Simplifies gameplay** - No need to micromanage concentration
2. **Increases power appropriately** - Fits level 21+ expectations
3. **Enables unique playstyle** - Tank/support/damage hybrid
4. **Rewards the legendary item** - Makes it feel truly special

### Alternative Considered

**Keep concentration** - Would maintain vanilla balance but feels underwhelming for a level 21+ legendary staff. The unlimited casts are already powerful, but concentration limits prevent true power stacking.

**Decision:** Remove concentration to match the item's legendary status and level requirement.

---
