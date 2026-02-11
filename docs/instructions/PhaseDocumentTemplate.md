# Phase [NUMBER]: [Phase Title]

**Status:** PENDING
**Date:** [YYYY-MM-DD]

---

## Goals

[List the primary goals of this phase. Be specific and measurable.]

1. **[Goal 1]:** [Description of what this goal accomplishes]
2. **[Goal 2]:** [Description of what this goal accomplishes]
3. **[Goal 3]:** [Description of what this goal accomplishes]

---

## Summary of Changes

[Optional: Include a table summarizing key changes if the phase modifies existing functionality]

| Change | From | To |
|--------|------|-----|
| **[Change Category]** | [Current state] | [New state] |
| **[Change Category]** | [Current state] | [New state] |

**Result:** [One-sentence summary of the overall outcome]

---

## Current State

[Describe the current state of the mod/feature before this phase begins]

### [Subsection if needed]

**File:** `[Path to relevant file]`

```
[Code snippet showing current implementation]
```

**Current Behavior:**
- [Bullet point describing current behavior]
- [Another current behavior]

**Problem:** [If applicable, describe the issue with the current state]

---

## Target State

[Describe the desired state after this phase is complete]

### [Subsection for each major change]

**[What will change]:**
```
[Code snippet or description of new implementation]
```

**Changes:**
- [Specific change 1]
- [Specific change 2]

**Result:** [Expected outcome]

---

## Implementation Plan

[Break down the implementation into logical tasks]

### Task 1: [Task Name]

**Description:** [What this task accomplishes]

**Steps:**
1. [Specific step]
2. [Specific step]
3. [Specific step]

**Files to modify:**
- `[filepath]` - [what to change]

### Task 2: [Task Name]

[Repeat structure for each task]

---

## Detailed Implementation

[Provide step-by-step implementation details]

### Step 1: [Step Name]

**File:** `[Path to file]`

**[Action to take]:**
```
[Code example or detailed instruction]
```

**Purpose:** [Why this step is necessary]

### Step 2: [Step Name]

[Repeat for all steps]

---

## Files to Modify/Create

| File | Action | Description |
|------|--------|-------------|
| `[filepath]` | Create/Edit/Delete | [What changes are being made] |
| `[filepath]` | Create/Edit/Delete | [What changes are being made] |

---

## UUID/Handle Requirements

[If this phase requires new UUIDs or handles, document them here]

### Estimated UUIDs Needed

**[Item/Feature Name]:**
- RootTemplate: 1 UUID
- DisplayName: 1 handle
- Description: 1 handle

**Total Estimated:** [X] UUIDs, [Y] handles

### UUID Allocation

[Fill in during implementation]

**[Item/Feature Name]:**
- **UUID:** `[UUID value]`
- **Handle:** `[handle value]`
- **Purpose:** [What this is used for]

---

## Testing Plan

[Define how to test each aspect of the implementation]

### Test 1: [Test Name]
1. [Specific action to take]
2. [Specific action to take]
3. **Verify:** [What should be observed]
4. **Verify:** [What should be observed]

### Test 2: [Test Name]
[Repeat for each test case]

---

## Technical Notes

[Document any technical details, gotchas, or important considerations]

### [Topic]
- [Important note or consideration]
- [Reference to related systems or files]

### [Another Topic]
[Additional technical information]

---

## Dependencies

[List any mods or external requirements]

**This phase depends on:**
- [Mod/system name] - [Why it's needed]
- [Another dependency] - [Why it's needed]

**This phase affects:**
- [What might be impacted by these changes]

---

## Questions for User

[Optional: Include if there are decisions that need user input before implementation]

1. **[Question]:** [Provide context and options]
   - Option A: [Description and pros/cons]
   - Option B: [Description and pros/cons]

**Decision Required:** [What needs to be decided]

---

## Success Criteria

[Define what "complete" means for this phase]

- [ ] [Specific measurable outcome]
- [ ] [Specific measurable outcome]
- [ ] [Specific measurable outcome]
- [ ] [Testing completed and verified]
- [ ] [Documentation updated]

---

## Related Documentation

[Link to relevant documentation files]

- **[Document name]** - [Why it's relevant]
- **[Another document]** - [Why it's relevant]

---

## Notes

[Any additional notes, context, or considerations]

- [Note about design decisions]
- [Note about future considerations]

---

## Implementation Summary

[Fill in after implementation is complete]

**Completed:**

1. **[Task/Feature Name]** ✓
   - [What was done]
   - [Key details]
   - [Files modified]

2. **[Another Task/Feature]** ✓
   - [What was done]
   - [Result]

**Status:** IMPLEMENTED (awaiting user testing)

---

## Post-Implementation

- [ ] [Testing task]
- [ ] [Verification task]
- [ ] [Documentation task]
- [ ] User testing required before marking COMPLETE

---

## Revision Sections

[Add revision sections if bugs are found or changes are needed during implementation]

### Revision 1: [Issue Name]

**Issue:** [Description of what went wrong or what needs to change]

**Root Cause:** [Analysis of why the issue occurred]

**Solution:** [What will be done to fix it]

**Actions Taken:**
1. [Specific change made]
2. [Specific change made]

**Status:** [Fixed/In Progress/etc.]

---

## Postmortem

[Add after phase is complete - document lessons learned]

### What Went Well

- [What worked smoothly]
- [Good decisions that were made]

### What Was Challenging

- [Difficulties encountered]
- [Unexpected complexity]

### Lessons Learned

**[Key Lesson 1]:**
[Detailed explanation of what was learned and why it matters]

**[Key Lesson 2]:**
[Another important lesson from this phase]

### Recommendations for Future

- [How to approach similar tasks in the future]
- [What to avoid or what to do differently]

---

## Phase [NUMBER] Status: [PENDING/IMPLEMENTED/COMPLETE]

**Final Implementation:**
- ✓ [Major accomplishment]
- ✓ [Major accomplishment]
- ✓ [Major accomplishment]

**Lesson Learned:** [One-sentence key takeaway from this phase]

---

## Template Instructions

### When Creating a New Phase Document:

1. **Copy this template** to `docs/phases/Phase[XXX].md`
2. **Replace all [PLACEHOLDERS]** with actual content
3. **Remove unused sections** (e.g., Questions for User if no decisions needed)
4. **Keep section order** for consistency across phase documents
5. **Update status** as you progress: PENDING → IMPLEMENTED → COMPLETE
6. **Add revision sections** if bugs/issues arise during implementation
7. **Complete postmortem** after phase is marked COMPLETE

### Status Definitions:

- **PENDING:** Not yet started, planning only
- **IMPLEMENTED:** Code changes complete, awaiting user testing
- **COMPLETE:** User has tested and confirmed working

### Section Guidelines:

- **Goals:** Keep focused and measurable
- **Current State:** Document what exists now (with code examples if relevant)
- **Target State:** Be specific about the desired outcome
- **Implementation Plan:** Break into logical, manageable tasks
- **Testing Plan:** Make tests specific and repeatable
- **Success Criteria:** Define clear, measurable completion criteria
- **Postmortem:** Be honest about challenges and lessons learned

### Optional Sections:

Remove these if not applicable to your phase:
- Summary of Changes (only if modifying existing functionality)
- UUID/Handle Requirements (only if creating new content)
- Questions for User (only if decisions needed)
- Dependencies (only if phase depends on or affects other systems)
- Technical Notes (only if there are important technical details)
- Revision sections (only add when issues arise)

### Best Practices:

- Write as you plan (don't wait until implementation is done)
- Update during implementation (document decisions and discoveries)
- Include code examples where helpful
- Link to related documentation
- Document both successes and failures
- Make it useful for future reference
