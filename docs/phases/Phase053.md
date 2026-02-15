# Phase 053: Enhance Akitaro's Staff - Silvered Bulwark and Additional Spells

**Status:** COMPLETE
**Date:** 2026-02-14

---

## Goals

1. **Replace Globe of Invulnerability Base** - Change Akitaro's Shield spell from Globe of Invulnerability to Silvered Bulwark
2. **Improve Spell Functionality** - Use the more powerful invulnerability effect that follows the target
3. **Apply Phase 052 Learnings** - Implement proper targeting that doesn't require Nightsong blessing
4. **Add Chromatic Orb** - Add unlimited Chromatic Orb spell (level 1 spellcaster) like Staff of the Archmage
5. **Add Arcane Gate** - Add once per short rest Arcane Gate spell like Ring of Spectral Power
6. **Add Knock** - Add unlimited Knock spell like Ring of Spectral Power

---

## Summary of Changes

| Change | From | To |
|--------|------|-----|
| **Akitaro's Shield Base** | `using "Target_GlobeOfInvulnerability"` | Silvered Bulwark properties (follows target) |
| **Invulnerability Type** | Static Globe (doesn't move) | Silvered Bulwark (follows target) |
| **Spell Count** | 11 spells | 14 spells |
| **New Spells Added** | N/A | Chromatic Orb (unlimited), Arcane Gate (short rest), Knock (unlimited) |

**Result:** Akitaro's Staff becomes significantly more versatile with improved protection (Silvered Bulwark), elemental damage (Chromatic Orb), utility mobility (Arcane Gate), and lock/container opening (Knock).

---

## Current State

### Akitaro's Staff (SMR_Staff_Akitaro)

**File:** `SampleMagicRingMod/Public/SampleMagicRingMod/Stats/Generated/Data/Weapon.txt`

**Current Boosts (Line 15):**
```
data "Boosts" "UnlockSpell(SMR_Target_Light_Unlimited);UnlockInterrupt(SMR_Interrupt_Counterspell_Unlimited);UnlockSpell(SMR_Shout_CelestialHaste_Unlimited);UnlockSpell(Shout_MAG_TheChromatic_ChromaticAttunement);UnlockSpell(Shout_MAG_SpellSlotRestoration);UnlockSpell(Shout_MAG_SpellSlotRestoration_PearlOfPower);UnlockInterrupt(SMR_Interrupt_Shield_Unlimited);UnlockSpell(SMR_Projectile_AkitarosBlast_ShortRest);UnlockSpell(SMR_Target_AkitarosTeleport_ShortRest);UnlockSpell(SMR_Projectile_AkitarosBarrage_Unlimited);UnlockSpell(SMR_Target_AkitarosShield_ShortRest)"
```

**Current Spells (11 total):**
1. Light (unlimited)
2. Counterspell (unlimited, interrupt)
3. Celestial Haste (unlimited)
4. Chromatic Attunement (spell slot restoration)
5. Spell Slot Restoration
6. Pearlescent Restoration
7. Shield (unlimited, interrupt)
8. Akitaro's Blast (short rest)
9. Akitaro's Teleport/Misty Step (short rest)
10. Akitaro's Barrage/Magic Missile (unlimited)
11. Akitaro's Shield/Globe of Invulnerability (short rest) - **TO BE MODIFIED**

**Missing Compared to References:**
- No Chromatic Orb (Staff of Archmage has this)
- No Arcane Gate (Ring of Spectral Power has this)
- No Knock (Ring of Spectral Power has this)

### Akitaro's Shield Spell (SMR_Target_AkitarosShield_ShortRest)

**File:** `SampleMagicRingMod/Public/SampleMagicRingMod/Stats/Generated/Data/Spell_Target.txt`

**Current Implementation (Lines 125-132):**
```
new entry "SMR_Target_AkitarosShield_ShortRest"
type "SpellData"
data "SpellType" "Target"
using "Target_GlobeOfInvulnerability"
data "DisplayName" "ha3b4c5d6g7e8fg9a0bg1c2dg3e4f5a6b7c8d9;1"
data "ExtraDescription" "hb4c5d6e7g8f9ag0b1cg2d3eg4f5a6b7c8d9e0;1"
data "UseCosts" "BonusActionPoint:1"
data "Cooldown" "OncePerShortRest"
```

**Current Behavior:**
- Uses Globe of Invulnerability as base spell
- Creates a stationary 3m radius invulnerability zone
- Zone doesn't move with the target
- Once per short rest, bonus action
- Concentration required

**Limitation:** Globe of Invulnerability creates a stationary protective zone. If the target moves, they leave the protection behind.

---

## Target State

### Akitaro's Staff (Updated Boosts)

**New Boosts:**
```
data "Boosts" "UnlockSpell(SMR_Target_Light_Unlimited);UnlockInterrupt(SMR_Interrupt_Counterspell_Unlimited);UnlockSpell(SMR_Shout_CelestialHaste_Unlimited);UnlockSpell(Shout_MAG_TheChromatic_ChromaticAttunement);UnlockSpell(Shout_MAG_SpellSlotRestoration);UnlockSpell(Shout_MAG_SpellSlotRestoration_PearlOfPower);UnlockInterrupt(SMR_Interrupt_Shield_Unlimited);UnlockSpell(SMR_Projectile_AkitarosBlast_ShortRest);UnlockSpell(SMR_Target_AkitarosTeleport_ShortRest);UnlockSpell(SMR_Projectile_AkitarosBarrage_Unlimited);UnlockSpell(SMR_Target_AkitarosShield_ShortRest);UnlockSpell(SMR_Projectile_ChromaticOrb_Unlimited);UnlockSpell(SMR_Teleportation_ArcaneGate_ShortRest);UnlockSpell(SMR_Target_Knock_Unlimited)"
```

**New Spells (14 total):**
1. Light (unlimited)
2. Counterspell (unlimited, interrupt)
3. Celestial Haste (unlimited)
4. Chromatic Attunement (spell slot restoration)
5. Spell Slot Restoration
6. Pearlescent Restoration
7. Shield (unlimited, interrupt)
8. Akitaro's Blast (short rest)
9. Akitaro's Teleport/Misty Step (short rest)
10. Akitaro's Barrage/Magic Missile (unlimited)
11. Akitaro's Shield (short rest) - **MODIFIED** to use Silvered Bulwark
12. **Chromatic Orb (unlimited)** - NEW
13. **Arcane Gate (short rest)** - NEW
14. **Knock (unlimited)** - NEW

### Akitaro's Shield (Updated with Silvered Bulwark)

**New Implementation:**
```
new entry "SMR_Target_AkitarosShield_ShortRest"
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
data "DisplayName" "ha3b4c5d6g7e8fg9a0bg1c2dg3e4f5a6b7c8d9;1"
data "ExtraDescription" "hb4c5d6e7g8f9ag0b1cg2d3eg4f5a6b7c8d9e0;1"
data "TooltipStatusApply" "ApplyStatus(LOW_RAMAZITHSTOWER_NIGHTSONG_GLOBE_FUNCTIONAL_AURA,100,-1)"
data "CastSound" "Spell_Cast_Control_GlobeOfInvulnerability_L6to8"
data "TargetSound" "Spell_Impact_Control_GlobeOfInvulnerability_L6to8"
data "PreviewCursor" "Cast"
data "CastTextEvent" "Cast"
data "UseCosts" "BonusActionPoint:1"
data "SpellAnimation" "554a18f7-952e-494a-b301-7702a85d4bc9,,;,,;ab7b6aac-b3c9-4918-8f17-f777a94dcb5e,,;57211a11-ed0b-46d7-9369-81df25a85df6,,;22dfbbf4-f417-4c84-b39e-2039315961e6,,;,,;5bfbe9f9-4fc3-4f26-b112-43d404db6a89,,;,,;,,"
data "VerbalIntent" "Buff"
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsConcentration;IsSpell"
data "HitAnimationType" "MagicalNonDamage"
data "SpellAnimationIntentType" "Aggressive"
data "Sheathing" "DontChange"
data "Cooldown" "OncePerShortRest"
```

**Changes from Current:**
- Added explicit spell properties matching Silvered Bulwark
- Added `SpellProperties` to apply Silvered Bulwark status
- Added `TargetConditions` to prevent stacking
- Added `TooltipStatusApply` to show invulnerability status
- Added sound effects, animations, and other spell metadata
- Applies `LOW_RAMAZITHSTOWER_NIGHTSONG_GLOBE_FUNCTIONAL_AURA` status (invulnerability + advantage on saves)
- Protective aura now follows the target
- Maintains original cooldown (once per short rest) and cost (bonus action)

**Result:** Akitaro's Shield becomes a mobile protective buff that follows the target, similar to the Silvered Bulwark spell from Phase 052.

### New Spell: Chromatic Orb (SMR_Projectile_ChromaticOrb_Unlimited)

**File:** `SampleMagicRingMod/Public/SampleMagicRingMod/Stats/Generated/Data/Spell_Projectile.txt`

**New Spell Entry:**
```
new entry "SMR_Projectile_ChromaticOrb_Unlimited"
type "SpellData"
data "SpellType" "Projectile"
using "Projectile_ChromaticOrb"
data "UseCosts" "ActionPoint:1"
```

**Purpose:**
- Grants unlimited casting of Chromatic Orb (level 1 evocation spell)
- Deals 3d8 elemental damage (choice of Acid, Cold, Fire, Lightning, Poison, or Thunder)
- Matches Staff of the Archmage implementation from Level13PlusGear
- No spell slot cost, just action point

### Existing Spells to Add

**Arcane Gate (SMR_Teleportation_ArcaneGate_ShortRest):**
- Already exists in SampleMagicRingMod (used by Ring of Spectral Power)
- Once per short rest teleportation portal
- No modifications needed, just add to staff's Boosts

**Knock (SMR_Target_Knock_Unlimited):**
- Already exists in SampleMagicRingMod (used by Ring of Spectral Power)
- Unlimited casting to unlock doors and containers
- No modifications needed, just add to staff's Boosts

---

## Rationale

### Why Change from Globe of Invulnerability to Silvered Bulwark?

**Globe of Invulnerability Limitations:**
- Creates a stationary 3m radius zone
- Target must stay within the zone to benefit
- Movement breaks protection
- Limited tactical flexibility

**Silvered Bulwark Benefits:**
- Protection follows the target as they move
- More versatile in combat
- Better for mobile characters
- Consistent with Phase 052 implementation (L13_Target_SilveredBulwark)

**Gameplay Consideration:**
Like all Silvered Bulwark implementations, the protective bubble also affects nearby creatures including enemies. This means:
- Best used on ranged characters
- Effective for moving through hazards
- Less effective for melee combatants (enemies become invulnerable when engaged)

### Consistency with Level13PlusGear

This change aligns SampleMagicRingMod with the custom Silvered Bulwark spell created in Phase 052 for Level13PlusGear, using the same spell mechanics and status effects.

---

## Implementation Plan

### Task 1: Create Chromatic Orb Spell

**Description:** Create SMR_Projectile_ChromaticOrb_Unlimited spell for unlimited casting

**Steps:**
1. Open `SampleMagicRingMod/Public/SampleMagicRingMod/Stats/Generated/Data/Spell_Projectile.txt`
2. Add new spell entry at end of file
3. Base on Projectile_ChromaticOrb
4. Set UseCosts to ActionPoint:1 only (no spell slot cost)
5. Save file

**Files to modify:**
- `SampleMagicRingMod/Public/SampleMagicRingMod/Stats/Generated/Data/Spell_Projectile.txt` - Add Chromatic Orb spell

### Task 2: Update Akitaro's Staff Boosts

**Description:** Add Chromatic Orb, Arcane Gate, and Knock spells to staff

**Steps:**
1. Open `SampleMagicRingMod/Public/SampleMagicRingMod/Stats/Generated/Data/Weapon.txt`
2. Locate SMR_Staff_Akitaro entry (lines 10-18)
3. Update Boosts line to include three new spells:
   - `UnlockSpell(SMR_Projectile_ChromaticOrb_Unlimited)`
   - `UnlockSpell(SMR_Teleportation_ArcaneGate_ShortRest)`
   - `UnlockSpell(SMR_Target_Knock_Unlimited)`
4. Save file

**Files to modify:**
- `SampleMagicRingMod/Public/SampleMagicRingMod/Stats/Generated/Data/Weapon.txt` - Update Boosts

### Task 3: Update Akitaro's Shield Spell Definition

**Description:** Modify SMR_Target_AkitarosShield_ShortRest to use Silvered Bulwark properties

**Steps:**
1. Open `SampleMagicRingMod/Public/SampleMagicRingMod/Stats/Generated/Data/Spell_Target.txt`
2. Locate SMR_Target_AkitarosShield_ShortRest spell (lines 125-132)
3. Replace the spell definition with Silvered Bulwark properties
4. Maintain existing DisplayName and ExtraDescription handles
5. Keep existing cooldown (OncePerShortRest)
6. Save file

**Files to modify:**
- `SampleMagicRingMod/Public/SampleMagicRingMod/Stats/Generated/Data/Spell_Target.txt` - Update spell definition

### Task 4: Update Version

**Description:** Increment mod version for new build

**Steps:**
1. Open `SampleMagicRingMod/Mods/SampleMagicRingMod/meta.lsx`
2. Increment Version64
3. Save file

**Files to modify:**
- `SampleMagicRingMod/Mods/SampleMagicRingMod/meta.lsx` - Increment version

---

## Detailed Implementation

### Step 1: Create Chromatic Orb Spell

**File:** `SampleMagicRingMod/Public/SampleMagicRingMod/Stats/Generated/Data/Spell_Projectile.txt`

**Add at end of file:**
```
new entry "SMR_Projectile_ChromaticOrb_Unlimited"
type "SpellData"
data "SpellType" "Projectile"
using "Projectile_ChromaticOrb"
data "UseCosts" "ActionPoint:1"
```

**Purpose:** Grant unlimited level 1 Chromatic Orb spell (3d8 elemental damage, choice of damage type)

### Step 2: Update Akitaro's Staff Boosts

**File:** `SampleMagicRingMod/Public/SampleMagicRingMod/Stats/Generated/Data/Weapon.txt`

**Current Boosts (Line 15):**
```
data "Boosts" "UnlockSpell(SMR_Target_Light_Unlimited);UnlockInterrupt(SMR_Interrupt_Counterspell_Unlimited);UnlockSpell(SMR_Shout_CelestialHaste_Unlimited);UnlockSpell(Shout_MAG_TheChromatic_ChromaticAttunement);UnlockSpell(Shout_MAG_SpellSlotRestoration);UnlockSpell(Shout_MAG_SpellSlotRestoration_PearlOfPower);UnlockInterrupt(SMR_Interrupt_Shield_Unlimited);UnlockSpell(SMR_Projectile_AkitarosBlast_ShortRest);UnlockSpell(SMR_Target_AkitarosTeleport_ShortRest);UnlockSpell(SMR_Projectile_AkitarosBarrage_Unlimited);UnlockSpell(SMR_Target_AkitarosShield_ShortRest)"
```

**New Boosts:**
```
data "Boosts" "UnlockSpell(SMR_Target_Light_Unlimited);UnlockInterrupt(SMR_Interrupt_Counterspell_Unlimited);UnlockSpell(SMR_Shout_CelestialHaste_Unlimited);UnlockSpell(Shout_MAG_TheChromatic_ChromaticAttunement);UnlockSpell(Shout_MAG_SpellSlotRestoration);UnlockSpell(Shout_MAG_SpellSlotRestoration_PearlOfPower);UnlockInterrupt(SMR_Interrupt_Shield_Unlimited);UnlockSpell(SMR_Projectile_AkitarosBlast_ShortRest);UnlockSpell(SMR_Target_AkitarosTeleport_ShortRest);UnlockSpell(SMR_Projectile_AkitarosBarrage_Unlimited);UnlockSpell(SMR_Target_AkitarosShield_ShortRest);UnlockSpell(SMR_Projectile_ChromaticOrb_Unlimited);UnlockSpell(SMR_Teleportation_ArcaneGate_ShortRest);UnlockSpell(SMR_Target_Knock_Unlimited)"
```

**Purpose:** Add three new spells to Akitaro's Staff

### Step 3: Update Akitaro's Shield Spell Definition

**File:** `SampleMagicRingMod/Public/SampleMagicRingMod/Stats/Generated/Data/Spell_Target.txt`

**Current (Lines 125-132):**
```
new entry "SMR_Target_AkitarosShield_ShortRest"
type "SpellData"
data "SpellType" "Target"
using "Target_GlobeOfInvulnerability"
data "DisplayName" "ha3b4c5d6g7e8fg9a0bg1c2dg3e4f5a6b7c8d9;1"
data "ExtraDescription" "hb4c5d6e7g8f9ag0b1cg2d3eg4f5a6b7c8d9e0;1"
data "UseCosts" "BonusActionPoint:1"
data "Cooldown" "OncePerShortRest"
```

**New:**
```
new entry "SMR_Target_AkitarosShield_ShortRest"
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
data "DisplayName" "ha3b4c5d6g7e8fg9a0bg1c2dg3e4f5a6b7c8d9;1"
data "ExtraDescription" "hb4c5d6e7g8f9ag0b1cg2d3eg4f5a6b7c8d9e0;1"
data "TooltipStatusApply" "ApplyStatus(LOW_RAMAZITHSTOWER_NIGHTSONG_GLOBE_FUNCTIONAL_AURA,100,-1)"
data "CastSound" "Spell_Cast_Control_GlobeOfInvulnerability_L6to8"
data "TargetSound" "Spell_Impact_Control_GlobeOfInvulnerability_L6to8"
data "PreviewCursor" "Cast"
data "CastTextEvent" "Cast"
data "UseCosts" "BonusActionPoint:1"
data "SpellAnimation" "554a18f7-952e-494a-b301-7702a85d4bc9,,;,,;ab7b6aac-b3c9-4918-8f17-f777a94dcb5e,,;57211a11-ed0b-46d7-9369-81df25a85df6,,;22dfbbf4-f417-4c84-b39e-2039315961e6,,;,,;5bfbe9f9-4fc3-4f26-b112-43d404db6a89,,;,,;,,"
data "VerbalIntent" "Buff"
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsConcentration;IsSpell"
data "HitAnimationType" "MagicalNonDamage"
data "SpellAnimationIntentType" "Aggressive"
data "Sheathing" "DontChange"
data "Cooldown" "OncePerShortRest"
```

**Purpose:** Transform Akitaro's Shield from stationary Globe to mobile Silvered Bulwark while maintaining once per short rest cooldown

### Step 2: Increment Version

**File:** `SampleMagicRingMod/Mods/SampleMagicRingMod/meta.lsx`

Increment Version64 value for new mod build.

**Purpose:** Track mod version for release management

---

## Files to Modify

| File | Action | Description |
|------|--------|-------------|
| `SampleMagicRingMod/Public/SampleMagicRingMod/Stats/Generated/Data/Spell_Projectile.txt` | Edit | Add SMR_Projectile_ChromaticOrb_Unlimited spell |
| `SampleMagicRingMod/Public/SampleMagicRingMod/Stats/Generated/Data/Weapon.txt` | Edit | Update SMR_Staff_Akitaro Boosts to add 3 new spells |
| `SampleMagicRingMod/Public/SampleMagicRingMod/Stats/Generated/Data/Spell_Target.txt` | Edit | Replace SMR_Target_AkitarosShield_ShortRest spell definition with Silvered Bulwark properties |
| `SampleMagicRingMod/Mods/SampleMagicRingMod/meta.lsx` | Edit | Increment version number |

---

## UUID/Handle Requirements

**None** - This phase only modifies an existing spell. All existing handles and UUIDs remain unchanged:
- DisplayName handle: `ha3b4c5d6g7e8fg9a0bg1c2dg3e4f5a6b7c8d9`
- ExtraDescription handle: `hb4c5d6e7g8f9ag0b1cg2d3eg4f5a6b7c8d9e0`

---

## Testing Plan

### Test 1: New Spells Availability

1. Equip Akitaro's Staff
2. Check spell list
3. **Verify:** All 14 spells appear including:
   - Chromatic Orb (new)
   - Arcane Gate (new)
   - Knock (new)
   - Akitaro's Shield (existing, will be modified)
4. **Verify:** Correct icons and names for new spells

### Test 2: Chromatic Orb Functionality

1. Equip Akitaro's Staff
2. Enter combat
3. Cast Chromatic Orb on an enemy
4. **Verify:** Spell selection shows elemental damage type choices (Acid, Cold, Fire, Lightning, Poison, Thunder)
5. Select a damage type and cast
6. **Verify:** Spell costs action point only (no spell slot)
7. **Verify:** Deals 3d8 damage of chosen type
8. **Verify:** Can cast repeatedly (unlimited)
9. Check combat log
10. **Verify:** Damage type matches selection

### Test 3: Arcane Gate Functionality

1. Equip Akitaro's Staff
2. Cast Arcane Gate
3. **Verify:** First portal placement works
4. **Verify:** Second portal placement works
5. **Verify:** Portals connect correctly
6. **Verify:** Can teleport through portals
7. **Verify:** Spell goes on short rest cooldown
8. **Verify:** Cannot cast again until short rest
9. Take short rest
10. **Verify:** Spell becomes available again

### Test 4: Knock Functionality

1. Equip Akitaro's Staff
2. Find locked door or container
3. Cast Knock on locked object
4. **Verify:** Lock opens automatically
5. **Verify:** No lockpicking required
6. **Verify:** Spell costs action point
7. **Verify:** Can cast repeatedly (unlimited)
8. Find multiple locked objects
9. **Verify:** Knock works on all lock types

### Test 5: Akitaro's Shield Spell Availability

1. Equip Akitaro's Staff
2. Check spell list
3. **Verify:** "Akitaro's Shield" spell appears
4. **Verify:** Shows correct icon (Globe of Invulnerability icon)
5. **Verify:** DisplayName and description are correct

### Test 6: Akitaro's Shield Spell Casting

1. Enter combat
2. Cast Akitaro's Shield on an ally
3. **Verify:** Spell accepts valid targets (allies, self)
4. **Verify:** Spell costs bonus action
5. **Verify:** Concentration icon appears
6. **Verify:** Visual effect (globe) appears around target
7. **Verify:** Target receives invulnerability status

### Test 7: Mobile Protection

1. Cast Akitaro's Shield on ally
2. Move the protected ally
3. **Verify:** Protective globe follows the ally
4. **Verify:** Ally remains invulnerable while moving
5. **Verify:** Globe doesn't stay in original location (unlike normal Globe of Invulnerability)

### Test 8: Invulnerability Effect

1. Cast Akitaro's Shield on ally
2. Have enemy attack the protected ally
3. **Verify:** All damage is negated (0 damage)
4. **Verify:** Ally shows invulnerable status
5. **Verify:** Combat log shows damage negated

### Test 9: Concentration Mechanics

1. Cast Akitaro's Shield
2. **Verify:** Concentration icon appears
3. Cast another concentration spell
4. **Verify:** Akitaro's Shield ends (concentration broken)
5. **Verify:** Invulnerability status removed

### Test 10: Akitaro's Shield Cooldown

1. Cast Akitaro's Shield
2. **Verify:** Spell goes on cooldown
3. **Verify:** Shows "Once per short rest" cooldown
4. Try to cast again before short rest
5. **Verify:** Spell is unavailable (grayed out)
6. Take short rest
7. **Verify:** Spell becomes available again

### Test 11: Targeting Restrictions

1. Cast Akitaro's Shield on an ally
2. Try to cast on same ally again while buff is active
3. **Verify:** Ally shows as invalid target (already has invulnerability)
4. Wait for buff to expire
5. **Verify:** Ally becomes valid target again

### Test 12: Bubble Mechanic (Gameplay Limitation)

1. Cast Akitaro's Shield on melee character
2. Move character into melee range with enemy
3. Attack enemy
4. **Verify:** Enemy may also be protected by bubble (becomes invulnerable)
5. **Note:** This is expected behavior - bubble protects all creatures in range

---

## Success Criteria

**Chromatic Orb:**
- [ ] SMR_Projectile_ChromaticOrb_Unlimited spell created
- [ ] Spell added to Akitaro's Staff Boosts
- [ ] Spell appears in spell list when staff equipped
- [ ] Spell allows choosing elemental damage type
- [ ] Spell deals 3d8 damage of chosen type
- [ ] Spell has unlimited uses (no spell slot cost)

**Arcane Gate:**
- [ ] SMR_Teleportation_ArcaneGate_ShortRest added to staff Boosts
- [ ] Spell appears in spell list when staff equipped
- [ ] Spell creates two connected portals
- [ ] Portals allow teleportation
- [ ] Spell recharges on short rest

**Knock:**
- [ ] SMR_Target_Knock_Unlimited added to staff Boosts
- [ ] Spell appears in spell list when staff equipped
- [ ] Spell unlocks locked doors and containers
- [ ] Spell has unlimited uses

**Akitaro's Shield (Silvered Bulwark):**
- [ ] Spell definition updated with Silvered Bulwark properties
- [ ] Spell maintains correct DisplayName and ExtraDescription
- [ ] Spell maintains once per short rest cooldown
- [ ] Spell accepts valid targets (allies and self)
- [ ] Spell applies invulnerability status to target
- [ ] Protective bubble follows target as they move
- [ ] Invulnerability negates all damage
- [ ] Concentration mechanics work correctly
- [ ] Cooldown works correctly (once per short rest)

**General:**
- [ ] Version incremented
- [ ] All 14 spells appear on staff
- [ ] Testing completed and verified

---

## Technical Notes

### Silvered Bulwark vs Globe of Invulnerability

**Key Differences:**
- **Globe of Invulnerability:** Creates stationary 3m zone, target must stay inside
- **Silvered Bulwark:** Protective bubble follows target, more mobile

**Shared Characteristics:**
- Both grant complete invulnerability
- Both require concentration
- Both use same visual effects
- Both protect creatures within the bubble (including enemies in melee range)

### Status Applied

**LOW_RAMAZITHSTOWER_NIGHTSONG_GLOBE_FUNCTIONAL_AURA:**
- Grants complete invulnerability (Invulnerable() boost)
- Grants advantage on all saving throws
- Displays invulnerability visual indicator
- Follows the target (attached to character, not ground)

### Consistency with Phase 052

This implementation uses the same approach as L13_Target_SilveredBulwark from Phase 052:
- Same SpellProperties
- Same TargetConditions
- Same status application (LOW_RAMAZITHSTOWER_NIGHTSONG_GLOBE_FUNCTIONAL_AURA)
- Only difference: Cooldown (short rest vs long rest)

---

## Dependencies

**This phase depends on:**
- SampleMagicRingMod (existing)
- Akitaro's Staff (existing)
- Vanilla BG3 Silvered Bulwark status effects
- Phase 052 learnings (Silvered Bulwark implementation)

**This phase affects:**
- Akitaro's Staff functionality
- Players using Akitaro's Shield spell

---

## Related Documentation

- **CLAUDE.md** - Active mods and project structure
- **Phase 052** - Silverlight sword with custom Silvered Bulwark implementation
- **docs/instructions/interesting_magical_effects.md** - Silvered Bulwark documentation and implementation challenges

---

## Notes

- This is a modification phase, not new content creation
- No new UUIDs or handles needed
- Maintains backward compatibility (same spell name and handles)
- Based on Phase 052 custom Silvered Bulwark implementation
- Shares same gameplay limitation as all Silvered Bulwark implementations (bubble protects nearby enemies)
- Once per short rest is more frequent than Phase 052's once per long rest (appropriate for different power level)

---

## Phase 053 Status: IMPLEMENTED

Akitaro's Staff enhancements have been implemented.

**Completed Changes:**

1. **Akitaro's Shield (Silvered Bulwark):**
   - ✅ Replace Globe of Invulnerability base with Silvered Bulwark properties
   - ✅ Protection follows target instead of being stationary
   - ✅ Maintains once per short rest cooldown
   - ✅ User tested and confirmed working

2. **New Spell: Chromatic Orb**
   - ✅ Create SMR_Projectile_ChromaticOrb_Unlimited spell
   - ✅ Unlimited level 1 evocation spell (3d8 elemental damage)
   - ✅ Choice of 6 damage types works correctly
   - ✅ User tested and confirmed working

3. **Add Arcane Gate:**
   - ✅ Add existing SMR_Teleportation_ArcaneGate_ShortRest to staff
   - ✅ Once per short rest portal creation
   - ✅ User tested and confirmed working

4. **Add Knock:**
   - ✅ Add existing SMR_Target_Knock_Unlimited to staff
   - ✅ Unlimited lock opening utility
   - ✅ User tested and confirmed working

**Implementation Details:**
- ✅ Created SMR_Projectile_ChromaticOrb_Unlimited spell in Spell_Projectile.txt
- ✅ Updated SMR_Staff_Akitaro Boosts to add 3 new spells
- ✅ Updated SMR_Target_AkitarosShield_ShortRest with Silvered Bulwark properties
- ✅ Incremented Version64 from 36028910835597312 to 36028910835597313
- ✅ All features tested and verified working by user

**Result:** Akitaro's Staff is now a complete and versatile legendary quarterstaff with improved protection (mobile Silvered Bulwark), offensive capability (Chromatic Orb with 6 damage types), mobility (Arcane Gate portals), and utility (Knock for locks). Total of 14 spells, up from 11. All functionality confirmed working in-game.

**Testing Complete:** All features verified working in-game by user. Phase marked as COMPLETE.
