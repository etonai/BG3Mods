# Phase 009 - Testing and Verification

**Status:** COMPLETE

## Goal
Verify existing functionality and fix any issues found.

---

## Part 1: Verify Misty Step on Ring of Spectral Power

### Expected Behavior
- Misty Step can be cast an unlimited number of times
- No action cost (not a bonus action, not an action - completely free)
- No cooldown

### Current Implementation

From `Spell_Target.txt`:
```
new entry "SMR_Target_MistyStep_Unlimited"
type "SpellData"
data "SpellType" "Target"
using "Target_MistyStep"
data "DisplayName" "hd4e5f6a7gb8c9g0d1ega2b3g6c7d8e9f0a1b2;1"
data "ExtraDescription" "h4d5e6f7ag8b9cg1d0eg3a2bg7c8d9e0f1a2b3;1"
data "UseCosts" ""
```

### Verification
- `UseCosts` is empty - should mean no action cost
- No `Cooldown` field - should mean unlimited uses

### Test Plan
- [ ] Equip Ring of Spectral Power
- [ ] Verify Misty Step appears in spell list
- [ ] Cast Misty Step and verify it works
- [ ] Verify no action point is consumed (action and bonus action remain available)
- [ ] Cast Misty Step multiple times in the same turn
- [ ] Verify it can be cast again after ending turn (no cooldown)

### If Issues Found
If Misty Step is consuming an action or has a cooldown:
1. Check if `Target_MistyStep` base spell has default UseCosts that need to be overridden
2. May need to explicitly set `data "Cooldown" ""` to remove any inherited cooldown
3. Verify the spell is properly referenced in the ring's Boosts

---

## Part 2: Make Artistry of War Unlimited

### Overview
Change Artistry of War on Ring of Spectral Power from once per short rest to unlimited.

### Changes Made

#### 1. Stats/Generated/Data/Spell_Projectile.txt
Renamed and updated spell:
```
new entry "SMR_Projectile_ArtistryOfWar_Unlimited"
type "SpellData"
data "SpellType" "Projectile"
using "Projectile_CursedTome_CurriculumofStrategy"
data "DisplayName" "h6d7e8f9ag2b3cg4d5eg6f7ag9b0c1d2e3f4a5b6;1"
data "ExtraDescription" "hd7e8f9a0g3b4cg5d6eg7f8ag0b1c2d3e4f5a6b7;1"
data "UseCosts" ""
```
- Removed `data "Cooldown" "OncePerShortRest"`

#### 2. Stats/Generated/Data/Armor.txt
Updated SMR_Ring_Spectral_Power to reference the renamed spell:
- Changed `UnlockSpell(SMR_Projectile_ArtistryOfWar_ShortRest)` to `UnlockSpell(SMR_Projectile_ArtistryOfWar_Unlimited)`

### Test Plan
- [ ] Equip Ring of Spectral Power
- [ ] Verify Artistry of War spell is available
- [ ] Cast Artistry of War and verify it works
- [ ] Cast Artistry of War again without resting (verify no cooldown)

---

## Implementation Order

1. [ ] Test Misty Step functionality as described above
2. [x] Make Artistry of War unlimited (implemented)

---

## Bugs Found During Testing

(None yet)

---

## Notes

- The spell currently inherits from `Target_MistyStep`
- Empty `UseCosts` should remove action cost
- No Cooldown field should allow unlimited casting
