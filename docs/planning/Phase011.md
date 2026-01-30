# Phase 011 - Staff of Akitaro Enhancements & Ring of Guardian Update

**Status:** IMPLEMENTED

## Goal
1. Change Staff of Akitaro appearance to match Staff of Interruption
2. Add Magic Missile (level 3) and Globe of Invulnerability to Staff of Akitaro
3. Add Mass Healing Word to Ring of the Guardian

---

## Part 1: Staff of Akitaro - Appearance Change

### Staff of Interruption Reference
- Internal Name: `MAG_LC_Counterspell_Quarterstaff`
- MapKey: `fcbb2c63-ac59-42e0-ad0b-d91cf9a47b60`
- ParentTemplateId: `e1e112b2-5465-4e37-acdc-372666ec1521`
- VisualTemplate: `fb8204e8-e265-7af3-86b1-7341c6880ba1`

### Files to Modify
- `RootTemplates/merged.lsx` - Update ParentTemplateId and VisualTemplate
- `RootTemplates/merged.lsf.lsx` - Update ParentTemplateId and VisualTemplate

---

## Part 2: Staff of Akitaro - New Powers

### New Powers to Add

| Power | Description | Source |
|-------|-------------|--------|
| **Akitaro's Barrage** | Magic Missile level 3 (bonus action, short rest) | SMR_Projectile_AkitarosBarrage_ShortRest |
| **Akitaro's Shield** | Globe of Invulnerability (bonus action, short rest) | SMR_Target_AkitarosShield_ShortRest |

### Files to Modify

#### Spell_Projectile.txt
```
new entry "SMR_Projectile_AkitarosBarrage_ShortRest"
type "SpellData"
data "SpellType" "Projectile"
using "Projectile_MagicMissile_3"
data "DisplayName" "he1f2a3b4g5c6dg7e8fg9a0bg1c2d3e4f5a6b7;1"
data "ExtraDescription" "hf2a3b4c5g6d7eg8f9ag0b1cg2d3e4f5a6b7c8;1"
data "UseCosts" "BonusActionPoint:1"
data "Cooldown" "OncePerShortRest"
```

#### Spell_Target.txt
```
new entry "SMR_Target_AkitarosShield_ShortRest"
type "SpellData"
data "SpellType" "Target"
using "Target_GlobeOfInvulnerability"
data "DisplayName" "ha3b4c5d6g7e8fg9a0bg1c2dg3e4f5a6b7c8d9;1"
data "ExtraDescription" "hb4c5d6e7g8f9ag0b1cg2d3eg4f5a6b7c8d9e0;1"
data "UseCosts" "BonusActionPoint:1"
data "Cooldown" "OncePerShortRest"
```

#### Weapon.txt
Update SMR_Staff_Akitaro Boosts to add:
- `UnlockSpell(SMR_Projectile_AkitarosBarrage_ShortRest)`
- `UnlockSpell(SMR_Target_AkitarosShield_ShortRest)`

---

## Part 3: Ring of the Guardian - Mass Healing Word

### New Power

| Power | Description | Source |
|-------|-------------|--------|
| **Guardian's Mass Healing** | Mass Healing Word (bonus action, unlimited) | SMR_Shout_MassHealingWord_Unlimited |

### Reference
- Vanilla spell: `Shout_HealingWord_Mass`

### Files to Modify

#### Spell_Shout.txt
```
new entry "SMR_Shout_MassHealingWord_Unlimited"
type "SpellData"
data "SpellType" "Shout"
using "Shout_HealingWord_Mass"
data "DisplayName" "hc5d6e7f8g9a0bg1c2dg3e4fg5a6b7c8d9e0f1;1"
data "ExtraDescription" "hd6e7f8a9g0b1cg2d3eg4f5ag6b7c8d9e0f1a2;1"
data "UseCosts" "BonusActionPoint:1"
```

#### Armor.txt
Update SMR_Ring_Guardian Boosts to add:
- `UnlockSpell(SMR_Shout_MassHealingWord_Unlimited)`

---

## Localization Entries

### Staff of Akitaro Powers
```xml
<content contentuid="he1f2a3b4g5c6dg7e8fg9a0bg1c2d3e4f5a6b7" version="1">Akitaro's Barrage</content>
<content contentuid="hf2a3b4c5g6d7eg8f9ag0b1cg2d3e4f5a6b7c8" version="1">Magic Missile level 3. Once per short rest.</content>
<content contentuid="ha3b4c5d6g7e8fg9a0bg1c2dg3e4f5a6b7c8d9" version="1">Akitaro's Shield</content>
<content contentuid="hb4c5d6e7g8f9ag0b1cg2d3eg4f5a6b7c8d9e0" version="1">Globe of Invulnerability. Once per short rest.</content>
```

### Ring of the Guardian Power
```xml
<content contentuid="hc5d6e7f8g9a0bg1c2dg3e4fg5a6b7c8d9e0f1" version="1">Guardian's Mass Healing</content>
<content contentuid="hd6e7f8a9g0b1cg2d3eg4f5ag6b7c8d9e0f1a2" version="1">Mass Healing Word. Unlimited uses.</content>
```

---

## Implementation Checklist

### Staff of Akitaro Appearance
- [x] Update ParentTemplateId in merged.lsx
- [x] Update VisualTemplate in merged.lsx
- [x] Update ParentTemplateId in merged.lsf.lsx
- [x] Update VisualTemplate in merged.lsf.lsx

### Staff of Akitaro Powers
- [x] Add SMR_Projectile_AkitarosBarrage_ShortRest to Spell_Projectile.txt
- [x] Add SMR_Target_AkitarosShield_ShortRest to Spell_Target.txt
- [x] Update SMR_Staff_Akitaro in Weapon.txt
- [x] Add localization entries to SampleMagicRingMod.xml
- [x] Add localization entries to SampleMagicRingMod.loca.xml

### Ring of the Guardian
- [x] Add SMR_Shout_MassHealingWord_Unlimited to Spell_Shout.txt
- [x] Update SMR_Ring_Guardian in Armor.txt
- [x] Add localization entries to SampleMagicRingMod.xml
- [x] Add localization entries to SampleMagicRingMod.loca.xml

### Documentation
- [x] Update staff_of_akitaro.md
- [x] Update ring_of_the_guardian.md

### Final
- [ ] Build and test mod

---

## Test Plan

### Staff of Akitaro
- [ ] Verify staff appears with Staff of Interruption visual
- [ ] Verify Akitaro's Barrage spell is available (bonus action)
- [ ] Cast Akitaro's Barrage and verify 5 missiles fire
- [ ] Verify Akitaro's Barrage has short rest cooldown
- [ ] Verify Akitaro's Shield spell is available (bonus action)
- [ ] Cast Akitaro's Shield and verify Globe of Invulnerability is created
- [ ] Verify Akitaro's Shield has short rest cooldown

### Ring of the Guardian
- [ ] Equip Ring of the Guardian
- [ ] Verify Guardian's Mass Healing spell is available (bonus action)
- [ ] Cast Guardian's Mass Healing and verify it heals multiple allies
- [ ] Verify unlimited casting (no cooldown)
