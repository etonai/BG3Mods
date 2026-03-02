# Phase 059: Rename to ForbiddenScrolls + Add Hellfire Orb Scroll

**Status:** COMPLETE
**Date:** 2026-02-22

---

## Goals

1. **Rename mod:** Rename `SilveredBulwarkScroll` to `ForbiddenScrolls` — all directories, internal folder names, metadata, and item/spell prefixes (`SBS_` → `FBS_`). UUID prefix (`ed58`) stays unchanged.
2. **Add Scroll of Hellfire Orb:** A new scroll that casts the vanilla Death Knight spell `Projectile_HellfireOrb_DeathKnight` (20d6 fire AoE, DC 18 Dex save, no spell slot, once per combat). Delivered via Tutorial Chest, not unique.

---

## Summary of Changes

| Item | From | To |
|------|------|----|
| Mod root directory | `SilveredBulwarkScroll/` | `ForbiddenScrolls/` |
| Mod folder (Mods/) | `Mods/SilveredBulwarkScroll/` | `Mods/ForbiddenScrolls/` |
| Public folder | `Public/SilveredBulwarkScroll/` | `Public/ForbiddenScrolls/` |
| Localization file | `SilveredBulwarkScroll.loca.xml` | `ForbiddenScrolls.loca.xml` |
| meta.lsx `Folder` | `SilveredBulwarkScroll` | `ForbiddenScrolls` |
| meta.lsx `Name` | `Silvered Bulwark Scroll` | `Forbidden Scrolls` |
| meta.lsx `Description` | (single-scroll desc) | (updated for multi-scroll mod) |
| Item/spell prefix | `SBS_` | `FBS_` |
| Docs directory | `docs/silveredbulwarkscroll/` | `docs/forbiddenscrolls/` |
| UUID prefix | `ed58` (unchanged) | `ed58` (unchanged) |

---

## Design Decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| UUID prefix change | **No** — keep `ed58` | Avoids invalidating any existing saves using the mod; user confirmed |
| Item/spell prefix change | **Yes** — `SBS_` → `FBS_` | Matches the new mod name `ForbiddenScrolls` |
| Hellfire Orb spell entry | **Vanilla** (`Projectile_HellfireOrb_DeathKnight`) | No custom spell stats needed; the vanilla spell is the correct one |
| Hellfire Orb scroll unique | **No** | Consistent with Silvered Bulwark scroll; consumable items |
| Delivery | Tutorial Chest (`TUT_Chest_Potions`) | Consistent with existing mod pattern |
| Rarity | VeryRare | 20d6 fire AoE with no spell slot is extremely powerful |

---

## Implementation Plan

### Task 1: Rename Directories

Rename (using git mv to preserve history):
- `SilveredBulwarkScroll/` → `ForbiddenScrolls/`
- `ForbiddenScrolls/Mods/SilveredBulwarkScroll/` → `ForbiddenScrolls/Mods/ForbiddenScrolls/`
- `ForbiddenScrolls/Public/SilveredBulwarkScroll/` → `ForbiddenScrolls/Public/ForbiddenScrolls/`
- `ForbiddenScrolls/Localization/English/SilveredBulwarkScroll.loca.xml` → `ForbiddenScrolls/Localization/English/ForbiddenScrolls.loca.xml`
- `ForbiddenScrolls/Public/ForbiddenScrolls/RootTemplates/SBS_Scroll_SilveredBulwark.lsf.lsx` → `ForbiddenScrolls/Public/ForbiddenScrolls/RootTemplates/FBS_Scroll_SilveredBulwark.lsf.lsx`
- `docs/silveredbulwarkscroll/` → `docs/forbiddenscrolls/`

### Task 2: Update meta.lsx

**File:** `ForbiddenScrolls/Mods/ForbiddenScrolls/meta.lsx`

Update:
- `Folder`: `SilveredBulwarkScroll` → `ForbiddenScrolls`
- `Name`: `Silvered Bulwark Scroll` → `Forbidden Scrolls`
- `Description`: Update to describe a multi-scroll mod

### Task 3: Update Spell Stats (SBS_ → FBS_)

**File:** `ForbiddenScrolls/Public/ForbiddenScrolls/Stats/Generated/Data/Spell_Target.txt`

Rename entry: `SBS_Target_SilveredBulwark` → `FBS_Target_SilveredBulwark`

### Task 4: Update Object Stats (SBS_ → FBS_)

**File:** `ForbiddenScrolls/Public/ForbiddenScrolls/Stats/Generated/Data/Object.txt`

Rename entry: `OBJ_SBS_Scroll_SilveredBulwark` → `OBJ_FBS_Scroll_SilveredBulwark`

Also add the new Hellfire Orb scroll entry `OBJ_FBS_Scroll_HellfireOrb`.

### Task 5: Update TreasureTable

**File:** `ForbiddenScrolls/Public/ForbiddenScrolls/Stats/Generated/TreasureTable.txt`

Update existing reference: `I_OBJ_SBS_Scroll_SilveredBulwark` → `I_OBJ_FBS_Scroll_SilveredBulwark`

Add new entry for Hellfire Orb scroll.

### Task 6: Update Silvered Bulwark RootTemplate

**File:** `ForbiddenScrolls/Public/ForbiddenScrolls/RootTemplates/FBS_Scroll_SilveredBulwark.lsf.lsx`

Update:
- `Name` attribute: `SBS_Scroll_SilveredBulwark` → `FBS_Scroll_SilveredBulwark`
- `Stats` attribute: `OBJ_SBS_Scroll_SilveredBulwark` → `OBJ_FBS_Scroll_SilveredBulwark`
- `SkillID` in ActionType 12: `SBS_Target_SilveredBulwark` → `FBS_Target_SilveredBulwark`
- `SpellId` in ActionType 33: `SBS_Target_SilveredBulwark` → `FBS_Target_SilveredBulwark`

### Task 7: Create Hellfire Orb RootTemplate

**New file:** `ForbiddenScrolls/Public/ForbiddenScrolls/RootTemplates/FBS_Scroll_HellfireOrb.lsf.lsx`

Uses vanilla spell `Projectile_HellfireOrb_DeathKnight` in `OnUsePeaceActions`. No custom spell stats entry is needed.

### Task 8: Update Localization

**File:** `ForbiddenScrolls/Localization/English/ForbiddenScrolls.loca.xml`

Add two new handles for the Hellfire Orb scroll name and description.

### Task 9: Update Documentation

- `CLAUDE.md`: Update mod name `SilveredBulwarkScroll` → `ForbiddenScrolls`; update docs path
- `docs/forbiddenscrolls/item_catalog.md`: Rename file (was `docs/silveredbulwarkscroll/item_catalog.md`), add Hellfire Orb scroll entry
- `docs/instructions/uuid_workflow.md`: Delete 3 used UUIDs, add usage note

---

## Detailed Implementation

### Step 1: Rename All Directories

Using git mv:
```bash
git mv SilveredBulwarkScroll ForbiddenScrolls
git mv ForbiddenScrolls/Mods/SilveredBulwarkScroll ForbiddenScrolls/Mods/ForbiddenScrolls
git mv ForbiddenScrolls/Public/SilveredBulwarkScroll ForbiddenScrolls/Public/ForbiddenScrolls
git mv "ForbiddenScrolls/Localization/English/SilveredBulwarkScroll.loca.xml" "ForbiddenScrolls/Localization/English/ForbiddenScrolls.loca.xml"
git mv "ForbiddenScrolls/Public/ForbiddenScrolls/RootTemplates/SBS_Scroll_SilveredBulwark.lsf.lsx" "ForbiddenScrolls/Public/ForbiddenScrolls/RootTemplates/FBS_Scroll_SilveredBulwark.lsf.lsx"
git mv docs/silveredbulwarkscroll docs/forbiddenscrolls
```

### Step 2: Update meta.lsx

**File:** `ForbiddenScrolls/Mods/ForbiddenScrolls/meta.lsx`

```xml
<attribute id="Description" type="LSString" value="A collection of powerful forbidden spell scrolls." />
<attribute id="Folder" type="LSString" value="ForbiddenScrolls" />
<attribute id="Name" type="LSString" value="Forbidden Scrolls" />
```

### Step 3: Update Spell_Target.txt (SBS_ → FBS_)

**File:** `ForbiddenScrolls/Public/ForbiddenScrolls/Stats/Generated/Data/Spell_Target.txt`

Change entry name from `SBS_Target_SilveredBulwark` to `FBS_Target_SilveredBulwark`.

### Step 4: Update Object.txt (SBS_ → FBS_, add Hellfire Orb)

**File:** `ForbiddenScrolls/Public/ForbiddenScrolls/Stats/Generated/Data/Object.txt`

Change existing entry name from `OBJ_SBS_Scroll_SilveredBulwark` to `OBJ_FBS_Scroll_SilveredBulwark`.

Add new entry at end of file:
```
new entry "OBJ_FBS_Scroll_HellfireOrb"
type "Object"
using "_MagicScroll"
data "RootTemplate" "ed5856e4-08e5-48ee-a20b-d240c0c6ad5b"
data "DisplayName" "hed58a6d6g21b9g42e9gb5e2g6bf596e8db73;1"
data "Description" "hed58f9e8g3824g4bf9gbec5g17d2943539be;1"
data "ValueLevel" "6"
data "Rarity" "VeryRare"
data "Priority" "1"
```

### Step 5: Update TreasureTable.txt

**File:** `ForbiddenScrolls/Public/ForbiddenScrolls/Stats/Generated/TreasureTable.txt`

```
new treasuretable "TUT_Chest_Potions"
 CanMerge 1
new subtable "1,1"
object category "I_OBJ_FBS_Scroll_SilveredBulwark",1,0,0,0,0,0,0,0
new subtable "1,1"
object category "I_OBJ_FBS_Scroll_HellfireOrb",1,0,0,0,0,0,0,0
```

### Step 6: Update FBS_Scroll_SilveredBulwark.lsf.lsx

**File:** `ForbiddenScrolls/Public/ForbiddenScrolls/RootTemplates/FBS_Scroll_SilveredBulwark.lsf.lsx`

Update these four values (UUID/handles are unchanged):
- `Name`: `SBS_Scroll_SilveredBulwark` → `FBS_Scroll_SilveredBulwark`
- `Stats`: `OBJ_SBS_Scroll_SilveredBulwark` → `OBJ_FBS_Scroll_SilveredBulwark`
- `SkillID` (ActionType 12): `SBS_Target_SilveredBulwark` → `FBS_Target_SilveredBulwark`
- `SpellId` (ActionType 33): `SBS_Target_SilveredBulwark` → `FBS_Target_SilveredBulwark`

### Step 7: Create FBS_Scroll_HellfireOrb.lsf.lsx

**New file:** `ForbiddenScrolls/Public/ForbiddenScrolls/RootTemplates/FBS_Scroll_HellfireOrb.lsf.lsx`

```xml
<?xml version="1.0" encoding="utf-8"?>
<save>
    <version major="4" minor="0" revision="6" build="5" lslib_meta="v1,bswap_guids" />
    <region id="Templates">
        <node id="Templates">
            <children>
                <node id="GameObjects">
                    <attribute id="Description" type="TranslatedString" handle="hed58f9e8g3824g4bf9gbec5g17d2943539be" version="1" />
                    <attribute id="DisplayName" type="TranslatedString" handle="hed58a6d6g21b9g42e9gb5e2g6bf596e8db73" version="1" />
                    <attribute id="LevelName" type="FixedString" value="" />
                    <attribute id="MapKey" type="FixedString" value="ed5856e4-08e5-48ee-a20b-d240c0c6ad5b" />
                    <attribute id="Name" type="LSString" value="FBS_Scroll_HellfireOrb" />
                    <attribute id="ParentTemplateId" type="FixedString" value="4ffd5c4b-4c56-4f05-a228-a33754bb1806" />
                    <attribute id="Stats" type="FixedString" value="OBJ_FBS_Scroll_HellfireOrb" />
                    <attribute id="Type" type="FixedString" value="item" />
                    <attribute id="_OriginalFileVersion_" type="int64" value="144115188075855912" />
                    <children>
                        <node id="GameMaster" />
                        <node id="OnUsePeaceActions">
                            <children>
                                <node id="Action">
                                    <attribute id="ActionType" type="int32" value="12" />
                                    <children>
                                        <node id="Attributes">
                                            <attribute id="Animation" type="FixedString" value="" />
                                            <attribute id="ClassId" type="guid" value="a865965f-501b-46e9-9eaa-7748e8c04d09" />
                                            <attribute id="Conditions" type="LSString" value="" />
                                            <attribute id="Consume" type="bool" value="True" />
                                            <attribute id="SkillID" type="FixedString" value="Projectile_HellfireOrb_DeathKnight" />
                                        </node>
                                    </children>
                                </node>
                                <node id="Action">
                                    <attribute id="ActionType" type="int32" value="33" />
                                    <children>
                                        <node id="Attributes">
                                            <attribute id="Animation" type="FixedString" value="" />
                                            <attribute id="Conditions" type="LSString" value="" />
                                            <attribute id="Consume" type="bool" value="True" />
                                            <attribute id="SpellId" type="FixedString" value="Projectile_HellfireOrb_DeathKnight" />
                                        </node>
                                    </children>
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

### Step 8: Update Localization

**File:** `ForbiddenScrolls/Localization/English/ForbiddenScrolls.loca.xml`

Add two new entries for the Hellfire Orb scroll (existing Silvered Bulwark handles are unchanged):

```xml
<!-- Hellfire Orb Scroll -->
<content contentuid="hed58a6d6g21b9g42e9gb5e2g6bf596e8db73" version="1">Scroll of Hellfire Orb</content>
<content contentuid="hed58f9e8g3824g4bf9gbec5g17d2943539be" version="1">A scroll inscribed with the Hellfire Orb incantation. Launches a searing orb that explodes in a 4-metre radius, dealing 20d6 Fire damage. DC 18 Dexterity saving throw for half damage. Single use.</content>
```

---

## Files to Modify/Create

| File | Action | Description |
|------|--------|-------------|
| `SilveredBulwarkScroll/` (entire dir) | Rename to `ForbiddenScrolls/` | Root mod directory |
| `Mods/SilveredBulwarkScroll/` | Rename to `Mods/ForbiddenScrolls/` | BG3 mod folder name |
| `Public/SilveredBulwarkScroll/` | Rename to `Public/ForbiddenScrolls/` | Public data folder |
| `Localization/English/SilveredBulwarkScroll.loca.xml` | Rename to `ForbiddenScrolls.loca.xml` + Edit | Add Hellfire Orb handles |
| `Mods/ForbiddenScrolls/meta.lsx` | Edit | Update `Folder`, `Name`, `Description` |
| `Stats/Generated/Data/Spell_Target.txt` | Edit | Rename `SBS_Target_SilveredBulwark` → `FBS_Target_SilveredBulwark` |
| `Stats/Generated/Data/Object.txt` | Edit | Rename existing entry; add `OBJ_FBS_Scroll_HellfireOrb` |
| `Stats/Generated/TreasureTable.txt` | Edit | Update SBS ref; add Hellfire Orb entry |
| `RootTemplates/SBS_Scroll_SilveredBulwark.lsf.lsx` | Rename to `FBS_...` + Edit | Update Name, Stats, SkillID, SpellId |
| `RootTemplates/FBS_Scroll_HellfireOrb.lsf.lsx` | Create | New scroll RootTemplate |
| `docs/silveredbulwarkscroll/` | Rename to `docs/forbiddenscrolls/` | Docs directory |
| `docs/forbiddenscrolls/item_catalog.md` | Edit | Add Hellfire Orb scroll entry |
| `CLAUDE.md` | Edit | Update mod name and docs path |
| `docs/instructions/uuid_workflow.md` | Edit | Delete 3 used UUIDs; add usage note |

---

## UUID/Handle Requirements

### UUID Convention

ForbiddenScrolls uses the **`ed58`** UUID prefix (unchanged from Phase 058). Take UUIDs from the pool in `docs/instructions/uuid_workflow.md`, replace the first 4 characters with `ed58`.

**Handle format:** `h` + UUID with `-` replaced by `g`

### UUIDs Needed for Phase 059

No new UUIDs are needed for the rename — existing content UUIDs and handles stay the same.

For the Hellfire Orb scroll:

| Purpose | Count |
|---------|-------|
| Scroll RootTemplate UUID | 1 |
| Scroll DisplayName handle | 1 |
| Scroll Description handle | 1 |
| **Total** | **3** |

### UUID Allocation

| Purpose | Type | Value |
|---------|------|-------|
| Scroll RootTemplate (`FBS_Scroll_HellfireOrb`) | UUID | `ed5856e4-08e5-48ee-a20b-d240c0c6ad5b` |
| Scroll DisplayName | Handle | `hed58a6d6g21b9g42e9gb5e2g6bf596e8db73` |
| Scroll Description | Handle | `hed58f9e8g3824g4bf9gbec5g17d2943539be` |

**Pool UUIDs consumed (delete these from `uuid_workflow.md`):**
```
d44f56e4-08e5-48ee-a20b-d240c0c6ad5b
ac9ca6d6-21b9-42e9-b5e2-6bf596e8db73
4c31f9e8-3824-4bf9-bec5-17d2943539be
```

---

## Testing Plan

### Test 1: Mod Loads Under New Name
1. Enable the `ForbiddenScrolls` mod in BG3.
2. Start a new game.
3. **Verify:** No load errors.
4. **Verify:** Mod appears as "Forbidden Scrolls" in the mod list.

### Test 2: Silvered Bulwark Scroll Still Works
1. Open the Tutorial Chest.
2. **Verify:** "Scroll of Silvered Bulwark" is present.
3. Use the scroll on an ally.
4. **Verify:** It casts Silvered Bulwark correctly (invulnerability + advantage on saves).
5. **Verify:** The scroll is consumed.

### Test 3: Hellfire Orb Scroll in Chest
1. Open the Tutorial Chest.
2. **Verify:** "Scroll of Hellfire Orb" is present.
3. **Verify:** The scroll has the correct name and description.

### Test 4: Hellfire Orb Scroll Casts Correctly
1. Use the Scroll of Hellfire Orb in combat.
2. **Verify:** The scroll is consumed after use.
3. **Verify:** A fireball-style projectile launches and explodes in ~4m radius.
4. **Verify:** Enemies take heavy fire damage (should be in the 20d6 range).
5. **Verify:** The spell has a once-per-combat cooldown after the scroll is used (note: this is a property of the spell, not the scroll — scroll is single-use anyway).

---

## Technical Notes

### No Custom Spell Entry for Hellfire Orb
Unlike the Silvered Bulwark scroll (which needs a custom spell because the vanilla Nightsong spell isn't player-accessible via stats), the Hellfire Orb scroll references the vanilla `Projectile_HellfireOrb_DeathKnight` directly in `OnUsePeaceActions`. No `Spell_Projectile.txt` entry needed in this mod.

### Vanilla Spell Location
`Projectile_HellfireOrb_DeathKnight` is defined in:
`VanillaBG3/Shared/Public/SharedDev/Stats/Generated/Data/Spell_Projectile.txt`

It uses `Projectile_Fireball` as base with DC 18 Dex save and 20d6 fire damage.

### Scroll RootTemplate Pattern
Use the same verified pattern from Phase 057/058:
- `ParentTemplateId`: `4ffd5c4b-4c56-4f05-a228-a33754bb1806` (generic scroll base)
- ActionType 12 (`SkillID`) + ActionType 33 (`SpellId`) both set to the spell name

### Rename Does Not Break Existing Saves
The mod UUID (`ed58126e-8531-43ce-93f2-8b4b49354e12`) and all content UUIDs are unchanged. Renaming directories and item/spell stat names is a breaking change for any saves that already have the scroll in inventory (the `OBJ_SBS_Scroll_SilveredBulwark` stat no longer exists), but since Phase 058 is still IMPLEMENTED (not yet user-tested in a real save), this is acceptable.

---

## Dependencies

**This phase depends on:**
- Phase 058 (IMPLEMENTED) — SilveredBulwarkScroll mod created; this phase renames and extends it.

---

## Success Criteria

- [ ] All directories renamed correctly (`SilveredBulwarkScroll` → `ForbiddenScrolls`)
- [ ] All `SBS_` stat/spell/template names updated to `FBS_`
- [ ] meta.lsx updated with new folder name, mod name, and description
- [ ] `FBS_Scroll_HellfireOrb.lsf.lsx` created with correct UUID and `OnUsePeaceActions`
- [ ] `OBJ_FBS_Scroll_HellfireOrb` added to Object.txt
- [ ] TreasureTable updated with both FBS scroll entries
- [ ] Localization file renamed and updated with Hellfire Orb handles
- [ ] 3 UUIDs consumed and deleted from `uuid_workflow.md`
- [ ] CLAUDE.md updated
- [ ] Both scrolls appear in Tutorial Chest in-game
- [ ] Silvered Bulwark scroll still casts correctly
- [ ] Hellfire Orb scroll casts correctly (large fire AoE)
- [ ] User-tested and confirmed

---

## Related Documentation

- **`docs/forbiddenscrolls/item_catalog.md`** — Item catalog for this mod (renamed from silveredbulwarkscroll)
- **`docs/instructions/uuid_workflow.md`** — UUID pool; use `ed58` prefix
- **`docs/instructions/interesting_magical_effects.md`** — Hellfire Orb spell details; custom scroll RootTemplate pattern
- **`docs/phases/Phase058.md`** — Original SilveredBulwarkScroll mod creation

---

## Phase 059 Status: COMPLETE
