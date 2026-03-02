# Claude Instructions

## Active Mods

The following mods are actively being developed. All other mods in this project are reference examples only.

| Mod | Description |
|-----|-------------|
| SampleMagicRingMod | Custom magic items mod with weapons, armor, and rings |
| Level13PlusGear | Custom magic items mod with weapons, armor, and rings (for level 13+ characters) |
| Level21Gear | Legendary gear mod for level 21+ characters (Tutorial Chest delivery) |
| RingOfCreation | Utility mod with a ring that summons items by ID (depends on Level13PlusGear and SampleMagicRingMod) |
| SilveredBulwarkScroll | Standalone scroll mod — delivers powerful spell scrolls (Silvered Bulwark, Hellfire Orb) in the Tutorial Chest (no dependencies) |

---

## Phase Status Guidelines

- **PENDING**: Not yet started
- **IMPLEMENTED**: Code changes complete, awaiting user testing
- **COMPLETE**: User has tested and confirmed working

Phases are NOT complete until the user has tested them. Only mark a phase as COMPLETE when the user explicitly confirms testing is successful.

## Project Directory Structure

| Directory | Description |
|-----------|-------------|
| ExampleMods/ | Example/reference mods (not actively developed) |
| VanillaBG3/ | Vanilla BG3 game files for reference |
| VanillaBG3/gustav/ | Vanilla BG3 items, stats, and templates |
| VanillaBG3/shared/ | Shared vanilla BG3 resources |
| SpawnAnyItem/ | Item spawning tool (not a mod - utility for console commands) |

## Phase Implementation Conventions

When creating or implementing a new phase, always follow these conventions:

| Convention | Default |
|------------|---------|
| Target mod | SampleMagicRingMod |
| Reference items location | VanillaBG3/gustav directory |
| Item delivery (SampleMagicRingMod) | Traveler's Chest (via OneTimeRewards.lsx) |
| Item delivery (Level13PlusGear) | Tutorial Chest (via TreasureTable injection) |
| Item delivery (Level21Gear) | Tutorial Chest (via TreasureTable injection) |
| Post-implementation | Update docs/planning/item_catalog.md with new items |

These defaults apply unless the user explicitly specifies otherwise.

## Critical: Container Delivery Limitation

**IMPORTANT:** Container-based item delivery (Tutorial Chest, Traveler's Chest) has a significant limitation:

- **Once a container is opened** in a save file, its loot is "locked in" to that save
- **Adding new items** to the mod will NOT retroactively appear in already-opened containers
- **This affects existing saves** when updating mods with new items

**Implications:**
- Level13PlusGear is designed for **new games**
- Updating the mod mid-playthrough may not add new items to existing saves
- Players need to start new games or use console commands to get new items

**Documented in:** Phase030.md - "Critical Discovery: Container Delivery Limitation"

**Future Consideration:** Research alternative delivery methods (Script Extender, multiple containers, OneTimeRewards behavior) for better mid-playthrough update support.

## Documentation Structure

### docs/phases/
Phase files (Phase001.md, Phase002.md, etc.) track implementation progress for each development milestone. Each phase document includes goals, implementation details, UUIDs/handles, and test plans.

- **docs/phases/OldPhases/** - Archive location for completed/old phase documents to keep the main phases directory clean.

### docs/planning/
Item planning documents with design decisions, powers, and implementation details.

| File | Description |
|------|-------------|
| item_catalog.md | Complete list of all magic items in SampleMagicRingMod with stats and powers |

### docs/level13plusgear/
Planning and catalog documents specifically for the Level13PlusGear mod.

| File | Description |
|------|-------------|
| item_catalog.md | Complete list of all magic items in Level13PlusGear with stats and powers |

### docs/silveredbulwarkscroll/
Planning and catalog documents specifically for the SilveredBulwarkScroll mod.

| File | Description |
|------|-------------|
| item_catalog.md | Item catalog for the SilveredBulwarkScroll mod |

### docs/instructions/
Technical reference documentation for BG3 modding.

| File | Description |
|------|-------------|
| PhaseDocumentTemplate.md | **Template for creating new phase documents** - Comprehensive structure with all sections, guidelines, and best practices |
| uuid_workflow.md | **READ BEFORE Level13Gear work** - UUID pool, naming conventions (L13 prefix, ed13 UUID prefix) |
| armor_workflow.md | **READ BEFORE creating armor** - Base template selection, container delivery compatibility, armor creation checklist |
| copying_items_between_mods.md | Step-by-step guide for copying items from one mod to another |
| adding_spells_without_item_source.md | Container spell technique for spells no item grants |
| interesting_magical_effects.md | Collection of effects/passives for future items |
| BG3_Modding_Lessons_Learned.md | Key lessons: handle format, file structure, debugging, item delivery methods |
