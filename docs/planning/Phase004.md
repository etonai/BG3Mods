# Phase 004 - Ring of the Guardian (Minimal)

**Status:** COMPLETE (2026-01-27)

## Goal
Create the Ring of the Guardian with only the Superior Healing Word spell for initial testing.

## Scope
- Ring with single power: Superior Healing Word (bonus action, no spell slot)
- Uses existing spell: SMR_Target_HealingWord_Superior
- Delivered to Traveler's Chest via OneTimeRewards

## UUIDs and Handles Needed

| Item | Type | Value |
|------|------|-------|
| Ring MapKey | UUID | `a1b2c3d4-e5f6-4a7b-8c9d-0e1f2a3b4c5d` |
| OneTimeReward | UUID | `b2c3d4e5-f6a7-4b8c-9d0e-1f2a3b4c5d6e` |
| Ring DisplayName | Handle | `he5f6a7b8gc9d0g1e2fga3b4g8c9d0e1f2a3b4` |
| Ring Description | Handle | `h5e6f7a8bg9c0dg2e1fg4a3bg9c0d1e2f3a4b5` |

Note: Superior Healing Word spell already exists with localization - no new spell handles needed.

---

## Files to Modify

### 1. RootTemplates/merged.lsx
- [ ] Add GameObjects node for SMR_Ring_Guardian

### 2. RootTemplates/merged.lsf.lsx
- [ ] Add GameObjects node for SMR_Ring_Guardian (BOTH files must match!)

### 3. Stats/Generated/Data/Armor.txt
- [ ] Add SMR_Ring_Guardian entry (Legendary, 750 gold)

### 4. Localization/English/SampleMagicRingMod.xml
- [ ] Add Ring DisplayName: "Ring of the Guardian"
- [ ] Add Ring Description

### 5. Localization/English/SampleMagicRingMod.loca.xml
- [ ] Add same localization entries (BOTH files must match!)

### 6. OneTimeRewards/OneTimeRewards.lsx
- [ ] Add OneTimeReward entry for the ring

---

## Implementation Details

### Ring Template (merged.lsx / merged.lsf.lsx)
```xml
<node id="GameObjects"> Ring of the Guardian
    <attribute id="Description" type="TranslatedString" handle="h5e6f7a8bg9c0dg2e1fg4a3bg9c0d1e2f3a4b5" version="2" />
    <attribute id="DisplayName" type="TranslatedString" handle="he5f6a7b8gc9d0g1e2fga3b4g8c9d0e1f2a3b4" version="3" />
    <attribute id="Icon" type="FixedString" value="Item_LOOT_GEN_Ring_F_Silver_A" />
    <attribute id="LevelName" type="FixedString" value="" />
    <attribute id="MapKey" type="FixedString" value="a1b2c3d4-e5f6-4a7b-8c9d-0e1f2a3b4c5d" />
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

### Ring Stats (Armor.txt)
```
new entry "SMR_Ring_Guardian"
type "Armor"
using "_Ring"
data "RootTemplate" "a1b2c3d4-e5f6-4a7b-8c9d-0e1f2a3b4c5d"
data "ObjectCategory" "Jewelry"
data "ValueOverride" "750"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(SMR_Target_HealingWord_Superior)"
```

### Localization
```xml
<content contentuid="he5f6a7b8gc9d0g1e2fga3b4g8c9d0e1f2a3b4" version="1">Ring of the Guardian</content>
<content contentuid="h5e6f7a8bg9c0dg2e1fg4a3bg9c0d1e2f3a4b5" version="1">A ring infused with protective energy. Grants Superior Healing Word.</content>
```

### OneTimeReward
```xml
<node id="OneTimeReward">
    <attribute id="Amount" type="uint32" value="1"/>
    <attribute id="ItemTemplateId" type="FixedString" value="a1b2c3d4-e5f6-4a7b-8c9d-0e1f2a3b4c5d"/>
    <attribute id="UUID" type="guid" value="b2c3d4e5-f6a7-4b8c-9d0e-1f2a3b4c5d6e"/>
</node>
```

---

## Implementation Order

1. [x] Add ring to merged.lsx
2. [x] Add ring to merged.lsf.lsx
3. [x] Add ring stats to Armor.txt
4. [x] Add localization to SampleMagicRingMod.xml
5. [x] Add localization to SampleMagicRingMod.loca.xml
6. [x] Add to OneTimeRewards.lsx
7. [x] Build and test mod

---

## Test Plan

- [ ] Build mod with BG3 Modder's Multitool
- [ ] Load game with mod enabled
- [ ] Go to camp and check Traveler's Chest
- [ ] Equip ring
- [ ] Verify "Superior Healing Word" spell appears
- [ ] Cast spell - should cost bonus action, no spell slot
- [ ] Verify healing amount (2d20 + modifier)

---

## Notes

- Reuses existing SMR_Target_HealingWord_Superior spell from Ring of Superior Healing Word
- Uses Star Athlete's Ring appearance (Ring_F_Silver_A)
- Future phases will add Bless and other powers
