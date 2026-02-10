# Claude Instructions

## Active Mods

The following mods are actively being developed. All other mods in this project are reference examples only.

| Mod | Description |
|-----|-------------|
| SampleMagicRingMod | Custom magic items mod with weapons, armor, and rings |
| Level13Gear | Custom magic items mod with weapons, armor, and rings |

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

## Phase Implementation Conventions

When creating or implementing a new phase, always follow these conventions:

| Convention | Default |
|------------|---------|
| Target mod | SampleMagicRingMod |
| Reference items location | VanillaBG3/gustav directory |
| Item delivery | Traveler's Chest (via OneTimeRewards.lsx) |
| Post-implementation | Update docs/planning/item_catalog.md with new items |

These defaults apply unless the user explicitly specifies otherwise.

## Documentation Structure

### docs/phases/
Phase files (Phase001.md, Phase002.md, etc.) track implementation progress for each development milestone. Each phase document includes goals, implementation details, UUIDs/handles, and test plans.

- **docs/phases/OldPhases/** - Archive location for completed/old phase documents to keep the main phases directory clean.

### docs/planning/
Item planning documents with design decisions, powers, and implementation details.

| File | Description |
|------|-------------|
| item_catalog.md | Complete list of all magic items in SampleMagicRingMod with stats and powers |

### docs/level13gear/
Planning documents specifically for the Level13Gear mod.

### docs/instructions/
Technical reference documentation for BG3 modding.

| File | Description |
|------|-------------|
| adding_spells_without_item_source.md | Container spell technique for spells no item grants |
| interesting_magical_effects.md | Collection of effects/passives for future items |
| BG3_Modding_Lessons_Learned.md | Key lessons: handle format, file structure, debugging |
