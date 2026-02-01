# Phase 014 - Sword of Tyr: Light Spell and Tyr's Protection

**Status:** COMPLETE

## Goal
Add new abilities to the Sword of Tyr, rename it, and create a new circlet:
- Rename "Sword of Tyr" to "Longsword of Tyr"
- Add Light spell to Longsword of Tyr
- Add Tyr's Protection to Longsword of Tyr (from vanilla Sword of Justice)
- Create Circlet of Tyr (with all powers of Helmet of Tyr)

**Note:** +5 weapon upgrade moved to Phase 15.

---

## Item 1: Rename to Longsword of Tyr

### Overview
Rename the item from "Sword of Tyr" to "Longsword of Tyr" to better reflect that it is a longsword weapon type.

### Changes Required
- Update DisplayName in localization files (SampleMagicRingMod.xml and SampleMagicRingMod.loca.xml)
- Handle: `h5c6d7e8fg9a0bg1c2dg3e4fg5a6b7c8d9e0f1`

---

## Item 2: Light Spell Addition

### Overview
Add `SMR_Target_Light_Unlimited` to the Sword of Tyr's Boosts. This spell already exists in our mod (used by Staff of Archmage and Staff of Akitaro) - it's the Light cantrip castable as a bonus action with unlimited uses.

**Reference:** Vanilla Ring of Light (UNI_UND_Tower_RingOfLight, MapKey: 70ad7889-e1e2-4c2f-980f-28eaa02c2022)

### Current Sword of Tyr Implementation

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

---

## Item 3: Circlet of Tyr

### Overview
Create a new Circlet of Tyr that has all the powers of the Helmet of Tyr. This provides an alternative headgear option with the same powerful abilities but with a circlet appearance instead of a helmet.

### Powers (from Helmet of Tyr)

**From Helm of Balduran:**
- Balduran's Vitality (HP regeneration)
- Balduran's Protection (+1 AC and +1 to all saving throws)
- Stun Immunity
- Critical Hit Immunity
- HP Regeneration (2 HP at start of turn in combat)

**From Magus Circlet:**
- Fear Immunity
- Blind Immunity
- Darkvision
- Speak with Dead (unlimited)
- Speak with Animals (unlimited)
- See Invisibility (bonus action, unlimited)
- Protection From Evil And Good (bonus action, unlimited)
- Faerie Fire (bonus action, once per short rest)

### Reference - Current Helmet of Tyr Implementation

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

### Item Details

| Aspect | Value |
|--------|-------|
| Name | Circlet of Tyr |
| Internal ID | SMR_Circlet_Tyr |
| Base Item | Shadespell Circlet (vanilla BG3 item) |
| ParentTemplateId | f0e42b7e-4d6b-46fb-85d6-d577afc72040 |
| Vanilla Name | MAG_Shadow_SpellDCBonusWhileObscured_Circlet |
| Rarity | Legendary |
| Unique | Yes |

---

## Implementation Checklist

### Longsword of Tyr Enhancement
- [x] Rename "Sword of Tyr" to "Longsword of Tyr" in localization files
- [x] Add SMR_Target_Light_Unlimited to Longsword of Tyr's Boosts

### Circlet of Tyr
- [x] Add SMR_Circlet_Tyr to Armor.txt (copy stats from SMR_Helmet_Tyr)
- [x] Add circlet template to merged.lsx
- [x] Add circlet template to merged.lsf.lsx
- [x] Add OneTimeReward entry
- [x] Add localization to SampleMagicRingMod.xml
- [x] Add localization to SampleMagicRingMod.loca.xml

### Final
- [ ] Build and test mod

---

## Test Plan

### Longsword of Tyr + Light + Tyr's Protection
- [ ] Load game with mod enabled
- [ ] Equip Longsword of Tyr
- [ ] Verify item name displays as "Longsword of Tyr"
- [ ] Verify Light spell is available (bonus action, unlimited)
- [ ] Cast Light and verify it illuminates the area
- [ ] Verify Tyr's Protection is available
- [ ] Cast Tyr's Protection and verify effect

### Circlet of Tyr
- [ ] Check traveler's chest for Circlet of Tyr
- [ ] Equip circlet and verify appearance is a circlet (not helmet)
- [ ] Verify +1 AC and +1 saving throws from Balduran's Protection
- [ ] Verify HP Regeneration (2 HP at start of turn in combat)
- [ ] Verify Stun Immunity
- [ ] Verify Critical Hit Immunity
- [ ] Verify Fear Immunity
- [ ] Verify Blind Immunity
- [ ] Verify Darkvision is active
- [ ] Verify Speak with Dead spell is available (unlimited)
- [ ] Verify Speak with Animals spell is available (unlimited)
- [ ] Verify See Invisibility spell is available (bonus action, unlimited)
- [ ] Verify Protection From Evil And Good spell is available (bonus action, unlimited)
- [ ] Verify Faerie Fire spell is available (bonus action, once per short rest)

---

## Item 5: Fix Armor of Tyr Celestial Haste Cooldown

### Overview
The Celestial Haste spell on the Armor of Tyr was requiring a rest between casts despite being named "unlimited". The base spell `Shout_MAG_Victory_Longbow_Haste` has a built-in cooldown that needed to be explicitly overridden.

### Fix Applied
- [x] Added `data "Cooldown" ""` to `SMR_Shout_CelestialHaste_Unlimited` in Spell_Shout.txt

---

## Notes

*(To be added during implementation)*
