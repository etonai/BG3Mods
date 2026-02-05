# Phase 017 - Selune's Moonmace

**Status:** COMPLETE

## Goal
Create a new legendary mace called "Selune's Moonmace" based on the vanilla Devotee's Mace, with additional moon/light-themed powers.

---

## Reference: Devotee's Mace (Vanilla BG3)

The base item for this weapon.

**Item Details:**
- MapKey: f8578a13-a857-4043-91e4-8101c9e7c004
- Internal ID: MAG_Cleric_Devotees_Mace
- Base Type: WPN_Mace_2

**Current Implementation (Weapon.txt):**
```
new entry "MAG_Cleric_Devotees_Mace"
type "Weapon"
using "WPN_Mace_2"
data "RootTemplate" "f8578a13-a857-4043-91e4-8101c9e7c004"
data "ValueUUID" "d24c441f-7ebe-4229-8522-cf34c257ff20"
data "ValueOverride" "0"
data "Rarity" "Legendary"
data "DefaultBoosts" "WeaponEnchantment(3);WeaponProperty(Magical)"
data "BoostsOnEquipMainHand" "UnlockSpell(Target_ConcussiveSmash);UnlockSpell(Target_PostureBreaker);UnlockSpell(Shout_MAG_DevoteesMace_Healing_Aura)"
data "Unique" "1"
```

**Devotee's Mace Powers:**
| Power | Type | Description |
|-------|------|-------------|
| Concussive Smash | Weapon Action | Melee attack that can Daze target |
| Posture Breaker | Weapon Action | Melee attack that reduces target's AC |
| Healing Incense Aura | Shout (Once per Long Rest) | 9m aura that heals allies 1d4 HP at start of each turn for 10 turns |

---

## Item Details

| Aspect | Value |
|--------|-------|
| Name | Selune's Moonmace |
| Internal ID | SMR_Mace_Selune_Moon |
| Base Type | WPN_Mace_2 |
| RootTemplate | a5b6c7d8-e9f0-4a1b-2c3d-4e5f6a7b8c9d (custom, uses Devotee's Mace as ParentTemplateId) |
| ParentTemplateId | f8578a13-a857-4043-91e4-8101c9e7c004 (Devotee's Mace appearance) |
| Rarity | Legendary |
| Unique | Yes |

---

## Powers

### Base Weapon Properties
| Property | Value |
|----------|-------|
| Weapon Enchantment | +3 |
| Magical | Yes |

### Weapon Actions (from Devotee's Mace)
| Power | Description | Source |
|-------|-------------|--------|
| Concussive Smash | Melee attack that can Daze target | Target_ConcussiveSmash (vanilla) |
| Posture Breaker | Melee attack that reduces target's AC | Target_PostureBreaker (vanilla) |

### Spells
| Status | Power | Description | Source |
|--------|-------|-------------|--------|
| [x] | **Healing Incense Aura** | 9m healing aura (1d4 HP/turn for 10 turns), once per long rest | Shout_MAG_DevoteesMace_Healing_Aura (vanilla) |

### Passive Abilities
| Status | Passive | Description | Source |
|--------|---------|-------------|--------|
| [x] | **Lathander's Light** | Toggled 6m aura that blinds Fiends/Undead (CON 14 save), emits light | CRE_LathandersLight_Passive (vanilla, from Blood of Lathander) |
| [x] | **Moonshield Aura** | Toggled 13m aura that grants Shadow Curse immunity to nearby allies, emits light | SMR_Moonshield_Passive (custom, using SCL_MOONSHIELD_AURA status) |

---

## Custom Passive: SMR_Moonshield_Passive

A toggled passive that applies the Moonshield aura. Based on the example from interesting_magical_effects.md.

### Passive Definition (Passive.txt)
```
new entry "SMR_Moonshield_Passive"
type "PassiveData"
data "Properties" "ToggledDefaultOn;ToggledDefaultAddToHotbar;IsToggled"
data "DisplayName" "hd6bd135bg4531g4124g9e22gfb187fe3b715;1"
data "ToggleOnFunctors" "ApplyStatus(SCL_MOONSHIELD_AURA, 100, -1)"
data "ToggleOffFunctors" "RemoveStatus(SCL_MOONSHIELD_AURA)"
```

**Notes:**
- Uses the vanilla SCL_MOONSHIELD_AURA status (13m radius, grants Shadow Curse immunity)
- ToggledDefaultOn means the aura is active when the weapon is equipped
- ToggledDefaultAddToHotbar adds a toggle button to the hotbar
- Uses vanilla DisplayName handle for "Moonshield" (may need custom localization)

---

## Planned Weapon Definition

### Weapon.txt Entry
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

### OneTimeReward Entry (OneTimeRewards.lsx)
```xml
<node id="OneTimeReward">
    <attribute id="Amount" type="uint32" value="1"/>
    <attribute id="ItemTemplateId" type="FixedString" value="a5b6c7d8-e9f0-4a1b-2c3d-4e5f6a7b8c9d"/>
    <attribute id="UUID" type="guid" value="b6c7d8e9-f0a1-4b2c-3d4e-5f6a7b8c9d0e"/>
</node>
```

---

## Implementation Checklist

### Weapon Definition
- [x] Add SMR_Mace_Selune_Moon to Weapon.txt
- [x] Add weapon template to merged.lsx (RootTemplate: a5b6c7d8-e9f0-4a1b-2c3d-4e5f6a7b8c9d, ParentTemplateId: f8578a13-a857-4043-91e4-8101c9e7c004)
- [x] Add weapon template to merged.lsf.lsx

### Localization
- [x] Add localization to SampleMagicRingMod.xml
- [x] Add localization to SampleMagicRingMod.loca.xml

### Delivery (Traveler's Chest)
- [x] Add OneTimeReward entry to OneTimeRewards.lsx (ItemTemplateId: a5b6c7d8-e9f0-4a1b-2c3d-4e5f6a7b8c9d, UUID: b6c7d8e9-f0a1-4b2c-3d4e-5f6a7b8c9d0e)

### Custom Passives
- [x] Add SMR_Moonshield_Passive to Passive.txt

### Final
- [x] Build and test mod

---

## Test Plan

### Selune's Moonmace
- [ ] Load game with mod enabled
- [ ] Check traveler's chest for Selune's Moonmace
- [ ] Equip mace and verify +3 enchantment
- [ ] Verify Concussive Smash weapon action is available
- [ ] Verify Posture Breaker weapon action is available
- [ ] Verify Healing Incense Aura spell is available
- [ ] Cast Healing Incense Aura and verify 9m healing aura effect

### Lathander's Light
- [ ] Verify Lathander's Light toggle appears on hotbar when mace equipped
- [ ] Verify 6m light aura is emitted when toggled on
- [ ] Test against Fiends/Undead - verify they are blinded (CON 14 save)
- [ ] Verify toggle can be turned off to disable the aura

### Moonshield Aura
- [ ] Verify Moonshield toggle appears on hotbar when mace equipped
- [ ] Verify 13m light aura is emitted when toggled on
- [ ] Verify nearby allies receive Shadow Curse immunity (SCL_MOONSHIELD status)
- [ ] Test in Shadow Cursed Lands - verify protection from curse
- [ ] Verify toggle can be turned off to disable the aura

---

## Notes

- Uses the Devotee's Mace appearance (RootTemplate from vanilla Devotee's Mace)
- Thematic focus: Moon/light abilities befitting Selune, goddess of the moon
- **Lathander's Light**: Borrowed from Blood of Lathander - vanilla passive, no custom code needed
- **Moonshield Aura**: Uses vanilla SCL_MOONSHIELD_AURA status, but requires custom toggled passive (SMR_Moonshield_Passive)
- Both auras emit gameplay light, fitting the moon/light theme
- The mace effectively combines healing (Devotee's Mace), anti-undead (Lathander's Light), and protection (Moonshield) abilities
