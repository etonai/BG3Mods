# Phase 023 - Thief Items

**Status:** COMPLETE

## Goal
- Create thief-themed magical items with shadow and critical hit powers
- At least one longsword
- At least one piece of light armor
- One cloak (using Cloak of Displacement appearance)

---

## Item 1: Rogueblade

### Item Details

| Aspect | Value |
|--------|-------|
| Name | Rogueblade |
| Internal ID | SMR_Rogueblade |
| Base Type | WPN_Longsword_2 |
| ParentTemplateId | d116f35c-4399-408c-ba90-b455a5d29a1f (WPN_HUM_Longsword_Adamantine_A) |
| Rarity | Legendary |
| Unique | Yes |

### Planned Powers

| Power | Source | Effect |
|-------|--------|--------|
| +5 Enchantment | DefaultBoosts | WeaponEnchantment(5);WeaponProperty(Magical) |
| Shadow Blade | ShadowBlade_Passive | Advantage on melee attacks when not in bright light |
| Critical Bonus | MAG_TheClover_Rearrangement_Passive | Crit on 19-20, reroll damage dice of 2 or lower |
| TBD | TBD | TBD |

---

## Item 2: Armor of the Rogue

### Item Details

| Aspect | Value |
|--------|-------|
| Name | Armor of the Rogue |
| Internal ID | SMR_Armor_Rogue |
| Base Type | ARM_StuddedLeather_Body_2 (+2 base) |
| ParentTemplateId | cab3455f-59fe-42be-8dcd-7cd61149389a (ARM_StuddedLeather_Drow) |
| Rarity | Legendary |
| Unique | Yes |

### Planned Powers

| Power | Source | Effect |
|-------|--------|--------|
| +5 Enchantment | Boosts | AC(3) (added to +2 base = +5 total) |
| Displacement | MAG_PHB_Displacement_Cloak_Passive + MAG_PHB_CLOAK_OF_DISPLACEMENT_TECHNICAL | Attackers have disadvantage, removed when hit, refreshes each turn |
| TBD | TBD | TBD |

---

## Item 3: Cloak of the Rogue

### Item Details

| Aspect | Value |
|--------|-------|
| Name | Cloak of the Rogue |
| Internal ID | SMR_Cloak_Rogue |
| Base Type | _Back_Magic |
| ParentTemplateId | 257aed3e-370d-40b3-b464-de10257dd82b (Cloak of Displacement appearance) |
| Rarity | Legendary |
| Unique | Yes |

### Planned Powers

| Power | Source | Effect |
|-------|--------|--------|
| Invisibility (Unlimited) | SMR_Target_Invisibility_Unlimited | Cast Invisibility as bonus action, unlimited |
| TBD | TBD | TBD |

### Custom Spell: SMR_Target_Invisibility_Unlimited (Spell_Target.txt)
```
new entry "SMR_Target_Invisibility_Unlimited"
type "SpellData"
data "SpellType" "Target"
using "Target_Invisibility"
data "UseCosts" "BonusActionPoint:1"
```

---

## UUIDs and Handles

### Rogueblade
| Type | Value |
|------|-------|
| MapKey/RootTemplate | a1b2c3d4-e5f6-4a7b-8c9d-0e1f2a3b4c5e |
| DisplayName Handle | h9a0b1c2dg3e4fg5a6bg7c8dg9e0f1a2b3c4d5e6;1 |
| Description Handle | h0b1c2d3eg4f5ag6b7cg8d9eg0f1a2b3c4d5e6f7;1 |

### Armor of the Rogue
| Type | Value |
|------|-------|
| MapKey/RootTemplate | b2c3d4e5-f6a7-4b8c-9d0e-1f2a3b4c5d6f |
| DisplayName Handle | h1c2d3e4fg5a6bg7c8dg9e0fg1a2b3c4d5e6f7a8;1 |
| Description Handle | h2d3e4f5ag6b7cg8d9eg0f1ag2b3c4d5e6f7a8b9;1 |

### Cloak of the Rogue
| Type | Value |
|------|-------|
| MapKey/RootTemplate | c3d4e5f6-a7b8-4c9d-0e1f-2a3b4c5d6e70 |
| DisplayName Handle | h3e4f5a6bg7c8dg9e0fg1a2bg3c4d5e6f7a8b9c0;1 |
| Description Handle | h4f5a6b7cg8d9eg0f1ag2b3cg4d5e6f7a8b9c0d1;1 |

### SMR_Target_Invisibility_Unlimited Spell
| Type | Value |
|------|-------|
| DisplayName Handle | h7f8a9b0cg1d2eg3f4ag5b6cg7d8e9f0a1b2c3d4;1 |
| ExtraDescription Handle | h8a9b0c1dg2e3fg4a5bg6c7dg8e9f0a1b2c3d4e5;1 |

---

## Reference: King's Knife Passives

### ShadowBlade_Passive
```
new entry "ShadowBlade_Passive"
type "PassiveData"
data "DisplayName" "h0160e9efg8974g43d6gb3fcg8d4e9d200a3c;4"
data "Description" "ha672fd65g0fe4g4596g9529gce372c013ca1;6"
data "Boosts" "IF(not HasObscuredState(ObscuredState.Clear) and IsMeleeAttack() and IsWeaponAttack()):Advantage(AttackRoll);"
```

### MAG_TheClover_Rearrangement_Passive
```
new entry "MAG_TheClover_Rearrangement_Passive"
type "PassiveData"
data "DisplayName" "h15c46cc7g164fg41ffga02ege59329268c58;2"
data "Description" "h6984b8aagbb23g46b3g8c29g1a65974e4bcb;4"
data "DescriptionParams" "2;19;18"
data "Boosts" "ReduceCriticalAttackThreshold(1);IF(AttackingWithMeleeWeapon(context.Source)):Reroll(Damage,2,true)"
```

---

## Reference: Cloak of Displacement (for Armor)

### MAG_PHB_Displacement_Cloak_Passive (UI only)
```
new entry "MAG_PHB_Displacement_Cloak_Passive"
type "PassiveData"
data "DisplayName" "h30dfd004g2e7dg49feg8e91gb062ecaf2520;2"
data "Description" "h22f785a3g6a73g4939gaa55gcd54c9f49a43;3"
```

### MAG_PHB_CLOAK_OF_DISPLACEMENT_TECHNICAL (applies effect each turn)
```
new entry "MAG_PHB_CLOAK_OF_DISPLACEMENT_TECHNICAL"
type "StatusData"
data "StatusType" "BOOST"
data "StackId" "MAG_PHB_CLOAK_OF_DISPLACEMENT_TECHNICAL"
data "TickType" "StartTurn"
data "TickFunctors" "IF(Combat() and not Dead()):ApplyStatus(MAG_PHB_CLOAK_OF_DISPLACEMENT, 100, 2)"
data "StatusPropertyFlags" "DisableOverhead;DisableCombatlog;DisablePortraitIndicator;IgnoreResting;ApplyToDead"
data "OnRemoveFunctors" "RemoveStatus(MAG_PHB_CLOAK_OF_DISPLACEMENT)"
```

### Usage
Both passive and status are required:
```
data "PassivesOnEquip" "MAG_PHB_Displacement_Cloak_Passive"
data "StatusOnEquip" "MAG_PHB_CLOAK_OF_DISPLACEMENT_TECHNICAL"
```

---

## Implementation Checklist

### Rogueblade
- [x] Generate UUIDs (MapKey, handles)
- [x] Add SMR_Rogueblade to Weapon.txt
- [x] Add RootTemplate to merged.lsx and merged.lsf.lsx
- [x] Add localization entries
- [x] Add OneTimeReward entry

### Armor of the Rogue
- [x] Generate UUIDs (MapKey, handles)
- [x] Add SMR_Armor_Rogue to Armor.txt
- [x] Add RootTemplate to merged.lsx and merged.lsf.lsx (use ARM_StuddedLeather_Drow as ParentTemplateId)
- [x] Add localization entries
- [x] Add OneTimeReward entry

### Cloak of the Rogue
- [x] Decide on additional powers
- [x] Generate UUIDs (MapKey, handles)
- [x] Add SMR_Cloak_Rogue to Armor.txt
- [x] Add RootTemplate to merged.lsx and merged.lsf.lsx (use Cloak of Displacement as ParentTemplateId)
- [x] Add localization entries
- [x] Add OneTimeReward entry
- [x] Add SMR_Target_Invisibility_Unlimited to Spell_Target.txt

### Final
- [ ] Build and test mod

---

## Test Plan

### Rogueblade
- [ ] Check traveler's chest for Rogueblade
- [ ] Verify Shadow Blade grants advantage in dim/dark light
- [ ] Verify critical hits occur on 19-20
- [ ] Verify damage dice of 2 or lower are rerolled

### Armor of the Rogue
- [ ] Check traveler's chest for Armor of the Rogue
- [ ] Verify Displacement grants disadvantage to attackers
- [ ] Verify armor powers function correctly

### Cloak of the Rogue
- [ ] Check traveler's chest for Cloak of the Rogue
- [ ] Verify cloak has Cloak of Displacement appearance
- [ ] Verify Invisibility can be cast as bonus action (unlimited)

---

## Notes

- Shadow Blade passive synergizes with Darkness spell, Devil's Sight, Gloom Stalker
- Critical hit bonus synergizes with Champion Fighter, Assassin Rogue
- Displacement synergizes with high AC, defensive fighting, Shadow Blade (advantage + disadvantage combo)
- Consider adding Celestial Haste to match other legendary weapons

## Known Issues

- ~~**Armor of the Rogue** - Wrong AC bonus (used AC(3) assuming base type had +2 built in)~~ **RESOLVED** - Changed to AC(5) for true +5 bonus
- ~~**Cloak of the Rogue** - Invalid UUID `c3d4e5f6-a7b8-4c9d-0e1f-2a3b4c5d6e7g` contained "g" which is not a valid hex character, causing item to not appear~~ **RESOLVED** (in Phase 24) - Changed to `c3d4e5f6-a7b8-4c9d-0e1f-2a3b4c5d6e70`
