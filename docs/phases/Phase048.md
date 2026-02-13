# Phase 048: Create Level 13 Plus Armor Chest

**Status:** COMPLETE
**Date:** 2026-02-12
**Completed:** 2026-02-12
**Type:** Implementation Phase

---

## Goals

1. **Create Level 13 Plus Armor Chest** - New container in Level13PlusGear mod
2. **Populate chest with all armor** - Configure chest to contain all Level13PlusGear armor pieces
3. **Deliver chest to Tutorial Chest** - Add via TreasureTable.txt
4. **Deliver chest to Traveler's Chest** - Add via OneTimeRewards.lsx
5. **Create chest summon spell** - Add to RingOfCreation mod
6. **Add spell to Ring of Creation** - Update Ring of Creation's boosts

---

## Strategy

**Problem:** Individual armor pieces fail to appear in chests (Phase 047 unresolved issue)

**Solution:** Deliver a chest container instead of individual armor pieces
- If chests can be delivered reliably, all armor becomes accessible via the chest
- Provides centralized armor storage
- Redundant delivery (Tutorial + Traveler's + Ring summon)

---

## Implementation Plan

### Task 1: Create Level 13 Plus Armor Chest (Level13PlusGear)

**Create new chest container:**

1. **RootTemplate** - `Level13PlusGear/Public/Level13PlusGear/RootTemplates/L13_Armor_Chest.lsf.lsx`
   - New UUID from pool (ed13 prefix)
   - Type: Container
   - ParentTemplateId: Research vanilla chest template UUID
   - DisplayName handle (ed13 prefix)
   - Description handle (ed13 prefix)

2. **Stats Entry** - `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Object.txt`
   - New entry: `L13_Armor_Chest`
   - Type: "Object"
   - RootTemplate: UUID from RootTemplate
   - Rarity: "Legendary" or "Unique"
   - Configure as container

3. **Localization** - `Level13PlusGear/Localization/English/Level13PlusGear.loca.xml`
   - DisplayName: "Level 13 Plus Armor Chest"
   - Description: Description of chest contents

**Chest Contents Configuration:**
- Need to research how to populate chest inventory
- Should contain all Level13PlusGear armor pieces:
  - L13_Armor_Tyr (Armor of Tyr)
  - L13_Armor_Moonguard (Moonguard Splint)
  - L13_Plate_Moonguard (Moonguard Plate)
  - L13_Armor_Dragonrider (Armor of the Dragonrider)
  - L13_Armor_Rogue (Armor of the Rogue)

### Task 2: Add Chest to Tutorial Chest (Level13PlusGear)

**Modify TreasureTable.txt:**

File: `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/TreasureTable.txt`

Add chest to existing `L13_Gear_Chest_TT` table:
```
object category "I_L13_Armor_Chest",1,0,0,0,0,0,0,0
```

### Task 3: Add Chest to Traveler's Chest (Level13PlusGear)

**Create/Modify OneTimeRewards.lsx:**

File: `Level13PlusGear/Public/Level13PlusGear/OneTimeRewards/OneTimeRewards.lsx`

Add chest entry:
```xml
<node id="OneTimeReward">
    <attribute id="Amount" type="uint32" value="1"/>
    <attribute id="ItemTemplateId" type="FixedString" value="[chest UUID]"/>
    <attribute id="UUID" type="guid" value="[new UUID from pool]"/>
</node>
```

### Task 4: Create Chest Summon Spell (RingOfCreation)

**Create summon spell:**

File: `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Spell_Target.txt`

New spell: `ROC_Summon_L13_Armor_Chest`
- SpellProperties: Summon chest at target location
- DisplayName/Description: Localization handles

**Localization:**

File: `RingOfCreation/Localization/English/RingOfCreation.loca.xml`
- Spell name: "Summon Level 13 Armor Chest"
- Spell description: Description of what the spell does

### Task 5: Add Spell to Ring of Creation (RingOfCreation)

**Modify Ring of Creation:**

File: `RingOfCreation/Public/RingOfCreation/Stats/Generated/Data/Armor.txt`

Update `ROC_Ring_Creation` entry:
- Add `UnlockSpell(ROC_Summon_L13_Armor_Chest)` to Boosts

---

## Research Needed

### 1. Vanilla Chest Template
- What ParentTemplateId should be used for a chest?
- Search VanillaBG3 for chest templates
- Common chest types: CONT_Chest, CONT_Crate, etc.

### 2. Chest Inventory Configuration
- How to populate a chest with specific items?
- Is this done in RootTemplate, Stats, or separate inventory file?
- Look at existing chest examples in VanillaBG3 or ExampleMods

### 3. Container Stats Entry
- What are the required fields for Object.txt container entry?
- Does it need special flags or attributes?

---

## UUIDs Needed

Estimated UUIDs from pool (uuid_workflow.md):
1. Chest RootTemplate MapKey
2. Chest DisplayName handle
3. Chest Description handle
4. OneTimeRewards entry UUID (Traveler's Chest)
5. Summon spell DisplayName handle
6. Summon spell Description handle

**Total: 6 UUIDs** (pool has 40+ available)

---

## Files to Create/Modify

### Level13PlusGear

**Create:**
- `Public/Level13PlusGear/RootTemplates/L13_Armor_Chest.lsf.lsx` - Chest RootTemplate

**Modify:**
- `Public/Level13PlusGear/Stats/Generated/Data/Object.txt` - Add chest stats entry
- `Public/Level13PlusGear/Stats/Generated/TreasureTable.txt` - Add chest to Tutorial Chest
- `Public/Level13PlusGear/OneTimeRewards/OneTimeRewards.lsx` - Add chest to Traveler's Chest (create if doesn't exist)
- `Localization/English/Level13PlusGear.loca.xml` - Add chest localization

### RingOfCreation

**Modify:**
- `Public/RingOfCreation/Stats/Generated/Data/Spell_Target.txt` - Add chest summon spell
- `Public/RingOfCreation/Stats/Generated/Data/Armor.txt` - Add spell to Ring of Creation
- `Localization/English/RingOfCreation.loca.xml` - Add summon spell localization

---

## Testing Plan

### Test 1: Chest in Tutorial Chest
1. Start new game
2. Reach Tutorial Chest (Nautiloid)
3. **Verify:** Level 13 Plus Armor Chest appears
4. **Verify:** Chest can be opened
5. **Verify:** All armor pieces are inside chest

### Test 2: Chest in Traveler's Chest
1. Continue to camp (after crash)
2. Open Traveler's Chest
3. **Verify:** Level 13 Plus Armor Chest appears
4. **Verify:** Chest contents are correct

### Test 3: Ring of Creation Summon
1. Equip Ring of Creation
2. Use "Summon Level 13 Armor Chest" spell
3. **Verify:** Chest appears at target location
4. **Verify:** Chest can be opened
5. **Verify:** All armor pieces are inside

### Test 4: Armor Functionality
1. Remove each armor piece from chest
2. Equip each armor
3. **Verify:** All powers and properties work correctly
4. **Verify:** Names and descriptions display correctly

---

## Success Criteria

- ✅ Level 13 Plus Armor Chest created in Level13PlusGear mod
- ✅ Chest contains all armor pieces
- ✅ Chest appears in Tutorial Chest
- ✅ Chest appears in Traveler's Chest
- ✅ Ring of Creation can summon chest
- ✅ All armor pieces accessible and functional
- ✅ All localization displays correctly

---

## Expected Benefits

1. **Solves Delivery Problem:** If chests deliver reliably, armor becomes accessible
2. **Redundant Delivery:** Three methods (Tutorial + Traveler's + Summon)
3. **Organized Storage:** All armor in one place
4. **Player Friendly:** Clear location for all armor pieces
5. **Workaround for Phase 047:** Avoids individual armor delivery issues

---

## Potential Issues

1. **Chest might not deliver either:** If chests have same issue as armor
2. **Inventory configuration complexity:** May be difficult to populate chest
3. **Chest inventory persistence:** Items might not stay in chest across saves
4. **Multiple chest instances:** Tutorial + Traveler's versions might create duplicates

---

## Fallback Plan

If chest delivery also fails:
1. Continue using Ring of Creation summons for individual armor
2. Research Script Extender or other advanced delivery methods
3. Consider creating multiple small chests for different armor categories

---

## Related Phases

- **Phase 047:** Research phase investigating armor delivery failure
- **Phase 044:** Initial identification of TreasureTable armor issues
- **Phase 030:** Container delivery limitation documentation

---

## Notes

- This is an experimental workaround approach
- Phase 047 concluded with unresolved issues about armor delivery
- Container-based delivery may circumvent individual armor restrictions
- If successful, this pattern could be used for other item categories
- DO NOT implement until user reviews this phase document

---

## Revision History

### Initial Creation (2026-02-12)
- Phase created as workaround for Phase 047 armor delivery issues
- Strategy: Deliver chest container instead of individual armor pieces
- Three delivery methods: Tutorial Chest, Traveler's Chest, Ring of Creation summon
- Status: PENDING - Awaiting user review before implementation

### Implementation Completed (2026-02-12)

**All tasks completed successfully:**

#### Level13PlusGear Files Created/Modified:

1. **RootTemplate Created:** `L13_Armor_Chest.lsf.lsx`
   - MapKey UUID: `ed133a09-b0f6-43a9-b47c-21100a829d57`
   - ParentTemplateId: `d91b10a4-b196-415d-963c-f8e90fc4eb47` (same as L13_Gear_Chest)
   - InventoryList references: `L13_Armor_Chest_TT`

2. **TreasureTable Created:** `L13_Armor_Chest_TT`
   - Contains 5 armor pieces:
     - I_L13_Armor_Tyr (Armor of Tyr)
     - I_L13_Armor_Rogue (Armor of the Rogue)
     - I_L13_Armor_Moonguard (Moonguard Splint)
     - I_L13_Plate_Moonguard (Moonguard Plate)
     - I_L13_Armor_Dragonrider (Armor of the Dragonrider)

3. **TreasureTable Updated:** Added `I_L13_Armor_Chest` to `TUT_Chest_Potions`
   - Delivers chest to Tutorial Chest

4. **Stats Entry Created:** `L13_Armor_Chest` in Object.txt
   - Type: "Object"
   - using: "OBJ_Chest"
   - Unique: "0"
   - RootTemplate: `ed133a09-b0f6-43a9-b47c-21100a829d57`

5. **Localization Added:** Level13PlusGear.loca.xml
   - DisplayName: "Level 13 Plus Armor Chest"
   - Description: Lists all armor contents

6. **OneTimeRewards Updated:** Added chest entry
   - ItemTemplateId: `ed133a09-b0f6-43a9-b47c-21100a829d57`
   - UUID: `ed13173a-0ea5-4512-a9ee-7bd3a3f92aec`
   - Delivers chest to Traveler's Chest

#### RingOfCreation Files Modified:

7. **Summon Spell Created:** `ROC_Summon_L13_Armor_Chest` in Spell_Target.txt
   - Summons chest UUID: `ed133a09-b0f6-43a9-b47c-21100a829d57`
   - Icon: Conjure Elemental
   - DisplayName handle: `hrocf771682gf152g407agbb1dg238f33a2f44e`
   - Description handle: `hroce995eeg71d4g40e0g9b6dg6162644c6f01`

8. **Ring of Creation Updated:** Added spell to boosts
   - Added: `UnlockSpell(ROC_Summon_L13_Armor_Chest)`

9. **Localization Added:** RingOfCreation.loca.xml
   - Spell name: "Summon Level 13 Armor Chest"
   - Spell description: Details about armor chest contents

**UUIDs Used (5 total):**
- `aac53a09-b0f6-43a9-b47c-21100a829d57` → `ed133a09-b0f6-43a9-b47c-21100a829d57` (Chest MapKey & DisplayName)
- `6f79941c-7297-4588-8253-3e7465c028af` → `hed1379941cg7297g4588g8253g3e7465c028af` (Chest Description)
- `7b1a173a-0ea5-4512-a9ee-7bd3a3f92aec` → `ed13173a-0ea5-4512-a9ee-7bd3a3f92aec` (OneTimeRewards)
- `fa771682-f152-407a-bb1d-238f33a2f44e` → `hrocf771682gf152g407agbb1dg238f33a2f44e` (Summon spell name)
- `79e995ee-71d4-40e0-9b6d-6162644c6f01` → `hroce995eeg71d4g40e0g9b6dg6162644c6f01` (Summon spell description)

All UUIDs deleted from uuid_workflow.md pool.

**Status:** IMPLEMENTED - Ready for testing

---

### Revision 1 - Test Results (2026-02-12)

**Test Status:** TESTED - Partial failure

**Test Result:**
- ❌ **L13_Armor_Chest contains only 1 out of 5 armor pieces**
- ✅ L13_Armor_Rogue (light armor) appears in chest
- ❌ L13_Armor_Tyr (half plate) does NOT appear
- ❌ L13_Armor_Moonguard (splint) does NOT appear
- ❌ L13_Plate_Moonguard (plate) does NOT appear
- ❌ L13_Armor_Dragonrider (half plate) does NOT appear

**Pattern Confirmed:**
- ✅ Light armor: Works in chest inventory
- ❌ Medium/heavy armor: Fails in chest inventory

**Critical Finding:**

The chest delivery workaround **does not solve the medium/heavy armor problem**. Even when armor is placed inside a chest's InventoryList (via TreasureTable), only light armor appears.

**Comparison to L13_Gear_Chest:**
The existing L13_Gear_Chest also has L13_Armor_Tyr and other armor in its L13_Gear_Chest_TT TreasureTable, and those items also don't appear. Only L13_Armor_Rogue appears from that chest as well.

**What This Proves:**

1. **Container inventory has same restrictions as direct chest delivery**
   - Chest InventoryList → TreasureTable still fails for medium/heavy armor
   - The problem is not the delivery method (TreasureTable vs OneTimeRewards)
   - The problem is not direct vs container delivery

2. **The issue is fundamental to medium/heavy armor in BG3**
   - Affects direct chest delivery (Phase 047)
   - Affects container inventory delivery (Phase 048)
   - Only light armor successfully populates

3. **Pattern is consistent across all tests:**
   - Tutorial Chest: Light armor works, medium/heavy fails
   - Traveler's Chest: Mixed results (Phase 047 unresolved)
   - Container inventory: Light armor works, medium/heavy fails
   - Ring of Creation summon: All armor types work

**Questions for Further Investigation:**

1. **Why does L13_Armor_Rogue work everywhere but other armor doesn't?**
   - Is it the light armor type specifically?
   - Is it something unique about L13_Armor_Rogue's configuration?
   - Compare L13_Armor_Rogue vs L13_Armor_Tyr in detail

2. **Why do Ring of Creation summons work for all armor?**
   - Direct spawn bypasses whatever restriction exists
   - Suggests the items themselves are valid

3. **Is this a BG3 engine limitation or configuration issue?**
   - Ed's feedback suggests Claude is making a mistake
   - But all configurations appear identical between working/non-working items

**Recommendation:**

At this point, the workaround approach has failed. The issue appears deeper than delivery methods. Next steps:
1. Perform detailed comparison of L13_Armor_Rogue (working) vs L13_Armor_Tyr (failing)
2. Check for subtle differences in Stats, RootTemplate, or other configuration
3. Consider that there may be a BG3 limitation we cannot work around
4. Continue using Ring of Creation summons as the reliable delivery method

---

## Analysis of Working Example Mod (2026-02-12)

**Example Mod Analyzed:** CL_InconstantMoon_ClericGear

**Container Examined:** `CL_Sel_TempBag` (Selunite Tempest Cleric Armor bag)

**Finding: This mod successfully delivers multiple medium armor pieces via container!**

#### Container Structure (CL_Sel_TempBag)

**RootTemplate:** `627937b2-7ca3-47c1-8371-c5e73ce5e2e5.lsf.lsx`
- Type: "item"
- ParentTemplateId: `baf0f19f-2128-4b5b-b43f-6ba5052af7ee`
- Stats: "CL_Sel_TempBag"
- InventoryList references: `CL_Sel_TempBag_TT`

**Stats Entry:** Object.txt
```
new entry "CL_Sel_TempBag"
type "Object"
using "_Container"
data "RootTemplate" "627937b2-7ca3-47c1-8371-c5e73ce5e2e5"
data "ValueOverride" "1"
data "Unique" "0"
data "MinLevel" "1"
```

**TreasureTable Contents:** `CL_Sel_TempBag_TT`
Contains 9 armor items including:
- `I_CL_TempSel_Shirt_HalfPlate` (medium armor)
- `I_CL_TempSel_Shirt_Plate` (called "plate" but actually medium)
- `I_CL_Sel_TempShirt_Plate_arm` (plate with arm)
- Plus 6 other armor variants

#### Critical Difference Found: "using" Clause

**Working Armor (CL mod):**
```
new entry "CL_TempSel_Shirt_HalfPlate"
type "Armor"
using "ARM_ScaleMail_Body"          ← NO _2 suffix!
data "RootTemplate" "a95fbecd-276c-4a4e-8a98-879e7623ae03"
data "ArmorClass" "12"
data "Rarity" "VeryRare"
data "Boosts" "Resistance(Lightning, Resistant)"
data "PassivesOnEquip" "MAG_ExoticMaterial_MediumArmor_Passive;..."
data "StatusOnEquip" "MAG_EXOTIC_MATERIAL_ARMOR_TECHNICAL"
data "Unique" "0"
```

**Working Armor (CL mod plate variant):**
```
new entry "CL_TempSel_Shirt_Plate"
type "Armor"
using "ARM_ScaleMail_Body"          ← NO _2 suffix, even for "plate"!
data "RootTemplate" "47a301c8-87c2-4370-8dc7-e9dd3ede8467"
...
data "Unique" "0"
```

**Non-Working Armor (L13 mod):**
```
new entry "L13_Armor_Tyr"
type "Armor"
using "ARM_HalfPlate_Body_2"        ← HAS _2 suffix!
data "RootTemplate" "ed13ac3a-47aa-4263-8147-34b583e18870"
...
data "Unique" "0"
```

```
new entry "L13_Armor_Moonguard"
type "Armor"
using "ARM_Splint_Body_2"           ← HAS _2 suffix!
data "RootTemplate" "ed1310a5-4fb8-4b8c-a043-6393a5e74ab5"
...
data "Unique" "0"
```

```
new entry "L13_Plate_Moonguard"
type "Armor"
using "ARM_Plate_Body_2"            ← HAS _2 suffix!
...
data "Unique" "0"
```

**Working Armor (L13 mod - light armor):**
```
new entry "L13_Armor_Rogue"
type "Armor"
using "ARM_StuddedLeather_Body_2"   ← HAS _2 suffix but WORKS!
data "RootTemplate" "ed136dac-370d-44d3-b96f-af7f76628b6e"
...
data "Unique" "0"
```

#### Pattern Analysis

**Armor that WORKS in containers:**
- `ARM_StuddedLeather_Body_2` (light armor with `_2`)
- `ARM_ScaleMail_Body` (medium armor without `_2`)

**Armor that FAILS in containers:**
- `ARM_HalfPlate_Body_2` (medium armor with `_2`)
- `ARM_Splint_Body_2` (heavy armor with `_2`)
- `ARM_Plate_Body_2` (heavy armor with `_2`)

#### Key Differences Between L13_Armor_Chest and CL_Sel_TempBag

| Attribute | L13_Armor_Chest | CL_Sel_TempBag |
|-----------|-----------------|----------------|
| **Stats using clause** | using "OBJ_Chest" | using "_Container" |
| **ParentTemplateId** | d91b10a4-b196-415d-963c-f8e90fc4eb47 | baf0f19f-2128-4b5b-b43f-6ba5052af7ee |
| **Armor using clauses** | ARM_HalfPlate_Body_2, ARM_Splint_Body_2, ARM_Plate_Body_2 | ARM_ScaleMail_Body (all armor) |
| **Result** | Only light armor appears | All armor appears ✅ |

#### Hypothesis

**The `_2` suffix in medium/heavy armor base templates may cause container delivery issues!**

Possible explanations:
1. BG3 engine treats `_2` variants differently for container population
2. `_2` variants may have additional restrictions or requirements
3. The CL mod deliberately uses `ARM_ScaleMail_Body` for all armor to avoid issues
4. Using `_Container` vs `OBJ_Chest` might also matter

#### Questions for Further Investigation

1. **What is the difference between `ARM_HalfPlate_Body_2` and `ARM_ScaleMail_Body`?**
   - Are these different armor types or just different base templates?
   - Why does the CL mod use `ARM_ScaleMail_Body` for both half plate and plate variants?

2. **Does the `_Container` vs `OBJ_Chest` matter?**
   - L13_Armor_Chest uses `OBJ_Chest`
   - CL_Sel_TempBag uses `_Container`

3. **Does the ParentTemplateId matter?**
   - Different parent templates between the two containers

4. **Why does L13_Armor_Rogue work with `_2` suffix?**
   - Light armor with `_2` works, but medium/heavy with `_2` fails
   - What's special about light armor?

#### Testing Plan - Multiple Revisions

To isolate which change fixes the issue, we'll test each hypothesis separately:

**Revision 2:** Change armor "using" clauses (remove `_2` suffix)
- Change L13_Armor_Tyr from `ARM_HalfPlate_Body_2` → `ARM_ScaleMail_Body`
- Change L13_Armor_Moonguard from `ARM_Splint_Body_2` → `ARM_ScaleMail_Body`
- Change L13_Plate_Moonguard from `ARM_Plate_Body_2` → `ARM_ScaleMail_Body`
- Change L13_Armor_Dragonrider from `ARM_HalfPlate_Body_2` → `ARM_ScaleMail_Body`
- Test: Does armor appear in L13_Armor_Chest?

**Revision 3:** Change container Stats "using" clause
- Change L13_Armor_Chest from `OBJ_Chest` → `_Container`
- Test: Does armor appear in L13_Armor_Chest?

**Revision 4:** Change container ParentTemplateId
- Change L13_Armor_Chest ParentTemplateId from `d91b10a4-b196-415d-963c-f8e90fc4eb47` → `baf0f19f-2128-4b5b-b43f-6ba5052af7ee` (match CL mod)
- Test: Does armor appear in L13_Armor_Chest?

**Testing Checklist:**

- [x] Revision 2: Change armor using clauses - ✅ SUCCESS
  - File modified: `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Armor.txt`
  - Changes: 4 armor entries (Tyr, Moonguard, Plate_Moonguard, Dragonrider)
  - Build: 2-3 (Version64: 36028900098179073 → 36028900098179074)
  - Test result: All armor appears in container!

- [ ] Revision 3: Change container using clause - PENDING
  - File to modify: `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Object.txt`
  - Changes: 1 line (L13_Armor_Chest using clause)
  - Test result: ?

- [ ] Revision 4: Change container ParentTemplateId - PENDING
  - File to modify: `Level13PlusGear/Public/Level13PlusGear/RootTemplates/L13_Armor_Chest.lsf.lsx`
  - Changes: 1 attribute (ParentTemplateId)
  - Test result: ?

**Revert Instructions:**

Each revision will document:
1. **Original values** before changes
2. **New values** after changes
3. **Files modified** with line numbers
4. **Test results** after changes

If a change doesn't work, revert by restoring original values from the revision documentation.

**Note:** Only implement revisions when user approves and requests implementation. Do not proceed without authorization.

---

### Revision 2 - Change Armor Using Clauses (2026-02-12)

**Status:** IMPLEMENTED - Awaiting testing

**Hypothesis:** The `_2` suffix in armor base templates causes container delivery issues. Changing to `ARM_ScaleMail_Body` (no suffix) should fix the problem.

**Files Modified:**

1. **Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Armor.txt**

**Changes Made:**

| Armor Entry | Original "using" | New "using" | Line |
|-------------|------------------|-------------|------|
| L13_Armor_Tyr | `ARM_HalfPlate_Body_2` | `ARM_ScaleMail_Body` | 33 |
| L13_Armor_Moonguard | `ARM_Splint_Body_2` | `ARM_ScaleMail_Body` | 54 |
| L13_Plate_Moonguard | `ARM_Plate_Body_2` | `ARM_ScaleMail_Body` | 64 |
| L13_Armor_Dragonrider | `ARM_HalfPlate_Body_Githyanki` | `ARM_ScaleMail_Body` | 183 |

2. **Level13PlusGear/Mods/Level13PlusGear/meta.lsx**

**Version Update:**
- Original Version64: `36028900098179072` (Build 1)
- New Version64: `36028900098179073` (Build 2)

**Revert Instructions:**

To revert Revision 2, restore the following values:

```
L13_Armor_Tyr: using "ARM_HalfPlate_Body_2"
L13_Armor_Moonguard: using "ARM_Splint_Body_2"
L13_Plate_Moonguard: using "ARM_Plate_Body_2"
L13_Armor_Dragonrider: using "ARM_HalfPlate_Body_Githyanki"
Version64: "36028900098179072"
```

**Test Instructions:**

1. Start new game or load save
2. Check L13_Armor_Chest in Tutorial Chest
3. Verify which armor pieces appear:
   - Expected: All 5 armor pieces (Tyr, Moonguard, Plate_Moonguard, Dragonrider, Rogue)
   - Previous result: Only Rogue appeared

**Test Result:** ✅ SUCCESS

All 5 armor pieces now appear in L13_Armor_Chest:
- ✅ L13_Armor_Tyr (Armor of Tyr)
- ✅ L13_Armor_Rogue (Armor of the Rogue)
- ✅ L13_Armor_Moonguard (Moonguard Splint)
- ✅ L13_Plate_Moonguard (Moonguard Plate)
- ✅ L13_Armor_Dragonrider (Armor of the Dragonrider)

**Root Cause Confirmed:** The `_2` suffix in medium/heavy armor base templates (`ARM_HalfPlate_Body_2`, `ARM_Splint_Body_2`, `ARM_Plate_Body_2`) prevents armor from appearing in container inventories.

**Solution:** Use `ARM_ScaleMail_Body` for all medium/heavy armor that needs to be delivered via containers.

**Note:** User incremented to Build 3 (Version64: 36028900098179074) during testing.

---

### Revision 3 - Cleanup: Remove Armor from L13_Gear_Chest (2026-02-12)

**Status:** IMPLEMENTED - Ready for testing

**Goal:** Remove the 5 armor pieces from L13_Gear_Chest since they now appear in the dedicated L13_Armor_Chest. Armor should only be in one location.

**Issue:** Currently, the 5 armor pieces appear in both:
- ✅ L13_Armor_Chest (dedicated armor chest) - KEEP
- ❌ L13_Gear_Chest (general gear chest) - REMOVE

**Armor Removed from L13_Gear_Chest:**
1. L13_Armor_Tyr (Armor of Tyr)
2. L13_Armor_Rogue (Armor of the Rogue)
3. L13_Armor_Moonguard (Moonguard Splint)
4. L13_Plate_Moonguard (Moonguard Plate)
5. L13_Armor_Dragonrider (Armor of the Dragonrider)

**Files Modified:**

1. **Level13PlusGear/Public/Level13PlusGear/Stats/Generated/TreasureTable.txt**
   - Table: `L13_Gear_Chest_TT`
   - Removed 5 armor entries:
     - Lines 33-34: Removed I_L13_Armor_Tyr subtable
     - Lines 35-36: Removed I_L13_Armor_Rogue subtable
     - Lines 37-38: Removed I_L13_Armor_Moonguard subtable
     - Lines 65-66: Removed I_L13_Plate_Moonguard subtable
     - Lines 67-68: Removed I_L13_Armor_Dragonrider subtable
   - Note: Armor remains in L13_Armor_Chest_TT (lines 74-82)

2. **Level13PlusGear/Mods/Level13PlusGear/meta.lsx**
   - Updated Version64 from Build 3 to Build 4
   - Previous: `36028900098179074`
   - Current: `36028900098179075`

**Expected Result:**
- L13_Gear_Chest: Contains weapons, rings, helmets, gloves, cloaks, shields, circlets, boots - NO body armor
- L13_Armor_Chest: Contains all 5 body armor pieces exclusively

**Test Instructions:**
1. Start new game
2. Check Tutorial Chest
3. Verify L13_Gear_Chest no longer contains the 5 body armor pieces
4. Verify L13_Armor_Chest still contains all 5 body armor pieces
5. Verify other items (helmets, gloves, etc.) remain in L13_Gear_Chest

**Revert Instructions:**
To revert Revision 3, restore the removed lines in TreasureTable.txt at their original positions in L13_Gear_Chest_TT table and change Version64 back to `36028900098179074`.
