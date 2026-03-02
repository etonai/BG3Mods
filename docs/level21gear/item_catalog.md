# Level 21 Gear - Item Catalog

Complete list of all items in the Level 21 Gear mod for BG3.

**Target Audience:** Level 21+ characters
**Delivery Method:** Tutorial Chest (via TreasureTable injection)

**Important:** Items will only appear in the Tutorial Chest for new games or saves where the chest hasn't been opened yet.

---

## Table of Contents
- [Weapons](#weapons)
  - [Swords](#swords)
  - [Staves](#staves)

---

## Weapons

### Swords

#### Silverlight Sword
**Internal Name:** `L21_Sword_Silverlight`
**Rarity:** Legendary
**Base Weapon:** WPN_Longsword_2 (+5 enchantment)

**RootTemplate UUID:** `ed21e061-f4d9-49f0-8aa0-e737813db4e4`

**Weapon Properties:**
- +5 magical longsword
- Not unique (multiple can exist)

**Passives:**
- `MAG_PlaneShifterSlayer_Passive` - Bonus damage vs planar creatures
- `L21_RadiantWeapon_Passive` - Radiant weapon enhancement
- `MAG_TheClover_Rearrangement_Passive` - Lucky rerolls
- `CRE_LathandersLight_Passive` - Lathander's Light toggled aura (blinds Fiends/Undead)
- `L21_Moonshield_Passive` - Shadow Curse immunity aura

**Status on Equip:**
- `MAG_LATHANDERS_LIGHT_TECHNICAL` - Lathander's Light aura system
- `LOW_RAMAZITHSTOWER_DEVA_BLESSING` - Deva's Blessing: weapon attacks deal +5d8 radiant damage

**Spells Granted:**

*Weapon Actions:*
- **Razor Gale** (`Zone_Mag_WeaponAction_RazorGale`) - Cleave-style attack in a 60-degree arc at 4m range; hit deals weapon damage + Proficiency Bonus, miss deals half; wind/air visual (Phase 060)

*Offensive Spells:*
- Wrathful Smite (`Target_MAG_Smite_Wrathful`) - Extra psychic damage + Frightened on hit
- Blinding Smite of Silverlight (`L21_Target_BlindingSmite_Silverlight`) - Extra radiant damage + Blind on hit (1 Action)

*Defensive/Buff Spells:*
- Silvered Bulwark (`L21_Target_SilveredBulwark`) - Bonus action, grants ally full invulnerability + advantage on saves (concentration)
- Shield of Faith (`Target_PLA_ShieldOfFaith_SwordOfJustice`) - +2 AC buff
- Celestial Haste (`L21_Shout_CelestialHaste_Unlimited`) - Self-haste, free action, no concentration, unlimited

*Aura Spells:*
- Spirit Guardians of Silverlight (`L21_Shout_SpiritGuardians_Silverlight`) - 3m radiant/necrotic damage aura, scales with spellcasting ability

*Utility Spells:*
- Light (`L21_Target_Light_Unlimited`) - Create light, bonus action, unlimited

**Phase:** 057 (created), 060 (Razor Gale added)

---

### Staves

#### Staff of Gimeitaro
**Internal Name:** `L21_Staff_Gimeitaro`
**Rarity:** Legendary
**Enchantment:** Quarterstaff (base)
**Base Weapon:** WPN_Quarterstaff_1

**RootTemplate UUID:** `ed21b86f-a7f7-4de6-ad51-1a2c33b9c779`
**Handle (Name):** `h8054ad1dg1aeag4b70gb63fgeabb5fb10181`
**Handle (Description):** `hb514d87agf785g4f45g8c93g4827fb5d7f3f`

**Weapon Properties:**
- Legendary quarterstaff with immense magical power
- Extensive spell repertoire covering combat, defense, and utility
- **+10 to all skill checks and ability checks**
- **+7 to initiative**
- **+8 to all saving throws**

**Passives:**
- MAG_CQCaster_GainArcaneChargeOnDamage_Quarterstaff_Passive - Arcane Charges on damage
- MAG_ArcaneEnchantment_Lesser_Passive - +1 Spell Save DC and Spell Attack
- MAG_Legendary_Chromatic_Spellslot_Passive - Chromatic spell slot restoration
- WW_Mystra_SpellAttkBonus_Passive - Spell attack bonuses
- WW_Mystra_Passive - Mystra's blessings
- WW_Netherese_Staff_Passive - Netherese magic enhancements
- Absorb_Elements_Passive - Absorb Elements reaction
- MAG_MagicalDurability_Passive - +2 saving throws vs spells
- MAG_Radiant_RadiatingOrb_Ring_Passive - Apply Radiating Orb on spell damage
- MAG_Gish_ArcaneAcuity_Gloves_Passive - Arcane Acuity on weapon/unarmed attacks
- MAG_Radiant_DamageBonusOnIlluminatedTarget_Ring_Passive - +2 radiant damage vs illuminated targets
- CRE_LathandersLight_Passive - Lathander's Light toggled aura

**Status on Equip:**
- MAG_LATHANDERS_LIGHT_TECHNICAL - Lathander's Light aura system

**Spells Granted:**

*Offensive Spells:*
- Gimeitaro's Blast (Short Rest) - Powerful blast attack
- Gimeitaro's Barrage (Unlimited, Bonus Action) - Magic missile barrage
- Chromatic Orb (Unlimited, Action) - Versatile elemental damage
- **Gimeitaro's Spirit Guardians (Unlimited, Free Action, NO CONCENTRATION)** - 3m aura dealing 3d8 Radiant or Necrotic damage

*Defensive/Buff Spells:*
- **Gimeitaro's Shield (Unlimited, Bonus Action, Concentration)** - Silvered Bulwark (mobile invulnerability)
- **Celestial Haste (Unlimited, Free Action, NO CONCENTRATION)** - Instant self-haste
- Shield (Unlimited, Bonus Action) - Interrupt shield reaction
- Chromatic Attunement - Chromatic magic enhancement
- Spell Slot Restoration - Restore spell slots
- Pearl of Power variant - Additional spell slot restoration

*Utility Spells:*
- Light (Unlimited, Bonus Action) - Create light
- Knock (Unlimited, Bonus Action) - Open locks
- Gimeitaro's Teleport (Short Rest) - Misty Step variant
- Arcane Gate (Short Rest) - Create teleportation portals
- Counterspell (Unlimited, Bonus Action) - Counter enemy spells

**Power Stacking:** Celestial Haste and Spirit Guardians can be active simultaneously without concentration conflicts. Gimeitaro's Shield requires concentration but can be combined with either Haste or Spirit Guardians for powerful tactical combinations.

**Lore:**
A legendary staff imbued with immense arcane power, granting its wielder unparalleled magical abilities and protective enchantments. This staff combines the blessings of Lathander with Netherese magic and Mystra's favor, creating one of the most powerful arcane focuses in existence. The wielder gains supernatural mastery over all skills and abilities, acts with lightning speed in combat, and resists magical effects with ease.

**Source:** Copied from SampleMagicRingMod (SMR_Staff_Akitaro) and adapted for Level 21 Gear. Renamed to Gimeitaro in Revision 1. Enhanced with Silvered Bulwark, Spirit Guardians, free action Haste, and comprehensive stat bonuses in Revision 2. Concentration removed from three major buffs in Phase 055.

**Phase:** 054 (Revision 2), 055

---

## Implementation Status

| Item | Status | Phase | Notes |
|------|--------|-------|-------|
| Silverlight Sword | COMPLETE | 057 (created), 060 (Razor Gale) | Legendary longsword with Razor Gale, Wrathful/Blinding Smite, Silvered Bulwark, Celestial Haste, Spirit Guardians, Deva's Blessing. |
| Staff of Gimeitaro | COMPLETE | 054-R2, 055-R1 | Enhanced with Silvered Bulwark, Spirit Guardians, free action Haste, +10 skills/abilities, +7 initiative, +8 saves. NO CONCENTRATION on Haste and Spirit Guardians (can stack). Shield requires concentration. |

---

## Statistics

- **Total Items:** 2
- **Weapons:** 2 (1 Longsword, 1 Staff)
- **Armor:** 0
- **Accessories:** 0

**Last Updated:** 2026-02-22 (Phase 060)
