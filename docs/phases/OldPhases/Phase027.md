# Phase 027 - Armor of Voss

**Status:** ABANDONED

## Goal
Create the Armor of Voss, a legendary chain armor based on the Elven Chain appearance with the powers of the Moonguard Splint.

---

## Item Details

### Armor of Voss
| Aspect | Value |
|--------|-------|
| Internal ID | SMR_Armor_Voss |
| Base Type | ARM_ChainShirt_Body_1 (Chain Shirt, Light Armor) |
| Visual Source | MAG_PHB_ElvenChain_Armor |
| Rarity | Legendary |
| Boosts | AC(5), +2 Saving Throws, no Dex cap |
| Spells | Celestial Haste (unlimited), Misty Step (unlimited), Spirit Guardians |
| Passives | Exotic Material, Combat Regeneration (1d4 HP/turn) |

**Powers Summary (from Moonguard Splint):**
- +5 AC bonus (Chain Shirt base + AC(5) boost)
- +2 to all Saving Throws
- No Dexterity modifier cap
- Celestial Haste (unlimited)
- Misty Step (unlimited)
- Spirit Guardians
- Exotic Material (no Stealth disadvantage for light armor)
- Combat Regeneration (regain 1d4 HP at start of each turn in combat)

---

## Implementation Checklist

### For the Item
- [x] Generate new UUIDs (MapKey, handles)
- [x] Add stats entry (Armor.txt)
- [x] Add RootTemplate to merged.lsx
- [x] Add localization entries
- [x] Add OneTimeReward entry

### Final
- [x] Update item_catalog.md
- [ ] Build and test mod

---

## Test Plan

- [ ] Check traveler's chest for Armor of Voss
- [ ] Verify item has correct name and description
- [ ] Verify Elven Chain appearance
- [ ] Verify all powers work correctly:
  - [ ] AC bonus (+5 total)
  - [ ] Saving throw bonus (+2)
  - [ ] No Dex cap applied
  - [ ] Celestial Haste casts without spell slot
  - [ ] Misty Step casts without spell slot
  - [ ] Spirit Guardians available
  - [ ] No Stealth disadvantage
  - [ ] Combat regen triggers each turn

---

## Implementation Details

### UUIDs (MapKey)
| Item | MapKey |
|------|--------|
| Armor of Voss | c8d9e0f1-a2b3-4c5d-6e7f-8a9b0c1d2e3f |

### Localization Handles
| Item | DisplayName Handle | Description Handle |
|------|-------------------|-------------------|
| Armor of Voss | h9e0f1a2bg3c4dg5e6fg7a8bg0c1d2e3f4a5b6 | h8d9e0f1ag2b3cg4d5eg6f7ag9b0c1d2e3f4a5 |

---

## Stats Entry (Armor.txt)

```
new entry "SMR_Armor_Voss"
type "Armor"
using "ARM_ChainShirt_Body_1"
data "RootTemplate" "c8d9e0f1-a2b3-4c5d-6e7f-8a9b0c1d2e3f"
data "Rarity" "Legendary"
data "Boosts" "AC(5);RollBonus(SavingThrow, 2);UnlockSpell(SMR_Shout_CelestialHaste_Unlimited);UnlockSpell(SMR_Target_MistyStep_Unlimited);UnlockSpell(SMR_Shout_SpiritGuardians_Tyr,AddChildren,,,SpellCastingAbility)"
data "PassivesOnEquip" "MAG_ExoticMaterial_MediumArmor_Passive;MAG_PHB_OfRegeneration_Ring_Passive"
data "StatusOnEquip" "MAG_EXOTIC_MATERIAL_ARMOR_TECHNICAL;MAG_PHB_RING_OF_REGENERATION_TECHNICAL"
data "Ability Modifier Cap" ""
data "Unique" "1"
```

---

## RootTemplate Entry (merged.lsx)

```xml
<node id="GameObjects">
    <attribute id="Description" type="TranslatedString" handle="h8d9e0f1ag2b3cg4d5eg6f7ag9b0c1d2e3f4a5" version="1" />
    <attribute id="DisplayName" type="TranslatedString" handle="h9e0f1a2bg3c4dg5e6fg7a8bg0c1d2e3f4a5b6" version="1" />
    <attribute id="Icon" type="FixedString" value="Generated_MAG_PHB_ElvenChain_Armor_Magic" />
    <attribute id="LevelName" type="FixedString" value="" />
    <attribute id="MapKey" type="FixedString" value="c8d9e0f1-a2b3-4c5d-6e7f-8a9b0c1d2e3f" />
    <attribute id="Name" type="LSString" value="SMR_Armor_Voss" />
    <attribute id="ParentTemplateId" type="FixedString" value="eac652ed-ecf7-4505-bf64-0fec29e7d677" />
    <attribute id="Stats" type="FixedString" value="SMR_Armor_Voss" />
    <attribute id="Type" type="FixedString" value="item" />
    <attribute id="VisualTemplate" type="FixedString" value="ac0b0670-d6e9-c806-4b77-2e4cb8599a5e" />
</node>
```

---

## Localization Entry (SampleMagicRingMod.loca.xml)

```xml
<content contentuid="h9e0f1a2bg3c4dg5e6fg7a8bg0c1d2e3f4a5b6" version="1">Armor of Voss</content>
<content contentuid="h8d9e0f1ag2b3cg4d5eg6f7ag9b0c1d2e3f4a5" version="1">This exquisite elven chain was forged for Kith'rak Voss, a legendary Githyanki warrior. The armor flows like liquid silver, providing exceptional protection while allowing complete freedom of movement. It grants powerful defensive magics and the ability to regenerate wounds in combat.</content>
```

---

## OneTimeReward Entry (OneTimeRewards.lsx)

```xml
<node id="Rewards">
    <attribute id="RewardId" type="guid" value="c8d9e0f1-a2b3-4c5d-6e7f-8a9b0c1d2e3f" />
    <children>
        <node id="Reward">
            <attribute id="Amount" type="int32" value="1" />
            <attribute id="TemplateId" type="guid" value="c8d9e0f1-a2b3-4c5d-6e7f-8a9b0c1d2e3f" />
            <attribute id="TreasureId" type="FixedString" value="" />
        </node>
    </children>
</node>
```

---

## Reference Items

| Item | Location | Purpose |
|------|----------|---------|
| MAG_PHB_ElvenChain_Armor | gustav | Visual appearance source |
| SMR_Armor_Moonguard | SampleMagicRingMod | Powers source |

---

## Notes

- Armor of Voss uses the Elven Chain appearance (light armor look)
- Powers are identical to Moonguard Splint
- Named after Kith'rak Voss, a Githyanki character in BG3
- Uses Chain Shirt base type (light armor) for proficiency
