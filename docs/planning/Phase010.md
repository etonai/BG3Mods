# Phase 010 - Staff of Akitaro

**Status:** COMPLETE

## Goal
Create a new legendary staff called "Staff of Akitaro" with Spellsparkler powers plus additional magic.

---

## Item Overview

| Aspect | Value |
|--------|-------|
| Name | Staff of Akitaro |
| Internal ID | SMR_Staff_Akitaro |
| Base Type | WPN_Quarterstaff_1 |
| Appearance | Spellsparkler visual |
| Rarity | Legendary |
| Unique | Yes |

### Powers

| Power | Description | Source |
|-------|-------------|--------|
| **Arcane Charge on Damage** | Gain 2 Lightning Charges when dealing damage with a spell while at close range | MAG_CQCaster_GainArcaneChargeOnDamage_Quarterstaff_Passive (Spellsparkler) |
| **Light** | Cast Light (unlimited, bonus action) | SMR_Target_Light_Unlimited (existing) |
| **Counterspell** | Cast Counterspell as a reaction (unlimited) | SMR_Interrupt_Counterspell_Unlimited (existing) |
| **Celestial Haste** | Cast Haste on self (unlimited, bonus action) | SMR_Shout_CelestialHaste_Unlimited (new) |

---

## UUIDs and Handles

Generate these before implementation:

| Item | Type | Value |
|------|------|-------|
| Staff MapKey | UUID | `f1a2b3c4-d5e6-4f7a-8b9c-0d1e2f3a4b5c` |
| OneTimeReward | UUID | `a2b3c4d5-e6f7-4a8b-9c0d-1e2f3a4b5c6d` |
| DisplayName | Handle | `h5a6b7c8dge9f0g1a2bg3c4dg5e6f7a8b9c0d` |
| Description | Handle | `h6b7c8d9egf0a1g2b3cg4d5eg6f7a8b9c0d1e` |

---

## Implementation Steps

### Step 1: Add Celestial Haste Spell to Spell_Shout.txt

```
new entry "SMR_Shout_CelestialHaste_Unlimited"
type "SpellData"
data "SpellType" "Shout"
using "Shout_MAG_Victory_Longbow_Haste"
data "UseCosts" "BonusActionPoint:1"
```

### Step 2: Add Staff Stats to Weapon.txt

```
new entry "SMR_Staff_Akitaro"
type "Weapon"
using "WPN_Quarterstaff_1"
data "RootTemplate" "f1a2b3c4-d5e6-4f7a-8b9c-0d1e2f3a4b5c"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(SMR_Target_Light_Unlimited);UnlockInterrupt(SMR_Interrupt_Counterspell_Unlimited);UnlockSpell(SMR_Shout_CelestialHaste_Unlimited)"
data "PassivesOnEquip" "MAG_CQCaster_GainArcaneChargeOnDamage_Quarterstaff_Passive"
data "Unique" "1"
```

### Step 3: Add Staff Template to merged.lsx

Add after the Magus Circlet entry:
```xml
<node id="GameObjects"> Staff of Akitaro
    <attribute id="Description" type="TranslatedString" handle="h6b7c8d9egf0a1g2b3cg4d5eg6f7a8b9c0d1e" version="1" />
    <attribute id="DisplayName" type="TranslatedString" handle="h5a6b7c8dge9f0g1a2bg3c4dg5e6f7a8b9c0d" version="1" />
    <attribute id="ExamineRotation" type="fvec3" value="75 180 0" />
    <attribute id="LevelName" type="FixedString" value="" />
    <attribute id="MapKey" type="FixedString" value="f1a2b3c4-d5e6-4f7a-8b9c-0d1e2f3a4b5c" />
    <attribute id="Name" type="LSString" value="SMR_Staff_Akitaro" />
    <attribute id="ParentTemplateId" type="FixedString" value="26c24ccf-8f4a-44a9-ba56-e1d8e9d49ae3" />
    <attribute id="Stats" type="FixedString" value="SMR_Staff_Akitaro" />
    <attribute id="Type" type="FixedString" value="item" />
    <attribute id="VisualTemplate" type="FixedString" value="91b88b2e-09c7-8523-ee50-df363cef3d9f" />
    <attribute id="_OriginalFileVersion_" type="int64" value="144115188075855912" />
    <children>
        <node id="GameMaster" />
    </children>
</node>
```

Note:
- ParentTemplateId `26c24ccf-8f4a-44a9-ba56-e1d8e9d49ae3` is the Spellsparkler's MapKey
- VisualTemplate `91b88b2e-09c7-8523-ee50-df363cef3d9f` is the Spellsparkler's visual

### Step 4: Add Staff Template to merged.lsf.lsx

Add the same GameObjects node (BOTH files must be updated).

### Step 5: Add to OneTimeRewards.lsx

Add before the closing `</children>` tag:
```xml
<node id="OneTimeReward">
    <attribute id="Amount" type="uint32" value="1"/>
    <attribute id="ItemTemplateId" type="FixedString" value="f1a2b3c4-d5e6-4f7a-8b9c-0d1e2f3a4b5c"/>
    <attribute id="UUID" type="guid" value="a2b3c4d5-e6f7-4a8b-9c0d-1e2f3a4b5c6d"/>
</node>
```

### Step 6: Add Localization Entries

Add to Localization/English/SampleMagicRingMod.xml:
```xml
<content contentuid="h5a6b7c8dge9f0g1a2bg3c4dg5e6f7a8b9c0d" version="1">Staff of Akitaro</content>
<content contentuid="h6b7c8d9egf0a1g2b3cg4d5eg6f7a8b9c0d1e" version="1">A quarterstaff crackling with arcane energy. Grants Lightning Charges when casting spells at close range, unlimited Light, unlimited Counterspell, and unlimited Celestial Haste.</content>
```

Add same entries to Localization/English/SampleMagicRingMod.loca.xml.

---

## Implementation Checklist

- [x] Add SMR_Shout_CelestialHaste_Unlimited to Spell_Shout.txt
- [x] Add SMR_Staff_Akitaro to Weapon.txt
- [x] Add staff template to merged.lsx
- [x] Add staff template to merged.lsf.lsx
- [x] Add OneTimeReward entry to OneTimeRewards.lsx
- [x] Add localization to SampleMagicRingMod.xml
- [x] Add localization to SampleMagicRingMod.loca.xml
- [ ] Build and test mod

---

## Test Plan

- [ ] Load game with mod enabled
- [ ] Check traveler's chest for Staff of Akitaro
- [ ] Equip staff and verify appearance (should look like Spellsparkler)
- [ ] Verify Light spell is available (bonus action, unlimited)
- [ ] Cast Light and verify it works
- [ ] Verify Counterspell interrupt is available (unlimited)
- [ ] Verify Celestial Haste spell is available (bonus action, unlimited)
- [ ] Cast Celestial Haste and verify Haste is applied
- [ ] Cast a close-range spell and verify Lightning Charges are gained (Arcane Charge passive)

---

## Notes

- Uses Spellsparkler's ParentTemplateId and VisualTemplate for appearance
- Reuses existing SMR_Target_Light_Unlimited and SMR_Interrupt_Counterspell_Unlimited
- New spell SMR_Shout_CelestialHaste_Unlimited based on Gontr Mael's Celestial Haste
