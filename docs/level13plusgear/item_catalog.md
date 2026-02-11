# Level13PlusGear Item Catalog

A complete list of all magic items in the Level13PlusGear mod.

---

## Weapons

### L13_Staff_Archmage (Staff of the Archmage)
**Type:** Quarterstaff | **Rarity:** Legendary

| Category | Details |
|----------|---------|
| Spells | Chromatic Attunement, Spell Slot Restoration (2 versions), Light (unlimited), Shield (unlimited), Counterspell (unlimited) |
| Passives | Arcane Enchantment (+1 spell DC/attack), Chromatic Spellslot, Mystra's Blessing (spell attack bonus), Netherese Staff |
| Description | A legendary staff imbued with the essence of the Weave itself. Grants Chromatic Attunement, Arcane Enchantment, Arcane Battery, Spell Slot Restoration, Pearlescent Restoration, Mystra's Grace, Weave's Reclamation, Echoes of Netheril, and unlimited Shield and Counterspell reactions. |

---

### L13_Sword_Tyr (Longsword of Tyr)
**Type:** Longsword +5 | **Rarity:** Legendary

| Category | Details |
|----------|---------|
| Enchantment | +5, Magical |
| Spells | Wrathful Smite, Blinding Smite (unlimited), Light (unlimited), Shield of Faith, Celestial Haste (unlimited) |
| Passives | Plane Shifter Slayer, Radiant Weapon (+1d4 radiant) |
| Description | A silver longsword blessed by Tyr, the God of Justice. Grants Wrathful Smite, Soulbreaker, and unlimited Blinding Smite. |

---

### L13_Blade_Moonguard (Moonguard Blade)
**Type:** Longsword +5 | **Rarity:** Legendary | **Appearance:** Primeval Silver Longsword

| Category | Details |
|----------|---------|
| Enchantment | +5, Magical |
| Spells | Wrathful Smite, Selûne's Blinding Smite (unlimited), Light (unlimited), Shield of Faith, Celestial Haste (free action), Spirit Guardians (free action) |
| Passives | Plane Shifter Slayer, Radiant Weapon (+1d8 radiant), Rearrangement (crit on 19-20, reroll damage ≤2), Lathander's Light (toggled aura blinds Fiends/Undead), Moonshield Aura (Shadow Curse protection) |
| Status | Lathander's Light Technical |
| Description | A longsword blessed by Selûne, the Moonmaiden. Grants Wrathful Smite, Selûne's Blinding Smite (unlimited), Light (unlimited), Shield of Faith, Celestial Haste (free action), Spirit Guardians (free action), Plane Shifter Slayer, Radiant Weapon (+1d8 radiant), Critical Bonus (crit on 19-20, reroll damage ≤2), Lathander's Light aura, and Moonshield Aura (Shadow Curse protection). |

---

## Armor

### L13_Boots_Stormwalker (Boots of Stormwalker)
**Type:** Magic Boots | **Rarity:** Legendary

| Category | Details |
|----------|---------|
| Spells | Misty Step (unlimited) |
| Passives | Reverberation on status apply, Web Immunity |
| Description | Legendary boots that combine the power of storms with shadowstep magic. Grants Misty Step, applies Reverberation when inflicting conditions, and provides immunity to web and terrain effects. |

---

## Custom Spells

### L13_Target_Light_Unlimited
**Type:** Target Spell | **Cost:** Bonus Action, Unlimited

Standard Light cantrip with unlimited casting.

### L13_Target_BlindingSmite_Unlimited
**Type:** Target Spell | **Cost:** Action, Unlimited

**Name:** Tyr's Blinding Smite
**Description:** Blinding Smite. Unlimited uses.
**Used by:** Longsword of Tyr

### L13_Target_BlindingSmite_Moonguard
**Type:** Target Spell | **Cost:** Action, Unlimited

**Name:** Selûne's Blinding Smite
**Description:** Channel Selûne's radiance to blind your foes. Unlimited uses.
**Used by:** Moonguard Blade

### L13_Shout_CelestialHaste_Unlimited
**Type:** Shout Spell | **Cost:** Bonus Action, Unlimited

Based on Haste (Victory Longbow version). Unlimited casting.

### L13_Shout_CelestialHaste_Free
**Type:** Shout Spell | **Cost:** Free Action

Based on Haste (Victory Longbow version). Free action casting with no cooldown.

### L13_Target_MistyStep_Unlimited
**Type:** Target Spell | **Cost:** Unlimited

**Name:** Spectral Step
**Description:** Unlimited casting of Misty Step.

### L13_Shout_SpiritGuardians_Moonguard
**Type:** Container Spell | **Cost:** Free Action | **Level:** 3

**Name:** Moonguard Spirit Guardians
**Description:** Call forth spirits to protect you. Nearby enemies take 3d8 Radiant or Necrotic damage. Free action casting.

**Contains:**
- **Radiant Variant:** Radiant spirits surround you. Applies SPIRIT_GUARDIANS_RADIANT_AURA.
- **Necrotic Variant:** Necrotic spirits surround you. Applies SPIRIT_GUARDIANS_NECROTIC_AURA.

---

## Custom Passives

### L13_RadiantWeapon_Passive
**Name:** Radiant Weapon
**Description:** This weapon is infused with divine radiance, dealing extra radiant damage on melee attacks.
**Effect:** Adds 1d8 Radiant damage to melee attacks.

### L13_Moonshield_Passive
**Name:** Moonshield Aura
**Description:** Emanates a protective aura that shields allies from the Shadow Curse.
**Type:** Toggled (Default On)
**Effect:** Applies SCL_MOONSHIELD_AURA status (Shadow Curse protection).

---

## Custom Interrupts

### L13_Interrupt_Shield_Unlimited
**Name:** Shield (Unlimited)
**Description:** Cast Shield as a bonus action without expending spell slots.

### L13_Interrupt_Counterspell_Unlimited
**Name:** Counterspell (Unlimited)
**Description:** Cast Counterspell as a bonus action without expending spell slots.

---

## Delivery System

All items are delivered via the **L13_Gear_Chest** container, which appears in the **Tutorial Chest** (Nautiloid crash site).

**Acquisition:**
1. Complete tutorial and reach Nautiloid crash site
2. Open Tutorial Chest
3. Find L13_Gear_Chest (Legendary container)
4. Open L13_Gear_Chest to access all items

---

## Item Origins

| Item | Copied From | Phase |
|------|-------------|-------|
| Staff of Archmage | SampleMagicRingMod | Phase 029 |
| Longsword of Tyr | SampleMagicRingMod | Phase 032 |
| Boots of Stormwalker | SampleMagicRingMod | Phase 033 |
| Moonguard Blade | SampleMagicRingMod | Phase 033 |

All items have been made independent from SampleMagicRingMod with custom L13_ prefixes and unique UUIDs.

---

## Summary

| Category | Count |
|----------|-------|
| Weapons | 3 |
| Armor (Feet) | 1 |
| Custom Spells | 7 |
| Custom Passives | 2 |
| Custom Interrupts | 2 |
| **Total Items** | **4** |

---

## Technical Notes

- All items use `ed13` UUID prefix
- All handles use `hed13` prefix
- All items set to `Unique: 0` for TreasureTable delivery
- Items reuse some vanilla spells/passives (Plane Shifter Slayer, Wrathful Smite, etc.)
- No dependencies on SampleMagicRingMod - fully independent mod
- Container delivery means items won't appear in existing saves (see CLAUDE.md: Container Delivery Limitation)

---

## Version History

- **2026-02-10**: Phase 035 - Fixed item names and descriptions
  - Added description to Moonshield Aura passive
  - Created Selûne's Blinding Smite (moon-themed version for Moonguard Blade)
  - Moonguard Blade now uses Selûne-themed Blinding Smite
  - Longsword of Tyr continues to use Tyr's Blinding Smite
  - Kept vanilla CRE_LathandersLight_Passive (could not locate to customize)
  - Fixed Radiant Weapon damage to 1d8 (was incorrectly listed as 1d4)

- **2026-02-10**: Initial catalog created (Phase 034)
  - 4 items documented
  - Test ring removed from mod
