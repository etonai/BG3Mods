# Phase 015 - Longsword of Tyr Enhancements

**Status:** PENDING

## Goal
- Research and implement upgrading the Longsword of Tyr from +2 to +5 weapon
- Add Tyr's Protection ability (from Sword of Justice)

---

## Item 1: Research - Upgrading Sword of Tyr to +5

### Overview
The Sword of Tyr currently uses `WPN_Longsword_2` as its base, which is a +2 longsword. We want to upgrade it to be a +5 weapon for maximum power.

### Research Questions

1. **How are weapon bonuses defined in BG3?**
   - Is it through the base weapon template (WPN_Longsword_2)?
   - Is it through Boosts like `WeaponEnchantment(5)`?
   - Is it through a combination of both?

2. **What base weapon templates exist?**
   - Does `WPN_Longsword_3`, `WPN_Longsword_4`, or `WPN_Longsword_5` exist?
   - What are the differences between weapon tier templates?

3. **Can we override the enchantment level?**
   - Can we use `using "WPN_Longsword_2"` but add `WeaponEnchantment(5)` boost?
   - Would this stack or override the base +2?

4. **How do existing legendary weapons handle this?**
   - Look at high-tier vanilla weapons for examples
   - Check if any weapons use explicit WeaponEnchantment boosts

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

### Research Tasks

- [ ] Search for WeaponEnchantment boost usage in vanilla game files
- [ ] Find examples of +3 or higher weapons
- [ ] Determine if enchantment can be set via Boosts field
- [ ] Test implementation approach

### Research Results

*(To be filled in after research)*

---

## Item 2: Tyr's Protection Addition

### Overview
Add Tyr's Protection from the vanilla Sword of Justice to the Longsword of Tyr.

**Reference:** Vanilla Sword of Justice (UNI_PLA_WPN_SwordOfJustice, MapKey: 455383a5-1211-4500-85f9-b71fad3fbf15)

### Research Tasks

- [ ] Find Tyr's Protection spell/ability in gustav
- [ ] Determine the internal name and implementation

### Research Results

*(To be filled in after research)*

---

## Implementation Checklist

### Research
- [ ] Complete weapon enchantment research
- [ ] Document findings
- [ ] Find Tyr's Protection implementation in gustav

### Longsword of Tyr Enhancement
- [ ] Update SMR_Sword_Tyr in Weapon.txt with +5 enchantment
- [ ] Add Tyr's Protection to Longsword of Tyr

### Final
- [ ] Build and test mod

---

## Test Plan

### Sword of Tyr +5
- [ ] Load game with mod enabled
- [ ] Equip Sword of Tyr
- [ ] Check weapon tooltip shows +5 bonus to attack and damage
- [ ] Verify attack rolls include +5 modifier
- [ ] Verify damage rolls include +5 modifier

---

## Notes

*(To be added during implementation)*
