# Phase 015 - Armor of Tyr Enhancements

**Status:** COMPLETE

## Goal
Enhance the Armor of Tyr with additional mobility and utility powers.

---

## Current Implementation

From Phase 013, the Armor of Tyr has:

```
new entry "SMR_Armor_Tyr"
type "Armor"
using "ARM_HalfPlate_Body_2"
data "RootTemplate" "c3d4e5f6-a7b8-4c9d-0e1f-2a3b4c5d6e7f"
data "Rarity" "Legendary"
data "Boosts" "RollBonus(SavingThrow, 2);UnlockSpell(SMR_Shout_CelestialHaste_Unlimited)"
data "PassivesOnEquip" "MAG_ExoticMaterial_MediumArmor_Passive"
data "StatusOnEquip" "MAG_EXOTIC_MATERIAL_ARMOR_TECHNICAL"
data "Ability Modifier Cap" ""
data "Unique" "1"
```

### Current Powers

| Power | Description | Source |
|-------|-------------|--------|
| **Saving Throw Bonus** | +2 to all saving throws | `RollBonus(SavingThrow, 2)` |
| **No Dex Cap** | Full Dexterity bonus to AC | `MAG_ExoticMaterial_MediumArmor_Passive` |
| **Celestial Haste** | Cast Celestial Haste (bonus action, unlimited) | `SMR_Shout_CelestialHaste_Unlimited` |

---

## New Powers to Add

### Power 1: Unlimited Misty Step

| Power | Description | Source |
|-------|-------------|--------|
| **Spectral Step** | Cast Misty Step (unlimited, no action cost) | `SMR_Target_MistyStep_Unlimited` (existing) |

This spell already exists in our mod from the Ring of Spectral Power and Boots of the Stormwalker.

### Power 2: Spirit Guardians

| Power | Description | Source |
|-------|-------------|--------|
| **Tyr's Spirit Guardians** | Cast Spirit Guardians (unlimited) | New container spell (no item source exists) |

**Note:** No vanilla item grants Spirit Guardians. This requires the container spell technique documented in `adding_spells_without_item_source.md`.

Spirit Guardians has two damage type variants:
- **Radiant** - For good-aligned/neutral casters
- **Necrotic** - For evil-aligned casters

#### Implementation Approach

Based on the BapeerySpiritShoes mod reference, we need to create:

1. **Container Spell** - `SMR_Shout_SpiritGuardians_Tyr`
   - Lists both variants in `ContainerSpells`
   - Has `IsLinkedSpellContainer` flag

2. **Radiant Variant** - `SMR_Shout_SpiritGuardians_Tyr_Radiant`
   - Uses `Shout_SpiritGuardians` as base
   - Links back via `SpellContainerID`
   - Applies `SPIRIT_GUARDIANS_RADIANT_AURA` status

3. **Necrotic Variant** - `SMR_Shout_SpiritGuardians_Tyr_Necrotic`
   - Uses `Shout_SpiritGuardians` as base
   - Links back via `SpellContainerID`
   - Applies `SPIRIT_GUARDIANS_NECROTIC_AURA` status

#### UUIDs and Handles Needed

| Item | Type | Value |
|------|------|-------|
| Container DisplayName | Handle | `ha1b2c3d4eg5f6ag7b8cg9d0eg1f2a3b4c5d6` |
| Container Description | Handle | `hb2c3d4e5fg6a7bg8c9dg0e1fg2a3b4c5d6e7` |
| Radiant ExtraDescription | Handle | `hc3d4e5f6ag7b8cg9d0eg1f2ag3b4c5d6e7f8` |
| Necrotic ExtraDescription | Handle | `hd4e5f6a7bg8c9dg0e1fg2a3bg4c5d6e7f8a9` |

#### Spell Definitions

##### Container Spell (Spell_Shout.txt)
```
new entry "SMR_Shout_SpiritGuardians_Tyr"
type "SpellData"
data "SpellType" "Shout"
data "Level" "3"
data "SpellSchool" "Conjuration"
data "ContainerSpells" "SMR_Shout_SpiritGuardians_Tyr_Necrotic;SMR_Shout_SpiritGuardians_Tyr_Radiant"
data "AreaRadius" "3"
data "TargetConditions" "Self()"
data "Icon" "Spell_Conjuration_SpiritGuardians"
data "DisplayName" "ha1b2c3d4eg5f6ag7b8cg9d0eg1f2a3b4c5d6;1"
data "Description" "hb2c3d4e5fg6a7bg8c9dg0e1fg2a3b4c5d6e7;1"
data "DescriptionParams" "DealDamage(3d8,Radiant);DealDamage(3d8,Necrotic)"
data "TooltipAttackSave" "Wisdom"
data "PrepareSound" "Spell_Prepare_Damage_Radiant_Gen_L1to3"
data "PrepareLoopSound" "Spell_Prepare_Damage_Radiant_Gen_L1to3_Loop"
data "CastSound" "Spell_Cast_Damage_Radiant_SpiritGuardian_L1to3"
data "TargetSound" "Spell_Impact_Damage_Radiant_SpiritGuardian_L1to3"
data "CastTextEvent" "Cast"
data "UseCosts" "ActionPoint:1"
data "SpellAnimation" "03496c4a-49e0-4132-b585-3e5ecd1ad8e5,,;,,;cb171bda-f065-4520-b470-e447f678ba1f,,;18a9b8b8-6cec-4a6d-be46-a4cc499505e9,,;cc5b0caf-3ed1-4711-a50d-11dc3f1fdc6a,,;,,;0b07883a-08b8-43b6-ac18-84dc9e84ff50,,;,,;,,"
data "VerbalIntent" "Damage"
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsConcentration;IsSpell;IsHarmful;IsLinkedSpellContainer"
data "PrepareEffect" "2534712b-d31e-45a4-b8e3-6385caa9ddc1"
data "CastEffect" "56ea5092-8ecd-4b86-8686-c1c35d016928"
```

##### Radiant Variant (Spell_Shout.txt)
```
new entry "SMR_Shout_SpiritGuardians_Tyr_Radiant"
type "SpellData"
data "SpellType" "Shout"
using "Shout_SpiritGuardians"
data "SpellContainerID" "SMR_Shout_SpiritGuardians_Tyr"
data "ContainerSpells" ""
data "SpellProperties" "ApplyStatus(SPIRIT_GUARDIANS_RADIANT_AURA,100,10)"
data "Description" "hb2c3d4e5fg6a7bg8c9dg0e1fg2a3b4c5d6e7;1"
data "ExtraDescription" "hc3d4e5f6ag7b8cg9d0eg1f2ag3b4c5d6e7f8;1"
data "ExtraDescriptionParams" "DealDamage(3d8,Radiant)"
data "TooltipDamageList" "DealDamage(3d8,Radiant)"
data "TooltipStatusApply" "ApplyStatus(SPIRIT_GUARDIANS_RADIANT_AURA,100,10)"
data "UseCosts" "ActionPoint:1"
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsConcentration;IsSpell;IsHarmful"
data "DamageType" "Radiant"
```

##### Necrotic Variant (Spell_Shout.txt)
```
new entry "SMR_Shout_SpiritGuardians_Tyr_Necrotic"
type "SpellData"
data "SpellType" "Shout"
using "Shout_SpiritGuardians"
data "SpellContainerID" "SMR_Shout_SpiritGuardians_Tyr"
data "ContainerSpells" ""
data "SpellProperties" "ApplyStatus(SPIRIT_GUARDIANS_NECROTIC_AURA,100,10)"
data "Description" "hb2c3d4e5fg6a7bg8c9dg0e1fg2a3b4c5d6e7;1"
data "ExtraDescription" "hd4e5f6a7bg8c9dg0e1fg2a3bg4c5d6e7f8a9;1"
data "ExtraDescriptionParams" "DealDamage(3d8,Necrotic)"
data "TooltipDamageList" "DealDamage(3d8,Necrotic)"
data "TooltipStatusApply" "ApplyStatus(SPIRIT_GUARDIANS_NECROTIC_AURA,100,10)"
data "UseCosts" "ActionPoint:1"
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsConcentration;IsSpell;IsHarmful"
data "DamageType" "Necrotic"
```

#### Localization Entries

```xml
<content contentuid="ha1b2c3d4eg5f6ag7b8cg9d0eg1f2a3b4c5d6" version="1">Tyr's Spirit Guardians</content>
<content contentuid="hb2c3d4e5fg6a7bg8c9dg0e1fg2a3b4c5d6e7" version="1">Call forth spirits to protect you. Nearby enemies take 3d8 Radiant or Necrotic damage. Unlimited casting.</content>
<content contentuid="hc3d4e5f6ag7b8cg9d0eg1f2ag3b4c5d6e7f8" version="1">Radiant spirits surround you. Unlimited casting.</content>
<content contentuid="hd4e5f6a7bg8c9dg0e1fg2a3bg4c5d6e7f8a9" version="1">Necrotic spirits surround you. Unlimited casting.</content>
```

---

## Implementation Steps

### Step 1: Create Spirit Guardians Container Spell

Add container spell to `Spell_Shout.txt` (see spell definitions above).

### Step 2: Create Spirit Guardians Variant Spells

Add Radiant and Necrotic variants to `Spell_Shout.txt` (see spell definitions above).

### Step 3: Add Localization Entries

Add to both `SampleMagicRingMod.xml` and `SampleMagicRingMod.loca.xml` (see localization entries above).

### Step 4: Update Armor Stats in Armor.txt

Update the Boosts field to add both Misty Step and Spirit Guardians:

**Before:**
```
data "Boosts" "RollBonus(SavingThrow, 2);UnlockSpell(SMR_Shout_CelestialHaste_Unlimited)"
```

**After:**
```
data "Boosts" "RollBonus(SavingThrow, 2);UnlockSpell(SMR_Shout_CelestialHaste_Unlimited);UnlockSpell(SMR_Target_MistyStep_Unlimited);UnlockSpell(SMR_Shout_SpiritGuardians_Tyr,AddChildren,,,SpellCastingAbility)"
```

**Note:** The extended `UnlockSpell` syntax is required for container spells:
- `AddChildren` - Includes the variant spells
- `SpellCastingAbility` - Uses character's spellcasting ability for saves

---

## Implementation Checklist

### Spirit Guardians Spell Creation
- [x] Add SMR_Shout_SpiritGuardians_Tyr (container) to Spell_Shout.txt
- [x] Add SMR_Shout_SpiritGuardians_Tyr_Radiant (variant) to Spell_Shout.txt
- [x] Add SMR_Shout_SpiritGuardians_Tyr_Necrotic (variant) to Spell_Shout.txt
- [x] Add localization entries to SampleMagicRingMod.xml
- [x] Add localization entries to SampleMagicRingMod.loca.xml

### Armor of Tyr Enhancement
- [x] Add SMR_Target_MistyStep_Unlimited to SMR_Armor_Tyr Boosts in Armor.txt
- [x] Add SMR_Shout_SpiritGuardians_Tyr (with AddChildren syntax, unlimited) to SMR_Armor_Tyr Boosts in Armor.txt

### Final
- [ ] Build and test mod

---

## Test Plan

### Armor of Tyr - Misty Step
- [ ] Load game with mod enabled
- [ ] Equip Armor of Tyr
- [ ] Verify Spectral Step (Misty Step) spell is available
- [ ] Cast Misty Step and verify teleportation works
- [ ] Verify no action point is consumed
- [ ] Verify spell can be cast multiple times per turn (unlimited)

### Armor of Tyr - Spirit Guardians
- [ ] Equip Armor of Tyr
- [ ] Verify Tyr's Spirit Guardians spell is available
- [ ] Verify both Radiant and Necrotic variants appear when selecting the spell
- [ ] Cast Radiant variant and verify:
  - [ ] Spirits appear around character
  - [ ] Enemies entering aura take Radiant damage
  - [ ] Concentration is required
- [ ] Cast Necrotic variant and verify:
  - [ ] Spirits appear around character
  - [ ] Enemies entering aura take Necrotic damage
  - [ ] Concentration is required
- [ ] End concentration and verify spell can be cast again immediately (unlimited)

---

## Bug Fixes

### Armor of Tyr Name Collision (2026-02-01)

**Issue:** The Armor of Tyr was displaying as "Radiant spirits surround you. Unlimited casting." instead of "Armor of Tyr".

**Root Cause:** Handle collision between Armor of Tyr and Spirit Guardians spell variants:
- Armor of Tyr DisplayName: `hc3d4e5f6ag7b8cg9d0eg1f2ag3b4c5d6e7f8`
- Spirit Guardians Radiant ExtraDescription: `hc3d4e5f6ag7b8cg9d0eg1f2ag3b4c5d6e7f8` (SAME!)
- Armor of Tyr Description: `hd4e5f6a7bg8c9dg0e1fg2a3bg4c5d6e7f8a9`
- Spirit Guardians Necrotic ExtraDescription: `hd4e5f6a7bg8c9dg0e1fg2a3bg4c5d6e7f8a9` (SAME!)

The XML parser uses the last definition for duplicate content UIDs, so the Spirit Guardians text was overwriting the Armor of Tyr name and description.

**Solution:** Changed Spirit Guardians spell ExtraDescription handles to new unique values:
- Radiant: `hc3d4e5f6ag7b8cg9d0eg1f2ag3b4c5d6e7f8` → `he5f6a7b8cg9d0eg1f2ag3b4cg8c9d0e1f2a3b4`
- Necrotic: `hd4e5f6a7bg8c9dg0e1fg2a3bg4c5d6e7f8a9` → `hf6a7b8c9dg0e1fg2a3bg4c5dg9d0e1f2a3b4c5`

**Files Modified:**
- `Stats/Generated/Data/Spell_Shout.txt` - Updated ExtraDescription handles for both Spirit Guardians variants
- `Localization/English/SampleMagicRingMod.xml` - Updated content UIDs for Spirit Guardians entries
- `Localization/English/SampleMagicRingMod.loca.xml` - Updated content UIDs for Spirit Guardians entries

---

## Notes

- Reuses existing `SMR_Target_MistyStep_Unlimited` spell - no new spell creation needed
- Spirit Guardians requires the container spell technique since no vanilla item grants it
- Reference: BapeerySpiritShoes mod in `BapeerySpiritShoes_428af67a-6681-3cd6-8203-18fff09c3282/`
- The extended `UnlockSpell` syntax with `AddChildren` is required for container spells
- Spirit Guardians is a concentration spell - cannot be active with Celestial Haste simultaneously
- Although unlimited, concentration limits practical usage (only one instance active at a time)
- This makes the Armor of Tyr excellent for mobile frontline casters (Clerics, Paladins)
