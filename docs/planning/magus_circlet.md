# Magus Circlet - Implementation Plan

## Overview
A Legendary circlet granting powerful divination, protection, and utility abilities focused on perception and defense against supernatural threats.

## Design Decisions (Complete)

| Aspect | Decision |
|--------|----------|
| Name | Magus Circlet |
| Internal ID | SMR_Circlet_Magus |
| Base Type | _Head_Magic_Circlet |
| RootTemplate | a2b3c4d5-e6f7-4a8b-9c0d-1e2f3a4b5c6d |
| Rarity | Legendary |
| Unique | Yes |

### Powers

| Status | Power | Description | Source |
|--------|-------|-------------|--------|
| [x] | **Speak with Dead** | Cast Speak with Dead (unlimited) | WW_Target_SpeakWithDead (Whimsical Wares mod) |
| [x] | **Speak with Animals** | Cast Speak with Animals (unlimited) | WW_Shout_SpeakWithAnimals (Whimsical Wares mod) |
| [x] | **See Invisibility** | Cast See Invisibility (unlimited, bonus action) | SMR_Shout_SeeInvisibility_Unlimited |
| [x] | **Protection From Evil And Good** | Cast Protection From Evil And Good (unlimited, bonus action) | SMR_Target_ProtectionFromEvilAndGood_Unlimited |
| [x] | **Faerie Fire** | Cast Faerie Fire (bonus action, once per short rest) | SMR_Target_FaerieFire_ShortRest |

### Passive Abilities

| Status | Passive | Description | Source |
|--------|---------|-------------|--------|
| [x] | **Fear Immunity** | Immune to fear effects | MAG_LC_Cyric_FearImmunity_Amulet_Passive (vanilla) |
| [x] | **Blind Immunity** | Immune to blindness, can see through darkness | MAG_Shadow_BlindImmunity_Ring_Passive (Eversight Ring) |
| [x] | **Darkvision** | Can see in the dark | UND_SocietyOfBrilliance_DarkvisionRing_Passive (Sunwalker's Gift Ring) |

---

## Current Implementation

### Stats/Generated/Data/Armor.txt
```
new entry "SMR_Circlet_Magus"
type "Armor"
using "_Head_Magic_Circlet"
data "RootTemplate" "a2b3c4d5-e6f7-4a8b-9c0d-1e2f3a4b5c6d"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(WW_Target_SpeakWithDead);UnlockSpell(WW_Shout_SpeakWithAnimals);UnlockSpell(SMR_Shout_SeeInvisibility_Unlimited);UnlockSpell(SMR_Target_ProtectionFromEvilAndGood_Unlimited);UnlockSpell(SMR_Target_FaerieFire_ShortRest)"
data "PassivesOnEquip" "MAG_LC_Cyric_FearImmunity_Amulet_Passive;MAG_Shadow_BlindImmunity_Ring_Passive;UND_SocietyOfBrilliance_DarkvisionRing_Passive"
data "Unique" "1"
```

### Custom Spells

#### SMR_Shout_SeeInvisibility_Unlimited (Spell_Shout.txt)
```
new entry "SMR_Shout_SeeInvisibility_Unlimited"
type "SpellData"
data "SpellType" "Shout"
using "Shout_SeeInvisibility"
data "UseCosts" "BonusActionPoint:1"
```

#### SMR_Target_ProtectionFromEvilAndGood_Unlimited (Spell_Target.txt)
```
new entry "SMR_Target_ProtectionFromEvilAndGood_Unlimited"
type "SpellData"
data "SpellType" "Target"
using "Target_ProtectionFromEvilAndGood"
data "UseCosts" "BonusActionPoint:1"
```

#### SMR_Target_FaerieFire_ShortRest (Spell_Zone.txt)
```
new entry "SMR_Target_FaerieFire_ShortRest"
type "SpellData"
data "SpellType" "Target"
using "Target_FaerieFire"
data "UseCosts" "BonusActionPoint:1"
data "Cooldown" "OncePerShortRest"
```

---

## Notes

- See Invisibility is a Shout type spell, not Target
- Faerie Fire is a Target type spell, not Zone
- Dependencies on Whimsical Wares mod for Speak with Dead/Animals spells
- Dependencies on vanilla passives for Fear Immunity, Blind Immunity, and Darkvision
