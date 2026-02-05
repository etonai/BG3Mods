# Phase 016 - Non-Unique Items Update

**Status:** COMPLETE

## Goal
Update select items to be non-unique and provide multiple copies for party-wide use.

---

## Item 1: Make Boots of the Stormwalker Non-Unique

### Overview
Remove the unique flag from Boots of the Stormwalker so multiple party members can equip them, and add 5 copies to the traveler's chest.

### Current Implementation

From Armor.txt:
```
new entry "SMR_Boots_Stormwalker"
type "Armor"
using "_Foot_Magic"
data "RootTemplate" "e1f2a3b4-c5d6-4e7f-8a9b-0c1d2e3f4a5b"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(SMR_Target_MistyStep_Unlimited)"
data "PassivesOnEquip" "MAG_Thunder_ReverberationOnStatusApply_Boots_Passive;FOR_NightWalkers_WebImmunity"
data "Unique" "1"
```

### Changes Required

#### 1. Stats/Generated/Data/Armor.txt
Remove the `data "Unique" "1"` line from SMR_Boots_Stormwalker entry.

#### 2. OneTimeRewards/OneTimeRewards.lsx
Update the Amount from 1 to 5 for the Boots of the Stormwalker reward.

---

---

## Item 2: Make Magus Circlet Non-Unique

### Overview
Remove the unique flag from Magus Circlet so multiple party members can equip them, and add 5 copies to the traveler's chest.

### Current Implementation

From Armor.txt:
```
new entry "SMR_Circlet_Magus"
type "Armor"
using "_Head_Magic_Circlet"
data "RootTemplate" "a2b3c4d5-e6f7-4a8b-9c0d-1e2f3a4b5c6d"
data "Rarity" "Legendary"
data "Boosts" "UnlockSpell(WW_Target_SpeakWithDead);UnlockSpell(WW_Shout_SpeakWithAnimals);UnlockSpell(SMR_Shout_SeeInvisibility_Unlimited);UnlockSpell(SMR_Target_ProtectionFromEvilAndGood_Unlimited);UnlockSpell(SMR_Target_FaerieFire_ShortRest)"
data "PassivesOnEquip" "MAG_LC_Cyric_FearImmunity_Amulet_Passive;MAG_Shadow_BlindImmunity_Ring_Passive;UND_SocietyOfBrilliance_DarkvisionRing_Passive"
data "Unique" "1"
```

### Changes Required

#### 1. Stats/Generated/Data/Armor.txt
Remove the `data "Unique" "1"` line from SMR_Circlet_Magus entry.

#### 2. OneTimeRewards/OneTimeRewards.lsx
Update the Amount from 1 to 5 for the Magus Circlet reward.

---

## Item 3: Make Circlet of Tyr Non-Unique

### Overview
Remove the unique flag from Circlet of Tyr so multiple party members can equip them, and add 3 copies to the traveler's chest.

### Changes Required

#### 1. Stats/Generated/Data/Armor.txt
Remove the `data "Unique" "1"` line from SMR_Circlet_Tyr entry.

#### 2. OneTimeRewards/OneTimeRewards.lsx
Update the Amount from 1 to 3 for the Circlet of Tyr reward.

---

## Implementation Checklist

### Boots of the Stormwalker
- [x] Remove `data "Unique" "1"` from SMR_Boots_Stormwalker in Armor.txt
- [x] Update OneTimeRewards.lsx to set Amount="10" for boots

### Magus Circlet
- [x] Remove `data "Unique" "1"` from SMR_Circlet_Magus in Armor.txt
- [x] Update OneTimeRewards.lsx to set Amount="5" for circlet

### Circlet of Tyr
- [x] Remove `data "Unique" "1"` from SMR_Circlet_Tyr in Armor.txt
- [x] Update OneTimeRewards.lsx to set Amount="3" for Circlet of Tyr

### Final
- [ ] Build and test mod

---

## Test Plan

### Boots of the Stormwalker
- [ ] Load game with mod enabled
- [ ] Check traveler's chest for 10 copies of Boots of the Stormwalker
- [ ] Equip boots on multiple party members simultaneously
- [ ] Verify all copies function correctly (Misty Step, Reverberation, Web Immunity)

### Magus Circlet
- [ ] Check traveler's chest for 5 copies of Magus Circlet
- [ ] Equip circlet on multiple party members simultaneously
- [ ] Verify all copies function correctly (Speak with Dead/Animals, See Invisibility, Protection From Evil And Good, Faerie Fire, Fear/Blind Immunity, Darkvision)

### Circlet of Tyr
- [ ] Check traveler's chest for 3 copies of Circlet of Tyr
- [ ] Equip circlet on multiple party members simultaneously
- [ ] Verify all copies function correctly (all Helmet of Tyr powers)

---

## Notes

*(To be added during implementation)*
