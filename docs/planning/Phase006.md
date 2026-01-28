# Phase 006 - Create Staff of the Archmage

**Status:** PENDING

## Goal
Create the Staff of the Archmage based on Markoheshkir with additional powers.

## Overview

The Staff of the Archmage is based on **Markoheshkir (MAG_TheChromatic_Staff)** - a Legendary +2 Quarterstaff with:
- Chromatic Attunement (choose elemental attunement, once per short rest)
- Arcane Enchantment (+1 Spell Save DC, +1 Spell Attack Rolls)
- Arcane Battery (once per long rest, next spell doesn't consume a spell slot)

We will copy all of Markoheshkir's powers and add:
- Unlimited Shield (reaction, no cost)
- Unlimited Counterspell (reaction, no cost)
- Spell Slot Restoration (from Spellcrux Amulet - restore L1-L6 spell slot, once per long rest)
- Pearlescent Restoration (from Pearl of Power - restore L1-L3 spell slot, once per long rest)
- Mystra's Grace (from WW_Wizard_Equipment mod - +half wizard level to spell attack rolls)
- Weave's Reclamation (from WW_Wizard_Equipment mod - chance to restore spell slot when hit by spell)
- Echoes of Netheril (from WW_Wizard_Equipment mod - chance to restore spell slot when casting a spell)

---

## Design Decisions

| Aspect | Decision |
|--------|----------|
| Name | Staff of the Archmage |
| Internal ID | SMR_Staff_Archmage |
| Base Weapon | WPN_Quarterstaff_2 (+2 Quarterstaff) |
| Appearance | Same as Spellsparkler (MAG_CQCaster_GainArcaneChargeOnDamage_Quarterstaff) |
| VisualTemplate | 91b88b2e-09c7-8523-ee50-df363cef3d9f |
| ParentTemplateId | d25bc94a-5ee9-448f-9210-f2dad61ae7e5 (Spellsparkler parent) |
| Rarity | Legendary |

### Powers

| Status | Power | Description | Source |
|--------|-------|-------------|--------|
| [ ] | **Chromatic Attunement** | Choose elemental attunement (once per short rest) | Markoheshkir |
| [ ] | **Arcane Enchantment** | +1 Spell Save DC, +1 Spell Attack Rolls | Markoheshkir |
| [ ] | **Arcane Battery** | Once per long rest, next spell costs no spell slot | Markoheshkir |
| [ ] | **Unlimited Shield** | Cast Shield as a reaction (unlimited) | Phase 5 |
| [ ] | **Unlimited Counterspell** | Cast Counterspell as a reaction (unlimited) | Phase 5 |
| [ ] | **Spell Slot Restoration** | Restore one spell slot L1-L6 (once per long rest) | Spellcrux Amulet |
| [ ] | **Pearlescent Restoration** | Restore one spell slot L1-L3 (once per long rest) | Pearl of Power |
| [ ] | **Mystra's Grace** | +half Wizard level to spell attack rolls | Mystra's Lost Robe (WW mod) |
| [ ] | **Weave's Reclamation** | Chance to restore spell slot when hit by spell (once/turn) | Mystra's Lost Robe (WW mod) |
| [ ] | **Echoes of Netheril** | Chance to restore spell slot when casting a spell (once/turn) | Netherese Staff (WW mod) |

---

## Reference: Source Items

### Markoheshkir (MAG_TheChromatic_Staff)
```
new entry "MAG_TheChromatic_Staff"
type "Weapon"
using "WPN_Quarterstaff_2"
data "RootTemplate" "7e39ad11-f8c3-421a-940c-05348c420c7d"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(Shout_MAG_TheChromatic_ChromaticAttunement)"
data "PassivesOnEquip" "MAG_ArcaneEnchantment_Lesser_Passive;MAG_Legendary_Chromatic_Spellslot_Passive"
data "StatusOnEquip" "MAG_THE_CHROMATIC_TECHNICAL"
data "Unique" "1"
```

### Spellcrux Amulet (MAG_Restoration_SpellSlotRestoration_Amulet)
```
new entry "MAG_Restoration_SpellSlotRestoration_Amulet"
type "Armor"
using "_Amulet_Magic"
data "RootTemplate" "ba147dc7-98bc-4bfb-9fbc-efa1735d0841"
data "Rarity" "VeryRare"
data "Boosts" "UnlockSpell(Shout_MAG_SpellSlotRestoration)"
data "Unique" "1"
```
- Spell restores one spell slot of your choice (L1-L6), once per long rest
- Uses bonus action

### Pearl of Power Amulet
```
new entry "MAG_PHB_PearlOfPower_Amulet"
type "Armor"
using "ARM_Amulet_Necklace_C_Bronze_A"
data "RootTemplate" "6b8fcc06-fa6a-4a11-8318-075d90d8e909"
data "Rarity" "Uncommon"
data "Boosts" "UnlockSpell(Shout_MAG_SpellSlotRestoration_PearlOfPower)"
data "Unique" "1"
```
- Spell restores one spell slot of your choice (L1-L3), once per long rest

### Mystra's Lost Robe (WW_Wizard_Equipment mod)
```
new entry "WW_Wizard_Equipment_Mystras_Lost_Robe"
type "Armor"
using "_Armor_Magic_Robe"
data "RootTemplate" "bd802d1d-c8a9-4e48-b2eb-2b0c6bca90b9"
data "Rarity" "Legendary"
data "Boosts" "AC(2)"
data "PassivesOnEquip" "WW_Mystra_SpellAttkBonus_Passive;WW_Mystra_Passive"
```

**WW_Mystra_SpellAttkBonus_Passive** (Mystra's Grace):
```
new entry "WW_Mystra_SpellAttkBonus_Passive"
type "PassiveData"
data "DisplayName" "h941a2a1agcc5ag4161gb947g4797cc56ab52;1"
data "Description" "h941a2a1agcc5ag4161gb947g4797cc56ab60;1"
data "Boosts" "RollBonus(MeleeSpellAttack, ClassLevel(Wizard)/2);RollBonus(RangedSpellAttack,ClassLevel(Wizard)/2)"
```
- +half Wizard level to spell attack rolls

**WW_Mystra_Passive** (Weave's Reclamation):
```
new entry "WW_Mystra_Passive"
type "PassiveData"
data "DisplayName" "h941a2a1agcc5ag4161gb947g4797cc56ab53;1"
data "Description" "h941a2a1agcc5ag4161gb947g4797cc56ab54;1"
data "Icon" "PassiveFeature_Generic_Magical"
data "Properties" "Highlighted;OncePerTurn"
data "StatsFunctorContext" "OnDamaged"
data "Conditions" "HasSpellFlag(SpellFlags.Spell) and Combat() and HasLastAttackTriggered() and not IsCantrip() and not NumberOfTargetsGreaterThan(1) and not WWMultiTargetSpellCheck()"
data "StatsFunctors" "IF(SpellPowerLevelEqualTo(1) and RollDieAgainstDC(DiceType.d100,70)):ApplyStatus(WW_RESTORE_SPELLSLOT_ONE,100,0,context.Source);IF(SpellPowerLevelEqualTo(2) and RollDieAgainstDC(DiceType.d100,75)):ApplyStatus(WW_RESTORE_SPELLSLOT_TWO,100,0,context.Source);IF(SpellPowerLevelEqualTo(3) and RollDieAgainstDC(DiceType.d100,80)):ApplyStatus(WW_RESTORE_SPELLSLOT_THREE,100,0,context.Source);IF(SpellPowerLevelEqualTo(4) and RollDieAgainstDC(DiceType.d100,85)):ApplyStatus(WW_RESTORE_SPELLSLOT_FOUR,100,0,context.Source);IF(SpellPowerLevelEqualTo(5) and RollDieAgainstDC(DiceType.d100,90)):ApplyStatus(WW_RESTORE_SPELLSLOT_FIVE,100,0,context.Source)"
```
- When hit by a spell in combat, chance to restore spell slot of that level
- L1: 70%, L2: 75%, L3: 80%, L4: 85%, L5: 90% chance
- Once per turn

**Note:** These passives use `ClassLevel(Wizard)` - the Mystra's Grace bonus scales with Wizard level. We assume WW_Wizard_Equipment mod is installed as a dependency.

### Netherese Staff (WW_Wizard_Equipment mod)
```
new entry "WW_Wizard_Equipment_Netherese_Staff"
type "Weapon"
using "WPN_Quarterstaff_1"
data "RootTemplate" "ed188ba5-2d79-4f8a-a0c1-14cbec5a8c3c"
data "Rarity" "Legendary"
data "DefaultBoosts" "WeaponProperty(Magical);WeaponEnchantment(3)"
data "Boosts" "UnlockSpell(WW_Shout_Netherstrike)"
data "PassivesOnEquip" "WW_Netherese_Staff_Passive;MAG_ArcaneEnchantment_Lesser_Passive"
```

**WW_Netherese_Staff_Passive** (Echoes of Netheril):
```
new entry "WW_Netherese_Staff_Passive"
type "PassiveData"
data "DisplayName" "h941a2a1agcc5ag4161gb947g4797cc56ab43;1"
data "Description" "h941a2a1agcc5ag4161gb947g4797cc56ab44;1"
data "Icon" "PassiveFeature_Generic_Magical"
data "Properties" "Highlighted;OncePerTurn"
data "StatsFunctorContext" "OnCast"
data "Conditions" "HasSpellFlag(SpellFlags.Spell) and Combat() and not IsCantrip() and not WWMultiTargetSpellCheck()"
data "StatsFunctors" "IF(SpellPowerLevelEqualTo(1) and RollDieAgainstDC(DiceType.d100,76)):ApplyStatus(SELF,WW_STAFF_RESTORE_SPELLSLOT_ONE,100, 0);IF(SpellPowerLevelEqualTo(2) and RollDieAgainstDC(DiceType.d100,80)):ApplyStatus(SELF,WW_STAFF_RESTORE_SPELLSLOT_TWO,100, 0);IF(SpellPowerLevelEqualTo(3) and RollDieAgainstDC(DiceType.d100,84)):ApplyStatus(SELF,WW_STAFF_RESTORE_SPELLSLOT_THREE,100, 0);IF(SpellPowerLevelEqualTo(4) and RollDieAgainstDC(DiceType.d100,88)):ApplyStatus(SELF,WW_STAFF_RESTORE_SPELLSLOT_FOUR,100, 0);IF(SpellPowerLevelEqualTo(5) and RollDieAgainstDC(DiceType.d100,92)):ApplyStatus(SELF,WW_STAFF_RESTORE_SPELLSLOT_FIVE,100, 0)"
```
- When casting a spell in combat, chance to restore spell slot of that level
- L1: 76%, L2: 80%, L3: 84%, L4: 88%, L5: 92% chance
- Once per turn

---

## UUIDs and Handles Needed

| Item | Type | Value |
|------|------|-------|
| Staff MapKey | UUID | `c2d3e4f5-a6b7-4c8d-9e0f-1a2b3c4d5e6f` |
| OneTimeReward | UUID | `d3e4f5a6-b7c8-4d9e-0f1a-2b3c4d5e6f7a` |
| Staff DisplayName | Handle | `h0a1b2c3dge4f5g6a7bg8c9dg0e1f2a3b4c5d6` |
| Staff Description | Handle | `ha1b2c3d4gf5e6g7a8bg9c0dg1e2f3a4b5c6d7` |

Note: Shield and Counterspell interrupts already exist from Phase 5:
- `SMR_Interrupt_Shield_Unlimited`
- `SMR_Interrupt_Counterspell_Unlimited`

---

## Files to Create/Modify

### 1. NEW FILE: Stats/Generated/Data/Weapon.txt

Create file with Staff of the Archmage:
```
new entry "SMR_Staff_Archmage"
type "Weapon"
using "WPN_Quarterstaff_2"
data "RootTemplate" "c2d3e4f5-a6b7-4c8d-9e0f-1a2b3c4d5e6f"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(Shout_MAG_TheChromatic_ChromaticAttunement);UnlockSpell(Shout_MAG_SpellSlotRestoration);UnlockSpell(Shout_MAG_SpellSlotRestoration_PearlOfPower);UnlockInterrupt(SMR_Interrupt_Shield_Unlimited);UnlockInterrupt(SMR_Interrupt_Counterspell_Unlimited)"
data "PassivesOnEquip" "MAG_ArcaneEnchantment_Lesser_Passive;MAG_Legendary_Chromatic_Spellslot_Passive;WW_Mystra_SpellAttkBonus_Passive;WW_Mystra_Passive;WW_Netherese_Staff_Passive"
data "Unique" "1"
```

**Boosts breakdown:**
- `UnlockSpell(Shout_MAG_TheChromatic_ChromaticAttunement)` - Chromatic Attunement (from Markoheshkir)
- `UnlockSpell(Shout_MAG_SpellSlotRestoration)` - Spell Slot Restoration L1-L6 (from Spellcrux)
- `UnlockSpell(Shout_MAG_SpellSlotRestoration_PearlOfPower)` - Pearlescent Restoration L1-L3 (from Pearl of Power)
- `UnlockInterrupt(SMR_Interrupt_Shield_Unlimited)` - Unlimited Shield (from Phase 5)
- `UnlockInterrupt(SMR_Interrupt_Counterspell_Unlimited)` - Unlimited Counterspell (from Phase 5)

**PassivesOnEquip breakdown:**
- `MAG_ArcaneEnchantment_Lesser_Passive` - +1 Spell Save DC, +1 Spell Attack (from Markoheshkir)
- `MAG_Legendary_Chromatic_Spellslot_Passive` - Arcane Battery (from Markoheshkir)
- `WW_Mystra_SpellAttkBonus_Passive` - Mystra's Grace: +half Wizard level to spell attacks (from WW mod)
- `WW_Mystra_Passive` - Weave's Reclamation: Chance to restore spell slot when hit by spell (from WW mod)
- `WW_Netherese_Staff_Passive` - Echoes of Netheril: Chance to restore spell slot when casting a spell (from WW mod)

### 2. RootTemplates/merged.lsx AND merged.lsf.lsx

Add GameObjects node for Staff (using Spellsparkler appearance):
```xml
<node id="GameObjects">
    <attribute id="Description" type="TranslatedString" handle="ha1b2c3d4gf5e6g7a8bg9c0dg1e2f3a4b5c6d7" version="1" />
    <attribute id="DisplayName" type="TranslatedString" handle="h0a1b2c3dge4f5g6a7bg8c9dg0e1f2a3b4c5d6" version="1" />
    <attribute id="ExamineRotation" type="fvec3" value="75 180 0" />
    <attribute id="LevelName" type="FixedString" value="" />
    <attribute id="MapKey" type="FixedString" value="c2d3e4f5-a6b7-4c8d-9e0f-1a2b3c4d5e6f" />
    <attribute id="Name" type="LSString" value="SMR_Staff_Archmage" />
    <attribute id="ParentTemplateId" type="FixedString" value="d25bc94a-5ee9-448f-9210-f2dad61ae7e5" />
    <attribute id="Stats" type="FixedString" value="SMR_Staff_Archmage" />
    <attribute id="Type" type="FixedString" value="item" />
    <attribute id="VisualTemplate" type="FixedString" value="91b88b2e-09c7-8523-ee50-df363cef3d9f" />
    <attribute id="_OriginalFileVersion_" type="int64" value="144115188075855912" />
    <children>
        <node id="GameMaster" />
    </children>
</node>
```

### 3. Localization/English/SampleMagicRingMod.xml AND .loca.xml

Add localization entries:
```xml
<content contentuid="h0a1b2c3dge4f5g6a7bg8c9dg0e1f2a3b4c5d6" version="1">Staff of the Archmage</content>
<content contentuid="ha1b2c3d4gf5e6g7a8bg9c0dg1e2f3a4b5c6d7" version="1">A legendary staff imbued with the essence of the Weave itself. Grants Chromatic Attunement, Arcane Enchantment, Arcane Battery, Spell Slot Restoration, Pearlescent Restoration, Mystra's Grace, Weave's Reclamation, Echoes of Netheril, and unlimited Shield and Counterspell reactions.</content>
```

### 4. OneTimeRewards/OneTimeRewards.lsx

Add OneTimeReward entry:
```xml
<node id="OneTimeReward">
    <attribute id="Amount" type="uint32" value="1"/>
    <attribute id="ItemTemplateId" type="FixedString" value="c2d3e4f5-a6b7-4c8d-9e0f-1a2b3c4d5e6f"/>
    <attribute id="UUID" type="guid" value="d3e4f5a6-b7c8-4d9e-0f1a-2b3c4d5e6f7a"/>
</node>
```

---

## Implementation Order

1. [ ] Create Weapon.txt with SMR_Staff_Archmage entry
2. [ ] Add staff to merged.lsx
3. [ ] Add staff to merged.lsf.lsx
4. [ ] Add localization to SampleMagicRingMod.xml
5. [ ] Add localization to SampleMagicRingMod.loca.xml
6. [ ] Add to OneTimeRewards.lsx
7. [ ] Build and test mod

---

## Test Plan

**Prerequisites:** WW_Wizard_Equipment mod must be installed

- [ ] Build mod with BG3 Modder's Multitool
- [ ] Load game with mod enabled (ensure WW_Wizard_Equipment is also enabled)
- [ ] Go to camp and check Traveler's Chest
- [ ] Equip Staff of the Archmage
- [ ] Verify staff appears with correct appearance (Spellsparkler visual)
- [ ] Verify staff description displays correctly

### Markoheshkir Powers
- [ ] Verify "Chromatic Attunement" spell appears and works (choose element, once per short rest)
- [ ] Verify Arcane Enchantment passive is active (+1 spell save DC, +1 spell attack)
- [ ] Verify Arcane Battery passive works (once per long rest free spell)

### Phase 5 Powers
- [ ] Verify Shield reaction is available and works (unlimited)
- [ ] Verify Counterspell reaction is available and works (unlimited)

### Spellcrux Powers
- [ ] Verify "Spell Slot Restoration" spell appears (restore L1-L6 slot, once per long rest)

### Pearl of Power Powers
- [ ] Verify "Pearlescent Restoration" spell appears (restore L1-L3 slot, once per long rest)

### Mystra's Lost Robe Powers (from WW mod)
- [ ] Verify "Mystra's Grace" passive is active (+half Wizard level to spell attacks)
- [ ] Verify "Weave's Reclamation" passive works (chance to restore spell slot when hit by spell)

### Netherese Staff Powers (from WW mod)
- [ ] Verify "Echoes of Netheril" passive works (chance to restore spell slot when casting a spell)

---

## Notes

- Staff uses Weapon type, not Armor type
- Reuses Markoheshkir's visual template and icon for appearance
- Reuses existing game passives:
  - `MAG_ArcaneEnchantment_Lesser_Passive` (Markoheshkir)
  - `MAG_Legendary_Chromatic_Spellslot_Passive` (Markoheshkir)
- Reuses passives from WW_Wizard_Equipment mod:
  - `WW_Mystra_SpellAttkBonus_Passive` (Mystra's Grace)
  - `WW_Mystra_Passive` (Weave's Reclamation)
  - `WW_Netherese_Staff_Passive` (Echoes of Netheril)
  - **Assumption:** WW_Wizard_Equipment mod is installed as a dependency
- Reuses existing game spells:
  - `Shout_MAG_TheChromatic_ChromaticAttunement` (Markoheshkir)
  - `Shout_MAG_SpellSlotRestoration` (Spellcrux Amulet)
  - `Shout_MAG_SpellSlotRestoration_PearlOfPower` (Pearl of Power)
- Reuses interrupts from Phase 5:
  - `SMR_Interrupt_Shield_Unlimited`
  - `SMR_Interrupt_Counterspell_Unlimited`
- Shield and Counterspell use the Interrupt system, not spells (learned in Phase 5)

---

## Future Powers (To Be Added Later)

- Chromatic Orb L3
