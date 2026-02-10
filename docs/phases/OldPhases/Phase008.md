# Phase 008 - Bug Fixes and Enhancements

**Status:** COMPLETE

## Goal
Fix bugs from previous phases and add new enhancements.

---

## Part 1: Fix Staff of the Archmage Appearance

### Issue
The Staff of the Archmage does not display with the Spellsparkler appearance as intended. The current ParentTemplateId (`26c24ccf-8f4a-44a9-ba56-e1d8e9d49ae3`) is the Spellsparkler's MapKey, but the appearance is still incorrect.

### Investigation Needed
- Verify the correct way to inherit appearance from another item
- Check if additional attributes are needed (Icon, VisualTemplate, etc.)
- Compare with how other mods handle custom weapon appearances

### Reference: Spellsparkler (MAG_CQCaster_GainArcaneChargeOnDamage_Quarterstaff)

From Gustav\Public\GustavDev\RootTemplates\_merged.lsf.lsx:
```xml
<node id="GameObjects">
    <attribute id="Description" type="TranslatedString" handle="h90f121bdg1eddg4487g90b9gae96264e8f6f" version="1" />
    <attribute id="DisplayName" type="TranslatedString" handle="hd4493830ge0fag4f85gb7edgc28b4c0c671c" version="2" />
    <attribute id="ExamineRotation" type="fvec3" value="75 180 0" />
    <attribute id="LevelName" type="FixedString" value="" />
    <attribute id="MapKey" type="FixedString" value="26c24ccf-8f4a-44a9-ba56-e1d8e9d49ae3" />
    <attribute id="Name" type="LSString" value="MAG_CQCaster_GainArcaneChargeOnDamage_Quarterstaff" />
    <attribute id="ParentTemplateId" type="FixedString" value="d25bc94a-5ee9-448f-9210-f2dad61ae7e5" />
    <attribute id="Stats" type="FixedString" value="MAG_CQCaster_GainArcaneChargeOnDamage_Quarterstaff" />
    <attribute id="Type" type="FixedString" value="item" />
    <attribute id="VisualTemplate" type="FixedString" value="91b88b2e-09c7-8523-ee50-df363cef3d9f" />
    <attribute id="_OriginalFileVersion_" type="int64" value="144115207403209023" />
    ...
</node>
```

### Current Staff of the Archmage Template
```xml
<node id="GameObjects">
    <attribute id="Description" type="TranslatedString" handle="ha1b2c3d4gf5e6g7a8bg9c0dg1e2f3a4b5c6d7" version="1" />
    <attribute id="DisplayName" type="TranslatedString" handle="h0a1b2c3dge4f5g6a7bg8c9dg0e1f2a3b4c5d6" version="1" />
    <attribute id="ExamineRotation" type="fvec3" value="75 180 0" />
    <attribute id="LevelName" type="FixedString" value="" />
    <attribute id="MapKey" type="FixedString" value="c2d3e4f5-a6b7-4c8d-9e0f-1a2b3c4d5e6f" />
    <attribute id="Name" type="LSString" value="SMR_Staff_Archmage" />
    <attribute id="ParentTemplateId" type="FixedString" value="26c24ccf-8f4a-44a9-ba56-e1d8e9d49ae3" />
    <attribute id="Stats" type="FixedString" value="SMR_Staff_Archmage" />
    <attribute id="Type" type="FixedString" value="item" />
    <attribute id="VisualTemplate" type="FixedString" value="91b88b2e-09c7-8523-ee50-df363cef3d9f" />
    <attribute id="_OriginalFileVersion_" type="int64" value="144115188075855912" />
    ...
</node>
```

### Possible Solutions
1. Add Icon attribute matching Spellsparkler
2. Check if VisualTemplate UUID is correct
3. Investigate if weapon stats need additional visual configuration
4. Look at how the WW mod or other mods configure weapon appearances

---

## Part 2: Add Telekinesis to Ring of Spectral Power

### Overview

Add **Telekinesis** spell to the Ring of Spectral Power, once per short rest.

### New Power

| Status | Power | Description | Source |
|--------|-------|-------------|--------|
| [ ] | **Telekinesis** | Cast Telekinesis (once per short rest) | Vanilla spell |

### Files to Modify

#### 1. Stats/Generated/Data/Spell_Target.txt

Add Telekinesis spell with short rest cooldown:
```
new entry "SMR_Target_Telekinesis_ShortRest"
type "SpellData"
data "SpellType" "Target"
using "Target_Telekinesis"
data "UseCosts" "ActionPoint:1"
data "Cooldown" "OncePerShortRest"
```

#### 2. Stats/Generated/Data/Armor.txt

Update SMR_Ring_Spectral_Power to add Telekinesis to Boosts.

---

## Part 3: Remove Counterspell from Ring of Spectral Power

### Overview

Remove the unlimited Counterspell interrupt from the Ring of Spectral Power.

### Change

Remove `UnlockInterrupt(SMR_Interrupt_Counterspell_Unlimited)` from the Boosts field in SMR_Ring_Spectral_Power.

---

## Part 4: Add Extra Magic Missile Projectile to Ring of Spectral Power

**STATUS: POSTPONED** - Cannot locate the stats entry for the Psychic Spark item in extracted game files.

### Overview

Add a passive that grants +1 extra missile to Magic Missile casts, similar to the vanilla item "Psychic Spark".

### Investigation Needed

- Find the Psychic Spark item in game files (may have different internal name)
- Identify the passive or boost that grants extra Magic Missile projectiles
- Apply similar effect to Ring of Spectral Power

### Possible Search Terms
- `ExtraProjectile`
- `SpellExtraProjectile`
- `MagicMissile`
- `Psychic`
- `Spark`

### Notes
- Could not find "Psychic Spark" in extracted Gustav/Shared files
- May need to search localization files for the display name to find internal name
- Alternative: Create custom passive with projectile bonus if vanilla reference not found

---

## Part 5: Add New Powers to Magus Circlet

### Overview

Add new spells and passive to the Magus Circlet.

### New Powers

| Status | Power | Description | Source |
|--------|-------|-------------|--------|
| [ ] | **See Invisibility** | Cast See Invisibility (unlimited, bonus action) | Vanilla spell |
| [ ] | **Faerie Fire** | Cast Faerie Fire (bonus action, once per short rest) | Vanilla spell |
| [ ] | **Blind Immunity** | Immune to blindness, can see through darkness | Eversight Ring passive |
| [ ] | **Protection From Evil And Good** | Cast Protection From Evil And Good (unlimited, bonus action) | Vanilla spell |
| [ ] | **Sunwalker's Gift** | Can see in the dark (darkvision) | Sunwalker's Gift Ring passive |

### Reference: Eversight Ring Passive

From Gustav\Public\GustavDev\Stats\Generated\Data\Passive.txt:
```
new entry "MAG_Shadow_BlindImmunity_Ring_Passive"
type "PassiveData"
data "DisplayName" "hf1d1e91dg0542g40a6g93e7ge0d5e31296c7;2"
data "Description" "hb00b5a9bg7c63g443fga699gb3341d39c41d;4"
data "Boosts" "StatusImmunity(SG_Blinded);IgnoreSurfaceCover(SurfaceDarknessCloud)"
```

### Reference: Sunwalker's Gift Ring Passive

The Sunwalker's Gift ring (UND_SocietyOfBrilliance_DarkvisionRing) uses passive `UND_SocietyOfBrilliance_DarkvisionRing_Passive` which grants darkvision.

### Files to Modify

#### 1. Stats/Generated/Data/Spell_Target.txt

Add See Invisibility and Protection From Evil And Good spells with bonus action cost:
```
new entry "SMR_Target_SeeInvisibility_Unlimited"
type "SpellData"
data "SpellType" "Target"
using "Target_SeeInvisibility"
data "UseCosts" "BonusActionPoint:1"

new entry "SMR_Target_ProtectionFromEvilAndGood_Unlimited"
type "SpellData"
data "SpellType" "Target"
using "Target_ProtectionFromEvilAndGood"
data "UseCosts" "BonusActionPoint:1"
```

#### 2. Stats/Generated/Data/Spell_Zone.txt

Add Faerie Fire spell with bonus action and short rest cooldown:
```
new entry "SMR_Zone_FaerieFire_ShortRest"
type "SpellData"
data "SpellType" "Zone"
using "Zone_FaerieFire"
data "UseCosts" "BonusActionPoint:1"
data "Cooldown" "OncePerShortRest"
```

#### 3. Stats/Generated/Data/Armor.txt

Update SMR_Circlet_Magus:
- Add the three new spells to Boosts (See Invisibility, Faerie Fire, Protection From Evil And Good)
- Add `MAG_Shadow_BlindImmunity_Ring_Passive` and `UND_SocietyOfBrilliance_DarkvisionRing_Passive` to PassivesOnEquip

---

## Part 6: Add Light to Staff of the Archmage

### Overview

Add **Light** spell to the Staff of the Archmage, unlimited as a bonus action.

### New Power

| Status | Power | Description | Source |
|--------|-------|-------------|--------|
| [ ] | **Light** | Cast Light (unlimited, bonus action) | Vanilla spell |

### Files to Modify

#### 1. Stats/Generated/Data/Spell_Target.txt

Add Light spell with bonus action cost:
```
new entry "SMR_Target_Light_Unlimited"
type "SpellData"
data "SpellType" "Target"
using "Target_Light"
data "UseCosts" "BonusActionPoint:1"
```

#### 2. Stats/Generated/Data/Weapon.txt

Update SMR_Staff_Archmage to add Light to Boosts.

---

## Part 7: Add Revivify to Ring of the Guardian

### Overview

Add **Revivify** spell to the Ring of the Guardian, once per long rest as a bonus action.

### New Power

| Status | Power | Description | Source |
|--------|-------|-------------|--------|
| [ ] | **Revivify** | Cast Revivify (once per long rest, bonus action) | Vanilla spell (Reviving Hands reference) |

### Reference: Reviving Hands (MAG_OfRevivify_Gloves)

From Gustav\Public\GustavDev\Stats\Generated\Data\Armor.txt:
```
new entry "MAG_OfRevivify_Gloves"
type "Armor"
using "ARM_Gloves_Metal"
data "RootTemplate" "0e94335a-bf4d-47b9-bde7-85ee2f01102f"
data "Rarity" "VeryRare"
data "Boosts" "RollBonus(SavingThrow, 1, Strength);UnlockSpell(Teleportation_MAG_Revivify)"
data "PassivesOnEquip" "MAG_Revivify_Gloves_Passive"
data "Unique" "1"
```

From Gustav\Public\GustavDev\Stats\Generated\Data\Spell_Teleportation.txt:
```
new entry "Teleportation_MAG_Revivify"
type "SpellData"
data "SpellType" "Teleportation"
using "Teleportation_Revivify"
data "Cooldown" "OncePerRestPerItem"
data "UseCosts" "ActionPoint:1"
```

### Files to Modify

#### 1. Stats/Generated/Data/Spell_Teleportation.txt

Add Revivify spell with long rest cooldown and bonus action:
```
new entry "SMR_Teleportation_Revivify_LongRest"
type "SpellData"
data "SpellType" "Teleportation"
using "Teleportation_Revivify"
data "UseCosts" "BonusActionPoint:1"
data "Cooldown" "OncePerLongRest"
```

#### 2. Stats/Generated/Data/Armor.txt

Update SMR_Ring_Guardian to add Revivify to Boosts.

---

## Implementation Order

### Staff Appearance Fix
1. [ ] Investigate correct method for weapon appearance inheritance
2. [ ] Fix Staff of the Archmage appearance in merged.lsx
3. [ ] Fix Staff of the Archmage appearance in merged.lsf.lsx

### Ring of Spectral Power - Telekinesis
4. [ ] Add SMR_Target_Telekinesis_ShortRest to Spell_Target.txt
5. [ ] Update SMR_Ring_Spectral_Power in Armor.txt to add Telekinesis

### Ring of Spectral Power - Remove Counterspell
6. [ ] Remove UnlockInterrupt(SMR_Interrupt_Counterspell_Unlimited) from SMR_Ring_Spectral_Power in Armor.txt

### Ring of Spectral Power - Extra Magic Missile (POSTPONED)
7. [x] Find Psychic Spark item in game files - Found template but stats entry missing from extraction
8. [ ] ~~Identify passive/boost that grants extra Magic Missile projectile~~
9. [ ] ~~Add passive to SMR_Ring_Spectral_Power in Armor.txt~~

### Magus Circlet - New Powers
10. [ ] Add SMR_Target_SeeInvisibility_Unlimited to Spell_Target.txt
11. [ ] Add SMR_Target_ProtectionFromEvilAndGood_Unlimited to Spell_Target.txt
12. [ ] Add SMR_Zone_FaerieFire_ShortRest to Spell_Zone.txt
13. [ ] Update SMR_Circlet_Magus in Armor.txt to add the three new spells and MAG_Shadow_BlindImmunity_Ring_Passive

### Staff of the Archmage - Light
14. [ ] Add SMR_Target_Light_Unlimited to Spell_Target.txt
15. [ ] Update SMR_Staff_Archmage in Weapon.txt to add Light

### Ring of the Guardian - Revivify
16. [ ] Add SMR_Teleportation_Revivify_LongRest to Spell_Teleportation.txt
17. [ ] Update SMR_Ring_Guardian in Armor.txt to add Revivify

### Final
18. [ ] Build and test mod

---

## Test Plan

### Staff Appearance
- [ ] Build mod with BG3 Modder's Multitool
- [ ] Load game with mod enabled
- [ ] Equip Staff of the Archmage
- [ ] Verify staff appears with Spellsparkler visual (lightning/sparkle effect staff)
- [ ] Compare side-by-side with actual Spellsparkler if available

### Ring of Spectral Power - Telekinesis
- [ ] Equip Ring of Spectral Power
- [ ] Verify Telekinesis spell is available
- [ ] Cast Telekinesis and verify it works
- [ ] Verify Telekinesis has short rest cooldown

### Ring of Spectral Power - Counterspell Removed
- [ ] Equip Ring of Spectral Power
- [ ] Verify Counterspell interrupt is no longer available

### Magus Circlet - New Powers
- [ ] Equip Magus Circlet
- [ ] Verify See Invisibility spell is available as bonus action
- [ ] Cast See Invisibility and verify it works (unlimited)
- [ ] Verify Protection From Evil And Good spell is available as bonus action
- [ ] Cast Protection From Evil And Good and verify it works (unlimited)
- [ ] Verify Faerie Fire spell is available as bonus action
- [ ] Cast Faerie Fire and verify it works
- [ ] Verify Faerie Fire has short rest cooldown
- [ ] Verify Blind Immunity passive is active (immune to blindness, can see through darkness)
- [ ] Verify Sunwalker's Gift passive is active (darkvision)

### Staff of the Archmage - Light
- [ ] Equip Staff of the Archmage
- [ ] Verify Light spell is available as bonus action
- [ ] Cast Light and verify it works (unlimited)

### Ring of the Guardian - Revivify
- [ ] Equip Ring of the Guardian
- [ ] Verify Revivify spell is available as bonus action
- [ ] Cast Revivify on a dead ally and verify it works
- [ ] Verify Revivify has long rest cooldown

---

## Bugs Found During Testing

1. **Telekinesis doesn't work on Ring of Spectral Power** - FIXED. Telekinesis is a "Throw" type spell, not a "Target" type spell. Created Spell_Throw.txt with correct spell definition using `Throw_Telekinesis` and updated Armor.txt to reference `SMR_Throw_Telekinesis_ShortRest`.

2. **Faerie Fire doesn't work on Magus Circlet** - FIXED. Faerie Fire is a "Target" type spell (`Target_FaerieFire`), not a "Zone" type. Changed spell entry to use correct base spell and renamed to `SMR_Target_FaerieFire_ShortRest`.

3. **See Invisibility doesn't work on Magus Circlet** - FIXED. See Invisibility is a "Shout" type spell (`Shout_SeeInvisibility`), not a "Target" type. Created new spell entry in Spell_Shout.txt and renamed to `SMR_Shout_SeeInvisibility_Unlimited`.

4. **Artistry of War doesn't work on Ring of Spectral Power** - FIXED. The spell's internal name is `Projectile_CursedTome_CurriculumofStrategy`, not `Projectile_ArtistryOfWar`. Updated Spell_Projectile.txt to use the correct base spell.

---

## Notes

- The Spellsparkler has a distinctive appearance with lightning/electrical effects
- Current staff may be showing as a generic quarterstaff
- May need to add Icon attribute or other visual properties
