# Adding Spells to Items When No Item Source Exists

## Overview

When adding a spell as an item power in BG3, there are two scenarios:

1. **Simple Case**: An existing item already grants the spell - just copy and modify
2. **Complex Case**: No item grants the spell - must create from the class spell

This document covers the complex case, using the BapeerySpiritShoes mod as a reference.

---

## The Problem

Most BG3 spells exist in two forms:
- **Class spells**: What characters learn (e.g., `Shout_SpiritGuardians`)
- **Item spells**: Modified versions granted by items (e.g., `Target_UNI_MistyStep_NightWalkers`)

Item spells typically have:
- Modified `UseCosts` (no spell slot requirement)
- Modified `Cooldown` (once per rest, etc.)
- Sometimes modified effects or damage

When no item grants a spell, you must create the item version yourself.

---

## Solution Approaches

### Approach 1: Simple Single-Variant Spell

For spells without damage type choices or upcast variants:

```
new entry "SMR_Shout_MySpell_Unlimited"
type "SpellData"
data "SpellType" "Shout"
using "Shout_OriginalSpell"        <-- Inherit from class spell
data "UseCosts" "BonusActionPoint:1"
data "Cooldown" ""                  <-- Or "OncePerShortRest", etc.
```

**When to use**: Simple spells like Bless, Haste, See Invisibility

---

### Approach 2: Container Spell with Variants

For spells with multiple variants (damage types, upcast levels):

#### Step 1: Create the Container Spell

```
new entry "MyMod_Shout_SpiritGuardians"
type "SpellData"
data "SpellType" "Shout"
data "Level" "3"
data "SpellSchool" "Conjuration"
data "ContainerSpells" "MyMod_Shout_SpiritGuardians_Necrotic;MyMod_Shout_SpiritGuardians_Radiant"
data "Cooldown" "OncePerShortRest"
data "AreaRadius" "3"
data "TargetConditions" "Self()"
data "Icon" "Spell_Conjuration_SpiritGuardians"
data "DisplayName" "hYOUR_HANDLE_HERE;1"
data "Description" "hYOUR_HANDLE_HERE;1"
data "DescriptionParams" "DealDamage(3d8,Radiant);DealDamage(3d8,Necrotic)"
data "TooltipAttackSave" "Wisdom"
data "PrepareSound" "Spell_Prepare_Damage_Radiant_Gen_L1to3"
data "PrepareLoopSound" "Spell_Prepare_Damage_Radiant_Gen_L1to3_Loop"
data "CastSound" "Spell_Cast_Damage_Radiant_SpiritGuardian_L1to3"
data "TargetSound" "Spell_Impact_Damage_Radiant_SpiritGuardian_L1to3"
data "CastTextEvent" "Cast"
data "UseCosts" "ActionPoint:1"
data "SpellAnimation" "03496c4a-49e0-4132-b585-3e5ecd1ad8e5,,;,,;..."
data "VerbalIntent" "Damage"
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsConcentration;IsSpell;IsHarmful;IsLinkedSpellContainer"
data "PrepareEffect" "2534712b-d31e-45a4-b8e3-6385caa9ddc1"
data "CastEffect" "56ea5092-8ecd-4b86-8686-c1c35d016928"
```

**Key container properties:**
- `ContainerSpells` - Semicolon-separated list of variant spells
- `IsLinkedSpellContainer` - Flag in SpellFlags

#### Step 2: Create Variant Spells

```
new entry "MyMod_Shout_SpiritGuardians_Necrotic"
type "SpellData"
data "SpellType" "Shout"
using "Shout_SpiritGuardians"              <-- Inherit from class spell
data "SpellContainerID" "MyMod_Shout_SpiritGuardians"
data "ContainerSpells" ""                   <-- Clear inherited container
data "Cooldown" "OncePerShortRest"
data "SpellProperties" "ApplyStatus(SPIRIT_GUARDIANS_NECROTIC_AURA,100,10)"
data "Description" "hYOUR_HANDLE_HERE;1"
data "ExtraDescription" "hYOUR_HANDLE_HERE;1"
data "ExtraDescriptionParams" "DealDamage(3d8,Necrotic)"
data "TooltipDamageList" "DealDamage(3d8,Necrotic)"
data "TooltipStatusApply" "ApplyStatus(SPIRIT_GUARDIANS_NECROTIC_AURA,100,10)"
data "UseCosts" "ActionPoint:1"
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsConcentration;IsSpell;IsHarmful"
data "DamageType" "Necrotic"
```

**Key variant properties:**
- `using "ClassSpell"` - Inherit base behavior from class spell
- `SpellContainerID` - Points back to container spell
- `ContainerSpells` ""` - Clear to prevent nested containers

#### Step 3: Add Upcast Variants (Optional)

```
new entry "MyMod_Shout_SpiritGuardians_Necrotic_4"
type "SpellData"
data "SpellType" "Shout"
using "Shout_SpiritGuardians_Necrotic"     <-- Inherit from class upcast version
data "Level" "4"
data "SpellContainerID" "MyMod_Shout_SpiritGuardians"
data "Cooldown" "OncePerShortRest"
data "SpellProperties" "ApplyStatus(SPIRIT_GUARDIANS_NECROTIC_AURA_4,100,10)"
data "ExtraDescriptionParams" "DealDamage(4d8,Necrotic)"
data "TooltipDamageList" "DealDamage(4d8,Necrotic)"
data "UseCosts" "ActionPoint:1"
```

---

## UnlockSpell Syntax

### Simple Syntax (Our Current Approach)
```
data "Boosts" "UnlockSpell(SpellName)"
```

### Extended Syntax (For Complex Spells)
```
data "Boosts" "UnlockSpell(SpellName,AddChildren,,Cooldown,SpellCastingAbility)"
```

**Parameters:**
| Position | Parameter | Description |
|----------|-----------|-------------|
| 1 | SpellName | The spell to unlock |
| 2 | AddChildren | Adds container child spells |
| 3 | (empty) | Reserved |
| 4 | Cooldown | Override cooldown (e.g., `OncePerCombat`) |
| 5 | SpellCastingAbility | Use character's spellcasting ability |

**Example from BapeerySpiritShoes:**
```
data "Boosts" "UnlockSpell(Shout_SpiritGuardiansBoots,AddChildren,,OncePerCombat,SpellCastingAbility);"
```

---

## Properties Reference

### Required for Container Spells

| Property | Purpose | Example |
|----------|---------|---------|
| `ContainerSpells` | List of variant spells | `"Spell_A;Spell_B;Spell_C"` |
| `IsLinkedSpellContainer` | Flag in SpellFlags | Include in SpellFlags string |
| `Icon` | Spell icon | `"Spell_Conjuration_SpiritGuardians"` |
| `DisplayName` | Localization handle | `"hXXXXXXXX;1"` |
| `Description` | Localization handle | `"hXXXXXXXX;1"` |

### Required for Variant Spells

| Property | Purpose | Example |
|----------|---------|---------|
| `using` | Inherit from class spell | `using "Shout_SpiritGuardians"` |
| `SpellContainerID` | Link to container | `"MyMod_Shout_SpiritGuardians"` |
| `ContainerSpells` | Clear inherited | `""` |

### Optional Enhancement Properties

| Property | Purpose | Example |
|----------|---------|---------|
| `PrepareSound` | Sound when preparing | `"Spell_Prepare_..."` |
| `CastSound` | Sound when casting | `"Spell_Cast_..."` |
| `PrepareEffect` | Visual effect UUID | `"2534712b-d31e-..."` |
| `CastEffect` | Visual effect UUID | `"56ea5092-8ecd-..."` |
| `SpellAnimation` | Animation data | Complex UUID string |

---

## Finding Class Spell Names

To find the class spell to inherit from:

1. **Search unpacked game files** for the spell name
2. **Common patterns:**
   - `Shout_SpellName` - Self-cast spells
   - `Target_SpellName` - Targeted spells
   - `Projectile_SpellName` - Projectile spells
   - `Zone_SpellName` - Area effect spells

3. **Check spell type** - Must match the SpellType in your definition

---

## Complete Example: Spirit Guardians Boots

### Armor.txt
```
new entry "UNI_SpirtStep"
type "Armor"
using "_Vanity_Shoes_Generic_Rich"
data "RootTemplate" "00b38ee6-7f2d-4eca-a27d-738e0657b8e7"
data "Rarity" "VeryRare"
data "Boosts" "UnlockSpell(Shout_SpiritGuardiansBoots,AddChildren,,OncePerCombat,SpellCastingAbility);"
data "Unique" "1"
```

### Spell_Shout.txt (Container)
```
new entry "Shout_SpiritGuardiansBoots"
type "SpellData"
data "SpellType" "Shout"
data "Level" "3"
data "ContainerSpells" "Shout_SpiritGuardiansBoots_Necrotic;Shout_SpiritGuardiansBoots_Radiant"
data "SpellFlags" "...IsLinkedSpellContainer"
... (full property definitions)
```

### Spell_Shout.txt (Variant)
```
new entry "Shout_SpiritGuardiansBoots_Necrotic"
type "SpellData"
data "SpellType" "Shout"
using "Shout_SpiritGuardians"
data "SpellContainerID" "Shout_SpiritGuardiansBoots"
data "ContainerSpells" ""
data "Cooldown" "OncePerCombat"
... (variant-specific properties)
```

---

## When to Use Each Approach

| Scenario | Approach |
|----------|----------|
| Spell has no variants | Simple single spell with `using` |
| Spell has damage type choices | Container with variant spells |
| Spell has upcast versions | Add level-specific variants to container |
| Spell needs custom visuals/sounds | Define all properties manually |

---

## Reference: BapeerySpiritShoes Mod Location

```
BapeerySpiritShoes_428af67a-6681-3cd6-8203-18fff09c3282/
├── Mods/.../Localization/English/english.xml
├── Public/.../Stats/Generated/Data/Armor.txt
├── Public/.../Stats/Generated/Data/Spell_Shout.txt
└── Public/.../RootTemplates/00b38ee6-7f2d-4eca-a27d-738e0657b8e7.lsf.lsx
```

---

## Summary

1. **Simple spells**: Use `using "ClassSpell"` and override properties
2. **Complex spells**: Create container + variants
3. **Extended UnlockSpell**: Use `AddChildren` and other parameters for containers
4. **Always test**: Spell behavior may differ between class and item versions
