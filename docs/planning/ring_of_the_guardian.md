# Ring of the Guardian

## Overview
A Legendary ring granting powerful protective and healing abilities.

## Item Details

| Aspect | Value |
|--------|-------|
| Name | Ring of the Guardian |
| Internal ID | SMR_Ring_Guardian |
| Appearance | LOOT_GEN_Ring_F_Silver_A (same as Star Athlete's Ring) |
| ParentTemplateId | 49b84359-6a28-460e-af98-4526c5fca6fd |
| MapKey | a1b2c3d4-e5f6-4a7b-8c9d-0e1f2a3b4c5d |
| Rarity | Legendary |
| Value | 750 gold |

---

## Powers

| Power | Description | Usage | Source |
|-------|-------------|-------|--------|
| **Superior Healing Word** | Enhanced healing (2d20+modifier) | Bonus action, unlimited | SMR_Target_HealingWord_Superior |
| **Guardian's Blessing** | Cast Bless | Unlimited | SMR_Target_Bless_Unlimited |
| **Guardian's Water** | Cast Create Water | Bonus action, unlimited | SMR_Target_CreateWater_Unlimited |
| **Guardian's Restoration** | Cast Lesser Restoration | Once per short rest | SMR_Target_LesserRestoration_ShortRest |
| **Guardian's Greater Restoration** | Cast Greater Restoration | Once per long rest | SMR_Target_GreaterRestoration_LongRest |
| **Guardian's Freedom** | Cast Freedom of Movement | Once per short rest | SMR_Target_FreedomOfMovement_ShortRest |
| **Guardian's Counter** | Cast Counterspell | Once per short rest | SMR_Interrupt_Counterspell_ShortRest |
| **Guardian's Feast** | Cast Heroes' Feast | Once per long rest | SMR_Shout_HeroesFeast_LongRest |
| **Remove Curse** | Cast Remove Curse | Once per long rest | SMR_Target_RemoveCurse_LongRest |
| **Revivify** | Cast Revivify | Once per long rest | SMR_Teleportation_Revivify_LongRest |
| **Guardian's Mass Healing** | Cast Mass Healing Word | Bonus action, unlimited | SMR_Shout_MassHealingWord_Unlimited |

---

## Implementation Files

### Armor.txt
```
new entry "SMR_Ring_Guardian"
type "Armor"
using "_Ring"
data "RootTemplate" "a1b2c3d4-e5f6-4a7b-8c9d-0e1f2a3b4c5d"
data "ObjectCategory" "Jewelry"
data "ValueOverride" "750"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(SMR_Target_HealingWord_Superior);UnlockSpell(SMR_Target_Bless_Unlimited);UnlockSpell(SMR_Target_CreateWater_Unlimited);UnlockSpell(SMR_Target_LesserRestoration_ShortRest);UnlockSpell(SMR_Target_GreaterRestoration_LongRest);UnlockSpell(SMR_Target_FreedomOfMovement_ShortRest);UnlockInterrupt(SMR_Interrupt_Counterspell_ShortRest);UnlockSpell(SMR_Shout_HeroesFeast_LongRest);UnlockSpell(SMR_Target_RemoveCurse_LongRest);UnlockSpell(SMR_Teleportation_Revivify_LongRest);UnlockSpell(SMR_Shout_MassHealingWord_Unlimited)"
```

### Spell_Shout.txt (Mass Healing Word)
```
new entry "SMR_Shout_MassHealingWord_Unlimited"
type "SpellData"
data "SpellType" "Shout"
using "Shout_HealingWord_Mass"
data "DisplayName" "hc5d6e7f8g9a0bg1c2dg3e4fg5a6b7c8d9e0f1;1"
data "ExtraDescription" "hd6e7f8a9g0b1cg2d3eg4f5ag6b7c8d9e0f1a2;1"
data "UseCosts" "BonusActionPoint:1"
```

### Localization Handles

| Element | Handle |
|---------|--------|
| DisplayName | he5f6a7b8gc9d0g1e2fga3b4g8c9d0e1f2a3b4 |
| Description | h5e6f7a8bg9c0dg2e1fg4a3bg9c0d1e2f3a4b5 |
| Guardian's Mass Healing Name | hc5d6e7f8g9a0bg1c2dg3e4fg5a6b7c8d9e0f1 |
| Guardian's Mass Healing Desc | hd6e7f8a9g0b1cg2d3eg4f5ag6b7c8d9e0f1a2 |

---

## Status: IMPLEMENTED

The Ring of the Guardian has been implemented and is available in the traveler's chest.
