# Phase 024 - Circlet of Willpower + Reverberation Move

**Status:** COMPLETE

## Goal
- Create a new circlet based on the Circlet of Tyr but without Speak with Animals and Speak with Dead
- Use the MAG_BarbMonk_Leather_Circlet appearance
- Not unique - provide 8 copies for party use
- Move Reverberation passive from Staff of Akitaro to Magus Circlet

---

## Item: Circlet of Willpower

### Item Details

| Aspect | Value |
|--------|-------|
| Name | Circlet of Willpower |
| Internal ID | SMR_Circlet_Willpower |
| Base Type | _Head_Magic_Circlet |
| ParentTemplateId | 48920bf4-85b0-44a1-9f6a-0ad8b493fa47 (MAG_BarbMonk_Leather_Circlet) |
| Rarity | Legendary |
| Unique | No |
| Quantity in Chest | 8 |

### Powers (Same as Circlet of Tyr, minus Speak with Dead/Animals)

| Power | Source | Effect |
|-------|--------|--------|
| Critical Hit Immunity | Boosts | CriticalHit(AttackTarget,Success,Never) |
| See Invisibility | SMR_Shout_SeeInvisibility_Unlimited | Unlimited See Invisibility |
| Protection from Evil and Good | SMR_Target_ProtectionFromEvilAndGood_Unlimited | Unlimited Protection from Evil and Good |
| Faerie Fire | SMR_Target_FaerieFire_ShortRest | Faerie Fire (short rest recharge) |
| Balduran's Vitality | MAG_HelmOfBalduran_MaxHP_Passive | +2 Max HP |
| Balduran's Protection | MAG_HelmOfBalduran_Protection_Passive | +1 to AC and Saving Throws |
| Stun Immunity | MAG_StunnImmunity_Passive | Immune to Stunned condition |
| Fear Immunity | MAG_LC_Cyric_FearImmunity_Amulet_Passive | Immune to Frightened condition |
| Blind Immunity | MAG_Shadow_BlindImmunity_Ring_Passive | Immune to Blinded condition |
| Darkvision | UND_SocietyOfBrilliance_DarkvisionRing_Passive | Grants Darkvision |
| HP Regeneration | MAG_HELM_OF_BALDURAN_REGENERATION | Regain 2 HP at start of each turn in combat |

### Removed from Circlet of Tyr

| Power | Reason |
|-------|--------|
| Speak with Dead | Removed per request |
| Speak with Animals | Removed per request |

---

## Task 2: Move Reverberation from Staff of Akitaro to Magus Circlet

### Overview

Move the `MAG_Thunder_Reverberation_Gloves_Passive` from Staff of Akitaro to Magus Circlet. This passive applies the Reverberation debuff when dealing Thunder, Lightning, or Radiant damage.

### Reverberation Effect

| Stacks | Effect |
|--------|--------|
| Per Stack | -1 to STR, DEX, CON saving throws |
| At 5 Stacks | Deals 1d4 Thunder damage, removes all stacks |
| At 5 Stacks | Target must make CON DC 10 save or be knocked Prone |

### Staff of Akitaro Changes

**Current PassivesOnEquip:**
```
MAG_CQCaster_GainArcaneChargeOnDamage_Quarterstaff_Passive;MAG_ArcaneEnchantment_Lesser_Passive;MAG_Legendary_Chromatic_Spellslot_Passive;WW_Mystra_SpellAttkBonus_Passive;WW_Mystra_Passive;WW_Netherese_Staff_Passive;Absorb_Elements_Passive;MAG_MagicalDurability_Passive;MAG_Radiant_RadiatingOrb_Ring_Passive;MAG_Thunder_Reverberation_Gloves_Passive;MAG_Gish_ArcaneAcuity_Gloves_Passive;MAG_Radiant_DamageBonusOnIlluminatedTarget_Ring_Passive;CRE_LathandersLight_Passive
```

**New PassivesOnEquip (remove MAG_Thunder_Reverberation_Gloves_Passive):**
```
MAG_CQCaster_GainArcaneChargeOnDamage_Quarterstaff_Passive;MAG_ArcaneEnchantment_Lesser_Passive;MAG_Legendary_Chromatic_Spellslot_Passive;WW_Mystra_SpellAttkBonus_Passive;WW_Mystra_Passive;WW_Netherese_Staff_Passive;Absorb_Elements_Passive;MAG_MagicalDurability_Passive;MAG_Radiant_RadiatingOrb_Ring_Passive;MAG_Gish_ArcaneAcuity_Gloves_Passive;MAG_Radiant_DamageBonusOnIlluminatedTarget_Ring_Passive;CRE_LathandersLight_Passive
```

### Magus Circlet Changes

**Current PassivesOnEquip:**
```
MAG_LC_Cyric_FearImmunity_Amulet_Passive;MAG_Shadow_BlindImmunity_Ring_Passive;UND_SocietyOfBrilliance_DarkvisionRing_Passive
```

**New PassivesOnEquip (add MAG_Thunder_Reverberation_Gloves_Passive):**
```
MAG_LC_Cyric_FearImmunity_Amulet_Passive;MAG_Shadow_BlindImmunity_Ring_Passive;UND_SocietyOfBrilliance_DarkvisionRing_Passive;MAG_Thunder_Reverberation_Gloves_Passive
```

---

## Task 3: Make Moonguard Blade Non-Unique

### Overview

Make the Moonguard Blade non-unique and provide 2 copies in the Traveler's Chest for dual-wielding.

### Changes Required

| File | Change |
|------|--------|
| Weapon.txt | Remove `data "Unique" "1"` from SMR_Blade_Moonguard |
| OneTimeRewards.lsx | Change Amount from 1 to 2 for ItemTemplateId `a1b2c3d4-e5f6-4a7b-8c9d-1e2f3a4b5c6d` |

---

## UUIDs and Handles

### Circlet of Willpower
| Type | Value |
|------|-------|
| MapKey/RootTemplate | d1e2f3a4-b5c6-4d7e-8f9a-0b1c2d3e4f5a |
| DisplayName Handle | h5f6a7b8cg9d0eg1f2ag3b4cg5d6e7f8a9b0c1d |
| Description Handle | h2b3c4d5eg6f7ag8b9cg0d1eg2f3a4b5c6d7e8 |
| OneTimeReward UUID | e2f3a4b5-c6d7-4e8f-9a0b-1c2d3e4f5a6b |

---

## Implementation Details

### Armor.txt Entry
```
new entry "SMR_Circlet_Willpower"
type "Armor"
using "_Head_Magic_Circlet"
data "RootTemplate" "d1e2f3a4-b5c6-4d7e-8f9a-0b1c2d3e4f5a"
data "Rarity" "Legendary"
data "Boosts" "CriticalHit(AttackTarget,Success,Never);UnlockSpell(SMR_Shout_SeeInvisibility_Unlimited);UnlockSpell(SMR_Target_ProtectionFromEvilAndGood_Unlimited);UnlockSpell(SMR_Target_FaerieFire_ShortRest)"
data "PassivesOnEquip" "MAG_HelmOfBalduran_MaxHP_Passive;MAG_HelmOfBalduran_Protection_Passive;MAG_StunnImmunity_Passive;MAG_LC_Cyric_FearImmunity_Amulet_Passive;MAG_Shadow_BlindImmunity_Ring_Passive;UND_SocietyOfBrilliance_DarkvisionRing_Passive"
data "StatusOnEquip" "MAG_HELM_OF_BALDURAN_REGENERATION"
```

### RootTemplate Entry (merged.lsx and merged.lsf.lsx)
```xml
<node id="GameObjects">
    <attribute id="DisplayName" type="TranslatedString" handle="h5f6a7b8cg9d0eg1f2ag3b4cg5d6e7f8a9b0c1d" version="1" />
    <attribute id="LevelName" type="FixedString" value="" />
    <attribute id="MapKey" type="FixedString" value="d1e2f3a4-b5c6-4d7e-8f9a-0b1c2d3e4f5a" />
    <attribute id="Name" type="LSString" value="SMR_Circlet_Willpower" />
    <attribute id="ParentTemplateId" type="FixedString" value="48920bf4-85b0-44a1-9f6a-0ad8b493fa47" />
    <attribute id="Stats" type="FixedString" value="SMR_Circlet_Willpower" />
    <attribute id="Type" type="FixedString" value="item" />
    <attribute id="_OriginalFileVersion_" type="int64" value="144115188075855912" />
</node>
```

### Localization Entries (SampleMagicRingMod.loca.xml and .xml)
```xml
<content contentuid="h5f6a7b8cg9d0eg1f2ag3b4cg5d6e7f8a9b0c1d" version="1">Circlet of Willpower</content>
<content contentuid="h2b3c4d5eg6f7ag8b9cg0d1eg2f3a4b5c6d7e8" version="1">A circlet that fortifies the mind and body. Grants Critical Hit Immunity, Stun/Fear/Blind Immunity, HP Regeneration, Darkvision, and the spells See Invisibility, Protection From Evil And Good, and Faerie Fire.</content>
```

### OneTimeReward Entry (8 copies)
```xml
<node id="OneTimeReward">
    <attribute id="Amount" type="uint32" value="8"/>
    <attribute id="ItemTemplateId" type="FixedString" value="d1e2f3a4-b5c6-4d7e-8f9a-0b1c2d3e4f5a"/>
    <attribute id="UUID" type="guid" value="e2f3a4b5-c6d7-4e8f-9a0b-1c2d3e4f5a6b"/>
</node>
```

---

## Implementation Checklist

### Circlet of Willpower
- [x] Add SMR_Circlet_Willpower to Armor.txt
- [x] Add RootTemplate to merged.lsx
- [x] Add RootTemplate to merged.lsf.lsx
- [x] Add localization entries to SampleMagicRingMod.xml
- [x] Add localization entries to SampleMagicRingMod.loca.xml
- [x] Add OneTimeReward entry (Amount: 8)

### Reverberation Move
- [x] Remove MAG_Thunder_Reverberation_Gloves_Passive from SMR_Staff_Akitaro in Weapon.txt
- [x] Add MAG_Thunder_Reverberation_Gloves_Passive to SMR_Circlet_Magus in Armor.txt

### Moonguard Blade Non-Unique
- [x] Remove `data "Unique" "1"` from SMR_Blade_Moonguard in Weapon.txt
- [x] Change Amount from 1 to 2 in OneTimeRewards.lsx

### Final
- [ ] Build and test mod

---

## Test Plan

### Circlet of Willpower
- [ ] Check traveler's chest for 8x Circlet of Willpower
- [ ] Verify circlet has MAG_BarbMonk_Leather_Circlet appearance
- [ ] Verify Critical Hit Immunity works
- [ ] Verify Stun/Fear/Blind Immunity works
- [ ] Verify HP Regeneration (2 HP/turn in combat)
- [ ] Verify Darkvision is granted
- [ ] Verify See Invisibility spell (unlimited)
- [ ] Verify Protection from Evil and Good spell (unlimited)
- [ ] Verify Faerie Fire spell (short rest recharge)
- [ ] Verify Speak with Dead is NOT present
- [ ] Verify Speak with Animals is NOT present

### Reverberation Move
- [ ] Verify Staff of Akitaro does NOT apply Reverberation on Thunder/Lightning/Radiant damage
- [ ] Verify Magus Circlet DOES apply Reverberation on Thunder/Lightning/Radiant damage
- [ ] Test Reverberation stacking and 5-stack explosion effect with Magus Circlet equipped

### Moonguard Blade Non-Unique
- [ ] Check traveler's chest for 2x Moonguard Blade
- [ ] Verify both can be equipped (dual-wielded)

---

## Known Issues

- ~~**BUG: Handle Collision** - The DisplayName handle `h1a2b3c4dg5e6fg7a8bg9c0dg1e2f3a4b5c6d7` was accidentally reused for Circlet of Willpower, but it was already used by Mantle of Tyr (Cloak of Tyr). This causes the Cloak of Tyr to display as "Circlet of Willpower" in-game.~~ **RESOLVED** - Changed Circlet of Willpower DisplayName handle to `h5f6a7b8cg9d0eg1f2ag3b4cg5d6e7f8a9b0c1d`

- ~~**BUG (Phase 23): Invalid UUID** - The Cloak of the Rogue MapKey UUID `c3d4e5f6-a7b8-4c9d-0e1f-2a3b4c5d6e7g` is invalid because it contains "g" which is not a valid hexadecimal character. UUIDs can only contain 0-9 and a-f. This causes the item to not appear in-game.~~ **RESOLVED** - Changed to valid UUID `c3d4e5f6-a7b8-4c9d-0e1f-2a3b4c5d6e70`

- ~~**BUG: Staff of Akitaro UUID Conflict** - The Staff of Akitaro UUID `f1a2b3c4-d5e6-4f7a-8b9c-0d1e2f3a4b5c` may conflict with something in the base game, causing the item to disappear from the chest.~~ **RESOLVED** - Changed to UUID `535f3b19-38d5-4898-a68d-687a73d85ed4`

---

## Notes

- Circlet of Willpower is designed for party-wide distribution (8 copies)
- Removed Speak with Dead and Speak with Animals to streamline the item
- Uses leather circlet appearance (MAG_BarbMonk_Leather_Circlet) for a different aesthetic than the metal Circlet of Tyr
- Moving Reverberation to Magus Circlet makes it a head slot power, freeing up Staff of Akitaro's passive list
- Reverberation synergizes with Thunder/Lightning/Radiant damage spells - good fit for a caster circlet
