# Phase 020 - Divine Maul

**Status:** COMPLETE

## Goal
- Create new weapon: Divine Maul (based on WPN_HUM_Maul_A_1, Maul +1)

---

## Item 1: Divine Maul

### Reference: Vanilla Maul +1

| Attribute | Value |
|-----------|-------|
| MapKey | 7e8ef269-0e7b-4352-8828-89c5fced943c |
| Name | WPN_HUM_Maul_A_1 |

### Item Details

| Aspect | Value |
|--------|-------|
| Name | Divine Maul |
| Internal ID | SMR_Maul_Divine |
| Base Type | WPN_Maul_2 |
| RootTemplate | f6a7b8c9-d0e1-4f2a-3b4c-5d6e7f8a9b0c (custom) |
| ParentTemplateId | 7e8ef269-0e7b-4352-8828-89c5fced943c (Maul +1 appearance) |
| Rarity | Legendary |
| Unique | Yes |

### Planned Powers

| Power | Source | Description |
|-------|--------|-------------|
| +5 Enchantment | DefaultBoosts | WeaponEnchantment(5);WeaponProperty(Magical) |
| Radiant Weapon | SMR_RadiantWeapon_Passive | +1d8 radiant damage on melee attacks (from Phase 19) |

---

## Planned Implementation

### Weapon Definition (Weapon.txt)

```
new entry "SMR_Maul_Divine"
type "Weapon"
using "WPN_Maul_2"
data "RootTemplate" "f6a7b8c9-d0e1-4f2a-3b4c-5d6e7f8a9b0c"
data "Rarity" "Legendary"
data "DefaultBoosts" "WeaponEnchantment(5);WeaponProperty(Magical)"
data "PassivesOnEquip" "SMR_RadiantWeapon_Passive"
data "Unique" "1"
```

### RootTemplate (merged.lsx / merged.lsf.lsx)

```xml
<node id="GameObjects">
    <attribute id="Description" type="TranslatedString" handle="hb0c1d2e3fg4a5bg6c7dg8e9fg0a1b2c3d4e5" version="1" />
    <attribute id="DisplayName" type="TranslatedString" handle="h1b2c3d4eg5f6ag7b8cg9d0eg1f2a3b4c5d6" version="1" />
    <attribute id="LevelName" type="FixedString" value="" />
    <attribute id="MapKey" type="FixedString" value="f6a7b8c9-d0e1-4f2a-3b4c-5d6e7f8a9b0c" />
    <attribute id="Name" type="LSString" value="SMR_Maul_Divine" />
    <attribute id="ParentTemplateId" type="FixedString" value="7e8ef269-0e7b-4352-8828-89c5fced943c" />
    <attribute id="Stats" type="FixedString" value="SMR_Maul_Divine" />
    <attribute id="Type" type="FixedString" value="item" />
    <attribute id="_OriginalFileVersion_" type="int64" value="144115188075855912" />
    <children>
        <node id="GameMaster" />
    </children>
</node>
```

### OneTimeReward (OneTimeRewards.lsx)

```xml
<node id="OneTimeReward">
    <attribute id="Amount" type="uint32" value="1"/>
    <attribute id="ItemTemplateId" type="FixedString" value="f6a7b8c9-d0e1-4f2a-3b4c-5d6e7f8a9b0c"/>
    <attribute id="UUID" type="guid" value="a7b8c9d0-e1f2-4a3b-4c5d-6e7f8a9b0c1d"/>
</node>
```

---

## Implementation Checklist

### Divine Maul
- [x] Add SMR_Maul_Divine to Weapon.txt
- [x] Add weapon template to merged.lsx
- [x] Add weapon template to merged.lsf.lsx
- [x] Add localization to SampleMagicRingMod.loca.xml
- [x] Add OneTimeReward entry to OneTimeRewards.lsx

### Final
- [ ] Build and test mod

---

## Test Plan

### Divine Maul
- [ ] Check traveler's chest for Divine Maul
- [ ] Verify maul has Maul +1 appearance
- [ ] Verify weapon tooltip shows +5 bonus to attack and damage
- [ ] Verify Radiant Weapon passive appears and adds +1d8 radiant damage

---

## Notes

- The Divine Maul uses the vanilla Maul +1 (WPN_HUM_Maul_A_1) as its visual template
- Base weapon type is WPN_Maul_2 for maul damage dice
- Reuses SMR_RadiantWeapon_Passive from Phase 19 for +1d8 radiant damage on melee attacks
- Similar divine theme to Selune's Moonmace (Phase 17)
