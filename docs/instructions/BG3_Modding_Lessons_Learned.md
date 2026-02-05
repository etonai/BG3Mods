# BG3 Modding Lessons Learned

This document summarizes key lessons learned while developing the Ring of Spectral Power mod for Baldur's Gate 3.

---

## File Structure

### Mod Directory Layout
```
ModName/
├── Mods/ModName/
│   ├── meta.lsx                          # Mod metadata and version
│   └── Story/RawFiles/Goals/             # Osiris scripts (optional)
├── Localization/English/
│   ├── ModName.xml                       # Localization source
│   └── ModName.loca.xml                  # Localization compiled (BOTH must be updated!)
└── Public/ModName/
    ├── RootTemplates/
    │   ├── merged.lsx                    # Item templates source
    │   └── merged.lsf.lsx                # Item templates compiled (BOTH must be updated!)
    ├── Stats/Generated/Data/
    │   ├── Armor.txt                     # Ring/armor stats
    │   ├── Spell_Projectile.txt          # Projectile spells
    │   ├── Spell_Target.txt              # Target spells
    │   └── Spell_Zone.txt                # Zone spells
    └── OneTimeRewards/
        └── OneTimeRewards.lsx            # Items delivered to Traveler's Chest
```

### Critical: Dual File Updates

**ALWAYS update BOTH versions of these files:**

| Source File | Compiled File | Purpose |
|-------------|---------------|---------|
| `merged.lsx` | `merged.lsf.lsx` | Item/object templates |
| `ModName.xml` | `ModName.loca.xml` | Localization strings |

The game reads the compiled versions. If you only update the source, changes won't appear in-game.

---

## Localization Handles

### Handle Format
Handles must follow this exact format:
```
h + 8 hex chars + g + 4 hex chars + g + 4 hex chars + g + 4 hex chars + g + 12 hex chars
```

**Example valid handle:** `hbd6db74ag37feg4288g8a9egf2dbf5e5cb17`

| Segment | Length |
|---------|--------|
| Prefix | 1 (`h`) |
| Block 1 | 8 |
| Separator | 1 (`g`) |
| Block 2 | 4 |
| Separator | 1 (`g`) |
| Block 3 | 4 |
| Separator | 1 (`g`) |
| Block 4 | 4 |
| Separator | 1 (`g`) |
| Block 5 | 12 |
| **Total** | **37 characters** |

**Common mistake:** Using 11 or 13 characters in the final block instead of exactly 12. This causes "Not Found" to display instead of the localized text.

### Localization File Structure
```xml
<contentList>
  <content contentuid="hxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx" version="1">Display Text Here</content>
</contentList>
```

---

## Spell Implementation

### Spell Types and Base Names

| Spell Type | File | Base Name Pattern | Example |
|------------|------|-------------------|---------|
| Projectile | Spell_Projectile.txt | `Projectile_SpellName` | `Projectile_MagicMissile` |
| Target | Spell_Target.txt | `Target_SpellName` | `Target_GlobeOfInvulnerability` |
| Zone | Spell_Zone.txt | `Zone_SpellName` | `Zone_Fear` |
| Shout | Spell_Shout.txt | `Shout_SpellName` | `Shout_Rage` |

### Spell Level Suffixes
Upcast versions use a numeric suffix indicating spell level:
- `Projectile_MagicMissile` - Level 1 (3 missiles)
- `Projectile_MagicMissile_2` - Level 2 (4 missiles)
- `Projectile_MagicMissile_3` - Level 3 (5 missiles)

### Making Spells Unlimited (No Spell Slot Cost)
```
data "UseCosts" ""
data "MemoryCost" ""
```

### Making Spells Cost a Bonus Action
```
data "UseCosts" "BonusActionPoint:1"
```

### Adding Short Rest Cooldown
```
data "Cooldown" "OncePerShortRest"
```

### Complete Spell Entry Example
```
new entry "SMR_Target_GlobeOfInvulnerability_ShortRest"
type "SpellData"
data "SpellType" "Target"
using "Target_GlobeOfInvulnerability"
data "DisplayName" "hc3d4e5f6ga7b8g9c0dga1b2g4c5d6e7f8a9b0;1"
data "ExtraDescription" "h3c4d5e6fg7a8bg0c9dg2a1bg5c6d7e8f9a0b1;1"
data "UseCosts" "BonusActionPoint:1"
data "Cooldown" "OncePerShortRest"
```

---

## Item Implementation

### Ring Stats Entry (Armor.txt)
```
new entry "SMR_Ring_Spectral_Power"
type "Armor"
using "_Ring"
data "RootTemplate" "d4e5f6a7-b8c9-4d0e-a1b2-c3d4e5f6a7b8"
data "ObjectCategory" "Jewelry"
data "ValueOverride" "750"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(SpellName1);UnlockSpell(SpellName2)"
```

### Rarity Values
- Common
- Uncommon
- Rare
- VeryRare
- Legendary

### Granting Spells from Items
Use `UnlockSpell()` in the Boosts field:
```
data "Boosts" "UnlockSpell(SMR_Projectile_MagicMissile_Unlimited_Lvl3);UnlockSpell(SMR_Target_GlobeOfInvulnerability_ShortRest)"
```

---

## OneTimeRewards (Traveler's Chest)

### Adding Items to Traveler's Chest
Use `OneTimeRewards.lsx` to deliver items once per save when entering camp:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<save>
    <version major="4" minor="8" revision="0" build="500"/>
    <region id="OneTimeRewards">
        <node id="root">
            <children>
                <node id="OneTimeReward">
                    <attribute id="Amount" type="uint32" value="1"/>
                    <attribute id="ItemTemplateId" type="FixedString" value="[ITEM_UUID]"/>
                    <attribute id="UUID" type="guid" value="[UNIQUE_REWARD_UUID]"/>
                </node>
            </children>
        </node>
    </region>
</save>
```

**Important:** Each OneTimeReward needs its own unique UUID. If the reward UUID has been claimed before (in a previous test), the item won't appear again. Change the reward UUID to re-test.

### Alternative: Osiris Script Method
For adding items on game start (not recommended - only triggers on new game):
```osiris
IF
    GameStarted()
THEN
    AddItemToTravelersChest("ITEM_UUID", 1);
```

---

## Version Management

### Version64 Format
The `meta.lsx` file uses an int64 encoded version number.

**Do NOT calculate manually.** Use one of these tools:
- **BG3 Mod Manager:** Press `Ctrl+G` or `Tools > Toggle Version Generator Window`
- **BG3 Modders Multitool:** `Utilities > Version Calculator`
- **BG3 Mini Tool:** Extra Tools Button

### meta.lsx Version Fields
Update both Version64 values:
```xml
<attribute id="Version64" type="int64" value="36028799166447616"/>
...
<node id="PublishVersion">
    <attribute id="Version64" type="int64" value="36028799166447616"/>
</node>
```

---

## Debugging Tips

### "Not Found" Display Name
1. Check handle format (must be exactly 37 characters with correct structure)
2. Verify handle matches in BOTH `.xml` and `.loca.xml` files
3. Verify handle matches between localization files and RootTemplates

### Spell Doesn't Cast / Wrong Icon
1. Verify the base spell name exists (check bg3.wiki for internal names)
2. Verify spell type matches (Target, Projectile, Zone, Shout)
3. Check that `using` references the correct base spell

### Item Doesn't Appear in Chest
1. Check if the OneTimeReward UUID was already claimed (change UUID to re-test)
2. Verify ItemTemplateId matches the MapKey in merged.lsx/lsf.lsx
3. Ensure both merged.lsx AND merged.lsf.lsx have the item

---

## Finding Vanilla Game Objects

### Directory Structure for Vanilla Assets
When researching vanilla BG3 items, spells, or other objects:

1. **Primary location:** `claudeModding/gustav` directory - Contains most vanilla game objects
2. **Secondary location:** `claudeModding/Shared` directory - If not found in gustav, check here

### Common File Locations
| Asset Type | Path |
|------------|------|
| Armor/Weapon Stats | `gustav/Public/GustavDev/Stats/Generated/Data/` |
| Spell Stats | `gustav/Public/GustavDev/Stats/Generated/Data/` |
| Root Templates | `gustav/Public/GustavDev/RootTemplates/` |
| Shared Stats | `Shared/Public/Shared/Stats/Generated/Data/` |

---

## Useful Resources

- [bg3.wiki - Modding Documentation](https://bg3.wiki/wiki/Modding:Creating_meta.lsx)
- [BG3 Mod Manager - GitHub](https://github.com/LaughingLeader/BG3ModManager)
- [bg3.norbyte.dev](https://bg3.norbyte.dev) - Technical spell/item data lookup

---

## Adding Extra Damage to Weapons

### Problem
We wanted to add +1d8 radiant damage to the Longsword of Tyr, similar to how the vanilla Devotee's Mace has +1d8 radiant damage.

### Failed Approach: StatusList in RootTemplate

The vanilla Devotee's Mace applies extra radiant damage via a **StatusList** in the RootTemplate:

```xml
<node id="StatusList">
    <children>
        <node id="Status">
            <attribute id="Object" type="FixedString" value="MAG_RADIANT_STRONG_RADIANCE_WEAPON" />
        </node>
    </children>
</node>
```

This status (`MAG_RADIANT_STRONG_RADIANCE_WEAPON`) is defined in GustavDev and adds `WeaponDamage(1d8, Radiant)`.

**Why it failed:** This approach did not work for our mod. The status is defined in the base game files (GustavDev) and may not be accessible or may require additional setup that isn't documented. Even after adding the Tags node that vanilla items use, the radiant damage still did not appear.

### Successful Approach: Custom Passive with CharacterWeaponDamage

The solution is to create a **custom passive** that adds extra damage via the `CharacterWeaponDamage` boost.

**Reference:** The vanilla `MAG_Legendary_PsionicWeapon_Passive` (used by Orpheus's Greatsword) demonstrates this pattern:

```
new entry "MAG_Legendary_PsionicWeapon_Passive"
type "PassiveData"
using "MAG_Githborn_Mindcrusher_Greatsword_Passive"
data "DescriptionParams" "DealDamage(1d6,Psychic)"
data "TooltipConditionalDamage" "DealDamage(1d6,Psychic)"
data "Boosts" "IF(IsMeleeAttack()):CharacterWeaponDamage(1d6, Psychic)"
```

**Our Implementation:**

1. **Create a custom passive in Passive.txt:**
```
new entry "SMR_RadiantWeapon_Passive"
type "PassiveData"
data "DisplayName" "h9e0f1a2bg3c4dg5e6fg7a8bg9c0d1e2f3a4b;1"
data "Description" "ha0f1b2c3gd4e5gf6a7g8b9cg0d1e2f3a4b5c;1"
data "DescriptionParams" "DealDamage(1d8,Radiant)"
data "TooltipConditionalDamage" "DealDamage(1d8,Radiant)"
data "Boosts" "IF(IsMeleeAttack()):CharacterWeaponDamage(1d8, Radiant)"
```

2. **Add the passive to the weapon's PassivesOnEquip:**
```
data "PassivesOnEquip" "MAG_PlaneShifterSlayer_Passive;SMR_RadiantWeapon_Passive"
```

3. **Add localization entries** for the passive's DisplayName and Description.

### Key Takeaways

- **Don't rely on vanilla statuses** applied via StatusList for custom mod items - they may not work
- **Use custom passives with `CharacterWeaponDamage`** to add extra damage to weapons
- The `IF(IsMeleeAttack())` condition ensures the damage only applies to melee attacks
- `DescriptionParams` and `TooltipConditionalDamage` ensure the damage displays correctly in tooltips

---

## Session Summary

### What We Built
**Ring of Spectral Power** - A Legendary ring with:
1. **Spectral Barrage** - Unlimited Level 3 Magic Missile (bonus action)
2. **Spectral Barrier** - Globe of Invulnerability (bonus action, short rest recharge)

### Files Created/Modified
- `Spell_Projectile.txt` - Added unlimited Magic Missile
- `Spell_Zone.txt` - Added Globe of Invulnerability (as Target type)
- `Armor.txt` - Added ring stats with spell boosts
- `merged.lsx` / `merged.lsf.lsx` - Added ring template
- `SampleMagicRingMod.xml` / `.loca.xml` - Added localization
- `OneTimeRewards.lsx` - Added ring delivery to chest
