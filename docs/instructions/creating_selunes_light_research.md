# Research: Creating Selûne's Light - Combined Aura Effect

**Date:** 2026-02-14
**Goal:** Create a custom aura that combines Lathander's Light (blinds Fiends/Undead) and Moonshield (Shadow Curse protection)
**Difficulty Assessment:** ⭐⭐⭐ Medium Difficulty

---

## Executive Summary

**Feasibility:** ✅ **HIGHLY FEASIBLE**

Creating a custom "Selûne's Light" that combines both Lathander's Light and Moonshield Aura effects is **definitely possible** and represents a **medium difficulty** implementation. The main challenge is understanding the AuraStatuses syntax for combining multiple conditional targets, but the vanilla game provides clear examples we can follow.

**Estimated Implementation Time:** 1-2 hours (including testing)

**Risk Level:** 🟢 **LOW** - Uses well-documented vanilla patterns, minimal chance of breaking existing functionality

---

## Concept: Selûne's Light

### Desired Effects

A single toggled aura that provides:

1. **Shadow Curse Protection** (from Moonshield Aura)
   - 13m radius
   - Grants `Tag(ACT2_SHADOW_CURSE_IMMUNE)` to allies
   - Emits moonlight

2. **Fiend/Undead Blinding** (from Lathander's Light)
   - Within the same 13m radius
   - Blinds enemy Fiends and Undead in combat
   - CON save DC 14 to resist

3. **Visual Theme**
   - Silver/blue moonlight (Selûne-themed)
   - Larger radius than Lathander's Light (13m vs 6m)
   - Combined visual effect of both auras

---

## Analysis: Vanilla Implementations

### Lathander's Light Structure

**Passive:** `CRE_LathandersLight_Passive`
```
new entry "CRE_LathandersLight_Passive"
type "PassiveData"
data "Properties" "ToggledDefaultOn;ToggledDefaultAddToHotbar;IsToggled"
data "ToggleOnFunctors" "ApplyStatus(MAG_LATHANDERS_LIGHT, 100, -1)"
data "ToggleOffFunctors" "RemoveStatus(MAG_LATHANDERS_LIGHT)"
```

**Aura Status:** `MAG_LATHANDERS_LIGHT`
```
new entry "MAG_LATHANDERS_LIGHT"
type "StatusData"
data "StatusType" "BOOST"
data "AuraRadius" "6"
data "AuraStatuses" "TARGET:IF(Combat() and Character() and Enemy() and (Tagged('FIEND') or Tagged('UNDEAD') or Tagged('UNDEAD_BEAST'))):ApplyStatus(MAG_LATHANDERS_LIGHT_BLIND_AURA_TARGET, 100, -1);YOURSELVES:YOURSELVES:ApplyStatus(MAG_LATHANDERS_LIGHT_SELF,100,-1)"
data "Boosts" "GameplayLight(6,false,0.1,true)"
```

**Key Observations:**
- Uses `AuraStatuses` with two targets: `TARGET:` (enemies) and `YOURSELVES:` (self)
- Conditional logic: `IF(Combat() and Character() and Enemy() and (Tagged('FIEND') or Tagged('UNDEAD')))`
- Applies different statuses to different targets
- Emits light with `GameplayLight(6,false,0.1,true)`

### Moonshield Aura Structure

**Aura Status:** `SCL_MOONSHIELD_AURA`
```
new entry "SCL_MOONSHIELD_AURA"
type "StatusData"
data "StatusType" "BOOST"
data "DisplayName" "hd6bd135bg4531g4124g9e22gfb187fe3b715;1"
data "Icon" "statIcons_Moonshield"
data "StackId" "SCL_MOONSHIELD_AURA"
data "AuraRadius" "13"
data "AuraStatuses" "TARGET:IF((Character() or Tagged('SPELLLIGHTOBJECT')) and not Tagged('SHADOW') and (not Tagged('ACT2_SHADOW_CURSE_IMMUNE') or HasStatus('SCL_MOONSHIELD'))):ApplyStatus(SCL_MOONSHIELD,100,-1)"
data "AuraFlags" "IgnoreItems"
data "Boosts" "GameplayLight(9,false,0.1)"
data "StatusPropertyFlags" "IgnoreResting"
```

**Protection Status:** `SCL_MOONSHIELD`
```
new entry "SCL_MOONSHIELD"
type "StatusData"
data "StatusType" "BOOST"
data "DisplayName" "h038b8505gf443g4003gb5f7g9ce3f2dbc1cc;2"
data "Description" "h532e2155gd26bg4152g9599gcacb1139e316;2"
data "Icon" "statIcons_Moonshield"
data "StackId" "SCL_SAFE"
data "StackPriority" "10"
data "StackType" "Ignore"
data "Boosts" "Tag(ACT2_SHADOW_CURSE_IMMUNE)"
data "StatusPropertyFlags" "DisableCombatlog;DisableOverhead"
```

**Key Observations:**
- Larger radius (13m vs 6m)
- Conditional logic: `IF((Character() or Tagged('SPELLLIGHTOBJECT')) and not Tagged('SHADOW')...)`
- Applies shadow curse immunity via `Tag(ACT2_SHADOW_CURSE_IMMUNE)`
- Uses `AuraFlags "IgnoreItems"` to avoid affecting items
- Applied via story scripting in vanilla, but can be toggled in custom implementation

---

## Technical Approach: Combining Both Effects

### Strategy: Multiple AuraStatuses Targets

The key insight is that `AuraStatuses` supports **multiple semicolon-separated target groups**. We can combine both effects by using three targets:

1. **TARGET 1:** Apply shadow curse protection to allies
2. **TARGET 2:** Blind enemy Fiends/Undead
3. **TARGET 3:** Apply self-status (for visual indicator)

### Proposed Implementation

#### Step 1: Create Custom Statuses

**1. Main Aura Status (L13_Selunes_Light_Aura)**

```
new entry "L13_SELUNES_LIGHT_AURA"
type "StatusData"
data "StatusType" "BOOST"
data "DisplayName" "h[HANDLE];1"
data "Description" "h[HANDLE];1"
data "Icon" "statIcons_Moonshield"
data "StackId" "L13_SELUNES_LIGHT_AURA"
data "AuraRadius" "13"
data "AuraStatuses" "TARGET:IF((Character() or Tagged('SPELLLIGHTOBJECT')) and not Tagged('SHADOW') and (not Tagged('ACT2_SHADOW_CURSE_IMMUNE') or HasStatus('L13_SELUNES_MOONSHIELD'))):ApplyStatus(L13_SELUNES_MOONSHIELD,100,-1);TARGET:IF(Combat() and Character() and Enemy() and (Tagged('FIEND') or Tagged('UNDEAD') or Tagged('UNDEAD_BEAST'))):ApplyStatus(L13_SELUNES_LIGHT_BLIND_TARGET, 100, -1);YOURSELVES:YOURSELVES:ApplyStatus(L13_SELUNES_LIGHT_SELF,100,-1)"
data "AuraFlags" "IgnoreItems"
data "Boosts" "GameplayLight(13,false,0.1)"
data "StatusPropertyFlags" "IgnoreResting"
data "StatusEffect" "[EFFECT_UUID]"
```

**Key Features:**
- 13m radius (matches Moonshield)
- Three target groups separated by semicolons
- First target: Applies shadow protection to allies
- Second target: Blinds enemy Fiends/Undead in combat
- Third target: Self-status for indicator
- Emits light at full radius (13m)

**2. Shadow Protection Status (L13_Selunes_Moonshield)**

```
new entry "L13_SELUNES_MOONSHIELD"
type "StatusData"
data "StatusType" "BOOST"
using "SCL_MOONSHIELD"
data "DisplayName" "h[HANDLE];1"
data "Description" "h[HANDLE];1"
data "Icon" "statIcons_Moonshield"
data "StackId" "SCL_SAFE"
data "StackPriority" "10"
data "StackType" "Ignore"
data "Boosts" "Tag(ACT2_SHADOW_CURSE_IMMUNE)"
data "StatusPropertyFlags" "DisableCombatlog;DisableOverhead"
```

**Key Features:**
- Uses `using "SCL_MOONSHIELD"` to inherit vanilla behavior
- Grants `Tag(ACT2_SHADOW_CURSE_IMMUNE)` for shadow curse protection
- Uses same StackId as vanilla (SCL_SAFE) for compatibility

**3. Blind Status (L13_Selunes_Light_Blind_Target)**

```
new entry "L13_SELUNES_LIGHT_BLIND_TARGET"
type "StatusData"
data "StatusType" "BOOST"
using "MAG_LATHANDERS_LIGHT_BLIND_AURA_TARGET"
data "DisplayName" "h[HANDLE];1"
data "Description" "h[HANDLE];1"
data "Icon" "[BLIND_ICON]"
data "StackId" "L13_SELUNES_BLIND"
```

**Key Features:**
- Uses `using "MAG_LATHANDERS_LIGHT_BLIND_AURA_TARGET"` to inherit vanilla blind behavior
- Targets make CON save DC 14 or become Blinded

**4. Self-Indicator Status (L13_Selunes_Light_Self)**

```
new entry "L13_SELUNES_LIGHT_SELF"
type "StatusData"
data "StatusType" "BOOST"
data "StatusType" "BOOST"
data "DisplayName" "h[HANDLE];1"
data "Description" "h[HANDLE];1"
data "Icon" "statIcons_Moonshield"
data "StatusPropertyFlags" "DisableCombatlog;DisableOverhead"
```

**Key Features:**
- Visual indicator that the aura is active
- Hidden from combat log and overhead

#### Step 2: Create Toggled Passive

```
new entry "L13_SelunesLight_Passive"
type "PassiveData"
data "DisplayName" "h[HANDLE];1"
data "Description" "h[HANDLE];1"
data "Icon" "statIcons_Moonshield"
data "Properties" "ToggledDefaultOn;ToggledDefaultAddToHotbar;IsToggled"
data "ToggleOnFunctors" "ApplyStatus(L13_SELUNES_LIGHT_AURA, 100, -1)"
data "ToggleOffFunctors" "RemoveStatus(L13_SELUNES_LIGHT_AURA)"
```

**Key Features:**
- Toggled on by default
- Appears in hotbar for easy toggling
- Same pattern as Lathander's Light

---

## Implementation Difficulty Assessment

### Difficulty Rating: ⭐⭐⭐ (3/5 - Medium)

### Easy Aspects ✅

1. **Well-Documented Patterns**
   - Both vanilla effects are well-documented in `interesting_magical_effects.md`
   - Clear examples to follow

2. **Using Vanilla Statuses**
   - Can inherit from vanilla statuses using `using` keyword
   - Don't need to recreate complex blind mechanics
   - Shadow curse immunity already implemented in vanilla

3. **Simple Toggled Passive**
   - Toggled passive pattern is straightforward
   - Same pattern used in many items

4. **No New Mechanics**
   - Not inventing new game mechanics
   - Just combining existing, tested systems

### Challenging Aspects ⚠️

1. **AuraStatuses Syntax**
   - Need to correctly format multiple target groups
   - Semicolons separate targets, colons separate conditions
   - Nested IF conditions can be tricky
   - **Mitigation:** Follow exact syntax from vanilla examples

2. **Conditional Logic Complexity**
   - Combining complex conditions for different targets
   - Need to understand Boolean logic (AND, OR, NOT)
   - **Mitigation:** Copy and modify vanilla conditions rather than creating from scratch

3. **Testing Requirements**
   - Need to test both effects work independently
   - Need to test they don't interfere with each other
   - Need to test in Shadow Curse areas (requires specific game location)
   - Need to test against Fiends/Undead enemies
   - **Mitigation:** Plan thorough testing phase, test each effect separately first

4. **Localization**
   - Need 8 handles total (4 DisplayNames + 4 Descriptions)
   - Need clear, thematic descriptions for Selûne
   - **Mitigation:** Write descriptions before implementation, use existing descriptions as templates

5. **Visual Effects**
   - May need to reference or create StatusEffect UUID for visual
   - Vanilla uses specific visual effects for each aura
   - **Mitigation:** Can reuse vanilla StatusEffect UUIDs initially, customize later

### Unknown/Uncertain Aspects ❓

1. **Aura Stacking Behavior**
   - Unclear if multiple auras on same item interact properly
   - May need to test carefully
   - **Risk:** Low - vanilla has multiple auras, should work fine

2. **Performance Impact**
   - 13m radius checking for multiple conditions on multiple targets
   - May have performance impact in crowded areas
   - **Risk:** Low - vanilla Moonshield uses same radius

3. **Story Script Compatibility**
   - Vanilla Moonshield uses story scripts for application
   - Custom version uses passive/status - may behave differently
   - **Risk:** Low - we're using standard status application, should work fine

---

## Resources Required

### UUIDs/Handles

| Resource | Quantity | Purpose |
|----------|----------|---------|
| Handles | 8 | DisplayName + Description for 4 statuses |
| StatusEffect UUID | 1 (optional) | Visual effect for main aura |

**Total:** 8 handles, 1 optional UUID

### Files to Create/Modify

**For Level13PlusGear mod:**

1. **Status_BOOST.txt** - Add 4 new status entries
2. **Passive.txt** - Add 1 new passive entry
3. **Level13PlusGear.loca.xml** - Add 8 localization entries
4. **Item Weapon.txt or Armor.txt** - Add passive to an item

**Estimated Lines of Code:** ~120-150 lines total

---

## Step-by-Step Implementation Plan

### Phase 1: Status Creation (45 mins)

1. ✅ Create L13_SELUNES_LIGHT_AURA status in Status_BOOST.txt
2. ✅ Create L13_SELUNES_MOONSHIELD status (using SCL_MOONSHIELD)
3. ✅ Create L13_SELUNES_LIGHT_BLIND_TARGET status (using MAG_LATHANDERS_LIGHT_BLIND_AURA_TARGET)
4. ✅ Create L13_SELUNES_LIGHT_SELF status

### Phase 2: Passive Creation (15 mins)

1. ✅ Create L13_SelunesLight_Passive in Passive.txt
2. ✅ Set up toggle functors

### Phase 3: Localization (20 mins)

1. ✅ Write 8 localization strings
2. ✅ Add to Level13PlusGear.loca.xml
3. ✅ Allocate handles

### Phase 4: Testing (30-60 mins)

**Test 1: Toggle Functionality**
1. Add passive to test item
2. Equip item
3. Verify toggle appears in hotbar
4. Test toggling on/off
5. Verify status appears/disappears

**Test 2: Shadow Curse Protection**
1. Travel to Shadow Curse area (Act 2)
2. Toggle aura on
3. Verify no shadow curse damage
4. Toggle aura off
5. Verify shadow curse damage returns
6. Test radius (13m) with party members

**Test 3: Fiend/Undead Blinding**
1. Find Fiend or Undead enemies
2. Toggle aura on
3. Enter combat
4. Verify enemies within 13m make CON save
5. Verify failed saves = Blinded status
6. Verify successful saves = no Blind
7. Test with multiple enemy types (Fiend, Undead, Undead Beast)

**Test 4: Combined Effect**
1. In Shadow Curse area with Fiend/Undead enemies
2. Toggle aura on
3. Verify both effects work simultaneously
4. Verify no conflicts or issues

**Test 5: Performance**
1. Test in crowded area
2. Verify no lag or performance issues
3. Test aura with multiple party members

---

## Potential Issues and Solutions

### Issue 1: AuraStatuses Syntax Error

**Problem:** Incorrect syntax in AuraStatuses causes aura to not work

**Solution:**
- Copy exact syntax from vanilla examples
- Test one target group at a time
- Add targets incrementally (first moonshield, then blind, then self)

### Issue 2: Both Effects Conflict

**Problem:** Blind and Shadow Protection don't work together

**Solution:**
- Test each effect independently first
- Check StackId conflicts
- Ensure different target conditions don't overlap

### Issue 3: Shadow Curse Protection Doesn't Work

**Problem:** Tag(ACT2_SHADOW_CURSE_IMMUNE) not applying correctly

**Solution:**
- Verify using same StackId as vanilla (SCL_SAFE)
- Check AuraStatuses condition matches vanilla
- Test if vanilla SCL_MOONSHIELD still works for reference

### Issue 4: Blind Not Working

**Problem:** Fiends/Undead not being blinded

**Solution:**
- Verify using vanilla blind status with `using`
- Check Enemy() condition is correct
- Verify Tagged('FIEND') and Tagged('UNDEAD') are correct tags
- Test against known Fiend/Undead enemies first

### Issue 5: Performance Impact

**Problem:** Aura causes lag in large areas

**Solution:**
- Reduce radius (13m → 10m)
- Add AuraFlags to limit checks
- Consider limiting to combat only: `IF(Combat() and ...)`

---

## Alternative Implementations

### Option A: Separate Toggle Passives (Easier)

Instead of one combined aura, create two separate toggled passives:
- **Selûne's Moonshield** - Shadow protection only
- **Selûne's Light** - Blind Fiends/Undead only

**Pros:**
- Easier to implement (no complex AuraStatuses)
- Can toggle effects independently
- Less risk of conflicts

**Cons:**
- Two hotbar slots instead of one
- Less elegant
- Not a true "combined" effect

**Difficulty:** ⭐⭐ (2/5 - Easy)

### Option B: Always-On Status (Easier)

Apply both statuses via StatusOnEquip instead of toggled passive:

```
data "StatusOnEquip" "L13_SELUNES_LIGHT_AURA"
```

**Pros:**
- Even simpler - no passive needed
- Always active when equipped
- One less file to modify (no Passive.txt)

**Cons:**
- Can't toggle off (may want to hide from enemies)
- Always uses resources/processing

**Difficulty:** ⭐⭐ (2/5 - Easy)

### Option C: Spell-Based Application (More Complex)

Create a spell that applies the aura status:

```
new entry "L13_Shout_SelunesLight"
type "SpellData"
data "SpellType" "Shout"
data "SpellProperties" "ApplyStatus(L13_SELUNES_LIGHT_AURA,100,-1)"
...
```

**Pros:**
- More control over application
- Can have cooldown/resource cost
- Thematic (casting "Selûne's Light")

**Cons:**
- More complex
- Requires spell definition
- Less convenient than toggle

**Difficulty:** ⭐⭐⭐⭐ (4/5 - Medium-Hard)

---

## Recommended Approach

### Primary Recommendation: Combined Aura with Toggled Passive

**Reasoning:**
1. Achieves the stated goal (combined effect)
2. Uses well-documented vanilla patterns
3. Medium difficulty is manageable
4. Single toggle is elegant and user-friendly
5. Can be tested incrementally

### Implementation Order:
1. Start with moonshield protection only
2. Test thoroughly
3. Add blind effect
4. Test both together
5. Polish and optimize

### Fallback Plan:
If combined aura proves problematic, fall back to **Option A** (separate toggles) which is easier and more reliable.

---

## Estimated Timeline

| Phase | Task | Time |
|-------|------|------|
| 1 | Research & Documentation | ✅ Complete |
| 2 | Status Creation | 45 mins |
| 3 | Passive Creation | 15 mins |
| 4 | Localization | 20 mins |
| 5 | Initial Testing | 30 mins |
| 6 | Thorough Testing | 30 mins |
| 7 | Bug Fixes & Polish | 15 mins |
| **Total** | | **~2 hours 35 mins** |

**Note:** Assumes access to Shadow Curse area for testing. If not, some tests will be delayed.

---

## Conclusion

### Final Assessment: ✅ HIGHLY FEASIBLE

**Difficulty:** ⭐⭐⭐ (3/5 - Medium)

**Confidence:** 🟢 **HIGH** (90%)

Creating "Selûne's Light" as a combined aura effect is **definitely achievable** for a modder with basic BG3 modding knowledge. The vanilla game provides clear examples of both effects, and combining them is a matter of:

1. Understanding the `AuraStatuses` syntax
2. Copying and modifying vanilla patterns
3. Careful testing to ensure both effects work together

**The main challenges are:**
- Getting the syntax exactly right
- Thorough testing requirements
- Managing 8 localization strings

**But these are manageable with:**
- Careful attention to detail
- Incremental testing (one effect at a time)
- Good documentation (which exists)

**Recommendation:** ✅ **PROCEED** with implementation, following the step-by-step plan above.

---

## Next Steps

1. **Decide on implementation approach** (recommended: combined aura with toggle)
2. **Allocate handles** (8 needed)
3. **Write localization strings** (before coding)
4. **Create statuses** (one at a time, test each)
5. **Create passive** (after statuses work)
6. **Test thoroughly** (plan Shadow Curse area visit)
7. **Document in item catalog** (after completion)

---

## References

- **interesting_magical_effects.md** - Detailed research on both vanilla effects
- **VanillaBG3/gustav/Public/GustavDev/Stats/Generated/Data/Status_BOOST.txt** - Vanilla status definitions
- **VanillaBG3/gustav/Public/GustavDev/Stats/Generated/Data/Passive.txt** - Vanilla passive definitions
- **Blood of Lathander** - Example item using Lathander's Light
- **Moon Lantern** - Example item using Moonshield Aura
