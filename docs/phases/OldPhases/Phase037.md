# Phase 37: Add Chromatic Orb and Magic Missile to Staff of the Archmage

**Status:** COMPLETE
**Date:** 2026-02-11
**Implementation Date:** 2026-02-11
**Completion Date:** 2026-02-11

---

## Goals

### Staff of the Archmage Enhancement
1. **Add Chromatic Orb Spell:** Give the Staff of the Archmage the vanilla BG3 Chromatic Orb spell (level 1)
2. **Add Magic Missile Spell:** Give the Staff of the Archmage the vanilla BG3 Magic Missile spell (level 1)
3. **Unlimited Uses:** Both spells should cost an action but have unlimited uses (no spell slot cost)
4. **Maintain Container Spell Structure:** Chromatic Orb is a container spell with 6 damage type variants (Acid, Cold, Fire, Lightning, Poison, Thunder)

### Copy Ring of Spectral Power
5. **Copy Item:** Copy Ring of Spectral Power from SampleMagicRingMod to Level13PlusGear
6. **Rename with L13 Prefix:** Update all identifiers from SMR_ to L13_ prefix
7. **Generate New UUIDs:** Create new UUIDs and handles for Level13PlusGear version
8. **Copy All Custom Spells:** Copy all custom spells the ring depends on (Magic Missile Lvl3, Globe of Invulnerability, Hold Person, Artistry of War, Invisibility, Knock, Arcane Gate, Telekinesis)
9. **Make Independent:** Ensure no dependencies on SampleMagicRingMod

---

## Current State

### Staff of the Archmage - Current Spells

**File:** `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Weapon.txt`

```
new entry "L13_Staff_Archmage"
type "Weapon"
using "WPN_Quarterstaff_2"
data "RootTemplate" "ed13f510-3c96-4308-813e-f9592c9afee4"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(Shout_MAG_TheChromatic_ChromaticAttunement);UnlockSpell(Shout_MAG_SpellSlotRestoration);UnlockSpell(Shout_MAG_SpellSlotRestoration_PearlOfPower);UnlockInterrupt(L13_Interrupt_Shield_Unlimited);UnlockInterrupt(L13_Interrupt_Counterspell_Unlimited);UnlockSpell(L13_Target_Light_Unlimited)"
data "PassivesOnEquip" "MAG_ArcaneEnchantment_Lesser_Passive;MAG_Legendary_Chromatic_Spellslot_Passive;WW_Mystra_SpellAttkBonus_Passive;WW_Mystra_Passive;WW_Netherese_Staff_Passive"
data "Unique" "0"
```

**Current Spells:**
- Chromatic Attunement (container spell for multiple spells)
- Spell Slot Restoration (2 versions)
- Light (unlimited, bonus action)
- Shield (unlimited interrupt)
- Counterspell (unlimited interrupt)

**Missing:**
- Chromatic Orb spell
- Magic Missile spell

---

## Target State

### Staff of the Archmage - With Chromatic Orb and Magic Missile

**Add to Boosts:**
```
data "Boosts" "UnlockSpell(Shout_MAG_TheChromatic_ChromaticAttunement);UnlockSpell(Shout_MAG_SpellSlotRestoration);UnlockSpell(Shout_MAG_SpellSlotRestoration_PearlOfPower);UnlockInterrupt(L13_Interrupt_Shield_Unlimited);UnlockInterrupt(L13_Interrupt_Counterspell_Unlimited);UnlockSpell(L13_Target_Light_Unlimited);UnlockSpell(L13_Projectile_ChromaticOrb_Unlimited);UnlockSpell(L13_Projectile_MagicMissile_Unlimited)"
```

**New Spells:**
- **L13_Projectile_ChromaticOrb_Unlimited** - Chromatic Orb (level 1) with unlimited uses (action cost, no spell slot cost)
- **L13_Projectile_MagicMissile_Unlimited** - Magic Missile (level 1) with unlimited uses (action cost, no spell slot cost)

---

## Vanilla Spell References

### Chromatic Orb Reference

### Base Spell Structure

**File:** `VanillaBG3/Shared/Public/Shared/Stats/Generated/Data/Spell_Projectile.txt`

**Container Spell:** `Projectile_ChromaticOrb` (line 739)
```
new entry "Projectile_ChromaticOrb"
type "SpellData"
data "SpellType" "Projectile"
data "Level" "1"
data "SpellSchool" "Evocation"
data "ContainerSpells" "Projectile_ChromaticOrb_Acid;Projectile_ChromaticOrb_Cold;Projectile_ChromaticOrb_Fire;Projectile_ChromaticOrb_Lightning;Projectile_ChromaticOrb_Poison;Projectile_ChromaticOrb_Thunder"
data "SpellProperties" "GROUND:CreateSurface(2,2,Acid)"
data "TargetFloor" "-1"
data "TargetRadius" "18"
data "TargetConditions" "not Self() and not Dead()"
data "ProjectileCount" "1"
data "Trajectories" "f77c14be-cc25-40d6-a7dd-99b2e0a2df1c"
data "Icon" "Spell_Evocation_ChromaticOrb"
data "DisplayName" "hd64d5d0ag20a6g4d74g8676gc34ad9ae4185;1"
data "Description" "h9ebff45bg8d4bg4074gb735gaafbb06d6d32;5"
data "DescriptionParams" "DealDamage(3d8,Thunder)"
data "TooltipDamageList" "DealDamage(3d8,Thunder)"
data "TooltipAttackSave" "RangedSpellAttack"
data "CastTextEvent" "Cast"
data "CycleConditions" "Enemy() and not Dead()"
data "UseCosts" "ActionPoint:1;SpellSlotsGroup:1:1:1"
data "SpellAnimation" "3ff87abf-1ea1-4c32-aadf-c822d74c7dc0,,;,,;38cdb41c-2eec-4e03-bb31-83cff0346c35,,;85414f5f-b448-4dda-9370-1b6c4b38b561,,;d8925ce4-d6d9-400c-92f5-ad772ef7f178,,;,,;eadedcce-d01b-4fbb-a1ae-d218f13aa5d6,,;,,;,,"
data "VerbalIntent" "Damage"
data "SpellFlags" "IsSpell;HasHighGroundRangeExtension;HasVerbalComponent;HasSomaticComponent;RangeIgnoreVerticalThreshold;IsHarmful;IsLinkedSpellContainer"
data "MemoryCost" "1"
```

**Key Properties:**
- **Container spell** with 6 variants (Acid, Cold, Fire, Lightning, Poison, Thunder)
- **Cost:** `ActionPoint:1;SpellSlotsGroup:1:1:1` (action + level 1 spell slot)
- **Damage:** 3d8 damage in chosen element
- **Range:** 18m
- **Level:** 1
- **School:** Evocation

### Magic Missile Reference

**File:** `VanillaBG3/Shared/Public/Shared/Stats/Generated/Data/Spell_Projectile.txt`

**Base Spell:** `Projectile_MagicMissile` (line 1373)
```
new entry "Projectile_MagicMissile"
type "SpellData"
data "SpellType" "Projectile"
data "Level" "1"
data "SpellSchool" "Evocation"
data "SpellProperties" "DealDamage(1d4+1,Force,Magical)"
data "TargetRadius" "18"
data "AmountOfTargets" "3"
data "TargetConditions" "not Self() and not Dead()"
data "ProjectileCount" "1"
data "CastTargetHitDelay" "100"
data "Angle" "120"
data "Icon" "Spell_Evocation_MagicMissile"
data "DisplayName" "h6d2c0287g9bf5g447dgace4g112975feaa66;1"
data "Description" "h2c2809afg17f9g4dc1g9424g75bc6cf60c69;4"
data "DescriptionParams" "DealDamage(1d4+1,Force);3"
data "TooltipDamageList" "DealDamage(3d4+3,Force)"
data "UseCosts" "ActionPoint:1;SpellSlotsGroup:1:1:1"
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsSpell;HasHighGroundRangeExtension;RangeIgnoreVerticalThreshold;IsHarmful"
data "MemoryCost" "1"
data "DamageType" "Force"
```

**Key Properties:**
- **3 missiles** that automatically hit (no attack roll)
- **Damage:** 1d4+1 Force per missile = 3d4+3 total (7-15 damage guaranteed)
- **Cost:** `ActionPoint:1;SpellSlotsGroup:1:1:1` (action + level 1 spell slot)
- **Range:** 18m
- **Level:** 1
- **School:** Evocation
- **Can split between up to 3 targets**

**Reference Implementation:** Ring of Spectral Power in SampleMagicRingMod uses `Projectile_MagicMissile_3` (level 3 version, 5 missiles) as a bonus action with unlimited uses.

---

## Implementation Plan

### Task 1: Create Unlimited Projectile Spells

**Create new spell file for Projectile spells**

Since Level13PlusGear currently only has `Spell_Target.txt` and `Spell_Shout.txt`, we need to create `Spell_Projectile.txt`.

**File:** `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Spell_Projectile.txt`

**Content:**
```
new entry "L13_Projectile_ChromaticOrb_Unlimited"
type "SpellData"
data "SpellType" "Projectile"
using "Projectile_ChromaticOrb"
data "UseCosts" "ActionPoint:1"

new entry "L13_Projectile_MagicMissile_Unlimited"
type "SpellData"
data "SpellType" "Projectile"
using "Projectile_MagicMissile"
data "UseCosts" "ActionPoint:1"
```

**Changes from vanilla:**

**Chromatic Orb:**
- **Inherits:** Uses vanilla `Projectile_ChromaticOrb` as base
- **UseCosts:** Changed from `ActionPoint:1;SpellSlotsGroup:1:1:1` to just `ActionPoint:1`
- **Result:** Costs an action but no spell slot (unlimited uses)

**Magic Missile:**
- **Inherits:** Uses vanilla `Projectile_MagicMissile` as base (level 1 = 3 missiles)
- **UseCosts:** Changed from `ActionPoint:1;SpellSlotsGroup:1:1:1` to just `ActionPoint:1`
- **Result:** Costs an action but no spell slot (unlimited uses)

### Task 2: Add Both Spells to Staff of the Archmage

**File:** `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Weapon.txt`

**Add to line 6 (Boosts):**
```
;UnlockSpell(L13_Projectile_ChromaticOrb_Unlimited);UnlockSpell(L13_Projectile_MagicMissile_Unlimited)
```

**Full updated Boosts line:**
```
data "Boosts" "UnlockSpell(Shout_MAG_TheChromatic_ChromaticAttunement);UnlockSpell(Shout_MAG_SpellSlotRestoration);UnlockSpell(Shout_MAG_SpellSlotRestoration_PearlOfPower);UnlockInterrupt(L13_Interrupt_Shield_Unlimited);UnlockInterrupt(L13_Interrupt_Counterspell_Unlimited);UnlockSpell(L13_Target_Light_Unlimited);UnlockSpell(L13_Projectile_ChromaticOrb_Unlimited);UnlockSpell(L13_Projectile_MagicMissile_Unlimited)"
```

### Task 3: Update Item Catalog

**File:** `docs/level13plusgear/item_catalog.md`

Update the Staff of the Archmage entry to include Chromatic Orb.

---

## Detailed Implementation

### Step 1: Create Spell_Projectile.txt

**File:** `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Spell_Projectile.txt`

**Create new file with content:**
```
new entry "L13_Projectile_ChromaticOrb_Unlimited"
type "SpellData"
data "SpellType" "Projectile"
using "Projectile_ChromaticOrb"
data "UseCosts" "ActionPoint:1"

new entry "L13_Projectile_MagicMissile_Unlimited"
type "SpellData"
data "SpellType" "Projectile"
using "Projectile_MagicMissile"
data "UseCosts" "ActionPoint:1"
```

**Purpose:**

**Chromatic Orb:**
- Creates custom unlimited version of Chromatic Orb (level 1)
- Inherits all properties from vanilla spell (6 damage type variants, 3d8 damage, range, etc.)
- Only overrides cost to remove spell slot requirement
- Player can cast as an action without expending spell slots

**Magic Missile:**
- Creates custom unlimited version of Magic Missile (level 1)
- Inherits all properties from vanilla spell (3 missiles, 1d4+1 Force each, auto-hit)
- Only overrides cost to remove spell slot requirement
- Player can cast as an action without expending spell slots

### Step 2: Update Staff of the Archmage Boosts

**File:** `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Weapon.txt`

**Current line 6:**
```
data "Boosts" "UnlockSpell(Shout_MAG_TheChromatic_ChromaticAttunement);UnlockSpell(Shout_MAG_SpellSlotRestoration);UnlockSpell(Shout_MAG_SpellSlotRestoration_PearlOfPower);UnlockInterrupt(L13_Interrupt_Shield_Unlimited);UnlockInterrupt(L13_Interrupt_Counterspell_Unlimited);UnlockSpell(L13_Target_Light_Unlimited)"
```

**New line 6:**
```
data "Boosts" "UnlockSpell(Shout_MAG_TheChromatic_ChromaticAttunement);UnlockSpell(Shout_MAG_SpellSlotRestoration);UnlockSpell(Shout_MAG_SpellSlotRestoration_PearlOfPower);UnlockInterrupt(L13_Interrupt_Shield_Unlimited);UnlockInterrupt(L13_Interrupt_Counterspell_Unlimited);UnlockSpell(L13_Target_Light_Unlimited);UnlockSpell(L13_Projectile_ChromaticOrb_Unlimited);UnlockSpell(L13_Projectile_MagicMissile_Unlimited)"
```

**Purpose:** Grants both custom unlimited spells when staff is equipped

### Step 3: Update Item Catalog

**File:** `docs/level13plusgear/item_catalog.md`

**Update lines 14-16 (Staff of the Archmage table):**

**Current:**
```
| Category | Details |
|----------|---------|
| Spells | Chromatic Attunement, Spell Slot Restoration (2 versions), Light (unlimited), Shield (unlimited), Counterspell (unlimited) |
```

**New:**
```
| Category | Details |
|----------|---------|
| Spells | Chromatic Orb (unlimited), Magic Missile (unlimited), Chromatic Attunement, Spell Slot Restoration (2 versions), Light (unlimited), Shield (unlimited), Counterspell (unlimited) |
```

**Add new custom spell entries at line 106 (after L13_Shout_SpiritGuardians_Moonguard):**
```

### L13_Projectile_ChromaticOrb_Unlimited
**Type:** Projectile Spell | **Cost:** Action, Unlimited | **Level:** 1

**Name:** Chromatic Orb
**Description:** Hurl a sphere of energy that deals 3d8 damage. Choose from Acid, Cold, Fire, Lightning, Poison, or Thunder damage. Unlimited uses.

**Damage Types (choose one):**
- Acid: 3d8 Acid damage, creates acid surface
- Cold: 3d8 Cold damage
- Fire: 3d8 Fire damage
- Lightning: 3d8 Lightning damage
- Poison: 3d8 Poison damage
- Thunder: 3d8 Thunder damage

**Used by:** Staff of the Archmage

### L13_Projectile_MagicMissile_Unlimited
**Type:** Projectile Spell | **Cost:** Action, Unlimited | **Level:** 1

**Name:** Magic Missile
**Description:** Create three darts of magical force that automatically hit their target. Each dart deals 1d4+1 Force damage (3d4+3 total). Can target up to 3 different creatures. Unlimited uses.

**Damage:** 3d4+3 Force (7-15 guaranteed damage, no attack roll)
**Missiles:** 3 missiles (can split between targets)

**Used by:** Staff of the Archmage
```

---

## Files to Modify/Create

### Staff of the Archmage - New Spells

| File | Action | Description |
|------|--------|-------------|
| `Spell_Projectile.txt` | Create/Edit | Add L13_Projectile_ChromaticOrb_Unlimited and L13_Projectile_MagicMissile_Unlimited |
| `Weapon.txt` | Edit | Add Chromatic Orb and Magic Missile to Staff of the Archmage Boosts |

### Ring of Spectral Power - Copy from SampleMagicRingMod

| File | Action | Description |
|------|--------|-------------|
| `Armor.txt` | Edit | Add L13_Ring_Spectral_Power entry |
| `RootTemplates/L13_Ring_Spectral_Power.lsf.lsx` | Create | RootTemplate for ring |
| `Spell_Projectile.txt` | Edit | Add L13_Projectile_MagicMissile_Unlimited_Lvl3 and L13_Projectile_ArtistryOfWar_ShortRest |
| `Spell_Target.txt` | Edit | Add L13_Target_HoldPerson_Unlimited, L13_Target_Invisibility_ShortRest, L13_Target_Knock_Unlimited |
| `Spell_Zone.txt` | Create | Add L13_Target_GlobeOfInvulnerability_ShortRest |
| `Spell_Teleportation.txt` | Create | Add L13_Teleportation_ArcaneGate_ShortRest |
| `Spell_Throw.txt` | Create | Add L13_Throw_Telekinesis_ShortRest |
| `Localization/English/Level13PlusGear.loca.xml` | Edit | Add localization for all custom spells |
| `TreasureTable.txt` | Edit | Add ring to Tutorial Chest |

### Documentation

| File | Action | Description |
|------|--------|-------------|
| `docs/level13plusgear/item_catalog.md` | Edit | Document new spells on staff and new Ring of Spectral Power |
| `docs/instructions/uuid_workflow.md` | Edit | Remove used UUIDs from pool |

---

## UUID/Handle Requirements

**None required** - This phase uses vanilla spells as base (`using "Projectile_ChromaticOrb"` and `using "Projectile_MagicMissile"`) and only overrides the cost. No custom names or descriptions needed.

---

## Testing Plan

### Test 1: Staff Grants Both New Spells
1. Start or load game with Level13PlusGear mod enabled
2. Obtain Staff of the Archmage (from L13_Gear_Chest in Tutorial Chest)
3. Equip the staff on a character
4. Open spellbook/action bar
5. **Verify:** Chromatic Orb appears in available spells
6. **Verify:** Magic Missile appears in available spells
7. **Verify:** Both spells show as "Level 1 Evocation" spells
8. **Verify:** Both have vanilla spell icons

### Test 2: Chromatic Orb - Unlimited Casting
1. With staff equipped, check character's spell slots
2. Note current spell slot count
3. Cast Chromatic Orb (choose any damage type)
4. **Verify:** Spell consumes an action
5. **Verify:** Spell slot count does NOT decrease
6. **Verify:** Spell can be cast again immediately on next turn (unlimited uses)
7. Cast Chromatic Orb 5+ times in sequence
8. **Verify:** Still works after many casts (no hidden limit)

### Test 3: Chromatic Orb - Damage and Container Spell
1. Open spellbook and locate Chromatic Orb
2. **Verify:** Hovering/clicking shows 6 sub-spells (Acid, Cold, Fire, Lightning, Poison, Thunder)
3. **Verify:** Can select which damage type before casting
4. Cast Chromatic Orb (Acid) at an enemy
5. **Verify:** Deals 3d8 Acid damage (check combat log)
6. **Verify:** Creates acid surface on ground
7. Cast Chromatic Orb (Fire) at an enemy
8. **Verify:** Deals 3d8 Fire damage
9. Test other damage types (Cold, Lightning, Poison, Thunder)
10. **Verify:** Each deals correct damage type and amount
11. **Verify:** Spell uses ranged spell attack roll

### Test 4: Magic Missile - Unlimited Casting
1. With staff equipped, check character's spell slots
2. Note current spell slot count
3. Cast Magic Missile at an enemy
4. **Verify:** Spell consumes an action
5. **Verify:** Spell slot count does NOT decrease
6. **Verify:** Spell can be cast again immediately on next turn (unlimited uses)
7. Cast Magic Missile 5+ times in sequence
8. **Verify:** Still works after many casts (no hidden limit)

### Test 5: Magic Missile - Damage and Auto-Hit
1. Cast Magic Missile at an enemy
2. **Verify:** 3 missiles fire automatically (no attack roll)
3. **Verify:** Check combat log: each missile deals 1d4+1 Force damage
4. **Verify:** Total damage is between 7-15 (3d4+3)
5. **Verify:** Missiles automatically hit (no miss chance)
6. Cast Magic Missile and split missiles between 2-3 enemies
7. **Verify:** Can target different creatures with different missiles
8. **Verify:** All missiles hit their respective targets

### Test 6: Staff Still Has Other Spells
1. With staff equipped, check all available spells
2. **Verify:** All original spells still present:
   - Chromatic Attunement
   - Spell Slot Restoration (2 versions)
   - Light (unlimited)
   - Shield (unlimited interrupt)
   - Counterspell (unlimited interrupt)
3. **Verify:** All passives still work:
   - Arcane Enchantment
   - Chromatic Spellslot
   - Mystra's Blessing
   - Netherese Staff
4. Test casting a few of the other spells
5. **Verify:** No conflicts or issues with new spells

### Test 7: Unequip Removes Spells
1. With staff equipped, verify Chromatic Orb and Magic Missile are available
2. Unequip the staff
3. **Verify:** Both spells are no longer in spellbook/action bar
4. Re-equip the staff
5. **Verify:** Both spells return to spellbook

---

## Technical Notes

### Spell Inheritance Pattern

Both spells use the **inheritance pattern** where we inherit from vanilla spells and only override the cost.

**Chromatic Orb - Container Spell:**

Chromatic Orb is a **container spell** (like Spirit Guardians in the Moonguard Blade). The vanilla spell `Projectile_ChromaticOrb` contains 6 sub-spells for different damage types.

```
using "Projectile_ChromaticOrb"
data "UseCosts" "ActionPoint:1"
```

**Inherits:**
- All 6 damage type variants (Acid, Cold, Fire, Lightning, Poison, Thunder)
- Container spell structure
- Damage values (3d8 per cast)
- Range (18m)
- Visual effects, animations, icon
- Name/description from vanilla

**Only overrides:** Cost (removes spell slot requirement)

**Magic Missile - Auto-Hit Projectile:**

Magic Missile automatically hits and fires multiple missiles.

```
using "Projectile_MagicMissile"
data "UseCosts" "ActionPoint:1"
```

**Inherits:**
- 3 missiles (level 1 version)
- 1d4+1 Force damage per missile (3d4+3 total)
- Auto-hit mechanic (no attack roll)
- Ability to split missiles between targets
- Range (18m)
- Visual effects, animations, icon
- Name/description from vanilla

**Only overrides:** Cost (removes spell slot requirement)

### Why This Works Without Custom Localization

Unlike custom spells that need unique names/descriptions, both spells:
- Use vanilla spells as base
- Don't override DisplayName or Description
- Inherit all vanilla text
- Player sees normal spell names ("Chromatic Orb", "Magic Missile") and vanilla tooltips

**Result:** No handles or localization needed.

### Comparison: Magic Missile Levels

BG3 has multiple Magic Missile variants:
- **Level 1:** 3 missiles (used by Staff of the Archmage)
- **Level 2:** 4 missiles
- **Level 3:** 5 missiles (used by Ring of Spectral Power in SampleMagicRingMod)

Staff uses level 1 for balance - still powerful as unlimited action, but not overwhelming.

### Spell Slot Removal Pattern

**Vanilla cost:**
```
data "UseCosts" "ActionPoint:1;SpellSlotsGroup:1:1:1"
```
- `ActionPoint:1` = costs 1 action
- `SpellSlotsGroup:1:1:1` = costs level 1 spell slot

**Unlimited cost:**
```
data "UseCosts" "ActionPoint:1"
```
- `ActionPoint:1` = still costs 1 action
- No `SpellSlotsGroup` = no spell slot cost
- **Result:** Unlimited uses (action-gated only)

**This pattern used in other L13 spells:**
- `L13_Target_BlindingSmite_Unlimited` (action cost only)
- `L13_Shout_CelestialHaste_Unlimited` (bonus action cost only)
- `L13_Target_MistyStep_Unlimited` (no cost at all)

### Projectile Spell File

Level13PlusGear currently has:
- ✅ `Spell_Target.txt` (Target spells: Light, Blinding Smite, Misty Step)
- ✅ `Spell_Shout.txt` (Shout spells: Celestial Haste, Spirit Guardians)
- ❌ `Spell_Projectile.txt` (NEW - needed for Chromatic Orb and Magic Missile)

**BG3 spell types:**
- **Target:** Spells cast on a specific target (melee/touch range or line-of-sight)
- **Shout:** Spells cast on self or area (no targeting required)
- **Projectile:** Spells that fire projectiles at targets (has travel time and trajectory)

Both Chromatic Orb and Magic Missile are **Projectile** type because they fire visible projectiles that travel to targets.

---

## Dependencies

**This phase depends on:**
- Level13PlusGear mod (target mod)
- Staff of the Archmage item already exists (created in earlier phase)
- Vanilla BG3 `Projectile_ChromaticOrb` spell (inherited)
- Vanilla BG3 `Projectile_MagicMissile` spell (inherited)
- SampleMagicRingMod Ring of Spectral Power (source for copying)
- UUID pool in `docs/instructions/uuid_workflow.md` (for new UUIDs/handles)

**This phase affects:**
- Staff of the Archmage becomes more powerful (adds two offensive spells)
- Level13PlusGear gains Ring of Spectral Power (new item)
- Creates 3 new spell file types in Level13PlusGear (Zone, Teleportation, Throw)
- No impact on other items or mods
- No new dependencies on SampleMagicRingMod (ring copy is independent)

---

## Success Criteria

### Staff of the Archmage - New Spells
- [ ] Spell_Projectile.txt file created/updated successfully
- [ ] L13_Projectile_ChromaticOrb_Unlimited spell defined
- [ ] L13_Projectile_MagicMissile_Unlimited spell defined
- [ ] Staff of the Archmage updated with both new spells in Boosts
- [ ] Staff grants Chromatic Orb when equipped
- [ ] Staff grants Magic Missile when equipped
- [ ] Chromatic Orb costs action (not spell slot) with unlimited uses
- [ ] All 6 Chromatic Orb damage variants work correctly
- [ ] Chromatic Orb deals proper 3d8 damage per cast
- [ ] Magic Missile costs action (not spell slot) with unlimited uses
- [ ] Magic Missile fires 3 missiles that auto-hit
- [ ] Magic Missile deals 3d4+3 Force damage (7-15 total)
- [ ] Staff's other spells still work

### Ring of Spectral Power - Copy from SampleMagicRingMod
- [ ] UUIDs generated and allocated from pool
- [ ] Handles generated for all custom spells
- [ ] L13_Ring_Spectral_Power stats entry created in Armor.txt
- [ ] RootTemplate created (L13_Ring_Spectral_Power.lsf.lsx)
- [ ] All custom spells copied and converted to L13 prefix:
  - [ ] Magic Missile Lvl3 (unlimited)
  - [ ] Globe of Invulnerability (short rest)
  - [ ] Hold Person (unlimited)
  - [ ] Artistry of War (short rest)
  - [ ] Invisibility (short rest)
  - [ ] Knock (unlimited)
  - [ ] Arcane Gate (short rest)
  - [ ] Telekinesis (short rest)
- [ ] New spell files created: Spell_Zone.txt, Spell_Teleportation.txt, Spell_Throw.txt
- [ ] Localization entries created for all custom spells
- [ ] Ring added to TreasureTable (Tutorial Chest)
- [ ] Ring appears in Tutorial Chest in-game
- [ ] Ring grants all spells when equipped
- [ ] Forceweaver passive works (+1d4 Force on spell attacks)
- [ ] Magic Missile Lvl3 fires 5 missiles
- [ ] All utility spells function correctly
- [ ] No dependency on SampleMagicRingMod

### General
- [ ] Game loads without errors
- [ ] Item catalog updated with both new spells and ring
- [ ] All testing completed and verified
- [ ] Documentation complete

---

## Related Documentation

- **docs/level13plusgear/item_catalog.md** - Item catalog to update with new spells and ring
- **docs/planning/item_catalog.md** - SampleMagicRingMod catalog (Ring of Spectral Power reference)
- **docs/instructions/copying_items_between_mods.md** - Workflow for copying items between mods
- **docs/instructions/uuid_workflow.md** - UUID pool and naming conventions for L13 mod
- **VanillaBG3/Shared/Public/Shared/Stats/Generated/Data/Spell_Projectile.txt** - Vanilla spell references (Chromatic Orb line 739, Magic Missile line 1373)
- **SampleMagicRingMod/Public/SampleMagicRingMod/Stats/Generated/Data/** - Source files for Ring of Spectral Power:
  - Armor.txt (ring stats, line 37)
  - Spell_Projectile.txt (Magic Missile Lvl3, Artistry of War)
  - Spell_Target.txt (Hold Person, Invisibility, Knock)
  - Spell_Zone.txt (Globe of Invulnerability)
  - Spell_Teleportation.txt (Arcane Gate)
  - Spell_Throw.txt (Telekinesis)
- **Phase029.md** - Previous item copy example (Staff of the Archmage)
- **Phase036.md** - Previous phase (Ring of Creation updates)

---

## Notes

### Chromatic Orb
- Level 1 spell but deals significant damage (3d8), making it powerful as an unlimited action
- Having 6 damage types provides tactical flexibility (choose based on enemy resistances)
- Ranged spell attack (uses spell attack bonus, not save DC)
- At later levels, this unlimited 3d8 damage may be less powerful than higher-level spells, but provides consistent damage option without resource cost

### Magic Missile
- Level 1 spell with guaranteed damage (no attack roll, no save)
- 3 missiles × (1d4+1) = 3d4+3 Force damage (7-15 guaranteed)
- Can split missiles between multiple targets for tactical flexibility
- Force damage rarely resisted, making it reliable
- Auto-hit nature makes it valuable against high-AC enemies
- At later levels, guaranteed 7-15 damage is modest but still useful as unlimited option

### Combined Power
- Staff now has both a flexible damage type option (Chromatic Orb) and a guaranteed damage option (Magic Missile)
- Chromatic Orb: Higher damage potential (3-24) but requires attack roll
- Magic Missile: Lower guaranteed damage (7-15) but always hits
- This combination makes the Staff of the Archmage exceptional for casters at all levels

---

## Ring of Spectral Power - Copy from SampleMagicRingMod

### Current State (SampleMagicRingMod)

**File:** `SampleMagicRingMod/Public/SampleMagicRingMod/Stats/Generated/Data/Armor.txt`

```
new entry "SMR_Ring_Spectral_Power"
type "Armor"
using "_Ring"
data "RootTemplate" "d4e5f6a7-b8c9-4d0e-a1b2-c3d4e5f6a7b8"
data "ObjectCategory" "Jewelry"
data "ValueOverride" "750"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(SMR_Projectile_MagicMissile_Unlimited_Lvl3);UnlockSpell(SMR_Target_GlobeOfInvulnerability_ShortRest);UnlockSpell(SMR_Target_MistyStep_Unlimited);UnlockInterrupt(SMR_Interrupt_Shield_Unlimited);UnlockSpell(SMR_Target_HoldPerson_Unlimited);UnlockSpell(SMR_Projectile_ArtistryOfWar_ShortRest);UnlockSpell(SMR_Target_Invisibility_ShortRest);UnlockSpell(SMR_Target_Knock_Unlimited);UnlockSpell(SMR_Teleportation_ArcaneGate_ShortRest);UnlockSpell(SMR_Throw_Telekinesis_ShortRest)"
data "PassivesOnEquip" "WW_Forceweaver_Passive"
```

**Ring Properties:**
- **Spells:** Magic Missile Lvl3 (unlimited), Globe of Invulnerability (short rest), Misty Step (unlimited), Hold Person (unlimited), Artistry of War (short rest), Invisibility (short rest), Knock (unlimited), Arcane Gate (short rest), Telekinesis (short rest)
- **Interrupts:** Shield (unlimited)
- **Passives:** Forceweaver (+1d4 Force on spell attack)

**Custom Spells to Copy:**
1. `SMR_Projectile_MagicMissile_Unlimited_Lvl3` (Spell_Projectile.txt)
2. `SMR_Target_GlobeOfInvulnerability_ShortRest` (Spell_Zone.txt)
3. `SMR_Target_MistyStep_Unlimited` (already exists in L13 as `L13_Target_MistyStep_Unlimited`)
4. `SMR_Interrupt_Shield_Unlimited` (already exists in L13 as `L13_Interrupt_Shield_Unlimited`)
5. `SMR_Target_HoldPerson_Unlimited` (Spell_Target.txt)
6. `SMR_Projectile_ArtistryOfWar_ShortRest` (Spell_Projectile.txt)
7. `SMR_Target_Invisibility_ShortRest` (Spell_Target.txt)
8. `SMR_Target_Knock_Unlimited` (Spell_Target.txt)
9. `SMR_Teleportation_ArcaneGate_ShortRest` (Spell_Teleportation.txt - NEW FILE TYPE)
10. `SMR_Throw_Telekinesis_ShortRest` (Spell_Throw.txt - NEW FILE TYPE)

**Vanilla Passives to Reuse:**
- `WW_Forceweaver_Passive` (vanilla passive, no copy needed)

### Target State (Level13PlusGear)

**New entry:** `L13_Ring_Spectral_Power`

**Naming conversions:**
- Stats name: `SMR_Ring_Spectral_Power` → `L13_Ring_Spectral_Power`
- All custom spells: `SMR_*` → `L13_*`
- UUID prefix: Generate new UUIDs with `ed13` prefix
- Handle prefix: Generate new handles with `hed13` prefix

**Files to Create/Modify:**

| File | Action | Description |
|------|--------|-------------|
| `Armor.txt` | Edit | Add L13_Ring_Spectral_Power entry |
| `RootTemplates/L13_Ring_Spectral_Power.lsf.lsx` | Create | RootTemplate for ring |
| `Spell_Projectile.txt` | Edit | Add Magic Missile Lvl3 and Artistry of War spells |
| `Spell_Target.txt` | Edit | Add Hold Person, Invisibility, Knock spells |
| `Spell_Zone.txt` | Create | Add Globe of Invulnerability spell |
| `Spell_Teleportation.txt` | Create | Add Arcane Gate spell |
| `Spell_Throw.txt` | Create | Add Telekinesis spell |
| `Localization/*.loca.xml` | Edit | Add all custom spell names/descriptions |

### Ring of Spectral Power Implementation Plan

**This section uses the workflow from `docs/instructions/copying_items_between_mods.md`**

#### Step 1: Generate UUIDs and Handles

**UUIDs needed:**
- 1 for RootTemplate
- ~10-15 for custom spell names/descriptions (DisplayName, ExtraDescription for each custom spell)

**Process:**
1. Take UUIDs from pool in `docs/instructions/uuid_workflow.md`
2. Replace first 4 chars with `ed13`
3. Generate handles from UUIDs (remove hyphens, format as `hed13...`)
4. Delete used UUIDs from pool

#### Step 2: Copy Ring Stats

**Source:** `SampleMagicRingMod/Public/SampleMagicRingMod/Stats/Generated/Data/Armor.txt` (lines 37-45)

**Target:** `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Armor.txt`

**Changes:**
- `SMR_Ring_Spectral_Power` → `L13_Ring_Spectral_Power`
- `RootTemplate` → new UUID with `ed13` prefix
- All `SMR_*` spell names → `L13_*`
- Set `data "Unique" "0"` for TreasureTable delivery
- Keep `WW_Forceweaver_Passive` (vanilla passive)

#### Step 3: Create RootTemplate

**Create:** `Level13PlusGear/Public/Level13PlusGear/RootTemplates/L13_Ring_Spectral_Power.lsf.lsx`

**Source template:** Copy structure from existing ring template (e.g., from SampleMagicRingMod or use standard ring template)

**Set:**
- MapKey UUID (same as RootTemplate in stats)
- Stats name: `L13_Ring_Spectral_Power`
- DisplayName handle
- Description handle

#### Step 4: Copy Custom Spells

**4a: Magic Missile Level 3 (Unlimited)**

**Source:** `SMR_Projectile_MagicMissile_Unlimited_Lvl3` (SampleMagicRingMod Spell_Projectile.txt, line 18)

**Target:** `L13_Projectile_MagicMissile_Unlimited_Lvl3` in Level13PlusGear Spell_Projectile.txt

```
new entry "L13_Projectile_MagicMissile_Unlimited_Lvl3"
type "SpellData"
data "SpellType" "Projectile"
using "Projectile_MagicMissile_3"
data "DisplayName" "[new hed13 handle];1"
data "ExtraDescription" "[new hed13 handle];1"
data "UseCosts" "BonusActionPoint:1"
data "MemoryCost" ""
```

**Note:** Uses level 3 Magic Missile (5 missiles) as bonus action with unlimited uses.

**4b: Globe of Invulnerability (Short Rest)**

**Source:** `SMR_Target_GlobeOfInvulnerability_ShortRest` (SampleMagicRingMod Spell_Zone.txt)

**Target:** Create `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Spell_Zone.txt`

**Copy spell entry** and convert to L13 naming.

**4c: Hold Person (Unlimited)**

**Source:** `SMR_Target_HoldPerson_Unlimited` (SampleMagicRingMod Spell_Target.txt)

**Target:** Add to Level13PlusGear Spell_Target.txt

**4d: Artistry of War (Short Rest)**

**Source:** `SMR_Projectile_ArtistryOfWar_ShortRest` (SampleMagicRingMod Spell_Projectile.txt, line 27)

**Target:** Add to Level13PlusGear Spell_Projectile.txt

**4e: Invisibility (Short Rest)**

**Source:** `SMR_Target_Invisibility_ShortRest` (SampleMagicRingMod Spell_Target.txt)

**Target:** Add to Level13PlusGear Spell_Target.txt

**4f: Knock (Unlimited)**

**Source:** `SMR_Target_Knock_Unlimited` (SampleMagicRingMod Spell_Target.txt)

**Target:** Add to Level13PlusGear Spell_Target.txt

**4g: Arcane Gate (Short Rest)**

**Source:** `SMR_Teleportation_ArcaneGate_ShortRest` (SampleMagicRingMod Spell_Teleportation.txt)

**Target:** Create `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Spell_Teleportation.txt`

**4h: Telekinesis (Short Rest)**

**Source:** `SMR_Throw_Telekinesis_ShortRest` (SampleMagicRingMod Spell_Throw.txt)

**Target:** Create `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Spell_Throw.txt`

#### Step 5: Create Localization Entries

**For each custom spell with DisplayName/ExtraDescription:**

Create localization entries in:
- `Level13PlusGear/Localization/English/Level13PlusGear.loca.xml`

**Process:**
1. Find SMR spell in `SampleMagicRingMod/Localization/English/SampleMagicRingMod.loca.xml`
2. Copy the English text content
3. Create new entry with L13 handle (generated from UUID pool)
4. Use same text content (can customize if desired)

#### Step 6: Add to TreasureTable

**File:** `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/TreasureTable.txt`

**Add to Tutorial Chest treasure table:**
```
new treasuretable "L13_TUT_Chest_Potions"
CanMerge 1
new subtable "1,1"
object category "I_L13_Ring_Spectral_Power",1,0,0,0,0,0,0,0
```

#### Step 7: Update Item Catalog

**File:** `docs/level13plusgear/item_catalog.md`

**Add new ring entry** with full documentation of all spells and passives.

### Ring of Spectral Power Testing Plan

**Test 1: Ring Appears in Tutorial Chest**
1. Start new game
2. Progress to Nautiloid Tutorial Chest
3. Open chest
4. **Verify:** Ring of Spectral Power (L13 version) is present

**Test 2: Ring Grants All Spells**
1. Equip ring
2. Check spellbook
3. **Verify:** All spells available:
   - Magic Missile Lvl3 (bonus action, unlimited)
   - Globe of Invulnerability (short rest)
   - Misty Step (unlimited)
   - Hold Person (unlimited)
   - Artistry of War (short rest)
   - Invisibility (short rest)
   - Knock (unlimited)
   - Arcane Gate (short rest)
   - Telekinesis (short rest)
   - Shield interrupt (unlimited)

**Test 3: Forceweaver Passive Works**
1. Equip ring
2. Cast any spell attack (e.g., Fire Bolt, Eldritch Blast)
3. **Verify:** Deals +1d4 Force damage (check combat log)
4. **Verify:** Shows "Forceweaver" in combat log

**Test 4: Magic Missile Level 3**
1. Cast Magic Missile from ring
2. **Verify:** Fires 5 missiles (level 3 version)
3. **Verify:** Each missile deals 1d4+1 Force damage
4. **Verify:** Can split between multiple targets
5. **Verify:** Uses bonus action
6. **Verify:** Unlimited uses (cast multiple times)

**Test 5: Utility Spells Work**
1. Test Globe of Invulnerability (creates protective zone)
2. Test Hold Person (paralyze humanoid)
3. Test Invisibility (become invisible)
4. Test Knock (unlock locks)
5. Test Arcane Gate (create portal)
6. Test Telekinesis (throw/move object)
7. **Verify:** All spells function correctly

**Test 6: No SampleMagicRingMod Dependency**
1. Disable SampleMagicRingMod
2. Load game with only Level13PlusGear active
3. **Verify:** Ring still works completely
4. **Verify:** No missing references or errors

### Ring of Spectral Power Notes

**Complexity:**
- This is one of the most complex items in SampleMagicRingMod
- Requires creating 2 new spell file types (Spell_Teleportation.txt, Spell_Throw.txt, Spell_Zone.txt)
- Has ~10 custom spells requiring localization
- Extensive testing needed due to spell variety

**Why Copy This Item:**
- Extremely powerful and versatile ring
- Showcases many spell types (projectile, target, teleportation, throw, zone)
- Good candidate for Level13PlusGear (endgame power level)
- Creates foundation for copying other complex items

**Estimated Implementation Time:**
- High complexity due to many custom spells across multiple new file types
- Requires significant localization work
- Good practice for Phase 38 (bulk item copying)

---

## Future Planning Note

**Phase 38 Suggestion:** Copy many more items from SampleMagicRingMod to Level13PlusGear mod. The Ring of Spectral Power copy in Phase 37 will establish patterns and file structures that make bulk copying in Phase 38 more efficient.

**Potential Phase 38 items:**
- Rings: Ring of the Guardian, Ring Magic 1-5
- Armor: Armor of Tyr, Armor of the Rogue, Moonguard Splint, Armor of Voss, Armor of Orpheus
- Helmets: Helmet of Tyr, Circlet of Tyr, Magus Circlet, Moonguard Helm
- Weapons: Sword of Tyr, Sword of Orpheus, Divine Maul, Selune's Moon Mace, Rogueblade, Moonguard Blade (already copied), Staff of Akitaro
- Boots: Boots of Stormwalker (already copied)

---

## Implementation Summary

**Completed:**

1. **Staff of the Archmage - New Spells** ✓
   - Created Spell_Projectile.txt with Chromatic Orb and Magic Missile (unlimited versions)
   - Updated Staff of the Archmage Boosts to include both spells
   - Staff now has powerful offensive options (Chromatic Orb for damage variety, Magic Missile for guaranteed hits)

2. **Ring of Spectral Power - Full Copy** ✓
   - Generated 17 UUIDs/handles from pool (1 RootTemplate + 16 spell handles)
   - Created L13_Ring_Spectral_Power entry in Armor.txt with all 9 custom spells
   - Created RootTemplate (L13_Ring_Spectral_Power.lsf.lsx)
   - Copied and adapted all custom spells:
     - Magic Missile Lvl3 (unlimited, bonus action) - Spell_Projectile.txt
     - Artistry of War (short rest) - Spell_Projectile.txt
     - Hold Person (unlimited) - Spell_Target.txt
     - Invisibility (short rest) - Spell_Target.txt
     - Knock (unlimited) - Spell_Target.txt
     - Globe of Invulnerability (short rest) - Spell_Zone.txt (NEW FILE)
     - Arcane Gate (short rest) - Spell_Teleportation.txt (NEW FILE)
     - Telekinesis (short rest) - Spell_Throw.txt (NEW FILE)
   - Created 3 new spell file types in Level13PlusGear
   - Added 16 localization entries for ring and spells
   - Added ring to TreasureTable (appears in L13_Gear_Chest)
   - Fully independent from SampleMagicRingMod (no dependencies)

3. **Documentation Updated** ✓
   - Updated Level13PlusGear item catalog with new spells and ring
   - Added version history entry for Phase 037
   - Updated item summary (5 items, 16 custom spells)
   - Updated UUID pool (removed 17 used UUIDs)
   - Phase 037 marked as IMPLEMENTED

**Files Created:**
- `Spell_Projectile.txt` (created with 4 spells total: 2 for staff, 2 for ring)
- `Spell_Zone.txt` (Globe of Invulnerability)
- `Spell_Teleportation.txt` (Arcane Gate)
- `Spell_Throw.txt` (Telekinesis)
- `L13_Ring_Spectral_Power.lsf.lsx` (RootTemplate)

**Files Modified:**
- `Weapon.txt` (Staff of the Archmage - added 2 spells)
- `Armor.txt` (added Ring of Spectral Power)
- `Spell_Target.txt` (added 3 spells for ring)
- `TreasureTable.txt` (added ring to L13_Gear_Chest)
- `Level13PlusGear.loca.xml` (added 16 localization entries)
- `item_catalog.md` (documented new spells and ring)
- `uuid_workflow.md` (removed used UUIDs)

**Status:** IMPLEMENTED (awaiting user testing)

---

## Phase 37 Status: COMPLETE

**User testing completed successfully.**

**Phase 37 accomplished two major tasks:**
1. ✓ Added Chromatic Orb and Magic Missile to Staff of the Archmage
2. ✓ Copied Ring of Spectral Power from SampleMagicRingMod with full independence

**Key Achievement:** Created infrastructure for 3 new spell types (Zone, Teleportation, Throw) that will support future item copies in Phase 38.

**Lesson Learned:** Copying complex items with multiple custom spells across different spell types is manageable when following a systematic workflow (UUID allocation, spell copying, localization, testing). The Ring of Spectral Power copy established patterns and infrastructure for Phase 38's bulk copying.
