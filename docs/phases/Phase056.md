# Phase 056: Add Level 21 Gear Chest

**Status:** COMPLETE
**Date:** 2026-02-17

---

## Goals

1. **Create L21_Gear_Chest** - A dedicated chest for Level 21 Gear items, mirroring the Level13PlusGear chest pattern
2. **Deliver chest via Tutorial Chest** - The L21_Gear_Chest appears inside TUT_Chest_Potions instead of the staff directly
3. **Add localization** - Add chest name and description to Level21Gear.loca.xml

**Note:** OneTimeRewards (Traveler's Chest) delivery was NOT used. The chest will later be added to the Ring of Creation for mid-playthrough access.

---

## Summary of Changes

| Component | Action | Description |
|-----------|--------|-------------|
| **L21_Gear_Chest RootTemplate** | Create | New chest template defining appearance and inventory |
| **Object.txt** | Create | Stats definition for the chest |
| **TreasureTable.txt** | Edit | Replace staff entry in TUT_Chest_Potions with L21_Gear_Chest; add L21_Gear_Chest_TT containing the staff |
| **Level21Gear.loca.xml** | Edit | Add chest DisplayName and Description |

**Result:** The L21_Gear_Chest appears inside the Tutorial Chest. The chest itself contains the Staff of Gimeitaro. The staff is no longer placed directly in the Tutorial Chest.

---

## Current State

### Staff Delivery

**File:** `Level21Gear/Public/Level21Gear/Stats/Generated/TreasureTable.txt`

```
new treasuretable "TUT_Chest_Potions"
CanMerge 1
new subtable "1,1"
object category "I_L21_Staff_Gimeitaro",1,0,0,0,0,0,0,0
```

**Current Behavior:**
- Staff of Gimeitaro is injected into the Tutorial Chest (TUT_Chest_Potions) at the Nautiloid crash site
- Once the Tutorial Chest is opened in a save, loot is locked
- No dedicated Level 21 Gear chest exists

---

## Target State

### New L21_Gear_Chest

**Appearance:** Uses the same rich vanilla chest visual as Level13PlusGear:
- **Icon:** `Item_CONT_GEN_Chest_Rich_A`
- **Visual Template:** `221ddde0-7e34-43a7-bc84-8ae3dfd09bb9`
- **Physics Template:** `92211506-18c3-18c2-6791-dd8c48fb94af`
- **Parent Template:** `d91b10a4-b196-415d-963c-f8e90fc4eb47` (vanilla chest base)

**Contents:** Staff of Gimeitaro

**Delivery:** OneTimeRewards (appears once per playthrough)

---

## Implementation Plan

### Task 1: Create RootTemplate for L21_Gear_Chest

**Description:** Create the chest's RootTemplate file, defining its appearance and inventory

**Steps:**
1. Read `Level13PlusGear/Public/Level13PlusGear/RootTemplates/L13_Gear_Chest.lsf.lsx` for reference
2. Allocate a new UUID from uuid_workflow.md pool (ed21 prefix) for the chest MapKey
3. Create `Level21Gear/Public/Level21Gear/RootTemplates/L21_Gear_Chest.lsf.lsx`
4. Set `InventoryList` to reference `L21_Gear_Chest_TT`
5. Set DisplayName and Description handles (allocated from UUID pool)

**Files to create:**
- `Level21Gear/Public/Level21Gear/RootTemplates/L21_Gear_Chest.lsf.lsx`

---

### Task 2: Create Object.txt Stats Entry

**Description:** Define the stats for the L21_Gear_Chest object

**Steps:**
1. Check if `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Object.txt` exists
2. If not, create it; if so, append to it
3. Add stats entry for `L21_Gear_Chest` using `OBJ_Chest` as base

**Target content:**
```
new entry "L21_Gear_Chest"
type "Object"
using "OBJ_Chest"
data "RootTemplate" "[NEW-CHEST-UUID]"
data "ValueOverride" "1000"
data "Rarity" "Legendary"
data "Unique" "1"
data "MinLevel" "1"
```

**Files to create/edit:**
- `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Object.txt` - Create with chest stats

---

### Task 3: Update TreasureTable.txt

**Description:** Replace the staff in TUT_Chest_Potions with the new chest, and add L21_Gear_Chest_TT containing the staff

**Steps:**
1. Open `Level21Gear/Public/Level21Gear/Stats/Generated/TreasureTable.txt`
2. In the `TUT_Chest_Potions` entry, replace `I_L21_Staff_Gimeitaro` with `I_L21_Gear_Chest`
3. Add a new `L21_Gear_Chest_TT` table containing `I_L21_Staff_Gimeitaro`

**Target content:**
```
new treasuretable "TUT_Chest_Potions"
 CanMerge 1
new subtable "1,1"
object category "I_L21_Gear_Chest",1,0,0,0,0,0,0,0

new treasuretable "L21_Gear_Chest_TT"
 CanMerge 1
new subtable "1,1"
object category "I_L21_Staff_Gimeitaro",1,0,0,0,0,0,0,0
```

**Files to edit:**
- `Level21Gear/Public/Level21Gear/Stats/Generated/TreasureTable.txt` - Update TUT_Chest_Potions to deliver chest; add L21_Gear_Chest_TT

---

### Task 4: Create OneTimeRewards.lsx

**Description:** Configure the chest to be delivered once per playthrough via OneTimeRewards

**Steps:**
1. Read `Level13PlusGear/Public/Level13PlusGear/OneTimeRewards/OneTimeRewards.lsx` for reference
2. Create `Level21Gear/Public/Level21Gear/OneTimeRewards/` directory
3. Create `Level21Gear/Public/Level21Gear/OneTimeRewards/OneTimeRewards.lsx`
4. Allocate a second UUID from the pool for the OneTimeReward UUID (different from the RootTemplate UUID)
5. Set `ItemTemplateId` to the chest's RootTemplate UUID

**Target content structure:**
```xml
<?xml version="1.0" encoding="utf-8"?>
<save>
    <version major="4" minor="0" revision="6" build="5" lslib_meta="v1,bswap_guids" />
    <region id="OneTimeRewards">
        <node id="root">
            <children>
                <node id="OneTimeReward">
                    <attribute id="Amount" type="uint32" value="1"/>
                    <attribute id="ItemTemplateId" type="FixedString" value="[CHEST-ROOTTEMPLATE-UUID]"/>
                    <attribute id="UUID" type="guid" value="[ONETIMEREWARD-UUID]"/>
                </node>
            </children>
        </node>
    </region>
</save>
```

**Files to create:**
- `Level21Gear/Public/Level21Gear/OneTimeRewards/OneTimeRewards.lsx`

---

### Task 5: Add Localization Entries

**Description:** Add DisplayName and Description for the chest to Level21Gear.loca.xml

**Steps:**
1. Allocate 2 UUIDs from the pool for DisplayName and Description handles
2. Open `Level21Gear/Localization/English/Level21Gear.loca.xml`
3. Add DisplayName and Description entries for L21_Gear_Chest

**Target localization:**
```xml
<!-- L21_Gear_Chest -->
<content contentuid="[DISPLAYNAME-HANDLE]" version="1">Level 21 Gear Chest</content>
<content contentuid="[DESCRIPTION-HANDLE]" version="1">A chest containing legendary gear for level 21+ characters. Contains the Staff of Gimeitaro.</content>
```

**Files to edit:**
- `Level21Gear/Localization/English/Level21Gear.loca.xml`

---

### Task 6: Update uuid_workflow.md and Documentation

**Description:** Remove used UUIDs from the pool and update docs

**Steps:**
1. Remove 4 used UUIDs from `docs/instructions/uuid_workflow.md`
2. Add note about Phase 056 UUID usage
3. Update `docs/level21gear/item_catalog.md` to note new delivery method

**Files to edit:**
- `docs/instructions/uuid_workflow.md` - Remove 4 used UUIDs
- `docs/level21gear/item_catalog.md` - Update delivery method to L21_Gear_Chest

---

## Detailed Implementation

### Step 1: Create L21_Gear_Chest RootTemplate

**File:** `Level21Gear/Public/Level21Gear/RootTemplates/L21_Gear_Chest.lsf.lsx`

**Content (based on L13_Gear_Chest pattern):**
```xml
<?xml version="1.0" encoding="utf-8"?>
<save>
    <version major="4" minor="0" revision="6" build="5" lslib_meta="v1,bswap_guids" />
    <region id="Templates">
        <node id="Templates">
            <children>
                <node id="GameObjects">
                    <attribute id="DisplayName" type="TranslatedString" handle="[DISPLAYNAME-HANDLE]" version="1" />
                    <attribute id="Description" type="TranslatedString" handle="[DESCRIPTION-HANDLE]" version="1" />
                    <attribute id="Icon" type="FixedString" value="Item_CONT_GEN_Chest_Rich_A" />
                    <attribute id="LevelName" type="FixedString" value="" />
                    <attribute id="MapKey" type="FixedString" value="[CHEST-UUID]" />
                    <attribute id="Name" type="LSString" value="L21_Gear_Chest" />
                    <attribute id="ParentTemplateId" type="FixedString" value="d91b10a4-b196-415d-963c-f8e90fc4eb47" />
                    <attribute id="PhysicsTemplate" type="FixedString" value="92211506-18c3-18c2-6791-dd8c48fb94af" />
                    <attribute id="Stats" type="FixedString" value="L21_Gear_Chest" />
                    <attribute id="Type" type="FixedString" value="item" />
                    <attribute id="VisualTemplate" type="FixedString" value="221ddde0-7e34-43a7-bc84-8ae3dfd09bb9" />
                    <attribute id="_OriginalFileVersion_" type="int64" value="144115188075855912" />
                    <children>
                        <node id="GameMaster" />
                        <node id="InventoryList">
                            <children>
                                <node id="InventoryItem">
                                    <attribute id="Object" type="FixedString" value="L21_Gear_Chest_TT" />
                                </node>
                            </children>
                        </node>
                    </children>
                </node>
            </children>
        </node>
    </region>
</save>
```

**Purpose:** Defines the visual chest object that appears in the player's inventory via OneTimeRewards, containing the L21_Gear_Chest_TT treasure table.

---

### Step 2: Create Object.txt

**File:** `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Object.txt`

**Content:**
```
new entry "L21_Gear_Chest"
type "Object"
using "OBJ_Chest"
data "RootTemplate" "[CHEST-UUID]"
data "ValueOverride" "1000"
data "Rarity" "Legendary"
data "Unique" "1"
data "MinLevel" "1"
```

**Purpose:** Registers the chest as a stats object so BG3 can reference it by name.

---

### Step 3: Update TreasureTable.txt

**File:** `Level21Gear/Public/Level21Gear/Stats/Generated/TreasureTable.txt`

**Current content:**
```
new treasuretable "TUT_Chest_Potions"
CanMerge 1
new subtable "1,1"
object category "I_L21_Staff_Gimeitaro",1,0,0,0,0,0,0,0
```

**New content:**
```
new treasuretable "TUT_Chest_Potions"
 CanMerge 1
new subtable "1,1"
object category "I_L21_Gear_Chest",1,0,0,0,0,0,0,0

new treasuretable "L21_Gear_Chest_TT"
 CanMerge 1
new subtable "1,1"
object category "I_L21_Staff_Gimeitaro",1,0,0,0,0,0,0,0
```

**Purpose:** The Tutorial Chest now delivers the L21_Gear_Chest container (instead of the staff directly). The L21_Gear_Chest_TT table defines what's inside the chest when opened.

---

### Step 4: Create OneTimeRewards.lsx

**Reference:** `Level13PlusGear/Public/Level13PlusGear/OneTimeRewards/OneTimeRewards.lsx`

**File:** `Level21Gear/Public/Level21Gear/OneTimeRewards/OneTimeRewards.lsx`

**Purpose:** Delivers the L21_Gear_Chest once per playthrough. The OneTimeRewards system spawns the chest when the player starts a new game.

---

### Step 5: Update Localization

**File:** `Level21Gear/Localization/English/Level21Gear.loca.xml`

**Add before closing `</contentList>` tag:**
```xml
<!-- L21_Gear_Chest -->
<content contentuid="[DISPLAYNAME-HANDLE]" version="1">Level 21 Gear Chest</content>
<content contentuid="[DESCRIPTION-HANDLE]" version="1">A chest containing legendary gear for level 21+ characters. Contains the Staff of Gimeitaro.</content>
```

**Purpose:** Provides display name and description for the chest in-game.

---

## Files to Modify/Create

| File | Action | Description |
|------|--------|-------------|
| `Level21Gear/Public/Level21Gear/RootTemplates/L21_Gear_Chest.lsf.lsx` | Create | Chest RootTemplate with appearance and inventory |
| `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Object.txt` | Create | Stats definition for L21_Gear_Chest |
| `Level21Gear/Public/Level21Gear/Stats/Generated/TreasureTable.txt` | Edit | Replace TUT_Chest_Potions with L21_Gear_Chest_TT |
| `Level21Gear/Public/Level21Gear/OneTimeRewards/OneTimeRewards.lsx` | Create | OneTimeRewards delivery for the chest |
| `Level21Gear/Localization/English/Level21Gear.loca.xml` | Edit | Add chest DisplayName and Description |
| `docs/instructions/uuid_workflow.md` | Edit | Remove 4 used UUIDs, add Phase 056 note |
| `docs/level21gear/item_catalog.md` | Edit | Update delivery method documentation |
| `docs/phases/Phase056.md` | Edit | Add implementation section when complete |

---

## UUID/Handle Requirements

### Estimated UUIDs Needed

**L21_Gear_Chest:**
- RootTemplate MapKey: 1 UUID
- OneTimeReward UUID: 1 UUID
- DisplayName handle: 1 UUID (converted to handle)
- Description handle: 1 UUID (converted to handle)

**Total Estimated:** 4 UUIDs

### UUID Allocation

| Purpose | Pool UUID | ed21 UUID | Handle |
|---------|-----------|-----------|--------|
| Chest RootTemplate MapKey | `aa3e541c-165a-4c18-aad1-175c59940bbb` | `ed21541c-165a-4c18-aad1-175c59940bbb` | N/A |
| OneTimeReward UUID | `4797d32e-9395-43f8-b4a6-6469c8b648c3` | `ed21d32e-9395-43f8-b4a6-6469c8b648c3` | N/A |
| DisplayName handle | `5d33db34-eba9-4c17-8436-c76452fc20d8` | `ed21db34-eba9-4c17-8436-c76452fc20d8` | `hed21db34geba9g4c17g8436gc76452fc20d8` |
| Description handle | `93382d3f-a487-49b8-b76b-3763201a26b7` | `ed212d3f-a487-49b8-b76b-3763201a26b7` | `hed212d3fga487g49b8gb76bg3763201a26b7` |

---

## Testing Plan

### Test 1: Chest Appears in Tutorial Chest

**Steps:**
1. Install updated Level21Gear mod
2. Start a new game or load a save where Tutorial Chest has not been opened
3. Navigate to the Tutorial Chest (Nautiloid crash site)
4. Open the Tutorial Chest
5. **Verify:** L21_Gear_Chest appears inside (displayed as a rich ornate chest)
6. **Verify:** Chest has correct name "Level 21 Gear Chest"
7. **Verify:** Staff of Gimeitaro is NOT directly in the Tutorial Chest (only the L21_Gear_Chest)

### Test 2: Chest Appears via OneTimeRewards

**Steps:**
1. Install updated Level21Gear mod
2. Start a new game (or load a save before any OneTimeRewards have been granted)
3. Check player inventory or ground near spawn
4. **Verify:** L21_Gear_Chest also appears via OneTimeRewards
5. **Verify:** Chest has correct name "Level 21 Gear Chest"
6. **Verify:** Chest has correct description

---

### Test 2: Chest Contains Staff of Gimeitaro

**Steps:**
1. Open the L21_Gear_Chest from inventory or ground
2. **Verify:** Staff of Gimeitaro is inside
3. **Verify:** No other unexpected items
4. Pick up the staff
5. **Verify:** Staff can be equipped and all abilities function correctly

---

### Test 3: Tutorial Chest No Longer Contains Staff

**Steps:**
1. Navigate to the Tutorial Chest (Nautiloid crash site)
2. Open the Tutorial Chest
3. **Verify:** Staff of Gimeitaro does NOT appear in the Tutorial Chest
4. **Verify:** Tutorial Chest opens normally with its usual contents

---

### Test 4: OneTimeRewards Fires Only Once

**Steps:**
1. Start a new game and receive the chest
2. Save the game
3. Load the save
4. **Verify:** No duplicate chest appears
5. **Verify:** Only one chest was received

---

## Technical Notes

### OneTimeRewards vs TreasureTable

**Level13PlusGear Pattern:**
- Uses OneTimeRewards to deliver the *chest object itself* to the player
- The chest then contains items via TreasureTable (L13_Gear_Chest_TT)
- This approach means items are locked when the chest is opened (same limitation as Tutorial Chest)
- However, the chest itself is a proper inventory item the player can hold before opening

**Level21Gear (Phase 056):**
- Following the same pattern as Level13PlusGear
- OneTimeRewards delivers L21_Gear_Chest to player
- Chest contains Staff of Gimeitaro via L21_Gear_Chest_TT

### UUID Prefix Convention

Following Level13PlusGear pattern:
- All new UUIDs use `ed21` prefix (first 4 chars replaced)
- Handle format: `hXXXXXXXXgXXXXgXXXXgXXXXgXXXXXXXXXXXX`

### Reference Implementation

Level13PlusGear chests (for comparison):
- **L13_Gear_Chest RootTemplate UUID:** `ed134bf4-d2cc-462b-81cd-ab61536c7375`
- **L13_Gear_Chest Stats Name:** `L13_Gear_Chest`
- **L13_Gear_Chest TreasureTable:** `L13_Gear_Chest_TT`
- **Delivery Method:** OneTimeRewards

---

## Dependencies

**This phase depends on:**
- Phase 054 (Complete) - Staff of Gimeitaro implementation
- Phase 055 (Complete) - Spell concentration adjustments
- UUID pool in `docs/instructions/uuid_workflow.md` - For generating new UUIDs

**This phase affects:**
- Staff of Gimeitaro delivery (no longer in Tutorial Chest)
- Level21Gear mod structure (adds OneTimeRewards system)

---

## Implementation Complete

**Files Created:**
- `Level21Gear/Public/Level21Gear/RootTemplates/L21_Gear_Chest.lsf.lsx` - Chest RootTemplate (UUID: `ed21541c-165a-4c18-aad1-175c59940bbb`)
- `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Object.txt` - Chest stats definition

**Files Modified:**
- `Level21Gear/Public/Level21Gear/Stats/Generated/TreasureTable.txt` - TUT_Chest_Potions now delivers `I_L21_Gear_Chest`; new `L21_Gear_Chest_TT` contains the staff
- `Level21Gear/Localization/English/Level21Gear.loca.xml` - Added chest DisplayName and Description
- `docs/instructions/uuid_workflow.md` - Removed 4 used UUIDs, added Phase 056 note

**Note:** OneTimeRewards was initially created but removed - delivery is Tutorial Chest only. The OneTimeReward UUID (`ed21d32e-9395-43f8-b4a6-6469c8b648c3`) was allocated but not used in any file; it can be reused when adding the chest to Ring of Creation.

---

## Success Criteria

- [x] L21_Gear_Chest RootTemplate created
- [x] Object.txt stats created for L21_Gear_Chest
- [x] TreasureTable updated (L21_Gear_Chest in TUT_Chest_Potions; staff in L21_Gear_Chest_TT)
- [x] Localization entries added for chest name and description
- [x] L21_Gear_Chest appears inside Tutorial Chest
- [x] Opening L21_Gear_Chest yields Staff of Gimeitaro
- [x] Staff of Gimeitaro is NOT directly in Tutorial Chest
- [x] UUID pool updated

---

## Related Documentation

- **Phase 054** - Staff of Gimeitaro initial implementation (Tutorial Chest delivery)
- **Phase 055** - Spell concentration adjustments
- **L13 Gear Chest pattern** - `Level13PlusGear/Public/Level13PlusGear/RootTemplates/L13_Gear_Chest.lsf.lsx`
- **docs/instructions/uuid_workflow.md** - UUID generation workflow
- **docs/level21gear/item_catalog.md** - Item documentation

---
