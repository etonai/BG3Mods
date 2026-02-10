# Phase 25: Moonguard Blade and Staff of Akitaro Power Enhancements

## Status: COMPLETE (WITH BUGS)

**Known Issues:**
- Armor of Orpheus not appearing in Traveler's Chest - to be fixed in Phase 26

## Goals

1. **Moonguard Blade**: Add Spirit Guardians as a free action (no action cost)
2. **Moonguard Blade**: Change Celestial Haste to a free action (no bonus action cost)
3. **Staff of Akitaro**: Change Akitaro's Barrage from short rest cooldown to unlimited use
4. **Armor of Orpheus**: New armor with Githyanki Half Plate appearance and Armor of Tyr powers
5. **Cloak of Tyr**: Remove unique flag and add 3 to traveler's chest

---

## Implementation Details

### 1. Spirit Guardians Free Action (Moonguard Blade)

The current `SMR_Shout_SpiritGuardians_Tyr` spell costs an action. To make it free for the Moonguard Blade, we create a new container spell and variants with empty `UseCosts`.

**New Spell Entries (Spell_Shout.txt):**

Container spell:
```
new entry "SMR_Shout_SpiritGuardians_Moonguard"
type "SpellData"
data "SpellType" "Shout"
data "Level" "3"
data "SpellSchool" "Conjuration"
data "ContainerSpells" "SMR_Shout_SpiritGuardians_Moonguard_Necrotic;SMR_Shout_SpiritGuardians_Moonguard_Radiant"
data "AreaRadius" "3"
data "TargetConditions" "Self()"
data "Icon" "Spell_Conjuration_SpiritGuardians"
data "DisplayName" "ha1b2c3d4eg5f6ag7b8cg9d0eg1f2a3b4c5d6;1"
data "Description" "hb2c3d4e5fg6a7bg8c9dg0e1fg2a3b4c5d6e7;1"
data "DescriptionParams" "DealDamage(3d8,Radiant);DealDamage(3d8,Necrotic)"
data "TooltipAttackSave" "Wisdom"
data "PrepareSound" "Spell_Prepare_Damage_Radiant_Gen_L1to3"
data "PrepareLoopSound" "Spell_Prepare_Damage_Radiant_Gen_L1to3_Loop"
data "CastSound" "Spell_Cast_Damage_Radiant_SpiritGuardian_L1to3"
data "TargetSound" "Spell_Impact_Damage_Radiant_SpiritGuardian_L1to3"
data "CastTextEvent" "Cast"
data "UseCosts" ""
data "SpellAnimation" "03496c4a-49e0-4132-b585-3e5ecd1ad8e5,,;,,;cb171bda-f065-4520-b470-e447f678ba1f,,;18a9b8b8-6cec-4a6d-be46-a4cc499505e9,,;cc5b0caf-3ed1-4711-a50d-11dc3f1fdc6a,,;,,;0b07883a-08b8-43b6-ac18-84dc9e84ff50,,;,,;,,"
data "VerbalIntent" "Damage"
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsConcentration;IsSpell;IsHarmful;IsLinkedSpellContainer"
data "PrepareEffect" "2534712b-d31e-45a4-b8e3-6385caa9ddc1"
data "CastEffect" "56ea5092-8ecd-4b86-8686-c1c35d016928"
```

Radiant variant:
```
new entry "SMR_Shout_SpiritGuardians_Moonguard_Radiant"
type "SpellData"
data "SpellType" "Shout"
using "Shout_SpiritGuardians"
data "SpellContainerID" "SMR_Shout_SpiritGuardians_Moonguard"
data "ContainerSpells" ""
data "SpellProperties" "ApplyStatus(SPIRIT_GUARDIANS_RADIANT_AURA,100,10)"
data "Description" "hb2c3d4e5fg6a7bg8c9dg0e1fg2a3b4c5d6e7;1"
data "ExtraDescription" "he5f6a7b8cg9d0eg1f2ag3b4cg8c9d0e1f2a3b4;1"
data "ExtraDescriptionParams" "DealDamage(3d8,Radiant)"
data "TooltipDamageList" "DealDamage(3d8,Radiant)"
data "TooltipStatusApply" "ApplyStatus(SPIRIT_GUARDIANS_RADIANT_AURA,100,10)"
data "UseCosts" ""
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsConcentration;IsSpell;IsHarmful"
data "DamageType" "Radiant"
```

Necrotic variant:
```
new entry "SMR_Shout_SpiritGuardians_Moonguard_Necrotic"
type "SpellData"
data "SpellType" "Shout"
using "Shout_SpiritGuardians"
data "SpellContainerID" "SMR_Shout_SpiritGuardians_Moonguard"
data "ContainerSpells" ""
data "SpellProperties" "ApplyStatus(SPIRIT_GUARDIANS_NECROTIC_AURA,100,10)"
data "Description" "hb2c3d4e5fg6a7bg8c9dg0e1fg2a3b4c5d6e7;1"
data "ExtraDescription" "hf6a7b8c9dg0e1fg2a3bg4c5dg9d0e1f2a3b4c5;1"
data "ExtraDescriptionParams" "DealDamage(3d8,Necrotic)"
data "TooltipDamageList" "DealDamage(3d8,Necrotic)"
data "TooltipStatusApply" "ApplyStatus(SPIRIT_GUARDIANS_NECROTIC_AURA,100,10)"
data "UseCosts" ""
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsConcentration;IsSpell;IsHarmful"
data "DamageType" "Necrotic"
```

**Weapon Update (Weapon.txt):**
Add `UnlockSpell(SMR_Shout_SpiritGuardians_Moonguard,AddChildren,,,SpellCastingAbility)` to `SMR_Blade_Moonguard` Boosts.

---

### 2. Celestial Haste Free Action (Moonguard Blade)

The current `SMR_Shout_CelestialHaste_Unlimited` costs a bonus action. Create a free action version for the Moonguard Blade.

**New Spell Entry (Spell_Shout.txt):**
```
new entry "SMR_Shout_CelestialHaste_Free"
type "SpellData"
data "SpellType" "Shout"
using "Shout_MAG_Victory_Longbow_Haste"
data "UseCosts" ""
data "Cooldown" ""
```

**Weapon Update (Weapon.txt):**
Replace `SMR_Shout_CelestialHaste_Unlimited` with `SMR_Shout_CelestialHaste_Free` in `SMR_Blade_Moonguard` Boosts.

---

### 3. Akitaro's Barrage Unlimited (Staff of Akitaro)

The current `SMR_Projectile_AkitarosBarrage_ShortRest` has a short rest cooldown. Following the pattern of `SMR_Projectile_MagicMissile_Unlimited_Lvl3` (Spectral Barrage), we create an unlimited version.

**New Spell Entry (Spell_Projectile.txt):**
```
new entry "SMR_Projectile_AkitarosBarrage_Unlimited"
type "SpellData"
data "SpellType" "Projectile"
using "Projectile_MagicMissile_3"
data "DisplayName" "he1f2a3b4g5c6dg7e8fg9a0bg1c2d3e4f5a6b7;1"
data "ExtraDescription" "hf2a3b4c5g6d7eg8f9ag0b1cg2d3e4f5a6b7c8;1"
data "UseCosts" "BonusActionPoint:1"
data "MemoryCost" ""
```

Note: No `Cooldown` field = unlimited use (same pattern as Spectral Barrage).

**Weapon Update (Weapon.txt):**
Update `SMR_Staff_Akitaro` to use `SMR_Projectile_AkitarosBarrage_Unlimited` instead of `SMR_Projectile_AkitarosBarrage_ShortRest`.

---

### 4. Armor of Orpheus (New Item)

A new legendary armor using the Githyanki Half Plate appearance with the same powers as Armor of Tyr.

**Base Template:**
- MapKey: `38c63f49-3c50-46d0-90d3-68b247542c36`
- Name: `ARM_HalfPlate_Githyanki`

**New RootTemplate (merged.lsx):**
```xml
<node id="GameObjects">
    <attribute id="DisplayName" type="TranslatedString" handle="h25a1b2c3g4d5eg6f7ag8b9cg0d1e2f3a4b5c6;1" version="1"/>
    <attribute id="Description" type="TranslatedString" handle="h25b2c3d4g5e6fg7a8bg9c0dg1e2f3a4b5c6d7;1" version="1"/>
    <attribute id="MapKey" type="FixedString" value="25a1b2c3-d4e5-4f6a-7b8c-9d0e1f2a3b4c"/>
    <attribute id="Name" type="LSString" value="SMR_Armor_Orpheus"/>
    <attribute id="ParentTemplateId" type="FixedString" value="38c63f49-3c50-46d0-90d3-68b247542c36"/>
    <attribute id="Stats" type="FixedString" value="SMR_Armor_Orpheus"/>
    <attribute id="Type" type="FixedString" value="item"/>
</node>
```

**New Stats Entry (Armor.txt):**
```
new entry "SMR_Armor_Orpheus"
type "Armor"
using "ARM_HalfPlate_Body_2"
data "RootTemplate" "25a1b2c3-d4e5-4f6a-7b8c-9d0e1f2a3b4c"
data "Rarity" "Legendary"
data "Boosts" "RollBonus(SavingThrow, 2);UnlockSpell(SMR_Shout_CelestialHaste_Unlimited);UnlockSpell(SMR_Target_MistyStep_Unlimited);UnlockSpell(SMR_Shout_SpiritGuardians_Tyr,AddChildren,,,SpellCastingAbility)"
data "PassivesOnEquip" "MAG_ExoticMaterial_MediumArmor_Passive"
data "StatusOnEquip" "MAG_EXOTIC_MATERIAL_ARMOR_TECHNICAL"
data "Ability Modifier Cap" ""
data "Unique" "1"
```

**Localization (SampleMagicRingMod.loca.xml):**
```xml
<content contentuid="h25a1b2c3g4d5eg6f7ag8b9cg0d1e2f3a4b5c6" version="1">Armor of Orpheus</content>
<content contentuid="h25b2c3d4g5e6fg7a8bg9c0dg1e2f3a4b5c6d7" version="1">Legendary Githyanki armor imbued with divine power. Grants the wearer protection from harm and access to powerful spells.</content>
```

**Traveler's Chest (OneTimeRewards.lsx):**
```xml
<node id="OneTimeReward">
    <attribute id="Amount" type="uint32" value="1"/>
    <attribute id="ItemTemplateId" type="FixedString" value="25a1b2c3-d4e5-4f6a-7b8c-9d0e1f2a3b4c"/>
    <attribute id="UUID" type="guid" value="25c3d4e5-f6a7-4b8c-9d0e-1f2a3b4c5d6e"/>
</node>
```

---

### 5. Cloak of Tyr (Non-Unique, Quantity 3)

Remove the unique flag from the Cloak of Tyr and update the traveler's chest to provide 3 copies.

**Stats Update (Armor.txt):**

Current:
```
data "Unique" "1"
```

Change to:
```
data "Unique" "0"
```

**Traveler's Chest Update (OneTimeRewards.lsx):**

Find the existing entry with ItemTemplateId `b1c2d3e4-f5a6-4b7c-8d9e-0f1a2b3c4d5e` and change Amount from 1 to 3:
```xml
<node id="OneTimeReward">
    <attribute id="Amount" type="uint32" value="3"/>
    <attribute id="ItemTemplateId" type="FixedString" value="b1c2d3e4-f5a6-4b7c-8d9e-0f1a2b3c4d5e"/>
    <attribute id="UUID" type="guid" value="c2d3e4f5-a6b7-4c8d-9e0f-1a2b3c4d5e6f"/>
</node>
```

---

## Files to Modify

| File | Change |
|------|--------|
| `Spell_Shout.txt` | Add `SMR_Shout_SpiritGuardians_Moonguard` (container + 2 variants), `SMR_Shout_CelestialHaste_Free` |
| `Spell_Projectile.txt` | Add `SMR_Projectile_AkitarosBarrage_Unlimited` |
| `Weapon.txt` | Update Moonguard Blade (add Spirit Guardians, replace Celestial Haste) and Staff of Akitaro (replace Barrage) |
| `Armor.txt` | Add `SMR_Armor_Orpheus`, update `SMR_Cloak_Tyr` (remove Unique) |
| `merged.lsx` | Add RootTemplate for Armor of Orpheus |
| `SampleMagicRingMod.loca.xml` | Add DisplayName and Description for Armor of Orpheus |
| `OneTimeRewards.lsx` | Add Armor of Orpheus, update Cloak of Tyr amount to 3 |

---

## UUIDs/Handles

### New (Phase 25)

| Asset | Handle/UUID |
|-------|-------------|
| Armor of Orpheus MapKey | `444e6150-09a3-49c3-9a95-6940a5713852` |
| Armor of Orpheus DisplayName | `h25a1b2c3g4d5eg6f7ag8b9cg0d1e2f3a4b5c6;1` |
| Armor of Orpheus Description | `h25b2c3d4g5e6fg7a8bg9c0dg1e2f3a4b5c6d7;1` |
| Armor of Orpheus Reward UUID | `25c3d4e5-f6a7-4b8c-9d0e-1f2a3b4c5d6e` |

### Reused from Existing

| Asset | Handle/UUID |
|-------|-------------|
| Spirit Guardians DisplayName | `ha1b2c3d4eg5f6ag7b8cg9d0eg1f2a3b4c5d6;1` |
| Spirit Guardians Description | `hb2c3d4e5fg6a7bg8c9dg0e1fg2a3b4c5d6e7;1` |
| Spirit Guardians Radiant ExtraDesc | `he5f6a7b8cg9d0eg1f2ag3b4cg8c9d0e1f2a3b4;1` |
| Spirit Guardians Necrotic ExtraDesc | `hf6a7b8c9dg0e1fg2a3bg4c5dg9d0e1f2a3b4c5;1` |
| Akitaro's Barrage DisplayName | `he1f2a3b4g5c6dg7e8fg9a0bg1c2d3e4f5a6b7;1` |
| Akitaro's Barrage ExtraDescription | `hf2a3b4c5g6d7eg8f9ag0b1cg2d3e4f5a6b7c8;1` |

Note: Celestial Haste Free inherits display name/description from base spell via `using`.

---

## Test Plan

1. Load the game with the mod active
2. **Moonguard Blade - Spirit Guardians Test:**
   - Equip the Moonguard Blade
   - Verify Spirit Guardians appears in spell list (Radiant/Necrotic options)
   - Cast Spirit Guardians - should NOT consume any action
   - Verify you can still take an action AND bonus action after casting
3. **Moonguard Blade - Celestial Haste Test:**
   - Verify Celestial Haste appears in spell list
   - Cast Celestial Haste - should NOT consume a bonus action
   - Verify you can still take a bonus action after casting
4. **Staff of Akitaro Test:**
   - Equip the Staff of Akitaro
   - Verify Akitaro's Barrage appears in spell list
   - Cast Akitaro's Barrage (uses bonus action)
   - Verify the spell is NOT grayed out after use (no cooldown)
   - Cast it again to confirm unlimited use
5. **Armor of Orpheus Test:**
   - Retrieve Armor of Orpheus from traveler's chest
   - Verify it has Githyanki Half Plate appearance
   - Equip the armor and verify:
     - +2 Saving Throw bonus
     - Celestial Haste (unlimited, bonus action)
     - Misty Step (unlimited)
     - Spirit Guardians (Radiant/Necrotic options)
     - No Stealth disadvantage (Exotic Material)
6. **Cloak of Tyr Test:**
   - Verify 3 Cloaks of Tyr appear in traveler's chest
   - Equip multiple cloaks on different party members (should work since not unique)

---

## Additional Modifications

### Mod 1: Armor of Orpheus Not Appearing in Traveler's Chest

**Issue:** User reports Armor of Orpheus is not appearing in the traveler's chest.

**Root Cause:** Invalid generated UUID format.

**Fix:** Changed MapKey from `25a1b2c3-d4e5-4f6a-7b8c-9d0e1f2a3b4c` to `444e6150-09a3-49c3-9a95-6940a5713852`

**Files Updated:**
- `merged.lsx` - MapKey
- `Armor.txt` - RootTemplate
- `OneTimeRewards.lsx` - ItemTemplateId

**Status:** Fixed - awaiting user verification

---

### Mod 2: Remove Concentration from Celestial Haste

**Request:** Make all mod versions of Celestial Haste non-concentration spells.

**Affected Spells:**
- `SMR_Shout_CelestialHaste_Unlimited` (used by Sword of Tyr, Sword of Orpheus, Divine Maul, Staff of Akitaro, Armor of Tyr, Moonguard Splint, Armor of Orpheus)
- `SMR_Shout_CelestialHaste_Free` (used by Moonguard Blade)

**Fix:** Add `SpellFlags` override without `IsConcentration`:
```
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsSpell"
```

**Status:** Implemented

---

## Notes

- The old `SMR_Shout_CelestialHaste_Unlimited` remains for other items (Sword of Tyr, Sword of Orpheus, Divine Maul, Armor of Tyr, Moonguard Splint)
- The old `SMR_Shout_SpiritGuardians_Tyr` remains for Armor of Tyr and Moonguard Splint
- The old `SMR_Projectile_AkitarosBarrage_ShortRest` can be removed in a future cleanup phase if desired
