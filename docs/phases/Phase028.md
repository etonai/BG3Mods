# Phase 028 - Level13Gear Preparation and Cleanup

**Status:** IMPLEMENTED

## Goal
Prepare the project for active development on the Level13Gear mod by cleaning up the repository, establishing documentation, and creating a more robust UUID workflow.

---

## Tasks

### 1. Add Example Mods to .gitignore
- [ ] ExampleMods and VanillaBG3 directories should be in .gitignore
- [ ] Update .gitignore to exclude these directories


### 2. Level13Gear UUID Workflow
Create a document establishing Level13Gear UUID and naming conventions:
- Item prefix for this mod should be `L13` (similar to `SMR` in SampleMagicRingMod)
- Generate a list of UUIDs using a UUID generator for L13Gear mod use
- Remove each UUID from the list when it's assigned to an item
- Replace the first 4 characters of generated UUIDs with `ed13` for easy identification


---

## Implementation Checklist

- [ ] Update .gitignore to exclude ExampleMods and VanillaBG3 directories
- [ ] Create Level13Gear UUID and naming convention document
- [ ] Generate initial UUID list for Level13Gear mod
- [ ] Test that excluded directories don't appear in git status

---

## Test Plan

- [ ] Run `git status` and verify ExampleMods and VanillaBG3 directories are excluded
- [ ] Verify Level13Gear UUID workflow document is clear and actionable
- [ ] Confirm UUID list is generated and ready for use

---

## Notes

- This is a preparation/cleanup phase, not an item implementation phase
- Level13Gear should be independent from SampleMagicRingMod going forward
- Better UUID practices will help avoid conflicts as the mod grows
