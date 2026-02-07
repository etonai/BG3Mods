# Interesting Magical Effects

A collection of interesting magical effects, passives, and spells discovered in BG3 that could be used in future magical items.

---

## Spells Without Item Sources

Spells that no vanilla item grants - would require the container spell technique (see `adding_spells_without_item_source.md`).

| Spell | Type | Notes |
|-------|------|-------|
| Spirit Guardians | Shout | Requires container for Radiant/Necrotic variants |
| Divine Smite | Target | Paladin melee spell, adds radiant damage to weapon attacks |

---

## Interesting Passives

| Passive | Source Item | Effect | Internal Name |
|---------|-------------|--------|---------------|
| Lathander's Light | Blood of Lathander (CRE_BloodOfLathander, MapKey: 7b961f08-46c1-46b1-99bc-c59283831a0b) | Toggled 6m aura that blinds Fiends/Undead (CON 14 save), emits light | CRE_LathandersLight_Passive |
| Lathander's Blessing | Blood of Lathander | When reduced to 0 HP, regain 2-12 HP and nearby allies regain 1-6 HP (once per long rest) | CRE_LathandersBlessing_Passive |

---

## Interesting Spells (With Item Sources)

Spells that existing items grant - can use simple `using` technique.

| Spell | Source Item | Effect | Internal Name |
|-------|-------------|--------|---------------|
| Sunbeam | Blood of Lathander (CRE_BloodOfLathander, MapKey: 7b961f08-46c1-46b1-99bc-c59283831a0b) | 6d8 radiant damage in a line, blinds targets (CON save), once per long rest | Zone_MAG_BloodOfLathander_Sunbeam |
| Wrathful Smite | Voss's Silver Sword (MAG_Primeval_Silver_Longsword, MapKey: 20c66f8d-f455-42fc-8e48-543512247e75) | Melee attack deals extra psychic damage, may Frighten target | Needs research |
| Searing Smite | Skybreaker (UNI_UND_DuergarBlacksmithHammer, MapKey: 733a70a1-2e0f-46f4-aca1-037c0335dc72) | Melee attack deals extra fire damage, target may take burning damage | Needs research |
| Thunderwave | Ring of Thunderous Force (UNI_UND_KC_RingOfAbsolute, MapKey: c7a58f48-f24f-4139-b0f0-8b12e1bf074e) | AOE thunder damage, pushes enemies back | Needs research |
| Haste (Self) | Gontr Mael / Victory Longbow (GOB_DrowCommander_Longbow, MapKey: 9acff693-81d5-43f3-8bec-78370c51e5ab) | Cast Haste on self, once per long rest | Shout_MAG_Victory_Longbow_Haste |

---

## Interesting Status Effects

| Status | Effect | Internal Name |
|--------|--------|---------------|
| Lathander's Light | 6m aura that blinds Fiends/Undead (CON 14 save), emits gameplay light | MAG_LATHANDERS_LIGHT |
| Lathander's Light Blind | Applied to Fiends/Undead in aura who fail CON 14 save | MAG_LATHANDERS_LIGHT_BLIND_AURA_TARGET |
| Moonshield Aura | 13m aura that grants Shadow Curse immunity, emits gameplay light | SCL_MOONSHIELD_AURA |
| Moonshield | Protection from Shadow Curse (grants ACT2_SHADOW_CURSE_IMMUNE tag) | SCL_MOONSHIELD |
| Pixie's Blessing | Same as Moonshield, applied when Pixie is freed | GLO_PIXIESHIELD |

---

## Interesting Boosts

| Boost | Effect | Syntax |
|-------|--------|--------|
| Ability Override | Sets an ability score to a minimum value | `AbilityOverrideMinimum(Intelligence,17)` |

### Items with Notable Boosts

| Item | Effect | Internal Name |
|------|--------|---------------|
| Warped Headband of Intellect (UNI_FOR_OgresForHire_HeadbandOfIntellect, MapKey: 8f4876f1-44d9-4bb8-802e-907c6b0a0dba) | Sets Intelligence to 17 | Uses AbilityOverrideMinimum boost |

---

## Combination Ideas

Ideas for combining multiple effects into new items.

### Idea 1: [Name]
- **Concept**:
- **Effects**:
  -
- **Notes**:

---

## Research Notes

Notes on effects that need further investigation.

| Effect | Question | Status |
|--------|----------|--------|
| Blood of Lathander (CRE_BloodOfLathander, MapKey: 7b961f08-46c1-46b1-99bc-c59283831a0b) | Sunbeam spell and Lathander's Light toggled aura passive | Complete - see detailed notes below |
| Moon Lantern (Quest_GLO_Moonlantern, MapKey: 9aca1109-a59d-47d3-8f35-f248b70518f9) | Moonshield aura protection system | Complete - see detailed notes below |
| Armor of Persistence (MAG_EndGame_Plate_Armor, MapKey: fb2ff6d1-3096-4904-813c-a448e3fbec4d) | Research passives and boosts that make this powerful endgame armor | Pending |
| Viconia's Shield (MAG_TheBulwark_Shield, MapKey: 4f313dde-14bb-43a2-abdd-07b2eb38b33a) | Reflective Shell, Warding Bond, Shield Riposte (2d4 Force), Spellguard (spell save advantage) | Complete - used for Shield of Tyr in Phase 12 |
| Helm of Balduran (MAG_WYRM_OfBalduran_Helmet, MapKey: 0a64283a-1fc4-45cd-9e5e-f463f6b762ea) | +1 AC/saves, Stun Immunity, Crit Immunity, 2 HP regen/turn | Complete - used for Helmet of Tyr in Phase 12 |
| Helldusk Helmet (MAG_Infernal_Metal_Helmet, MapKey: 1c198060-6b6a-41c5-82ce-a3d3c3d76404) | Research passives and boosts for this infernal helmet | Pending |
| Gauntlets of the Warmaster (MAG_OfWarMaster_Gloves, MapKey: 85865321-5feb-447f-92e7-5c04359fe3af) | Research passives and boosts for these martial gloves | Pending |
| Mantle of the Holy Warrior (MAG_Radiant_CrusaderMantle_Cloak, MapKey: f1fdb8db-e754-4ea9-b6ce-440db6b776ac) | Research passives and boosts for this radiant cloak | Pending |
| Cloak of the Weave (MAG_EndGameCaster_Cloak, MapKey: 58c9bc94-b0ac-4ab9-a005-28cc445186f8) | Arcane Enchantment (+1 spell DC/attack) and Absorb Elements reaction | Complete - see detailed notes below |
| Infernal Rapier's Helm (QUEST_HAV_InfernalReward_002, MapKey: 6d60fcbb-e7a5-47ad-9cca-44565cbc0856) | Magical Durability (+2 saving throws vs spells) | Complete - see detailed notes below |
| Callous Glow Ring (MAG_Radiant_DamageBonusOnIlluminatedTarget_Ring, MapKey: afdcde80-f976-4781-86be-75a5fb0ae05e) | +2 radiant damage vs illuminated targets | Complete - see detailed notes below |
| Coruscation Ring (MAG_Radiant_RadiatingOrb_Ring, MapKey: 3bd041cf-bff5-4464-9002-5c17b957b3c7) | Applies Radiating Orb status on spell damage | Complete - see detailed notes below |
| Gloves of Belligerent Skies (MAG_Thunder_Reverberation_Gloves, MapKey: c987b6e4-adcb-47d6-8dfd-6d4d2f15a381) | Applies Reverberation on Thunder/Lightning/Radiant damage | Complete - see detailed notes below |
| Gloves of Battlemage's Power (MAG_Gish_ArcaneAcuity_Gloves, MapKey: 15381544-e616-46e6-a881-0af793971863) | Applies Arcane Acuity on weapon/unarmed attacks | Complete - see detailed notes below |
| King's Knife (MAG_Duergar_Sword_KingsKnife, MapKey: 025e162a-45ec-4f4c-89da-04d8e8dfe606) | Critical hit bonus (crit on 19-20), reroll low damage, Shadow Blade (advantage in darkness) | Complete - see detailed notes below |
| Cloak of Displacement (MAG_PHB_CloakOfDisplacement_Cloak, MapKey: 257aed3e-370d-40b3-b464-de10257dd82b) | Displacement - attackers have disadvantage, removed when hit, refreshes each turn | Complete - see detailed notes below |
| Shifting Corpus Ring (MAG_FlamingFist_ScoutRing, MapKey: 959e9aa6-b12b-4b71-83b4-0debdf647e9c) | Invisibility and Blur spells (once per long rest each) | Complete - see detailed notes below |
| Stalker Gloves (MAG_Stalker_Gloves, MapKey: dd99248c-fe42-4d07-9861-853e9291ea51) | Seldom Caught Unawares (+1 initiative), Skullduggery Attack (+1d4 Force on Sneak Attack) | Complete - see detailed notes below |
| Radiating Helmet (MAG_Radiant_Radiating_Helmet, MapKey: 5b3c40c5-b0c0-44b5-9b75-e642069fd2cc) | Smite the Graceless - when enemies miss you, they take 1d4 radiant (DEX 14 save) and get Radiating Orb | Complete - see detailed notes below |
| Ring of Regeneration (MAG_PHB_OfRegeneration_Ring, MapKey: d6ee2594-7373-4fed-a167-f9d95cb4ecfd) | Combat Regeneration - regain 1d4 HP at start of each turn while in combat | Complete - see detailed notes below |

---

## Detailed Research: Blood of Lathander

The Blood of Lathander mace (CRE_BloodOfLathander) is a Legendary weapon with interesting spell and passive implementations.

### Weapon Definition (Weapon.txt)
```
new entry "CRE_BloodOfLathander"
type "Weapon"
using "WPN_Mace_2"
data "RootTemplate" "96a35552-0c05-4df0-9974-2a8f142e4be6"
data "Rarity" "Legendary"
data "DefaultBoosts" "WeaponEnchantment(3);WeaponProperty(Magical)"
data "Boosts" "UnlockSpell(Zone_MAG_BloodOfLathander_Sunbeam)"
data "PassivesOnEquip" "CRE_LathandersBlessing_Passive;CRE_LathandersLight_Passive;CRE_LathandersBlessing_Cooldown_Passive"
data "StatusOnEquip" "MAG_LATHANDERS_LIGHT_TECHNICAL"
```

### Sunbeam Spell (Spell_Zone.txt)
```
new entry "Zone_MAG_BloodOfLathander_Sunbeam"
type "SpellData"
data "SpellType" "Zone"
using "Zone_Sunbeam"
data "Cooldown" "OncePerRestPerItem"
data "UseCosts" "ActionPoint:1"
```

### Lathander's Light Passive (Passive.txt)
A toggled passive that applies an aura status. Uses ToggledDefaultOn so it's active by default.
```
new entry "CRE_LathandersLight_Passive"
type "PassiveData"
data "Properties" "ToggledDefaultOn;ToggledDefaultAddToHotbar;IsToggled"
data "ToggleOnFunctors" "ApplyStatus(MAG_LATHANDERS_LIGHT, 100, -1)"
data "ToggleOffFunctors" "RemoveStatus(MAG_LATHANDERS_LIGHT)"
```

### Lathander's Light Status (Status_BOOST.txt)
The aura status that blinds Fiends and Undead within 6m radius.
```
new entry "MAG_LATHANDERS_LIGHT"
type "StatusData"
data "StatusType" "BOOST"
data "AuraRadius" "6"
data "AuraStatuses" "TARGET:IF(Combat() and Character() and Enemy() and (Tagged('FIEND') or Tagged('UNDEAD') or Tagged('UNDEAD_BEAST'))):ApplyStatus(MAG_LATHANDERS_LIGHT_BLIND_AURA_TARGET, 100, -1);YOURSELVES:YOURSELVES:ApplyStatus(MAG_LATHANDERS_LIGHT_SELF,100,-1)"
data "Boosts" "GameplayLight(6,false,0.1,true)"
```

### Key Techniques Demonstrated
1. **Toggled Passives**: Use `Properties "ToggledDefaultOn;ToggledDefaultAddToHotbar;IsToggled"` with `ToggleOnFunctors`/`ToggleOffFunctors`
2. **Aura-Based Status**: Use `AuraRadius` and `AuraStatuses` with conditional targeting (Combat(), Tagged(), Enemy())
3. **Conditional Aura Targets**: `IF(Combat() and Character() and Enemy() and Tagged('FIEND'))` filters who receives aura effects
4. **Gameplay Light**: `GameplayLight(6,false,0.1,true)` emits light from the character

---

## Detailed Research: Moon Lantern

The Moon Lantern (Quest_GLO_Moonlantern) is a quest item that provides protection from the Shadow Curse via a 13m aura effect.

### Item Definition (Weapon.txt)
```
new entry "Quest_GLO_Moonlantern"
type "Weapon"
using "WPN_Torch"
data "RootTemplate" "9aca1109-a59d-47d3-8f35-f248b70518f9"
data "ValueScale" "1"
data "StatusOnEquip" "SCL_MOONLANTERN_TECHNICAL"
data "VersatileDamage" "1d6"
data "Weapon Properties" "Melee;Light;AddToHotbar;Versatile;Unstowable;Torch"
data "UniqueWeaponSoundSwitch" "MoonLantern"
```

### Moonshield Aura Status (Status_BOOST.txt)
The main aura status that protects from Shadow Curse. Note: The aura is applied via story scripting, not via StatusOnEquip.
```
new entry "SCL_MOONSHIELD_AURA"
type "StatusData"
data "StatusType" "BOOST"
data "DisplayName" "hd6bd135bg4531g4124g9e22gfb187fe3b715;1"
data "Icon" "statIcons_Moonshield"
data "StackId" "SCL_MOONSHIELD_AURA"
data "AuraRadius" "13"
data "AuraStatuses" "TARGET:IF((Character() or Tagged('SPELLLIGHTOBJECT')) and not Tagged('SHADOW') and (not Tagged('ACT2_SHADOW_CURSE_IMMUNE') or HasStatus('SCL_MOONSHIELD'))):ApplyStatus(SCL_MOONSHIELD,100,-1)"
data "AuraFlags" "IgnoreItems"
data "Boosts" "GameplayLight(9,false,0.1)"
data "StatusPropertyFlags" "IgnoreResting"
data "StatusEffect" "fbe9316d-b39f-4a38-8bef-79787ee2602f"
```

### Moonshield Protection Status (Status_BOOST.txt)
The status applied to characters within the aura range.
```
new entry "SCL_MOONSHIELD"
type "StatusData"
data "StatusType" "BOOST"
data "DisplayName" "h038b8505gf443g4003gb5f7g9ce3f2dbc1cc;2"
data "Description" "h532e2155gd26bg4152g9599gcacb1139e316;2"
data "Icon" "statIcons_Moonshield"
data "StackId" "SCL_SAFE"
data "StackPriority" "10"
data "StackType" "Ignore"
data "Boosts" "Tag(ACT2_SHADOW_CURSE_IMMUNE)"
data "StatusPropertyFlags" "DisableCombatlog;DisableOverhead"
data "StatusEffect" "06b6b0a5-22a1-4c5a-ae8f-2d31595c5fee"
```

### Pixie's Blessing (Status_BOOST.txt)
Variant of Moonshield applied when the Pixie is freed.
```
new entry "GLO_PIXIESHIELD"
type "StatusData"
data "StatusType" "BOOST"
using "SCL_MOONSHIELD"
data "DisplayName" "hb52f28cbgfd85g4ae9gb906g2d2bdd1eede1;1"
data "Description" "h43f81dd2g0527g4cd9g95ccg50ff7d133646;1"
data "StackId" "SCL_SAFE"
data "StackPriority" "20"
data "StatusPropertyFlags" "DisableCombatlog;DisableOverhead;IgnoreResting"
```

### Key Techniques Demonstrated
1. **Aura-Based Protection**: Use `AuraRadius` and `AuraStatuses` to apply protection to nearby allies
2. **Conditional Aura Targeting**: `IF((Character() or Tagged('SPELLLIGHTOBJECT')) and not Tagged('SHADOW'))` filters valid targets
3. **Tag-Based Immunity**: `Boosts "Tag(ACT2_SHADOW_CURSE_IMMUNE)"` grants immunity via game tag
4. **Gameplay Light**: `GameplayLight(9,false,0.1)` emits light in a 9m radius
5. **Story-Driven Application**: The aura is applied via story scripting, not direct StatusOnEquip

### Using Moonshield in Custom Items
To create a custom item with moonshield-like aura:
1. Create a custom aura status using SCL_MOONSHIELD_AURA as reference
2. Either use StatusOnEquip to apply directly, OR
3. Create a toggled passive (like Lathander's Light) to toggle the aura on/off

Example toggled passive approach:
```
new entry "MY_Moonshield_Passive"
type "PassiveData"
data "Properties" "ToggledDefaultOn;ToggledDefaultAddToHotbar;IsToggled"
data "ToggleOnFunctors" "ApplyStatus(SCL_MOONSHIELD_AURA, 100, -1)"
data "ToggleOffFunctors" "RemoveStatus(SCL_MOONSHIELD_AURA)"
```

---

## Detailed Research: Cloak of the Weave

The Cloak of the Weave (MAG_EndGameCaster_Cloak) is a VeryRare cloak with two powerful caster abilities: Arcane Enchantment and Absorb Elements.

### Item Definition (Armor.txt)
```
new entry "MAG_EndGameCaster_Cloak"
type "Armor"
using "ARM_Cloak_Long_B"
data "RootTemplate" "58c9bc94-b0ac-4ab9-a005-28cc445186f8"
data "ValueUUID" "c5ad02e9-b4d4-4df1-a9cd-02b80d017eaa"
data "Rarity" "VeryRare"
data "PassivesOnEquip" "MAG_ArcaneEnchantment_Lesser_Passive;Absorb_Elements_Passive"
data "Unique" "1"
```

### Arcane Enchantment Passive (Passive.txt)

There are three tiers of this passive:

**Lesser (+1):**
```
new entry "MAG_ArcaneEnchantment_Lesser_Passive"
type "PassiveData"
using "MAG_ArcaneEnchantment_Passive"
data "DescriptionParams" "1"
data "Boosts" "SpellSaveDC(1);RollBonus(MeleeSpellAttack, 1);RollBonus(RangedSpellAttack,1)"
```

**Standard (+2):**
```
new entry "MAG_ArcaneEnchantment_Passive"
type "PassiveData"
data "DisplayName" "h181f9246g612ag484cg99c2g57ca3e4ffcb5;3"
data "Description" "h6a7f9b37g7213g4328g9bceg352bf62c1c31;4"
data "DescriptionParams" "2"
data "Boosts" "SpellSaveDC(2);RollBonus(MeleeSpellAttack, 2);RollBonus(RangedSpellAttack,2)"
```

**Legendary (+3):**
```
new entry "MAG_Legendary_ArcaneEnchantment_Passive"
type "PassiveData"
using "MAG_ArcaneEnchantment_Passive"
data "DescriptionParams" "3"
data "Boosts" "SpellSaveDC(3);RollBonus(MeleeSpellAttack, 3);RollBonus(RangedSpellAttack,3)"
```

### Absorb Elements Passive (Passive.txt)

The passive unlocks an interrupt (reaction) ability:
```
new entry "Absorb_Elements_Passive"
type "PassiveData"
data "DisplayName" "h867c957ag5de7g4ae9gbaf3g443e3cfffd6e;2"
data "Description" "h2de0dccag2991g4e2fg8c14g852929b0d62e;4"
data "DescriptionParams" "1d6"
data "Icon" "PassiveFeature_AbsorbElements"
data "Boosts" "UnlockInterrupt(Interrupt_AbsorbElements)"
```

### Absorb Elements Interrupt (Interrupt.txt)

The actual reaction ability that triggers when taking elemental damage:
```
new entry "Interrupt_AbsorbElements"
type "InterruptData"
using "Interrupt_DampenElements"
data "DisplayName" "h061f2c2ag7fe0g4eafg8b0dg3a108ace358b;1"
data "Description" "h765aa8fbg842ag4baag9b89g352140c0b860;3"
data "DescriptionParams" "1d6"
data "Icon" "PassiveFeature_AbsorbElements"
data "InterruptContextScope" "Self"
data "Conditions" "IsAbleToReact(context.Observer) and Self(context.Target,context.Observer) and (SpellDamageTypeIs(DamageType.Acid) or SpellDamageTypeIs(DamageType.Cold) or SpellDamageTypeIs(DamageType.Fire) or SpellDamageTypeIs(DamageType.Lightning) or SpellDamageTypeIs(DamageType.Thunder)) and not AnyEntityIsItem()"
data "Properties" "SetDamageResistance(Acid);SetDamageResistance(Cold);SetDamageResistance(Fire);SetDamageResistance(Lightning);SetDamageResistance(Thunder);ApplyStatus(OBSERVER_TARGET, ABSORB_ELEMENTS_ACTIVE,100,1)"
data "Cost" "ReactionActionPoint:1;Interrupt_AbsorbElements:1"
data "Cooldown" "OncePerShortRestPerItem"
data "EnableCondition" "(not HasStatus('SG_Polymorph') or Tagged('MINDFLAYER') or HasStatus('SG_Disguise')) and HasActionResource('Interrupt_AbsorbElements', 1, 0, false, false, context.Source)"
data "EnableContext" "OnActionResourcesChanged"
```

### Absorb Elements Active Status (Status_BOOST.txt)

The status applied after using the reaction (adds damage to next melee attack):
```
new entry "ABSORB_ELEMENTS_ACTIVE"
type "StatusData"
data "StatusType" "BOOST"
data "DisplayName" "h7c893f57gccd6g4623g99d2gb49450694b76;2"
data "Description" "hdf20dec9g0a4eg4202g9d6eg0ff791eb9526;2"
data "DescriptionParams" "1d6"
data "Icon" "PassiveFeature_AbsorbElements"
data "StackId" "ABSORB_ELEMENTS_ACTIVE"
data "StatusPropertyFlags" "DisableOverhead;DisableCombatlog;DisablePortraitIndicator"
```

### Key Techniques Demonstrated

1. **Spell Save DC Bonus**: Use `SpellSaveDC(X)` to increase spell save DC
2. **Spell Attack Bonus**: Use `RollBonus(MeleeSpellAttack, X)` and `RollBonus(RangedSpellAttack, X)` for spell attack bonuses
3. **Unlocking Interrupts**: Use `UnlockInterrupt(InterruptName)` in a passive to grant reaction abilities
4. **Interrupt Conditions**: Check damage types with `SpellDamageTypeIs(DamageType.Fire)` etc.
5. **Damage Resistance via Interrupt**: Use `SetDamageResistance(DamageType)` in interrupt Properties
6. **Tiered Passives**: Create multiple versions using `using` to inherit from base passive

### Using These Effects in Custom Items

**To add Arcane Enchantment:**
```
data "PassivesOnEquip" "MAG_ArcaneEnchantment_Lesser_Passive"  // +1
data "PassivesOnEquip" "MAG_ArcaneEnchantment_Passive"         // +2
data "PassivesOnEquip" "MAG_Legendary_ArcaneEnchantment_Passive" // +3
```

**To add Absorb Elements:**
```
data "PassivesOnEquip" "Absorb_Elements_Passive"
```

Note: The Cloak of the Weave uses the Elemental Gish cloak (MAG_ElementalGish_AbsorbElements_Cloak) has additional passives for resource management.

---

## Detailed Research: Magical Durability

The Magical Durability passive grants a bonus to saving throws specifically against spells. Found on several items including the Infernal Rapier's Helm (QUEST_HAV_InfernalReward_002).

### Source Item: MAG_Lesser_Infernal_Metal_Helmet (Armor.txt)
```
new entry "MAG_Lesser_Infernal_Metal_Helmet"
type "Armor"
using "_Head_Magic_Metal"
data "RootTemplate" "2b69a73f-0d1b-4514-bdae-5565a8045e26"
data "ValueUUID" "a229f048-70b0-4b0c-88cb-29b5c6bdb2d0"
data "Rarity" "Rare"
data "Boosts" "RollBonus(SavingThrow, 1, Constitution)"
data "PassivesOnEquip" "MAG_MagicalDurability_Passive"
data "Unique" "1"
```

### Magical Durability Passive (Passive.txt)

There are two tiers of this passive:

**Standard (+2):**
```
new entry "MAG_MagicalDurability_Passive"
type "PassiveData"
data "DisplayName" "h32f3b7bcg3a41g4047ga458g1916b7e1e9ff;2"
data "Description" "h96c18cbfgecdbg49f9ga878g0b4b98062380;2"
data "DescriptionParams" "2"
data "Boosts" "IF(IsSpell()):RollBonus(SavingThrow,2)"
```

**Lesser (+1):**
```
new entry "MAG_Lesser_MagicalDurability_Passive"
type "PassiveData"
using "MAG_MagicalDurability_Passive"
data "DescriptionParams" "1"
data "Boosts" "IF(IsSpell()):RollBonus(SavingThrow,1)"
```

### Key Techniques Demonstrated

1. **Conditional Saving Throw Bonus**: Use `IF(IsSpell()):RollBonus(SavingThrow,X)` to add a bonus to saving throws only against spells
2. **Tiered Passives**: Create multiple versions using `using` to inherit from base passive
3. **IsSpell() Condition**: The `IsSpell()` condition checks if the triggering effect is a spell (as opposed to other abilities)

### Using Magical Durability in Custom Items

**To add Magical Durability:**
```
data "PassivesOnEquip" "MAG_MagicalDurability_Passive"         // +2 vs spells
data "PassivesOnEquip" "MAG_Lesser_MagicalDurability_Passive"  // +1 vs spells
```

### Other Items Using This Passive

- **Helldusk Helmet** (MAG_Infernal_Metal_Helmet) - Uses MAG_MagicalDurability_Passive (+2)
- **Sarevok's Horned Helmet** (UNI_ShadowConcentration_Helmet) - Uses MAG_Lesser_MagicalDurability_Passive (+1)
- **Emperor's Longsword** (LOW_Elfsong_EmperorSword_LongSword) - Uses MAG_MagicalDurability_Passive (+2)

---

## Detailed Research: Callous Glow Ring

The Callous Glow Ring (MAG_Radiant_DamageBonusOnIlluminatedTarget_Ring) adds bonus radiant damage when attacking targets that are illuminated (in bright light).

### Item Definition (Armor.txt)
```
new entry "MAG_Radiant_DamageBonusOnIlluminatedTarget_Ring"
type "Armor"
using "_Ring_Magic"
data "RootTemplate" "afdcde80-f976-4781-86be-75a5fb0ae05e"
data "Rarity" "Uncommon"
data "PassivesOnEquip" "MAG_Radiant_DamageBonusOnIlluminatedTarget_Ring_Passive"
data "Unique" "1"
```

### Callous Glow Passive (Passive.txt)
```
new entry "MAG_Radiant_DamageBonusOnIlluminatedTarget_Ring_Passive"
type "PassiveData"
data "DisplayName" "hdba9745bg03acg4a09ga574gf94a721dce47;2"
data "Description" "h9a6474c3gcb32g406bg9750gc15797688a45;4"
data "DescriptionParams" "2"
data "BoostContext" "OnCreate"
data "Boosts" "IF(HasObscuredState(ObscuredState.Clear, context.Target)):DamageBonus(2, Radiant)"
```

### Key Techniques Demonstrated

1. **Conditional Damage Based on Light**: Use `IF(HasObscuredState(ObscuredState.Clear, context.Target)):DamageBonus(X, DamageType)` to add damage against illuminated targets
2. **ObscuredState Values**:
   - `ObscuredState.Clear` - Target is in bright light (not obscured)
   - `ObscuredState.Lightly` - Target is lightly obscured
   - `ObscuredState.Heavily` - Target is heavily obscured
3. **DamageBonus**: Use `DamageBonus(amount, DamageType)` to add flat damage of a specific type

### Using Illuminated Target Damage in Custom Items

**To add damage vs illuminated targets:**
```
data "PassivesOnEquip" "MAG_Radiant_DamageBonusOnIlluminatedTarget_Ring_Passive"
```

**Or create a custom passive:**
```
new entry "MY_IlluminatedDamage_Passive"
type "PassiveData"
data "DisplayName" "handle;1"
data "Description" "handle;1"
data "DescriptionParams" "3"
data "BoostContext" "OnCreate"
data "Boosts" "IF(HasObscuredState(ObscuredState.Clear, context.Target)):DamageBonus(3, Radiant)"
```

### Synergy Notes

This passive synergizes well with:
- **Light cantrip** - Illuminates targets
- **Daylight spell** - Creates bright light in area
- **Dancing Lights** - Creates light sources
- **Lathander's Light** aura - Illuminates area around wielder
- **Radiating Orb** status - Applied by various radiant items (see Coruscation Ring below)

---

## Detailed Research: Coruscation Ring (Radiating Orb)

The Coruscation Ring (MAG_Radiant_RadiatingOrb_Ring) applies the Radiating Orb debuff to enemies when you damage them with spells. This is part of a set of "Radiant" items that synergize together.

### Item Definition (Armor.txt)
```
new entry "MAG_Radiant_RadiatingOrb_Ring"
type "Armor"
using "_Ring_Magic"
data "RootTemplate" "3bd041cf-bff5-4464-9002-5c17b957b3c7"
data "Rarity" "Uncommon"
data "PassivesOnEquip" "MAG_Radiant_RadiatingOrb_Ring_Passive"
data "Unique" "1"
```

### Radiating Orb Passive (Passive.txt)
```
new entry "MAG_Radiant_RadiatingOrb_Ring_Passive"
type "PassiveData"
data "DisplayName" "h1008416cg7796g48ccgb1fagfcc3c31cd6f7;2"
data "Description" "h069f45d3g7246g488dg9737g876c62ed35a7;4"
data "DescriptionParams" "2"
data "StatsFunctorContext" "OnDamage"
data "Conditions" "IsSpell() and not Item()"
data "StatsFunctors" "ApplyStatus(MAG_RADIANT_RADIATING_ORB, 100, 2);ApplyStatus(MAG_RADIANT_RADIATING_ORB_DURATION_TECHNICAL, 100, 1)"
```

### Radiating Orb Status (Status_BOOST.txt)
```
new entry "MAG_RADIANT_RADIATING_ORB"
type "StatusData"
data "StatusType" "BOOST"
data "DisplayName" "h71e9454cg0dc3g45fega05egd0f72572f419;2"
data "Description" "h30df09d8g9eb9g47f5gb0f6gc4964d40cbc2;9"
data "DescriptionParams" "-1;2"
data "Icon" "statIcons_RadiatingOrb"
data "StackId" "MAG_RADIANT_RADIATING_ORB"
data "StackType" "Additive"
data "Boosts" "RollBonus(Attack,-1);GameplayLight(3,false,0.1)"
data "Passives" "MAG_RadiatingOrb_ReduceDurationPerAttack_Passive"
data "StatusPropertyFlags" "MultiplyEffectsByDuration"
```

### Key Techniques Demonstrated

1. **OnDamage Functor Context**: Use `StatsFunctorContext "OnDamage"` to trigger when dealing damage
2. **Spell-Only Condition**: Use `IsSpell() and not Item()` to trigger only on spell damage (not item effects)
3. **Applying Debuff Status**: Use `ApplyStatus(StatusName, Chance, Duration)` in StatsFunctors
4. **Stacking Debuffs**: Use `StackType "Additive"` to allow stacking, with `StatusPropertyFlags "MultiplyEffectsByDuration"` to multiply the effect by stack count
5. **Attack Penalty**: Use `RollBonus(Attack,-X)` to apply penalty to attack rolls
6. **Illuminate Target**: Use `GameplayLight(radius,false,intensity)` to make the target emit light

### Using Radiating Orb in Custom Items

**To use the vanilla passive:**
```
data "PassivesOnEquip" "MAG_Radiant_RadiatingOrb_Ring_Passive"
```

### Synergy: Radiant Item Set

These items work together for a powerful radiant-themed build:

| Item | Effect |
|------|--------|
| **Coruscation Ring** | Applies Radiating Orb on spell damage |
| **Callous Glow Ring** | +2 radiant damage vs illuminated targets |
| **Luminous Armour** (MAG_Radiant_RadiatingOrb_Armor) | Applies Radiating Orb when dealing radiant damage |
| **Luminous Gloves** (MAG_Radiant_RadiatingOrb_Gloves) | Applies Radiating Orb when dealing radiant damage |
| **Radiating Helmet** (MAG_Radiant_Radiating_Helmet) | Deals radiant damage to Radiating Orb targets |

The Radiating Orb status:
- Applies -1 attack penalty per stack
- Illuminates the target (synergizes with Callous Glow Ring)
- Duration reduces by 2 turns when the affected creature attacks

---

## Detailed Research: Gloves of Belligerent Skies (Reverberation)

The Gloves of Belligerent Skies (MAG_Thunder_Reverberation_Gloves) apply the Reverberation debuff when dealing Thunder, Lightning, or Radiant damage. At 5 stacks, the target takes thunder damage and may be knocked Prone.

### Item Definition (Armor.txt)
```
new entry "MAG_Thunder_Reverberation_Gloves"
type "Armor"
using "_Hand_Magic"
data "RootTemplate" "c987b6e4-adcb-47d6-8dfd-6d4d2f15a381"
data "Rarity" "Uncommon"
data "PassivesOnEquip" "MAG_Thunder_Reverberation_Gloves_Passive"
data "Unique" "1"
```

### Reverberation Passive (Passive.txt)
```
new entry "MAG_Thunder_Reverberation_Gloves_Passive"
type "PassiveData"
data "DisplayName" "h65bd774ag9b29g4d15g8f57gea9f48ff2dc0;3"
data "Description" "h8da1229fgbbf8g41adg90f9g346ca37af828;5"
data "DescriptionParams" "DealDamage(,Thunder);DealDamage(,Lightning);DealDamage(,Radiant);2"
data "Properties" "OncePerAttack"
data "StatsFunctorContext" "OnDamage"
data "Conditions" "IsDamageTypeLightning() or IsDamageTypeThunder() or IsDamageTypeRadiant()"
data "StatsFunctors" "ApplyStatus(MAG_THUNDER_REVERBERATION, 100, 2);ApplyStatus(MAG_THUNDER_REVERBERATION_DURATION_TECHNICAL, 100, 1)"
```

### Reverberation Status (Status_BOOST.txt)
```
new entry "MAG_THUNDER_REVERBERATION"
type "StatusData"
data "StatusType" "BOOST"
data "DisplayName" "h5f13f6bag4a66g499dga57dg5351662d30b5;2"
data "Description" "hc46be560g7bbcg4f89gbfc8g385b958bd8b8;6"
data "DescriptionParams" "5;DealDamage(1d4, Thunder)"
data "Icon" "GenericIcon_Intent_Debuff"
data "StackId" "MAG_THUNDER_REVERBERATION"
data "StackType" "Additive"
data "Boosts" "RollBonus(SavingThrow, -1, Strength);RollBonus(SavingThrow, -1, Dexterity);RollBonus(SavingThrow, -1, Constitution)"
data "Passives" "MAG_Thunder_Reverberation;MAG_Thunder_Reverberation_Blast"
data "StatusPropertyFlags" "MultiplyEffectsByDuration"
```

### Key Techniques Demonstrated

1. **Multiple Damage Type Conditions**: Use `IsDamageTypeLightning() or IsDamageTypeThunder() or IsDamageTypeRadiant()` to trigger on multiple damage types
2. **Once Per Attack**: Use `Properties "OncePerAttack"` to prevent multiple applications per attack
3. **Stacking Debuff with Threshold**: Status stacks additively with `StackType "Additive"`, and passives attached to the status trigger effects at 5 stacks
4. **Physical Saving Throw Penalty**: Use `RollBonus(SavingThrow, -1, AbilityName)` for specific saving throw penalties
5. **Blast on Threshold**: The `MAG_Thunder_Reverberation_Blast` passive triggers when stacks reach 5, dealing 1d4 Thunder damage and potentially knocking Prone (CON DC 10)

### Reverberation Effects Summary

| Stacks | Effect |
|--------|--------|
| Per Stack | -1 to STR, DEX, CON saving throws |
| At 5 Stacks | Deals 1d4 Thunder damage, removes all stacks |
| At 5 Stacks | Target must make CON DC 10 save or be knocked Prone |

### Using Reverberation in Custom Items

**To use the vanilla passive:**
```
data "PassivesOnEquip" "MAG_Thunder_Reverberation_Gloves_Passive"
```

### Synergy: Thunder/Lightning/Radiant Items

These damage types trigger Reverberation:
- **Thunder**: Shatter, Thunderwave, Thunder damage weapons
- **Lightning**: Witch Bolt, Lightning Bolt, Call Lightning
- **Radiant**: Sacred Flame, Guiding Bolt, Spirit Guardians, radiant weapons

Synergizes well with:
- **Callous Glow Ring** - +2 radiant damage vs illuminated (radiant spells trigger both)
- **Coruscation Ring** - Radiating Orb on spell damage
- **The Sparkswall** (shield) - Lightning Charges synergy

---

## Detailed Research: Gloves of Battlemage's Power (Arcane Acuity)

The Gloves of Battlemage's Power (MAG_Gish_ArcaneAcuity_Gloves) apply Arcane Acuity stacks when dealing damage with weapon or unarmed attacks. This is a powerful self-buff for gish (melee spellcaster) builds.

### Item Definition (Armor.txt)
```
new entry "MAG_Gish_ArcaneAcuity_Gloves"
type "Armor"
using "_Hand_Magic_Metal"
data "RootTemplate" "15381544-e616-46e6-a881-0af793971863"
data "ValueUUID" "a229f048-70b0-4b0c-88cb-29b5c6bdb2d0"
data "Rarity" "Rare"
data "PassivesOnEquip" "MAG_Gish_ArcaneAcuity_Gloves_Passive"
data "Unique" "1"
```

### Arcane Acuity Passive (Passive.txt - GustavDev)
```
new entry "MAG_Gish_ArcaneAcuity_Gloves_Passive"
type "PassiveData"
data "DisplayName" "haab50542gb3f3g41c5g9ee9gefb50accc757;3"
data "Description" "hbae6c94bg09c9g45e6ga267gef7984d501be;11"
data "Properties" "OncePerAttack"
data "StatsFunctorContext" "OnDamage"
data "Conditions" "ArcaneAcuityGlovesCondition();"
data "StatsFunctors" "ApplyStatus(SELF, MAG_GISH_ARCANE_ACUITY, 100, 2);ApplyStatus(SELF, MAG_GISH_ARCANE_ACUITY_DURATION_TECHNICAL, 100, 1)"
```

### Arcane Acuity Status (Status_BOOST.txt - SharedDev)
```
new entry "MAG_GISH_ARCANE_ACUITY"
type "StatusData"
data "StatusType" "BOOST"
data "DisplayName" "ha5f07a62g4eefg4ce3gb36egbccbb316e957;2"
data "Description" "h98740ecdg7b6ag49feg8616g1d025bf32624;5"
data "DescriptionParams" "1;2"
data "Icon" "statIcons_ArcaneAcuity"
data "StackId" "MAG_GISH_ARCANE_ACUITY"
data "StackType" "Additive"
data "Boosts" "RollBonus(MeleeSpellAttack,1);RollBonus(RangedSpellAttack, 1);SpellSaveDC(1)"
data "Passives" "MAG_ArcaneAcuity_ReduceDurationPerDamage_Passive"
data "StatusPropertyFlags" "MultiplyEffectsByDuration"
```

### Key Techniques Demonstrated

1. **Self-Buff on Attack**: Use `ApplyStatus(SELF, StatusName, 100, Duration)` to apply buffs to yourself
2. **Built-in Condition Function**: `ArcaneAcuityGlovesCondition()` is a game-defined condition for weapon/unarmed attacks
3. **Stacking Spell Bonuses**: Use `RollBonus(MeleeSpellAttack,X)`, `RollBonus(RangedSpellAttack,X)`, and `SpellSaveDC(X)` with `StackType "Additive"` and `MultiplyEffectsByDuration`
4. **Duration Management**: Technical status (`MAG_GISH_ARCANE_ACUITY_DURATION_TECHNICAL`) manages stack duration refresh

### Arcane Acuity Effects Summary

| Stacks | Effect |
|--------|--------|
| Per Stack | +1 Spell Attack Roll (melee and ranged) |
| Per Stack | +1 Spell Save DC |
| Max Stacks | 10 (caps at +10 to both) |
| Duration | 2 turns, refreshed on new stacks |

### Using Arcane Acuity in Custom Items

**To use the vanilla passive:**
```
data "PassivesOnEquip" "MAG_Gish_ArcaneAcuity_Gloves_Passive"
```

### Related Items

Other items that grant Arcane Acuity:
- **Elixir of Battlemage's Power** - Maintains 3 stacks of Arcane Acuity
- **Circlet of Hunting** (MAG_ElementalGish_ArcaneAcuity_Helmet) - Arcane Acuity on concentration spell damage

### Synergy Notes

This is a key item for "Gish" builds (melee spellcasters) as it rewards:
- Attacking with weapons to build spell power
- Following up with powerful spells at increased DC/attack
- Works especially well with Eldritch Knight, Bladesinger, War Cleric, or Swords Bard

---

## Detailed Research: Shifting Corpus Ring (Invisibility + Blur)

The Shifting Corpus Ring (MAG_FlamingFist_ScoutRing) is a Rare ring that grants both Invisibility and Blur spells.

### Item Definition (Armor.txt - GustavDev)
```
new entry "MAG_FlamingFist_ScoutRing"
type "Armor"
using "_Ring_Magic"
data "RootTemplate" "959e9aa6-b12b-4b71-83b4-0debdf647e9c"
data "ValueUUID" "94356ef2-bb14-4595-88cf-86f544ef12eb"
data "Rarity" "Rare"
data "Boosts" "IF(Tagged('PLAYABLE',context.Source)):UnlockSpell(Target_MAG_FlamingFist_ScoutRing_Invisibility);IF(Tagged('PLAYABLE',context.Source)):UnlockSpell(Shout_MAG_FlamingFist_ScoutRing_Blur)"
data "Unique" "1"
```

### Invisibility Spell (Spell_Target.txt - GustavDev)
```
new entry "Target_MAG_FlamingFist_ScoutRing_Invisibility"
type "SpellData"
data "SpellType" "Target"
using "Target_Invisibility"
data "Cooldown" "OncePerRestPerItem"
data "UseCosts" "ActionPoint:1"
data "Sheathing" "Sheathed"
```

### Blur Spell (Spell_Shout.txt - GustavDev)
```
new entry "Shout_MAG_FlamingFist_ScoutRing_Blur"
type "SpellData"
data "SpellType" "Shout"
using "Shout_Blur"
data "Cooldown" "OncePerRestPerItem"
data "UseCosts" "ActionPoint:1"
data "Sheathing" "Sheathed"
```

### Key Techniques Demonstrated

1. **Conditional Spell Unlock**: Use `IF(Tagged('PLAYABLE',context.Source)):UnlockSpell(...)` to only grant spells to playable characters (not companions/summons)
2. **Item-Specific Spells**: Create custom spell entries using the base spell to set custom cooldowns and costs
3. **Once Per Long Rest**: Use `Cooldown "OncePerRestPerItem"` for long rest cooldowns
4. **Sheathing**: Use `Sheathing "Sheathed"` to allow casting while weapons are sheathed

### Using These Spells in Custom Items

**To add Invisibility (once per long rest):**
```
data "Boosts" "UnlockSpell(Target_MAG_FlamingFist_ScoutRing_Invisibility)"
```

**To add Blur (once per long rest):**
```
data "Boosts" "UnlockSpell(Shout_MAG_FlamingFist_ScoutRing_Blur)"
```

**To create an unlimited bonus action version:**
```
new entry "SMR_Target_Invisibility_Unlimited"
type "SpellData"
data "SpellType" "Target"
using "Target_Invisibility"
data "UseCosts" "BonusActionPoint:1"
```

---

## Detailed Research: Cloak of Displacement

The Cloak of Displacement (MAG_PHB_CloakOfDisplacement_Cloak) is a Rare cloak that grants the Displacement effect - attackers have disadvantage against you until you take damage, then it refreshes at the start of your next turn.

### Item Definition (Armor.txt - GustavDev)
```
new entry "MAG_PHB_CloakOfDisplacement_Cloak"
type "Armor"
using "_Back_Magic"
data "RootTemplate" "257aed3e-370d-40b3-b464-de10257dd82b"
data "ValueUUID" "a229f048-70b0-4b0c-88cb-29b5c6bdb2d0"
data "Rarity" "Rare"
data "PassivesOnEquip" "MAG_PHB_Displacement_Cloak_Passive"
data "StatusOnEquip" "MAG_PHB_CLOAK_OF_DISPLACEMENT_TECHNICAL"
data "Unique" "1"
```

### Displacement Passive (Passive.txt - GustavDev)
The passive is UI-only (shows the power in item tooltip). The actual effect comes from the status.
```
new entry "MAG_PHB_Displacement_Cloak_Passive"
type "PassiveData"
data "DisplayName" "h30dfd004g2e7dg49feg8e91gb062ecaf2520;2"
data "Description" "h22f785a3g6a73g4939gaa55gcd54c9f49a43;3"
```

### Technical Status (Status_BOOST.txt - GustavDev)
Applies the Displacement status at the start of each turn in combat.
```
new entry "MAG_PHB_CLOAK_OF_DISPLACEMENT_TECHNICAL"
type "StatusData"
data "StatusType" "BOOST"
data "DisplayName" "h83f77d95ga2a7g405bgb335gb410d56891ad;1"
data "Description" "h03006389g343cg4dc3gab0fgff9de272e46f;1"
data "StackId" "MAG_PHB_CLOAK_OF_DISPLACEMENT_TECHNICAL"
data "TickType" "StartTurn"
data "TickFunctors" "IF(Combat() and not Dead()):ApplyStatus(MAG_PHB_CLOAK_OF_DISPLACEMENT, 100, 2)"
data "StatusPropertyFlags" "DisableOverhead;DisableCombatlog;DisablePortraitIndicator;IgnoreResting;ApplyToDead"
data "OnRemoveFunctors" "RemoveStatus(MAG_PHB_CLOAK_OF_DISPLACEMENT)"
```

### Displacement Status (Status_BOOST.txt - GustavDev)
The actual Displacement effect - based on BLUR (disadvantage to attackers), removed when hit.
```
new entry "MAG_PHB_CLOAK_OF_DISPLACEMENT"
type "StatusData"
data "StatusType" "BOOST"
using "BLUR"
data "DisplayName" "hf0a2cd38gb975g40ffg9787g99ae6ae1ce58;2"
data "Description" "h957e994cgb2bdg4e97gbe82gad62540534fc;5"
data "SoundStart" "MAG_Status_CloakOfDisplacement_Start"
data "SoundLoop" "MAG_Status_CloakOfDisplacement_MO"
data "SoundStop" "MAG_Status_CloakOfDisplacement_End"
data "StackId" "MAG_PHB_CLOAK_OF_DISPLACEMENT"
data "RemoveConditions" "(IsStatusEvent(StatusEvent.OnAttacked) and IsHit() and not IsCriticalMiss() and TotalAttackDamageDoneGreaterThan(0)) or IsStatusEvent(StatusEvent.OnCombatEnded)"
data "RemoveEvents" "OnCombatEnded;OnAttacked"
data "StatusPropertyFlags" "DisableOverhead"
data "StatusGroups" ""
```

### Key Techniques Demonstrated

1. **Technical Status for Turn-Based Effects**: Use `StatusOnEquip` with a technical status that has `TickType "StartTurn"` and `TickFunctors` to apply effects at start of each turn
2. **Using BLUR as Base**: The `using "BLUR"` gives attackers disadvantage without needing custom boosts
3. **Conditional Removal**: Use `RemoveConditions` with `IsStatusEvent(StatusEvent.OnAttacked) and IsHit() and TotalAttackDamageDoneGreaterThan(0)` to remove when taking damage
4. **Remove Events**: `RemoveEvents "OnCombatEnded;OnAttacked"` specifies when to check RemoveConditions
5. **UI-Only Passive**: Passive with just DisplayName/Description shows in tooltip but actual logic is in status

### Using Displacement in Custom Items

**To use the full Displacement system:**
```
data "PassivesOnEquip" "MAG_PHB_Displacement_Cloak_Passive"
data "StatusOnEquip" "MAG_PHB_CLOAK_OF_DISPLACEMENT_TECHNICAL"
```

**Note:** Both the passive (for UI) and the technical status (for effect) are required.

### Synergy Notes

Displacement synergizes well with:
- **High AC builds** - Fewer attacks hit, Displacement stays active longer
- **Defensive fighting** - Dodge action + Displacement = very hard to hit
- **Shadow Blade** - Advantage in darkness + disadvantage for enemies = strong combo
- **Mirror Image** - Multiple defensive layers

---

## Detailed Research: King's Knife (Shadow Blade + Critical Bonus)

The King's Knife (MAG_Duergar_Sword_KingsKnife) is a VeryRare shortsword with powerful critical hit bonuses and advantage in darkness.

### Item Definition (Weapon.txt - GustavDev)
```
new entry "MAG_Duergar_Sword_KingsKnife"
type "Weapon"
using "WPN_Shortsword_2"
data "RootTemplate" "025e162a-45ec-4f4c-89da-04d8e8dfe606"
data "ValueUUID" "81764c3c-c7a9-49a7-b145-d31ffd5aebe1"
data "Rarity" "VeryRare"
data "PassivesOnEquip" "MAG_TheClover_Rearrangement_Passive;ShadowBlade_Passive"
data "Unique" "1"
```

### Shadow Blade Passive (Passive.txt - GustavDev)
Grants advantage on melee weapon attacks when not in bright light (darkness or dim light).
```
new entry "ShadowBlade_Passive"
type "PassiveData"
data "DisplayName" "h0160e9efg8974g43d6gb3fcg8d4e9d200a3c;4"
data "Description" "ha672fd65g0fe4g4596g9529gce372c013ca1;6"
data "Boosts" "IF(not HasObscuredState(ObscuredState.Clear) and IsMeleeAttack() and IsWeaponAttack()):Advantage(AttackRoll);"
```

### The Clover Rearrangement Passive (Passive.txt - GustavDev)
Reduces critical hit threshold by 1 (crit on 19-20) and rerolls damage dice of 2 or lower.
```
new entry "MAG_TheClover_Rearrangement_Passive"
type "PassiveData"
data "DisplayName" "h15c46cc7g164fg41ffga02ege59329268c58;2"
data "Description" "h6984b8aagbb23g46b3g8c29g1a65974e4bcb;4"
data "DescriptionParams" "2;19;18"
data "Boosts" "ReduceCriticalAttackThreshold(1);IF(AttackingWithMeleeWeapon(context.Source)):Reroll(Damage,2,true)"
```

### Key Techniques Demonstrated

1. **Reduce Critical Threshold**: Use `ReduceCriticalAttackThreshold(X)` to lower the number needed for a critical hit (1 = crit on 19-20, 2 = crit on 18-20)
2. **Damage Reroll**: Use `Reroll(Damage,X,true)` to reroll damage dice that are X or lower (the `true` keeps the new roll even if lower)
3. **Conditional Advantage Based on Light**: Use `IF(not HasObscuredState(ObscuredState.Clear)):Advantage(AttackRoll)` for advantage when not in bright light
4. **ObscuredState Check**: `HasObscuredState(ObscuredState.Clear)` returns true when in bright light; negating it gives advantage in dim/dark conditions

### Using These Effects in Custom Items

**To add Shadow Blade:**
```
data "PassivesOnEquip" "ShadowBlade_Passive"
```

**To add Critical Hit Bonus + Damage Reroll:**
```
data "PassivesOnEquip" "MAG_TheClover_Rearrangement_Passive"
```

**To create a custom critical threshold passive:**
```
new entry "MY_CritBonus_Passive"
type "PassiveData"
data "DisplayName" "handle;1"
data "Description" "handle;1"
data "Boosts" "ReduceCriticalAttackThreshold(2)"
```

### Synergy Notes

Shadow Blade synergizes well with:
- **Darkness spell** - Creates darkness for advantage
- **Devil's Sight** - See in magical darkness while getting advantage
- **Skulker feat** - Better stealth in dim light
- **Gloom Stalker Ranger** - Bonuses in darkness

The critical hit bonus synergizes with:
- **Champion Fighter** - Improved Critical stacks (crit on 18-20 becomes 17-20)
- **Savage Attacker** - Reroll all damage dice once per turn
- **Great Weapon Master** - Bonus action attack on crit
- **Assassin Rogue** - Auto-crit on surprised targets

---

## Detailed Research: Stalker Gloves (Initiative + Sneak Attack Bonus)

The Stalker Gloves (MAG_Stalker_Gloves) are Rare gloves that grant an initiative bonus and extra Force damage on Sneak Attacks.

### Item Definition (Armor.txt - GustavDev)
```
new entry "MAG_Stalker_Gloves"
type "Armor"
using "ARM_Gloves_Leather"
data "RootTemplate" "dd99248c-fe42-4d07-9861-853e9291ea51"
data "ValueUUID" "a229f048-70b0-4b0c-88cb-29b5c6bdb2d0"
data "Rarity" "Rare"
data "PassivesOnEquip" "MAG_InitiativeBonus_1_Passive;MAG_ForcefulSneakAttack_Passive"
data "Unique" "1"
```

### Seldom Caught Unawares Passive (Passive.txt - GustavDev)
Grants a +1 bonus to initiative rolls.
```
new entry "MAG_InitiativeBonus_1_Passive"
type "PassiveData"
data "DisplayName" "h72f85fe9g3f50g4cafg9e54g7f9c8542cd7b;1"
data "Description" "hd96c976bg61c0g4804g8000g839a4826b923;1"
data "DescriptionParams" "1"
data "Boosts" "Initiative(1)"
```

There's also a +2 version:
```
new entry "MAG_InitiativeBonus_2_Passive"
type "PassiveData"
using "MAG_InitiativeBonus_1_Passive"
data "DescriptionParams" "2"
data "Boosts" "Initiative(2)"
```

### Skullduggery Attack Passive (Passive.txt - GustavDev)
Adds 1d4 Force damage when dealing Sneak Attack damage.
```
new entry "MAG_ForcefulSneakAttack_Passive"
type "PassiveData"
data "DisplayName" "h5593a398g9a3bg4272gaf2cga94278f772cd;1"
data "Description" "hfa1c8818g9301g48afgba5ege06d5bd04fbf;1"
data "DescriptionParams" "DealDamage(1d4, Force)"
data "StatsFunctorContext" "OnDamage"
data "Conditions" "SpellId('Target_SneakAttack') or SpellId('Projectile_SneakAttack') or SpellId('Interrupt_SneakAttack')"
data "StatsFunctors" "DealDamage(1d4, Force,Magical)"
```

### Key Techniques Demonstrated

1. **Initiative Bonus**: Use `Initiative(X)` boost to add to initiative rolls
2. **Conditional Damage on Specific Spells**: Use `SpellId('SpellName')` in Conditions to trigger only on specific abilities
3. **OnDamage Context**: Use `StatsFunctorContext "OnDamage"` to trigger when dealing damage
4. **Multiple Spell Conditions**: Chain spell checks with `or` to trigger on any matching spell (Target, Projectile, or Interrupt versions of Sneak Attack)

### Using These Effects in Custom Items

**To add Initiative Bonus:**
```
data "PassivesOnEquip" "MAG_InitiativeBonus_1_Passive"  // +1
data "PassivesOnEquip" "MAG_InitiativeBonus_2_Passive"  // +2
```

**To add Sneak Attack Force Damage:**
```
data "PassivesOnEquip" "MAG_ForcefulSneakAttack_Passive"
```

### Synergy Notes

These effects synergize well with:
- **Rogue builds** - Sneak Attack is core to Rogue
- **Assassin Rogue** - Going first in combat ensures surprised targets for auto-crits
- **Alert feat** - Stacks with initiative bonus
- **Gloom Stalker Ranger** - Dread Ambusher adds initiative bonus from Wisdom

---

## Detailed Research: Radiating Helmet (Smite the Graceless)

The Radiating Helmet (MAG_Radiant_Radiating_Helmet) is an Uncommon helmet that punishes enemies who miss their attacks against you.

### Item Definition (Armor.txt - GustavDev)
```
new entry "MAG_Radiant_Radiating_Helmet"
type "Armor"
using "_Head_Magic_Metal"
data "RootTemplate" "5b3c40c5-b0c0-44b5-9b75-e642069fd2cc"
data "Rarity" "Uncommon"
data "PassivesOnEquip" "MAG_Radiant_Radiating_Helmet_Passive"
data "Unique" "1"
```

### Smite the Graceless Passive (Passive.txt - GustavDev)
Triggers when an enemy misses you, applying a damaging status to them.
```
new entry "MAG_Radiant_Radiating_Helmet_Passive"
type "PassiveData"
data "DisplayName" "h283a1588g015fg46cag9579g559f2a99c6b6;2"
data "Description" "h875596dcg27d8g4878gae8cgafe9cbd4dc57;5"
data "DescriptionParams" "DealDamage(1d4, Radiant)"
data "StatsFunctorContext" "OnAttacked"
data "Conditions" "IsMiss() or IsCriticalMiss()"
data "StatsFunctors" "ApplyStatus(SWAP, MAG_SMITE_THE_GRACELSS_DAMAGE, 100, 0)"
```

### Smite the Graceless Status (Status_BOOST.txt - GustavDev)
The status applied to the attacker - forces a DEX save or take radiant damage and Radiating Orb.
```
new entry "MAG_SMITE_THE_GRACELSS_DAMAGE"
type "StatusData"
data "StatusType" "BOOST"
data "DisplayName" "h08c593e4gef4ag490cgb755gb0cd54c856c0;2"
data "StatusPropertyFlags" "DisableOverhead;DisablePortraitIndicator;DisableCombatlog"
data "OnApplyRoll" "not SavingThrow(Ability.Dexterity, 14)"
data "OnApplySuccess" "DealDamage(1d4, Radiant,Magical);ApplyStatus(MAG_RADIANT_RADIANT_BLAST_TECHNICAL, 100, 0)"
```

### Key Techniques Demonstrated

1. **OnAttacked Context**: Use `StatsFunctorContext "OnAttacked"` to trigger when being attacked
2. **Miss Detection**: Use `IsMiss() or IsCriticalMiss()` in Conditions to trigger only on missed attacks
3. **SWAP Target**: Use `ApplyStatus(SWAP, ...)` to apply status to the attacker instead of self
4. **OnApplyRoll Save**: Use `OnApplyRoll "not SavingThrow(Ability.Dexterity, DC)"` to require a save before effect
5. **OnApplySuccess**: Use `OnApplySuccess` to define what happens when the target fails the save

### Using Smite the Graceless in Custom Items

**To use the vanilla passive:**
```
data "PassivesOnEquip" "MAG_Radiant_Radiating_Helmet_Passive"
```

### Synergy Notes

This passive synergizes well with:
- **High AC builds** - More misses = more procs
- **Radiating Orb items** - Stacks with other sources of Radiating Orb
- **Callous Glow Ring** - Enemies with Radiating Orb are illuminated, triggering bonus radiant damage
- **Shield spell** - Emergency AC boost causes more misses

---

## Detailed Research: Ring of Regeneration (Combat Regeneration)

The Ring of Regeneration (MAG_PHB_OfRegeneration_Ring) is a Rare ring that grants 1d4 HP regeneration at the start of each turn while in combat.

### Item Definition (Armor.txt - GustavDev)
```
new entry "MAG_PHB_OfRegeneration_Ring"
type "Armor"
using "ARM_Ring_B_Gold_A"
data "RootTemplate" "d6ee2594-7373-4fed-a167-f9d95cb4ecfd"
data "Rarity" "Rare"
data "PassivesOnEquip" "MAG_PHB_OfRegeneration_Ring_Passive"
data "StatusOnEquip" "MAG_PHB_RING_OF_REGENERATION_TECHNICAL"
data "Unique" "1"
```

### Combat Regeneration Passive (Passive.txt - GustavDev)
The passive is UI-only (shows the power in item tooltip). The actual healing comes from the status.
```
new entry "MAG_PHB_OfRegeneration_Ring_Passive"
type "PassiveData"
data "DisplayName" "hf38111b1ge9afg4034ga7cbg86406451dfa1;2"
data "Description" "hdfdc93dfg4eabg4da2ga445g7eb95fb47125;2"
data "DescriptionParams" "RegainHitPoints(1d4)"
```

### Technical Status (Status_BOOST.txt - GustavDev)
Heals 1d4 HP at the start of each turn in combat.
```
new entry "MAG_PHB_RING_OF_REGENERATION_TECHNICAL"
type "StatusData"
data "StatusType" "BOOST"
data "DisplayName" "h20ce355fg294dg449bg9642g668c54aad2b1;1"
data "StackId" "MAG_PHB_RING_OF_REGENERATION_TECHNICAL"
data "TickType" "StartTurn"
data "TickFunctors" "IF(not HasStatus('DOWNED') and not Dead() and Combat()):RegainHitPoints(1d4)"
data "StatusPropertyFlags" "DisableOverhead;DisableCombatlog;DisablePortraitIndicator;IgnoreResting;ApplyToDead"
```

### Key Techniques Demonstrated

1. **StartTurn Healing**: Use `TickType "StartTurn"` with `TickFunctors` to heal at the start of each turn
2. **Combat-Only Effect**: Use `Combat()` condition to only heal during combat
3. **Safety Checks**: Use `not HasStatus('DOWNED') and not Dead()` to prevent healing when downed or dead
4. **UI-Only Passive**: Passive with just DisplayName/Description/DescriptionParams shows in tooltip but actual logic is in status
5. **Hidden Status**: Use `StatusPropertyFlags "DisableOverhead;DisableCombatlog;DisablePortraitIndicator"` to hide status from UI

### Using Combat Regeneration in Custom Items

**To add Combat Regeneration (1d4/turn):**
```
data "PassivesOnEquip" "MAG_PHB_OfRegeneration_Ring_Passive"
data "StatusOnEquip" "MAG_PHB_RING_OF_REGENERATION_TECHNICAL"
```

**Note:** Both the passive (for UI) and the technical status (for effect) are required.

### Related Status: Helm of Balduran Regeneration

The Helm of Balduran uses a similar system but heals 2 HP (flat) instead of 1d4:
```
new entry "MAG_HELM_OF_BALDURAN_REGENERATION"
type "StatusData"
using "MAG_PHB_RING_OF_REGENERATION_TECHNICAL"
data "DisplayName" "h06ccd815gad40g4e35gac8bg209888989b3c;1"
data "StackId" "MAG_HELM_OF_BALDURAN_REGENERATION"
data "TickFunctors" "IF(not HasStatus('DOWNED') and not Dead() and Combat()):RegainHitPoints(2)"
```

### Synergy Notes

Combat Regeneration synergizes well with:
- **High HP pools** - Small healing adds up over long fights
- **Defensive builds** - Taking less damage makes healing more impactful
- **Amulet of Greater Health** - More HP to regenerate
- **Heavy Armor Master** - Reduce incoming damage, regeneration keeps you topped off

---

## Sources

- BapeerySpiritShoes mod - Spirit Guardians on boots
- Whimsical Wares mod - Various passives and spells
- Vanilla game items - Extracted via unpacking

