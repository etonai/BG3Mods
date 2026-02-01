# Phase 012 - Tyr's Arsenal

**Status:** COMPLETE

## Goal
Create Tyr-themed legendary items (Mantle, Sword, Shield) and enhance existing items.

---

## Item 1: Mantle of Tyr

### Overview
A legendary cloak based on the Mantle of the Holy Warrior, with the added power of granting divine strength (Strength set to 24).

### Item Details

| Aspect | Value |
|--------|-------|
| Name | Mantle of Tyr |
| Internal ID | SMR_Cloak_Tyr |
| Base Item | Mantle of the Holy Warrior (MAG_Radiant_CrusaderMantle_Cloak) |
| ParentTemplateId | f1fdb8db-e754-4ea9-b6ce-440db6b776ac |
| Rarity | Legendary |
| Unique | Yes |

### Powers

| Power | Description | Implementation |
|-------|-------------|----------------|
| **Crusader's Mantle** | Cast Crusader's Mantle (unlimited, no rest required) | `UnlockSpell(SMR_Shout_CrusadersMantle_Unlimited)` |
| **Divine Strength** | Sets Strength to 24 | `AbilityOverrideMinimum(Strength,24)` |
| **Divine Constitution** | Sets Constitution to 21 | `AbilityOverrideMinimum(Constitution,21)` |
| **Divine Dexterity** | Sets Dexterity to 21 | `AbilityOverrideMinimum(Dexterity,21)` |

### UUIDs and Handles Needed

| Item | Type | Value |
|------|------|-------|
| Cloak MapKey | UUID | `b1c2d3e4-f5a6-4b7c-8d9e-0f1a2b3c4d5e` |
| OneTimeReward | UUID | `c2d3e4f5-a6b7-4c8d-9e0f-1a2b3c4d5e6f` |
| Cloak DisplayName | Handle | `h1a2b3c4dg5e6fg7a8bg9c0dg1e2f3a4b5c6d7` |
| Cloak Description | Handle | `h2b3c4d5eg6f7ag8b9cg0d1eg2f3a4b5c6d7e8` |
| Spell DisplayName | Handle | `h3b4c5d6eg7f8ag9b0cg1d2eg3f4a5b6c7d8e9f0` |
| Spell ExtraDescription | Handle | `h4c5d6e7fg8a9bg0c1dg2e3fg4a5b6c7d8e9f0a1` |

---

## Research Results

### Mantle of the Holy Warrior (MAG_Radiant_CrusaderMantle_Cloak)

```
new entry "MAG_Radiant_CrusaderMantle_Cloak"
type "Armor"
using "ARM_Cloak_Long_C"
data "RootTemplate" "f1fdb8db-e754-4ea9-b6ce-440db6b776ac"
data "Rarity" "VeryRare"
data "Boosts" "UnlockSpell(Shout_MAG_CrusadersMantle)"
data "Unique" "1"
```

- ParentTemplateId: `a5f5a875-932b-44c4-8b45-88d2ed379787`
- Icon: `Generated_MAG_Radiant_CrusaderMantle_Cloak_Magic`

---

## Implementation Steps

### Step 1: Add Unlimited Crusader's Mantle Spell to Spell_Shout.txt

```
new entry "SMR_Shout_CrusadersMantle_Unlimited"
type "SpellData"
data "SpellType" "Shout"
using "Shout_MAG_CrusadersMantle"
data "DisplayName" "h3b4c5d6eg7f8ag9b0cg1d2eg3f4a5b6c7d8e9f0;1"
data "ExtraDescription" "h4c5d6e7fg8a9bg0c1dg2e3fg4a5b6c7d8e9f0a1;1"
data "UseCosts" "ActionPoint:1"
```

### Step 2: Add Cloak Stats to Armor.txt

```
new entry "SMR_Cloak_Tyr"
type "Armor"
using "ARM_Cloak_Long_C"
data "RootTemplate" "b1c2d3e4-f5a6-4b7c-8d9e-0f1a2b3c4d5e"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(SMR_Shout_CrusadersMantle_Unlimited);AbilityOverrideMinimum(Strength,24);AbilityOverrideMinimum(Constitution,21);AbilityOverrideMinimum(Dexterity,21)"
data "Unique" "1"
```

### Step 3: Add Cloak Template to merged.lsx

```xml
<node id="GameObjects">
    <attribute id="Description" type="TranslatedString" handle="h2b3c4d5eg6f7ag8b9cg0d1eg2f3a4b5c6d7e8" version="1" />
    <attribute id="DisplayName" type="TranslatedString" handle="h1a2b3c4dg5e6fg7a8bg9c0dg1e2f3a4b5c6d7" version="1" />
    <attribute id="LevelName" type="FixedString" value="" />
    <attribute id="MapKey" type="FixedString" value="b1c2d3e4-f5a6-4b7c-8d9e-0f1a2b3c4d5e" />
    <attribute id="Name" type="LSString" value="SMR_Cloak_Tyr" />
    <attribute id="ParentTemplateId" type="FixedString" value="f1fdb8db-e754-4ea9-b6ce-440db6b776ac" />
    <attribute id="Stats" type="FixedString" value="SMR_Cloak_Tyr" />
    <attribute id="Type" type="FixedString" value="item" />
    <attribute id="_OriginalFileVersion_" type="int64" value="144115188075855912" />
    <children>
        <node id="GameMaster" />
    </children>
</node>
```

### Step 4: Add Cloak Template to merged.lsf.lsx

Add the same GameObjects node (BOTH files must be updated).

### Step 5: Add to OneTimeRewards.lsx

```xml
<node id="OneTimeReward">
    <attribute id="Amount" type="uint32" value="1"/>
    <attribute id="ItemTemplateId" type="FixedString" value="b1c2d3e4-f5a6-4b7c-8d9e-0f1a2b3c4d5e"/>
    <attribute id="UUID" type="guid" value="c2d3e4f5-a6b7-4c8d-9e0f-1a2b3c4d5e6f"/>
</node>
```

### Step 6: Add Localization Entries

Add to Localization/English/SampleMagicRingMod.xml:
```xml
<content contentuid="h1a2b3c4dg5e6fg7a8bg9c0dg1e2f3a4b5c6d7" version="1">Mantle of Tyr</content>
<content contentuid="h2b3c4d5eg6f7ag8b9cg0d1eg2f3a4b5c6d7e8" version="1">A cloak blessed by Tyr, the God of Justice. Grants unlimited Crusader's Mantle and divine physical prowess (Strength 24, Constitution 21, Dexterity 21).</content>
<content contentuid="h3b4c5d6eg7f8ag9b0cg1d2eg3f4a5b6c7d8e9f0" version="1">Tyr's Crusade</content>
<content contentuid="h4c5d6e7fg8a9bg0c1dg2e3fg4a5b6c7d8e9f0a1" version="1">Crusader's Mantle. Unlimited uses.</content>
```

Add same entries to Localization/English/SampleMagicRingMod.loca.xml.

---

## Implementation Checklist

### Research
- [x] Find MAG_Radiant_CrusaderMantle_Cloak stats in game files
- [x] Document base item's Boosts and PassivesOnEquip

### Mantle of Tyr
- [x] Add SMR_Shout_CrusadersMantle_Unlimited to Spell_Shout.txt
- [x] Add SMR_Cloak_Tyr to Armor.txt
- [x] Add cloak template to merged.lsx
- [x] Add cloak template to merged.lsf.lsx
- [x] Add OneTimeReward entry
- [x] Add localization to SampleMagicRingMod.xml
- [x] Add localization to SampleMagicRingMod.loca.xml

### Sword of Tyr
- [x] Add SMR_Target_BlindingSmite_Unlimited to Spell_Target.txt
- [x] Add SMR_Sword_Tyr to Weapon.txt
- [x] Add sword template to merged.lsx
- [x] Add sword template to merged.lsf.lsx
- [x] Add OneTimeReward entry
- [x] Add localization to SampleMagicRingMod.xml
- [x] Add localization to SampleMagicRingMod.loca.xml

### Shield of Tyr
- [x] Add SMR_Shield_Tyr to Armor.txt
- [x] Add shield template to merged.lsx
- [x] Add shield template to merged.lsf.lsx
- [x] Add OneTimeReward entry
- [x] Add localization to SampleMagicRingMod.xml
- [x] Add localization to SampleMagicRingMod.loca.xml

### Helmet of Tyr
- [x] Add SMR_Helmet_Tyr to Armor.txt
- [x] Add helmet template to merged.lsx
- [x] Add helmet template to merged.lsf.lsx
- [x] Add OneTimeReward entry
- [x] Add localization to SampleMagicRingMod.xml
- [x] Add localization to SampleMagicRingMod.loca.xml

### Gloves of Tyr
- [x] Add SMR_Zone_Thunderwave_ShortRest to Spell_Zone.txt
- [x] Add SMR_Gloves_Tyr to Armor.txt
- [x] Add gloves template to merged.lsx
- [x] Add gloves template to merged.lsf.lsx
- [x] Add OneTimeReward entry
- [x] Add localization to SampleMagicRingMod.xml
- [x] Add localization to SampleMagicRingMod.loca.xml

### Boots of the Stormwalker
- [x] Update SMR_Boots_Stormwalker in Armor.txt to use SMR_Target_MistyStep_Unlimited

### Documentation
- [ ] Create mantle_of_tyr.md (optional)
- [ ] Create sword_of_tyr.md (optional)
- [ ] Create shield_of_tyr.md (optional)
- [ ] Create helmet_of_tyr.md (optional)
- [ ] Create gloves_of_tyr.md (optional)
- [ ] Update boots_of_the_stormwalker.md (optional)

### Final
- [x] Build and test mod

---

## Test Plan

### Mantle of Tyr
- [ ] Load game with mod enabled
- [ ] Check traveler's chest for Mantle of Tyr
- [ ] Equip cloak and verify appearance matches Mantle of the Holy Warrior
- [ ] Verify Strength is set to 24 (or unchanged if already higher)
- [ ] Verify Constitution is set to 21 (or unchanged if already higher)
- [ ] Verify Dexterity is set to 21 (or unchanged if already higher)
- [ ] Verify Tyr's Crusade (Crusader's Mantle) spell is available
- [ ] Cast Crusader's Mantle and verify it works
- [ ] Verify spell can be cast again without resting (unlimited)

### Sword of Tyr
- [ ] Check traveler's chest for Sword of Tyr
- [ ] Equip sword and verify appearance matches Voss's Silver Sword
- [ ] Verify Wrathful Smite spell is available
- [ ] Verify Tyr's Blinding Smite spell is available
- [ ] Cast Blinding Smite and verify it works
- [ ] Verify Blinding Smite can be cast again without resting (unlimited)
- [ ] Verify Soulbreaker passive works

### Shield of Tyr
- [ ] Check traveler's chest for Shield of Tyr
- [ ] Equip shield and verify appearance matches Viconia's Walking Fortress
- [ ] Verify Reflective Shell spell is available (once per short rest)
- [ ] Cast Reflective Shell and verify +2 AC against ranged attacks
- [ ] Verify Warding Bond spell is available (once per long rest)
- [ ] Cast Warding Bond on ally and verify bond is established
- [ ] Verify Shield Riposte reaction is available (2d4 Force damage when hit)
- [ ] Verify Spellguard passive works (advantage on spell saves)
- [ ] Verify Shield reaction is available (unlimited)
- [ ] Use Shield reaction when attacked and verify +5 AC bonus

### Helmet of Tyr
- [ ] Check traveler's chest for Helmet of Tyr
- [ ] Equip helmet and verify appearance matches Helm of Balduran
- [ ] Verify +1 AC bonus from Balduran's Protection
- [ ] Verify +1 saving throw bonus from Balduran's Protection
- [ ] Verify Stun Immunity (cannot be stunned)
- [ ] Verify Critical Hit Immunity (enemies cannot crit)
- [ ] Verify HP Regeneration (heal 2 HP at start of turn in combat)
- [ ] Verify Fear Immunity (cannot be frightened)
- [ ] Verify Blind Immunity (cannot be blinded)
- [ ] Verify Darkvision is active
- [ ] Verify Speak with Dead spell is available (unlimited)
- [ ] Verify Speak with Animals spell is available (unlimited)
- [ ] Verify See Invisibility spell is available (bonus action, unlimited)
- [ ] Verify Protection From Evil And Good spell is available (bonus action, unlimited)
- [ ] Verify Faerie Fire spell is available (bonus action, once per short rest)

### Gloves of Tyr
- [ ] Check traveler's chest for Gloves of Tyr
- [ ] Equip gloves and verify appearance matches Luminous Gloves
- [ ] Verify Radiating Orb passive works (deal Radiant damage, target gets Radiating Orb)
- [ ] Verify Tyr's Thunder (Thunderwave) spell is available (bonus action)
- [ ] Cast Thunderwave and verify it works (AOE thunder damage + push)
- [ ] Verify Thunderwave has short rest cooldown

### Boots of the Stormwalker
- [ ] Equip Boots of the Stormwalker
- [ ] Verify Spectral Step (Misty Step) spell is available
- [ ] Cast Misty Step and verify it works
- [ ] Verify spell can be cast again without resting (unlimited)
- [ ] Verify Reverberation passive still works
- [ ] Verify Web Immunity still works

---

---

## Item 2: Sword of Tyr

### Overview
A legendary longsword based on Voss's Silver Sword, with all its powers plus unlimited Blinding Smite.

### Item Details

| Aspect | Value |
|--------|-------|
| Name | Sword of Tyr |
| Internal ID | SMR_Sword_Tyr |
| Base Item | Voss's Silver Sword (MAG_Primeval_Silver_Longsword) |
| ParentTemplateId | e3b2adb6-7493-466e-9c65-4281fb74e83f |
| VisualTemplate | 5f9832fa-7633-5e68-b69c-0156eda17471 |
| Rarity | Legendary |
| Unique | Yes |

### Research Results - Voss's Silver Sword

```
new entry "MAG_Primeval_Silver_Longsword"
type "Weapon"
using "WPN_Longsword_2"
data "RootTemplate" "20c66f8d-f455-42fc-8e48-543512247e75"
data "Rarity" "VeryRare"
data "Boosts" "UnlockSpell(Target_MAG_Smite_Wrathful)"
data "PassivesOnEquip" "MAG_PlaneShifterSlayer_Passive"
data "Unique" "1"
```

### Powers

| Power | Description | Implementation |
|-------|-------------|----------------|
| **Wrathful Smite** | Melee attack deals extra psychic damage, may Frighten | `UnlockSpell(Target_MAG_Smite_Wrathful)` (from Voss's sword) |
| **Soulbreaker** | Extra damage vs specific creatures | `MAG_PlaneShifterSlayer_Passive` (from Voss's sword) |
| **Tyr's Blinding Smite** | Blinding Smite (unlimited) | `UnlockSpell(SMR_Target_BlindingSmite_Unlimited)` |

### UUIDs and Handles

| Item | Type | Value |
|------|------|-------|
| Sword MapKey | UUID | `d2e3f4a5-b6c7-4d8e-9f0a-1b2c3d4e5f6a` |
| OneTimeReward | UUID | `e3f4a5b6-c7d8-4e9f-0a1b-2c3d4e5f6a7b` |
| Sword DisplayName | Handle | `h5c6d7e8fg9a0bg1c2dg3e4fg5a6b7c8d9e0f1` |
| Sword Description | Handle | `h6d7e8f9ag0b1cg2d3eg4f5ag6b7c8d9e0f1a2` |
| Spell DisplayName | Handle | `h7e8f9a0bg1c2dg3e4fg5a6bg7c8d9e0f1a2b3` |
| Spell ExtraDescription | Handle | `h8f9a0b1cg2d3eg4f5ag6b7cg8d9e0f1a2b3c4` |

### Implementation

#### Spell_Target.txt - Unlimited Blinding Smite
```
new entry "SMR_Target_BlindingSmite_Unlimited"
type "SpellData"
data "SpellType" "Target"
using "Target_Smite_Blinding"
data "DisplayName" "h7e8f9a0bg1c2dg3e4fg5a6bg7c8d9e0f1a2b3;1"
data "ExtraDescription" "h8f9a0b1cg2d3eg4f5ag6b7cg8d9e0f1a2b3c4;1"
data "UseCosts" "ActionPoint:1"
```

#### Weapon.txt
```
new entry "SMR_Sword_Tyr"
type "Weapon"
using "WPN_Longsword_2"
data "RootTemplate" "d2e3f4a5-b6c7-4d8e-9f0a-1b2c3d4e5f6a"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(Target_MAG_Smite_Wrathful);UnlockSpell(SMR_Target_BlindingSmite_Unlimited)"
data "PassivesOnEquip" "MAG_PlaneShifterSlayer_Passive"
data "Unique" "1"
```

#### RootTemplates (merged.lsx and merged.lsf.lsx)
```xml
<node id="GameObjects">
    <attribute id="Description" type="TranslatedString" handle="h6d7e8f9ag0b1cg2d3eg4f5ag6b7c8d9e0f1a2" version="1" />
    <attribute id="DisplayName" type="TranslatedString" handle="h5c6d7e8fg9a0bg1c2dg3e4fg5a6b7c8d9e0f1" version="1" />
    <attribute id="LevelName" type="FixedString" value="" />
    <attribute id="MapKey" type="FixedString" value="d2e3f4a5-b6c7-4d8e-9f0a-1b2c3d4e5f6a" />
    <attribute id="Name" type="LSString" value="SMR_Sword_Tyr" />
    <attribute id="ParentTemplateId" type="FixedString" value="e3b2adb6-7493-466e-9c65-4281fb74e83f" />
    <attribute id="Stats" type="FixedString" value="SMR_Sword_Tyr" />
    <attribute id="Type" type="FixedString" value="item" />
    <attribute id="VisualTemplate" type="FixedString" value="5f9832fa-7633-5e68-b69c-0156eda17471" />
    <attribute id="_OriginalFileVersion_" type="int64" value="144115188075855912" />
    <children>
        <node id="GameMaster" />
    </children>
</node>
```

#### Localization
```xml
<content contentuid="h5c6d7e8fg9a0bg1c2dg3e4fg5a6b7c8d9e0f1" version="1">Sword of Tyr</content>
<content contentuid="h6d7e8f9ag0b1cg2d3eg4f5ag6b7c8d9e0f1a2" version="1">A silver longsword blessed by Tyr, the God of Justice. Grants Wrathful Smite, Soulbreaker, and unlimited Blinding Smite.</content>
<content contentuid="h7e8f9a0bg1c2dg3e4fg5a6bg7c8d9e0f1a2b3" version="1">Tyr's Blinding Smite</content>
<content contentuid="h8f9a0b1cg2d3eg4f5ag6b7cg8d9e0f1a2b3c4" version="1">Blinding Smite. Unlimited uses.</content>
```

---

## Item 3: Shield of Tyr

### Overview
A legendary shield based on Viconia's Walking Fortress (Viconia's Shield), with all its powerful defensive abilities.

### Item Details

| Aspect | Value |
|--------|-------|
| Name | Shield of Tyr |
| Internal ID | SMR_Shield_Tyr |
| Base Item | Viconia's Walking Fortress (MAG_TheBulwark_Shield) |
| ParentTemplateId | 4f313dde-14bb-43a2-abdd-07b2eb38b33a |
| Rarity | Legendary |
| Unique | Yes |

### Research Results - Viconia's Walking Fortress

```
new entry "MAG_TheBulwark_Shield"
type "Armor"
using "ARM_Shield_1"
data "RootTemplate" "4f313dde-14bb-43a2-abdd-07b2eb38b33a"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(Shout_MAG_TheBulwark_ReflectiveShell);UnlockSpell(Target_MAG_WardingBond)"
data "PassivesOnEquip" "MAG_Legendary_ShieldRiposte_Passive;MAG_Legendary_Spellguard_Passive"
data "Unique" "1"
```

**Passives:**
- `MAG_Legendary_ShieldRiposte_Passive` - Unlocks `Interrupt_Legendary_ShieldBlow` (2d4 Force damage reaction when attacked)
- `MAG_Legendary_Spellguard_Passive` - Advantage on saving throws against spells; attackers have disadvantage on spell attacks

**Spells:**
- `Shout_MAG_TheBulwark_ReflectiveShell` - Reflective Shell (once per short rest)
- `Target_MAG_WardingBond` - Warding Bond (once per long rest)

### Powers

| Power | Description | Implementation |
|-------|-------------|----------------|
| **Reflective Shell** | Gain +2 AC against ranged attacks for 2 turns | `UnlockSpell(Shout_MAG_TheBulwark_ReflectiveShell)` |
| **Warding Bond** | Link with ally - share damage and grant +1 AC/saves | `UnlockSpell(Target_MAG_WardingBond)` |
| **Shield Riposte** | When hit, can deal 2d4 Force damage as reaction | `MAG_Legendary_ShieldRiposte_Passive` |
| **Spellguard** | Advantage on spell saves; attackers have disadvantage on spell attacks | `MAG_Legendary_Spellguard_Passive` |
| **Shield** | Cast Shield as a reaction (unlimited) | `UnlockInterrupt(SMR_Interrupt_Shield_Unlimited)` |

### UUIDs and Handles

| Item | Type | Value |
|------|------|-------|
| Shield MapKey | UUID | `f3a4b5c6-d7e8-4f9a-0b1c-2d3e4f5a6b7c` |
| OneTimeReward | UUID | `a4b5c6d7-e8f9-4a0b-1c2d-3e4f5a6b7c8d` |
| Shield DisplayName | Handle | `h9a0b1c2dg3e4fg5a6bg7c8dg9e0f1a2b3c4d5` |
| Shield Description | Handle | `ha0b1c2d3eg4f5ag6b7cg8d9eg0f1a2b3c4d5e6` |

### Implementation

#### Armor.txt
```
new entry "SMR_Shield_Tyr"
type "Armor"
using "ARM_Shield_1"
data "RootTemplate" "f3a4b5c6-d7e8-4f9a-0b1c-2d3e4f5a6b7c"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(Shout_MAG_TheBulwark_ReflectiveShell);UnlockSpell(Target_MAG_WardingBond);UnlockInterrupt(SMR_Interrupt_Shield_Unlimited)"
data "PassivesOnEquip" "MAG_Legendary_ShieldRiposte_Passive;MAG_Legendary_Spellguard_Passive"
data "Unique" "1"
```

#### RootTemplates (merged.lsx and merged.lsf.lsx)
```xml
<node id="GameObjects">
    <attribute id="Description" type="TranslatedString" handle="ha0b1c2d3eg4f5ag6b7cg8d9eg0f1a2b3c4d5e6" version="1" />
    <attribute id="DisplayName" type="TranslatedString" handle="h9a0b1c2dg3e4fg5a6bg7c8dg9e0f1a2b3c4d5" version="1" />
    <attribute id="LevelName" type="FixedString" value="" />
    <attribute id="MapKey" type="FixedString" value="f3a4b5c6-d7e8-4f9a-0b1c-2d3e4f5a6b7c" />
    <attribute id="Name" type="LSString" value="SMR_Shield_Tyr" />
    <attribute id="ParentTemplateId" type="FixedString" value="4f313dde-14bb-43a2-abdd-07b2eb38b33a" />
    <attribute id="Stats" type="FixedString" value="SMR_Shield_Tyr" />
    <attribute id="Type" type="FixedString" value="item" />
    <attribute id="_OriginalFileVersion_" type="int64" value="144115188075855912" />
    <children>
        <node id="GameMaster" />
    </children>
</node>
```

#### Localization
```xml
<content contentuid="h9a0b1c2dg3e4fg5a6bg7c8dg9e0f1a2b3c4d5" version="1">Shield of Tyr</content>
<content contentuid="ha0b1c2d3eg4f5ag6b7cg8d9eg0f1a2b3c4d5e6" version="1">A shield blessed by Tyr, the God of Justice. Grants Reflective Shell, Warding Bond, Shield Riposte, Spellguard, and unlimited Shield spell.</content>
```

---

## Item 4: Helmet of Tyr

### Overview
A legendary helmet combining the defensive powers of the Helm of Balduran with all the divination and utility abilities of the Magus Circlet.

### Item Details

| Aspect | Value |
|--------|-------|
| Name | Helmet of Tyr |
| Internal ID | SMR_Helmet_Tyr |
| Base Item | Helm of Balduran (MAG_WYRM_OfBalduran_Helmet) + Magus Circlet powers |
| ParentTemplateId | 0a64283a-1fc4-45cd-9e5e-f463f6b762ea |
| Rarity | Legendary |
| Unique | Yes |

### Research Results - Helm of Balduran

```
new entry "MAG_WYRM_OfBalduran_Helmet"
type "Armor"
using "_Head_Magic_Metal"
data "RootTemplate" "0a64283a-1fc4-45cd-9e5e-f463f6b762ea"
data "Rarity" "Legendary"
data "Boosts" "CriticalHit(AttackTarget,Success,Never)"
data "PassivesOnEquip" "MAG_HelmOfBalduran_MaxHP_Passive;MAG_HelmOfBalduran_Protection_Passive;MAG_StunnImmunity_Passive"
data "StatusOnEquip" "MAG_HELM_OF_BALDURAN_REGENERATION"
data "Unique" "1"
```

**Boosts:**
- `CriticalHit(AttackTarget,Success,Never)` - Enemies cannot land critical hits on the wearer

**Passives:**
- `MAG_HelmOfBalduran_MaxHP_Passive` - Balduran's Vitality (regeneration related)
- `MAG_HelmOfBalduran_Protection_Passive` - +1 AC and +1 to all saving throws
- `MAG_StunnImmunity_Passive` - Immunity to Stunned condition

**Status:**
- `MAG_HELM_OF_BALDURAN_REGENERATION` - Regenerate 2 HP at the start of each turn (in combat, if not downed)

### Powers

#### From Helm of Balduran

| Power | Description | Implementation |
|-------|-------------|----------------|
| **Balduran's Vitality** | Regenerate HP, max HP bonus | `MAG_HelmOfBalduran_MaxHP_Passive` |
| **Balduran's Protection** | +1 AC and +1 to all saving throws | `MAG_HelmOfBalduran_Protection_Passive` |
| **Stun Immunity** | Immune to Stunned condition | `MAG_StunnImmunity_Passive` |
| **Critical Hit Immunity** | Enemies cannot crit you | `CriticalHit(AttackTarget,Success,Never)` |
| **Regeneration** | Heal 2 HP at start of turn in combat | `MAG_HELM_OF_BALDURAN_REGENERATION` status |

#### From Magus Circlet

| Power | Description | Implementation |
|-------|-------------|----------------|
| **Speak with Dead** | Cast Speak with Dead (unlimited) | `UnlockSpell(WW_Target_SpeakWithDead)` |
| **Speak with Animals** | Cast Speak with Animals (unlimited) | `UnlockSpell(WW_Shout_SpeakWithAnimals)` |
| **See Invisibility** | Cast See Invisibility (unlimited, bonus action) | `UnlockSpell(SMR_Shout_SeeInvisibility_Unlimited)` |
| **Protection From Evil And Good** | Cast Protection From Evil And Good (unlimited, bonus action) | `UnlockSpell(SMR_Target_ProtectionFromEvilAndGood_Unlimited)` |
| **Faerie Fire** | Cast Faerie Fire (bonus action, once per short rest) | `UnlockSpell(SMR_Target_FaerieFire_ShortRest)` |
| **Fear Immunity** | Immune to Frightened condition | `MAG_LC_Cyric_FearImmunity_Amulet_Passive` |
| **Blind Immunity** | Immune to blindness, can see through darkness | `MAG_Shadow_BlindImmunity_Ring_Passive` |
| **Darkvision** | Can see in the dark | `UND_SocietyOfBrilliance_DarkvisionRing_Passive` |

### UUIDs and Handles

| Item | Type | Value |
|------|------|-------|
| Helmet MapKey | UUID | `b4c5d6e7-f8a9-4b0c-1d2e-3f4a5b6c7d8e` |
| OneTimeReward | UUID | `c5d6e7f8-a9b0-4c1d-2e3f-4a5b6c7d8e9f` |
| Helmet DisplayName | Handle | `hb1c2d3e4fg5a6bg7c8dg9e0fg1a2b3c4d5e6` |
| Helmet Description | Handle | `hc2d3e4f5ag6b7cg8d9eg0f1ag2b3c4d5e6f7` |

### Implementation

#### Armor.txt
```
new entry "SMR_Helmet_Tyr"
type "Armor"
using "_Head_Magic_Metal"
data "RootTemplate" "b4c5d6e7-f8a9-4b0c-1d2e-3f4a5b6c7d8e"
data "Rarity" "Legendary"
data "Boosts" "CriticalHit(AttackTarget,Success,Never);UnlockSpell(WW_Target_SpeakWithDead);UnlockSpell(WW_Shout_SpeakWithAnimals);UnlockSpell(SMR_Shout_SeeInvisibility_Unlimited);UnlockSpell(SMR_Target_ProtectionFromEvilAndGood_Unlimited);UnlockSpell(SMR_Target_FaerieFire_ShortRest)"
data "PassivesOnEquip" "MAG_HelmOfBalduran_MaxHP_Passive;MAG_HelmOfBalduran_Protection_Passive;MAG_StunnImmunity_Passive;MAG_LC_Cyric_FearImmunity_Amulet_Passive;MAG_Shadow_BlindImmunity_Ring_Passive;UND_SocietyOfBrilliance_DarkvisionRing_Passive"
data "StatusOnEquip" "MAG_HELM_OF_BALDURAN_REGENERATION"
data "Unique" "1"
```

#### RootTemplates (merged.lsx and merged.lsf.lsx)
```xml
<node id="GameObjects">
    <attribute id="Description" type="TranslatedString" handle="hc2d3e4f5ag6b7cg8d9eg0f1ag2b3c4d5e6f7" version="1" />
    <attribute id="DisplayName" type="TranslatedString" handle="hb1c2d3e4fg5a6bg7c8dg9e0fg1a2b3c4d5e6" version="1" />
    <attribute id="LevelName" type="FixedString" value="" />
    <attribute id="MapKey" type="FixedString" value="b4c5d6e7-f8a9-4b0c-1d2e-3f4a5b6c7d8e" />
    <attribute id="Name" type="LSString" value="SMR_Helmet_Tyr" />
    <attribute id="ParentTemplateId" type="FixedString" value="0a64283a-1fc4-45cd-9e5e-f463f6b762ea" />
    <attribute id="Stats" type="FixedString" value="SMR_Helmet_Tyr" />
    <attribute id="Type" type="FixedString" value="item" />
    <attribute id="_OriginalFileVersion_" type="int64" value="144115188075855912" />
    <children>
        <node id="GameMaster" />
    </children>
</node>
```

#### Localization
```xml
<content contentuid="hb1c2d3e4fg5a6bg7c8dg9e0fg1a2b3c4d5e6" version="1">Helmet of Tyr</content>
<content contentuid="hc2d3e4f5ag6b7cg8d9eg0f1ag2b3c4d5e6f7" version="1">A helmet blessed by Tyr, the God of Justice. Grants Balduran's Vitality, Balduran's Protection, Stun/Fear/Blind Immunity, Critical Hit Immunity, HP Regeneration, Darkvision, and the spells Speak with Dead, Speak with Animals, See Invisibility, Protection From Evil And Good, and Faerie Fire.</content>
```

---

## Item 5: Gloves of Tyr

### Overview
Legendary gloves based on the Luminous Gloves, with the added power of Thunderwave.

### Item Details

| Aspect | Value |
|--------|-------|
| Name | Gloves of Tyr |
| Internal ID | SMR_Gloves_Tyr |
| Base Item | Luminous Gloves (MAG_Radiant_RadiatingOrb_Gloves) |
| ParentTemplateId | e8a72355-b81f-484e-bc7d-945ec81c04a3 |
| Rarity | Legendary |
| Unique | Yes |

### Research Results - Luminous Gloves

```
new entry "MAG_Radiant_RadiatingOrb_Gloves"
type "Armor"
using "_Hand_Magic_Metal"
data "RootTemplate" "e8a72355-b81f-484e-bc7d-945ec81c04a3"
data "Rarity" "Uncommon"
data "PassivesOnEquip" "MAG_Radiant_RadiatingOrb_Gloves_Passive"
data "Unique" "1"
```

**Passives:**
- `MAG_Radiant_RadiatingOrb_Gloves_Passive` - Radiating Orb: When dealing Radiant damage, inflict 2 turns of Radiating Orb on the target (reduces attack rolls)

### Powers

| Power | Description | Implementation |
|-------|-------------|----------------|
| **Radiating Orb** | When dealing Radiant damage, inflict Radiating Orb on target | `MAG_Radiant_RadiatingOrb_Gloves_Passive` |
| **Tyr's Thunder** | Cast Thunderwave (bonus action, once per short rest) | `UnlockSpell(SMR_Zone_Thunderwave_ShortRest)` |

### UUIDs and Handles

| Item | Type | Value |
|------|------|-------|
| Gloves MapKey | UUID | `d5e6f7a8-b9c0-4d1e-2f3a-4b5c6d7e8f9a` |
| OneTimeReward | UUID | `e6f7a8b9-c0d1-4e2f-3a4b-5c6d7e8f9a0b` |
| Gloves DisplayName | Handle | `hd3e4f5a6bg7c8dg9e0fg1a2bg3c4d5e6f7a8` |
| Gloves Description | Handle | `he4f5a6b7cg8d9eg0f1ag2b3cg4d5e6f7a8b9` |
| Spell DisplayName | Handle | `hf5a6b7c8dg9e0fg1a2bg3c4dg5e6f7a8b9c0` |
| Spell ExtraDescription | Handle | `ha6b7c8d9eg0f1ag2b3cg4d5eg6f7a8b9c0d1` |

### Implementation

#### Spell_Zone.txt - Tyr's Thunder
```
new entry "SMR_Zone_Thunderwave_ShortRest"
type "SpellData"
data "SpellType" "Zone"
using "Zone_Thunderwave"
data "DisplayName" "hf5a6b7c8dg9e0fg1a2bg3c4dg5e6f7a8b9c0;1"
data "ExtraDescription" "ha6b7c8d9eg0f1ag2b3cg4d5eg6f7a8b9c0d1;1"
data "UseCosts" "BonusActionPoint:1"
data "Cooldown" "OncePerShortRest"
```

#### Armor.txt
```
new entry "SMR_Gloves_Tyr"
type "Armor"
using "_Hand_Magic_Metal"
data "RootTemplate" "d5e6f7a8-b9c0-4d1e-2f3a-4b5c6d7e8f9a"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(SMR_Zone_Thunderwave_ShortRest)"
data "PassivesOnEquip" "MAG_Radiant_RadiatingOrb_Gloves_Passive"
data "Unique" "1"
```

#### RootTemplates (merged.lsx and merged.lsf.lsx)
```xml
<node id="GameObjects">
    <attribute id="Description" type="TranslatedString" handle="he4f5a6b7cg8d9eg0f1ag2b3cg4d5e6f7a8b9" version="1" />
    <attribute id="DisplayName" type="TranslatedString" handle="hd3e4f5a6bg7c8dg9e0fg1a2bg3c4d5e6f7a8" version="1" />
    <attribute id="LevelName" type="FixedString" value="" />
    <attribute id="MapKey" type="FixedString" value="d5e6f7a8-b9c0-4d1e-2f3a-4b5c6d7e8f9a" />
    <attribute id="Name" type="LSString" value="SMR_Gloves_Tyr" />
    <attribute id="ParentTemplateId" type="FixedString" value="e8a72355-b81f-484e-bc7d-945ec81c04a3" />
    <attribute id="Stats" type="FixedString" value="SMR_Gloves_Tyr" />
    <attribute id="Type" type="FixedString" value="item" />
    <attribute id="_OriginalFileVersion_" type="int64" value="144115188075855912" />
    <children>
        <node id="GameMaster" />
    </children>
</node>
```

#### Localization
```xml
<content contentuid="hd3e4f5a6bg7c8dg9e0fg1a2bg3c4d5e6f7a8" version="1">Gloves of Tyr</content>
<content contentuid="he4f5a6b7cg8d9eg0f1ag2b3cg4d5e6f7a8b9" version="1">Gloves blessed by Tyr, the God of Justice. Inflicts Radiating Orb when dealing Radiant damage and grants Tyr's Thunder (Thunderwave).</content>
<content contentuid="hf5a6b7c8dg9e0fg1a2bg3c4dg5e6f7a8b9c0" version="1">Tyr's Thunder</content>
<content contentuid="ha6b7c8d9eg0f1ag2b3cg4d5eg6f7a8b9c0d1" version="1">Thunderwave. Once per short rest.</content>
```

---

## Item 6: Boots of the Stormwalker Enhancement

### Overview
Update the existing Boots of the Stormwalker to allow unlimited Misty Step casts instead of once per short rest.

### Current Implementation
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

### Change Required
Replace `Target_UNI_MistyStep_NightWalkers` (once per short rest) with `SMR_Target_MistyStep_Unlimited` (already exists in mod from Ring of Spectral Power).

### New Implementation
```
new entry "SMR_Boots_Stormwalker"
type "Armor"
using "_Foot_Magic"
data "RootTemplate" "e1f2a3b4-c5d6-4e7f-8a9b-0c1d2e3f4a5b"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(SMR_Target_MistyStep_Unlimited)"
data "PassivesOnEquip" "MAG_Thunder_ReverberationOnStatusApply_Boots_Passive;FOR_NightWalkers_WebImmunity"
data "Unique" "1"
```

---

## Notes

### Mantle of Tyr
- Uses Mantle of the Holy Warrior's ParentTemplateId (a5f5a875-932b-44c4-8b45-88d2ed379787) for appearance
- Base item only grants Crusader's Mantle spell - we replace it with unlimited version
- Strength 24 exceeds normal maximum of 20, making this very powerful
- Spell renamed to "Tyr's Crusade" to fit the item theme

### Sword of Tyr
- Uses Voss's Silver Sword's ParentTemplateId and VisualTemplate for appearance
- Inherits Wrathful Smite and Soulbreaker passive from base sword
- Adds unlimited Blinding Smite (no item currently grants this spell)
- Blinding Smite blinds target on failed Constitution save

### Shield of Tyr
- Uses Viconia's Walking Fortress's ParentTemplateId for appearance
- Copies all powers from the original shield plus adds Shield spell
- Shield Riposte is a reaction that deals 2d4 Force damage when hit
- Spellguard grants advantage on saves vs spells AND disadvantage to attackers using spell attacks
- Adds unlimited Shield spell reaction using existing SMR_Interrupt_Shield_Unlimited from Ring of Spectral Power
- No new spells or passives needed - reuses existing mod and vanilla references

### Helmet of Tyr
- Uses Helm of Balduran's ParentTemplateId for appearance
- Combines all powers from Helm of Balduran AND Magus Circlet
- **From Helm of Balduran:**
  - Balduran's Protection grants +1 AC and +1 to all saving throws
  - Regeneration heals 2 HP at start of each turn (only in combat, if not downed)
  - Critical Hit Immunity prevents enemies from landing crits
  - Stun Immunity prevents being stunned
- **From Magus Circlet:**
  - Fear Immunity, Blind Immunity, Darkvision (passives)
  - Speak with Dead, Speak with Animals, See Invisibility, Protection From Evil And Good, Faerie Fire (spells)
- Dependencies: WW_Wizard_Equipment mod for Speak with Dead/Animals spells
- Uses existing SMR spells from the mod for See Invisibility, Protection From Evil And Good, Faerie Fire

### Gloves of Tyr
- Uses Luminous Gloves' ParentTemplateId for appearance
- Keeps the Radiating Orb passive from the base gloves
- Adds new Thunderwave spell (SMR_Zone_Thunderwave_ShortRest) as bonus action, once per short rest
- Thunderwave is a Zone type spell - creates AOE thunder damage and pushes enemies
- New spell file entry needed in Spell_Zone.txt

### Boots of the Stormwalker
- Reuses existing SMR_Target_MistyStep_Unlimited spell from Ring of Spectral Power
- No new spell creation needed
- Only change is in Armor.txt
