# Phase 26: Fix Armor of Orpheus

## Status: ABANDONED

### Diagnostic Test 1: FAILED
Tested using Armor of Tyr's ParentTemplateId (`42e6357a-4c05-4eda-9415-6b6b4c7d44c5` / MAG_EndGame_HalfPlate).
**Result:** Armor of Orpheus still did not appear.

### Diagnostic Test 2: FAILED
Tested using Elven Chain as the base armor (`391bccb7-8199-41e3-9aa3-261def2ebf26` / MAG_PHB_ElvenChain_Armor).
**Result:** Armor of Orpheus still did not appear.

---

## ABANDONED: Armor of Orpheus

The Armor of Orpheus has been abandoned due to persistent issues with the item not appearing in the traveler's chest. The root cause remains unknown.

---

## ABANDONED: Armor of Gith

Created a fresh armor item from scratch but it also failed to appear in the traveler's chest.

**Result:** FAILED - Item did not appear.

### Item Details (for reference)

| Attribute | Value |
|-----------|-------|
| Name | Armor of Gith |
| Base Armor | MAG_PHB_ElvenChain_Armor (`391bccb7-8199-41e3-9aa3-261def2ebf26`) |
| AC Bonus | +5 |

---

## Conclusion

Both Armor of Orpheus and Armor of Gith failed to appear in the traveler's chest despite multiple attempts with different parent templates. The root cause remains unknown. Phase 26 is abandoned.

## Goals

1. Fix Armor of Orpheus not appearing in Traveler's Chest
2. Compare implementation with working Armor of Tyr to identify differences

---

## Analysis: Armor of Tyr vs Armor of Orpheus

### merged.lsx Comparison

| Attribute | Armor of Tyr | Armor of Orpheus |
|-----------|--------------|------------------|
| DisplayName handle | `hc3d4e5f6ag7b8cg9d0eg1f2ag3b4c5d6e7f8` | `h25a1b2c3g4d5eg6f7ag8b9cg0d1e2f3a4b5c6` |
| Description handle | `hd4e5f6a7bg8c9dg0e1fg2a3bg4c5d6e7f8a9` | `h25b2c3d4g5e6fg7a8bg9c0dg1e2f3a4b5c6d7` |
| MapKey | `c3d4e5f6-a7b8-4c9d-0e1f-2a3b4c5d6e7f` | `444e6150-09a3-49c3-9a95-6940a5713852` |
| Name | `SMR_Armor_Tyr` | `SMR_Armor_Orpheus` |
| ParentTemplateId | `42e6357a-4c05-4eda-9415-6b6b4c7d44c5` | `38c63f49-3c50-46d0-90d3-68b247542c36` |
| Stats | `SMR_Armor_Tyr` | `SMR_Armor_Orpheus` |

**Potential Issue:** ParentTemplateId differs:
- Armor of Tyr uses `42e6357a-4c05-4eda-9415-6b6b4c7d44c5` (MAG_EndGame_HalfPlate - confirmed in gustav)
- Armor of Orpheus uses `38c63f49-3c50-46d0-90d3-68b247542c36` (ARM_HalfPlate_Githyanki - needs verification)

### Armor.txt Comparison

| Attribute | Armor of Tyr | Armor of Orpheus |
|-----------|--------------|------------------|
| using | `ARM_HalfPlate_Body_2` | `ARM_HalfPlate_Body_2` |
| RootTemplate | `c3d4e5f6-a7b8-4c9d-0e1f-2a3b4c5d6e7f` | `444e6150-09a3-49c3-9a95-6940a5713852` |
| Rarity | `Legendary` | `Legendary` |
| Boosts | Same spells | Same spells |
| PassivesOnEquip | `MAG_ExoticMaterial_MediumArmor_Passive` | `MAG_ExoticMaterial_MediumArmor_Passive` |
| StatusOnEquip | `MAG_EXOTIC_MATERIAL_ARMOR_TECHNICAL` | `MAG_EXOTIC_MATERIAL_ARMOR_TECHNICAL` |
| Ability Modifier Cap | `""` | `""` |
| Unique | `1` | `1` |

**No differences found in Armor.txt structure.**

### OneTimeRewards.lsx Comparison

| Attribute | Armor of Tyr | Armor of Orpheus |
|-----------|--------------|------------------|
| Amount | `1` | `1` |
| ItemTemplateId | `c3d4e5f6-a7b8-4c9d-0e1f-2a3b4c5d6e7f` | `444e6150-09a3-49c3-9a95-6940a5713852` |
| UUID | `d4e5f6a7-b8c9-4d0e-1f2a-3b4c5d6e7f8a` | `25c3d4e5-f6a7-4b8c-9d0e-1f2a3b4c5d6e` |

**ItemTemplateId matches MapKey correctly for both.**

### Localization Comparison

Both have entries in SampleMagicRingMod.loca.xml:
- Armor of Tyr: DisplayName and Description present
- Armor of Orpheus: DisplayName and Description present

---

## Investigation Findings

### ParentTemplateId is VALID

The Githyanki Half Plate template has been confirmed in base game files:
```
MapKey: 38c63f49-3c50-46d0-90d3-68b247542c36
Name: ARM_HalfPlate_Githyanki
ParentTemplateId: 34a71679-0ab5-4fd4-bba8-d6ad341ee490 (ARM_HalfPlate)
```

**This rules out ParentTemplateId as the cause of the issue.**

---

## Remaining Potential Causes

1. **Module Loading Order**: ARM_HalfPlate_Githyanki may be in Shared module while our mod loads differently
2. **Missing Required Attributes**: Some base game armors have additional attributes (e.g., Tags, Icon) that may be required
3. **Stats Entry Issue**: Something in Armor.txt may be malformed
4. **Cache Issue**: Game may need cache cleared after adding new items

---

## Implementation Plan

### Step 1: Compare with Base Game Template Structure
Look at what attributes ARM_HalfPlate_Githyanki has in the base game and ensure our template matches the required structure.

### Step 2: Test with Armor of Tyr's ParentTemplateId
As a diagnostic step, temporarily change Armor of Orpheus to use the same ParentTemplateId as Armor of Tyr (`42e6357a-4c05-4eda-9415-6b6b4c7d44c5`). If this works, the issue is with how we're referencing the Githyanki template.

### Step 3: Add Missing Attributes
If Step 2 works, investigate what additional attributes might be needed to use ARM_HalfPlate_Githyanki as a parent.

---

## Files to Modify

| File | Change |
|------|--------|
| `merged.lsx` | Update ParentTemplateId and/or add VisualTemplate for Armor of Orpheus |

---

## Test Plan

1. Load the game with the mod active
2. Open traveler's chest
3. Verify Armor of Orpheus appears in the chest
4. Equip the armor and verify:
   - Correct Githyanki Half Plate appearance
   - +2 Saving Throw bonus
   - Celestial Haste (unlimited, bonus action)
   - Misty Step (unlimited)
   - Spirit Guardians (Radiant/Necrotic options)
   - No Stealth disadvantage (Exotic Material)
