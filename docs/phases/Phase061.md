# Phase 061: Rename ForbiddenScrolls Back to SilveredBulwarkScroll

**Status:** IMPLEMENTED
**Date:** 2026-02-23

---

## Goals

1. **Rename mod back:** Rename `ForbiddenScrolls` back to `SilveredBulwarkScroll` — all directories, internal folder names, and metadata.
2. **Update item/spell prefix:** Revert `FBS_` back to `SBS_` on all stat entries, RootTemplate names, and spell references, including the Hellfire Orb scroll added in Phase 059.
3. **Keep Hellfire Orb scroll:** The scroll remains in the mod, just renamed from `FBS_` to `SBS_`.

---

## Summary of Changes

| Item | From | To |
|------|------|----|
| Mod root directory | `ForbiddenScrolls/` | `SilveredBulwarkScroll/` |
| Mod folder (Mods/) | `Mods/ForbiddenScrolls/` | `Mods/SilveredBulwarkScroll/` |
| Public folder | `Public/ForbiddenScrolls/` | `Public/SilveredBulwarkScroll/` |
| Localization file | `ForbiddenScrolls.loca.xml` | `SilveredBulwarkScroll.loca.xml` |
| meta.lsx `Folder` | `ForbiddenScrolls` | `SilveredBulwarkScroll` |
| meta.lsx `Name` | `Forbidden Scrolls` | `Silvered Bulwark Scroll` |
| meta.lsx `Description` | (multi-scroll desc) | (updated) |
| Item/spell prefix | `FBS_` | `SBS_` |
| Docs directory | `docs/forbiddenscrolls/` | `docs/silveredbulwarkscroll/` |
| UUID prefix | `ed58` (unchanged) | `ed58` (unchanged) |

**Note:** The Hellfire Orb scroll remains in the mod. Its stats entry, RootTemplate, and localization handles all have their prefix updated from `FBS_` to `SBS_`.

---

## Files to Rename

| From | To |
|------|----|
| `ForbiddenScrolls/` | `SilveredBulwarkScroll/` |
| `Mods/ForbiddenScrolls/` | `Mods/SilveredBulwarkScroll/` |
| `Public/ForbiddenScrolls/` | `Public/SilveredBulwarkScroll/` |
| `Localization/English/ForbiddenScrolls.loca.xml` | `Localization/English/SilveredBulwarkScroll.loca.xml` |
| `RootTemplates/FBS_Scroll_SilveredBulwark.lsf.lsx` | `RootTemplates/SBS_Scroll_SilveredBulwark.lsf.lsx` |
| `RootTemplates/FBS_Scroll_HellfireOrb.lsf.lsx` | `RootTemplates/SBS_Scroll_HellfireOrb.lsf.lsx` |
| `docs/forbiddenscrolls/` | `docs/silveredbulwarkscroll/` |

---

## Files to Edit (Content Changes)

### meta.lsx
- `Folder`: `ForbiddenScrolls` → `SilveredBulwarkScroll`
- `Name`: `Forbidden Scrolls` → `Silvered Bulwark Scroll`
- `Description`: update to describe a multi-scroll mod under new name

### Spell_Target.txt
- Entry name: `FBS_Target_SilveredBulwark` → `SBS_Target_SilveredBulwark`

### Object.txt
- Entry names:
  - `OBJ_FBS_Scroll_SilveredBulwark` → `OBJ_SBS_Scroll_SilveredBulwark`
  - `OBJ_FBS_Scroll_HellfireOrb` → `OBJ_SBS_Scroll_HellfireOrb`

### TreasureTable.txt
- `I_OBJ_FBS_Scroll_SilveredBulwark` → `I_OBJ_SBS_Scroll_SilveredBulwark`
- `I_OBJ_FBS_Scroll_HellfireOrb` → `I_OBJ_SBS_Scroll_HellfireOrb`

### SBS_Scroll_SilveredBulwark.lsf.lsx (renamed from FBS_)
- `Name`: `FBS_Scroll_SilveredBulwark` → `SBS_Scroll_SilveredBulwark`
- `Stats`: `OBJ_FBS_Scroll_SilveredBulwark` → `OBJ_SBS_Scroll_SilveredBulwark`
- `SkillID` (ActionType 12): `FBS_Target_SilveredBulwark` → `SBS_Target_SilveredBulwark`
- `SpellId` (ActionType 33): `FBS_Target_SilveredBulwark` → `SBS_Target_SilveredBulwark`

### SBS_Scroll_HellfireOrb.lsf.lsx (renamed from FBS_)
- `Name`: `FBS_Scroll_HellfireOrb` → `SBS_Scroll_HellfireOrb`
- `Stats`: `OBJ_FBS_Scroll_HellfireOrb` → `OBJ_SBS_Scroll_HellfireOrb`
- (SkillID and SpellId reference `Projectile_HellfireOrb_DeathKnight` — no change needed)

### CLAUDE.md
- Mod listing: `ForbiddenScrolls` → `SilveredBulwarkScroll`
- Docs path: `docs/forbiddenscrolls/` → `docs/silveredbulwarkscroll/`

### docs/silveredbulwarkscroll/item_catalog.md (renamed)
- Update all `FBS_` references back to `SBS_`
- Update mod name header

---

## UUID/Handle Requirements

None. No new content is being created; this is a pure rename/prefix revert.

---

## Testing Plan

### Test 1: Mod Loads Under Restored Name
1. Enable the `SilveredBulwarkScroll` mod in BG3.
2. Start a new game.
3. **Verify:** No load errors.
4. **Verify:** Mod appears as "Silvered Bulwark Scroll" in the mod list.

### Test 2: Both Scrolls in Tutorial Chest
1. Open the Tutorial Chest.
2. **Verify:** "Scroll of Silvered Bulwark" is present.
3. **Verify:** "Scroll of Hellfire Orb" is present.

### Test 3: Scrolls Cast Correctly
1. Use Scroll of Silvered Bulwark — verify invulnerability effect on target.
2. Use Scroll of Hellfire Orb — verify large fire AoE explosion.

---

## Dependencies

**This phase depends on:**
- Phase 059 (COMPLETE) — ForbiddenScrolls rename and Hellfire Orb scroll addition.

---

## Success Criteria

- [ ] All directories renamed to `SilveredBulwarkScroll`
- [ ] All `FBS_` stat/spell/template names reverted to `SBS_`
- [ ] meta.lsx updated with correct folder name, mod name
- [ ] TreasureTable references updated
- [ ] Both scroll RootTemplates updated
- [ ] CLAUDE.md and docs updated
- [ ] Both scrolls appear in Tutorial Chest
- [ ] Both scrolls function correctly
- [ ] User-tested and confirmed

---

## Related Documentation

- **`docs/silveredbulwarkscroll/item_catalog.md`** — Item catalog for this mod
- **`docs/phases/Phase058.md`** — Original mod creation
- **`docs/phases/Phase059.md`** — ForbiddenScrolls rename + Hellfire Orb addition

---

## Phase 061 Status: IMPLEMENTED
