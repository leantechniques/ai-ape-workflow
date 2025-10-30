---
---

# Session Start Protocol

---

## STEP 1: READ CORE FILES

**Before anything else, read these files**:
1. **docs/context/MISSION.md** - Project identity, purpose, target users
2. **docs/TAG_INDEX.json** - Documentation tag index
3. **briefs/** directory - Check active briefs for current work

**If project-specific documentation exists**:
4. Check TAG_INDEX.json for relevant technical references

Read these first, every session.

---

## STEP 2: COLLABORATION DISCIPLINE

**Core Truth**: AI responds to instruction tone over documentation. Human language directly affects AI mode adherence.

| Mode | Human Says | AI Response | AI Never |
|------|------------|-------------|----------|
| **Exploration** | "What if...", "Should we...", "Something feels off..." | "Let me document this decision first" | Start implementation |
| **Planning** | "How should we break this down?", "What's the approach?" | "Let me create task breakdown for approval" | Jump to code without approval |
| **Implementation** | "Create X", "Implement Y", "Fix Z" | Execute directive | Question architecture (return to exploration) |

**Critical Signals**:
- **"Something feels off"** → STOP everything, return to exploration
- **Directive during wrong mode** → AI pauses, documents/plans first
- **Architecture questions mid-implementation** → STOP, return to exploration
- **Context collapse** (any bugs, workarounds) → STOP, rollback, smaller slices

**Recovery**: Implementation without plan → STOP → Retroactive plan → Keep/rollback | Exploration not documented → Pause → Document in docs/context/ or docs/standards/ → Resume

---

## STEP 3: DO YOU NEED TO CREATE A BRIEF?

**Is human expressing new intent and wants help structuring it?**

**YES** → Read `docs/workflow/brief-creation.md`

**NO** → Continue to Step 4

**Note**: Briefs can be created three ways:
1. **AI-assisted** (brief-creation.md) - Conversational structuring
2. **Human-written** (directly in `briefs/` using template) - Then validate in Exploration
3. **During exploration** (Exploration mode creates brief as artifact) - Documents discoveries

All paths valid. Briefs are tools, not requirements.

---

## STEP 4: IDENTIFY YOUR MODE

**What mode are you in?**

### EXPLORATION MODE
**Signals**:
- Asking "are we building the right thing?"
- Questioning architecture or design
- Making foundational decisions
- Human expresses uncertainty ("something feels off")
- No clear implementation plan exists

**→ Read:** `docs/workflow/exploration-mode.md`

---

### PLANNING MODE
**Signals**:
- Architecture decided
- Need to break work into tasks
- Creating implementation roadmap
- Ready to design approach

**→ Read:** `docs/workflow/planning-mode.md`

---

### IMPLEMENTATION MODE
**Signals**:
- Clear task list exists
- TDD workflow active
- Building/testing/validating
- Concrete goal file in place

**→ Read:** `docs/workflow/implementation-mode.md`

---

## WHERE ARE WE?

**To understand current project state:**
1. Check `briefs/` directory
   - List active briefs (work in progress)
   - Check completed briefs in `briefs/completed/`
   - Note if none exist
2. Review recent architecture decisions if needed
   - Check `docs/TAG_INDEX.json` for documentation tags and navigation
   - Load relevant docs/context/ and docs/standards/ docs based on current work
3. Find documentation by topic
   - Check `/docs/TAG_INDEX.json` to locate documentation by tags/topics
   - Minimal single-file index: tags, document mappings, and reading sequences
4. **Present to user, let them decide next action**

**This file defines PROCESS. Briefs track STATE. User chooses path.**

---

**Last Updated**: 2025-10-15 (Generalized and optimized)
