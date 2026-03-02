# Phase 054: Create Level 21 Gear Mod

**Status:** COMPLETE
**Date:** 2026-02-15

---

## Goals

1. **Create New Mod Structure** - Set up Level21Gear mod with proper directory structure similar to Level13PlusGear
2. **Copy Staff of Akitaro** - Import the Staff of Akitaro from SampleMagicRingMod as the first item
3. **Set Up Documentation** - Create docs/level21gear/ directory with initial item_catalog.md
4. **Configure Mod Files** - Create meta.lsx, info.json, and other required mod files

---

## Summary of Changes

| Action | Component | Description |
|--------|-----------|-------------|
| **Create** | Level21Gear mod directory | New mod structure parallel to Level13PlusGear |
| **Create** | docs/level21gear/ | Documentation directory for Level 21 items |
| **Copy** | Staff of Akitaro | First legendary item in Level21Gear mod |
| **Create** | Mod configuration files | meta.lsx, info.json, etc. |

**Result:** A new mod "Level21Gear" is created with the Staff of Akitaro as its first item, ready for expansion with level 21+ gear.

---

## Current State

### Existing Mod Structure

**SampleMagicRingMod:**
- Contains Staff of Akitaro (legendary staff with powerful abilities)
- Located at `SampleMagicRingMod/`

**Level13PlusGear:**
- Mod for level 13+ characters
- Located at `Level13PlusGear/`
- Has documentation at `docs/level13plusgear/`
- Uses Tutorial Chest delivery via TreasureTable

**Staff of Akitaro (in SampleMagicRingMod):**
- **File:** `SampleMagicRingMod/Public/SampleMagicRingMod/Stats/Generated/Data/Weapon.txt`
- **Name:** SMR_Staff_Akitaro
- **Rarity:** Legendary
- **Powers:** Extremely powerful endgame staff with multiple abilities

---

## Target State

### New Mod: Level21Gear

**Directory Structure:**
```
Level21Gear/
├── Mods/
│   └── Level21Gear/
│       ├── meta.lsx
│       └── ScriptExtender/
│           └── Lua/
├── Public/
│   └── Level21Gear/
│       ├── Content/
│       │   └── [PAK]/
│       │       └── RootTemplates/
│       │           └── _merged.lsf.lsx
│       ├── GUI/
│       │   └── metadata.lsf.lsx
│       ├── Stats/
│       │   └── Generated/
│       │       └── Data/
│       │           ├── Spell_Projectile.txt
│       │           ├── Spell_Target.txt
│       │           └── Weapon.txt
│       └── [PAK]_Localization/
│           └── English/
│               └── english.xml
└── info.json
```

**Documentation Structure:**
```
docs/
├── level21gear/
│   └── item_catalog.md
└── phases/
    └── Phase054.md (this file)
```

**Initial Item:**
- Staff of Akitaro (copied from SampleMagicRingMod with new UUIDs)
- Internal name: L21_Staff_Akitaro

---

## Implementation Plan

### Task 1: Create Mod Directory Structure

**Description:** Set up the Level21Gear mod directory with all required subdirectories

**Steps:**
1. Create `Level21Gear/` root directory
2. Create `Level21Gear/Mods/Level21Gear/` directory
3. Create `Level21Gear/Public/Level21Gear/` directory
4. Create Stats directory: `Level21Gear/Public/Level21Gear/Stats/Generated/Data/`
5. Create RootTemplates directory: `Level21Gear/Public/Level21Gear/Content/[PAK]/RootTemplates/`
6. Create Localization directory: `Level21Gear/Public/Level21Gear/[PAK]_Localization/English/`
7. Create GUI directory: `Level21Gear/Public/Level21Gear/GUI/`

**Files to create:**
- Directory structure only (no files yet)

### Task 2: Create Mod Configuration Files

**Description:** Create meta.lsx and info.json files for the mod

**Steps:**
1. Create `Level21Gear/Mods/Level21Gear/meta.lsx` based on Level13PlusGear structure
2. Create `Level21Gear/info.json` with mod metadata
3. Create `Level21Gear/Public/Level21Gear/GUI/metadata.lsf.lsx`

**Files to create:**
- `Level21Gear/Mods/Level21Gear/meta.lsx`
- `Level21Gear/info.json`
- `Level21Gear/Public/Level21Gear/GUI/metadata.lsf.lsx`

### Task 3: Copy Staff of Akitaro

**Description:** Copy the Staff of Akitaro from SampleMagicRingMod to Level21Gear with new UUIDs

**Steps:**
1. Copy staff entry from `SampleMagicRingMod/Public/SampleMagicRingMod/Stats/Generated/Data/Weapon.txt`
2. Rename from SMR_Staff_Akitaro to L21_Staff_Akitaro
3. Generate new UUIDs for RootTemplate and any other references
4. Copy related spells from Spell_Projectile.txt and Spell_Target.txt
5. Update spell names with L21 prefix
6. Create RootTemplate file for the staff

**Files to create:**
- `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Weapon.txt`
- `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Projectile.txt`
- `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Target.txt`
- `Level21Gear/Public/Level21Gear/Content/[PAK]/RootTemplates/_merged.lsf.lsx`

### Task 4: Create Localization File

**Description:** Create english.xml with localized strings for the staff

**Steps:**
1. Create `Level21Gear/Public/Level21Gear/[PAK]_Localization/English/english.xml`
2. Add DisplayName and Description handles for Staff of Akitaro
3. Add any spell-related localization strings

**Files to create:**
- `Level21Gear/Public/Level21Gear/[PAK]_Localization/English/english.xml`

### Task 5: Set Up Documentation

**Description:** Create documentation directory and initial item catalog

**Steps:**
1. Create `docs/level21gear/` directory
2. Create `docs/level21gear/item_catalog.md` based on level13plusgear template
3. Add Staff of Akitaro entry to the catalog

**Files to create:**
- `docs/level21gear/item_catalog.md`

### Task 6: Set Up Tutorial Chest Delivery

**Description:** Configure TreasureTable to add Staff of Akitaro to Tutorial Chest

**Steps:**
1. Create `Level21Gear/Public/Level21Gear/Stats/Generated/TreasureTable.txt`
2. Add Tutorial Chest TreasureTable entry with Staff of Akitaro
3. Use same pattern as Level13PlusGear mod

**Files to create:**
- `Level21Gear/Public/Level21Gear/Stats/Generated/TreasureTable.txt`

### Task 7: Update CLAUDE.md

**Description:** Add Level21Gear to the active mods list in CLAUDE.md

**Steps:**
1. Open `CLAUDE.md`
2. Add Level21Gear to the "Active Mods" table
3. Document Tutorial Chest delivery method
4. Note that it follows similar structure to Level13PlusGear

**Files to modify:**
- `CLAUDE.md` - Add Level21Gear to active mods list

---

## Detailed Implementation

### Step 1: Create Mod Configuration Files

**File:** `Level21Gear/Mods/Level21Gear/meta.lsx`

**Content:**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<save>
    <version major="4" minor="0" revision="9" build="331"/>
    <region id="Config">
        <node id="root">
            <children>
                <node id="Dependencies"/>
                <node id="ModuleInfo">
                    <attribute id="Author" type="LSString" value="YourName"/>
                    <attribute id="CharacterCreationLevelName" type="FixedString" value=""/>
                    <attribute id="Description" type="LSString" value="Legendary gear for level 21+ characters"/>
                    <attribute id="Folder" type="LSString" value="Level21Gear"/>
                    <attribute id="LobbyLevelName" type="FixedString" value=""/>
                    <attribute id="MD5" type="LSString" value=""/>
                    <attribute id="MainMenuBackgroundVideo" type="FixedString" value=""/>
                    <attribute id="MenuLevelName" type="FixedString" value=""/>
                    <attribute id="Name" type="LSString" value="Level 21 Gear"/>
                    <attribute id="NumPlayers" type="uint8" value="4"/>
                    <attribute id="PhotoBoothLevelName" type="FixedString" value=""/>
                    <attribute id="StartupLevelName" type="FixedString" value=""/>
                    <attribute id="Tags" type="LSString" value=""/>
                    <attribute id="Type" type="FixedString" value="Add-on"/>
                    <attribute id="UUID" type="FixedString" value="[GENERATE-NEW-UUID]"/>
                    <attribute id="Version64" type="int64" value="36028797018963968"/>
                    <children>
                        <node id="PublishVersion">
                            <attribute id="Version64" type="int64" value="36028797018963968"/>
                        </node>
                        <node id="Scripts"/>
                        <node id="TargetModes">
                            <children>
                                <node id="Target">
                                    <attribute id="Object" type="FixedString" value="Story"/>
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

**File:** `Level21Gear/info.json`

**Content:**
```json
{
    "Mods": [
        {
            "Author": "YourName",
            "Name": "Level 21 Gear",
            "Folder": "Level21Gear",
            "Version": "1.0.0",
            "Description": "Legendary gear for level 21+ characters. Starts with the Staff of Akitaro.",
            "UUID": "[SAME-UUID-AS-META-LSX]",
            "Created": "2026-02-15T00:00:00",
            "Group": "d16c5eb3-5269-40ce-baf0-20aa34b5c87e"
        }
    ]
}
```

### Step 2: Copy Staff of Akitaro to Weapon.txt

**File:** `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Weapon.txt`

**Steps:**
1. Read Staff of Akitaro from SampleMagicRingMod
2. Rename SMR_Staff_Akitaro → L21_Staff_Akitaro
3. Generate new RootTemplate UUID
4. Update all spell references to use L21 prefix

**Purpose:** Creates the weapon stats for the Staff of Akitaro in the new mod

### Step 3: Copy and Update Spells

**Files:**
- `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Projectile.txt`
- `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Target.txt`

**Steps:**
1. Copy all Staff of Akitaro spell entries from SampleMagicRingMod
2. Rename all spell names with L21 prefix
3. Update any cross-references between spells

**Purpose:** Maintains all spell functionality for the staff

### Step 4: Create RootTemplate

**File:** `Level21Gear/Public/Level21Gear/Content/[PAK]/RootTemplates/_merged.lsf.lsx`

**Template:**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<save>
    <version major="4" minor="0" revision="9" build="328"/>
    <region id="Templates">
        <node id="Templates">
            <children>
                <node id="GameObjects">
                    <attribute id="LevelName" type="FixedString" value=""/>
                    <attribute id="MapKey" type="FixedString" value="[NEW-UUID]"/>
                    <attribute id="Name" type="LSString" value="L21_Staff_Akitaro"/>
                    <attribute id="ParentTemplateId" type="FixedString" value="[STAFF-PARENT-TEMPLATE]"/>
                    <attribute id="Stats" type="FixedString" value="L21_Staff_Akitaro"/>
                    <attribute id="Type" type="FixedString" value="item"/>
                    <attribute id="_OriginalFileVersion_" type="int64" value="144115188075855912"/>
                    <children>
                        <node id="GameMaster"/>
                    </children>
                </node>
            </children>
        </node>
    </region>
</save>
```

### Step 5: Create TreasureTable for Tutorial Chest

**File:** `Level21Gear/Public/Level21Gear/Stats/Generated/TreasureTable.txt`

**Content:**
```
new treasuretable "TUT_Chest_Potions"
CanMerge 1
new subtable "1,1"
object category "I_L21_Staff_Akitaro",1,0,0,0,0,0,0,0
```

**Purpose:** Injects the Staff of Akitaro into the Tutorial Chest so it appears when the chest is opened

**Technical Notes:**
- Uses the same Tutorial Chest ID as Level13PlusGear: `TUT_Chest_Potions`
- The `CanMerge 1` flag allows this to merge with other mods' treasure table entries
- Format: `object category "InternalName",1,0,0,0,0,0,0,0`

### Step 6: Create Initial Documentation

**File:** `docs/level21gear/item_catalog.md`

**Template:**
```markdown
# Level 21 Gear - Item Catalog

Complete list of all items in the Level 21 Gear mod for BG3.

**Target Audience:** Level 21+ characters
**Delivery Method:** TBD (likely console commands or Script Extender)

---

## Table of Contents
- [Weapons](#weapons)
  - [Staves](#staves)

---

## Weapons

### Staves

#### Staff of Akitaro
**Internal Name:** `L21_Staff_Akitaro`
**Rarity:** Legendary
**Enchantment:** +3
**Base Weapon:** Quarterstaff

**RootTemplate UUID:** `[UUID]`
**Handle (Name):** `[handle]`
**Handle (Description):** `[handle]`

**Weapon Properties:**
- [List properties from original]

**Passives:**
- [List passives from original]

**Spells Granted:**
- [List spells from original]

**Lore:**
[Copy lore from original if available]

**Source:** Copied from SampleMagicRingMod (SMR_Staff_Akitaro) and adapted for Level 21 Gear.

---

## Implementation Status

| Item | Status | Phase | Notes |
|------|--------|-------|-------|
| Staff of Akitaro | PENDING | 054 | Initial item for mod |

---

## Statistics

- **Total Items:** 1
- **Weapons:** 1 (1 Staff)
- **Armor:** 0
- **Accessories:** 0

**Last Updated:** 2026-02-15
```

---

## Files to Create

| File | Action | Description |
|------|--------|-------------|
| `Level21Gear/Mods/Level21Gear/meta.lsx` | Create | Mod metadata and configuration |
| `Level21Gear/info.json` | Create | Mod information for mod managers |
| `Level21Gear/Public/Level21Gear/GUI/metadata.lsf.lsx` | Create | GUI metadata |
| `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Weapon.txt` | Create | Staff of Akitaro weapon stats |
| `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Projectile.txt` | Create | Projectile spells for staff |
| `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Target.txt` | Create | Target spells for staff |
| `Level21Gear/Public/Level21Gear/Stats/Generated/TreasureTable.txt` | Create | Tutorial Chest treasure table injection |
| `Level21Gear/Public/Level21Gear/Content/[PAK]/RootTemplates/_merged.lsf.lsx` | Create | RootTemplate for staff |
| `Level21Gear/Public/Level21Gear/[PAK]_Localization/English/english.xml` | Create | Localized strings |
| `docs/level21gear/item_catalog.md` | Create | Documentation for Level 21 items |
| `CLAUDE.md` | Edit | Add Level21Gear to active mods list |

---

## UUID/Handle Requirements

### Estimated UUIDs Needed

**Mod Configuration:**
- Mod UUID (meta.lsx and info.json): 1 UUID

**Staff of Akitaro:**
- RootTemplate: 1 UUID
- DisplayName: 1 handle
- Description: 1 handle

**Spells (if any new handles needed):**
- Spell names/descriptions: TBD (likely can reuse from SampleMagicRingMod)

**Total Estimated:** 2 UUIDs, 2 handles (minimum)

### UUID Allocation

**Note:** Will use UUID pool from `docs/instructions/uuid_workflow.md` for Level 21 Gear following the same `ed21` prefix pattern as Level 13 Gear uses `ed13`.

[To be filled in during implementation]

---

## Testing Plan

### Test 1: Mod Loads Successfully
1. Package the Level21Gear mod
2. Install in BG3 Mod Manager
3. Enable the mod
4. Launch BG3
5. **Verify:** Mod appears in mod list
6. **Verify:** No errors in Script Extender console

### Test 2: Staff of Akitaro Appears in Tutorial Chest
1. Start a new game or load a save where Tutorial Chest has not been opened
2. Navigate to the Tutorial Chest location (Nautiloid crash site)
3. Open the Tutorial Chest
4. **Verify:** Staff of Akitaro appears in the chest loot
5. **Verify:** Staff has correct name and description
6. **Verify:** Staff shows Legendary rarity
7. **Verify:** Can be picked up and added to inventory

**Note:** If testing with a save where chest was already opened, will need to use console commands to spawn the staff for testing

### Test 3: Staff Properties Work Correctly
1. Equip the Staff of Akitaro
2. Check character sheet for stat bonuses
3. **Verify:** All passives are applied
4. **Verify:** All spells appear in hotbar/spell list
5. **Verify:** Weapon properties match original from SampleMagicRingMod

### Test 4: Staff Spells Function
1. With Staff of Akitaro equipped
2. Test each spell granted by the staff
3. **Verify:** All spells cast successfully
4. **Verify:** Spell effects match original functionality
5. **Verify:** Cooldowns work correctly

---

## Technical Notes

### UUID Prefix Convention

Following the pattern from Level13PlusGear:
- Level 13 Gear uses `ed13` prefix for UUIDs
- Level 21 Gear will use `ed21` prefix for UUIDs

**Example:**
- Pool UUID: `0fc32b7f-6fb7-4d5b-8e87-4c1e9c1a0d0a`
- L21 UUID: `ed212b7f-6fb7-4d5b-8e87-4c1e9c1a0d0a`

### Naming Convention

**Internal Names:**
- Prefix: `L21_` (for Level 21)
- Example: `L21_Staff_Akitaro`

**Spell Names:**
- Prefix: `L21_`
- Example: `L21_Projectile_Akitaro_LightningBolt`

### Parent Templates

The Staff of Akitaro will need to reference the correct parent template UUID from vanilla BG3. This should be copied from the original staff's RootTemplate.

### PAK Name

The `[PAK]` placeholder in directory names will be replaced with the actual mod name during packaging. For consistency with other mods, this should be `Level21Gear`.

### Tutorial Chest Delivery

Following the same pattern as Level13PlusGear:
- Uses TreasureTable injection to add items to `TUT_Chest_Potions`
- Items appear when the Tutorial Chest is opened on the Nautiloid crash site
- **Limitation:** Once chest is opened in a save, loot is locked - new items won't appear in existing saves
- This means the mod is designed for new games or saves where Tutorial Chest hasn't been opened yet

**TreasureTable Format:**
```
new treasuretable "TUT_Chest_Potions"
CanMerge 1
new subtable "1,1"
object category "InternalName",1,0,0,0,0,0,0,0
```

---

## Dependencies

**This phase depends on:**
- SampleMagicRingMod - Source for Staff of Akitaro
- UUID pool in `docs/instructions/uuid_workflow.md` - For generating new UUIDs
- BG3 Mod Manager - For packaging and testing

**This phase affects:**
- CLAUDE.md - Will be updated to include Level21Gear in active mods
- Future Level 21 Gear development - Establishes foundation for additional items

---

## Decisions Made

1. **Item Delivery Method:** Tutorial Chest injection (same as Level13PlusGear)
   - Items will appear in the Tutorial Chest via TreasureTable injection
   - Follows the same pattern as Level13PlusGear mod
   - Note: Once chest is opened in a save, loot is locked (same limitation as L13 mod)

2. **Staff of Akitaro Modifications:** Keep identical to SampleMagicRingMod version
   - Will maintain all original powers and stats
   - Future phases can enhance the staff if needed
   - Provides a strong legendary baseline for level 21+ characters

---

## Success Criteria

- [ ] Level21Gear mod directory structure created
- [ ] Mod configuration files (meta.lsx, info.json) created with valid UUIDs
- [ ] Staff of Akitaro copied and renamed with L21 prefix
- [ ] All staff spells copied and updated
- [ ] RootTemplate created for staff
- [ ] Localization file created with staff strings
- [ ] Documentation directory (docs/level21gear/) created
- [ ] item_catalog.md created with Staff of Akitaro entry
- [ ] CLAUDE.md updated with Level21Gear in active mods
- [ ] Mod successfully loads in BG3
- [ ] Staff of Akitaro can be spawned and functions correctly

---

## Related Documentation

- **Level13PlusGear structure** - Reference for mod organization
- **docs/instructions/uuid_workflow.md** - UUID generation workflow
- **docs/instructions/PhaseDocumentTemplate.md** - Phase document template
- **SampleMagicRingMod** - Source for Staff of Akitaro

---

## Notes

### Why Start with Staff of Akitaro?

The Staff of Akitaro is an excellent starting point for Level 21 Gear because:
- It's already a powerful legendary item
- It has complex functionality (multiple spells, passives)
- It serves as a good template for future high-level items
- It's well-documented and tested in SampleMagicRingMod

### Future Expansion

Level 21 Gear is intended to be a collection of endgame items for characters who have exceeded the normal level cap. After establishing the mod with Staff of Akitaro, future phases can add:
- More legendary weapons
- Legendary armor sets
- Unique accessories
- Special utility items
- Items that synergize with level 20+ abilities

### Comparison to Level13PlusGear

**Similarities:**
- Directory structure
- Documentation structure (docs/level21gear/ mirrors docs/level13plusgear/)
- UUID prefix convention (ed21 vs ed13)
- Internal name prefix (L21 vs L13)

**Differences:**
- Target level (21+ vs 13+)
- Power level of items (should be more powerful)
- Delivery method (TBD vs Tutorial Chest)

---

## Implementation Summary

**Completed:**

1. **Directory Structure Created** ✓
   - Created Level21Gear/Mods/Level21Gear/
   - Created Level21Gear/Public/Level21Gear/Stats/Generated/Data/
   - Created Level21Gear/Public/Level21Gear/RootTemplates/
   - Created Level21Gear/Public/Level21Gear/Localization/English/
   - Created docs/level21gear/

2. **Mod Configuration Files Created** ✓
   - meta.lsx with Mod UUID: ed2135f2-a754-4cb9-851d-a16e8c8ebef2
   - info.json with mod metadata
   - Files created and configured

3. **Staff of Akitaro Copied and Adapted** ✓
   - Weapon.txt created with L21_Staff_Akitaro entry
   - RootTemplate UUID: ed21b86f-a7f7-4de6-ad51-1a2c33b9c779
   - All passives and boosts preserved from original
   - StatusOnEquip maintained

4. **Spells Copied and Renamed** ✓
   - Created Spell_Target.txt (4 target spells)
   - Created Spell_Projectile.txt (3 projectile spells)
   - Created Spell_Shout.txt (1 shout spell)
   - Created Spell_Teleportation.txt (1 teleportation spell)
   - Created Interrupt.txt (2 interrupt spells)
   - All spell names updated from SMR_ to L21_ prefix

5. **Tutorial Chest Delivery Configured** ✓
   - Created TreasureTable.txt
   - Configured injection into TUT_Chest_Potions
   - Uses same delivery method as Level13PlusGear

6. **RootTemplate Created** ✓
   - Created L21_Staff_Akitaro.lsf.lsx
   - Parent template: e1e112b2-5465-4e37-acdc-372666ec1521
   - Visual template: fb8204e8-e265-7af3-86b1-7341c6880ba1
   - All required attributes set

7. **Localization File Created** ✓
   - Created english.xml with DisplayName and Description
   - Uses handles from SampleMagicRingMod for consistency

8. **Documentation Created** ✓
   - Created docs/level21gear/item_catalog.md
   - Documented Staff of Akitaro with full details
   - Listed all passives, spells, and properties

9. **CLAUDE.md Updated** ✓
   - Added Level21Gear to active mods table
   - Added delivery method convention
   - Documented Tutorial Chest delivery

10. **UUID Pool Updated** ✓
    - Removed used UUIDs from uuid_workflow.md
    - Mod UUID: ed2135f2-a754-4cb9-851d-a16e8c8ebef2
    - Staff UUID: ed21b86f-a7f7-4de6-ad51-1a2c33b9c779

**Status:** IMPLEMENTED (awaiting user testing)

---

## UUID Allocation (Completed)

**Mod Configuration:**
- **Mod UUID:** `ed2135f2-a754-4cb9-851d-a16e8c8ebef2`
- **Purpose:** Level21Gear mod identifier (used in meta.lsx and info.json)
- **Source:** UUID pool, prefix changed to ed21

**Staff of Akitaro:**
- **RootTemplate UUID:** `ed21b86f-a7f7-4de6-ad51-1a2c33b9c779`
- **Purpose:** Staff of Akitaro RootTemplate MapKey
- **Source:** UUID pool, prefix changed to ed21
- **DisplayName Handle:** `h1a2b3c4dg5e6fg7a8bg9c0dg1e2f3a4b5c6d7` (reused from SampleMagicRingMod)
- **Description Handle:** `h2b3c4d5eg6f7ag8b9cg0d1eg2f3a4b5c6d7e8` (reused from SampleMagicRingMod)

**Spell Handles:** All spell handles reused from SampleMagicRingMod originals for consistency

---

## Revision Sections

### Revision 1: Rename Staff and Randomize Handles

**Issue:**
1. Staff name "Akitaro" should be changed to "Gimeitaro" to differentiate from SampleMagicRingMod
2. Many handles and UUIDs are reused from SampleMagicRingMod - need to review which should be randomized from uuid_workflow.md pool

**Root Cause:**
Initial implementation copied handles directly from SampleMagicRingMod for speed, but this may cause conflicts or confusion.

**Solution:**
1. Rename all references from "Akitaro" to "Gimeitaro"
2. Review all UUIDs and handles (see table below)
3. Replace handles with new random ones from UUID pool where appropriate

**UUID and Handle Inventory:**

The following table lists all UUIDs and UUID-like handles in the Level21Gear mod:

| Type | Current Value | Location | Source | Recommendation |
|------|---------------|----------|--------|----------------|
| **Mod UUID** | `ed2135f2-a754-4cb9-851d-a16e8c8ebef2` | meta.lsx, info.json | UUID pool (ed21 prefix) | ✓ Keep - properly randomized |
| **Staff RootTemplate UUID** | `ed21b86f-a7f7-4de6-ad51-1a2c33b9c779` | Weapon.txt, L21_Staff_Akitaro.lsf.lsx | UUID pool (ed21 prefix) | ✓ Keep - properly randomized |
| **Staff Parent Template** | `e1e112b2-5465-4e37-acdc-372666ec1521` | L21_Staff_Akitaro.lsf.lsx | From SampleMagicRingMod | ✓ Keep - vanilla reference |
| **Staff Visual Template** | `fb8204e8-e265-7af3-86b1-7341c6880ba1` | L21_Staff_Akitaro.lsf.lsx | From SampleMagicRingMod | ✓ Keep - visual asset reference |
| **Staff DisplayName Handle** | `h8054ad1dg1aeag4b70gb63fgeabb5fb10181` | L21_Staff_Gimeitaro.lsf.lsx | UUID pool (randomized in R1) | ✓ Randomized |
| **Staff Description Handle** | `hb514d87agf785g4f45g8c93g4827fb5d7f3f` | L21_Staff_Gimeitaro.lsf.lsx | UUID pool (randomized in R1) | ✓ Randomized |
| **Light Spell DisplayName** | `(none - uses vanilla)` | Spell_Target.txt | Vanilla | ✓ Keep |
| **Knock DisplayName** | `h623f3f43gc3e3g4811g866dg2c78072bc69a` | Spell_Target.txt | UUID pool (randomized in R1) | ✓ Randomized |
| **Knock Description** | `h81c15d59gc758g4b66g96c9gded4998d6a9f` | Spell_Target.txt | UUID pool (randomized in R1) | ✓ Randomized |
| **GimeitarosTeleport DisplayName** | `hed73d5c7g1c7cg4ed2gbc7eged6b4d454460` | Spell_Target.txt | UUID pool (randomized in R1) | ✓ Randomized |
| **GimeitarosTeleport Description** | `h41f5f4a4gc036g4db2g9763g51e01ba28887` | Spell_Target.txt | UUID pool (randomized in R1) | ✓ Randomized |
| **GimeitarosShield DisplayName** | `h57a21a18g4d37g4935g926cg8ea8169f84f6` | Spell_Target.txt | UUID pool (randomized in R1) | ✓ Randomized |
| **GimeitarosShield Description** | `h7eec854fgb997g466fg8a74g59e5d6e6e978` | Spell_Target.txt | UUID pool (randomized in R1) | ✓ Randomized |
| **GimeitarosBlast DisplayName** | `h80380ea8g80a2g4a71g8269g3c7d26dd91a5` | Spell_Projectile.txt | UUID pool (randomized in R1) | ✓ Randomized |
| **GimeitarosBlast Description** | `h3e018fbcgf4a3g440egb169gc938dfde49f5` | Spell_Projectile.txt | UUID pool (randomized in R1) | ✓ Randomized |
| **GimeitarosBarrage DisplayName** | `h6b3e5669g8780g4a36g8e55gf59f22b5ebfa` | Spell_Projectile.txt | UUID pool (randomized in R1) | ✓ Randomized |
| **GimeitarosBarrage Description** | `had00001aga204g4af5g9f9cg2703b9654ec0` | Spell_Projectile.txt | UUID pool (randomized in R1) | ✓ Randomized |
| **Shield Interrupt DisplayName** | `hc56fc6ebg7b46g4739g96e5g4f896829c10c` | Interrupt.txt | UUID pool (randomized in R1) | ✓ Randomized |
| **Shield Interrupt Description** | `haaf7657agcc38g445cgb1e8g8c8a93d1f648` | Interrupt.txt | UUID pool (randomized in R1) | ✓ Randomized |
| **Counterspell DisplayName** | `h49fe5773g5cdeg4791g9668g7f67f1bb9d1c` | Interrupt.txt | UUID pool (randomized in R1) | ✓ Randomized |
| **Counterspell Description** | `h06b70227g4bcbg4ed6ga3b9ga458a9bf9e31` | Interrupt.txt | UUID pool (randomized in R1) | ✓ Randomized |
| **Arcane Gate DisplayName** | `h023d53c4g351dg47ecgb7ebg32765783d8d3` | Spell_Teleportation.txt | UUID pool (randomized in R1) | ✓ Randomized |
| **Arcane Gate Description** | `hbc94a0beg96afg4c71ga16dg86741886005e` | Spell_Teleportation.txt | UUID pool (randomized in R1) | ✓ Randomized |

**Summary:**
- **2 UUIDs properly randomized** (mod UUID, staff UUID) ✓
- **2 template references** (parent, visual) - vanilla references ✓
- **18 handles randomized in Revision 1** ✓
  - 2 for staff name/description
  - 16 for spell names/descriptions

**Actions Needed:**
1. ✓ Rename "Akitaro" to "Gimeitaro" in all files
2. ✓ Replace all 18 reviewed handles with randomized UUIDs from pool
3. ✓ Update handles in spell files (Spell_Target.txt, Spell_Projectile.txt, Interrupt.txt, Spell_Teleportation.txt)
4. ✓ Update RootTemplate with new handles
5. ✓ Update TreasureTable.txt with new staff name
6. ✓ Update docs/level21gear/item_catalog.md with new name and handles
7. ✓ Remove used UUIDs from uuid_workflow.md pool

**Implementation Complete:**

**Files Updated:**
- `Level21Gear/Public/Level21Gear/RootTemplates/L21_Staff_Gimeitaro.lsf.lsx` (renamed from L21_Staff_Akitaro.lsf.lsx)
  - Updated DisplayName handle: h8054ad1dg1aeag4b70gb63fgeabb5fb10181
  - Updated Description handle: hb514d87agf785g4f45g8c93g4827fb5d7f3f
- `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Weapon.txt`
  - Renamed L21_Staff_Akitaro → L21_Staff_Gimeitaro
  - Renamed all spell references from Akitaros → Gimeitaros
- `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Target.txt`
  - Renamed L21_Target_AkitarosTeleport_ShortRest → L21_Target_GimeitarosTeleport_ShortRest
  - Renamed L21_Target_AkitarosShield_ShortRest → L21_Target_GimeitarosShield_ShortRest
  - Updated 6 handles with randomized UUIDs
- `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Projectile.txt`
  - Renamed L21_Projectile_AkitarosBlast_ShortRest → L21_Projectile_GimeitarosBlast_ShortRest
  - Renamed L21_Projectile_AkitarosBarrage_Unlimited → L21_Projectile_GimeitarosBarrage_Unlimited
  - Updated 4 handles with randomized UUIDs
- `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Interrupt.txt`
  - Updated 4 handles with randomized UUIDs
- `Level21Gear/Public/Level21Gear/Stats/Generated/Data/Spell_Teleportation.txt`
  - Updated 2 handles with randomized UUIDs
- `Level21Gear/Public/Level21Gear/Stats/Generated/TreasureTable.txt`
  - Changed I_L21_Staff_Akitaro → I_L21_Staff_Gimeitaro
- `Level21Gear/Public/Level21Gear/Localization/English/english.xml`
  - Updated all 18 handles with new randomized values
  - Changed all "Akitaro" references to "Gimeitaro"
  - Added complete localization for all custom spells
- `docs/level21gear/item_catalog.md`
  - Changed "Staff of Akitaro" → "Staff of Gimeitaro"
  - Updated internal name L21_Staff_Akitaro → L21_Staff_Gimeitaro
  - Updated handles to match new randomized UUIDs
  - Changed all spell references from "Akitaro's" → "Gimeitaro's"
- `docs/instructions/uuid_workflow.md`
  - Removed 18 used UUIDs from pool
  - Added note: "Phase 054 Revision 1 used 18 UUIDs (18 handles)"

**UUID Allocation (Revision 1):**
Converted 18 UUIDs from pool to handles using standard format (xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx → hxxxxxxxxgxxxxgxxxxgxxxxgxxxxxxxxxxxx):

1. Staff DisplayName: h8054ad1dg1aeag4b70gb63fgeabb5fb10181
2. Staff Description: hb514d87agf785g4f45g8c93g4827fb5d7f3f
3. Knock DisplayName: h623f3f43gc3e3g4811g866dg2c78072bc69a
4. Knock Description: h81c15d59gc758g4b66g96c9gded4998d6a9f
5. GimeitarosTeleport DisplayName: hed73d5c7g1c7cg4ed2gbc7eged6b4d454460
6. GimeitarosTeleport Description: h41f5f4a4gc036g4db2g9763g51e01ba28887
7. GimeitarosShield DisplayName: h57a21a18g4d37g4935g926cg8ea8169f84f6
8. GimeitarosShield Description: h7eec854fgb997g466fg8a74g59e5d6e6e978
9. GimeitarosBlast DisplayName: h80380ea8g80a2g4a71g8269g3c7d26dd91a5
10. GimeitarosBlast Description: h3e018fbcgf4a3g440egb169gc938dfde49f5
11. GimeitarosBarrage DisplayName: h6b3e5669g8780g4a36g8e55gf59f22b5ebfa
12. GimeitarosBarrage Description: had00001aga204g4af5g9f9cg2703b9654ec0
13. Shield Interrupt DisplayName: hc56fc6ebg7b46g4739g96e5g4f896829c10c
14. Shield Interrupt Description: haaf7657agcc38g445cgb1e8g8c8a93d1f648
15. Counterspell DisplayName: h49fe5773g5cdeg4791g9668g7f67f1bb9d1c
16. Counterspell Description: h06b70227g4bcbg4ed6ga3b9ga458a9bf9e31
17. Arcane Gate DisplayName: h023d53c4g351dg47ecgb7ebg32765783d8d3
18. Arcane Gate Description: hbc94a0beg96afg4c71ga16dg86741886005e

**Status:** COMPLETE - All handles randomized, staff renamed to Gimeitaro

---

### Revision 2: Upgrade Gimeitaro's Shield to Silvered Bulwark

**Issue:**
Gimeitaro's Shield currently uses Globe of Invulnerability as its base spell. This creates a stationary protective zone that doesn't move with the target. Phase 053 upgraded the Akitaro's Shield spell in SampleMagicRingMod to use the superior Silvered Bulwark power, which follows the target.

**Root Cause:**
Initial Phase 054 implementation copied the staff before Phase 053's Silvered Bulwark upgrade was completed.

**Solution:**
Update L21_Target_GimeitarosShield_ShortRest to match the Silvered Bulwark implementation from Phase 053.

**Changes Required:**

1. **Update Spell_Target.txt** - Replace current Gimeitaro's Shield entry with full Silvered Bulwark implementation
2. **Update Spell_Shout.txt** - Change Celestial Haste from bonus action to free action AND add Spirit Guardians (free action, unlimited)
3. **Update Weapon.txt** - Update spell reference for renamed Gimeitaro's Shield, add skill/ability/initiative/save bonuses, and add Spirit Guardians
4. **Update Localization** - Update spell descriptions and staff description to reflect all changes

**Current Implementation (Globe of Invulnerability):**
```
new entry "L21_Target_GimeitarosShield_ShortRest"
type "SpellData"
data "SpellType" "Target"
using "Target_GlobeOfInvulnerability"
data "DisplayName" "h57a21a18g4d37g4935g926cg8ea8169f84f6;1"
data "ExtraDescription" "h7eec854fgb997g466fg8a74g59e5d6e6e978;1"
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

**Target Implementation (Silvered Bulwark - Unlimited):**
```
new entry "L21_Target_GimeitarosShield_Unlimited"
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
data "DisplayName" "h57a21a18g4d37g4935g926cg8ea8169f84f6;1"
data "ExtraDescription" "h7eec854fgb997g466fg8a74g59e5d6e6e978;1"
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
```

**Key Differences:**
- Renamed spell from `L21_Target_GimeitarosShield_ShortRest` to `L21_Target_GimeitarosShield_Unlimited`
- Added `Level "6"` and `SpellSchool "Abjuration"` for proper spell classification
- Added `SpellProperties` to apply the Silvered Bulwark status effect
- Added `TargetRadius "18"` and cleared `AreaRadius ""` to make it target-following
- Added `TargetConditions` to prevent stacking multiple Silvered Bulwarks
- **Removed `Cooldown "OncePerShortRest"`** - now unlimited uses
- Kept `UseCosts "BonusActionPoint:1"` - bonus action to cast
- Result: Shield now follows the target and can be cast unlimited times as a bonus action

**Localization Update:**

Current text (english.xml):
```xml
<content contentuid="h57a21a18g4d37g4935g926cg8ea8169f84f6" version="1">Gimeitaro's Shield</content>
<content contentuid="h7eec854fgb997g466fg8a74g59e5d6e6e978" version="1">Globe of Invulnerability. Once per short rest.</content>
```

Updated text:
```xml
<content contentuid="h57a21a18g4d37g4935g926cg8ea8169f84f6" version="1">Gimeitaro's Shield</content>
<content contentuid="h7eec854fgb997g466fg8a74g59e5d6e6e978" version="1">Silvered Bulwark. Grants invulnerability that follows the target. Unlimited uses as a bonus action.</content>
```

**Additional Changes:**

**1. Celestial Haste - Change to Free Action:**

Current (Spell_Shout.txt):
```
new entry "L21_Shout_CelestialHaste_Unlimited"
type "SpellData"
data "SpellType" "Shout"
using "Shout_MAG_Victory_Longbow_Haste"
data "UseCosts" "BonusActionPoint:1"
data "Cooldown" ""
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsSpell"
```

Target (Free Action):
```
new entry "L21_Shout_CelestialHaste_Unlimited"
type "SpellData"
data "SpellType" "Shout"
using "Shout_MAG_Victory_Longbow_Haste"
data "UseCosts" ""
data "Cooldown" ""
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsSpell"
```

Change: `UseCosts "BonusActionPoint:1"` → `UseCosts ""` (makes it a free action)

**b) Add Spirit Guardians (Free Action, Unlimited):**

Add three new spell entries to Spell_Shout.txt:

```
new entry "L21_Shout_SpiritGuardians_Gimeitaro"
type "SpellData"
data "SpellType" "Shout"
data "Level" "3"
data "SpellSchool" "Conjuration"
data "ContainerSpells" "L21_Shout_SpiritGuardians_Gimeitaro_Necrotic;L21_Shout_SpiritGuardians_Gimeitaro_Radiant"
data "AreaRadius" "3"
data "TargetConditions" "Self()"
data "Icon" "Spell_Conjuration_SpiritGuardians"
data "DisplayName" "[HANDLE];1"
data "Description" "[HANDLE];1"
data "DescriptionParams" "DealDamage(3d8,Radiant);DealDamage(3d8,Necrotic)"
data "TooltipAttackSave" "Wisdom"
data "PrepareSound" "Spell_Prepare_Damage_Radiant_Gen_L1to3"
data "PrepareLoopSound" "Spell_Prepare_Damage_Radiant_Gen_L1to3_Loop"
data "CastSound" "Spell_Cast_Damage_Radiant_SpiritGuardian_L1to3"
data "TargetSound" "Spell_Impact_Damage_Radiant_SpiritGuardian_L1to3"
data "CastTextEvent" "Cast"
data "UseCosts" ""
data "SpellAnimation" "03496c4a-49e0-4132-b585-3e5ecd1ad8e5,,;,,;cb171bda-f065-4520-b470-e447f678ba1f,,;18a9b8b8-6cec-4a6d-be46-a4cc499505e9,,;cc5b0caf-3ed1-4711-a50d-11dc3f1fdc6a,,;,,;0b07883a-08b8-43b6-ac18-84dc9e84ff50,,;,,;,,"
data "VerbalIntent" "Damage"
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsConcentration;IsSpell;IsHarmful;IsLinkedSpellContainer"
data "PrepareEffect" "2534712b-d31e-45a4-b8e3-6385caa9ddc1"
data "CastEffect" "56ea5092-8ecd-4b86-8686-c1c35d016928"

new entry "L21_Shout_SpiritGuardians_Gimeitaro_Radiant"
type "SpellData"
data "SpellType" "Shout"
using "Shout_SpiritGuardians"
data "SpellContainerID" "L21_Shout_SpiritGuardians_Gimeitaro"
data "ContainerSpells" ""
data "SpellProperties" "ApplyStatus(SPIRIT_GUARDIANS_RADIANT_AURA,100,10)"
data "Description" "[HANDLE];1"
data "ExtraDescription" "[HANDLE];1"
data "ExtraDescriptionParams" "DealDamage(3d8,Radiant)"
data "TooltipDamageList" "DealDamage(3d8,Radiant)"
data "TooltipStatusApply" "ApplyStatus(SPIRIT_GUARDIANS_RADIANT_AURA,100,10)"
data "UseCosts" ""
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsConcentration;IsSpell;IsHarmful"
data "DamageType" "Radiant"

new entry "L21_Shout_SpiritGuardians_Gimeitaro_Necrotic"
type "SpellData"
data "SpellType" "Shout"
using "Shout_SpiritGuardians"
data "SpellContainerID" "L21_Shout_SpiritGuardians_Gimeitaro"
data "ContainerSpells" ""
data "SpellProperties" "ApplyStatus(SPIRIT_GUARDIANS_NECROTIC_AURA,100,10)"
data "Description" "[HANDLE];1"
data "ExtraDescription" "[HANDLE];1"
data "ExtraDescriptionParams" "DealDamage(3d8,Necrotic)"
data "TooltipDamageList" "DealDamage(3d8,Necrotic)"
data "TooltipStatusApply" "ApplyStatus(SPIRIT_GUARDIANS_NECROTIC_AURA,100,10)"
data "UseCosts" ""
data "SpellFlags" "HasVerbalComponent;HasSomaticComponent;IsConcentration;IsSpell;IsHarmful"
data "DamageType" "Necrotic"
```

**Note:** Will need 5 new handles for localization (1 main spell name + description, 2 radiant descriptions, 2 necrotic descriptions)

**2. Weapon.txt Updates:**

**a) Rename Shield Spell Reference:**
- Change: `UnlockSpell(L21_Target_GimeitarosShield_ShortRest)` → `UnlockSpell(L21_Target_GimeitarosShield_Unlimited)`

**b) Add Skill Check, Ability Check, Initiative, and Saving Throw Bonuses:**

Current Boosts line:
```
data "Boosts" "UnlockSpell(L21_Target_Light_Unlimited);UnlockInterrupt(L21_Interrupt_Counterspell_Unlimited);UnlockSpell(L21_Shout_CelestialHaste_Unlimited);UnlockSpell(Shout_MAG_TheChromatic_ChromaticAttunement);UnlockSpell(Shout_MAG_SpellSlotRestoration);UnlockSpell(Shout_MAG_SpellSlotRestoration_PearlOfPower);UnlockInterrupt(L21_Interrupt_Shield_Unlimited);UnlockSpell(L21_Projectile_GimeitarosBlast_ShortRest);UnlockSpell(L21_Target_GimeitarosTeleport_ShortRest);UnlockSpell(L21_Projectile_GimeitarosBarrage_Unlimited);UnlockSpell(L21_Target_GimeitarosShield_ShortRest);UnlockSpell(L21_Projectile_ChromaticOrb_Unlimited);UnlockSpell(L21_Teleportation_ArcaneGate_ShortRest);UnlockSpell(L21_Target_Knock_Unlimited)"
```

Target Boosts line:
```
data "Boosts" "UnlockSpell(L21_Target_Light_Unlimited);UnlockInterrupt(L21_Interrupt_Counterspell_Unlimited);UnlockSpell(L21_Shout_CelestialHaste_Unlimited);UnlockSpell(Shout_MAG_TheChromatic_ChromaticAttunement);UnlockSpell(Shout_MAG_SpellSlotRestoration);UnlockSpell(Shout_MAG_SpellSlotRestoration_PearlOfPower);UnlockInterrupt(L21_Interrupt_Shield_Unlimited);UnlockSpell(L21_Projectile_GimeitarosBlast_ShortRest);UnlockSpell(L21_Target_GimeitarosTeleport_ShortRest);UnlockSpell(L21_Projectile_GimeitarosBarrage_Unlimited);UnlockSpell(L21_Target_GimeitarosShield_Unlimited);UnlockSpell(L21_Projectile_ChromaticOrb_Unlimited);UnlockSpell(L21_Teleportation_ArcaneGate_ShortRest);UnlockSpell(L21_Target_Knock_Unlimited);UnlockSpell(L21_Shout_SpiritGuardians_Gimeitaro,AddChildren,,,SpellCastingAbility);RollBonus(SkillCheck,10);RollBonus(RawAbility,10,Strength);RollBonus(RawAbility,10,Dexterity);RollBonus(RawAbility,10,Constitution);RollBonus(RawAbility,10,Intelligence);RollBonus(RawAbility,10,Wisdom);RollBonus(RawAbility,10,Charisma);Initiative(7);RollBonus(SavingThrow,8)"
```

Changes:
- Replace `L21_Target_GimeitarosShield_ShortRest` with `L21_Target_GimeitarosShield_Unlimited`
- Add `UnlockSpell(L21_Shout_SpiritGuardians_Gimeitaro,AddChildren,,,SpellCastingAbility)` - grants Spirit Guardians
- Add `RollBonus(SkillCheck,10)` - grants +10 to all skill checks
- Add `RollBonus(RawAbility,10,Strength)` - grants +10 to raw Strength checks
- Add `RollBonus(RawAbility,10,Dexterity)` - grants +10 to raw Dexterity checks
- Add `RollBonus(RawAbility,10,Constitution)` - grants +10 to raw Constitution checks
- Add `RollBonus(RawAbility,10,Intelligence)` - grants +10 to raw Intelligence checks
- Add `RollBonus(RawAbility,10,Wisdom)` - grants +10 to raw Wisdom checks
- Add `RollBonus(RawAbility,10,Charisma)` - grants +10 to raw Charisma checks
- Add `Initiative(7)` - grants +7 to initiative rolls
- Add `RollBonus(SavingThrow,8)` - grants +8 to all saving throws

Effect:
- **Spirit Guardians**: Free action concentration spell, 3m aura dealing 3d8 Radiant or Necrotic damage to nearby enemies, unlimited casts
- **Skill Checks**: +10 bonus to ALL skill checks (all 18 skills: Acrobatics, Animal Handling, Arcana, Athletics, Deception, History, Insight, Intimidation, Investigation, Medicine, Nature, Perception, Performance, Persuasion, Religion, Sleight of Hand, Stealth, Survival)
- **Raw Ability Checks**: +10 bonus to raw ability checks (checks without proficiency, such as breaking down doors with Strength, resisting effects, etc.)
- **Initiative**: +7 bonus to initiative rolls (act earlier in combat)
- **Saving Throws**: +8 bonus to ALL saving throws (Strength, Dexterity, Constitution, Intelligence, Wisdom, Charisma)

**Localization Updates:**

Staff description (english.xml) should be updated to mention all bonuses and Spirit Guardians:
```xml
<content contentuid="hb514d87agf785g4f45g8c93g4827fb5d7f3f" version="1">A quarterstaff crackling with arcane energy. Grants +10 to all skill checks and ability checks, +7 to initiative, +8 to saving throws, Lightning Charges when casting spells at close range, Chromatic Attunement, Arcane Enchantment, Arcane Battery, Spell Slot Restoration, Pearlescent Restoration, Mystra's Grace, Weave's Reclamation, Echoes of Netheril, unlimited Light, unlimited Shield and Counterspell reactions, Celestial Haste (free action), Spirit Guardians (free action, unlimited), Gimeitaro's Blast, Gimeitaro's Teleport, Gimeitaro's Barrage, and Gimeitaro's Shield (unlimited Silvered Bulwark).</content>
```

Spirit Guardians localization entries (5 new handles needed):
```xml
<content contentuid="[HANDLE1]" version="1">Gimeitaro's Spirit Guardians</content>
<content contentuid="[HANDLE2]" version="1">Call forth spirits to protect you. Nearby enemies take 3d8 Radiant or Necrotic damage. Unlimited casting, free action.</content>
<content contentuid="[HANDLE3]" version="1">Radiant spirits surround you.</content>
<content contentuid="[HANDLE4]" version="1">Necrotic spirits surround you.</content>
```

**Benefits:**
1. **Mobile Protection** - Silvered Bulwark follows the target, allowing movement during invulnerability
2. **Unlimited Silvered Bulwark** - Can be cast as many times as needed (concentration limits simultaneous effects)
3. **Free Action Buffs** - Celestial Haste AND Spirit Guardians both free action (instant combat prep)
4. **Area Damage** - Spirit Guardians deals 3d8 damage per turn to all nearby enemies automatically
5. **Complete Mastery** - +10 to all skill checks and raw ability checks (excels at everything)
6. **Combat Superiority** - +7 initiative (act first) and +8 saving throws (resist effects easily)
7. **Improved Utility** - Better protection, faster buffing, enhanced skills, better saves, AoE damage
5. **Improved Utility** - Better protection, faster buffing, enhanced skills and abilities
6. **Better Tactical Options** - More flexibility in combat and exploration

**Implementation Complete:**

**Files Updated:**
- ✓ `Spell_Target.txt` - Gimeitaro's Shield renamed to Unlimited, Cooldown removed
- ✓ `Spell_Shout.txt` - Celestial Haste changed to free action (UseCosts ""), Spirit Guardians added (3 spell entries)
- ✓ `Weapon.txt` - All boosts updated: renamed shield spell, added Spirit Guardians unlock, added 9 stat bonuses
- ✓ `english.xml` - Staff description updated, Silvered Bulwark description updated, 4 Spirit Guardians entries added
- ✓ `docs/level21gear/item_catalog.md` - Updated with all Revision 2 enhancements
- ✓ `docs/instructions/uuid_workflow.md` - Removed 5 used UUIDs, added Phase 054 R2 note

**UUID Allocation (Revision 2):**
Converted 5 UUIDs from pool to handles for Spirit Guardians:
1. Main spell DisplayName: h2971301fgd552g4a72g8d84g126e51811bc4
2. Main spell Description: h0da4a14fg00f4g40a0gb0a2g826e58cf044e
3. Radiant ExtraDescription: h1857d276gb362g40b6ga438g9205fdf6c3af
4. Necrotic ExtraDescription: he9685b00g394dg4b9cgbbc9g1868de4de69e
5. (Note: Only 4 handles needed, 5th UUID not used)

**Status:** COMPLETE - Silvered Bulwark unlimited, free action Haste, free action Spirit Guardians, comprehensive stat bonuses implemented

---

---

### Revision 3: Fix Localization Handles with ed21 Prefix

**Issue:**
Game loads and staff appears in chest, but all names show as "Not found". Localization handles are not being recognized by BG3.

**Root Cause:**
The handles were created by converting UUIDs directly to handle format WITHOUT first changing the UUID prefix to `ed21`. According to uuid_workflow.md, the correct process is:
1. Take UUID from pool (e.g., `8054ad1d-1aea-4b70-b63f-eabb5fb10181`)
2. Change first 4 chars to `ed21` (e.g., `ed21ad1d-1aea-4b70-b63f-eabb5fb10181`)
3. Convert to handle format (e.g., `hed21ad1dg1aeag4b70gb63fgeabb5fb10181`)

But Revision 1 skipped step 2, creating handles like `h8054ad1dg1aeag4b70gb63fgeabb5fb10181` instead of `hed21ad1dg1aeag4b70gb63fgeabb5fb10181`.

**Solution:**
Update all 18 handles (from Revision 1) and 4 Spirit Guardians handles (from Revision 2) to use the `ed21` prefix pattern, matching the Level13PlusGear convention.

**Affected Files:**
- RootTemplate (2 handles): DisplayName, Description
- Spell files (16 handles): Various spell names and descriptions
- Spirit Guardians (4 handles): Main spell + variants
- Localization file: All 22 handles need ed21 prefix

**Corrected Handles:**

| Original Handle (Wrong) | Corrected Handle (ed21 prefix) |
|------------------------|-------------------------------|
| h8054ad1dg1aeag4b70gb63fgeabb5fb10181 | hed21ad1dg1aeag4b70gb63fgeabb5fb10181 |
| hb514d87agf785g4f45g8c93g4827fb5d7f3f | hed214d87agf785g4f45g8c93g4827fb5d7f3f |
| h623f3f43gc3e3g4811g866dg2c78072bc69a | hed213f43gc3e3g4811g866dg2c78072bc69a |
| h81c15d59gc758g4b66g96c9gded4998d6a9f | hed215d59gc758g4b66g96c9gded4998d6a9f |
| hed73d5c7g1c7cg4ed2gbc7eged6b4d454460 | hed213d5c7g1c7cg4ed2gbc7eged6b4d454460 |
| h41f5f4a4gc036g4db2g9763g51e01ba28887 | hed215f4a4gc036g4db2g9763g51e01ba28887 |
| h57a21a18g4d37g4935g926cg8ea8169f84f6 | hed211a18g4d37g4935g926cg8ea8169f84f6 |
| h7eec854fgb997g466fg8a74g59e5d6e6e978 | hed21c854fgb997g466fg8a74g59e5d6e6e978 |
| h80380ea8g80a2g4a71g8269g3c7d26dd91a5 | hed210ea8g80a2g4a71g8269g3c7d26dd91a5 |
| h3e018fbcgf4a3g440egb169gc938dfde49f5 | hed218fbcgf4a3g440egb169gc938dfde49f5 |
| h6b3e5669g8780g4a36g8e55gf59f22b5ebfa | hed215669g8780g4a36g8e55gf59f22b5ebfa |
| had00001aga204g4af5g9f9cg2703b9654ec0 | hed210001aga204g4af5g9f9cg2703b9654ec0 |
| hc56fc6ebg7b46g4739g96e5g4f896829c10c | hed21c6ebg7b46g4739g96e5g4f896829c10c |
| haaf7657agcc38g445cgb1e8g8c8a93d1f648 | hed217657agcc38g445cgb1e8g8c8a93d1f648 |
| h49fe5773g5cdeg4791g9668g7f67f1bb9d1c | hed215773g5cdeg4791g9668g7f67f1bb9d1c |
| h06b70227g4bcbg4ed6ga3b9ga458a9bf9e31 | hed210227g4bcbg4ed6ga3b9ga458a9bf9e31 |
| h023d53c4g351dg47ecgb7ebg32765783d8d3 | hed2153c4g351dg47ecgb7ebg32765783d8d3 |
| hbc94a0beg96afg4c71ga16dg86741886005e | hed21a0beg96afg4c71ga16dg86741886005e |
| h2971301fgd552g4a72g8d84g126e51811bc4 | hed21301fgd552g4a72g8d84g126e51811bc4 |
| h0da4a14fg00f4g40a0gb0a2g826e58cf044e | hed21a14fg00f4g40a0gb0a2g826e58cf044e |
| h1857d276gb362g40b6ga438g9205fdf6c3af | hed21d276gb362g40b6ga438g9205fdf6c3af |
| he9685b00g394dg4b9cgbbc9g1868de4de69e | hed215b00g394dg4b9cgbbc9g1868de4de69e |

**Implementation Complete:**

**Initial Fix (Handles):**
All 22 handles were corrected across all files using batch sed replacements to use ed21 prefix.

**Files Updated (Handle Fix):**
1. **L21_Staff_Gimeitaro.lsf.lsx** - Updated 2 handles (DisplayName, Description)
2. **Spell_Target.txt** - Updated 6 handles (Knock, GimeitarosTeleport, GimeitarosShield)
3. **Spell_Projectile.txt** - Updated 4 handles (GimeitarosBlast, GimeitarosBarrage)
4. **Spell_Shout.txt** - Updated 4 handles (Spirit Guardians main + variants)
5. **Interrupt.txt** - Updated 4 handles (Shield, Counterspell)
6. **Spell_Teleportation.txt** - Updated 2 handles (Arcane Gate)
7. **Level21Gear.loca.xml** - Updated all 22 handles to match

**Second Fix (Directory Structure):**
After user testing, discovered the localization file was in the wrong directory location.

**Root Cause:** Localization file was incorrectly placed at:
- `Level21Gear/Public/Level21Gear/Localization/English/Level21Gear.loca.xml` ❌

**Correct Location:** Must be at mod root, not inside Public folder:
- `Level21Gear/Localization/English/Level21Gear.loca.xml` ✓

**Action Taken:**
- Moved `Level21Gear.loca.xml` from `Public/Level21Gear/Localization/` to `Localization/` at mod root
- Removed empty old directories

**Result:** All item and spell names/descriptions should now display correctly in-game.

**Status:** COMPLETE - Handles corrected AND file moved to proper location

---

## Phase 054 Status: COMPLETE ✓

**Final Implementation:**
- ✓ Level21Gear mod created with complete directory structure
- ✓ Staff of Gimeitaro implemented with L21 prefix
- ✓ All 11 custom spells copied with L21 prefix
- ✓ Tutorial Chest delivery configured via TreasureTable
- ✓ Complete documentation created
- ✓ CLAUDE.md updated with new mod
- ✓ All three revisions completed and tested
- ✓ Localization working correctly

**User Testing Complete:**
- ✓ Mod loads in BG3
- ✓ Staff of Gimeitaro appears in Tutorial Chest
- ✓ All names and descriptions display correctly
- ✓ All enhancements working (Silvered Bulwark unlimited, free action Haste/Spirit Guardians, +10 skill/ability checks, +7 initiative, +8 saves)

---
