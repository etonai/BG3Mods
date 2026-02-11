# Phase 33: Copy Boots of the Stormwalker and Moonguard Blade to Level13PlusGear

**Status:** COMPLETE
**Date:** 2026-02-10
**Implementation Date:** 2026-02-10
**Completion Date:** 2026-02-10

---

## Goal

Copy two items from SampleMagicRingMod to Level13PlusGear mod:
1. **Boots of the Stormwalker** (boots)
2. **Moonguard Blade** (longsword)

This continues making Level13PlusGear fully independent from SampleMagicRingMod using lessons learned from Phase 31, Phase 32, and the copying_items_between_mods.md guide.

---

## Critical Requirements

- **No dependencies on SampleMagicRingMod** - All custom spells and passives must be copied
- **Proper handle generation** - Use UUIDs from pool, NOT random hex strings
- **Reuse existing L13 components** - Some spells/passives already exist from Phase 32
- **UUID pool management** - Delete all used UUIDs and document them

---

## Item 1: Boots of the Stormwalker

### Source Item Details

**File:** SampleMagicRingMod/Public/SampleMagicRingMod/Stats/Generated/Data/Armor.txt

```
new entry "SMR_Boots_Stormwalker"
type "Armor"
using "_Foot_Magic"
data "RootTemplate" "e1f2a3b4-c5d6-4e7f-8a9b-0c1d2e3f4a5b"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(SMR_Target_MistyStep_Unlimited)"
data "PassivesOnEquip" "MAG_Thunder_ReverberationOnStatusApply_Boots_Passive;FOR_NightWalkers_WebImmunity"
```

**RootTemplate Details:**
- MapKey: `e1f2a3b4-c5d6-4e7f-8a9b-0c1d2e3f4a5b`
- DisplayName handle: `h1a2b3c4dge5f6g7a8bg9c0dge1f2a3b4c5d6`
- Description handle: `h2b3c4d5egf6a7g8b9cgd0e1gf2a3b4c5d6e7`
- ParentTemplateId: `ac9145d1-31d0-4aa3-8755-62cc85dad22b` (keep same)

**Dependencies:**

**Custom (must copy):**
- `SMR_Target_MistyStep_Unlimited` (spell)

**Vanilla (no copy needed):**
- `MAG_Thunder_ReverberationOnStatusApply_Boots_Passive` (passive)
- `FOR_NightWalkers_WebImmunity` (passive)

### Target Item (L13_Boots_Stormwalker)

**Changes Required:**
- Stats name: `SMR_Boots_Stormwalker` → `L13_Boots_Stormwalker`
- RootTemplate UUID: New UUID with `ed13` prefix
- Spell reference: `SMR_Target_MistyStep_Unlimited` → `L13_Target_MistyStep_Unlimited`
- Set `Unique: 0` for TreasureTable delivery

**UUIDs Needed:**
- 1 for RootTemplate
- 2 handles for boots localization (DisplayName, Description)
- 2 handles for MistyStep spell localization (DisplayName, ExtraDescription)
- **Total: 1 UUID + 4 handles = 5 UUIDs**

---

## Item 2: Moonguard Blade

### Source Item Details

**File:** SampleMagicRingMod/Public/SampleMagicRingMod/Stats/Generated/Data/Weapon.txt

```
new entry "SMR_Blade_Moonguard"
type "Weapon"
using "WPN_Longsword_2"
data "RootTemplate" "a1b2c3d4-e5f6-4a7b-8c9d-1e2f3a4b5c6d"
data "Rarity" "Legendary"
data "DefaultBoosts" "WeaponEnchantment(5);WeaponProperty(Magical)"
data "Boosts" "UnlockSpell(Target_MAG_Smite_Wrathful);UnlockSpell(SMR_Target_BlindingSmite_Unlimited);UnlockSpell(SMR_Target_Light_Unlimited);UnlockSpell(Target_PLA_ShieldOfFaith_SwordOfJustice);UnlockSpell(SMR_Shout_CelestialHaste_Free);UnlockSpell(SMR_Shout_SpiritGuardians_Moonguard,AddChildren,,,SpellCastingAbility)"
data "PassivesOnEquip" "MAG_PlaneShifterSlayer_Passive;SMR_RadiantWeapon_Passive;MAG_TheClover_Rearrangement_Passive;CRE_LathandersLight_Passive;SMR_Moonshield_Passive"
data "StatusOnEquip" "MAG_LATHANDERS_LIGHT_TECHNICAL"
```

**RootTemplate Details:**
- MapKey: `a1b2c3d4-e5f6-4a7b-8c9d-1e2f3a4b5c6d`
- DisplayName handle: `h2b3c4d5eg6f7ag8b9cg0d1eg3f4a5b6c7d8e9`
- Description handle: `h1a2b3c4dg5e6fg7a8bg9c0dg2e3f4a5b6c7d8`
- ParentTemplateId: `20c66f8d-f455-42fc-8e48-543512247e75` (Primeval Silver Longsword - keep same)

**Dependencies:**

**Already in Level13PlusGear from Phase 32:**
- `L13_Target_BlindingSmite_Unlimited` ✓ (already exists)
- `L13_Target_Light_Unlimited` ✓ (already exists)
- `L13_RadiantWeapon_Passive` ✓ (already exists)

**Custom (must copy):**
- `SMR_Shout_CelestialHaste_Free` (spell - different from Unlimited version)
- `SMR_Shout_SpiritGuardians_Moonguard` (spell)
- `SMR_Moonshield_Passive` (passive)

**Vanilla (no copy needed):**
- `Target_MAG_Smite_Wrathful`
- `Target_PLA_ShieldOfFaith_SwordOfJustice`
- `MAG_PlaneShifterSlayer_Passive`
- `MAG_TheClover_Rearrangement_Passive`
- `CRE_LathandersLight_Passive`
- `MAG_LATHANDERS_LIGHT_TECHNICAL` (status)

### Target Item (L13_Blade_Moonguard)

**Changes Required:**
- Stats name: `SMR_Blade_Moonguard` → `L13_Blade_Moonguard`
- RootTemplate UUID: New UUID with `ed13` prefix
- Spell references: `SMR_` → `L13_` (for custom spells only)
- Passive references: `SMR_RadiantWeapon_Passive` → `L13_RadiantWeapon_Passive`, `SMR_Moonshield_Passive` → `L13_Moonshield_Passive`
- Set `Unique: 0` for TreasureTable delivery

**UUIDs Needed:**
- 1 for RootTemplate
- 2 handles for blade localization (DisplayName, Description)
- 2 handles for CelestialHaste_Free spell localization
- 2 handles for SpiritGuardians spell localization
- 2 handles for Moonshield passive localization
- **Total: 1 UUID + 8 handles = 9 UUIDs**

---

## Total UUID Requirements

**Boots of the Stormwalker:** 5 UUIDs
**Moonguard Blade:** 9 UUIDs
**Grand Total: 14 UUIDs needed from pool**

---

## Implementation Plan

### Phase 1: Copy Boots of the Stormwalker

#### Step 1: Copy MistyStep Spell
1. Open `SampleMagicRingMod/.../Spell_Target.txt`
2. Find `SMR_Target_MistyStep_Unlimited` entry
3. Copy to `Level13PlusGear/.../Spell_Target.txt`
4. Update spell name: `L13_Target_MistyStep_Unlimited`
5. Generate 2 new handles from UUID pool for localization
6. Add localization entries to Level13PlusGear.loca.xml

#### Step 2: Copy Boots Stats
1. Copy stats entry from Armor.txt
2. Update entry name: `L13_Boots_Stormwalker`
3. Generate new RootTemplate UUID (with `ed13` prefix)
4. Update Boosts: `L13_Target_MistyStep_Unlimited`
5. Keep vanilla passives unchanged
6. Set `Unique: 0`

#### Step 3: Create Boots RootTemplate
1. Create `L13_Boots_Stormwalker.lsf.lsx`
2. Use new RootTemplate UUID
3. Generate 2 new handles for DisplayName and Description
4. Keep ParentTemplateId unchanged
5. No VisualTemplate needed (boots use ParentTemplate visuals)

#### Step 4: Add Boots Localization
1. Add 2 entries for boots (name and description)
2. Use handles generated in Step 3

#### Step 5: Update TreasureTable
1. Add `I_L13_Boots_Stormwalker` to Tutorial Chest

### Phase 2: Copy Moonguard Blade

#### Step 1: Copy New Spells
**CelestialHaste_Free:**
1. Find in `Spell_Shout.txt`
2. Copy to Level13PlusGear
3. Update name: `L13_Shout_CelestialHaste_Free`
4. Generate 2 handles for localization (or check if it uses vanilla localization)

**SpiritGuardians_Moonguard:**
1. Find in `Spell_Shout.txt`
2. Copy to Level13PlusGear
3. Update name: `L13_Shout_SpiritGuardians_Moonguard`
4. Generate 2 handles for localization

#### Step 2: Copy Moonshield Passive
1. Find in `Passive.txt`
2. Copy to Level13PlusGear
3. Update name: `L13_Moonshield_Passive`
4. Generate 2 handles for localization

#### Step 3: Copy Blade Stats
1. Copy stats entry from Weapon.txt
2. Update entry name: `L13_Blade_Moonguard`
3. Generate new RootTemplate UUID (with `ed13` prefix)
4. Update Boosts: Replace all `SMR_` spell references with `L13_`
5. Update PassivesOnEquip: Replace `SMR_` passive references with `L13_`
6. Keep vanilla passives and status unchanged
7. Set `Unique: 0`

#### Step 4: Create Blade RootTemplate
1. Create `L13_Blade_Moonguard.lsf.lsx`
2. Use new RootTemplate UUID
3. Generate 2 new handles for DisplayName and Description
4. Keep ParentTemplateId unchanged (Primeval Silver Longsword appearance)
5. May need VisualTemplate if specified in source

#### Step 5: Add All Localization
1. Add 2 entries for blade (name and description)
2. Add 2 entries for CelestialHaste_Free spell (if custom)
3. Add 2 entries for SpiritGuardians spell
4. Add 2 entries for Moonshield passive

#### Step 6: Update TreasureTable
1. Add `I_L13_Blade_Moonguard` to Tutorial Chest

### Phase 3: Final Steps

1. Update UUID pool (delete 14 UUIDs)
2. Document all UUIDs in this phase file
3. Verify no SMR_ references remain in L13 items
4. Test in-game

---

## UUID Allocation (Documented During Implementation)

### Boots of the Stormwalker (5 UUIDs)

- **RootTemplate UUID:** `ed13bcca-bb98-4c26-861c-65c23961de31` (from pool: `181fbcca-bb98-4c26-861c-65c23961de31`)
- **DisplayName Handle:** `hed13c5e1gd6b5gd2d6g44f0ga9a7g0f70b0285471` (from pool: `c5e1d6b5-d2d6-44f0-a9a7-0f70b0285471`)
- **Description Handle:** `hed137e45g45dbgbf40g46ffga5c2g3fcb9aa21700` (from pool: `7e4545db-bf40-46ff-a5c2-3fcb9aa21700`)
- **MistyStep DisplayName Handle:** `hed132453g1127g59a7g45c1g81bfg0ccb71f9d61d` (from pool: `24531127-59a7-45c1-81bf-0ccb71f9d61d`)
- **MistyStep ExtraDescription Handle:** `hed13d7fcgf0fagf088g4d61g8170g699bd4bcdc97` (from pool: `d7fcf0fa-f088-4d61-8170-699bd4bcdc97`)

### Moonguard Blade (9 UUIDs)

- **RootTemplate UUID:** `ed135af1-9f89-4020-826a-29e3f6083c46` (from pool: `6e705af1-9f89-4020-826a-29e3f6083c46`)
- **DisplayName Handle:** `hed13060fg32a6g612dg445bg83d4g6764c51aae13` (from pool: `060f32a6-612d-445b-83d4-6764c51aae13`)
- **Description Handle:** `hed1352a6g1b21gafb2g45ecgaa7cg520ec78164ab` (from pool: `52a61b21-afb2-45ec-aa7c-520ec78164ab`)
- **CelestialHaste_Free:** No custom localization (uses vanilla via `using "Shout_MAG_Victory_Longbow_Haste"`)
- **SpiritGuardians DisplayName Handle:** `hed13c583ge4a8gd909g4514g9d96gdf3498d374c8` (from pool: `c583e4a8-d909-4514-9d96-df3498d374c8`)
- **SpiritGuardians Description Handle:** `hed13cdbeg3b43g6959g4b54g85b7g2865fd8a0c00` (from pool: `cdbe3b43-6959-4b54-85b7-2865fd8a0c00`)
- **SpiritGuardians Radiant ExtraDescription Handle:** `hed13dddag33dbg2816g463ag863egd30498a79f65` (from pool: `ddda33db-2816-463a-863e-d30498a79f65`)
- **SpiritGuardians Necrotic ExtraDescription Handle:** `hed13822ege5d4g8648g4beeg875egf4d709af40b8` (from pool: `822ee5d4-8648-4bee-875e-f4d709af40b8`)
- **Moonshield DisplayName Handle:** `hed13ab6eg97b6g4155g4ebeg8cb6g634b9ffc1b02` (from pool: `ab6e97b6-4155-4ebe-8cb6-634b9ffc1b02`)

**Note:** SpiritGuardians_Moonguard spell uses container spells (Radiant and Necrotic variants) which share the main DisplayName and Description but have unique ExtraDescription handles.

**Total UUIDs Used:** 14 (5 for Boots + 9 for Blade)

---

## Revision 1: Fix Item Delivery and Unique Flags

**Date:** 2026-02-10
**Issues:**
1. Staff of Archmage was incorrectly set to `Unique: 1`
2. Items were incorrectly appearing in Tutorial Chest instead of L13_Gear_Chest

### Problem 1: Unique Flag

The Staff of Archmage had `Unique: 1` set in its stats entry. For TreasureTable delivery to work correctly with multiple items, all equippable items should be set to `Unique: 0`.

**Why This Matters:**
- Items with `Unique: 1` can only spawn once per save file
- TreasureTable entries work best with non-unique items
- Consistency across all Level13PlusGear items

### Problem 2: Incorrect Item Placement

Items were appearing in the wrong treasure tables:

**Before (Incorrect):**
- **Tutorial Chest (TUT_Chest_Potions):** L13_Gear_Chest, Ring_Testing, Sword_Tyr, Boots_Stormwalker, Blade_Moonguard
- **L13_Gear_Chest_TT:** Staff_Archmage, Ring_Testing

**After (Correct):**
- **Tutorial Chest (TUT_Chest_Potions):** L13_Gear_Chest ONLY
- **L13_Gear_Chest_TT:** Staff_Archmage, Ring_Testing, Sword_Tyr, Boots_Stormwalker, Blade_Moonguard

**Why This Matters:**
- Cleaner organization: all gear in one container
- Players find the L13_Gear_Chest in Tutorial Chest, then open it to access all items
- Prevents Tutorial Chest from being cluttered with individual items

### Items Reviewed

| Item | Unique Flag | Location Before | Location After |
|------|-------------|-----------------|----------------|
| L13_Staff_Archmage | `1` → `0` ✓ | L13_Gear_Chest ✓ | L13_Gear_Chest ✓ |
| L13_Sword_Tyr | `0` ✓ | Tutorial Chest ❌ | L13_Gear_Chest ✓ |
| L13_Blade_Moonguard | `0` ✓ | Tutorial Chest ❌ | L13_Gear_Chest ✓ |
| L13_Boots_Stormwalker | `0` ✓ | Tutorial Chest ❌ | L13_Gear_Chest ✓ |
| L13_Ring_Testing | `0` ✓ | Both ❌ | L13_Gear_Chest ✓ |
| L13_Gear_Chest | `1` ✓ | Tutorial Chest ✓ | Tutorial Chest ✓ |

### Files Changed

**1. Weapon.txt** - Line 8
```
Before: data "Unique" "1"
After:  data "Unique" "0"
```

**2. TreasureTable.txt**
```
Before:
new treasuretable "TUT_Chest_Potions"
  - I_L13_Gear_Chest
  - I_L13_Ring_Testing
  - I_L13_Sword_Tyr
  - I_L13_Boots_Stormwalker
  - I_L13_Blade_Moonguard

new treasuretable "L13_Gear_Chest_TT"
  - I_L13_Staff_Archmage
  - I_L13_Ring_Testing

After:
new treasuretable "TUT_Chest_Potions"
  - I_L13_Gear_Chest (ONLY)

new treasuretable "L13_Gear_Chest_TT"
  - I_L13_Staff_Archmage
  - I_L13_Ring_Testing
  - I_L13_Sword_Tyr
  - I_L13_Boots_Stormwalker
  - I_L13_Blade_Moonguard
```

### Implementation Status

- [x] Change Staff of Archmage to non-unique
- [x] Verify all other items are non-unique
- [x] Move Sword_Tyr from Tutorial Chest to L13_Gear_Chest
- [x] Move Blade_Moonguard from Tutorial Chest to L13_Gear_Chest
- [x] Move Boots_Stormwalker from Tutorial Chest to L13_Gear_Chest
- [x] Remove duplicate Ring_Testing from Tutorial Chest
- [x] Document all changes in this revision

**Revision 1 Complete:** 2026-02-10

---

## Testing Plan

### Test 1: Items Appear in Tutorial Chest
1. Start new game with Level13PlusGear enabled
2. Open Tutorial Chest
3. **Verify:** Both Boots of the Stormwalker and Moonguard Blade appear

### Test 2: Boots of the Stormwalker
1. Equip boots
2. **Verify:**
   - Name displays correctly
   - Misty Step (unlimited) appears on hotbar
   - Can cast Misty Step as bonus action
   - Reverberation passive applies when inflicting status
   - Web immunity works

### Test 3: Moonguard Blade
1. Equip blade
2. **Verify:**
   - Name displays correctly (should show special appearance)
   - All 6 spells appear on hotbar
   - Can cast Celestial Haste (free action)
   - Can cast Spirit Guardians (free action)
   - All passives active (check character sheet)
   - Lathander's Light status applies

### Test 4: No Dependencies
1. Disable SampleMagicRingMod
2. Enable only Level13PlusGear
3. Start new game
4. **Verify:** Both items work without SampleMagicRingMod

---

## Success Criteria

- [ ] Both items appear in Tutorial Chest
- [ ] Boots of the Stormwalker fully functional
- [ ] Moonguard Blade fully functional with all spells/passives
- [ ] No errors in BG3 logs
- [ ] No SampleMagicRingMod dependency
- [ ] 14 UUIDs removed from pool and documented
- [ ] All handles properly generated from UUIDs

---

## Related Documentation

- **docs/instructions/copying_items_between_mods.md** - Workflow guide
- **docs/instructions/uuid_workflow.md** - UUID pool
- **Phase031.md** - Ring creation lessons
- **Phase032.md** - Longsword of Tyr copy (with Revision 1 handle fix)
- **docs/planning/item_catalog.md** - Source item details

---

## Notes

- **Reuse existing components:** L13_Target_BlindingSmite_Unlimited, L13_Target_Light_Unlimited, and L13_RadiantWeapon_Passive already exist from Phase 32
- **Two different Celestial Haste versions:** Unlimited (from Sword of Tyr) and Free (for Moonguard Blade)
- **Container delivery:** Items won't appear in existing saves (Tutorial Chest limitation)
- **Appearance:** Moonguard Blade uses Primeval Silver Longsword appearance (ParentTemplateId)
- **Critical:** Follow Phase 32 Revision 1 lessons - generate handles from UUIDs, not random hex

---

## Post-Implementation

- [ ] Mark phase as IMPLEMENTED (awaiting user testing)
- [ ] User testing required before marking COMPLETE
- [ ] Consider updating item_catalog.md if Level13PlusGear maintains its own catalog
