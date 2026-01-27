# Phase 001 - Ring of Spectral Power (Minimal)

## Goal
Create the Ring of Spectral Power with only the unlimited bonus action Magic Missile spell for initial testing.

## Scope
- Ring with single power: Unlimited Level 3 Magic Missile (bonus action)
- Delivered to Traveler's Chest via OneTimeRewards

## UUIDs and Handles Needed

| Item | Type | Value |
|------|------|-------|
| Ring MapKey | UUID | `________-____-____-____-____________` |
| OneTimeReward | UUID | `________-____-____-____-____________` |
| Ring DisplayName | Handle | `h________________________________` |
| Ring Description | Handle | `h________________________________` |
| Spell DisplayName | Handle | `h________________________________` |
| Spell ExtraDescription | Handle | `h________________________________` |

---

## Files to Modify

### 1. RootTemplates/merged.lsx
Add new GameObjects node for the ring.

### 2. Stats/Generated/Data/Armor.txt
Add ring stats entry with `UnlockSpell(SMR_Projectile_MagicMissile_Unlimited_Lvl3)`.

### 3. Stats/Generated/Data/Spell_Projectile.txt
Add unlimited Magic Missile spell entry:
```
new entry "SMR_Projectile_MagicMissile_Unlimited_Lvl3"
type "SpellData"
data "SpellType" "Projectile"
using "Projectile_MagicMissile_3"
data "DisplayName" "[HANDLE];1"
data "ExtraDescription" "[HANDLE];1"
data "UseCosts" "BonusActionPoint:1"
```

### 4. Localization/English/SampleMagicRingMod.xml
Add 4 content entries:
- Ring DisplayName: "Ring of Spectral Power"
- Ring Description: "A ring crackling with arcane force. Grants unlimited Magic Missile as a bonus action."
- Spell DisplayName: "Spectral Barrage"
- Spell ExtraDescription: "Unlimited Level 3 Magic Missile as a bonus action."

### 5. OneTimeRewards/OneTimeRewards.lsx
Add new OneTimeReward node for the ring.

---

## Implementation Order

1. [ ] Generate 2 UUIDs and 4 handles
2. [ ] Add spell to Spell_Projectile.txt
3. [ ] Add localization entries to SampleMagicRingMod.xml
4. [ ] Add ring to merged.lsx
5. [ ] Add ring stats to Armor.txt
6. [ ] Add ring to OneTimeRewards.lsx
7. [ ] Build and test mod

---

## Test Plan
- Load game with mod enabled
- Go to camp and check Traveler's Chest
- Equip ring
- Verify "Spectral Barrage" spell appears
- Cast spell - should cost bonus action, no spell slot
- Verify 5 missiles fire (Level 3)
