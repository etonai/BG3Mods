# Staff of Akitaro

## Overview

A Legendary quarterstaff combining the arcane charge abilities of the Spellsparkler with all the powers of the Staff of the Archmage, plus unique Akitaro-themed powers.

## Item Details

| Aspect | Value |
|--------|-------|
| Name | Staff of Akitaro |
| Internal ID | SMR_Staff_Akitaro |
| Base Type | WPN_Quarterstaff_1 |
| Appearance | Staff of Interruption visual |
| Rarity | Legendary |
| Unique | Yes |
| MapKey | f1a2b3c4-d5e6-4f7a-8b9c-0d1e2f3a4b5c |

---

## Powers

### From Spellsparkler

| Power | Description | Source |
|-------|-------------|--------|
| **Arcane Charge on Damage** | Gain 2 Lightning Charges when dealing damage with a spell while at close range | MAG_CQCaster_GainArcaneChargeOnDamage_Quarterstaff_Passive |

### From Staff of the Archmage

| Power | Description | Source |
|-------|-------------|--------|
| **Chromatic Attunement** | Change damage type of spells | Shout_MAG_TheChromatic_ChromaticAttunement |
| **Spell Slot Restoration** | Restore spell slots | Shout_MAG_SpellSlotRestoration |
| **Pearlescent Restoration** | Restore spell slots (Pearl of Power) | Shout_MAG_SpellSlotRestoration_PearlOfPower |
| **Unlimited Shield** | Cast Shield as a reaction (unlimited) | SMR_Interrupt_Shield_Unlimited |
| **Unlimited Counterspell** | Cast Counterspell as a reaction (unlimited) | SMR_Interrupt_Counterspell_Unlimited |
| **Unlimited Light** | Cast Light (unlimited) | SMR_Target_Light_Unlimited |
| **Arcane Enchantment** | +1 bonus to spell save DC and spell attack rolls | MAG_ArcaneEnchantment_Lesser_Passive |
| **Arcane Battery** | Next spell doesn't cost a spell slot after long rest | MAG_Legendary_Chromatic_Spellslot_Passive |
| **Mystra's Grace** | +1 bonus to spell save DC and spell attack rolls | WW_Mystra_SpellAttkBonus_Passive |
| **Weave's Reclamation** | Once per turn, regain 1d4 hit points when dealing spell damage | WW_Mystra_Passive |
| **Echoes of Netheril** | Cantrips deal additional damage | WW_Netherese_Staff_Passive |

### Unique Akitaro Powers

| Power | Description | Source |
|-------|-------------|--------|
| **Celestial Haste** | Cast Haste on self (unlimited, bonus action) | SMR_Shout_CelestialHaste_Unlimited |
| **Akitaro's Blast** | Artistry of War (once per short rest) | SMR_Projectile_AkitarosBlast_ShortRest |
| **Akitaro's Teleport** | Misty Step (once per short rest) | SMR_Target_AkitarosTeleport_ShortRest |
| **Akitaro's Barrage** | Magic Missile level 3 (bonus action, once per short rest) | SMR_Projectile_AkitarosBarrage_ShortRest |
| **Akitaro's Shield** | Globe of Invulnerability (bonus action, once per short rest) | SMR_Target_AkitarosShield_ShortRest |

### Phase 21 Powers (Defensive/Utility)

| Power | Description | Source |
|-------|-------------|--------|
| **Absorb Elements** | Reaction: gain resistance to elemental damage, add 1d6 to next melee attack | Absorb_Elements_Passive |
| **Magical Durability** | +2 to saving throws vs spells | MAG_MagicalDurability_Passive |

### Phase 21 Powers (Offensive Synergies)

| Power | Description | Source |
|-------|-------------|--------|
| **Radiating Orb** | Apply Radiating Orb on spell damage (-1 attack per stack, illuminates target) | MAG_Radiant_RadiatingOrb_Ring_Passive |
| **Reverberation** | Apply Reverberation on Thunder/Lightning/Radiant damage (-1 STR/DEX/CON saves per stack) | MAG_Thunder_Reverberation_Gloves_Passive |
| **Arcane Acuity** | Gain Arcane Acuity on weapon attacks (+1 spell DC/attack per stack) | MAG_Gish_ArcaneAcuity_Gloves_Passive |

### Phase 21 Powers (Light/Radiant Theme)

| Power | Description | Source |
|-------|-------------|--------|
| **Callous Glow** | +2 radiant damage vs illuminated targets | MAG_Radiant_DamageBonusOnIlluminatedTarget_Ring_Passive |
| **Lathander's Light** | Toggled 6m aura that blinds Fiends/Undead (CON 14 save) | CRE_LathandersLight_Passive |

---

## Implementation Files

### Weapon.txt
```
new entry "SMR_Staff_Akitaro"
type "Weapon"
using "WPN_Quarterstaff_1"
data "RootTemplate" "f1a2b3c4-d5e6-4f7a-8b9c-0d1e2f3a4b5c"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(SMR_Target_Light_Unlimited);UnlockInterrupt(SMR_Interrupt_Counterspell_Unlimited);UnlockSpell(SMR_Shout_CelestialHaste_Unlimited);UnlockSpell(Shout_MAG_TheChromatic_ChromaticAttunement);UnlockSpell(Shout_MAG_SpellSlotRestoration);UnlockSpell(Shout_MAG_SpellSlotRestoration_PearlOfPower);UnlockInterrupt(SMR_Interrupt_Shield_Unlimited);UnlockSpell(SMR_Projectile_AkitarosBlast_ShortRest);UnlockSpell(SMR_Target_AkitarosTeleport_ShortRest);UnlockSpell(SMR_Projectile_AkitarosBarrage_ShortRest);UnlockSpell(SMR_Target_AkitarosShield_ShortRest)"
data "PassivesOnEquip" "MAG_CQCaster_GainArcaneChargeOnDamage_Quarterstaff_Passive;MAG_ArcaneEnchantment_Lesser_Passive;MAG_Legendary_Chromatic_Spellslot_Passive;WW_Mystra_SpellAttkBonus_Passive;WW_Mystra_Passive;WW_Netherese_Staff_Passive;Absorb_Elements_Passive;MAG_MagicalDurability_Passive;MAG_Radiant_RadiatingOrb_Ring_Passive;MAG_Thunder_Reverberation_Gloves_Passive;MAG_Gish_ArcaneAcuity_Gloves_Passive;MAG_Radiant_DamageBonusOnIlluminatedTarget_Ring_Passive;CRE_LathandersLight_Passive"
data "StatusOnEquip" "MAG_LATHANDERS_LIGHT_TECHNICAL"
data "Unique" "1"
```

### Spell_Shout.txt
```
new entry "SMR_Shout_CelestialHaste_Unlimited"
type "SpellData"
data "SpellType" "Shout"
using "Shout_MAG_Victory_Longbow_Haste"
data "UseCosts" "BonusActionPoint:1"
```

### Spell_Projectile.txt (Akitaro's Barrage)
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

### Spell_Target.txt (Akitaro's Shield)
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

### RootTemplates
- ParentTemplateId: `e1e112b2-5465-4e37-acdc-372666ec1521` (Staff of Interruption)
- VisualTemplate: `fb8204e8-e265-7af3-86b1-7341c6880ba1` (Staff of Interruption visual)

### Localization
- DisplayName handle: `h5a6b7c8dge9f0g1a2bg3c4dg5e6f7a8b9c0d`
- Description handle: `h6b7c8d9egf0a1g2b3cg4d5eg6f7a8b9c0d1e`
- Akitaro's Barrage DisplayName: `he1f2a3b4g5c6dg7e8fg9a0bg1c2d3e4f5a6b7`
- Akitaro's Barrage Description: `hf2a3b4c5g6d7eg8f9ag0b1cg2d3e4f5a6b7c8`
- Akitaro's Shield DisplayName: `ha3b4c5d6g7e8fg9a0bg1c2dg3e4f5a6b7c8d9`
- Akitaro's Shield Description: `hb4c5d6e7g8f9ag0b1cg2d3eg4f5a6b7c8d9e0`

---

## Status: IMPLEMENTED

The Staff of Akitaro has been implemented and is available in the traveler's chest.
