# Phase 021 - Staff of Akitaro Power Expansion

**Status:** COMPLETE

## Goal
- Add additional powers to the Staff of Akitaro to make it the ultimate arcane staff
- Add Haste (Self) power (unlimited, bonus action) to select magic items

---

## Current Staff of Akitaro

| Aspect | Value |
|--------|-------|
| Internal ID | SMR_Staff_Akitaro |
| MapKey | f1a2b3c4-d5e6-4f7a-8b9c-0d1e2f3a4b5c |
| Rarity | Legendary |

### Existing Powers
- Arcane Charge on Damage (Lightning Charges)
- Chromatic Attunement (change spell damage type)
- Spell Slot Restoration
- Pearlescent Restoration
- Unlimited Shield (reaction)
- Unlimited Counterspell (reaction)
- Unlimited Light
- Arcane Enchantment (+1 spell DC/attack)
- Arcane Battery (free spell after long rest)
- Mystra's Grace (+1 spell DC/attack)
- Weave's Reclamation (heal on spell damage)
- Echoes of Netheril (cantrip bonus damage)
- Celestial Haste (self-haste, bonus action)
- Akitaro's Blast, Teleport, Barrage, Shield

---

## New Powers to Add

### Defensive/Utility

| Power | Source Passive | Effect |
|-------|----------------|--------|
| **Absorb Elements** | Absorb_Elements_Passive | Reaction: gain resistance to elemental damage, add 1d6 to next melee attack |
| **Magical Durability** | MAG_MagicalDurability_Passive | +2 to saving throws vs spells |

### Offensive Synergies

| Power | Source Passive | Effect |
|-------|----------------|--------|
| **Radiating Orb** | MAG_Radiant_RadiatingOrb_Ring_Passive | Apply Radiating Orb on spell damage (-1 attack per stack, illuminates target) |
| **Reverberation** | MAG_Thunder_Reverberation_Gloves_Passive | Apply Reverberation on Thunder/Lightning/Radiant damage (-1 STR/DEX/CON saves per stack, blast at 5 stacks) |
| **Arcane Acuity** | MAG_Gish_ArcaneAcuity_Gloves_Passive | Gain Arcane Acuity on weapon attacks (+1 spell DC/attack per stack) |

### Light/Radiant Theme

| Power | Source Passive | Effect |
|-------|----------------|--------|
| **Callous Glow** | MAG_Radiant_DamageBonusOnIlluminatedTarget_Ring_Passive | +2 radiant damage vs illuminated targets |
| **Lathander's Light** | CRE_LathandersLight_Passive | Toggled 6m aura that blinds Fiends/Undead (CON 14 save) |

---

## Haste (Self) Power for Multiple Items

### Overview

Add the Haste (Self) power as an unlimited bonus action spell to select magic items. This is based on the Victory Longbow's `Shout_MAG_Victory_Longbow_Haste` spell, modified to be unlimited and cost a bonus action (like the existing `SMR_Shout_CelestialHaste_Unlimited` on Staff of Akitaro).

### Source Spell Reference

| Aspect | Value |
|--------|-------|
| Source Item | Gontr Mael / Victory Longbow |
| Source Spell | Shout_MAG_Victory_Longbow_Haste |
| Custom Spell | SMR_Shout_CelestialHaste_Unlimited |
| Cost | Bonus Action (unlimited) |
| Effect | Cast Haste on self |

### Items to Receive Haste (Self)

| Item | Internal ID | Current Boosts Line |
|------|-------------|---------------------|
| Sword of Tyr | SMR_Sword_Tyr | `Boosts` |
| Divine Maul | SMR_Maul_Divine | None (add new `Boosts` line) |
| Sword of Orpheus | SMR_Sword_Orpheus | `BoostsOnEquipMainHand` |

### Spell Definition (Spell_Shout.txt)

Already exists from Staff of Akitaro implementation:
```
new entry "SMR_Shout_CelestialHaste_Unlimited"
type "SpellData"
data "SpellType" "Shout"
using "Shout_MAG_Victory_Longbow_Haste"
data "UseCosts" "BonusActionPoint:1"
```

### Adding to Items

Add `UnlockSpell(SMR_Shout_CelestialHaste_Unlimited)` to each item's Boosts line.

#### Sword of Tyr (SMR_Sword_Tyr)
Current:
```
data "Boosts" "UnlockSpell(Target_MAG_Smite_Wrathful);UnlockSpell(SMR_Target_BlindingSmite_Unlimited);UnlockSpell(SMR_Target_Light_Unlimited);UnlockSpell(Target_PLA_ShieldOfFaith_SwordOfJustice)"
```
Updated:
```
data "Boosts" "UnlockSpell(Target_MAG_Smite_Wrathful);UnlockSpell(SMR_Target_BlindingSmite_Unlimited);UnlockSpell(SMR_Target_Light_Unlimited);UnlockSpell(Target_PLA_ShieldOfFaith_SwordOfJustice);UnlockSpell(SMR_Shout_CelestialHaste_Unlimited)"
```

#### Divine Maul (SMR_Maul_Divine)
Current: No Boosts line
Add:
```
data "Boosts" "UnlockSpell(SMR_Shout_CelestialHaste_Unlimited)"
```

#### Sword of Orpheus (SMR_Sword_Orpheus)
Current:
```
data "BoostsOnEquipMainHand" "UnlockSpell(Target_PommelStrike);UnlockSpell(Target_Slash_New);UnlockSpell(Zone_Cleave);UnlockSpell(Target_MAG_WeaponAction_Mindcrush)"
```
Updated:
```
data "BoostsOnEquipMainHand" "UnlockSpell(Target_PommelStrike);UnlockSpell(Target_Slash_New);UnlockSpell(Zone_Cleave);UnlockSpell(Target_MAG_WeaponAction_Mindcrush);UnlockSpell(SMR_Shout_CelestialHaste_Unlimited)"
```

---

## Implementation

### Updated Weapon Definition (Weapon.txt)

Current PassivesOnEquip:
```
MAG_CQCaster_GainArcaneChargeOnDamage_Quarterstaff_Passive;MAG_ArcaneEnchantment_Lesser_Passive;MAG_Legendary_Chromatic_Spellslot_Passive;WW_Mystra_SpellAttkBonus_Passive;WW_Mystra_Passive;WW_Netherese_Staff_Passive
```

New PassivesOnEquip (add these):
```
Absorb_Elements_Passive;MAG_MagicalDurability_Passive;MAG_Radiant_RadiatingOrb_Ring_Passive;MAG_Thunder_Reverberation_Gloves_Passive;MAG_Gish_ArcaneAcuity_Gloves_Passive;MAG_Radiant_DamageBonusOnIlluminatedTarget_Ring_Passive;CRE_LathandersLight_Passive
```

Full updated entry:
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

**Note:** Added `StatusOnEquip "MAG_LATHANDERS_LIGHT_TECHNICAL"` which is required for Lathander's Light passive to function properly (see Blood of Lathander reference in interesting_magical_effects.md).

---

## Implementation Checklist

### Staff of Akitaro
- [x] Update SMR_Staff_Akitaro in Weapon.txt with new passives
- [x] Add StatusOnEquip for Lathander's Light technical status
- [x] Update staff_of_akitaro.md planning document

### Haste (Self) on Other Items
- [x] Add Celestial Haste to SMR_Sword_Tyr (Boosts line)
- [x] Add Celestial Haste to SMR_Maul_Divine (new Boosts line)
- [x] Add Celestial Haste to SMR_Sword_Orpheus (BoostsOnEquipMainHand line)

### Final
- [ ] Build and test mod

---

## Test Plan

### New Passives
- [ ] Verify Absorb Elements reaction appears and can be triggered on elemental damage
- [ ] Verify Magical Durability grants +2 to saving throws vs spells
- [ ] Verify Radiating Orb applies on spell damage (check target for debuff icon)
- [ ] Verify Reverberation applies on Thunder/Lightning/Radiant damage
- [ ] Verify Arcane Acuity stacks appear when attacking with the staff
- [ ] Verify Callous Glow adds +2 radiant damage vs illuminated targets
- [ ] Verify Lathander's Light toggle appears and creates 6m aura
- [ ] Verify Lathander's Light blinds Fiends/Undead in combat

### Synergy Testing
- [ ] Test Radiating Orb + Callous Glow synergy (orb illuminates, glow adds damage)
- [ ] Test Arcane Acuity + spell casting (build stacks with staff attacks, cast powerful spell)
- [ ] Test Reverberation stacking to 5 for thunder blast

### Haste (Self) on Other Items
- [ ] Sword of Tyr: Verify Celestial Haste appears and works (bonus action, unlimited)
- [ ] Divine Maul: Verify Celestial Haste appears and works (bonus action, unlimited)
- [ ] Sword of Orpheus: Verify Celestial Haste appears and works (bonus action, unlimited)

---

## Notes

- All new passives are vanilla game passives, no custom definitions needed
- Lathander's Light requires the technical status to function (based on Blood of Lathander implementation)
- The staff now has excellent synergy between its radiant/lightning theme and the new passives
- Arcane Acuity rewards using the staff as a melee weapon before casting spells
- Radiating Orb + Callous Glow creates a light-based damage loop

---

## Power Summary (After Phase 21)

### Passive Abilities (13 total)
1. Arcane Charge on Damage (Lightning Charges)
2. Arcane Enchantment (+1 spell DC/attack)
3. Arcane Battery (free spell after long rest)
4. Mystra's Grace (+1 spell DC/attack)
5. Weave's Reclamation (heal on spell damage)
6. Echoes of Netheril (cantrip bonus damage)
7. **Absorb Elements** (NEW - elemental resistance reaction)
8. **Magical Durability** (NEW - +2 saves vs spells)
9. **Radiating Orb** (NEW - debuff on spell damage)
10. **Reverberation** (NEW - debuff on Thunder/Lightning/Radiant)
11. **Arcane Acuity** (NEW - spell bonus on weapon attacks)
12. **Callous Glow** (NEW - +2 radiant vs illuminated)
13. **Lathander's Light** (NEW - toggled blind aura)

### Active Abilities (11 total)
1. Light (unlimited)
2. Shield (unlimited reaction)
3. Counterspell (unlimited reaction)
4. Chromatic Attunement
5. Spell Slot Restoration
6. Pearlescent Restoration
7. Celestial Haste (bonus action)
8. Akitaro's Blast (short rest)
9. Akitaro's Teleport (short rest)
10. Akitaro's Barrage (bonus action, short rest)
11. Akitaro's Shield (bonus action, short rest)
