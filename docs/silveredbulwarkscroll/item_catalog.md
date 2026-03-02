# SilveredBulwarkScroll — Item Catalog

A standalone mod that delivers powerful spell scrolls in the Tutorial Chest.

---

## Mod Info

| Field | Value |
|-------|-------|
| Mod Name | SilveredBulwarkScroll |
| Author | PseudonymousEd |
| Item Prefix | `SBS_` |
| UUID Prefix | `ed58` |
| Handle Prefix | `hed58` |
| Delivery | Tutorial Chest (`TUT_Chest_Potions`) |
| Dependencies | None (standalone) |

---

## Items

### OBJ_SBS_Scroll_SilveredBulwark (Scroll of Silvered Bulwark)

**Type:** Spell Scroll | **Rarity:** Rare | **Unique:** No

| Field | Value |
|-------|-------|
| Stats Entry | `OBJ_SBS_Scroll_SilveredBulwark` |
| RootTemplate UUID | `ed583900-31d6-4628-8073-44a00b243c80` |
| Spell Cast | `SBS_Target_SilveredBulwark` |
| Use Cost | 1 Action (from `_MagicScroll` base) |
| Delivery | `TUT_Chest_Potions` (Tutorial Chest) |
| Phase | Phase 058 (created), Phase 059 (renamed SBS_ → FBS_), Phase 061 (renamed back to SBS_) |

**Description:** A scroll inscribed with the Silvered Bulwark invocation. Encase an ally in a radiant shield of invulnerability. Single use.

---

### OBJ_SBS_Scroll_HellfireOrb (Scroll of Hellfire Orb)

**Type:** Spell Scroll | **Rarity:** VeryRare | **Unique:** No

| Field | Value |
|-------|-------|
| Stats Entry | `OBJ_SBS_Scroll_HellfireOrb` |
| RootTemplate UUID | `ed5856e4-08e5-48ee-a20b-d240c0c6ad5b` |
| Spell Cast | `Projectile_HellfireOrb_DeathKnight` (vanilla) |
| Use Cost | 1 Action (from `_MagicScroll` base) |
| Delivery | `TUT_Chest_Potions` (Tutorial Chest) |
| Phase | Phase 059 (created as FBS_), Phase 061 (renamed to SBS_) |

**Description:** A scroll inscribed with the Hellfire Orb incantation. Launches a searing orb that explodes in a 4-metre radius, dealing 20d6 Fire damage. DC 18 Dexterity saving throw for half damage. Single use.

---

## Custom Spells

### SBS_Target_SilveredBulwark

A standalone copy of `L21_Target_SilveredBulwark`. Used only by the Silvered Bulwark scroll.

| Field | Value |
|-------|-------|
| Base | `using "Target_GlobeOfInvulnerability"` |
| Level | 6 |
| School | Abjuration |
| Effect | Applies `LOW_RAMAZITHSTOWER_NIGHTSONG_GLOBE_1` (invulnerability aura that follows target) |
| Use Cost | BonusActionPoint:1 |
| Phase | Phase 058 (created as SBS_), Phase 059 (renamed to FBS_), Phase 061 (renamed back to SBS_) |

*Note: The Hellfire Orb scroll uses the vanilla spell `Projectile_HellfireOrb_DeathKnight` directly — no custom spell entry.*

---

## Summary

| Category | Count |
|----------|-------|
| Scrolls | 2 |
| Custom Spells | 1 |
| Total Items | 2 |
