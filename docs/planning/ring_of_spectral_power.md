# Ring of Spectral Power

## Overview

A Legendary ring granting powerful spectral/force magic abilities.

## Item Details

| Aspect | Value |
|--------|-------|
| Name | Ring of Spectral Power |
| Internal ID | SMR_Ring_Spectral_Power |
| Appearance | Item_LOOT_GEN_Ring_D_Silver_A |
| Rarity | Legendary |
| Value | 750 gold |
| MapKey | d4e5f6a7-b8c9-4d0e-a1b2-c3d4e5f6a7b8 |

---

## Powers

### Unlimited Powers

| Power | Description | Source |
|-------|-------------|--------|
| **Spectral Barrage** | Level 3 Magic Missile (5 missiles) as a bonus action | SMR_Projectile_MagicMissile_Unlimited_Lvl3 |
| **Spectral Step** | Misty Step (no action cost, no spell slot) | SMR_Target_MistyStep_Unlimited |
| **Spectral Shield** | Shield as a reaction | SMR_Interrupt_Shield_Unlimited |
| **Spectral Hold** | Hold Person as a bonus action | SMR_Target_HoldPerson_Unlimited |
| **Spectral Knock** | Knock as a bonus action | SMR_Target_Knock_Unlimited |

### Once Per Short Rest

| Power | Description | Source |
|-------|-------------|--------|
| **Spectral Barrier** | Globe of Invulnerability | SMR_Target_GlobeOfInvulnerability_ShortRest |
| **Spectral Artistry** | Artistry of War | SMR_Projectile_ArtistryOfWar_ShortRest |
| **Spectral Veil** | Invisibility | SMR_Target_Invisibility_ShortRest |
| **Spectral Gate** | Arcane Gate | SMR_Teleportation_ArcaneGate_ShortRest |
| **Telekinesis** | Telekinesis | SMR_Throw_Telekinesis_ShortRest |

### Passive Abilities

| Power | Description | Source |
|-------|-------------|--------|
| **Forceweaver** | Force damage bonus | WW_Forceweaver_Passive |

---

## Implementation Files

### Armor.txt
```
new entry "SMR_Ring_Spectral_Power"
type "Armor"
using "_Ring"
data "RootTemplate" "d4e5f6a7-b8c9-4d0e-a1b2-c3d4e5f6a7b8"
data "ObjectCategory" "Jewelry"
data "ValueOverride" "750"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(SMR_Projectile_MagicMissile_Unlimited_Lvl3);UnlockSpell(SMR_Target_GlobeOfInvulnerability_ShortRest);UnlockSpell(SMR_Target_MistyStep_Unlimited);UnlockInterrupt(SMR_Interrupt_Shield_Unlimited);UnlockSpell(SMR_Target_HoldPerson_Unlimited);UnlockSpell(SMR_Projectile_ArtistryOfWar_ShortRest);UnlockSpell(SMR_Target_Invisibility_ShortRest);UnlockSpell(SMR_Target_Knock_Unlimited);UnlockSpell(SMR_Teleportation_ArcaneGate_ShortRest);UnlockSpell(SMR_Throw_Telekinesis_ShortRest)"
data "PassivesOnEquip" "WW_Forceweaver_Passive"
```

### Localization
- DisplayName handle: `ha1b2c3d4ge5f6g7a8bg9c0dg1e2f3a4b5c6d`
- Description handle: `h1a2b3c4dg5e6fg7a8bg9c0dge1f2a3b4c5d6`

---

## Status: IMPLEMENTED

The Ring of Spectral Power has been implemented and is available in the traveler's chest.
