# Phase 057: Silverlight (Level21Gear)

**Status:** COMPLETE
**Date:** 2026-02-20

---

## Goals

1. **Copy L13_Sword_Silverlight:** Create `L21_Sword_Silverlight` in Level21Gear as a standalone copy of `L13_Sword_Silverlight`, with all L13-prefixed spells and passives duplicated under L21 prefixes. Level21Gear must NOT depend on Level13PlusGear.
2. **Create Silvered Bulwark Scroll:** Create a spell scroll (`OBJ_L21_Scroll_SilveredBulwark`) that casts `L21_Target_SilveredBulwark`. Deliver it in `L21_Gear_Chest_TT` alongside the sword.

---

## Source Item: L13_Sword_Silverlight

For reference, here is the full `L13_Sword_Silverlight` definition to be ported:

**Weapon entry (`Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Weapon.txt`):**
```
new entry "L13_Sword_Silverlight"
type "Weapon"
using "WPN_Longsword_2"
data "RootTemplate" "ed137558-6b60-4193-97d1-c7d26f8a858b"
data "Rarity" "Legendary"
data "DefaultBoosts" "WeaponEnchantment(5);WeaponProperty(Magical)"
data "Boosts" "UnlockSpell(Target_MAG_Smite_Wrathful);UnlockSpell(L13_Target_BlindingSmite_Moonguard);UnlockSpell(L13_Target_Light_Unlimited);UnlockSpell(Target_PLA_ShieldOfFaith_SwordOfJustice);UnlockSpell(L13_Shout_CelestialHaste_Free);UnlockSpell(L13_Shout_SpiritGuardians_Moonguard,AddChildren,,,SpellCastingAbility);UnlockSpell(L13_Target_SilveredBulwark)"
data "PassivesOnEquip" "MAG_PlaneShifterSlayer_Passive;L13_RadiantWeapon_Passive;MAG_TheClover_Rearrangement_Passive;CRE_LathandersLight_Passive;L13_Moonshield_Passive"
data "StatusOnEquip" "MAG_LATHANDERS_LIGHT_TECHNICAL;LOW_RAMAZITHSTOWER_DEVA_BLESSING"
data "Unique" "0"
```

### L13 Spells Used (by Silverlight)

**Spells that need copying to L21 (L13-prefixed, not available outside that mod):**

| L13 Spell | L21 Equivalent | Notes |
|-----------|----------------|-------|
| `L13_Target_BlindingSmite_Moonguard` | `L21_Target_BlindingSmite_Silverlight` | Unlimited Blinding Smite, no slot cost |
| `L13_Shout_CelestialHaste_Free` | *(reuse `L21_Shout_CelestialHaste_Unlimited`)* | Already in Level21Gear; already free (no cost) |
| `L13_Shout_SpiritGuardians_Moonguard` | `L21_Shout_SpiritGuardians_Silverlight` | Container spell (parent) |
| `L13_Shout_SpiritGuardians_Moonguard_Radiant` | `L21_Shout_SpiritGuardians_Silverlight_Radiant` | Child spell |
| `L13_Shout_SpiritGuardians_Moonguard_Necrotic` | `L21_Shout_SpiritGuardians_Silverlight_Necrotic` | Child spell |
| `L13_Target_SilveredBulwark` | `L21_Target_SilveredBulwark` | Invulnerability aura (Globe of Invulnerability variant) |

**Spells already available in vanilla / Level21Gear (do NOT need copying):**

| Spell | Source |
|-------|--------|
| `Target_MAG_Smite_Wrathful` | Vanilla |
| `Target_PLA_ShieldOfFaith_SwordOfJustice` | Vanilla |
| `L21_Target_Light_Unlimited` | Already in Level21Gear |
| `L21_Shout_CelestialHaste_Unlimited` | Already in Level21Gear (and it's already free — replaces `L13_Shout_CelestialHaste_Free`) |

### L13 Passives Used (by the Moonguard Blade)

**Passives that need copying to L21 (L13-prefixed):**

| L13 Passive | L21 Equivalent | Effect |
|-------------|----------------|--------|
| `L13_RadiantWeapon_Passive` | `L21_RadiantWeapon_Passive` | +1d8 Radiant damage on melee attacks |
| `L13_Moonshield_Passive` | `L21_Moonshield_Passive` | Toggled aura: Shadow Curse immunity (SCL_MOONSHIELD_AURA) |

**Passives/statuses already in vanilla (do NOT need copying):**

| Passive/Status | Source |
|----------------|--------|
| `MAG_PlaneShifterSlayer_Passive` | Vanilla |
| `MAG_TheClover_Rearrangement_Passive` | Vanilla (crit on 19-20, reroll ≤2) |
| `CRE_LathandersLight_Passive` | Vanilla |
| `MAG_LATHANDERS_LIGHT_TECHNICAL` | Vanilla (status) |
| `LOW_RAMAZITHSTOWER_DEVA_BLESSING` | Vanilla (status — +5d8 radiant on weapon attacks) |

---

## Part 1 Implementation Plan

### Task 1: New RootTemplate

Create `Level21Gear/Public/Level21Gear/RootTemplates/L21_Sword_Silverlight.lsf.lsx`.

Copy structure from `L13_Blade_Moonguard.lsf.lsx`, replacing:
- `MapKey` → new UUID from pool (ed21 prefix)
- `Name` → `L21_Sword_Silverlight`
- `Stats` → `L21_Sword_Silverlight`
- `DisplayName` handle → new L21 handle
- `Description` handle → new L21 handle
- `ParentTemplateId` → **keep** `20c66f8d-f455-42fc-8e48-543512247e75` (Voss's Silver Sword visual — a Legendary silver longsword look)

```xml
<?xml version="1.0" encoding="utf-8"?>
<save>
    <version major="4" minor="0" revision="6" build="5" lslib_meta="v1,bswap_guids" />
    <region id="Templates">
        <node id="Templates">
            <children>
                <node id="GameObjects">
                    <attribute id="Description" type="TranslatedString" handle="[NEW_DESC_HANDLE]" version="1" />
                    <attribute id="DisplayName" type="TranslatedString" handle="[NEW_NAME_HANDLE]" version="1" />
                    <attribute id="LevelName" type="FixedString" value="" />
                    <attribute id="MapKey" type="FixedString" value="[NEW_ROOT_UUID]" />
                    <attribute id="Name" type="LSString" value="L21_Sword_Silverlight" />
                    <attribute id="ParentTemplateId" type="FixedString" value="20c66f8d-f455-42fc-8e48-543512247e75" />
                    <attribute id="Stats" type="FixedString" value="L21_Sword_Silverlight" />
                    <attribute id="Type" type="FixedString" value="item" />
                    <attribute id="_OriginalFileVersion_" type="int64" value="144115188075855912" />
                    <children>
                        <node id="GameMaster" />
                    </children>
                </node>
            </children>
        </node>
    </region>
</save>
```

### Task 2: Weapon Stats Entry

Add to `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Weapon.txt`:

```
new entry "L21_Sword_Silverlight"
type "Weapon"
using "WPN_Longsword_2"
data "RootTemplate" "[NEW_ROOT_UUID]"
data "Rarity" "Legendary"
data "DefaultBoosts" "WeaponEnchantment(5);WeaponProperty(Magical)"
data "Boosts" "UnlockSpell(Target_MAG_Smite_Wrathful);UnlockSpell(L21_Target_BlindingSmite_Silverlight);UnlockSpell(L21_Target_Light_Unlimited);UnlockSpell(Target_PLA_ShieldOfFaith_SwordOfJustice);UnlockSpell(L21_Shout_CelestialHaste_Unlimited);UnlockSpell(L21_Shout_SpiritGuardians_Silverlight,AddChildren,,,SpellCastingAbility);UnlockSpell(L21_Target_SilveredBulwark)"
data "PassivesOnEquip" "MAG_PlaneShifterSlayer_Passive;L21_RadiantWeapon_Passive;MAG_TheClover_Rearrangement_Passive;CRE_LathandersLight_Passive;L21_Moonshield_Passive"
data "StatusOnEquip" "MAG_LATHANDERS_LIGHT_TECHNICAL;LOW_RAMAZITHSTOWER_DEVA_BLESSING"
data "Unique" "0"
```

### Task 3: Copy Spells to Spell_Target.txt

Add to `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Target.txt`:

```
new entry "L21_Target_BlindingSmite_Silverlight"
type "SpellData"
data "SpellType" "Target"
using "Target_Smite_Blinding"
data "DisplayName" "[NEW_BLINDINGSMITE_NAME_HANDLE];1"
data "ExtraDescription" "[NEW_BLINDINGSMITE_DESC_HANDLE];1"
data "UseCosts" "ActionPoint:1"
```

*(Source: `L13_Target_BlindingSmite_Moonguard` — unlimited Blinding Smite, costs 1 action, no spell slot)*

```
new entry "L21_Target_SilveredBulwark"
type "SpellData"
data "SpellType" "Target"
using "Target_GlobeOfInvulnerability"
data "Level" "6"
data "SpellSchool" "Abjuration"
data "SpellProperties" "AI_ONLY:ApplyStatus(SELF,AI_HELPER_BUFF_LARGE,100,30);AI_IGNORE:ApplyStatus(LOW_RAMAZITHSTOWER_NIGHTSONG_GLOBE_1,100,-1)"
data "TargetRadius" "18"
data "AreaRadius" ""
data "TargetConditions" "not HasStatus('LOW_RAMAZITHSTOWER_NIGHTSONG_GLOBE_1')"
data "Icon" "Spell_Abjuration_GlobeOfInvulnerability"
data "DisplayName" "[NEW_SILVEREDBULWARK_NAME_HANDLE];1"
data "Description" "[NEW_SILVEREDBULWARK_DESC_HANDLE];1"
data "UseCosts" ""
```

*(Source: `L13_Target_SilveredBulwark` — invulnerability aura, free action, no cost)*

### Task 4: Copy Spells to Spell_Shout.txt

Add to `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Shout.txt`:

**Note:** `L21_Shout_CelestialHaste_Unlimited` already exists in Level21Gear and is already free (no cost). No new CelestialHaste spell needed.

```
new entry "L21_Shout_SpiritGuardians_Silverlight"
type "SpellData"
data "SpellType" "Shout"
data "Level" "3"
data "SpellSchool" "Conjuration"
data "ContainerSpells" "L21_Shout_SpiritGuardians_Silverlight_Necrotic;L21_Shout_SpiritGuardians_Silverlight_Radiant"
data "AreaRadius" "3"
data "TargetConditions" "Self()"
data "Icon" "Spell_Conjuration_SpiritGuardians"
data "DisplayName" "[NEW_SG_NAME_HANDLE];1"
data "Description" "[NEW_SG_DESC_HANDLE];1"
data "DescriptionParams" "DealDamage(3d8,Radiant);DealDamage(3d8,Necrotic)"
data "TooltipAttackSave" "Wisdom"
data "PrepareSound" "Spell_Prepare_Damage_Radiant_Gen_L1to3"
data "PrepareLoopSound" "Spell_Prepare_Damage_Radiant_Gen_L1to3_Loop"
data "CastSound" "Spell_Cast_Damage_Radiant_SpiritGuardians_L1to3"
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsSpell;IsConcentration;DisplayInItemTooltip;AddFallBackOrigin"

new entry "L21_Shout_SpiritGuardians_Silverlight_Radiant"
type "SpellData"
data "SpellType" "Shout"
using "Shout_SpiritGuardians"
data "SpellContainerID" "L21_Shout_SpiritGuardians_Silverlight"
data "ContainerSpells" ""
data "SpellProperties" "ApplyStatus(SPIRIT_GUARDIANS_RADIANT_AURA,100,10)"
data "Description" "[NEW_SG_DESC_HANDLE];1"
data "ExtraDescription" "[NEW_SG_RADIANT_EXTRADESC_HANDLE];1"
data "ExtraDescriptionParams" "DealDamage(3d8,Radiant)"
data "TooltipStatusApply" "ApplyStatus(SPIRIT_GUARDIANS_RADIANT_AURA,100,10)"

new entry "L21_Shout_SpiritGuardians_Silverlight_Necrotic"
type "SpellData"
data "SpellType" "Shout"
using "Shout_SpiritGuardians"
data "SpellContainerID" "L21_Shout_SpiritGuardians_Silverlight"
data "ContainerSpells" ""
data "SpellProperties" "ApplyStatus(SPIRIT_GUARDIANS_NECROTIC_AURA,100,10)"
data "Description" "[NEW_SG_DESC_HANDLE];1"
data "ExtraDescription" "[NEW_SG_NECROTIC_EXTRADESC_HANDLE];1"
data "ExtraDescriptionParams" "DealDamage(3d8,Necrotic)"
data "TooltipStatusApply" "ApplyStatus(SPIRIT_GUARDIANS_NECROTIC_AURA,100,10)"
```

### Task 5: Create Passive.txt

Level21Gear does not yet have a `Passive.txt`. Create:
`Level21Gear/Public/Level21Gear/Stats/Generated/Data/Passive.txt`

```
new entry "L21_RadiantWeapon_Passive"
type "PassiveData"
data "DisplayName" "[NEW_RADIANTWEAPON_NAME_HANDLE];1"
data "Description" "[NEW_RADIANTWEAPON_DESC_HANDLE];1"
data "DescriptionParams" "DealDamage(1d8,Radiant)"
data "TooltipConditionalDamage" "DealDamage(1d8,Radiant)"
data "Boosts" "IF(IsMeleeAttack()):CharacterWeaponDamage(1d8, Radiant)"

new entry "L21_Moonshield_Passive"
type "PassiveData"
data "Properties" "ToggledDefaultOn;ToggledDefaultAddToHotbar;IsToggled"
data "DisplayName" "[NEW_MOONSHIELD_NAME_HANDLE];1"
data "Description" "[NEW_MOONSHIELD_DESC_HANDLE];1"
data "ToggleOnFunctors" "ApplyStatus(SCL_MOONSHIELD_AURA, 100, -1)"
data "ToggleOffFunctors" "RemoveStatus(SCL_MOONSHIELD_AURA)"
```

### Task 6: Add to TreasureTable

Edit `Level21Gear/Public/Level21Gear/Stats/Generated/TreasureTable.txt` to add Silverlight and the scroll to `L21_Gear_Chest_TT`:

```
new treasuretable "L21_Gear_Chest_TT"
 CanMerge 1
new subtable "1,1"
object category "I_L21_Staff_Gimeitaro",1,0,0,0,0,0,0,0
new subtable "1,1"
object category "I_L21_Sword_Silverlight",1,0,0,0,0,0,0,0
new subtable "1,1"
object category "I_OBJ_L21_Scroll_SilveredBulwark",1,0,0,0,0,0,0,0
```

### Task 7: Localization

Add all new entries to `Level21Gear/Localization/English/Level21Gear.loca.xml`:

```xml
<!-- Silverlight Sword -->
<content contentuid="[NEW_NAME_HANDLE]" version="1">Silverlight</content>
<content contentuid="[NEW_DESC_HANDLE]" version="1">A longsword blessed by both Selûne and celestial Devas. Grants Wrathful Smite, Blinding Smite (unlimited), Light (unlimited), Shield of Faith, Celestial Haste (free action), Spirit Guardians (free action), Silvered Bulwark (invulnerability), Plane Shifter Slayer, Radiant Weapon (+1d8 radiant), Deva's Blessing (+5d8 radiant), Critical Bonus (crit on 19-20, reroll ≤2), Lathander's Light aura, and Moonshield Aura (Shadow Curse protection).</content>

<!-- Blinding Smite (Silverlight) -->
<content contentuid="[NEW_BLINDINGSMITE_NAME_HANDLE]" version="1">Blinding Smite (Unlimited)</content>
<content contentuid="[NEW_BLINDINGSMITE_DESC_HANDLE]" version="1">Unlimited Blinding Smite. Costs 1 action, no spell slot.</content>

<!-- Spirit Guardians (Silverlight) -->
<content contentuid="[NEW_SG_NAME_HANDLE]" version="1">Silverlight's Spirit Guardians</content>
<content contentuid="[NEW_SG_DESC_HANDLE]" version="1">Call forth spirits to protect you. Nearby enemies take 3d8 Radiant or Necrotic damage. Free action casting.</content>
<content contentuid="[NEW_SG_RADIANT_EXTRADESC_HANDLE]" version="1">Radiant spirits surround you. Free action casting.</content>
<content contentuid="[NEW_SG_NECROTIC_EXTRADESC_HANDLE]" version="1">Necrotic spirits surround you. Free action casting.</content>

<!-- Radiant Weapon Passive -->
<content contentuid="[NEW_RADIANTWEAPON_NAME_HANDLE]" version="1">Radiant Weapon</content>
<content contentuid="[NEW_RADIANTWEAPON_DESC_HANDLE]" version="1">This weapon is infused with divine radiance, dealing extra radiant damage on melee attacks.</content>

<!-- Moonshield Passive -->
<content contentuid="[NEW_MOONSHIELD_NAME_HANDLE]" version="1">Moonshield Aura</content>
<content contentuid="[NEW_MOONSHIELD_DESC_HANDLE]" version="1">Toggled aura that grants immunity to the Shadow Curse.</content>

<!-- Silvered Bulwark Spell -->
<content contentuid="[NEW_SILVEREDBULWARK_NAME_HANDLE]" version="1">Silvered Bulwark</content>
<content contentuid="[NEW_SILVEREDBULWARK_DESC_HANDLE]" version="1">Encase an ally in a radiant shield of invulnerability. The target becomes completely immune to all damage and gains advantage on all saving throws. The protective aura follows the target as they move.</content>

<!-- Silvered Bulwark Scroll -->
<content contentuid="[NEW_SCROLL_NAME_HANDLE]" version="1">Scroll of Silvered Bulwark</content>
<content contentuid="[NEW_SCROLL_DESC_HANDLE]" version="1">A scroll inscribed with the Silvered Bulwark invocation. Encase an ally in a radiant shield of invulnerability. Single use.</content>
```

### Task 8: Scroll Stats Entry

Add to `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Object.txt`:

```
new entry "OBJ_L21_Scroll_SilveredBulwark"
type "Object"
using "_MagicScroll"
data "RootTemplate" "[NEW_SCROLL_ROOT_UUID]"
data "DisplayName" "[NEW_SCROLL_NAME_HANDLE];1"
data "Description" "[NEW_SCROLL_DESC_HANDLE];1"
data "ValueLevel" "6"
data "Rarity" "Rare"
data "Priority" "1"
```

**Notes:**
- Uses `_MagicScroll` base (which inherits from `OBJ_Scroll_Indestructible → OBJ_Scroll → _Book`)
- `_MagicScroll` already sets: `ItemUseType Scroll`, `UseCosts ActionPoint:1`, `UseConditions not IsSummon()`
- The spell the scroll casts is defined in the RootTemplate (Task 9), not in the stats entry
- TreasureTable reference: `I_OBJ_L21_Scroll_SilveredBulwark` (added in Task 6)

### Task 9: Scroll RootTemplate

Create `Level21Gear/Public/Level21Gear/RootTemplates/L21_Scroll_SilveredBulwark.lsf.lsx`.

**Research needed:** The vanilla scroll RootTemplates are not extracted to VanillaBG3. The mechanism linking a scroll's RootTemplate to the spell it casts needs to be determined. Use the vanilla Globe of Invulnerability scroll (`8d4c06d1-e504-49b0-a4fa-5179ab717f1e`) as the `ParentTemplateId` so the scroll inherits its spell-casting behavior — then override the spell to `L21_Target_SilveredBulwark`.

**Tentative structure** (verify against a working scroll):

```xml
<?xml version="1.0" encoding="utf-8"?>
<save>
    <version major="4" minor="0" revision="6" build="5" lslib_meta="v1,bswap_guids" />
    <region id="Templates">
        <node id="Templates">
            <children>
                <node id="GameObjects">
                    <attribute id="Description" type="TranslatedString" handle="[NEW_SCROLL_DESC_HANDLE]" version="1" />
                    <attribute id="DisplayName" type="TranslatedString" handle="[NEW_SCROLL_NAME_HANDLE]" version="1" />
                    <attribute id="LevelName" type="FixedString" value="" />
                    <attribute id="MapKey" type="FixedString" value="[NEW_SCROLL_ROOT_UUID]" />
                    <attribute id="Name" type="LSString" value="L21_Scroll_SilveredBulwark" />
                    <attribute id="ParentTemplateId" type="FixedString" value="8d4c06d1-e504-49b0-a4fa-5179ab717f1e" />
                    <attribute id="Stats" type="FixedString" value="OBJ_L21_Scroll_SilveredBulwark" />
                    <attribute id="Type" type="FixedString" value="item" />
                    <attribute id="_OriginalFileVersion_" type="int64" value="144115188075855912" />
                    <children>
                        <node id="GameMaster" />
                    </children>
                </node>
            </children>
        </node>
    </region>
</save>
```

**If inheriting from the Globe of Invulnerability scroll's ParentTemplate doesn't automatically assign the spell:** Look at how the SampleMagicRingMod or other working scrolls link their RootTemplate to their spell. The spell may need to be specified via a `ScrollSpell` attribute or similar.

---

## Files to Modify/Create

| File | Action | Description |
|------|--------|-------------|
| `Level21Gear/Public/Level21Gear/RootTemplates/L21_Sword_Silverlight.lsf.lsx` | Create | RootTemplate for the sword |
| `Level21Gear/Public/Level21Gear/RootTemplates/L21_Scroll_SilveredBulwark.lsf.lsx` | Create | RootTemplate for the Silvered Bulwark scroll |
| `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Weapon.txt` | Edit | Add L21_Sword_Silverlight entry |
| `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Object.txt` | Edit | Add OBJ_L21_Scroll_SilveredBulwark entry |
| `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Target.txt` | Edit | Add L21_Target_BlindingSmite_Silverlight and L21_Target_SilveredBulwark |
| `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Shout.txt` | Edit | Add SpiritGuardians container + Radiant/Necrotic children |
| `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Passive.txt` | Create | New file with L21_RadiantWeapon_Passive and L21_Moonshield_Passive |
| `Level21Gear/Public/Level21Gear/Stats/Generated/TreasureTable.txt` | Edit | Add Silverlight and Silvered Bulwark scroll to L21_Gear_Chest_TT |
| `Level21Gear/Localization/English/Level21Gear.loca.xml` | Edit | All display names and descriptions (sword + scroll) |

---

## UUID/Handle Requirements

### UUID Convention for Level21Gear

Level21Gear uses the **`ed21`** UUID prefix (not `ed13`). Take UUIDs from the pool in `docs/instructions/uuid_workflow.md`, but replace the first 4 characters with `ed21`.

**Handle format:** `h` + UUID with `-` replaced by `g`
- Example UUID: `ed21xxxx-yyyy-zzzz-aaaa-bbbbbbbbbbbb`
- Example handle: `hed21xxxxgyyyygzzzzgaaaagbbbbbbbbbbbb`

### Estimated UUIDs Needed

| Purpose | Count |
|---------|-------|
| RootTemplate UUID (L21_Sword_Silverlight) | 1 |
| Localization handles (sword name + description) | 2 |
| Localization handles (BlindingSmite name + desc) | 2 |
| Localization handles (SpiritGuardians name + desc) | 2 |
| Localization handles (SG Radiant + Necrotic extra descs) | 2 |
| Localization handles (RadiantWeapon passive name + desc) | 2 |
| Localization handles (Moonshield passive name + desc) | 2 |
| Localization handles (SilveredBulwark name + desc) | 2 |
| RootTemplate UUID (Silvered Bulwark scroll) | 1 |
| Localization handles (scroll name + description) | 2 |
| **Total** | **18** |

### UUID Allocation

*Fill in during implementation. Delete used UUIDs from the pool in `uuid_workflow.md`.*

| Purpose | UUID / Handle | Value |
|---------|---------------|-------|
| L21_Sword_Silverlight RootTemplate | UUID | `ed21e061-f4d9-49f0-8aa0-e737813db4e4` |
| Silverlight DisplayName | Handle | `hed21b41fg25f6g4b48ga058g98882385ec98` |
| Silverlight Description | Handle | `hed21219cgbdb5g4b2cga6bdg75aa4061f5b9` |
| BlindingSmite DisplayName | Handle | `hed2136c4gc084g4bb9gb8cdg4ee2ceed5e44` |
| BlindingSmite ExtraDescription | Handle | `hed213c4cg37f4g419bgb7d8g6a99ba882b59` |
| SpiritGuardians DisplayName | Handle | `hed2195ebgc3b4g4c56g84e0g5b9be483da78` |
| SpiritGuardians Description | Handle | `hed21b2deg0467g4c28gb2d3g68d9241d9fbf` |
| SpiritGuardians Radiant ExtraDescription | Handle | `hed21f39dg9a39g4020g8633g8baa0346f142` |
| SpiritGuardians Necrotic ExtraDescription | Handle | `hed211779g1e07g4abag94b1g837b1f5bf081` |
| RadiantWeapon DisplayName | Handle | `hed211c3bga028g4c40g9974g48a782f2611b` |
| RadiantWeapon Description | Handle | `hed219799g77ffg4983gbbc0g2c7c6a098a0c` |
| Moonshield DisplayName | Handle | `hed2116ddgbdfcg4f8egb30fg7e97d64fb985` |
| Moonshield Description | Handle | `hed218d2eg299cg4166g9d49ga2ef0b6a4f6b` |
| SilveredBulwark DisplayName | Handle | `hed210df9gfc13g40b3g93f5gf712e0859489` |
| SilveredBulwark Description | Handle | `hed2174cfg334bg4279g88dega41c002d7a49` |
| Silvered Bulwark Scroll RootTemplate | UUID | `ed21299d-a404-4f73-b54b-3d6154d12261` |
| Scroll DisplayName | Handle | `hed21b0d7gcad1g42eag802fg871ed925a317` |
| Scroll Description | Handle | `hed2106a3g39b6g4408ga2b9gae1418a6ca87` |

---

## Testing Plan

### Test 1: Sword Appears in Chest
1. Start a new game or use a save where the Tutorial Chest has not been opened.
2. Open Tutorial Chest → open L21_Gear_Chest inside it.
3. **Verify:** Silverlight appears in the chest alongside Staff of Gimeitaro.
4. **Verify:** Sword has correct name "Silverlight" and readable description.

### Test 2: Equip and Spells
1. Equip Silverlight in main hand.
2. **Verify:** Following spells appear in the hotbar/spell book:
   - Wrathful Smite
   - Blinding Smite (Unlimited)
   - Light (Unlimited)
   - Shield of Faith
   - Celestial Haste (free action)
   - Silverlight's Spirit Guardians (with Radiant and Necrotic variants)
   - Silvered Bulwark
3. **Verify:** Spirit Guardians container shows both variants on expansion.

### Test 3: Passives and Statuses
1. With Silverlight equipped:
2. **Verify:** Moonshield Aura passive appears in passive list (toggled on by default).
3. **Verify:** Melee attacks deal +1d8 radiant damage (Radiant Weapon passive).
4. **Verify:** Melee attacks deal +5d8 radiant damage (Deva's Blessing status).
5. **Verify:** Lathander's Light aura is active.
6. **Verify:** Critical hits land on 19-20 rolls.

### Test 4: Silvered Bulwark Scroll
1. Open L21_Gear_Chest.
2. **Verify:** "Scroll of Silvered Bulwark" appears in the chest alongside Silverlight.
3. Use the scroll on an ally.
4. **Verify:** The Silvered Bulwark invulnerability effect is applied to the target.

### Test 5: No L13 Dependency
1. Disable Level13PlusGear mod.
2. **Verify:** Level21Gear loads without errors and Silverlight still works correctly.

---

## Technical Notes

### Scroll Spell-Casting Behavior (RESOLVED)
BG3 scroll RootTemplates do NOT inherit their spell from the `ParentTemplateId`. The spell is always specified explicitly via `OnUsePeaceActions` children in the RootTemplate. Initial implementation used the vanilla Globe scroll as ParentTemplateId and incorrectly inherited Globe of Invulnerability.

**Correct scroll RootTemplate structure (two Action nodes required):**
- **ActionType 12** — Skill check: set `SkillID` to the spell name, `Conditions` to `""` (empty = usable by anyone), `ClassId` = `a865965f-501b-46e9-9eaa-7748e8c04d09` (fixed class id for scroll actions)
- **ActionType 33** — Cast spell: set `SpellId` to the spell name

**Generic scroll ParentTemplateId:** `4ffd5c4b-4c56-4f05-a228-a33754bb1806` (use this, not a specific vanilla spell scroll)

### Passive.txt is a New File for Level21Gear
Level21Gear currently has no `Passive.txt`. This phase creates it. Verify BG3 mod loading picks it up (it follows the same pattern as Level13PlusGear's `Passive.txt` which works).

### L21_Shout_CelestialHaste_Unlimited Reuse
`L13_Shout_CelestialHaste_Free` (no action cost) is equivalent to `L21_Shout_CelestialHaste_Unlimited` which already exists in Level21Gear with `UseCosts ""`. No new spell needed.

### Spirit Guardians Container Pattern
The container spell pattern (parent with `ContainerSpells`, children with `SpellContainerID`) is well-established in Level21Gear (Gimeitaro version) and Level13PlusGear (Moonguard version). Follow the same structure.

### No `UseCosts` on SpiritGuardians children
The L13 children (`_Radiant`, `_Necrotic`) don't set `UseCosts`. This is intentional — they inherit from the container or vanilla base. The L21 children should follow the same pattern.

### ParentTemplateId (Silver Longsword Visual)
`20c66f8d-f455-42fc-8e48-543512247e75` is Voss's Silver Sword — a Legendary silver longsword visual used for both L13_Blade_Moonguard and L13_Sword_Tyr. Keeping this for Silverlight gives it an appropriate Legendary silver blade appearance.

---

## Dependencies

**This phase depends on:**
- Phase 056 (COMPLETE) — L21_Gear_Chest must exist for Silverlight to be delivered via it.

**This phase has no dependency on:**
- Level13PlusGear mod — all L13-prefixed spells and passives are copied to L21 equivalents.

---

## Success Criteria

- [ ] `L21_Sword_Silverlight.lsf.lsx` created with correct UUID and handles
- [ ] `L21_Scroll_SilveredBulwark.lsf.lsx` created with correct UUID and handles
- [ ] `Weapon.txt` entry added with all L21-prefixed references
- [ ] `Object.txt` entry added for `OBJ_L21_Scroll_SilveredBulwark`
- [ ] `Spell_Target.txt` updated with `L21_Target_BlindingSmite_Silverlight` and `L21_Target_SilveredBulwark`
- [ ] `Spell_Shout.txt` updated with SpiritGuardians container + Radiant/Necrotic children
- [ ] `Passive.txt` created with `L21_RadiantWeapon_Passive` and `L21_Moonshield_Passive`
- [ ] `TreasureTable.txt` updated to include Silverlight and Silvered Bulwark scroll in `L21_Gear_Chest_TT`
- [ ] `Level21Gear.loca.xml` updated with all 18 handles
- [ ] 18 UUIDs consumed from pool and deleted from `uuid_workflow.md`
- [ ] Sword appears in L21_Gear_Chest in-game
- [ ] Scroll of Silvered Bulwark appears in L21_Gear_Chest in-game
- [ ] All spells and passives function correctly (including Silvered Bulwark and Deva's Blessing)
- [ ] Scroll casts Silvered Bulwark correctly when used
- [ ] Level21Gear works without Level13PlusGear enabled
- [ ] User-tested and confirmed

---

## Related Documentation

- **`docs/instructions/uuid_workflow.md`** — UUID pool; use `ed21` prefix for Level21Gear
- **`docs/instructions/armor_workflow.md`** — N/A (sword, not armor)
- **`docs/phases/Phase056.md`** — L21_Gear_Chest creation (delivery mechanism for Silverlight)
- **`Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Weapon.txt`** — Source: L13_Sword_Silverlight
- **`Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Passive.txt`** — Source: L13_RadiantWeapon_Passive, L13_Moonshield_Passive
- **`Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Spell_Shout.txt`** — Source: SpiritGuardians spells
- **`Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Spell_Target.txt`** — Source: L13_Target_BlindingSmite_Moonguard, L13_Target_SilveredBulwark

---

## Phase 057 Status: COMPLETE

---

## Revision 2: Ring of Creation — Summon L21 Gear Chest

**Status:** IMPLEMENTED
**Date:** 2026-02-20

### Goal

Add a `ROC_Summon_L21_Chest` spell to the Ring of Creation mod that summons the `L21_Gear_Chest` at the target location, and add it to the ring's spell list.

### Implementation

**New spell** (`ROC_Summon_L21_Chest`) added to `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Spell_Target.txt`:
- Summons `L21_Gear_Chest` (MapKey `ed21541c-165a-4c18-aad1-175c59940bbb`) using the established summon chest pattern
- Free action (`UseCosts ""`), unlimited uses
- Follows identical structure to `ROC_Summon_L13_Chest`

**Ring Boosts** updated in `Armor.txt` — `ROC_Summon_L21_Chest` added first in the spell list.

### UUID/Handle Allocation

| Purpose | Handle |
|---------|--------|
| Spell DisplayName | `hroc1ff21g9ed0g49ddg80f1g381f1c5aded4` |
| Spell Description | `hroc19db7g3d0ag4126gaa82g84526bc09580` |

*(Pool UUIDs used with `roc1` prefix: `0ee2ff21` and `00009db7` deleted from pool)*

### Files Modified

| File | Change |
|------|--------|
| `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Spell_Target.txt` | Added `ROC_Summon_L21_Chest` |
| `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Armor.txt` | Added `UnlockSpell(ROC_Summon_L21_Chest)` to ring Boosts |
| `RingOfCreation/Localization/English/RingOfCreation.loca.xml` | Added spell name/description; updated ring description to mention Level 21 Gear Chest |

### Success Criteria

- [ ] Ring of Creation equip grants the "Summon Level 21 Gear Chest" spell
- [ ] Casting the spell summons the L21_Gear_Chest containing Staff of Gimeitaro, Silverlight, and the Silvered Bulwark Scroll
- [ ] User-tested and confirmed

---
