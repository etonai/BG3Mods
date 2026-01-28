# Ring of the Guardian - Implementation Plan

## Overview
A Legendary ring granting powerful protective and healing abilities.

## Design Decisions (Complete)

| Aspect | Decision |
|--------|----------|
| Name | Ring of the Guardian |
| Internal ID | SMR_Ring_Guardian |
| Appearance | LOOT_GEN_Ring_F_Silver_A (same as Star Athlete's Ring) |
| ParentTemplateId | 49b84359-6a28-460e-af98-4526c5fca6fd |
| Rarity | Legendary |
| Value | 750 gold |

### Powers

| Status | Power | Description | Phase |
|--------|-------|-------------|-------|
| [x] | **Superior Healing Word** | Enhanced healing (2d20+modifier), bonus action, no spell slot cost | Phase 4 |
| [x] | **Unlimited Bless** | Cast Bless unlimited times | Phase 5 |
| [x] | **Unlimited Create Water** | Cast Create Water as a bonus action (unlimited) | Phase 5 |
| [x] | **Lesser Restoration** | Cast Lesser Restoration (once per short rest) | Phase 5 |
| [x] | **Greater Restoration** | Cast Greater Restoration (once per long rest) | Phase 5 |
| [x] | **Freedom of Movement** | Cast Freedom of Movement (once per short rest) | Phase 5 |
| [x] | **Counterspell** | Cast Counterspell (once per short rest) | Phase 5 |
| [x] | **Heroes' Feast** | Cast Heroes' Feast (once per long rest) | Phase 5 |
| [ ] | **Remove Curse** | Cast Remove Curse (once per long rest) | Phase 7 |

---

## UUIDs and Handles Needed

Generate these before implementation:
- [ ] Ring MapKey UUID: `________-____-____-____-____________`
- [ ] OneTimeReward UUID: `________-____-____-____-____________`
- [ ] DisplayName handle: `h________________________________`
- [ ] Description handle: `h________________________________`
- [ ] Bless DisplayName handle: `h________________________________`
- [ ] Bless ExtraDescription handle: `h________________________________`
- [ ] CreateWater DisplayName handle: `h________________________________`
- [ ] CreateWater ExtraDescription handle: `h________________________________`
- [ ] LesserRestoration DisplayName handle: `h________________________________`
- [ ] LesserRestoration ExtraDescription handle: `h________________________________`
- [ ] GreaterRestoration DisplayName handle: `h________________________________`
- [ ] GreaterRestoration ExtraDescription handle: `h________________________________`
- [ ] FreedomOfMovement DisplayName handle: `h________________________________`
- [ ] FreedomOfMovement ExtraDescription handle: `h________________________________`
- [ ] Counterspell DisplayName handle: `h________________________________`
- [ ] Counterspell ExtraDescription handle: `h________________________________`
- [ ] HeroesFeast DisplayName handle: `h________________________________`
- [ ] HeroesFeast ExtraDescription handle: `h________________________________`

Note: Superior Healing Word spell already exists (SMR_Target_HealingWord_Superior) with existing localization.

---

## Files to Modify

### 1. Public/SampleMagicRingMod/RootTemplates/merged.lsx

Add new GameObjects node:
```xml
<node id="GameObjects"> Ring of the Guardian
    <attribute id="Description" type="TranslatedString" handle="[DESCRIPTION_HANDLE]" version="2" />
    <attribute id="DisplayName" type="TranslatedString" handle="[DISPLAYNAME_HANDLE]" version="3" />
    <attribute id="Icon" type="FixedString" value="Item_LOOT_GEN_Ring_F_Silver_A" />
    <attribute id="LevelName" type="FixedString" value="" />
    <attribute id="MapKey" type="FixedString" value="[RING_UUID]" />
    <attribute id="Name" type="LSString" value="SMR_Ring_Guardian" />
    <attribute id="ParentTemplateId" type="FixedString" value="49b84359-6a28-460e-af98-4526c5fca6fd" />
    <attribute id="Stats" type="FixedString" value="SMR_Ring_Guardian" />
    <attribute id="Type" type="FixedString" value="item" />
    <attribute id="_OriginalFileVersion_" type="int64" value="144115188075855912" />
    <children>
        <node id="GameMaster" />
    </children>
</node>
```

### 2. Public/SampleMagicRingMod/RootTemplates/merged.lsf.lsx

Add same GameObjects node (BOTH files must be updated!)

### 3. Public/SampleMagicRingMod/Stats/Generated/Data/Armor.txt

Add entry:
```
new entry "SMR_Ring_Guardian"
type "Armor"
using "_Ring"
data "RootTemplate" "[RING_UUID]"
data "ObjectCategory" "Jewelry"
data "ValueOverride" "750"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(SMR_Target_HealingWord_Superior);UnlockSpell(SMR_Shout_Bless_Unlimited)"
```

### 4. Public/SampleMagicRingMod/Stats/Generated/Data/Spell_Shout.txt (NEW FILE)

Create file with Bless spell:
```
new entry "SMR_Shout_Bless_Unlimited"
type "SpellData"
data "SpellType" "Shout"
using "Shout_Bless"
data "DisplayName" "[BLESS_DISPLAYNAME_HANDLE];1"
data "ExtraDescription" "[BLESS_EXTRADESC_HANDLE];1"
data "UseCosts" ""
```

### 5. Localization/English/SampleMagicRingMod.xml

Add entries:
```xml
<content contentuid="[DISPLAYNAME_HANDLE]" version="1">Ring of the Guardian</content>
<content contentuid="[DESCRIPTION_HANDLE]" version="1">A ring infused with protective energy. Grants Superior Healing Word and unlimited Bless.</content>

<content contentuid="[BLESS_DISPLAYNAME_HANDLE]" version="1">Guardian's Blessing</content>
<content contentuid="[BLESS_EXTRADESC_HANDLE]" version="1">Unlimited casting from Ring of the Guardian.</content>
```

### 6. Localization/English/SampleMagicRingMod.loca.xml

Add same entries (BOTH files must be updated!)

### 7. Public/SampleMagicRingMod/OneTimeRewards/OneTimeRewards.lsx

Add to children:
```xml
<node id="OneTimeReward">
    <attribute id="Amount" type="uint32" value="1"/>
    <attribute id="ItemTemplateId" type="FixedString" value="[RING_UUID]"/>
    <attribute id="UUID" type="guid" value="[ONETIMEREWARD_UUID]"/>
</node>
```

---

## Implementation Checklist

- [ ] Generate all UUIDs and handles using BG3 Modder's Multitool
- [ ] Add ring to merged.lsx
- [ ] Add ring to merged.lsf.lsx
- [ ] Add ring stats to Armor.txt
- [ ] Create Spell_Shout.txt with Bless spell
- [ ] Add localization entries to .xml
- [ ] Add localization entries to .loca.xml
- [ ] Add to OneTimeRewards.lsx
- [ ] Test in-game

---

## Notes

- Superior Healing Word spell (SMR_Target_HealingWord_Superior) already exists and can be reused
- Bless is a Shout type spell in BG3
- Base spell: `Shout_Bless`
