# Phase 001 - Ring of Spectral Power (Minimal)

**Status:** COMPLETE (2026-01-27)

## Goal
Create the Ring of Spectral Power with only the unlimited bonus action Magic Missile spell for initial testing.

## Scope
- Ring with single power: Unlimited Level 3 Magic Missile (bonus action)
- Delivered to Traveler's Chest via OneTimeRewards

## UUIDs and Handles

| Item | Type | Value |
|------|------|-------|
| Ring MapKey | UUID | `d4e5f6a7-b8c9-4d0e-a1b2-c3d4e5f6a7b8` |
| OneTimeReward | UUID | `e5f6a7b8-c9d0-4e1f-b2a3-d4e5f6a7b8c9` |
| Ring DisplayName | Handle | `ha1b2c3d4ge5f6g7a8bg9c0dg1e2f3a4b5c6d7` |
| Ring Description | Handle | `h1a2b3c4dg5e6fg7a8bg9c0dge1f2a3b4c5d6` |
| Spell DisplayName | Handle | `hb2c3d4e5gf6a7g8b9cga0d1g2e3f4a5b6c7d8` |
| Spell ExtraDescription | Handle | `h2b3c4d5eg6f7ag8b9cg0a1dg3e4f5a6b7c8d9` |

---

## Files Modified

### 1. Stats/Generated/Data/Spell_Projectile.txt
- [x] Added `SMR_Projectile_MagicMissile_Unlimited_Lvl3` spell entry

### 2. Localization/English/SampleMagicRingMod.xml
- [x] Added Ring DisplayName: "Ring of Spectral Power"
- [x] Added Ring Description
- [x] Added Spell DisplayName: "Spectral Barrage"
- [x] Added Spell ExtraDescription

### 3. RootTemplates/merged.lsx
- [x] Added GameObjects node for SMR_Ring_Spectral_Power

### 4. Stats/Generated/Data/Armor.txt
- [x] Added SMR_Ring_Spectral_Power entry (Legendary, 750 gold)

### 5. OneTimeRewards/OneTimeRewards.lsx
- [x] Added OneTimeReward entry for the ring

---

## Implementation Complete

All files have been modified. Ready for build and test.

---

## Test Plan
- [x] Build mod with BG3 Modder's Multitool
- [x] Load game with mod enabled
- [x] Go to camp and check Traveler's Chest
- [x] Equip ring
- [x] Verify "Spectral Barrage" spell appears
- [x] Cast spell - should cost bonus action, no spell slot
- [x] Verify 5 missiles fire (Level 3)

## Lessons Learned
- Must update BOTH `.xml` and `.loca.xml` localization files
- Must update BOTH `merged.lsx` and `merged.lsf.lsx` RootTemplates files
- Handle format: `h` + 8 hex + `g` + 4 hex + `g` + 4 hex + `g` + 4 hex + `g` + 12 hex (exactly)
