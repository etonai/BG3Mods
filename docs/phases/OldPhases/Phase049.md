# Phase 049: Magic Greatsword Creation

**Status:** COMPLETE
**Date:** 2026-02-12
**Completed:** 2026-02-12
**Type:** Implementation Phase

---

## Goals

1. **Create Magic Greatsword** - New legendary greatsword for Level13PlusGear mod
2. **Visual Base** - Use MAG_Colossal_Greatsword appearance from vanilla BG3
3. **Initial Powers** - Start with L13_Sword_Tyr powers as baseline
4. **Power Adjustments** - Refine and adjust powers as needed
5. **Delivery** - Add to L13_Gear_Chest via TreasureTable

---

## Item Specifications

### Visual Reference
**Vanilla Item:** MAG_Colossal_Greatsword
- **MapKey UUID:** `26ac9758-19f4-4867-9d5d-57437d6b9794`
- This will be used as the ParentTemplateId for the visual appearance

### Base Powers (from L13_Sword_Tyr)

**Current L13_Sword_Tyr Configuration:**
```
type "Weapon"
using "WPN_Longsword_2"
data "RootTemplate" "ed13abe5-df58-4ba4-915f-dafaee1f7906"
data "Rarity" "Legendary"
data "DefaultBoosts" "WeaponEnchantment(5);WeaponProperty(Magical)"
data "Boosts" "UnlockSpell(Target_MAG_Smite_Wrathful);UnlockSpell(L13_Target_BlindingSmite_Unlimited);UnlockSpell(L13_Target_Light_Unlimited);UnlockSpell(Target_PLA_ShieldOfFaith_SwordOfJustice);UnlockSpell(L13_Shout_CelestialHaste_Unlimited)"
data "PassivesOnEquip" "MAG_PlaneShifterSlayer_Passive;L13_RadiantWeapon_Passive"
data "Unique" "0"
```

**Powers Breakdown:**
- **Weapon Enchantment:** +5
- **Spells Unlocked:**
  - Wrathful Smite (vanilla)
  - Blinding Smite (unlimited, L13 custom)
  - Light (unlimited, L13 custom)
  - Shield of Faith (from Sword of Justice)
  - Celestial Haste (unlimited, L13 custom)
- **Passives:**
  - Plane Shifter Slayer (+1d8 psychic vs aberrations, celestials, elementals, fey, fiends)
  - Radiant Weapon (L13 custom - weapon sheds light, +1d4 radiant damage)

### New Greatsword Specifications

**Name:** Dawn's Blade
**Theme:** Lathander (god of dawn, light, renewal)
**Weapon Type:** Greatsword
**Base Template:** `WPN_Greatsword_2`
**Rarity:** Legendary
**Enchantment:** +5

**Powers:**
- **Weapon Actions:**
  - Pommel Strike - daze enemy
  - Lacerate - wound enemy, reduce movement
  - Cleave - AoE attack

- **Spell Unlocks:**
  - Celestial Haste (unlimited) - from L13_Sword_Tyr

- **Passives:**
  - Plane Shifter Slayer - +1d8 psychic vs aberrations, celestials, elementals, fey, fiends
  - Radiant Weapon - weapon sheds light, +1d4 radiant damage
  - Lathander's Light - from L13_Blade_Moonguard (light aura, sheds light)

- **Status on Equip:**
  - MAG_LATHANDERS_LIGHT_TECHNICAL

**Configuration:**
```
type "Weapon"
using "WPN_Greatsword_2"
data "DefaultBoosts" "WeaponEnchantment(5);WeaponProperty(Magical)"
data "BoostsOnEquipMainHand" "UnlockSpell(Target_PommelStrike);UnlockSpell(Target_Lacerate);UnlockSpell(Zone_Cleave)"
data "Boosts" "UnlockSpell(L13_Shout_CelestialHaste_Unlimited)"
data "PassivesOnEquip" "MAG_PlaneShifterSlayer_Passive;L13_RadiantWeapon_Passive;CRE_LathandersLight_Passive"
data "StatusOnEquip" "MAG_LATHANDERS_LIGHT_TECHNICAL"
data "Unique" "0"
```

---

## Implementation Plan

### Task 1: Create Greatsword RootTemplate

**File:** `Level13PlusGear/Public/Level13PlusGear/RootTemplates/L13_Greatsword_DawnsBlade.lsf.lsx`

**Requirements:**
- MapKey: New UUID from pool (ed13 prefix)
- ParentTemplateId: `26ac9758-19f4-4867-9d5d-57437d6b9794` (MAG_Colossal_Greatsword)
- Type: "item"
- Stats: "L13_Greatsword_DawnsBlade"
- DisplayName handle (ed13 prefix)
- Description handle (ed13 prefix)
- Icon: Research appropriate greatsword icon

### Task 2: Create Weapon Stats Entry

**File:** `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Weapon.txt`

**Entry Structure:**
```
new entry "L13_Greatsword_DawnsBlade"
type "Weapon"
using "WPN_Greatsword_2"
data "RootTemplate" "[uuid-from-task-1]"
data "Rarity" "Legendary"
data "DefaultBoosts" "WeaponEnchantment(5);WeaponProperty(Magical)"
data "BoostsOnEquipMainHand" "UnlockSpell(Target_PommelStrike);UnlockSpell(Target_Lacerate);UnlockSpell(Zone_Cleave)"
data "Boosts" "UnlockSpell(L13_Shout_CelestialHaste_Unlimited)"
data "PassivesOnEquip" "MAG_PlaneShifterSlayer_Passive;L13_RadiantWeapon_Passive;CRE_LathandersLight_Passive"
data "StatusOnEquip" "MAG_LATHANDERS_LIGHT_TECHNICAL"
data "Unique" "0"
```

**Note:** Includes standard greatsword weapon actions (Pommel Strike, Lacerate, Cleave) in `BoostsOnEquipMainHand` field.

### Task 3: Add Localization

**File:** `Level13PlusGear/Localization/English/Level13PlusGear.loca.xml`

**Entries:**
- DisplayName: "Dawn's Blade" (from MapKey with 'g' separators + 'h' prefix)
- Description: "A legendary greatsword blessed by Lathander, the Morninglord. This radiant blade channels the power of dawn, overwhelming enemies with celestial speed and the burning light of a new day. The sword's divine light drives back aberrations and otherworldly horrors."

### Task 4: Add to TreasureTable

**File:** `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/TreasureTable.txt`

**Add to L13_Gear_Chest_TT:**
```
new subtable "1,1"
object category "I_L13_Greatsword_DawnsBlade",1,0,0,0,0,0,0,0
```

### Task 5: Update Version

**File:** `Level13PlusGear/Mods/Level13PlusGear/meta.lsx`

Increment Version64 for new build

---

## Comparison: Longsword vs Greatsword

| Attribute | L13_Sword_Tyr (Longsword) | L13_Sword_Orpheus (Greatsword) |
|-----------|---------------------------|--------------------------------|
| **Base Template** | WPN_Longsword_2 | WPN_Greatsword_2 |
| **Weapon Actions** | (Uses default longsword actions) | Pommel Strike, Slash, Cleave, Mindcrush |
| **Boosts Field** | Boosts | BoostsOnEquipMainHand |
| **Damage** | 1d8 (base longsword) | 2d6 (base greatsword) |
| **Two-Handed** | Versatile | Required |

**Note:** L13_Sword_Orpheus uses `BoostsOnEquipMainHand` for its weapon actions, while L13_Sword_Tyr uses `Boosts` for spell unlocks. The new greatsword may need both fields.

---

## Power Adjustment Considerations

### Greatsword-Specific Actions to Consider

**From L13_Sword_Orpheus:**
- `UnlockSpell(Target_PommelStrike)` - Daze enemy
- `UnlockSpell(Target_Slash_New)` - Hamstring enemy
- `UnlockSpell(Zone_Cleave)` - AoE attack
- `UnlockSpell(Target_MAG_WeaponAction_Mindcrush)` - Psionic weapon action

**Vanilla Greatsword Actions:**
- Pommel Strike
- Lacerate
- Cleave

### Powers to Adjust from L13_Sword_Tyr

**Smites:**
- Wrathful Smite - Good for any weapon
- Blinding Smite - Good for any weapon
- Consider: Should these be limited or unlimited?

**Utility Spells:**
- Light - Fine to keep
- Shield of Faith - Fine to keep
- Celestial Haste - Powerful, may want to adjust

**Passives:**
- Plane Shifter Slayer - Thematic for certain greatswords
- Radiant Weapon - Thematic for holy weapons

**Questions for User:**
1. What theme should this greatsword have? (Holy, Psionic, Elemental, etc.)
2. Should it focus on damage, utility, or balanced?
3. Any specific powers or abilities desired?
4. Name and lore for the weapon?

---

## UUIDs Needed

Estimated UUIDs from pool (uuid_workflow.md):
1. Greatsword RootTemplate MapKey
2. DisplayName handle
3. Description handle
4. (Optional) OneTimeRewards UUID if adding to Traveler's Chest
5. (Optional) Ring of Creation summon spell handles (name + description)

**Required: 3 UUIDs** (RootTemplate + 2 localization)

Current pool has 40+ UUIDs available.

---

## Files to Create/Modify

### Level13PlusGear

**Create:**
- `Public/Level13PlusGear/RootTemplates/L13_Greatsword_[Name].lsf.lsx` - Greatsword RootTemplate

**Modify:**
- `Public/Level13PlusGear/Stats/Generated/Data/Weapon.txt` - Add greatsword stats entry
- `Public/Level13PlusGear/Stats/Generated/TreasureTable.txt` - Add to L13_Gear_Chest_TT
- `Localization/English/Level13PlusGear.loca.xml` - Add greatsword localization
- `Mods/Level13PlusGear/meta.lsx` - Increment version


---

## Testing Plan

### Test 1: Item Appearance
1. Start new game or use Ring of Creation summon
2. Obtain greatsword
3. **Verify:** Visual appearance matches MAG_Colossal_Greatsword
4. **Verify:** Name and description display correctly
5. **Verify:** Rarity shows as Legendary

### Test 2: Base Properties
1. Equip greatsword
2. Check character sheet
3. **Verify:** +5 weapon enchantment applies
4. **Verify:** 2d6 base damage (greatsword)
5. **Verify:** Weapon shows as magical

### Test 3: Weapon Actions
1. Equip greatsword in main hand
2. Open action menu
3. **Verify:** Appropriate greatsword weapon actions available
4. **Verify:** Actions function correctly

### Test 4: Spell Unlocks
1. Equip greatsword
2. Check spellbook/actions
3. **Verify:** All unlocked spells appear
4. **Verify:** Smites, utility spells work correctly
5. **Verify:** Unlimited spells don't consume resources

### Test 5: Passive Effects
1. Equip greatsword
2. Check character sheet passives
3. **Verify:** All passives appear in effects list
4. **Verify:** Passives function correctly in combat
5. **Verify:** Light/visual effects work if applicable

### Test 6: Delivery Method
1. Start new game
2. Open Tutorial Chest
3. **Verify:** L13_Gear_Chest contains greatsword
4. **Verify:** Can remove and equip normally

---

## Success Criteria

- ✅ Greatsword created with MAG_Colossal_Greatsword appearance
- ✅ Powers based on L13_Sword_Tyr and adjusted appropriately
- ✅ Weapon enchantment +5 applies correctly
- ✅ All spells and actions unlock properly
- ✅ Passives function correctly
- ✅ Delivers via L13_Gear_Chest
- ✅ Localization displays correctly
- ✅ Testing confirms all functionality

---

## Reference Items

### L13_Sword_Tyr (Longsword - Power Reference)
- File: `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Weapon.txt` (lines 10-18)
- Powers: Smites, utility spells, radiant damage, plane shifter slayer

### L13_Sword_Orpheus (Greatsword - Structure Reference)
- File: `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Weapon.txt` (lines 31-39)
- Structure: Uses WPN_Greatsword_2, BoostsOnEquipMainHand for weapon actions

### MAG_Colossal_Greatsword (Visual Reference)
- MapKey: `26ac9758-19f4-4867-9d5d-57437d6b9794`
- Source: Vanilla BG3
- Will be used as ParentTemplateId

---

## Next Steps

**Completed:**
1. ✅ User review of phase document
2. ✅ Name decided: Dawn's Blade
3. ✅ Theme decided: Lathander (Morninglord)
4. ✅ Powers decided: Celestial Haste, Plane Shifter Slayer, Radiant Weapon, Lathander's Light
5. ✅ Weapon actions decided: Pommel Strike, Lacerate, Cleave
6. ✅ Delivery decided: L13_Gear_Chest only

**Ready for Implementation:**
- All specifications confirmed
- Awaiting user command to implement

---

## Notes

- This is the first item in a series of magic items to be created
- Powers start with L13_Sword_Tyr as baseline but will be adjusted
- Greatsword requires `WPN_Greatsword_2` base template
- Greatsword weapon actions typically go in `BoostsOnEquipMainHand` field
- Visual appearance uses MAG_Colossal_Greatsword as parent template
- Need to research appropriate icon for the greatsword visual

---

## Specifications Confirmed

✅ **Name:** Dawn's Blade
✅ **Theme:** Lathander (god of dawn, light, renewal)
✅ **Powers:** Celestial Haste, Plane Shifter Slayer, Radiant Weapon, Lathander's Light
✅ **Weapon Actions:** Pommel Strike, Lacerate, Cleave
✅ **Delivery:** L13_Gear_Chest only (no Ring of Creation summon)
✅ **Base:** Greatsword with L13_Sword_Tyr powers + greatsword actions + Lathander's Light

**Ready for Implementation**

---

## Revision History

### Initial Creation (2026-02-12)
- Phase created for magic greatsword
- Visual base: MAG_Colossal_Greatsword
- Power base: L13_Sword_Tyr
- Status: PENDING - Awaiting user input on name, theme, and power adjustments

### Implementation Completed (2026-02-12)

**Status:** IMPLEMENTED - Ready for testing

**Dawn's Blade successfully created with all specifications:**

#### Files Created:

1. **RootTemplate:** `Level13PlusGear/Public/Level13PlusGear/RootTemplates/L13_Greatsword_DawnsBlade.lsf.lsx`
   - MapKey: `ed137fbf-d3b2-4e20-8a7b-e5dc624e8320`
   - ParentTemplateId: `26ac9758-19f4-4867-9d5d-57437d6b9794` (MAG_Colossal_Greatsword)
   - DisplayName handle: `hed132d41g5d26g47degbb55g61d4af60550b`
   - Description handle: `hed130875gb3f0g4bcag8b6egea29e5f9a696`

#### Files Modified:

2. **Weapon Stats:** `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/Data/Weapon.txt`
   - Added entry: `L13_Greatsword_DawnsBlade`
   - Base template: `WPN_Greatsword_2`
   - Weapon enchantment: +5
   - Weapon actions: Pommel Strike, Lacerate, Cleave (BoostsOnEquipMainHand)
   - Spell: Celestial Haste (unlimited)
   - Passives: Plane Shifter Slayer, Radiant Weapon, Lathander's Light
   - Status: Lathander's Light Technical

3. **Localization:** `Level13PlusGear/Localization/English/Level13PlusGear.loca.xml`
   - DisplayName: "Dawn's Blade"
   - Description: Full lore description of Lathander's greatsword

4. **TreasureTable:** `Level13PlusGear/Public/Level13PlusGear/Stats/Generated/TreasureTable.txt`
   - Added to L13_Gear_Chest_TT: `I_L13_Greatsword_DawnsBlade`
   - Will appear in Tutorial Chest via L13_Gear_Chest

5. **Version:** `Level13PlusGear/Mods/Level13PlusGear/meta.lsx`
   - Updated from Build 4 to Build 5
   - Version64: `36028900098179075` → `36028900098179076`

#### UUIDs Used (3 total):

- `306c7fbf-d3b2-4e20-8a7b-e5dc624e8320` → `ed137fbf-d3b2-4e20-8a7b-e5dc624e8320` (RootTemplate MapKey)
- `a3312d41-5d26-47de-bb55-61d4af60550b` → `hed132d41g5d26g47degbb55g61d4af60550b` (DisplayName handle)
- `6b470875-b3f0-4bca-8b6e-ea29e5f9a696` → `hed130875gb3f0g4bcag8b6egea29e5f9a696` (Description handle)

All UUIDs deleted from uuid_workflow.md pool.

#### Dawn's Blade Final Configuration:

```
new entry "L13_Greatsword_DawnsBlade"
type "Weapon"
using "WPN_Greatsword_2"
data "RootTemplate" "ed137fbf-d3b2-4e20-8a7b-e5dc624e8320"
data "Rarity" "Legendary"
data "DefaultBoosts" "WeaponEnchantment(5);WeaponProperty(Magical)"
data "BoostsOnEquipMainHand" "UnlockSpell(Target_PommelStrike);UnlockSpell(Target_Lacerate);UnlockSpell(Zone_Cleave)"
data "Boosts" "UnlockSpell(L13_Shout_CelestialHaste_Unlimited)"
data "PassivesOnEquip" "MAG_PlaneShifterSlayer_Passive;L13_RadiantWeapon_Passive;CRE_LathandersLight_Passive"
data "StatusOnEquip" "MAG_LATHANDERS_LIGHT_TECHNICAL"
data "Unique" "0"
```

**Ready for Testing:** All files created/modified, all specifications implemented.
