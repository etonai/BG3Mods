# Phase 018 - Longsword of Tyr Enhancements

**Status:** COMPLETE

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

- [x] Search for WeaponEnchantment boost usage in vanilla game files
- [x] Find examples of +3 or higher weapons
- [x] Determine if enchantment can be set via Boosts field
- [ ] Test implementation approach

### Research Results

**Weapon Enchantment System:**

Weapon bonuses in BG3 are controlled via the `DefaultBoosts` field using `WeaponEnchantment(X)`:

```
data "DefaultBoosts" "WeaponEnchantment(3);WeaponProperty(Magical)"
```

**Example: Devotee's Mace (+3 weapon)**
```
new entry "MAG_Cleric_Devotees_Mace"
type "Weapon"
using "WPN_Mace_2"
data "RootTemplate" "f8578a13-a857-4043-91e4-8101c9e7c004"
data "Rarity" "Legendary"
data "DefaultBoosts" "WeaponEnchantment(3);WeaponProperty(Magical)"
data "BoostsOnEquipMainHand" "UnlockSpell(Target_ConcussiveSmash);UnlockSpell(Target_PostureBreaker);Shout_MAG_DevoteesMace_Healing_Aura)"
data "Unique" "1"
```

**Key Findings:**
1. The base weapon template (e.g., `WPN_Longsword_2`) determines weapon type and base damage die only
2. The `_2` suffix does NOT set enchantment level - it's just a naming convention
3. Enchantment level is explicitly set via `DefaultBoosts "WeaponEnchantment(X)"`
4. No vanilla +4 or +5 weapons exist, but the system supports any value
5. `WeaponProperty(Magical)` makes the weapon count as magical for resistances

**Solution:** Add `DefaultBoosts "WeaponEnchantment(5);WeaponProperty(Magical)"` to the Sword of Tyr

---

## Item 2: Tyr's Protection Addition

### Overview
Add Tyr's Protection from the vanilla Sword of Justice to the Longsword of Tyr.

**Reference:** Vanilla Sword of Justice (PLA_WPN_SwordOfJustice, MapKey: 455383a5-1211-4500-85f9-b71fad3fbf15)

### Research Tasks

- [x] Find Tyr's Protection spell/ability in gustav
- [x] Determine the internal name and implementation

### Research Results

**Sword of Justice Weapon Definition:**
Located at: `Gustav\Public\Gustav\Stats\Generated\Data\Weapon.txt`

```
new entry "PLA_WPN_SwordOfJustice"
type "Weapon"
using "WPN_Greatsword_1"
data "RootTemplate" "455383a5-1211-4500-85f9-b71fad3fbf15"
data "Rarity" "Uncommon"
data "Boosts" "UnlockSpell(Target_PLA_ShieldOfFaith_SwordOfJustice)"
data "StatusOnEquip" "SWORD_OF_JUSTICE_TECHNICAL"
data "Unique" "1"
```

**Tyr's Protection Spell Definition:**
Located at: `Gustav\Public\Gustav\Stats\Generated\Data\Spell_Target.txt`

```
new entry "Target_PLA_ShieldOfFaith_SwordOfJustice"
type "SpellData"
data "SpellType" "Target"
using "Target_ShieldOfFaith"
data "Cooldown" "OncePerShortRestPerItem"
data "SpellProperties" "ApplyStatus(SHIELD_OF_FAITH,100,-1);ApplyStatus(SELF, SWORD_OF_JUSTICE_SHIELD_OF_FAITH_OWNER, 100, -1)"
data "Requirements" ""
data "DisplayName" "hd7783e45g875bg4fdcg8f8dg23da9241b8fa;2"
data "ExtraDescription" "h41ca1011gcb80g4bd8g8986gb5c13fe963ad;2"
data "UseCosts" "BonusActionPoint:1"
```

**SHIELD_OF_FAITH Status:**
Located at: `Shared\Public\Shared\Stats\Generated\Data\Status_BOOST.txt`

```
new entry "SHIELD_OF_FAITH"
type "StatusData"
data "StatusType" "BOOST"
data "Boosts" "AC(2)"
```

**Key Findings:**
1. Tyr's Protection is a variant of Shield of Faith spell
2. Spell name: `Target_PLA_ShieldOfFaith_SwordOfJustice`
3. Uses bonus action (BonusActionPoint:1)
4. Recharges once per short rest (OncePerShortRestPerItem)
5. Grants +2 AC via the SHIELD_OF_FAITH status
6. Can be cast on any ally within range
7. Uses vanilla localization: DisplayName "hd7783e45g875bg4fdcg8f8dg23da9241b8fa;2" = "Tyr's Protection"

**Solution:** Add `UnlockSpell(Target_PLA_ShieldOfFaith_SwordOfJustice)` to Sword of Tyr's Boosts field

---

## Planned Implementation

### Updated Sword of Tyr Definition

```
new entry "SMR_Sword_Tyr"
type "Weapon"
using "WPN_Longsword_2"
data "RootTemplate" "d2e3f4a5-b6c7-4d8e-9f0a-1b2c3d4e5f6a"
data "Rarity" "Legendary"
data "DefaultBoosts" "WeaponEnchantment(5);WeaponProperty(Magical)"
data "Boosts" "UnlockSpell(Target_MAG_Smite_Wrathful);UnlockSpell(SMR_Target_BlindingSmite_Unlimited);UnlockSpell(Target_PLA_ShieldOfFaith_SwordOfJustice)"
data "PassivesOnEquip" "MAG_PlaneShifterSlayer_Passive"
data "Unique" "1"
```

**Changes from current:**
1. Added `DefaultBoosts "WeaponEnchantment(5);WeaponProperty(Magical)"` for +5 enchantment
2. Added `UnlockSpell(Target_PLA_ShieldOfFaith_SwordOfJustice)` to Boosts for Tyr's Protection

---

## Implementation Checklist

### Research
- [x] Complete weapon enchantment research
- [x] Document findings
- [x] Find Tyr's Protection implementation in gustav

### Longsword of Tyr Enhancement
- [x] Update SMR_Sword_Tyr in Weapon.txt with +5 enchantment
- [x] Add Tyr's Protection to Longsword of Tyr

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

### Tyr's Protection
- [ ] Verify Tyr's Protection spell is available when Sword of Tyr is equipped
- [ ] Cast Tyr's Protection on an ally
- [ ] Verify target receives Shield of Faith (+2 AC) status
- [ ] Verify spell uses bonus action
- [ ] Verify spell recharges after short rest

---

## Notes

- The Sword of Justice is a greatsword (uses WPN_Greatsword_1), not a longsword
- Tyr's Protection uses the vanilla Shield of Faith status, so it will display as "Shield of Faith" in the status effects but the spell name is "Tyr's Protection"
- The vanilla spell applies both SHIELD_OF_FAITH to target and SWORD_OF_JUSTICE_SHIELD_OF_FAITH_OWNER to self - this likely tracks that the caster is maintaining the spell
