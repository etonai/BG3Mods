# Phase 003 - Add Unlimited Misty Step

**Status:** COMPLETE (2026-01-27)

## Goal
Add unlimited Misty Step to the Ring of Spectral Power.

## Scope
- New spell: Spectral Step (Misty Step, unlimited casting)
- Update ring to grant this spell
- Update ring description

## UUIDs and Handles Needed

| Item | Type | Value |
|------|------|-------|
| MistyStep DisplayName | Handle | `hd4e5f6a7gb8c9g0d1ega2b3g6c7d8e9f0a1b2` |
| MistyStep ExtraDescription | Handle | `h4d5e6f7ag8b9cg1d0eg3a2bg7c8d9e0f1a2b3` |

---

## Files to Modify

### 1. Stats/Generated/Data/Spell_Target.txt

Add Misty Step spell entry:
```
new entry "SMR_Target_MistyStep_Unlimited"
type "SpellData"
data "SpellType" "Target"
using "Target_MistyStep"
data "DisplayName" "hd4e5f6a7gb8c9g0d1ega2b3g6c7d8e9f0a1b2;1"
data "ExtraDescription" "h4d5e6f7ag8b9cg1d0eg3a2bg7c8d9e0f1a2b3;1"
data "UseCosts" ""
```

### 2. Stats/Generated/Data/Armor.txt

Update SMR_Ring_Spectral_Power Boosts to add the new spell:
```
data "Boosts" "UnlockSpell(SMR_Projectile_MagicMissile_Unlimited_Lvl3);UnlockSpell(SMR_Target_GlobeOfInvulnerability_ShortRest);UnlockSpell(SMR_Target_MistyStep_Unlimited)"
```

### 3. Localization/English/SampleMagicRingMod.xml

Add 2 content entries:
```xml
<content contentuid="hd4e5f6a7gb8c9g0d1ega2b3g6c7d8e9f0a1b2" version="1">Spectral Step</content>
<content contentuid="h4d5e6f7ag8b9cg1d0eg3a2bg7c8d9e0f1a2b3" version="1">Unlimited casting from Ring of Spectral Power.</content>
```

### 4. Localization/English/SampleMagicRingMod.loca.xml

Add same 2 content entries (IMPORTANT: must update both files!)

### 5. Update Ring Description (both .xml and .loca.xml)

Update the ring description to mention the new power:
- Old: "A ring crackling with arcane force. Grants unlimited Magic Missile as a bonus action and Globe of Invulnerability once per short rest."
- New: "A ring crackling with arcane force. Grants unlimited Misty Step, unlimited Magic Missile as a bonus action, and Globe of Invulnerability once per short rest."

---

## Implementation Order

1. [x] Add Misty Step spell to Spell_Target.txt
2. [x] Add localization entries to SampleMagicRingMod.xml
3. [x] Add localization entries to SampleMagicRingMod.loca.xml
4. [x] Update ring description in both localization files
5. [x] Update ring Boosts in Armor.txt
6. [x] Build and test mod

---

## Test Plan

- [ ] Build mod with BG3 Modder's Multitool
- [ ] Load game with mod enabled
- [ ] Equip Ring of Spectral Power
- [ ] Verify "Spectral Step" spell appears in spell list
- [ ] Cast spell - should teleport character
- [ ] Verify no spell slot consumed
- [ ] Verify can cast multiple times per turn
- [ ] Verify ring description updated

---

## Notes

- Misty Step is a **Target** type spell
- Base spell: `Target_MistyStep`
- Based on lessons from Phase 001 and 002:
  - Must update BOTH `.xml` and `.loca.xml` localization files
  - Handle format: `h` + 8 hex + `g` + 4 hex + `g` + 4 hex + `g` + 4 hex + `g` + 12 hex
