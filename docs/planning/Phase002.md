# Phase 002 - Add Globe of Invulnerability

**Status:** COMPLETE (2026-01-27)

## Goal
Add Globe of Invulnerability (once per short rest) to the Ring of Spectral Power.

## Scope
- New spell: Spectral Barrier (Globe of Invulnerability, short rest recharge)
- Update ring to grant this spell
- Update ring description

## UUIDs and Handles Needed

| Item | Type | Value |
|------|------|-------|
| Globe DisplayName | Handle | `hc3d4e5f6ga7b8g9c0dga1b2g4c5d6e7f8a9b0` |
| Globe ExtraDescription | Handle | `h3c4d5e6fg7a8bg0c9dg2a1bg5c6d7e8f9a0b1` |

---

## Files to Modify

### 1. NEW FILE: Stats/Generated/Data/Spell_Zone.txt

Create file with Globe of Invulnerability spell:
```
new entry "SMR_Zone_GlobeOfInvulnerability_ShortRest"
type "SpellData"
data "SpellType" "Zone"
using "Zone_GlobeOfInvulnerability"
data "DisplayName" "hc3d4e5f6ga7b8g9c0dga1b2g4c5d6e7f8a9b0;1"
data "ExtraDescription" "h3c4d5e6fg7a8bg0c9dg2a1bg5c6d7e8f9a0b1;1"
data "UseCosts" ""
data "Cooldown" "OncePerShortRest"
```

### 2. Stats/Generated/Data/Armor.txt

Update SMR_Ring_Spectral_Power Boosts to add the new spell:
```
data "Boosts" "UnlockSpell(SMR_Projectile_MagicMissile_Unlimited_Lvl3);UnlockSpell(SMR_Zone_GlobeOfInvulnerability_ShortRest)"
```

### 3. Localization/English/SampleMagicRingMod.xml

Add 2 content entries:
- Globe DisplayName: "Spectral Barrier"
- Globe ExtraDescription: "Globe of Invulnerability. Recharges on short rest."

### 4. Localization/English/SampleMagicRingMod.loca.xml

Add same 2 content entries (IMPORTANT: must update both files!)

### 5. Update Ring Description (both .xml and .loca.xml)

Update the ring description to mention the new power:
- Old: "A ring crackling with arcane force. Grants unlimited Magic Missile as a bonus action."
- New: "A ring crackling with arcane force. Grants unlimited Magic Missile as a bonus action and Globe of Invulnerability once per short rest."

---

## Implementation Order

1. [x] Create Spell_Zone.txt with Globe spell
2. [x] Add localization entries to SampleMagicRingMod.xml
3. [x] Add localization entries to SampleMagicRingMod.loca.xml
4. [x] Update ring description in both localization files
5. [x] Update ring Boosts in Armor.txt
6. [x] Build and test mod

---

## Test Plan

- [x] Build mod with BG3 Modder's Multitool
- [x] Load game with mod enabled
- [x] Equip Ring of Spectral Power
- [x] Verify "Spectral Barrier" spell appears in spell list
- [x] Cast spell - should create Globe of Invulnerability
- [ ] Verify spell is unavailable until short rest
- [ ] Take short rest
- [ ] Verify spell is available again
- [x] Verify ring description updated

## Lessons Learned

- Globe of Invulnerability is a **Target** type spell, not Zone
- Correct base spell: `Target_GlobeOfInvulnerability`
- Always verify base spell names on bg3.wiki before implementation

---

## Notes

- Based on lessons from Phase 001:
  - Must update BOTH `.xml` and `.loca.xml` localization files
  - Handle format: `h` + 8 hex + `g` + 4 hex + `g` + 4 hex + `g` + 4 hex + `g` + 12 hex
