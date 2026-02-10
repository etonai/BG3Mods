# Phase 022 - Moonguard Items

**Status:** COMPLETE

## Goal
Create copies of the Tyr magic item set, renamed as Moonguard items. Most items will have identical stats and powers to their Tyr counterparts, with some exceptions noted below.

---

## Item Mapping

| Tyr Item | Tyr Internal ID | Moonguard Item | Moonguard Internal ID |
|----------|-----------------|----------------|----------------------|
| Sword of Tyr | SMR_Sword_Tyr | Moonguard Blade | SMR_Blade_Moonguard |
| Armor of Tyr | SMR_Armor_Tyr | Moonguard Splint | SMR_Armor_Moonguard |
| Helmet of Tyr | SMR_Helmet_Tyr | Moonguard Helm | SMR_Helmet_Moonguard |
| Circlet of Tyr | SMR_Circlet_Tyr | Moonguard Circlet | SMR_Circlet_Moonguard |
| Gloves of Tyr | SMR_Gloves_Tyr | Moonguard Gloves | SMR_Gloves_Moonguard |
| Cloak of Tyr | SMR_Cloak_Tyr | Moonguard Cloak | SMR_Cloak_Moonguard |
| Shield of Tyr | SMR_Shield_Tyr | Moonguard Shield | SMR_Shield_Moonguard |

---

## Item Details

### Moonguard Blade
| Aspect | Value |
|--------|-------|
| Base | SMR_Sword_Tyr (copy) |
| Type | Longsword +5 |
| Rarity | Legendary |
| Powers | Wrathful Smite, Blinding Smite (unlimited), Light (unlimited), Shield of Faith, Celestial Haste (unlimited), Plane Shifter Slayer, Radiant Weapon (+1d4), Critical Bonus |

**Difference from Tyr:** Added Critical Bonus (MAG_TheClover_Rearrangement_Passive) - crit on 19-20, reroll damage dice of 2 or lower

### Moonguard Splint
| Aspect | Value |
|--------|-------|
| Base | SMR_Armor_Tyr (copy) |
| Base Type | ARM_Splint_Body_2 (+2 base) |
| Boosts | AC(3) (added to +2 base = +5 total) |
| Rarity | Legendary |
| Powers | +2 Saving Throws, no Dex cap, Celestial Haste (unlimited), Misty Step (unlimited), Spirit Guardians, Exotic Material |

**Difference from Tyr:** Changed from Half Plate +2 to Splint Armor +5 (using ARM_Splint_Body_2 base + AC(3) boost)

### Moonguard Circlet
| Aspect | Value |
|--------|-------|
| Base | SMR_Circlet_Tyr (copy) |
| Type | Circlet |
| Rarity | Legendary |
| Powers | Crit Immunity, Speak with Dead/Animals, See Invisibility, Protection from Evil/Good, Faerie Fire, +1 AC/Saves, Stun/Fear/Blind Immunity, Darkvision, Regen 2 HP/turn |

### Moonguard Helm
| Aspect | Value |
|--------|-------|
| Base | SMR_Helmet_Tyr (copy) |
| Type | Metal Helmet |
| ParentTemplateId | 197c32e4-6693-4d0e-846e-c5e1dc085010 (ARM_Helmet_Nightsong) |
| Rarity | Legendary |
| Powers | Same as Moonguard Circlet, plus Smite the Graceless |

**Difference from Tyr:** Different appearance (Nightsong helmet), added Smite the Graceless (MAG_Radiant_Radiating_Helmet_Passive) - when enemies miss you, they take 1d4 radiant (DEX 14 save) and get Radiating Orb

### Moonguard Gloves
| Aspect | Value |
|--------|-------|
| Base | SMR_Gloves_Tyr (copy) |
| Type | Metal Gloves |
| Rarity | Legendary |
| Powers | Thunderwave (short rest), Radiating Orb passive |

### Moonguard Cloak
| Aspect | Value |
|--------|-------|
| Base | SMR_Cloak_Tyr (copy) |
| Type | Long Cloak |
| Rarity | Legendary |
| Powers | Crusader's Mantle (unlimited), STR 29 min, CON 23 min, DEX 23 min |

### Moonguard Shield
| Aspect | Value |
|--------|-------|
| Base | SMR_Shield_Tyr (copy) |
| Base Type | ARM_Shield_2 (+2 base) |
| Boosts | AC(3) (added to +2 base = +5 total) |
| Rarity | Legendary |
| Powers | Reflective Shell, Warding Bond, Shield (unlimited), Shield Riposte, Spellguard |

**Difference from Tyr:** Changed from Shield +1 to Shield +5 (using ARM_Shield_2 base + AC(3) boost)

---

## Implementation Checklist

### For Each Item
- [x] Generate new UUIDs (MapKey, handles)
- [x] Add stats entry (Weapon.txt or Armor.txt)
- [x] Add RootTemplate to merged.lsx and merged.lsf.lsx
- [x] Add localization entries
- [x] Add OneTimeReward entry

### Items
- [x] Moonguard Blade
- [x] Moonguard Splint
- [x] Moonguard Helm
- [x] Moonguard Circlet
- [x] Moonguard Gloves
- [x] Moonguard Cloak
- [x] Moonguard Shield

### Final
- [x] Update item_catalog.md
- [ ] Build and test mod

---

## Test Plan

- [ ] Check traveler's chest for all 7 Moonguard items
- [ ] Verify each item has correct name and description
- [ ] Verify powers match Tyr counterparts

---

## Implementation Details

### UUIDs (MapKey)
| Item | MapKey |
|------|--------|
| Moonguard Blade | a1b2c3d4-e5f6-4a7b-8c9d-1e2f3a4b5c6d |
| Moonguard Splint | b2c3d4e5-f6a7-4b8c-9d0e-2f3a4b5c6d7e |
| Moonguard Helm | c3d4e5f6-a7b8-4c9d-0e1f-3a4b5c6d7e8f |
| Moonguard Circlet | d4e5f6a7-b8c9-4d0e-1a2b-4c5d6e7f8a9b |
| Moonguard Gloves | e5f6a7b8-c9d0-4e1f-2b3c-5d6e7f8a9b0c |
| Moonguard Cloak | f6a7b8c9-d0e1-4f2a-3c4d-6e7f8a9b0c1d |
| Moonguard Shield | a7b8c9d0-e1f2-4a3b-4d5e-7f8a9b0c1d2e |

### Localization Handles
| Item | DisplayName Handle | Description Handle |
|------|-------------------|-------------------|
| Moonguard Blade | h2b3c4d5eg6f7ag8b9cg0d1eg3f4a5b6c7d8e9 | h1a2b3c4dg5e6fg7a8bg9c0dg2e3f4a5b6c7d8 |
| Moonguard Splint | h4d5e6f7ag8b9cg0d1eg2f3ag5b6c7d8e9f0a1 | h3c4d5e6fg7a8bg9c0dg1e2fg4a5b6c7d8e9f0 |
| Moonguard Helm | h6f7a8b9cg0d1eg2f3ag4b5cg7d8e9f0a1b2c3 | h5e6f7a8bg9c0dg1e2fg3a4bg6c7d8e9f0a1b2 |
| Moonguard Circlet | h8b9c0d1eg2f3ag4b5cg6d7eg9f0a1b2c3d4e5 | h7a8b9c0dg1e2fg3a4bg5c6dg8e9f0a1b2c3d4 |
| Moonguard Gloves | h0d1e2f3ag4b5cg6d7eg8f9ag1b2c3d4e5f6a7 | h9c0d1e2fg3a4bg5c6dg7e8fg0a1b2c3d4e5f6 |
| Moonguard Cloak | h2f3a4b5cg6d7eg8f9ag0b1cg3d4e5f6a7b8c9 | h1e2f3a4bg5c6dg7e8fg9a0bg2c3d4e5f6a7b8 |
| Moonguard Shield | h4b5c6d7eg8f9ag0b1cg2d3eg5f6a7b8c9d0e1 | h3a4b5c6dg7e8fg9a0bg1c2dg4e5f6a7b8c9d0 |

---

## Notes

- Most items are copies of Tyr set with different names
- Exceptions documented in each item's "Difference from Tyr" note
- Consider creating unique visual appearances in future phase
- Consider adding moon-themed powers in future phase

## Planned Enhancements - IMPLEMENTED

### Moonguard Blade

**1. Add moon-themed effects from Selune's Mace (SMR_Mace_Selune_Moon):** ✓

| Effect | Passive | Description |
|--------|---------|-------------|
| Light of Lathander | CRE_LathandersLight_Passive | Toggled aura that blinds Fiends and Undead |
| Moonshield Aura | SMR_Moonshield_Passive | Protects allies from the Shadow Curse |

Also added: `StatusOnEquip "MAG_LATHANDERS_LIGHT_TECHNICAL"`

**2. Change appearance to Primeval Silver Longsword:** ✓

| Aspect | Value |
|--------|-------|
| ParentTemplateId | 20c66f8d-f455-42fc-8e48-543512247e75 |
| Source | MAG_Primeval_Silver_Longsword (vanilla) |

### Moonguard Splint

**1. Add Combat Regeneration from Ring of Regeneration:** ✓

| Aspect | Value |
|--------|-------|
| Passive | MAG_PHB_OfRegeneration_Ring_Passive |
| Status | MAG_PHB_RING_OF_REGENERATION_TECHNICAL |
| Effect | Regain 1d4 HP at start of each turn while in combat |
| Source | MAG_PHB_OfRegeneration_Ring (vanilla) |

---

## Known Issues

- ~~**Moonguard Shield** - Does not look like Shield of Tyr (different ParentTemplateId used)~~ **RESOLVED** - Fixed ParentTemplateId to match Shield of Tyr
- ~~**Moonguard Splint** - Does not look like Armor of Tyr (different ParentTemplateId used due to Splint base type)~~ **RESOLVED** - Fixed ParentTemplateId to match Armor of Tyr
- ~~**Moonguard Shield and Splint** - Wrong AC bonus (used AC(3) assuming base type had +2 built in)~~ **RESOLVED** - Changed to AC(5) for true +5 bonus

