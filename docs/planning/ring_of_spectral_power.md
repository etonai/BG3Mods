# Ring of Spectral Power - Implementation Plan

## Overview
A Legendary ring granting powerful spectral/force magic abilities.

## Design Decisions (Complete)

| Aspect | Decision |
|--------|----------|
| Name | Ring of Spectral Power |
| Internal ID | SMR_Ring_Spectral_Power |
| Appearance | LOOT_GEN_Ring_D_Silver_A (same as Ring of Superior Healing Word) |
| Rarity | Legendary |
| Value | 750 gold |

### Powers
1. **Unlimited Misty Step** - Teleport at will (no spell slot cost)
2. **Globe of Invulnerability** - Once per short rest
3. **Unlimited Level 3 Magic Missile** - 5 missiles at will (bonus action)
4. **Unlimited Shield** - Cast Shield as a bonus action (unlimited)
5. **+1 Magic Missile** - Adds one extra missile to every Magic Missile cast (needs research)

---

## UUIDs and Handles Needed

Generate these before implementation:
- [ ] Ring MapKey UUID: `________-____-____-____-____________`
- [ ] OneTimeReward UUID: `________-____-____-____-____________`
- [ ] DisplayName handle: `h________________________________`
- [ ] Description handle: `h________________________________`
- [ ] MistyStep DisplayName handle: `h________________________________`
- [ ] MistyStep ExtraDescription handle: `h________________________________`
- [ ] MagicMissile DisplayName handle: `h________________________________`
- [ ] MagicMissile ExtraDescription handle: `h________________________________`
- [ ] Globe DisplayName handle: `h________________________________`
- [ ] Globe ExtraDescription handle: `h________________________________`
- [ ] Shield DisplayName handle: `h________________________________`
- [ ] Shield ExtraDescription handle: `h________________________________`

---

## Files to Modify

### 1. Public/SampleMagicRingMod/RootTemplates/merged.lsx

Add new GameObjects node:
```xml
<node id="GameObjects"> Ring of Spectral Power
    <attribute id="Description" type="TranslatedString" handle="[DESCRIPTION_HANDLE]" version="2" />
    <attribute id="DisplayName" type="TranslatedString" handle="[DISPLAYNAME_HANDLE]" version="3" />
    <attribute id="Icon" type="FixedString" value="Item_LOOT_GEN_Ring_D_Silver_A" />
    <attribute id="LevelName" type="FixedString" value="" />
    <attribute id="MapKey" type="FixedString" value="[RING_UUID]" />
    <attribute id="Name" type="LSString" value="SMR_Ring_Spectral_Power" />
    <attribute id="ParentTemplateId" type="FixedString" value="a9f741f6-a758-47ea-bb21-9a37d3ddfe42" />
    <attribute id="Stats" type="FixedString" value="SMR_Ring_Spectral_Power" />
    <attribute id="Type" type="FixedString" value="item" />
    <attribute id="_OriginalFileVersion_" type="int64" value="144115188075855912" />
    <children>
        <node id="GameMaster" />
    </children>
</node>
```

### 2. Public/SampleMagicRingMod/Stats/Generated/Data/Armor.txt

Add entry:
```
new entry "SMR_Ring_Spectral_Power"
type "Armor"
using "_Ring"
data "RootTemplate" "[RING_UUID]"
data "ObjectCategory" "Jewelry"
data "ValueOverride" "750"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(SMR_Target_MistyStep_Unlimited);UnlockSpell(SMR_Projectile_MagicMissile_Unlimited_Lvl3);UnlockSpell(SMR_Zone_GlobeOfInvulnerability_ShortRest)"
```

Note: +1 Magic Missile passive may need additional boost syntax (research required)

### 3. Public/SampleMagicRingMod/Stats/Generated/Data/Spell_Target.txt

Add entry:
```
new entry "SMR_Target_MistyStep_Unlimited"
type "SpellData"
data "SpellType" "Target"
using "Target_MistyStep"
data "DisplayName" "[MISTYSTEP_DISPLAYNAME_HANDLE];1"
data "ExtraDescription" "[MISTYSTEP_EXTRADESC_HANDLE];1"
data "UseCosts" ""
```

### 4. Public/SampleMagicRingMod/Stats/Generated/Data/Spell_Projectile.txt

Add entry:
```
new entry "SMR_Projectile_MagicMissile_Unlimited_Lvl3"
type "SpellData"
data "SpellType" "Projectile"
using "Projectile_MagicMissile_3"
data "DisplayName" "[MAGICMISSILE_DISPLAYNAME_HANDLE];1"
data "ExtraDescription" "[MAGICMISSILE_EXTRADESC_HANDLE];1"
data "UseCosts" "BonusActionPoint:1"
```

### 5. NEW FILE: Public/SampleMagicRingMod/Stats/Generated/Data/Spell_Zone.txt

Create file with:
```
new entry "SMR_Zone_GlobeOfInvulnerability_ShortRest"
type "SpellData"
data "SpellType" "Zone"
using "Zone_GlobeOfInvulnerability"
data "DisplayName" "[GLOBE_DISPLAYNAME_HANDLE];1"
data "ExtraDescription" "[GLOBE_EXTRADESC_HANDLE];1"
data "UseCosts" ""
data "Cooldown" "OncePerShortRest"
```

### 6. Localization/English/SampleMagicRingMod.xml

Add entries:
```xml
<content contentuid="[DISPLAYNAME_HANDLE]" version="1">Ring of Spectral Power</content>
<content contentuid="[DESCRIPTION_HANDLE]" version="1">A ring crackling with arcane force. Grants unlimited Misty Step and Magic Missile (Level 3), plus Globe of Invulnerability once per short rest.</content>

<content contentuid="[MISTYSTEP_DISPLAYNAME_HANDLE]" version="1">Spectral Step</content>
<content contentuid="[MISTYSTEP_EXTRADESC_HANDLE]" version="1">Unlimited casting from Ring of Spectral Power.</content>

<content contentuid="[MAGICMISSILE_DISPLAYNAME_HANDLE]" version="1">Spectral Barrage</content>
<content contentuid="[MAGICMISSILE_EXTRADESC_HANDLE]" version="1">Unlimited Level 3 Magic Missile as a bonus action from Ring of Spectral Power.</content>

<content contentuid="[GLOBE_DISPLAYNAME_HANDLE]" version="1">Spectral Barrier</content>
<content contentuid="[GLOBE_EXTRADESC_HANDLE]" version="1">Globe of Invulnerability. Recharges on short rest.</content>
```

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

## Open Questions

### +1 Magic Missile Passive
Need to research how to implement "adds one extra missile to every Magic Missile cast":
- May require a Passive entry with conditional boost
- Could use `SpellExtraProjectiles` or similar boost
- Alternative: Create custom Magic Missile variants with +1 missile baked in

---

## Implementation Checklist

- [ ] Generate all UUIDs and handles using BG3 Modder's Multitool
- [ ] Add ring to merged.lsx
- [ ] Add ring stats to Armor.txt
- [ ] Add Misty Step spell to Spell_Target.txt
- [ ] Add Magic Missile spell to Spell_Projectile.txt
- [ ] Create Spell_Zone.txt with Globe spell
- [ ] Add localization entries
- [ ] Add to OneTimeRewards.lsx
- [ ] Test in-game
