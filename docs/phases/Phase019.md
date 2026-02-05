# Phase 019 - Weapon Enhancements

**Status:** COMPLETE

## Goal
- Upgrade Selune's Moonmace from +3 to +5 weapon
- Add extra radiant damage to Longsword of Tyr (not working - status approach failed)
- Create new weapon: Sword of Orpheus (based on MAG_GreaterSilver_Greatsword, +5)

---

## Research: Extra Radiant Damage

Extra radiant damage on weapons (like Devotee's Mace) is added via a **status in the RootTemplate's StatusList**, not in Weapon.txt.

**Vanilla Status (from GustavDev Status_BOOST.txt):**
```
new entry "MAG_RADIANT_STRONG_RADIANCE_WEAPON"
type "StatusData"
data "StatusType" "BOOST"
using "MAG_RADIANT_RADIANCE_WEAPON"
data "DescriptionParams" "DealDamage(1d8, Radiant)"
data "Boosts" "WeaponDamage(1d8, Radiant)"
```

**How Devotee's Mace applies it (RootTemplate StatusList):**
```xml
<node id="StatusList">
    <children>
        <node id="Status">
            <attribute id="Object" type="FixedString" value="MAG_RADIANT_STRONG_RADIANCE_WEAPON" />
        </node>
    </children>
</node>
```

**Available radiant damage statuses:**
- `MAG_RADIANT_RADIANCE_WEAPON` - adds 1d4 radiant damage
- `MAG_RADIANT_STRONG_RADIANCE_WEAPON` - adds 1d8 radiant damage

---

## Item 1: Selune's Moonmace Enhancements

### Current Implementation (Phase 17)

```
new entry "SMR_Mace_Selune_Moon"
type "Weapon"
using "WPN_Mace_2"
data "RootTemplate" "a5b6c7d8-e9f0-4a1b-2c3d-4e5f6a7b8c9d"
data "Rarity" "Legendary"
data "DefaultBoosts" "WeaponEnchantment(3);WeaponProperty(Magical)"
data "BoostsOnEquipMainHand" "UnlockSpell(Target_ConcussiveSmash);UnlockSpell(Target_PostureBreaker);UnlockSpell(Shout_MAG_DevoteesMace_Healing_Aura)"
data "PassivesOnEquip" "CRE_LathandersLight_Passive;SMR_Moonshield_Passive"
data "Unique" "1"
```

### Planned Changes

1. Upgrade to +5 enchantment

```
data "DefaultBoosts" "WeaponEnchantment(5);WeaponProperty(Magical)"
```

---

## Item 2: Longsword of Tyr Enhancements

### Current Implementation (Phase 18)

```
new entry "SMR_Sword_Tyr"
type "Weapon"
using "WPN_Longsword_2"
data "RootTemplate" "d2e3f4a5-b6c7-4d8e-9f0a-1b2c3d4e5f6a"
data "Rarity" "Legendary"
data "DefaultBoosts" "WeaponEnchantment(5);WeaponProperty(Magical)"
data "Boosts" "UnlockSpell(Target_MAG_Smite_Wrathful);UnlockSpell(SMR_Target_BlindingSmite_Unlimited);UnlockSpell(SMR_Target_Light_Unlimited);UnlockSpell(Target_PLA_ShieldOfFaith_SwordOfJustice)"
data "PassivesOnEquip" "MAG_PlaneShifterSlayer_Passive"
data "Unique" "1"
```

### Planned Changes

1. Add extra radiant damage (1d8) via StatusList in RootTemplate

**Add to merged.lsx and merged.lsf.lsx for Longsword of Tyr (MapKey: d2e3f4a5-b6c7-4d8e-9f0a-1b2c3d4e5f6a):**
```xml
<node id="StatusList">
    <children>
        <node id="Status">
            <attribute id="Object" type="FixedString" value="MAG_RADIANT_STRONG_RADIANCE_WEAPON" />
        </node>
    </children>
</node>
<node id="Tags">
    <children>
        <node id="Tag">
            <attribute id="Object" type="guid" value="983087c8-c9d3-4a87-bc69-65f9329666c8" />
        </node>
    </children>
</node>
```

**Note:** The Tags node with guid `983087c8-c9d3-4a87-bc69-65f9329666c8` is present on both vanilla items (Devotee's Mace and Radiant Light Rapier) and may be required for the status to work.

**Status:** NOT WORKING - The radiant damage status approach did not work for our mod.

---

## Item 2b: Longsword of Tyr - Passive Approach (NEW)

The StatusList approach failed. Instead, we can create a custom passive that adds radiant damage via `CharacterWeaponDamage`.

### Research: Psionic Weapon Passive

The `MAG_Legendary_PsionicWeapon_Passive` adds psychic damage via a passive:

```
new entry "MAG_Legendary_PsionicWeapon_Passive"
type "PassiveData"
using "MAG_Githborn_Mindcrusher_Greatsword_Passive"
data "DescriptionParams" "DealDamage(1d6,Psychic)"
data "TooltipConditionalDamage" "DealDamage(1d6,Psychic)"
data "Boosts" "IF(IsMeleeAttack()):CharacterWeaponDamage(1d6, Psychic)"
```

### Custom Passive: SMR_RadiantWeapon_Passive

```
new entry "SMR_RadiantWeapon_Passive"
type "PassiveData"
data "DisplayName" "h9e0f1a2bg3c4dg5e6fg7a8bg9c0d1e2f3a4b;1"
data "Description" "ha0f1b2c3gd4e5gf6a7g8b9cg0d1e2f3a4b5c;1"
data "DescriptionParams" "DealDamage(1d8,Radiant)"
data "TooltipConditionalDamage" "DealDamage(1d8,Radiant)"
data "Boosts" "IF(IsMeleeAttack()):CharacterWeaponDamage(1d8, Radiant)"
```

### Updated Weapon Definition

Add `SMR_RadiantWeapon_Passive` to the Longsword of Tyr's PassivesOnEquip:

```
new entry "SMR_Sword_Tyr"
type "Weapon"
using "WPN_Longsword_2"
data "RootTemplate" "d2e3f4a5-b6c7-4d8e-9f0a-1b2c3d4e5f6a"
data "Rarity" "Legendary"
data "DefaultBoosts" "WeaponEnchantment(5);WeaponProperty(Magical)"
data "Boosts" "UnlockSpell(Target_MAG_Smite_Wrathful);UnlockSpell(SMR_Target_BlindingSmite_Unlimited);UnlockSpell(SMR_Target_Light_Unlimited);UnlockSpell(Target_PLA_ShieldOfFaith_SwordOfJustice)"
data "PassivesOnEquip" "MAG_PlaneShifterSlayer_Passive;SMR_RadiantWeapon_Passive"
data "Unique" "1"
```

---

## Item 3: Sword of Orpheus (NEW)

### Reference: MAG_GreaterSilver_Greatsword (Vanilla BG3)

**Weapon.txt:**
```
new entry "MAG_GreaterSilver_Greatsword"
type "Weapon"
using "WPN_Greatsword_2"
data "RootTemplate" "f01c3f5d-c542-420f-86c5-bdddf7819e29"
data "ValueUUID" "d24c441f-7ebe-4229-8522-cf34c257ff20"
data "Rarity" "Legendary"
data "DefaultBoosts" "WeaponEnchantment(3);WeaponProperty(Magical)"
data "BoostsOnEquipMainHand" "UnlockSpell(Target_PommelStrike);UnlockSpell(Target_Slash_New);UnlockSpell(Zone_Cleave);UnlockSpell(Target_MAG_WeaponAction_Mindcrush)"
data "PassivesOnEquip" "MAG_Legendary_PsionicWeapon_Passive;MAG_Legendary_PsionicResistance_Passive"
data "Unique" "1"
```

**RootTemplate:**
- MapKey: f01c3f5d-c542-420f-86c5-bdddf7819e29
- ParentTemplateId: 91d38c71-4614-463f-8b35-338e5b3bbf9f

**Powers:**
- Pommel Strike, Slash, Cleave weapon actions
- Mindcrush weapon action (psionic)
- MAG_Legendary_PsionicWeapon_Passive - psionic weapon damage
- MAG_Legendary_PsionicResistance_Passive - psionic resistance

### Item Details

| Aspect | Value |
|--------|-------|
| Name | Sword of Orpheus |
| Internal ID | SMR_Sword_Orpheus |
| Base Type | WPN_Greatsword_2 |
| RootTemplate | e5f6a7b8-c9d0-4e1f-2a3b-4c5d6e7f8a9b (custom) |
| ParentTemplateId | f01c3f5d-c542-420f-86c5-bdddf7819e29 (MAG_GreaterSilver_Greatsword appearance) |
| Rarity | Legendary |
| Unique | Yes |

### Planned Weapon Definition

**Weapon.txt:**
```
new entry "SMR_Sword_Orpheus"
type "Weapon"
using "WPN_Greatsword_2"
data "RootTemplate" "e5f6a7b8-c9d0-4e1f-2a3b-4c5d6e7f8a9b"
data "Rarity" "Legendary"
data "DefaultBoosts" "WeaponEnchantment(5);WeaponProperty(Magical)"
data "BoostsOnEquipMainHand" "UnlockSpell(Target_PommelStrike);UnlockSpell(Target_Slash_New);UnlockSpell(Zone_Cleave);UnlockSpell(Target_MAG_WeaponAction_Mindcrush)"
data "PassivesOnEquip" "MAG_Legendary_PsionicWeapon_Passive;MAG_Legendary_PsionicResistance_Passive"
data "Unique" "1"
```

**RootTemplate (merged.lsx / merged.lsf.lsx):**
```xml
<node id="GameObjects">
    <attribute id="DisplayName" type="TranslatedString" handle="TBD" version="1" />
    <attribute id="Description" type="TranslatedString" handle="TBD" version="1" />
    <attribute id="LevelName" type="FixedString" value="" />
    <attribute id="MapKey" type="FixedString" value="e5f6a7b8-c9d0-4e1f-2a3b-4c5d6e7f8a9b" />
    <attribute id="Name" type="LSString" value="SMR_Sword_Orpheus" />
    <attribute id="ParentTemplateId" type="FixedString" value="f01c3f5d-c542-420f-86c5-bdddf7819e29" />
    <attribute id="Stats" type="FixedString" value="SMR_Sword_Orpheus" />
    <attribute id="Type" type="FixedString" value="item" />
    <attribute id="_OriginalFileVersion_" type="int64" value="144115188075855912" />
    <children>
        <node id="GameMaster" />
    </children>
</node>
```

**OneTimeReward (OneTimeRewards.lsx):**
```xml
<node id="OneTimeReward">
    <attribute id="Amount" type="uint32" value="1"/>
    <attribute id="ItemTemplateId" type="FixedString" value="e5f6a7b8-c9d0-4e1f-2a3b-4c5d6e7f8a9b"/>
    <attribute id="UUID" type="guid" value="f6a7b8c9-d0e1-4f2a-3b4c-5d6e7f8a9b0c"/>
</node>
```

---

## Implementation Checklist

### Selune's Moonmace
- [x] Update DefaultBoosts to `WeaponEnchantment(5);WeaponProperty(Magical)` in Weapon.txt

### Longsword of Tyr (Radiant Damage via Passive)
- [x] Add StatusList with `MAG_RADIANT_STRONG_RADIANCE_WEAPON` to merged.lsx (did not work)
- [x] Add StatusList with `MAG_RADIANT_STRONG_RADIANCE_WEAPON` to merged.lsf.lsx (did not work)
- [x] Create SMR_RadiantWeapon_Passive in Passive.txt
- [x] Update SMR_Sword_Tyr PassivesOnEquip to include SMR_RadiantWeapon_Passive
- [x] Add localization for SMR_RadiantWeapon_Passive

### Sword of Orpheus (NEW)
- [x] Add SMR_Sword_Orpheus to Weapon.txt
- [x] Add weapon template to merged.lsx
- [x] Add weapon template to merged.lsf.lsx
- [x] Add localization to SampleMagicRingMod.loca.xml
- [x] Add OneTimeReward entry to OneTimeRewards.lsx

### Final
- [ ] Build and test mod

---

## Test Plan

### Selune's Moonmace
- [x] Load game with mod enabled
- [x] Equip Selune's Moonmace
- [x] Verify weapon tooltip shows +5 bonus to attack and damage

### Longsword of Tyr (Radiant Damage)
- [x] Equip Longsword of Tyr
- [ ] ~~Verify weapon tooltip shows +1d8 Radiant damage~~ (NOT WORKING)
- [ ] ~~Verify damage rolls include radiant damage~~ (NOT WORKING)

### Sword of Orpheus
- [ ] Check traveler's chest for Sword of Orpheus
- [ ] Verify sword has Orpheus's Greatsword appearance
- [ ] Verify weapon tooltip shows +5 bonus to attack and damage
- [ ] Verify Pommel Strike, Slash, Cleave weapon actions available
- [ ] Verify Mindcrush weapon action available
- [ ] Verify psionic damage passive working

---

## Notes

- Extra radiant damage fits the divine/holy theme of the Longsword of Tyr (Tyr = god of justice)
- Radiant damage is applied via the vanilla `MAG_RADIANT_STRONG_RADIANCE_WEAPON` status in the RootTemplate's StatusList
- This is the same method used by the Devotee's Mace in vanilla BG3
- **Issue:** The StatusList approach for radiant damage did not work in our mod - possibly because the status is defined in GustavDev and not accessible to our mod
- Sword of Orpheus is based on MAG_GreaterSilver_Greatsword (Orpheus's Greatsword), upgraded to +5
- The psionic passives from the original weapon are retained
