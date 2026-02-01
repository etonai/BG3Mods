# Phase 013 - Tyr's Arsenal Enhancements

**Status:** COMPLETE

## Goal
Enhance the Tyr items from Phase 12 with more powerful stats:
- Upgrade Mantle of Tyr ability scores (STR 29, CON 23, DEX 23)
- Add new Armor of Tyr (based on Armor of Agility)

**Note:** Sword of Tyr enhancements moved to Phase 14.

---

## Item 1: Mantle of Tyr - Enhanced Ability Scores

### Overview
Upgrade the Mantle of Tyr to grant even higher ability scores, making it a truly divine artifact.

### Current Implementation

```
new entry "SMR_Cloak_Tyr"
type "Armor"
using "ARM_Cloak_Long_C"
data "RootTemplate" "b1c2d3e4-f5a6-4b7c-8d9e-0f1a2b3c4d5e"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(SMR_Shout_CrusadersMantle_Unlimited);AbilityOverrideMinimum(Strength,24);AbilityOverrideMinimum(Constitution,21);AbilityOverrideMinimum(Dexterity,21)"
data "Unique" "1"
```

### Proposed Changes

| Ability | Current | New |
|---------|---------|-----|
| Strength | 24 | 29 |
| Constitution | 21 | 23 |
| Dexterity | 21 | 23 |

### New Implementation

```
new entry "SMR_Cloak_Tyr"
type "Armor"
using "ARM_Cloak_Long_C"
data "RootTemplate" "b1c2d3e4-f5a6-4b7c-8d9e-0f1a2b3c4d5e"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(SMR_Shout_CrusadersMantle_Unlimited);AbilityOverrideMinimum(Strength,29);AbilityOverrideMinimum(Constitution,23);AbilityOverrideMinimum(Dexterity,23)"
data "Unique" "1"
```

---

## Item 2: Armor of Tyr

### Overview
A new legendary armor based on the Armor of Agility (MAG_EndGame_HalfPlate). This half plate armor allows full Dexterity modifier to AC, grants +2 to saving throws, and can cast unlimited Celestial Haste (like the Staff of Akitaro).

### Research Results - Armor of Agility

```
new entry "MAG_EndGame_HalfPlate"
type "Armor"
using "ARM_HalfPlate_Body_2"
data "RootTemplate" "42e6357a-4c05-4eda-9415-6b6b4c7d44c5"
data "ValueUUID" "adfdafe5-f4da-4c64-a1e6-a33d626437d2"
data "Rarity" "VeryRare"
data "Boosts" "RollBonus(SavingThrow, 2)"
data "PassivesOnEquip" "MAG_ExoticMaterial_MediumArmor_Passive"
data "StatusOnEquip" "MAG_EXOTIC_MATERIAL_ARMOR_TECHNICAL"
data "Unique" "1"
data "Ability Modifier Cap" ""
```

**Key Features:**
- `ARM_HalfPlate_Body_2` - Base half plate (+2 enchanted)
- `RollBonus(SavingThrow, 2)` - +2 to all saving throws
- `MAG_ExoticMaterial_MediumArmor_Passive` - Removes Dexterity cap (normally +2 for half plate)
- `Ability Modifier Cap` set to empty - Allows full DEX bonus to AC

### Item Details

| Aspect | Value |
|--------|-------|
| Name | Armor of Tyr |
| Internal ID | SMR_Armor_Tyr |
| Base Item | Armor of Agility (MAG_EndGame_HalfPlate) |
| ParentTemplateId | 42e6357a-4c05-4eda-9415-6b6b4c7d44c5 |
| Rarity | Legendary |
| Unique | Yes |

### Powers

| Power | Description | Implementation |
|-------|-------------|----------------|
| **Saving Throw Bonus** | +2 to all saving throws | `RollBonus(SavingThrow, 2)` |
| **No Dex Cap** | Full Dexterity bonus to AC | `MAG_ExoticMaterial_MediumArmor_Passive` + empty `Ability Modifier Cap` |
| **Celestial Haste** | Cast Celestial Haste (bonus action, unlimited) | `UnlockSpell(SMR_Shout_CelestialHaste_Unlimited)` |

### UUIDs and Handles

| Item | Type | Value |
|------|------|-------|
| Armor MapKey | UUID | `c3d4e5f6-a7b8-4c9d-0e1f-2a3b4c5d6e7f` |
| OneTimeReward | UUID | `d4e5f6a7-b8c9-4d0e-1f2a-3b4c5d6e7f8a` |
| Armor DisplayName | Handle | `hc3d4e5f6ag7b8cg9d0eg1f2ag3b4c5d6e7f8` |
| Armor Description | Handle | `hd4e5f6a7bg8c9dg0e1fg2a3bg4c5d6e7f8a9` |

### Implementation

#### Armor.txt
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

#### RootTemplates (merged.lsx and merged.lsf.lsx)
```xml
<node id="GameObjects">
    <attribute id="Description" type="TranslatedString" handle="hd4e5f6a7bg8c9dg0e1fg2a3bg4c5d6e7f8a9" version="1" />
    <attribute id="DisplayName" type="TranslatedString" handle="hc3d4e5f6ag7b8cg9d0eg1f2ag3b4c5d6e7f8" version="1" />
    <attribute id="LevelName" type="FixedString" value="" />
    <attribute id="MapKey" type="FixedString" value="c3d4e5f6-a7b8-4c9d-0e1f-2a3b4c5d6e7f" />
    <attribute id="Name" type="LSString" value="SMR_Armor_Tyr" />
    <attribute id="ParentTemplateId" type="FixedString" value="42e6357a-4c05-4eda-9415-6b6b4c7d44c5" />
    <attribute id="Stats" type="FixedString" value="SMR_Armor_Tyr" />
    <attribute id="Type" type="FixedString" value="item" />
    <attribute id="_OriginalFileVersion_" type="int64" value="144115188075855912" />
    <children>
        <node id="GameMaster" />
    </children>
</node>
```

#### Localization
```xml
<content contentuid="hc3d4e5f6ag7b8cg9d0eg1f2ag3b4c5d6e7f8" version="1">Armor of Tyr</content>
<content contentuid="hd4e5f6a7bg8c9dg0e1fg2a3bg4c5d6e7f8a9" version="1">Half plate armor blessed by Tyr, the God of Justice. Grants +2 to all saving throws, allows full Dexterity bonus to AC, and can cast unlimited Celestial Haste.</content>
```

---

## Implementation Checklist

### Mantle of Tyr Enhancement
- [x] Update SMR_Cloak_Tyr in Armor.txt with new ability scores (STR 29, CON 23, DEX 23)

### Armor of Tyr
- [x] Add SMR_Armor_Tyr to Armor.txt
- [x] Add armor template to merged.lsx
- [x] Add armor template to merged.lsf.lsx
- [x] Add OneTimeReward entry
- [x] Add localization to SampleMagicRingMod.xml
- [x] Add localization to SampleMagicRingMod.loca.xml

### Final
- [x] Build and test mod

---

## Test Plan

### Mantle of Tyr Enhanced Stats
- [ ] Equip Mantle of Tyr
- [ ] Verify Strength is set to 29 (or unchanged if already higher)
- [ ] Verify Constitution is set to 23 (or unchanged if already higher)
- [ ] Verify Dexterity is set to 23 (or unchanged if already higher)
- [ ] Verify Crusader's Mantle spell still works

### Armor of Tyr
- [ ] Check traveler's chest for Armor of Tyr
- [ ] Equip armor and verify appearance matches Armor of Agility
- [ ] Verify +2 bonus to all saving throws
- [ ] Verify full Dexterity bonus applies to AC (no +2 cap)
- [ ] Test with high DEX character to confirm no cap
- [ ] Verify Celestial Haste spell is available (bonus action)
- [ ] Cast Celestial Haste and verify it works (grants extra action)
- [ ] Verify Celestial Haste can be cast again without resting (unlimited)

---

## Notes

*(To be added during implementation)*
