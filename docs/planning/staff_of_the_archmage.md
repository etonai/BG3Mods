# Staff of the Archmage - Implementation Plan

## Overview
A Legendary quarterstaff granting powerful arcane abilities, spell slot restoration, and defensive reactions. Designed for a master spellcaster.

## Design Decisions (Complete)

| Aspect | Decision |
|--------|----------|
| Name | Staff of the Archmage |
| Internal ID | SMR_Staff_Archmage |
| Base Type | WPN_Quarterstaff_2 |
| RootTemplate | c2d3e4f5-a6b7-4c8d-9e0f-1a2b3c4d5e6f |
| Appearance | Spellsparkler visual (intended) |
| Rarity | Legendary |
| Unique | Yes |

### Powers (Spells)

| Status | Power | Description | Source |
|--------|-------|-------------|--------|
| [x] | **Chromatic Attunement** | Gain resistance to elemental damage types | Shout_MAG_TheChromatic_ChromaticAttunement (Markoheshkir) |
| [x] | **Arcane Battery** | Restore spell slots | Shout_MAG_SpellSlotRestoration (Markoheshkir) |
| [x] | **Pearl of Power** | Restore spell slots (alternative) | Shout_MAG_SpellSlotRestoration_PearlOfPower |
| [x] | **Unlimited Shield** | Cast Shield as a reaction (unlimited) | SMR_Interrupt_Shield_Unlimited |
| [x] | **Unlimited Counterspell** | Cast Counterspell as a reaction (unlimited) | SMR_Interrupt_Counterspell_Unlimited |
| [x] | **Light** | Cast Light (unlimited, bonus action) | SMR_Target_Light_Unlimited |

### Passive Abilities

| Status | Passive | Description | Source |
|--------|---------|-------------|--------|
| [x] | **Arcane Enchantment** | +1 to Spell Save DC and Spell Attack Rolls | MAG_ArcaneEnchantment_Lesser_Passive (vanilla) |
| [x] | **Chromatic Spellslot** | Bonus spell slot from Markoheshkir | MAG_Legendary_Chromatic_Spellslot_Passive (Markoheshkir) |
| [x] | **Mystra's Spell Attack Bonus** | Bonus to spell attack rolls | WW_Mystra_SpellAttkBonus_Passive (Whimsical Wares) |
| [x] | **Mystra's Blessing** | Additional magical benefits | WW_Mystra_Passive (Whimsical Wares) |
| [x] | **Netherese Staff Power** | Netherese magic enhancement | WW_Netherese_Staff_Passive (Whimsical Wares) |

---

## Current Implementation

### Stats/Generated/Data/Weapon.txt
```
new entry "SMR_Staff_Archmage"
type "Weapon"
using "WPN_Quarterstaff_2"
data "RootTemplate" "c2d3e4f5-a6b7-4c8d-9e0f-1a2b3c4d5e6f"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(Shout_MAG_TheChromatic_ChromaticAttunement);UnlockSpell(Shout_MAG_SpellSlotRestoration);UnlockSpell(Shout_MAG_SpellSlotRestoration_PearlOfPower);UnlockInterrupt(SMR_Interrupt_Shield_Unlimited);UnlockInterrupt(SMR_Interrupt_Counterspell_Unlimited);UnlockSpell(SMR_Target_Light_Unlimited)"
data "PassivesOnEquip" "MAG_ArcaneEnchantment_Lesser_Passive;MAG_Legendary_Chromatic_Spellslot_Passive;WW_Mystra_SpellAttkBonus_Passive;WW_Mystra_Passive;WW_Netherese_Staff_Passive"
data "Unique" "1"
```

### Custom Spells/Interrupts

#### SMR_Interrupt_Shield_Unlimited (Interrupt.txt)
Unlimited Shield reaction.

#### SMR_Interrupt_Counterspell_Unlimited (Interrupt.txt)
Unlimited Counterspell reaction.

#### SMR_Target_Light_Unlimited (Spell_Target.txt)
```
new entry "SMR_Target_Light_Unlimited"
type "SpellData"
data "SpellType" "Target"
using "Target_Light"
data "UseCosts" "BonusActionPoint:1"
```

---

## Known Issues

### Appearance Bug (Phase 8 - Part 1)
The Staff of the Archmage does not display with the Spellsparkler appearance as intended. Investigation needed:
- Current ParentTemplateId references Spellsparkler's MapKey
- VisualTemplate is set to Spellsparkler's visual
- May need additional attributes (Icon, etc.)

---

## Notes

- Dependencies on Markoheshkir (vanilla) for Chromatic Attunement and spell slot restoration
- Dependencies on Whimsical Wares mod for Mystra and Netherese passives
- Uses vanilla MAG_ArcaneEnchantment_Lesser_Passive for spell DC/attack bonus
