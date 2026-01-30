# Boots of the Stormwalker - Implementation Plan

## Overview
Legendary boots granting mobility, thunder-based abilities, and immunity to movement-impairing effects. Inspired by the Nightwalker boots with added thunder magic.

## Design Decisions (Complete)

| Aspect | Decision |
|--------|----------|
| Name | Boots of the Stormwalker |
| Internal ID | SMR_Boots_Stormwalker |
| Base Type | _Foot_Magic |
| RootTemplate | e1f2a3b4-c5d6-4e7f-8a9b-0c1d2e3f4a5b |
| Rarity | Legendary |
| Unique | Yes |

### Powers (Spells)

| Status | Power | Description | Source |
|--------|-------|-------------|--------|
| [x] | **Misty Step** | Cast Misty Step (Nightwalkers version) | Target_UNI_MistyStep_NightWalkers (vanilla Nightwalker boots) |

### Passive Abilities

| Status | Passive | Description | Source |
|--------|---------|-------------|--------|
| [x] | **Reverberation** | Apply Reverberation status on thunder damage | MAG_Thunder_ReverberationOnStatusApply_Boots_Passive (vanilla) |
| [x] | **Web Immunity** | Immune to Enwebbed condition, cannot be slowed by webs | FOR_NightWalkers_WebImmunity (Nightwalker boots) |

---

## Current Implementation

### Stats/Generated/Data/Armor.txt
```
new entry "SMR_Boots_Stormwalker"
type "Armor"
using "_Foot_Magic"
data "RootTemplate" "e1f2a3b4-c5d6-4e7f-8a9b-0c1d2e3f4a5b"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(Target_UNI_MistyStep_NightWalkers)"
data "PassivesOnEquip" "MAG_Thunder_ReverberationOnStatusApply_Boots_Passive;FOR_NightWalkers_WebImmunity"
data "Unique" "1"
```

---

## Reference Items

### Nightwalker Boots (FOR_NightWalkers)
The primary inspiration for these boots:
- Grants Misty Step
- Web Immunity
- Night vision-related benefits

### Boots of Stormy Clamour
Source of the Reverberation passive:
- Applies Reverberation on thunder damage
- Synergizes with thunder-based spells and abilities

---

## Thematic Design

The Stormwalker boots combine:
1. **Mobility** - Misty Step for tactical repositioning
2. **Thunder Magic** - Reverberation passive enhances thunder damage builds
3. **Freedom** - Web immunity prevents movement restriction

Ideal for:
- Tempest Clerics
- Storm Sorcerers
- Any character using thunder damage spells
- Characters who need mobility in spider-infested areas

---

## Notes

- Uses vanilla Nightwalker Misty Step spell (no custom spell needed)
- All passives are from vanilla game items
- No dependencies on other mods
