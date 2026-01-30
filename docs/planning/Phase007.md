# Phase 007 - Boots of Stormwalker & Ring of Spectral Power Enhancement

**Status:** COMPLETE

## Goal
1. Create the **Boots of Stormwalker** combining powers from Boots of Stormy Clamour and Disintegrating Night Walkers
2. Add **Force Amplification** from Forceweaver Gauntlets to the Ring of Spectral Power

---

## Part 1: Boots of Stormwalker

### Overview

The Boots of Stormwalker combine two vanilla boots:
- **Boots of Stormy Clamour** (`MAG_Thunder_ReverberationOnStatusApply_Boots`) - Apply Reverberation when inflicting conditions
- **Disintegrating Night Walkers** (`FOR_NightWalkers`) - Misty Step and immunity to difficult terrain effects

### Design Decisions

| Aspect | Decision |
|--------|----------|
| Name | Boots of Stormwalker |
| Internal ID | SMR_Boots_Stormwalker |
| Base Item | `_Foot_Magic` |
| Rarity | Legendary |

### Powers

| Status | Power | Description | Source |
|--------|-------|-------------|--------|
| [ ] | **Stormy Clamour** | When inflicting a condition on enemy, apply 2 stacks of Reverberation | Boots of Stormy Clamour |
| [ ] | **Misty Step** | Cast Misty Step (with unique visual) | Disintegrating Night Walkers |
| [ ] | **Sure-Footed** | Immunity to web, ensnared, prone from grease/ice | Disintegrating Night Walkers |

---

### Reference: Source Items

#### Boots of Stormy Clamour (MAG_Thunder_ReverberationOnStatusApply_Boots)
```
new entry "MAG_Thunder_ReverberationOnStatusApply_Boots"
type "Armor"
using "_Foot_Magic"
data "RootTemplate" "3908725d-29d1-4c9a-be46-4e03c8c65238"
data "Rarity" "Uncommon"
data "PassivesOnEquip" "MAG_Thunder_ReverberationOnStatusApply_Boots_Passive"
data "Unique" "1"
```

**MAG_Thunder_ReverberationOnStatusApply_Boots_Passive** (Stormy Clamour):
```
new entry "MAG_Thunder_ReverberationOnStatusApply_Boots_Passive"
type "PassiveData"
data "DisplayName" "hdb19f00ag6138g4bc6gb174g1dff84d45a57;2"
data "Description" "hdec25ee2gb8b0g4e21ga3f4g181253f20364;4"
data "DescriptionParams" "2"
data "Properties" "OncePerAttack"
data "StatsFunctorContext" "OnStatusApply"
data "Conditions" "Enemy() and not Self() and not StatusId('MAG_THUNDER_REVERBERATION') and not StatusDoesNotInvokeOnStatusApply()"
data "StatsFunctors" "ApplyStatus(MAG_THUNDER_REVERBERATION, 100, 2);ApplyStatus(MAG_THUNDER_REVERBERATION_DURATION_TECHNICAL, 100, 1)"
```
- When you inflict a condition on an enemy, apply 2 stacks of Reverberation
- Once per attack

#### Disintegrating Night Walkers (FOR_NightWalkers)
```
new entry "FOR_NightWalkers"
type "Armor"
using "_Foot_Magic"
data "RootTemplate" "ac9145d1-31d0-4aa3-8755-62cc85dad22b"
data "Rarity" "VeryRare"
data "Boosts" "UnlockSpell(Target_UNI_MistyStep_NightWalkers)"
data "PassivesOnEquip" "FOR_NightWalkers_WebImmunity"
data "Unique" "1"
```

**FOR_NightWalkers_WebImmunity** (Sure-Footed):
```
new entry "FOR_NightWalkers_WebImmunity"
type "PassiveData"
data "DisplayName" "hf0cf1a49g0ff9g4dafg917dg6e4de4794c10;2"
data "Description" "h82ca5839gf1a5g4a10g8781g70fa32685532;5"
data "Boosts" "StatusImmunity(WEB);StatusImmunity(ENSNARED);StatusImmunity(PRONE_GREASE);StatusImmunity(PRONE_ICE);StatusImmunity(ENSNARED_VINES);StatusImmunity(ENSNARING_STRIKE);StatusImmunity(ENSNARING_STRIKE_2)"
```
- Immunity to Web, Ensnared, Prone from Grease/Ice, Ensnaring Strike

---

### UUIDs and Handles Needed (Boots)

| Item | Type | Value |
|------|------|-------|
| Boots MapKey | UUID | `e1f2a3b4-c5d6-4e7f-8a9b-0c1d2e3f4a5b` |
| OneTimeReward | UUID | `f2a3b4c5-d6e7-4f8a-9b0c-1d2e3f4a5b6c` |
| Boots DisplayName | Handle | `h1a2b3c4dge5f6g7a8bg9c0dge1f2a3b4c5d6` |
| Boots Description | Handle | `h2b3c4d5egf6a7g8b9cgd0e1gf2a3b4c5d6e7` |

---

### Files to Create/Modify (Boots)

#### 1. NEW FILE: Stats/Generated/Data/Boots.txt

Create file with Boots of Stormwalker:
```
new entry "SMR_Boots_Stormwalker"
type "Armor"
using "_Foot_Magic"
data "RootTemplate" "e1f2a3b4-c5d6-4e7f-8a9b-0c1d2e3f4a5b"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(Target_UNI_MistyStep_NightWalkers)"
data "PassivesOnEquip" "MAG_Thunder_ReverberationOnStatusApply_Boots_Passive;FOR_NightWalkers_WebImmunity"
data "Unique" "1"
```

**Boosts breakdown:**
- `UnlockSpell(Target_UNI_MistyStep_NightWalkers)` - Misty Step with Night Walkers visual (from Night Walkers)

**PassivesOnEquip breakdown:**
- `MAG_Thunder_ReverberationOnStatusApply_Boots_Passive` - Stormy Clamour: Apply 2 Reverberation on condition inflict
- `FOR_NightWalkers_WebImmunity` - Sure-Footed: Immunity to terrain effects

#### 2. RootTemplates/merged.lsx AND merged.lsf.lsx

Add GameObjects node for Boots:
```xml
<node id="GameObjects">
    <attribute id="Description" type="TranslatedString" handle="h2b3c4d5egf6a7g8b9cgd0e1gf2a3b4c5d6e7" version="1" />
    <attribute id="DisplayName" type="TranslatedString" handle="h1a2b3c4dge5f6g7a8bg9c0dge1f2a3b4c5d6" version="1" />
    <attribute id="LevelName" type="FixedString" value="" />
    <attribute id="MapKey" type="FixedString" value="e1f2a3b4-c5d6-4e7f-8a9b-0c1d2e3f4a5b" />
    <attribute id="Name" type="LSString" value="SMR_Boots_Stormwalker" />
    <attribute id="ParentTemplateId" type="FixedString" value="ac9145d1-31d0-4aa3-8755-62cc85dad22b" />
    <attribute id="Stats" type="FixedString" value="SMR_Boots_Stormwalker" />
    <attribute id="Type" type="FixedString" value="item" />
    <attribute id="_OriginalFileVersion_" type="int64" value="144115188075855912" />
    <children>
        <node id="GameMaster" />
    </children>
</node>
```

Note: Using Night Walkers as ParentTemplateId for visual appearance.

#### 3. Localization/English/SampleMagicRingMod.xml AND .loca.xml

Add localization entries:
```xml
<content contentuid="h1a2b3c4dge5f6g7a8bg9c0dge1f2a3b4c5d6" version="1">Boots of Stormwalker</content>
<content contentuid="h2b3c4d5egf6a7g8b9cgd0e1gf2a3b4c5d6e7" version="1">Legendary boots that combine the power of storms with shadowstep magic. Grants Misty Step, applies Reverberation when inflicting conditions, and provides immunity to web and terrain effects.</content>
```

#### 4. OneTimeRewards/OneTimeRewards.lsx

Add OneTimeReward entry:
```xml
<node id="OneTimeReward">
    <attribute id="Amount" type="uint32" value="1"/>
    <attribute id="ItemTemplateId" type="FixedString" value="e1f2a3b4-c5d6-4e7f-8a9b-0c1d2e3f4a5b"/>
    <attribute id="UUID" type="guid" value="f2a3b4c5-d6e7-4f8a-9b0c-1d2e3f4a5b6c"/>
</node>
```

---

## Part 2: Ring of Spectral Power Enhancement

### Overview

Add **Force Amplification** from the WW mod's Forceweaver Gauntlets to the Ring of Spectral Power.

**Note:** WW_Wizard_Equipment mod must be installed as a dependency.

### New Power

| Status | Power | Description | Source |
|--------|-------|-------------|--------|
| [ ] | **Force Amplification** | Spells deal an additional 1d4 Force damage | Forceweaver Gauntlets (WW mod) |

---

### Reference: Forceweaver Gauntlets (WW_Wizard_Equipment mod)

```
new entry "WW_Wizard_Equipment_Forceweavers_Gauntlets"
type "Armor"
using "_Hand_Magic"
data "RootTemplate" "14f5b5a4-4d8c-47c2-afc8-837fbc253f87"
data "Rarity" "Uncommon"
data "PassivesOnEquip" "WW_Forceweaver_Passive"
data "Unique" "1"
```

**WW_Forceweaver_Passive** (Force Amplification):
```
new entry "WW_Forceweaver_Passive"
type "PassiveData"
data "DisplayName" "h941a2a1agcc5ag4161gb947g4797cc56ab38;1"
data "Description" "h941a2a1agcc5ag4161gb947g4797cc56ab39;1"
data "DescriptionParams" "DealDamage(1d4,Force)"
data "Boosts" "IF(IsSpell()):DamageBonus(1d4,Force)"
```
- Spells deal an additional 1d4 Force damage

---

### Current Ring of Spectral Power

```
new entry "SMR_Ring_Spectral_Power"
type "Armor"
using "_Ring"
data "RootTemplate" "d4e5f6a7-b8c9-4d0e-a1b2-c3d4e5f6a7b8"
data "ObjectCategory" "Jewelry"
data "ValueOverride" "750"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(SMR_Projectile_MagicMissile_Unlimited_Lvl3);UnlockSpell(SMR_Target_GlobeOfInvulnerability_ShortRest);UnlockSpell(SMR_Target_MistyStep_Unlimited);UnlockInterrupt(SMR_Interrupt_Shield_Unlimited);UnlockInterrupt(SMR_Interrupt_Counterspell_Unlimited);UnlockSpell(SMR_Target_HoldPerson_Unlimited);UnlockSpell(SMR_Projectile_ArtistryOfWar_ShortRest);UnlockSpell(SMR_Target_Invisibility_ShortRest);UnlockSpell(SMR_Target_Knock_Unlimited);UnlockSpell(SMR_Teleportation_ArcaneGate_ShortRest)"
```

---

### Files to Modify (Ring)

#### 1. Stats/Generated/Data/Armor.txt

Update SMR_Ring_Spectral_Power to add PassivesOnEquip:

**Before:**
```
new entry "SMR_Ring_Spectral_Power"
type "Armor"
using "_Ring"
data "RootTemplate" "d4e5f6a7-b8c9-4d0e-a1b2-c3d4e5f6a7b8"
data "ObjectCategory" "Jewelry"
data "ValueOverride" "750"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(SMR_Projectile_MagicMissile_Unlimited_Lvl3);UnlockSpell(SMR_Target_GlobeOfInvulnerability_ShortRest);UnlockSpell(SMR_Target_MistyStep_Unlimited);UnlockInterrupt(SMR_Interrupt_Shield_Unlimited);UnlockInterrupt(SMR_Interrupt_Counterspell_Unlimited);UnlockSpell(SMR_Target_HoldPerson_Unlimited);UnlockSpell(SMR_Projectile_ArtistryOfWar_ShortRest);UnlockSpell(SMR_Target_Invisibility_ShortRest);UnlockSpell(SMR_Target_Knock_Unlimited);UnlockSpell(SMR_Teleportation_ArcaneGate_ShortRest)"
```

**After:**
```
new entry "SMR_Ring_Spectral_Power"
type "Armor"
using "_Ring"
data "RootTemplate" "d4e5f6a7-b8c9-4d0e-a1b2-c3d4e5f6a7b8"
data "ObjectCategory" "Jewelry"
data "ValueOverride" "750"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(SMR_Projectile_MagicMissile_Unlimited_Lvl3);UnlockSpell(SMR_Target_GlobeOfInvulnerability_ShortRest);UnlockSpell(SMR_Target_MistyStep_Unlimited);UnlockInterrupt(SMR_Interrupt_Shield_Unlimited);UnlockInterrupt(SMR_Interrupt_Counterspell_Unlimited);UnlockSpell(SMR_Target_HoldPerson_Unlimited);UnlockSpell(SMR_Projectile_ArtistryOfWar_ShortRest);UnlockSpell(SMR_Target_Invisibility_ShortRest);UnlockSpell(SMR_Target_Knock_Unlimited);UnlockSpell(SMR_Teleportation_ArcaneGate_ShortRest)"
data "PassivesOnEquip" "WW_Forceweaver_Passive"
```

#### 2. Update Ring Description in Localization

Update description to mention Force Amplification (optional - depends on existing localization).

---

---

## Part 3: Magus Circlet

### Overview

Create a **Magus Circlet** with the appearance of the Warped Headband of Intellect, granting the Dauntless power from the Cloth of Authority. Additional powers will be added later.

### Design Decisions

| Aspect | Decision |
|--------|----------|
| Name | Magus Circlet |
| Internal ID | SMR_Circlet_Magus |
| Base Item | `_Head_Magic_Circlet` |
| Appearance | Warped Headband of Intellect |
| VisualTemplate | `21f8ec11-2ecf-73e8-123b-a5da10ebd800` |
| ParentTemplateId | `8779b30f-dc6f-4264-b7af-9dc0eff51bb0` (Headband of Intellect) |
| Rarity | Legendary |

### Powers

| Status | Power | Description | Source |
|--------|-------|-------------|--------|
| [ ] | **Dauntless** | Immunity to Frightened condition | Cloth of Authority |
| [ ] | **Speak with Dead** | Cast Speak with Dead (once per short rest) | Amulet of Lost Voices (WW mod) |
| [ ] | **Speak with Animals** | Cast Speak with Animals (once per short rest) | Amulet of Lost Voices (WW mod) |

---

### Reference: Source Items

#### Warped Headband of Intellect (ARM_HeadbandOfIntellect)
```
new entry "ARM_HeadbandOfIntellect"
type "Armor"
using "_Head_Magic_Circlet"
data "RootTemplate" "8779b30f-dc6f-4264-b7af-9dc0eff51bb0"
data "Rarity" "Rare"
data "Boosts" "AbilityOverrideMinimum(Intelligence,19)"
```
- Used for appearance only

#### Cloth of Authority (MAG_Gortash_Cloth)
```
new entry "MAG_Gortash_Cloth"
type "Armor"
using "ARM_Cloth_Body_1"
data "RootTemplate" "8b868b78-320b-43d0-b5a8-5e52669fc11e"
data "Rarity" "Rare"
data "PassivesOnEquip" "MAG_LC_Cyric_FearImmunity_Amulet_Passive;MAG_ArmorOfAuthority_Passive"
data "Unique" "1"
```

**MAG_LC_Cyric_FearImmunity_Amulet_Passive** (Dauntless):
- Immunity to Frightened condition
- This is the "Dauntless" passive from the Cloth of Authority

#### Amulet of Lost Voices (WW_Wizard_Equipment mod)
```
new entry "WW_Wizard_Equipment_Amulet_of_Lost_Voices"
type "Armor"
using "_Amulet_Magic"
data "RootTemplate" "4630871d-95ea-4d29-8421-fcb4fe2e024a"
data "Rarity" "Uncommon"
data "Boosts" "UnlockSpell(WW_Target_SpeakWithDead);UnlockSpell(WW_Shout_SpeakWithAnimals)"
data "Unique" "1"
```

**WW_Target_SpeakWithDead**:
```
new entry "WW_Target_SpeakWithDead"
type "SpellData"
data "SpellType" "Target"
using "Target_SpeakWithDead"
data "Cooldown" "OncePerRestPerItem"
data "UseCosts" "ActionPoint:1"
```
- Speak with Dead, once per short rest

**WW_Shout_SpeakWithAnimals**:
```
new entry "WW_Shout_SpeakWithAnimals"
type "SpellData"
data "SpellType" "Shout"
using "Shout_SpeakWithAnimals"
data "Cooldown" "OncePerRestPerItem"
data "UseCosts" "ActionPoint:1"
```
- Speak with Animals, once per short rest

---

### UUIDs and Handles Needed (Circlet)

| Item | Type | Value |
|------|------|-------|
| Circlet MapKey | UUID | `a2b3c4d5-e6f7-4a8b-9c0d-1e2f3a4b5c6d` |
| OneTimeReward | UUID | `b3c4d5e6-f7a8-4b9c-0d1e-2f3a4b5c6d7e` |
| Circlet DisplayName | Handle | `h3c4d5e6fga7b8g9c0dgd1e2gf3a4b5c6d7e8` |
| Circlet Description | Handle | `h4d5e6f7agb8c9gd0e1ge2f3ga4b5c6d7e8f9` |

---

### Files to Create/Modify (Circlet)

#### 1. Stats/Generated/Data/Armor.txt

Add Magus Circlet entry:
```
new entry "SMR_Circlet_Magus"
type "Armor"
using "_Head_Magic_Circlet"
data "RootTemplate" "a2b3c4d5-e6f7-4a8b-9c0d-1e2f3a4b5c6d"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(WW_Target_SpeakWithDead);UnlockSpell(WW_Shout_SpeakWithAnimals)"
data "PassivesOnEquip" "MAG_LC_Cyric_FearImmunity_Amulet_Passive"
data "Unique" "1"
```

**Boosts breakdown:**
- `UnlockSpell(WW_Target_SpeakWithDead)` - Speak with Dead (once per short rest, from WW mod)
- `UnlockSpell(WW_Shout_SpeakWithAnimals)` - Speak with Animals (once per short rest, from WW mod)

**PassivesOnEquip breakdown:**
- `MAG_LC_Cyric_FearImmunity_Amulet_Passive` - Dauntless: Immunity to Frightened (from Cloth of Authority)

#### 2. RootTemplates/merged.lsx AND merged.lsf.lsx

Add GameObjects node for Circlet (using Headband of Intellect appearance):
```xml
<node id="GameObjects">
    <attribute id="Description" type="TranslatedString" handle="h4d5e6f7agb8c9gd0e1ge2f3ga4b5c6d7e8f9" version="1" />
    <attribute id="DisplayName" type="TranslatedString" handle="h3c4d5e6fga7b8g9c0dgd1e2gf3a4b5c6d7e8" version="1" />
    <attribute id="Icon" type="FixedString" value="Item_ARM_HeadbandOfIntellect" />
    <attribute id="LevelName" type="FixedString" value="" />
    <attribute id="MapKey" type="FixedString" value="a2b3c4d5-e6f7-4a8b-9c0d-1e2f3a4b5c6d" />
    <attribute id="Name" type="LSString" value="SMR_Circlet_Magus" />
    <attribute id="ParentTemplateId" type="FixedString" value="8779b30f-dc6f-4264-b7af-9dc0eff51bb0" />
    <attribute id="Stats" type="FixedString" value="SMR_Circlet_Magus" />
    <attribute id="Type" type="FixedString" value="item" />
    <attribute id="VisualTemplate" type="FixedString" value="21f8ec11-2ecf-73e8-123b-a5da10ebd800" />
    <attribute id="_OriginalFileVersion_" type="int64" value="144115188075855912" />
    <children>
        <node id="GameMaster" />
    </children>
</node>
```

#### 3. Localization/English/SampleMagicRingMod.xml AND .loca.xml

Add localization entries:
```xml
<content contentuid="h3c4d5e6fga7b8g9c0dgd1e2gf3a4b5c6d7e8" version="1">Magus Circlet</content>
<content contentuid="h4d5e6f7agb8c9gd0e1ge2f3ga4b5c6d7e8f9" version="1">A circlet worn by archmages of old. Grants Dauntless (immunity to Frightened), Speak with Dead, and Speak with Animals.</content>
```

#### 4. OneTimeRewards/OneTimeRewards.lsx

Add OneTimeReward entry:
```xml
<node id="OneTimeReward">
    <attribute id="Amount" type="uint32" value="1"/>
    <attribute id="ItemTemplateId" type="FixedString" value="a2b3c4d5-e6f7-4a8b-9c0d-1e2f3a4b5c6d"/>
    <attribute id="UUID" type="guid" value="b3c4d5e6-f7a8-4b9c-0d1e-2f3a4b5c6d7e"/>
</node>
```

---

## Part 4: Ring of the Guardian Enhancement

### Overview

Add **Remove Curse** spell to the Ring of the Guardian, once per long rest.

### New Power

| Status | Power | Description | Source |
|--------|-------|-------------|--------|
| [ ] | **Remove Curse** | Cast Remove Curse (once per long rest) | Vanilla spell |

---

### Reference: Remove Curse Spell

```
new entry "Target_RemoveCurse"
type "SpellData"
data "SpellType" "Target"
data "Level" "3"
data "SpellSchool" "Abjuration"
data "SpellProperties" "RemoveStatus(SG_Cursed)"
data "TargetConditions" "HasStatus('SG_Cursed')"
data "Icon" "Spell_Abjuration_RemoveCurse"
data "DisplayName" "h140012f8gf686g452eg8414gb9ec01cce5ea;1"
data "Description" "h57351d43g66cbg4980gae65g24cc18188edf;6"
data "UseCosts" "ActionPoint:1;SpellSlotsGroup:1:1:3"
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsSpell;IsMelee"
```
- Removes cursed status from target
- Level 3 Abjuration spell

---

### Current Ring of the Guardian

```
new entry "SMR_Ring_Guardian"
type "Armor"
using "_Ring"
data "RootTemplate" "a1b2c3d4-e5f6-4a7b-8c9d-0e1f2a3b4c5d"
data "ObjectCategory" "Jewelry"
data "ValueOverride" "750"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(SMR_Target_HealingWord_Superior);UnlockSpell(SMR_Target_Bless_Unlimited);UnlockSpell(SMR_Target_CreateWater_Unlimited);UnlockSpell(SMR_Target_LesserRestoration_ShortRest);UnlockSpell(SMR_Target_GreaterRestoration_LongRest);UnlockSpell(SMR_Target_FreedomOfMovement_ShortRest);UnlockInterrupt(SMR_Interrupt_Counterspell_ShortRest);UnlockSpell(SMR_Shout_HeroesFeast_LongRest)"
```

---

### Files to Create/Modify (Ring of the Guardian)

#### 1. Stats/Generated/Data/Spell_Target.txt

Add Remove Curse spell with long rest cooldown:
```
new entry "SMR_Target_RemoveCurse_LongRest"
type "SpellData"
data "SpellType" "Target"
using "Target_RemoveCurse"
data "UseCosts" "ActionPoint:1"
data "Cooldown" "OncePerLongRest"
```

#### 2. Stats/Generated/Data/Armor.txt

Update SMR_Ring_Guardian to add Remove Curse:

**Before:**
```
data "Boosts" "UnlockSpell(SMR_Target_HealingWord_Superior);UnlockSpell(SMR_Target_Bless_Unlimited);UnlockSpell(SMR_Target_CreateWater_Unlimited);UnlockSpell(SMR_Target_LesserRestoration_ShortRest);UnlockSpell(SMR_Target_GreaterRestoration_LongRest);UnlockSpell(SMR_Target_FreedomOfMovement_ShortRest);UnlockInterrupt(SMR_Interrupt_Counterspell_ShortRest);UnlockSpell(SMR_Shout_HeroesFeast_LongRest)"
```

**After:**
```
data "Boosts" "UnlockSpell(SMR_Target_HealingWord_Superior);UnlockSpell(SMR_Target_Bless_Unlimited);UnlockSpell(SMR_Target_CreateWater_Unlimited);UnlockSpell(SMR_Target_LesserRestoration_ShortRest);UnlockSpell(SMR_Target_GreaterRestoration_LongRest);UnlockSpell(SMR_Target_FreedomOfMovement_ShortRest);UnlockInterrupt(SMR_Interrupt_Counterspell_ShortRest);UnlockSpell(SMR_Shout_HeroesFeast_LongRest);UnlockSpell(SMR_Target_RemoveCurse_LongRest)"
```

---

## Implementation Order

### Boots of Stormwalker
1. [x] Create Boots.txt with SMR_Boots_Stormwalker entry (added to Armor.txt)
2. [x] Add boots to merged.lsx
3. [x] Add boots to merged.lsf.lsx
4. [x] Add localization to SampleMagicRingMod.xml
5. [x] Add localization to SampleMagicRingMod.loca.xml
6. [x] Add to OneTimeRewards.lsx

### Ring of Spectral Power Enhancement
7. [x] Update SMR_Ring_Spectral_Power in Armor.txt to add PassivesOnEquip
8. [ ] (Optional) Update ring description in localization

### Magus Circlet
9. [x] Add SMR_Circlet_Magus to Armor.txt
10. [x] Add circlet to merged.lsx
11. [x] Add circlet to merged.lsf.lsx
12. [x] Add localization to SampleMagicRingMod.xml
13. [x] Add localization to SampleMagicRingMod.loca.xml
14. [x] Add to OneTimeRewards.lsx

### Ring of the Guardian Enhancement
15. [x] Add SMR_Target_RemoveCurse_LongRest to Spell_Target.txt
16. [x] Update SMR_Ring_Guardian in Armor.txt to add Remove Curse

### Final
17. [ ] Build and test mod

---

## Test Plan

**Prerequisites:** WW_Wizard_Equipment mod must be installed

### Boots of Stormwalker
- [ ] Build mod with BG3 Modder's Multitool
- [ ] Load game with mod enabled (ensure WW_Wizard_Equipment is also enabled)
- [ ] Go to camp and check Traveler's Chest for Boots of Stormwalker
- [ ] Equip Boots of Stormwalker
- [ ] Verify boots appear with correct appearance (Night Walkers visual)
- [ ] Verify boots description displays correctly

#### Powers Test
- [ ] Verify Misty Step spell is available and works
- [ ] Verify Stormy Clamour: inflict a condition (e.g., Prone, Frightened) and check for Reverberation stacks
- [ ] Verify Sure-Footed: walk through web/grease without being affected

### Ring of Spectral Power Enhancement
- [ ] Equip Ring of Spectral Power
- [ ] Verify "Force Amplification" passive is active in character sheet
- [ ] Cast a spell and verify +1d4 Force damage is added

### Magus Circlet
- [ ] Go to camp and check Traveler's Chest for Magus Circlet
- [ ] Equip Magus Circlet
- [ ] Verify circlet appears with correct appearance (Headband of Intellect visual)
- [ ] Verify circlet description displays correctly
- [ ] Verify "Dauntless" passive is active (Immunity to Frightened)
- [ ] Verify Speak with Dead spell is available and works (once per short rest)
- [ ] Verify Speak with Animals spell is available and works (once per short rest)

### Ring of the Guardian Enhancement
- [ ] Equip Ring of the Guardian
- [ ] Verify Remove Curse spell is available
- [ ] Cast Remove Curse on a cursed target (if available) and verify it works
- [ ] Verify Remove Curse has long rest cooldown

---

## Notes

- Boots use vanilla passives that require no WW mod dependency:
  - `MAG_Thunder_ReverberationOnStatusApply_Boots_Passive` (Boots of Stormy Clamour)
  - `FOR_NightWalkers_WebImmunity` (Night Walkers)
- Boots use vanilla spell from Night Walkers:
  - `Target_UNI_MistyStep_NightWalkers` (Misty Step with unique visual)
- Circlet uses vanilla passive from Cloth of Authority:
  - `MAG_LC_Cyric_FearImmunity_Amulet_Passive` (Dauntless - Fear Immunity)
- Circlet uses WW mod spells from Amulet of Lost Voices:
  - `WW_Target_SpeakWithDead` (Speak with Dead)
  - `WW_Shout_SpeakWithAnimals` (Speak with Animals)
- Ring of Spectral Power enhancement uses WW mod passive:
  - `WW_Forceweaver_Passive` (Force Amplification)
  - **Assumption:** WW_Wizard_Equipment mod is installed as a dependency
- Ring of the Guardian enhancement uses vanilla spell:
  - `Target_RemoveCurse` (Remove Curse)
- Boots and Circlet can be added to existing Armor.txt instead of creating separate files

---

## Updated Ring of Spectral Power Powers (After Phase 7)

| Status | Power | Description | Phase |
|--------|-------|-------------|-------|
| [x] | **Unlimited Level 3 Magic Missile** | 5 missiles at will (bonus action) | Phase 1 |
| [x] | **Globe of Invulnerability** | Once per short rest | Phase 2 |
| [x] | **Unlimited Misty Step** | Teleport at will (no spell slot cost) | Phase 3 |
| [x] | **Unlimited Shield** | Cast Shield as a reaction (unlimited) | Phase 5 |
| [x] | **Unlimited Counterspell** | Cast Counterspell as a reaction (unlimited) | Phase 5 |
| [x] | **Unlimited Hold Person** | Cast Hold Person as a bonus action (unlimited) | Phase 5 |
| [x] | **Artistry of War** | Cast Artistry of War as an action (once per short rest) | Phase 5 |
| [x] | **Invisibility** | Cast Invisibility (once per short rest) | Phase 5 |
| [x] | **Unlimited Knock** | Cast Knock as a bonus action (unlimited) | Phase 5 |
| [x] | **Arcane Gate** | Cast Arcane Gate (once per short rest) | Phase 5 |
| [ ] | **Force Amplification** | Spells deal +1d4 Force damage | Phase 7 |
