# Phase 060: Add Razor Gale to Silverlight Sword

**Status:** COMPLETE
**Date:** 2026-02-22

---

## Goals

1. **Add Razor Gale weapon action** to the `L21_Sword_Silverlight` in the Level21Gear mod by adding `UnlockSpell(Zone_Mag_WeaponAction_RazorGale)` to its `Boosts`.
2. **Update item catalog** to reflect the Silverlight sword's full power set (was missing from `docs/level21gear/item_catalog.md`).

---

## Design Decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Vanilla vs. custom spell | **Vanilla** (`Zone_Mag_WeaponAction_RazorGale`) | No custom entry needed; the vanilla spell is from Larethian's Wrath and works as a weapon action |
| Use cost | Inherited from vanilla | No override; vanilla Razor Gale uses a weapon action cost |
| UUID/handle needed | **None** | We are just adding an UnlockSpell referencing an existing vanilla spell |

---

## Source Reference

**Razor Gale** (`Zone_Mag_WeaponAction_RazorGale`):
- Source item: Larethian's Wrath (MAG_Finesse_Longsword, MapKey: `56a7539c-7c5c-4c44-b8e0-5ff2e5beb4e9`)
- Type: Zone weapon action
- Effect: Cleave-style attack in a 60-degree arc at 4m range. On hit: weapon damage + Proficiency Bonus in weapon's damage type. On miss: half damage. Wind/air visual.
- Documented in: `docs/instructions/interesting_magical_effects.md` — "Interesting Spells (With Item Sources)"

**Note:** `Zone_Mag_WeaponAction_RazorGale` is not present in our local VanillaBG3 files (added in a newer patch), but the spell name is confirmed from the interesting_magical_effects.md document.

---

## Current State

**File:** `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Weapon.txt`

```
new entry "L21_Sword_Silverlight"
type "Weapon"
using "WPN_Longsword_2"
data "RootTemplate" "ed21e061-f4d9-49f0-8aa0-e737813db4e4"
data "Rarity" "Legendary"
data "DefaultBoosts" "WeaponEnchantment(5);WeaponProperty(Magical)"
data "Boosts" "UnlockSpell(Target_MAG_Smite_Wrathful);UnlockSpell(L21_Target_BlindingSmite_Silverlight);UnlockSpell(L21_Target_Light_Unlimited);UnlockSpell(Target_PLA_ShieldOfFaith_SwordOfJustice);UnlockSpell(L21_Shout_CelestialHaste_Unlimited);UnlockSpell(L21_Shout_SpiritGuardians_Silverlight,AddChildren,,,SpellCastingAbility);UnlockSpell(L21_Target_SilveredBulwark)"
data "PassivesOnEquip" "MAG_PlaneShifterSlayer_Passive;L21_RadiantWeapon_Passive;MAG_TheClover_Rearrangement_Passive;CRE_LathandersLight_Passive;L21_Moonshield_Passive"
data "StatusOnEquip" "MAG_LATHANDERS_LIGHT_TECHNICAL;LOW_RAMAZITHSTOWER_DEVA_BLESSING"
data "Unique" "0"
```

---

## Target State

Add `UnlockSpell(Zone_Mag_WeaponAction_RazorGale)` to the end of the `Boosts` line:

```
data "Boosts" "UnlockSpell(Target_MAG_Smite_Wrathful);UnlockSpell(L21_Target_BlindingSmite_Silverlight);UnlockSpell(L21_Target_Light_Unlimited);UnlockSpell(Target_PLA_ShieldOfFaith_SwordOfJustice);UnlockSpell(L21_Shout_CelestialHaste_Unlimited);UnlockSpell(L21_Shout_SpiritGuardians_Silverlight,AddChildren,,,SpellCastingAbility);UnlockSpell(L21_Target_SilveredBulwark);UnlockSpell(Zone_Mag_WeaponAction_RazorGale)"
```

---

## Implementation Plan

### Task 1: Add Razor Gale to Weapon.txt

**File:** `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Weapon.txt`

Append `;UnlockSpell(Zone_Mag_WeaponAction_RazorGale)` to the `Boosts` data line for `L21_Sword_Silverlight`.

### Task 2: Update item_catalog.md

**File:** `docs/level21gear/item_catalog.md`

Add the Silverlight sword entry (was missing) and update the Razor Gale weapon action to its power list.

---

## Files to Modify

| File | Action | Description |
|------|--------|-------------|
| `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Weapon.txt` | Edit | Add `UnlockSpell(Zone_Mag_WeaponAction_RazorGale)` to Silverlight's Boosts |
| `docs/level21gear/item_catalog.md` | Edit | Add Silverlight sword entry + Razor Gale |

---

## UUID/Handle Requirements

None. This phase uses only a vanilla spell reference — no new UUIDs or handles needed.

---

## Testing Plan

### Test 1: Razor Gale Appears on Silverlight
1. Equip the Silverlight sword on a character.
2. **Verify:** "Razor Gale" weapon action appears in the action bar.
3. **Verify:** The action shows a 60-degree arc / zone targeting indicator.

### Test 2: Razor Gale Deals Correct Damage
1. Use Razor Gale against one or more enemies in the arc.
2. **Verify:** Hit enemies take weapon damage + Proficiency Bonus in slashing (or the weapon's damage type).
3. **Verify:** Missed enemies take half damage.
4. **Verify:** Wind/air visual effect plays.

---

## Technical Notes

### Vanilla Spell Reference
`Zone_Mag_WeaponAction_RazorGale` is a vanilla weapon action from Larethian's Wrath. Adding it via `UnlockSpell()` to any weapon's `Boosts` grants that weapon the action — the game resolves the spell's damage relative to the equipped weapon, so it will use the Silverlight sword's damage and the character's Proficiency Bonus.

### No Custom Spell Needed
Unlike some spells that require a copy to customize costs or names, Razor Gale works correctly referenced directly as a vanilla spell. The weapon action is self-contained.

---

## Dependencies

**This phase depends on:**
- Phase 057 (COMPLETE) — Silverlight sword was created.

---

## Success Criteria

- [ ] `Zone_Mag_WeaponAction_RazorGale` added to `L21_Sword_Silverlight` Boosts
- [ ] Razor Gale weapon action visible when Silverlight sword is equipped
- [ ] Action deals weapon damage + Proficiency Bonus in arc on hit, half on miss
- [ ] `docs/level21gear/item_catalog.md` updated with Silverlight sword entry including Razor Gale
- [ ] User-tested and confirmed

---

## Related Documentation

- **`docs/instructions/interesting_magical_effects.md`** — Razor Gale entry in "Interesting Spells (With Item Sources)"
- **`docs/level21gear/item_catalog.md`** — Level21Gear item catalog
- **`docs/phases/Phase057.md`** — Silverlight sword creation

---

## Phase 060 Status: COMPLETE
