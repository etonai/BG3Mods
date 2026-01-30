# Phase 005 - Add All Remaining Powers to Both Rings

**Status:** COMPLETE

## Goal
1. Add all remaining powers to the Ring of Spectral Power
2. Add all remaining powers to the Ring of the Guardian

## Scope

### Ring of Spectral Power
Add all remaining powers:
- Unlimited Shield (bonus action)
- Unlimited Counterspell (bonus action)
- Unlimited Hold Person (bonus action)
- Artistry of War (once per short rest)
- Invisibility (once per short rest)
- Unlimited Knock (bonus action)
- Arcane Gate (once per short rest)

### Ring of the Guardian
Add all remaining powers:
- Unlimited Bless
- Unlimited Create Water (bonus action)
- Lesser Restoration (once per short rest)
- Greater Restoration (once per long rest)
- Freedom of Movement (once per short rest)
- Counterspell (once per short rest)
- Heroes' Feast (once per long rest)

## UUIDs and Handles Needed

### Ring of Spectral Power

| Item | Type | Value |
|------|------|-------|
| Shield DisplayName | Handle | `hf6a7b8c9gd0e1g2f3ag4b5cga0b1c2d3e4f5a6` |
| Shield ExtraDescription | Handle | `h6f7a8b9cg0d1eg3f2ag5b4cg1a0b2c3d4e5f6a7` |
| Counterspell DisplayName | Handle | `h4b5c6d7eg8f9ag0b1cg2d3eg5f6a7b8c9d0e1f2` |
| Counterspell ExtraDescription | Handle | `hb5c6d7e8g9f0ag1b2cg3d4eg6f7a8b9c0d1e2f3` |
| HoldPerson DisplayName | Handle | `h5c6d7e8fg0a1bg2c3dg4e5fg7a8b9c0d1e2f3a4` |
| HoldPerson ExtraDescription | Handle | `hc6d7e8f9g1a2bg3c4dg5e6fg8a9b0c1d2e3f4a5` |
| ArtistryOfWar DisplayName | Handle | `h6d7e8f9ag2b3cg4d5eg6f7ag9b0c1d2e3f4a5b6` |
| ArtistryOfWar ExtraDescription | Handle | `hd7e8f9a0g3b4cg5d6eg7f8ag0b1c2d3e4f5a6b7` |
| Invisibility DisplayName | Handle | `h7e8f9a0bg4c5dg6e7fg8a9bg1c2d3e4f5a6b7c8` |
| Invisibility ExtraDescription | Handle | `he8f9a0b1g5c6dg7e8fg9a0bg2c3d4e5f6a7b8c9` |
| Knock DisplayName | Handle | `h8f9a0b1cg6d7eg8f9ag0b1cg3d4e5f6a7b8c9d0` |
| Knock ExtraDescription | Handle | `hf9a0b1c2g7d8eg9f0ag1b2cg4d5e6f7a8b9c0d1` |
| ArcaneGate DisplayName | Handle | `h9a0b1c2dg8e9fg0a1bg2c3dg5e6f7a8b9c0d1e2` |
| ArcaneGate ExtraDescription | Handle | `ha0b1c2d3g9e0fg1a2bg3c4dg6e7f8a9b0c1d2e3` |

### Ring of the Guardian

| Item | Type | Value |
|------|------|-------|
| Bless DisplayName | Handle | `h7a8b9c0dge1f2g3a4bg5c6dg2a3b4c5d6e7f8a9` |
| Bless ExtraDescription | Handle | `ha8b9c0d1gf2e3g4a5bg6c7dg3a4b5c6d7e8f9a0` |
| CreateWater DisplayName | Handle | `h8b9c0d1eg2f3ag5b4cg7d6eg4b5c6d7e8f9a0b1` |
| CreateWater ExtraDescription | Handle | `hb9c0d1e2g3f4ag6b5cg8d7eg5b6c7d8e9f0a1b2` |
| LesserRestoration DisplayName | Handle | `h9c0d1e2fg4a5bg7c6dg9e8fg6c7d8e9f0a1b2c3` |
| LesserRestoration ExtraDescription | Handle | `hc0d1e2f3g5a6bg8c7dg0e9fg7c8d9e0f1a2b3c4` |
| GreaterRestoration DisplayName | Handle | `h0d1e2f3ag6b7cg9d8eg1f0ag8d9e0f1a2b3c4d5` |
| GreaterRestoration ExtraDescription | Handle | `hd1e2f3a4g7b8cg0d9eg2f1ag9d0e1f2a3b4c5d6` |
| FreedomOfMovement DisplayName | Handle | `h1e2f3a4bg8c9dg1e0fg3a2bg0e1f2a3b4c5d6e7` |
| FreedomOfMovement ExtraDescription | Handle | `he2f3a4b5g9c0dg2e1fg4a3bg1e2f3a4b5c6d7e8` |
| Counterspell DisplayName | Handle | `h2f3a4b5cg0d1eg3f2ag5b4cg2f3a4b5c6d7e8f9` |
| Counterspell ExtraDescription | Handle | `hf3a4b5c6g1d2eg4f3ag6b5cg3f4a5b6c7d8e9f0` |
| HeroesFeast DisplayName | Handle | `h3a4b5c6dg2e3fg5a4bg7c6dg4a5b6c7d8e9f0a1` |
| HeroesFeast ExtraDescription | Handle | `ha4b5c6d7g3e4fg6a5bg8c7dg5a6b7c8d9e0f1a2` |

---

## Ring of Spectral Power - Files to Modify

### 1. Stats/Generated/Data/Spell_Shout.txt

Add Shield and Counterspell spells (Shout type - reactions):
```
new entry "SMR_Shout_Shield_Unlimited"
type "SpellData"
data "SpellType" "Shout"
using "Shout_Shield"
data "DisplayName" "hf6a7b8c9gd0e1g2f3ag4b5cga0b1c2d3e4f5a6;1"
data "ExtraDescription" "h6f7a8b9cg0d1eg3f2ag5b4cg1a0b2c3d4e5f6a7;1"
data "UseCosts" "BonusActionPoint:1"

new entry "SMR_Shout_Counterspell_Unlimited"
type "SpellData"
data "SpellType" "Shout"
using "Shout_Counterspell"
data "DisplayName" "h4b5c6d7eg8f9ag0b1cg2d3eg5f6a7b8c9d0e1f2;1"
data "ExtraDescription" "hb5c6d7e8g9f0ag1b2cg3d4eg6f7a8b9c0d1e2f3;1"
data "UseCosts" "BonusActionPoint:1"

new entry "SMR_Shout_ArtistryOfWar_ShortRest"
type "SpellData"
data "SpellType" "Shout"
using "Shout_ArtistryOfWar"
data "DisplayName" "h6d7e8f9ag2b3cg4d5eg6f7ag9b0c1d2e3f4a5b6;1"
data "ExtraDescription" "hd7e8f9a0g3b4cg5d6eg7f8ag0b1c2d3e4f5a6b7;1"
data "UseCosts" ""
data "Cooldown" "OncePerShortRest"
```

### 2. Stats/Generated/Data/Spell_Target.txt

Add Hold Person, Invisibility, Knock, and Arcane Gate spells:
```
new entry "SMR_Target_HoldPerson_Unlimited"
type "SpellData"
data "SpellType" "Target"
using "Target_HoldPerson"
data "DisplayName" "h5c6d7e8fg0a1bg2c3dg4e5fg7a8b9c0d1e2f3a4;1"
data "ExtraDescription" "hc6d7e8f9g1a2bg3c4dg5e6fg8a9b0c1d2e3f4a5;1"
data "UseCosts" "BonusActionPoint:1"

new entry "SMR_Target_Invisibility_ShortRest"
type "SpellData"
data "SpellType" "Target"
using "Target_Invisibility"
data "DisplayName" "h7e8f9a0bg4c5dg6e7fg8a9bg1c2d3e4f5a6b7c8;1"
data "ExtraDescription" "he8f9a0b1g5c6dg7e8fg9a0bg2c3d4e5f6a7b8c9;1"
data "UseCosts" ""
data "Cooldown" "OncePerShortRest"

new entry "SMR_Target_Knock_Unlimited"
type "SpellData"
data "SpellType" "Target"
using "Target_Knock"
data "DisplayName" "h8f9a0b1cg6d7eg8f9ag0b1cg3d4e5f6a7b8c9d0;1"
data "ExtraDescription" "hf9a0b1c2g7d8eg9f0ag1b2cg4d5e6f7a8b9c0d1;1"
data "UseCosts" "BonusActionPoint:1"

new entry "SMR_Target_ArcaneGate_ShortRest"
type "SpellData"
data "SpellType" "Target"
using "Target_ArcaneGate"
data "DisplayName" "h9a0b1c2dg8e9fg0a1bg2c3dg5e6f7a8b9c0d1e2;1"
data "ExtraDescription" "ha0b1c2d3g9e0fg1a2bg3c4dg6e7f8a9b0c1d2e3;1"
data "UseCosts" ""
data "Cooldown" "OncePerShortRest"
```

### 3. Stats/Generated/Data/Armor.txt

Update SMR_Ring_Spectral_Power Boosts to add all new spells:
```
data "Boosts" "UnlockSpell(SMR_Projectile_MagicMissile_Unlimited_Lvl3);UnlockSpell(SMR_Target_GlobeOfInvulnerability_ShortRest);UnlockSpell(SMR_Target_MistyStep_Unlimited);UnlockSpell(SMR_Shout_Shield_Unlimited);UnlockSpell(SMR_Shout_Counterspell_Unlimited);UnlockSpell(SMR_Target_HoldPerson_Unlimited);UnlockSpell(SMR_Shout_ArtistryOfWar_ShortRest);UnlockSpell(SMR_Target_Invisibility_ShortRest);UnlockSpell(SMR_Target_Knock_Unlimited);UnlockSpell(SMR_Target_ArcaneGate_ShortRest)"
```

### 4. Localization/English/SampleMagicRingMod.xml

Add all Ring of Spectral Power spell entries:
```xml
<content contentuid="hf6a7b8c9gd0e1g2f3ag4b5cga0b1c2d3e4f5a6" version="1">Spectral Shield</content>
<content contentuid="h6f7a8b9cg0d1eg3f2ag5b4cg1a0b2c3d4e5f6a7" version="1">Unlimited Shield as a bonus action from Ring of Spectral Power.</content>
<content contentuid="h4b5c6d7eg8f9ag0b1cg2d3eg5f6a7b8c9d0e1f2" version="1">Spectral Counter</content>
<content contentuid="hb5c6d7e8g9f0ag1b2cg3d4eg6f7a8b9c0d1e2f3" version="1">Unlimited Counterspell as a bonus action from Ring of Spectral Power.</content>
<content contentuid="h5c6d7e8fg0a1bg2c3dg4e5fg7a8b9c0d1e2f3a4" version="1">Spectral Hold</content>
<content contentuid="hc6d7e8f9g1a2bg3c4dg5e6fg8a9b0c1d2e3f4a5" version="1">Unlimited Hold Person as a bonus action from Ring of Spectral Power.</content>
<content contentuid="h6d7e8f9ag2b3cg4d5eg6f7ag9b0c1d2e3f4a5b6" version="1">Spectral Artistry</content>
<content contentuid="hd7e8f9a0g3b4cg5d6eg7f8ag0b1c2d3e4f5a6b7" version="1">Artistry of War. Recharges on short rest.</content>
<content contentuid="h7e8f9a0bg4c5dg6e7fg8a9bg1c2d3e4f5a6b7c8" version="1">Spectral Veil</content>
<content contentuid="he8f9a0b1g5c6dg7e8fg9a0bg2c3d4e5f6a7b8c9" version="1">Invisibility. Recharges on short rest.</content>
<content contentuid="h8f9a0b1cg6d7eg8f9ag0b1cg3d4e5f6a7b8c9d0" version="1">Spectral Knock</content>
<content contentuid="hf9a0b1c2g7d8eg9f0ag1b2cg4d5e6f7a8b9c0d1" version="1">Unlimited Knock as a bonus action from Ring of Spectral Power.</content>
<content contentuid="h9a0b1c2dg8e9fg0a1bg2c3dg5e6f7a8b9c0d1e2" version="1">Spectral Gate</content>
<content contentuid="ha0b1c2d3g9e0fg1a2bg3c4dg6e7f8a9b0c1d2e3" version="1">Arcane Gate. Recharges on short rest.</content>
```

### 5. Localization/English/SampleMagicRingMod.loca.xml

Add same entries (IMPORTANT: must update both files!)

### 6. Update Ring of Spectral Power Description (both .xml and .loca.xml)

Update the ring description to mention all powers.

---

## Ring of the Guardian - Files to Modify

### 1. Stats/Generated/Data/Spell_Shout.txt

Add Bless and Counterspell spells:
```
new entry "SMR_Shout_Bless_Unlimited"
type "SpellData"
data "SpellType" "Shout"
using "Shout_Bless"
data "DisplayName" "h7a8b9c0dge1f2g3a4bg5c6dg2a3b4c5d6e7f8a9;1"
data "ExtraDescription" "ha8b9c0d1gf2e3g4a5bg6c7dg3a4b5c6d7e8f9a0;1"
data "UseCosts" ""

new entry "SMR_Shout_Counterspell_ShortRest"
type "SpellData"
data "SpellType" "Shout"
using "Shout_Counterspell"
data "DisplayName" "h2f3a4b5cg0d1eg3f2ag5b4cg2f3a4b5c6d7e8f9;1"
data "ExtraDescription" "hf3a4b5c6g1d2eg4f3ag6b5cg3f4a5b6c7d8e9f0;1"
data "UseCosts" ""
data "Cooldown" "OncePerShortRest"
```

### 2. Stats/Generated/Data/Spell_Target.txt

Add remaining target spells:
```
new entry "SMR_Target_CreateWater_Unlimited"
type "SpellData"
data "SpellType" "Target"
using "Target_CreateOrDestroyWater_Create"
data "DisplayName" "h8b9c0d1eg2f3ag5b4cg7d6eg4b5c6d7e8f9a0b1;1"
data "ExtraDescription" "hb9c0d1e2g3f4ag6b5cg8d7eg5b6c7d8e9f0a1b2;1"
data "UseCosts" "BonusActionPoint:1"

new entry "SMR_Target_LesserRestoration_ShortRest"
type "SpellData"
data "SpellType" "Target"
using "Target_LesserRestoration"
data "DisplayName" "h9c0d1e2fg4a5bg7c6dg9e8fg6c7d8e9f0a1b2c3;1"
data "ExtraDescription" "hc0d1e2f3g5a6bg8c7dg0e9fg7c8d9e0f1a2b3c4;1"
data "UseCosts" ""
data "Cooldown" "OncePerShortRest"

new entry "SMR_Target_GreaterRestoration_LongRest"
type "SpellData"
data "SpellType" "Target"
using "Target_GreaterRestoration"
data "DisplayName" "h0d1e2f3ag6b7cg9d8eg1f0ag8d9e0f1a2b3c4d5;1"
data "ExtraDescription" "hd1e2f3a4g7b8cg0d9eg2f1ag9d0e1f2a3b4c5d6;1"
data "UseCosts" ""
data "Cooldown" "OncePerLongRest"

new entry "SMR_Target_FreedomOfMovement_ShortRest"
type "SpellData"
data "SpellType" "Target"
using "Target_FreedomOfMovement"
data "DisplayName" "h1e2f3a4bg8c9dg1e0fg3a2bg0e1f2a3b4c5d6e7;1"
data "ExtraDescription" "he2f3a4b5g9c0dg2e1fg4a3bg1e2f3a4b5c6d7e8;1"
data "UseCosts" ""
data "Cooldown" "OncePerShortRest"

new entry "SMR_Target_HeroesFeast_LongRest"
type "SpellData"
data "SpellType" "Target"
using "Target_HeroesFeast"
data "DisplayName" "h3a4b5c6dg2e3fg5a4bg7c6dg4a5b6c7d8e9f0a1;1"
data "ExtraDescription" "ha4b5c6d7g3e4fg6a5bg8c7dg5a6b7c8d9e0f1a2;1"
data "UseCosts" ""
data "Cooldown" "OncePerLongRest"
```

### 3. Stats/Generated/Data/Armor.txt

Update SMR_Ring_Guardian Boosts:
```
data "Boosts" "UnlockSpell(SMR_Target_HealingWord_Superior);UnlockSpell(SMR_Shout_Bless_Unlimited);UnlockSpell(SMR_Target_CreateWater_Unlimited);UnlockSpell(SMR_Target_LesserRestoration_ShortRest);UnlockSpell(SMR_Target_GreaterRestoration_LongRest);UnlockSpell(SMR_Target_FreedomOfMovement_ShortRest);UnlockSpell(SMR_Shout_Counterspell_ShortRest);UnlockSpell(SMR_Target_HeroesFeast_LongRest)"
```

### 4. Localization Files (both .xml and .loca.xml)

Add all Ring of the Guardian spell entries:
```xml
<content contentuid="h7a8b9c0dge1f2g3a4bg5c6dg2a3b4c5d6e7f8a9" version="1">Guardian's Blessing</content>
<content contentuid="ha8b9c0d1gf2e3g4a5bg6c7dg3a4b5c6d7e8f9a0" version="1">Unlimited casting from Ring of the Guardian.</content>
<content contentuid="h8b9c0d1eg2f3ag5b4cg7d6eg4b5c6d7e8f9a0b1" version="1">Guardian's Water</content>
<content contentuid="hb9c0d1e2g3f4ag6b5cg8d7eg5b6c7d8e9f0a1b2" version="1">Unlimited Create Water as a bonus action from Ring of the Guardian.</content>
<content contentuid="h9c0d1e2fg4a5bg7c6dg9e8fg6c7d8e9f0a1b2c3" version="1">Guardian's Restoration</content>
<content contentuid="hc0d1e2f3g5a6bg8c7dg0e9fg7c8d9e0f1a2b3c4" version="1">Lesser Restoration. Recharges on short rest.</content>
<content contentuid="h0d1e2f3ag6b7cg9d8eg1f0ag8d9e0f1a2b3c4d5" version="1">Guardian's Greater Restoration</content>
<content contentuid="hd1e2f3a4g7b8cg0d9eg2f1ag9d0e1f2a3b4c5d6" version="1">Greater Restoration. Recharges on long rest.</content>
<content contentuid="h1e2f3a4bg8c9dg1e0fg3a2bg0e1f2a3b4c5d6e7" version="1">Guardian's Freedom</content>
<content contentuid="he2f3a4b5g9c0dg2e1fg4a3bg1e2f3a4b5c6d7e8" version="1">Freedom of Movement. Recharges on short rest.</content>
<content contentuid="h2f3a4b5cg0d1eg3f2ag5b4cg2f3a4b5c6d7e8f9" version="1">Guardian's Counter</content>
<content contentuid="hf3a4b5c6g1d2eg4f3ag6b5cg3f4a5b6c7d8e9f0" version="1">Counterspell. Recharges on short rest.</content>
<content contentuid="h3a4b5c6dg2e3fg5a4bg7c6dg4a5b6c7d8e9f0a1" version="1">Guardian's Feast</content>
<content contentuid="ha4b5c6d7g3e4fg6a5bg8c7dg5a6b7c8d9e0f1a2" version="1">Heroes' Feast. Recharges on long rest.</content>
```

### 5. Update Ring of the Guardian Description (both .xml and .loca.xml)

Update description to reflect all powers.

---

## Implementation Order

### Ring of Spectral Power
1. [x] Add Shield, Counterspell, Artistry of War spells to Spell_Shout.txt (create file if needed)
2. [x] Add Hold Person, Invisibility, Knock, Arcane Gate spells to Spell_Target.txt
3. [x] Add all Ring of Spectral Power localization entries to SampleMagicRingMod.xml
4. [x] Add all Ring of Spectral Power localization entries to SampleMagicRingMod.loca.xml
5. [x] Update Ring of Spectral Power description in both localization files
6. [x] Update Ring of Spectral Power Boosts in Armor.txt

### Ring of the Guardian
7. [x] Add Bless and Counterspell spells to Spell_Shout.txt
8. [x] Add Create Water, Lesser/Greater Restoration, Freedom of Movement, Heroes' Feast to Spell_Target.txt
9. [x] Add all Ring of the Guardian localization entries to SampleMagicRingMod.xml
10. [x] Add all Ring of the Guardian localization entries to SampleMagicRingMod.loca.xml
11. [x] Update Ring of the Guardian description in both localization files
12. [x] Update Ring of the Guardian Boosts in Armor.txt

### Final
13. [ ] Build and test mod

---

## Test Plan

### Ring of Spectral Power
- [ ] Build mod with BG3 Modder's Multitool
- [ ] Load game with mod enabled
- [ ] Equip Ring of Spectral Power
- [ ] Verify all new spells appear:
  - [ ] Spectral Shield (Shield) - bonus action, unlimited
  - [ ] Spectral Counter (Counterspell) - bonus action, unlimited
  - [ ] Spectral Hold (Hold Person) - bonus action, unlimited
  - [ ] Spectral Artistry (Artistry of War) - once per short rest
  - [ ] Spectral Veil (Invisibility) - once per short rest
  - [ ] Spectral Knock (Knock) - bonus action, unlimited
  - [ ] Spectral Gate (Arcane Gate) - once per short rest
- [ ] Test each spell functions correctly
- [ ] Verify cooldowns work as expected
- [ ] Verify ring description updated

### Ring of the Guardian
- [ ] Equip Ring of the Guardian
- [ ] Verify all new spells appear:
  - [ ] Guardian's Blessing (Bless) - unlimited
  - [ ] Guardian's Water (Create Water) - bonus action, unlimited
  - [ ] Guardian's Restoration (Lesser Restoration) - once per short rest
  - [ ] Guardian's Greater Restoration - once per long rest
  - [ ] Guardian's Freedom (Freedom of Movement) - once per short rest
  - [ ] Guardian's Counter (Counterspell) - once per short rest
  - [ ] Guardian's Feast (Heroes' Feast) - once per long rest
- [ ] Test each spell functions correctly
- [ ] Verify cooldowns work as expected
- [ ] Verify ring description updated

---

## Bugged Powers (Placeholder Icon / Not Working)

### Ring of Spectral Power
- [x] **Spectral Shield** (Shield) - bonus action, unlimited - **FIXED (Interrupt system)**
- [x] **Spectral Counter** (Counterspell) - bonus action, unlimited - **FIXED (Interrupt system)**
- [ ] **Spectral Artistry** (Artistry of War) - once per short rest - **STILL BROKEN** (tried Projectile_ArtistryOfWar, not working)
- [x] **Spectral Gate** (Arcane Gate) - once per short rest - **FIXED (Teleportation_ArcaneGate, not Target_ArcaneGate)**

### Ring of the Guardian
- [x] **Guardian's Blessing** (Bless) - unlimited - **FIXED (Target_Bless, not Shout_Bless)**
- [x] **Guardian's Water** (Create Water) - bonus action, unlimited - **FIXED (Target_CreateWater, not Target_CreateOrDestroyWater_Create)**
- [x] **Guardian's Counter** (Counterspell) - once per short rest - **FIXED (Interrupt system)**
- [x] **Guardian's Feast** (Heroes' Feast) - once per long rest - **FIXED (Shout_HeroesFeast, not Target_HeroesFeast)**

### Working Powers (Confirmed)
- Spectral Hold (Hold Person)
- Spectral Veil (Invisibility)
- Spectral Knock (Knock)
- Guardian's Restoration (Lesser Restoration)
- Guardian's Greater Restoration (Greater Restoration)
- Guardian's Freedom (Freedom of Movement)

---

## Bug Fixes

### Shield & Counterspell Fix (2026-01-27)

**Root Cause:** Shield and Counterspell are REACTION spells in BG3. Reaction spells use the **Interrupt** system, not the regular Spell system. Using `Shout_Shield` or `Shout_Counterspell` with `UnlockSpell()` is incorrect.

**Discovery:** Analyzed grannylootrings mod which correctly uses:
```
data "Boosts" "UnlockInterrupt(Interrupt_Counterspell);ActionResource(ReactionActionPoint,1,0);"
```

**Solution:**
1. Created `Stats/Generated/Data/Interrupt.txt` with custom interrupt definitions:
   - `SMR_Interrupt_Shield_Unlimited` - uses `Interrupt_Shield_Wizard` as base, cost changed to `BonusActionPoint:1`
   - `SMR_Interrupt_Counterspell_Unlimited` - uses `Interrupt_Counterspell` as base, cost changed to `BonusActionPoint:1`
   - `SMR_Interrupt_Counterspell_ShortRest` - uses `Interrupt_Counterspell` as base, normal reaction cost with `OncePerShortRest` cooldown

2. Updated `Armor.txt` to use `UnlockInterrupt()` instead of `UnlockSpell()`:
   - Ring of Spectral Power: `UnlockInterrupt(SMR_Interrupt_Shield_Unlimited);UnlockInterrupt(SMR_Interrupt_Counterspell_Unlimited)`
   - Ring of Guardian: `UnlockInterrupt(SMR_Interrupt_Counterspell_ShortRest)`

3. Removed incorrect entries from `Spell_Shout.txt`:
   - Deleted `SMR_Shout_Shield_Unlimited`
   - Deleted `SMR_Shout_Counterspell_Unlimited`
   - Deleted `SMR_Shout_Counterspell_ShortRest`

### Bless Fix (2026-01-27)

**Root Cause:** Bless is a `Target` type spell, not a `Shout` type spell. The SpellSet.txt shows `Target_Bless`.

**Solution:**
1. Created `SMR_Target_Bless_Unlimited` in `Spell_Target.txt` using `Target_Bless`
2. Removed `SMR_Shout_Bless_Unlimited` from `Spell_Shout.txt`
3. Updated `Armor.txt` to use `UnlockSpell(SMR_Target_Bless_Unlimited)`

### Create Water Fix (2026-01-27)

**Root Cause:** The base spell is `Target_CreateWater`, not `Target_CreateOrDestroyWater_Create`.

**Solution:** Changed `using "Target_CreateOrDestroyWater_Create"` to `using "Target_CreateWater"` in `Spell_Target.txt`

### Heroes' Feast Fix (2026-01-27)

**Root Cause:** Heroes' Feast is a `Shout` type spell, not a `Target` type spell. The grannylootrings mod uses `Shout_HeroesFeast`.

**Solution:**
1. Created `SMR_Shout_HeroesFeast_LongRest` in `Spell_Shout.txt` using `Shout_HeroesFeast`
2. Removed `SMR_Target_HeroesFeast_LongRest` from `Spell_Target.txt`
3. Updated `Armor.txt` to use `UnlockSpell(SMR_Shout_HeroesFeast_LongRest)`

### Artistry of War Attempted Fix (2026-01-27) - STILL BROKEN

**Attempted Solution:** Changed from `Shout` to `Projectile` type spell using `Projectile_ArtistryOfWar`.

**Status:** Still not working. Deferred for future investigation.

### Arcane Gate Fix (2026-01-27)

**Root Cause:** Arcane Gate is a `Teleportation` type spell, not a `Target` type spell. The grannylootrings mod (Doorstep ring) uses `Teleportation_ArcaneGate`.

**Solution:**
1. Created `Spell_Teleportation.txt` with `SMR_Teleportation_ArcaneGate_ShortRest` using `Teleportation_ArcaneGate`
2. Removed `SMR_Target_ArcaneGate_ShortRest` from `Spell_Target.txt`
3. Updated `Armor.txt` to use `UnlockSpell(SMR_Teleportation_ArcaneGate_ShortRest)`

---

## Notes

- **IMPORTANT:** Shield and Counterspell are REACTION spells that use the Interrupt system, not the Shout spell system
- Use `UnlockInterrupt(Interrupt_X)` for reaction abilities, not `UnlockSpell(Shout_X)`
- Base interrupts: `Interrupt_Shield_Wizard`, `Interrupt_Counterspell`
- To change action cost: use `Cost` field in InterruptData (e.g., `BonusActionPoint:1` instead of `ReactionActionPoint:1`)
- To add cooldown: use `Cooldown` field (e.g., `OncePerShortRest`)
- Based on lessons from previous phases:
  - Must update BOTH `.xml` and `.loca.xml` localization files
  - Handle format: `h` + 8 hex + `g` + 4 hex + `g` + 4 hex + `g` + 4 hex + `g` + 12 hex

---

## Known Issues

### Artistry of War - NOT WORKING
- **Spell:** Spectral Artistry (Artistry of War) on Ring of Spectral Power
- **Status:** Still showing placeholder icon / not functioning
- **Attempted fixes:**
  - Changed from Shout type to Projectile type
  - Used `Projectile_ArtistryOfWar` as base spell
- **Deferred:** For future investigation
