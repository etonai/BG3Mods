# Level13PlusGear Item Catalog

A complete list of all magic items in the Level13PlusGear mod.

---

## Weapons

### L13_Staff_Archmage (Staff of the Archmage)
**Type:** Quarterstaff | **Rarity:** Legendary

| Category | Details |
|----------|---------|
| Spells | Chromatic Orb (unlimited), Magic Missile (unlimited), Chromatic Attunement, Spell Slot Restoration (2 versions), Light (unlimited), Shield (unlimited), Counterspell (unlimited) |
| Passives | Arcane Enchantment (+1 spell DC/attack), Chromatic Spellslot, Mystra's Blessing (spell attack bonus), Netherese Staff |
| Description | A legendary staff imbued with the essence of the Weave itself. Grants unlimited Chromatic Orb and Magic Missile, Chromatic Attunement, Arcane Enchantment, Arcane Battery, Spell Slot Restoration, Pearlescent Restoration, Mystra's Grace, Weave's Reclamation, Echoes of Netheril, and unlimited Shield and Counterspell reactions. |

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

### L13_Ring_Spectral_Power (Ring of Spectral Power)
**Type:** Ring | **Rarity:** Legendary

| Category | Details |
|----------|---------|
| Spells | Magic Missile Lvl3 (unlimited, bonus action), Globe of Invulnerability (short rest), Misty Step (unlimited), Hold Person (unlimited), Artistry of War (short rest), Invisibility (short rest), Knock (unlimited), Arcane Gate (short rest), Telekinesis (short rest) |
| Interrupts | Shield (unlimited) |
| Passives | Forceweaver (+1d4 Force on spell attack) |
| Description | A ring crackling with arcane force. Grants powerful spectral magic including 5-missile Magic Missile, defensive Globe of Invulnerability, control spells (Hold Person), utility spells (Knock, Invisibility), teleportation (Misty Step, Arcane Gate), and manipulation (Telekinesis). |

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

### L13_Projectile_ChromaticOrb_Unlimited
**Type:** Projectile Spell | **Cost:** Action, Unlimited | **Level:** 1

**Name:** Chromatic Orb
**Description:** Hurl a sphere of energy that deals 3d8 damage. Choose from Acid, Cold, Fire, Lightning, Poison, or Thunder damage. Unlimited uses.

**Damage Types (choose one):**
- Acid: 3d8 Acid damage, creates acid surface
- Cold: 3d8 Cold damage
- Fire: 3d8 Fire damage
- Lightning: 3d8 Lightning damage
- Poison: 3d8 Poison damage
- Thunder: 3d8 Thunder damage

**Used by:** Staff of the Archmage

### L13_Projectile_MagicMissile_Unlimited
**Type:** Projectile Spell | **Cost:** Action, Unlimited | **Level:** 1

**Name:** Magic Missile
**Description:** Create three darts of magical force that automatically hit their target. Each dart deals 1d4+1 Force damage (3d4+3 total). Can target up to 3 different creatures. Unlimited uses.

**Damage:** 3d4+3 Force (7-15 guaranteed damage, no attack roll)
**Missiles:** 3 missiles (can split between targets)

**Used by:** Staff of the Archmage

### L13_Projectile_MagicMissile_Unlimited_Lvl3
**Type:** Projectile Spell | **Cost:** Bonus Action, Unlimited | **Level:** 3

**Name:** Spectral Barrage
**Description:** Create five darts of magical force that automatically hit their target. Each dart deals 1d4+1 Force damage (5d4+5 total). Can target up to 3 different creatures. Unlimited uses.

**Damage:** 5d4+5 Force (10-25 guaranteed damage, no attack roll)
**Missiles:** 5 missiles (can split between targets)

**Used by:** Ring of Spectral Power

### L13_Projectile_ArtistryOfWar_ShortRest
**Type:** Projectile Spell | **Cost:** Once per Short Rest

**Name:** Spectral Artistry
**Description:** Artistry of War. Once per short rest.

**Used by:** Ring of Spectral Power

### L13_Target_HoldPerson_Unlimited
**Type:** Target Spell | **Cost:** Bonus Action, Unlimited

**Name:** Spectral Hold
**Description:** Unlimited Hold Person as a bonus action. Paralyzes a humanoid target.

**Used by:** Ring of Spectral Power

### L13_Target_Invisibility_ShortRest
**Type:** Target Spell | **Cost:** Once per Short Rest

**Name:** Spectral Veil
**Description:** Invisibility. Recharges on short rest.

**Used by:** Ring of Spectral Power

### L13_Target_Knock_Unlimited
**Type:** Target Spell | **Cost:** Bonus Action, Unlimited

**Name:** Spectral Knock
**Description:** Unlimited Knock as a bonus action. Unlocks doors and containers.

**Used by:** Ring of Spectral Power

### L13_Target_GlobeOfInvulnerability_ShortRest
**Type:** Zone Spell | **Cost:** Bonus Action, Once per Short Rest

**Name:** Spectral Barrier
**Description:** Globe of Invulnerability. Recharges on short rest. Creates a protective barrier against spells.

**Used by:** Ring of Spectral Power

### L13_Teleportation_ArcaneGate_ShortRest
**Type:** Teleportation Spell | **Cost:** Once per Short Rest

**Name:** Spectral Gate
**Description:** Arcane Gate. Recharges on short rest. Creates two linked portals for teleportation.

**Used by:** Ring of Spectral Power

### L13_Throw_Telekinesis_ShortRest
**Type:** Throw Spell | **Cost:** Action, Once per Short Rest

**Name:** Telekinesis
**Description:** Telekinesis. Recharges on short rest. Manipulate objects and creatures with your mind.

**Used by:** Ring of Spectral Power

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
| Armor (Ring) | 1 |
| Custom Spells | 16 |
| Custom Passives | 2 |
| Custom Interrupts | 2 |
| **Total Items** | **5** |

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

- **2026-02-11**: Phase 037 - Added spells to Staff and copied Ring of Spectral Power
  - Added Chromatic Orb (unlimited, level 1) to Staff of the Archmage
  - Added Magic Missile (unlimited, level 1) to Staff of the Archmage
  - Copied Ring of Spectral Power from SampleMagicRingMod to Level13PlusGear
  - Ring includes 9 custom spells: Magic Missile Lvl3, Globe of Invulnerability, Hold Person, Artistry of War, Invisibility, Knock, Arcane Gate, Telekinesis
  - Created 3 new spell file types: Spell_Zone.txt, Spell_Teleportation.txt, Spell_Throw.txt
  - Ring fully independent from SampleMagicRingMod with custom L13 prefixes
  - Total item count: 5 items (3 weapons, 1 boots, 1 ring)
  - Total custom spell count: 16 spells

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
