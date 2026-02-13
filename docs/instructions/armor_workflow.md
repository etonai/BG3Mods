# Armor Creation Workflow for BG3 Modding

## Overview
This document provides guidelines and lessons learned for creating custom armor in BG3 mods, with special attention to container delivery compatibility.

---

## Critical Finding: Armor Base Templates and Container Delivery

### The Problem
During Phase 047-048 development, we discovered that certain armor base templates prevent armor from appearing in container inventories (Tutorial Chest, Traveler's Chest, custom containers).

### What We Know

**❌ FAILED Container Delivery:**
- `ARM_HalfPlate_Body_2` - Did NOT appear in containers
- `ARM_Splint_Body_2` - Did NOT appear in containers
- `ARM_Plate_Body_2` - Did NOT appear in containers

**✅ SUCCEEDED Container Delivery:**
- `ARM_ScaleMail_Body` - Successfully appeared in containers
- `ARM_StuddedLeather_Body_2` - Light armor exception, works with `_2` suffix

**⚠️ UNTESTED:**
Other base template variants may work but have not been tested. The pattern suggests that `_2` suffix variants for medium/heavy armor are problematic, but we cannot definitively state that ALL `_2` variants fail or that ARM_ScaleMail_Body is the ONLY solution.

### Symptoms
When armor fails container delivery, you'll see:
- Armor entry exists in Stats files ✓
- RootTemplate exists ✓
- TreasureTable references the armor ✓
- **But armor does NOT appear in the container in-game** ✗

### Solution That Worked
**Phase 048 Revision 2:** Changed all medium/heavy armor from `_2` variants to `ARM_ScaleMail_Body` and all armor appeared successfully in containers.

### Evidence Source
**Working Example:** The `CL_InconstantMoon_ClericGear` mod successfully delivers multiple medium armor pieces in containers using `ARM_ScaleMail_Body`.

---

## Armor Creation Checklist

### 1. Planning Phase
- [ ] Determine armor type (Light/Medium/Heavy)
- [ ] Choose base template (research vanilla examples if unsure)
- [ ] Plan armor class, rarity, and unique status
- [ ] Design boosts and passives
- [ ] Verify delivery method (container vs other)

### 2. Base Template Selection

**For Container Delivery (TreasureTable/OneTimeRewards):**
- [ ] **Avoid `_2` suffix variants** for medium/heavy armor (known failures: ARM_HalfPlate_Body_2, ARM_Splint_Body_2, ARM_Plate_Body_2)
- [ ] **Use ARM_ScaleMail_Body** (confirmed working for all armor weights)
- [ ] OR research alternative base templates from working example mods

**For Direct/Script Delivery:**
- [ ] `_2` variants may be acceptable (not tested for non-container delivery)

### 3. Stats Entry Creation

Required fields in Armor.txt:
```
new entry "L13_Armor_Example"
type "Armor"
using "ARM_ScaleMail_Body"              ← Base template
data "RootTemplate" "uuid-here"
data "ArmorClass" "15"                   ← AC value
data "Rarity" "Legendary"
data "Weight" "20"
data "MinLevel" "13"
data "Boosts" "..."                      ← Optional
data "PassivesOnEquip" "..."             ← Optional
data "Unique" "1"                        ← 0 or 1
```

### 4. RootTemplate Creation
- [ ] Create in `Public/[ModName]/RootTemplates/`
- [ ] MapKey matches RootTemplate UUID in Stats
- [ ] ParentTemplateId references appropriate vanilla armor
- [ ] Set Type="item"
- [ ] Add localization references (Name, Description)

### 5. Localization
- [ ] DisplayName handle (MapKey with 'g' separators + 'h' prefix)
- [ ] Description handle (different UUID with 'g' separators + 'h' prefix)
- [ ] Add to English/[ModName].loca.xml

### 6. Container Delivery Setup

**For TreasureTable (Tutorial Chest):**
```
new treasuretable "TUT_Chest_Potions"
new subtable "1,1"
object category "I_L13_Armor_Example",1,0,0,0,0,0,0,0
```

**For OneTimeRewards (Traveler's Chest):**
```xml
<node id="OneTimeReward">
    <attribute id="Amount" type="uint32" value="1"/>
    <attribute id="ItemTemplateId" type="FixedString" value="uuid-here"/>
    <attribute id="UUID" type="guid" value="unique-uuid-here"/>
</node>
```

### 7. Pre-Testing Validation
- [ ] Verify base template choice (avoid known `_2` failures)
- [ ] Confirm all UUIDs are unique and properly formatted
- [ ] Check localization handles match RootTemplate MapKey
- [ ] Increment Version64 in meta.lsx for new build
- [ ] Verify TreasureTable or OneTimeRewards syntax

### 8. Testing
- [ ] Start new game (containers lock loot after first open)
- [ ] Check Tutorial Chest (Nautiloid) if using TreasureTable
- [ ] Check Traveler's Chest (camp) if using OneTimeRewards
- [ ] Verify armor appearance, stats, and functionality
- [ ] Document results in phase document

---

## Common Pitfalls

### 1. Container Already Opened
**Problem:** Adding items to a container that's already been opened in a save file won't make them appear retroactively.

**Solution:** Always test with a new game when adding new items to containers.

### 2. Using `_2` Suffix Base Templates
**Problem:** Medium/heavy armor using ARM_HalfPlate_Body_2, ARM_Splint_Body_2, or ARM_Plate_Body_2 don't appear in containers.

**Solution:** Use ARM_ScaleMail_Body or research alternative base templates from working mods.

### 3. Wrong Stats Entry Type
**Problem:** Using `type "Object"` instead of `type "Armor"` prevents proper armor functionality.

**Solution:** Always use `type "Armor"` for armor pieces.

### 4. Mismatched UUIDs
**Problem:** RootTemplate UUID in Stats doesn't match MapKey in RootTemplate file.

**Solution:** Double-check UUID values match exactly between Stats and RootTemplate.

### 5. Incorrect Localization Handles
**Problem:** DisplayName handle in RootTemplate doesn't match localization content contentuid.

**Solution:** Convert MapKey UUID to 'g' separator format: `ed133a09-b0f6-43a9-b47c-21100a829d57` → `hed133a09gb0f6g43a9gb47cg21100a829d57`

---

## Reference Examples

### Working Example Mods
| Mod | File | Notes |
|-----|------|-------|
| CL_InconstantMoon_ClericGear | Armor.txt | Uses ARM_ScaleMail_Body for container-delivered medium armor |
| SampleMagicRingMod | Armor.txt | Light armor examples |

### Vanilla Reference Files
| File | Location | Purpose |
|------|----------|---------|
| Armor.txt | VanillaBG3/gustav/Public/Gustav/Stats/Generated/Data/ | Base template options |
| Shared.txt | VanillaBG3/shared/Public/Shared/Stats/Generated/Data/ | Common base templates |

---

## Quick Reference: Base Template Research

When choosing a base template:

1. **Check working example mods** in ExampleMods/ directory
2. **Search vanilla files** for similar armor types
3. **Avoid known failures:** ARM_HalfPlate_Body_2, ARM_Splint_Body_2, ARM_Plate_Body_2 (for containers)
4. **Test ARM_ScaleMail_Body first** - confirmed working for all weights
5. **Document your findings** - add to this file if you discover new working/failing templates

---

## Related Documentation

- **BG3_Modding_Lessons_Learned.md** - Detailed technical explanation of the `_2` suffix problem
- **Phase048.md** - Full investigation and testing documentation
- **uuid_workflow.md** - UUID management and naming conventions
- **copying_items_between_mods.md** - Process for copying armor between mods

---

## Version History

**2026-02-12:** Initial creation based on Phase 047-048 findings regarding armor base templates and container delivery.
