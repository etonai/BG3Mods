# Staff of Akitaro

## Overview

A Legendary quarterstaff combining the arcane charge abilities of the Spellsparkler with all the powers of the Staff of the Archmage, plus unlimited Celestial Haste.

## Item Details

| Aspect | Value |
|--------|-------|
| Name | Staff of Akitaro |
| Internal ID | SMR_Staff_Akitaro |
| Base Type | WPN_Quarterstaff_1 |
| Appearance | Quarterstaff +1 visual |
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

### Unique Powers

| Power | Description | Source |
|-------|-------------|--------|
| **Celestial Haste** | Cast Haste on self (unlimited, bonus action) | SMR_Shout_CelestialHaste_Unlimited |
| **Akitaro's Blast** | Artistry of War (once per short rest) | SMR_Projectile_AkitarosBlast_ShortRest |
| **Akitaro's Teleport** | Misty Step (once per short rest) | SMR_Target_AkitarosTeleport_ShortRest |

---

## Implementation Files

### Weapon.txt
```
new entry "SMR_Staff_Akitaro"
type "Weapon"
using "WPN_Quarterstaff_1"
data "RootTemplate" "f1a2b3c4-d5e6-4f7a-8b9c-0d1e2f3a4b5c"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(SMR_Target_Light_Unlimited);UnlockInterrupt(SMR_Interrupt_Counterspell_Unlimited);UnlockSpell(SMR_Shout_CelestialHaste_Unlimited);UnlockSpell(Shout_MAG_TheChromatic_ChromaticAttunement);UnlockSpell(Shout_MAG_SpellSlotRestoration);UnlockSpell(Shout_MAG_SpellSlotRestoration_PearlOfPower);UnlockInterrupt(SMR_Interrupt_Shield_Unlimited);UnlockSpell(SMR_Projectile_AkitarosBlast_ShortRest);UnlockSpell(SMR_Target_AkitarosTeleport_ShortRest)"
data "PassivesOnEquip" "MAG_CQCaster_GainArcaneChargeOnDamage_Quarterstaff_Passive;MAG_ArcaneEnchantment_Lesser_Passive;MAG_Legendary_Chromatic_Spellslot_Passive;WW_Mystra_SpellAttkBonus_Passive;WW_Mystra_Passive;WW_Netherese_Staff_Passive"
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

### RootTemplates
- ParentTemplateId: `96e2abaf-78ff-4dcb-a6a3-a5f0c348bd9f` (Quarterstaff +1)
- VisualTemplate: `46537c0f-21bf-f64a-c873-50c3ac11e3a3`

### Localization
- DisplayName handle: `h5a6b7c8dge9f0g1a2bg3c4dg5e6f7a8b9c0d`
- Description handle: `h6b7c8d9egf0a1g2b3cg4d5eg6f7a8b9c0d1e`

---

## Status: IMPLEMENTED

The Staff of Akitaro has been implemented and is available in the traveler's chest.
