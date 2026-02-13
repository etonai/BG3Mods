# BG3 Modding Lessons Learned

This document summarizes key lessons learned while developing mods for Baldur's Gate 3.

## Active Mod

All custom items are developed in **SampleMagicRingMod**. Other mods in this project (e.g., gustav, Shared, WhimsicalWares) are reference examples for researching vanilla game objects and existing mod patterns.

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

## Item Delivery Methods

### Overview of Delivery Options

| Method | Location | Complexity | Compilation Required | Best For |
|--------|----------|------------|---------------------|----------|
| **TreasureTable.txt** | Tutorial Chest, specific containers | Low | No | Early game access, simple delivery |
| **OneTimeRewards.lsx** | Traveler's Chest | Low | No | Mid-game access, reliable delivery |
| **Story Goals** | Starting inventory | **Very High** | **Yes** | True starting inventory (rarely worth it) |
| **Script Extender** | Starting inventory, custom logic | High | No (but requires SE) | Advanced mods, dynamic behavior |

**Phase 36 Lesson:** Starting inventory via Story Goals requires compiled binary files (goals.raw, story.div.osi, story_ac.dat) generated by external tools (LSLib/Divinity Engine). **The complexity usually doesn't justify the marginal UX improvement over Tutorial Chest delivery.**

---

## CRITICAL: Armor Base Templates for Container Delivery

### The `_2` Suffix Problem

**Phase 047-048 Discovery:** Medium and heavy armor using base templates with the `_2` suffix **CANNOT be delivered via container inventories** (TreasureTable or OneTimeRewards).

### The Issue

When creating armor that will be delivered through chests or containers:

**❌ BROKEN - Will NOT appear in containers:**
```
new entry "MyArmor"
type "Armor"
using "ARM_HalfPlate_Body_2"        ← Has _2 suffix - WILL FAIL!
using "ARM_Splint_Body_2"           ← Has _2 suffix - WILL FAIL!
using "ARM_Plate_Body_2"            ← Has _2 suffix - WILL FAIL!
```

**✅ WORKING - Will appear in containers:**
```
new entry "MyArmor"
type "Armor"
using "ARM_ScaleMail_Body"          ← No _2 suffix - WORKS!
using "ARM_StuddedLeather_Body_2"   ← Light armor - Exception, works with _2
```

### The Solution

**For ALL medium/heavy armor that needs container delivery:**
```
using "ARM_ScaleMail_Body"
```

This base template works for:
- Half Plate armor
- Splint armor
- Plate armor
- Any medium/heavy armor

### Pattern Observed

| Armor Type | Template with `_2` | Template without `_2` | Container Delivery |
|------------|-------------------|----------------------|-------------------|
| Light armor | `ARM_StuddedLeather_Body_2` | N/A | ✅ Works with `_2` |
| Medium/Heavy | `ARM_HalfPlate_Body_2` | `ARM_ScaleMail_Body` | ❌ Fails with `_2` |
| Medium/Heavy | `ARM_Splint_Body_2` | `ARM_ScaleMail_Body` | ❌ Fails with `_2` |
| Medium/Heavy | `ARM_Plate_Body_2` | `ARM_ScaleMail_Body` | ❌ Fails with `_2` |

### Symptoms

If your medium/heavy armor:
- ✅ Works when summoned via spells or direct spawn
- ✅ Has correct RootTemplate and Stats entries
- ✅ Displays correctly when equipped
- ❌ Does NOT appear in chests/containers

**Root Cause:** You're using a base template with `_2` suffix. Change to `ARM_ScaleMail_Body`.

### Example: CL_InconstantMoon_ClericGear Reference

The working example mod uses `ARM_ScaleMail_Body` for all medium armor:

```
new entry "CL_TempSel_Shirt_HalfPlate"
type "Armor"
using "ARM_ScaleMail_Body"          ← Works!
data "ArmorClass" "12"
data "Rarity" "VeryRare"
data "Boosts" "Resistance(Lightning, Resistant)"
data "PassivesOnEquip" "MAG_ExoticMaterial_MediumArmor_Passive;..."
data "Unique" "0"
```

Even items named "Plate" use `ARM_ScaleMail_Body`:
```
new entry "CL_TempSel_Shirt_Plate"
type "Armor"
using "ARM_ScaleMail_Body"          ← Works for "plate" too!
```

### Checklist for Container-Delivered Armor

Before adding armor to TreasureTable or container inventories:

- [ ] Armor uses `ARM_ScaleMail_Body` (or light armor variant)
- [ ] NOT using `ARM_HalfPlate_Body_2`
- [ ] NOT using `ARM_Splint_Body_2`
- [ ] NOT using `ARM_Plate_Body_2`
- [ ] NOT using `ARM_HalfPlate_Body_Githyanki` or other `_2` variants
- [ ] Unique flag set to "0" if multiple copies needed

### Why This Happens

**Unknown.** This appears to be a BG3 engine limitation. The `_2` suffix variants work fine for:
- Direct spawning (console commands)
- Spell summons
- Direct inventory addition

But they **fail silently** when delivered via:
- TreasureTable container inventory population
- OneTimeRewards chest delivery

**Workaround:** Always use `ARM_ScaleMail_Body` for medium/heavy armor in containers.

### Related Issues

- **Phase 047:** Research phase investigating why L13_Armor_Tyr failed to appear in chests
- **Phase 048:** Created L13_Armor_Chest, discovered `_2` suffix issue via CL_InconstantMoon_ClericGear example
- **Revision 2:** Changing all medium/heavy armor from `_2` variants to `ARM_ScaleMail_Body` fixed the issue

---

## TreasureTable.txt (Tutorial Chest Injection)

### Adding Items to Tutorial Chest
Use `TreasureTable.txt` to inject items into existing game containers:

```
treasure itemtypes "Common","Uncommon","Rare","Epic","Legendary","Divine","Unique"

new treasuretable "TUT_Chest_Potions"
CanMerge 1
new subtable "1,1"
object category "I_YourItem",1,0,0,0,0,0,0,0
```

**Key Points:**
- `CanMerge 1` allows merging with vanilla table (adds to existing loot)
- Tutorial Chest provides **early access** (available on Nautiloid)
- Simple text format, no compilation required
- Reliable and easy to test

**When to Use:**
- ✅ You want items available early in the game
- ✅ You want simple, reliable delivery
- ✅ Tutorial Chest access is "good enough" for your UX needs

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

**When to Use:**
- ✅ You want items in Traveler's Chest specifically
- ✅ You want backup/alternative delivery location
- ✅ Simple XML format preferred

---

## Story Goals (Starting Inventory) - **NOT RECOMMENDED**

### Warning: Extreme Complexity

**Phase 36 Discovery:** Adding items to starting inventory via Story Goals is **significantly more complex** than it appears and usually **not worth the effort**.

### What Story Goals Require

1. **Source Files (RawFiles/):**
   - `Story/RawFiles/Goals/OneTimeRewards.txt` - Osiris script
   - `Story/RawFiles/story_header.div` - **HUGE** auto-generated file (53,000+ tokens)

2. **Compiled Binary Files (Story/):**
   - `goals.raw` - Compiled goals
   - `story.div` - Compiled story
   - `story.div.osi` - Osiris bytecode
   - `story_ac.dat` - Additional data
   - `story_orphanqueries_ignore.txt` - Orphan queries

3. **External Compilation Tools:**
   - **LSLib (divine.exe)** - Command-line compilation tool
   - OR **Divinity Engine** - Full modding suite
   - OR **BG3 Mod Manager** - May have compilation features

### Why It's So Complex

**The game does NOT read source files directly.** You must:
1. Write Osiris scripts in RawFiles/
2. Use external tools to compile to binary format
3. Debug compiled output if errors occur
4. Repeat for any script changes

**Without compiled files, the game will not start.**

### Example Story Goals Script

```osiris
Version 1
SubGoalCombiner SGC_AND
INITSECTION
DB_OneTimeRewards_ModName(1,(ITEMROOT)ItemName_UUID-with-hyphens);
KBSECTION
IF
LevelGameplayStarted(_,_)
AND
DB_Avatars(_Player)
THEN
PROC_OneTimeReward_GiveReward_ModName(1,1,1,_Player);

PROC
PROC_OneTimeReward_GiveReward_ModName((INTEGER)_RewardNo,(INTEGER)_Amount,(INTEGER)_Notification,(GUIDSTRING)_Player)
AND
NOT DB_OneTimeRewards_RewardGiven_ModName(_RewardNo)
AND
DB_OneTimeRewards_ModName(_RewardNo,_Reward)
THEN
DB_OneTimeRewards_RewardGiven_ModName(_RewardNo);
TemplateAddTo(_Reward,_Player,_Amount,_Notification);
EXITSECTION

ENDEXITSECTION
```

**Note:** UUID format uses **hyphens** not underscores: `ed315901-9dab-41eb-a5b4-cb0f073ef272`

### Cost-Benefit Analysis

**Benefits:**
- ✅ Player has item immediately at game start
- ✅ Best possible UX (no chest hunting)

**Costs:**
- ❌ Must learn Osiris scripting
- ❌ Must set up LSLib/Divinity Engine
- ❌ Must compile after every change
- ❌ Debugging compiled output is difficult
- ❌ Significantly higher maintenance burden

**Phase 36 Conclusion:** Tutorial Chest provides **nearly identical UX** (items available on Nautiloid) with **vastly lower complexity**. The cost-benefit analysis rarely justifies Story Goals for simple item delivery.

### When Story Goals ARE Worth It

Story Goals are powerful for:
- ✅ Complex quest logic and conditionals
- ✅ Dynamic NPC interactions
- ✅ Progression tracking across game events
- ✅ Advanced scripting that can't be done other ways

**Don't use Story Goals just for starting inventory.** Use TreasureTable.txt (Tutorial Chest) instead.

---

## Dual Delivery Strategy

**Phase 36 Solution:** Combine multiple delivery methods for best results.

### Example: Tutorial Chest + Traveler's Chest

```
TreasureTable.txt (Tutorial Chest):
- Early access on Nautiloid
- Simple text format

OneTimeRewards.lsx (Traveler's Chest):
- Backup/alternative location
- Simple XML format
```

**Benefits:**
- ✅ Player gets item early (Tutorial Chest)
- ✅ Backup if Tutorial Chest missed (Traveler's Chest)
- ✅ No compilation required
- ✅ Both methods are simple and reliable

**Set items as non-unique (Unique: 0)** so player can have multiple copies from different sources.

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
