# Augmented Product Engineer Workflow
*Mode-Based Development with Product Engineer Briefs*

## Overview

A structured workflow system for AI-driven development that uses **slash commands** (`/start`, `/explore`, `/plan`, `/implement`) to drive mode-based work through **Product Engineer Briefs** (documents combining product thinking and engineering execution) - living documents that collapse the entire planning-to-execution pipeline into one AI-optimized artifact that persists across multiple work sessions.

**For whom:** Solo developers and small teams building with AI-as-implementer, with adaptation patterns for larger organizations.

**Core Innovation**: Work flows through modes based on **what you don't know yet** (exploration for architecture, planning for implementation), not arbitrary process steps. Each brief evolves from exploration → planning → implementation, with explicit session restart rituals that create clean boundaries for multi-session work.

**Validated**: 23 product engineer briefs completed implementing experimental project, 613 tests passing (100% pass rate), significantly reduced "what was I working on?" moments. **Human never opened or read implementation files** - Claude CLI did all file creation, code writing, and implementation. Human role: conversational guidance as "lead dev/mentor" providing architectural decisions and design direction.

**Important caveat:** While validated on a substantial greenfield project (23 briefs, 58k total lines across code, tests, and documentation), this workflow has not been battle-tested in complex legacy applications. Future experiments planned to explore additional contexts.

---

## The Problem

**The traditional assumption**: AI helps developers write code faster through suggestions and implementations, but humans remain responsible for integrating, validating, and understanding the code.

**The actual opportunity**: AI can do ALL the implementation while humans focus on strategic thinking, architectural decisions, and product direction.

**The gap**: Traditional tools (JIRA, PRDs, technical specs) assume human memory and context. They're not designed for AI-driven workflows where AI is the implementer, starts fresh each session, and needs explicit resumption markers.

**For AI-driven workflows, traditional tools break down in three critical ways:**

**1. Artifact Fragmentation**

Traditional development relies on multiple artifacts spread across systems: PRDs for product thinking, technical specs for engineering design, tickets for task tracking, and progress boards for coordination. Each transition requires handoffs—product managers write PRDs, engineers translate them into specs, teams break specs into tickets. Context fragments across systems and roles.

**2. No Forcing Functions**

There's no mechanism to prevent skipping from initial idea straight to implementation without proper planning. Long sessions blend exploration, planning, and implementation without clear boundaries, leading to implementation drift, forgotten constraints, and decisions contradicting earlier planning.

**3. Human Memory Assumption**

Most critically, these tools assume human memory: developers remember previous sessions, understand unstated context, and know where they left off. AI doesn't. It starts fresh each session, needs explicit "resume here" markers, and benefits from enforced mode boundaries rather than free-form work. Without this structure, AI-driven development produces inconsistent, unmaintainable code.

---

## Comparison to Traditional Artifacts

| Feature | Brief¹ | User Story² | PRD² | JIRA Ticket | JIRA Epic³ | Technical Spec | ADR |
|---------|--------|-------------|------|-------------|------------|----------------|-----|
| **AI-Optimized** | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Intent/Why** | ✅ | ✅ | ✅ | ⚠️ | ⚠️ | ⚠️ | ✅ |
| **Single Source** | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Progress** | ✅ | ❌ | ❌ | ✅ | ⚠️ | ❌ | ❌ |
| **Task Tracking** | ✅ | ❌ | ❌ | ✅ | ⚠️ | ❌ | ❌ |
| **Explicit Constraints** | ✅ | ❌ | ⚠️ | ⚠️ | ⚠️ | ⚠️ | ✅ |
| **Dependency Map** | ✅ | ❌ | ❌ | ⚠️ | ⚠️ | ❌ | ❌ |
| **Multi-Session** | ✅ | ❌ | ❌ | ⚠️ | ⚠️ | ❌ | ❌ |
| **Living Doc** | ✅ | ❌ | ❌ | ⚠️ | ⚠️ | ❌ | ❌ |
| **Decision Rationale** | ✅ | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ✅ |
| **Alternatives Considered** | ✅ | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ✅ |
| **How to Build** | ✅ | ❌ | ❌ | ❌ | ❌ | ✅ | ❌ |
| **Forcing Functions** | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Scope/Coverage** | Heavy (400-800 lines) | Very Light (5-15) | Medium (100-300) | Light (20-50) | Light (50-150) | Medium (200-400) | Light (50-200) |

> ¹Briefs serve as the single source of truth for AI-driven development. Future work may include automated extraction of completed briefs into traditional artifact formats (User Stories, PRDs, Tech Specs, ADRs, JIRA tickets) for organizations requiring compliance or handoff documentation.

> ²User Stories and PRDs serve as natural product planning inputs to Brief creation in larger organizations. User Stories capture user empathy and drive Intent conversations; PRDs provide stakeholder alignment and detailed requirements. For solo/small teams, the Brief's strengthened Intent section captures this value directly without separate artifacts.

> ³JIRA Epic pattern used in this workflow (briefs with sub-briefs) is not fully fleshed out but served the purposes needed in the prior experiments. Sub-brief iteration and refinement planned for future experiments.

### Key Difference: Briefs as Source of Truth

Briefs collapse the entire planning-to-execution pipeline into one session-persistent, AI-optimized artifact. For solo/small teams, Briefs replace traditional artifacts. For larger organizations, Briefs serve as the living source of truth with product artifacts as input and compliance artifacts as output.

Traditional development relies on multiple artifacts with handoffs between people and systems:

**Traditional workflow**:
```
PM writes PRD (what/why)
  ↓ (handoff between people)
Engineer writes Spec (how)
  ↓ (handoff between people)
Engineer creates Tickets (tasks)
  ↓ (handoff to tracking)
Team updates Progress (separate system)
  → Artifacts go stale, context fragments
```

**Solo/Small Team workflow**:
```
Create Brief with strengthened Intent
  ↓
Human + AI collaborate in one artifact:
- Exploration → Planning → Implementation
  → Brief complete, no additional artifacts needed
```

**Large Organization workflow**:
```
[Input: Optional User Story/PRD from Product team]
  ↓
Create Brief (Product artifacts inform Intent section)
  ↓
Human + AI collaborate in one artifact:
- Exploration → Planning → Implementation
  ↓
[Extraction: Generate compliance artifacts as needed]
- Tech Specs, ADRs, JIRA tickets
  → Brief remains source of truth throughout
```

---

## The Solution

Three components address the three breakdowns: **Product Engineer Briefs** eliminate fragmentation (single source), **Mode-Based Workflow** prevents skipping planning (forcing functions), and **Session Restart Rituals** work with AI's fresh-start nature (explicit resumption).

#### 1. **Product Engineer Briefs**
One artifact that combines:
- **Product thinking**: Intent, constraints, signal (the "what" and "why")
- **Engineering design**: Exploration findings, technical decisions, alternatives (the "how")
- **Execution tracking**: Atomic TDD tasks, phase progress, multi-session resumption (the "doing")

**Four core sections** (always present):
1. **Intent** - For whom? What problem? What outcome? Why now? (User-focused "why")
2. **Constraints** - What can't change? (ADRs, mission, technical limits)
3. **Signal** - User signal (how users know), Technical signal (tests), Outcome signal (what ships)
4. **Open Questions** - What don't we know? (Drives mode selection)

**Three mode sections** (filled as work progresses):
- **Exploration Findings** (filled during `/explore`)
- **Planning Output** (filled during `/plan`)
- **Implementation Progress** (updated during `/implement`)

**Evolution pattern**: Brief starts as Intent + Constraints + Signal + Open Questions, then grows through modes as decisions get made and work gets done.

**Example:** Start with "We need authentication" (Intent) → Explore "Token-based or session-based?" (Findings) → Plan "8 phases, TDD pairs" (Output) → Implement phase-by-phase (Progress).

**Open Questions drive mode selection:** Architecture unknowns → Exploration, Implementation unknowns → Planning, No unknowns → Implementation. This forcing function prevents premature implementation.

#### 2. **Mode-Based Workflow**
Work flows through three modes based on explicit unknowns (inspired by [Patrick Robinson's RPI strategy](https://patrickarobinson.com/blog/introducing-rpi-strategy/)):

*Exploration* - Problem space unclear, architecture unknown
Document decisions, alternatives considered, and rationale.

*Planning* - Know what to build, need to design how
Create atomic task breakdown with dependencies, organized into phases.

*Implementation* - Plan exists, ready to execute
Execute one phase at a time, tests green, commit, restart for next phase.

**Driven by slash commands:** `/start` initializes session and loads MISSION.md, `/explore` answers Open Questions and documents decisions, `/plan` creates atomic task breakdown with dependencies, `/implement` executes one phase with tests and commits.

#### 3. **Session Restart Ritual**
Clean boundaries separate modes:

```
Exploration → [COMMIT + RESTART] → Planning → [COMMIT + RESTART] → Phase A → [COMMIT + RESTART] → Phase B → ...
```

**After ANY completion:**
- ✅ Exploration mode complete → restart
- ✅ Planning mode complete → restart
- ✅ Implementation phase complete → restart

**Why restart?** Prevents context drift while Brief preserves decisions. Each session starts clean with explicit resumption markers from the Brief.

**Example:** After completing Exploration mode across 2 sessions, commit all findings to the brief, close Claude CLI, then `/start` fresh for Planning mode. The brief's Exploration Findings section preserves all context—no human memory required.

**Multi-session resumption:** Phase Progress Tracker shows completed phases, TodoWrite status, and session commits - AI knows exactly where to resume without human memory.

---

**How they work together:** Briefs serve as the persistent artifact that evolves through work. Modes prevent premature implementation by forcing unknowns to be resolved first. Restarts create clean session boundaries that work with AI's fresh-start nature. Each component addresses a specific breakdown from traditional tools.

---

## Validation Patterns

### TDD Pairs Enforced in Planning

Every phase structured as:
```markdown
Phase A: Foundation
1. [ ] Write Test: Specific behavior
2. [ ] Implement: Make test pass
3. [ ] Write Test: Next behavior
4. [ ] Implement: Make test pass
5. [ ] Run tests: All green
6. [ ] Commit: "Phase A complete"
7. [ ] STOP: Session boundary
```

**Result**: 100% test pass rate maintained (613/613 tests).

### Dependency Mapping Prevents Blocking

Planning mode requires explicit dependency map:
```markdown
Dependencies:
- Phase 0 (Tokenizer) → Phase A (Parser) [A needs tokens]
- Phase A (Parser) → Phase B (Codegen) [B needs AST]
- Phase D (Validators) parallel to Phase B [Independent]
```

**Result**: Significantly reduced blocking issues by making dependencies explicit before implementation.

---

## Brief Structure

A typical brief contains 400-800 lines organized into seven sections. Four sections are always present (Intent, Constraints, Signal, Open Questions), and three sections fill as work progresses (Exploration Findings, Planning Output, Implementation Progress).

**Example structure:**

```markdown
## 📋 CURRENT MODE: [exploration/planning/implementation]
Status: active | completed
Architecture Tags: #compiler #control-flow #stage-2
(Tags help organize briefs by domain and sequence)

---

## Intent
For: [Who is this for - specific role/persona]
Problem: [What problem are they experiencing]
Outcome: [What becomes possible/easier/better]
Why Now: [Why is this important now]

## Constraints
- Mission alignment (references MISSION.md)
- ADR references (e.g., ADR-006)
- Technical limits
- Previous brief dependencies

## Signal
### User Signal
- How users know it works (feedback/behavior)
### Technical Signal
- Tests that prove it (validation)
### Outcome Signal
- What ships at the end (deliverables)

## Open Questions
1. Architectural unknown?
2. Implementation uncertain?
3. (None = ready for implementation)

---

## Exploration Findings
(Filled during /explore)
- Decision: What we chose
- Rationale: Why this approach
- Alternatives: What we didn't choose
- Planning Input: What to build next

---

## Planning Output
(Filled during /plan)

### Dependency Map
Phase X → Phase Y (why)

### Phase A: Name
1. [ ] Write Test: ...
2. [ ] Implement: ...
...
12. [ ] STOP: Session boundary

### Phase B: Name
...

---

## Implementation Progress
(Updated during /implement)

### Phase Progress Tracker
- [x] Phase A: Complete (Session 2, commit abc123)
- [ ] Phase B: Pending
- [ ] Phase C: Pending

### TodoWrite Status
- Phase A: 12/12 complete
- Phase B: 0/15 complete
```

---

## The Augmented Product Engineer Role

**What this workflow enables:**

**Human role (Augmented Product Engineer)**:
- Strategic thinking: "What should we build and why?"
- Architectural decisions: "Recursive descent or PEG parser?"
- Constraint setting: "Must align with mission, ADRs, design philosophy"
- Mode selection: `/explore`, `/plan`, or `/implement`?
- Quality gates: "Are tests passing? Is the brief complete?"
- **Zero implementation**: Never opened or read implementation files

**AI role (Claude CLI)**:
- All implementation: File creation, code writing, test writing
- Task execution: Following TDD pairs from planning
- Progress tracking: Updating briefs, marking phases complete
- Git commits: One commit per phase
- Test running: Ensuring 100% pass rate
- **Zero strategic decisions**: Following human guidance and brief structure

**This isn't AI-assisted development. It's human-guided AI development.** The human sets direction and constraints; the AI executes all technical work. Traditional AI-assisted development inverts this relationship.

---

## Evidence & Metrics

**Human contribution**:
- Implementation files opened: **0**
- Lines of code written: **0**
- Role: Conversational guidance, architectural decisions, mode selection
- Time: Strategic thinking and decision-making only

**AI contribution (Claude CLI)**:
- Files created: 217 (across code, tests, docs, and briefs)
- Lines of code written: ~58,000 total
  - 6,042 lines compiler code
  - 11,651 lines tests
  - 29,653 lines documentation
  - 10,625 lines briefs
- Role: All implementation, file creation, test writing, commits

**From 23 briefs**:
- Brief size: 400-800 lines (avg ~450)
- Phases per brief: 4-8 phases
- Tests: 613 tests, 100% pass rate maintained throughout
- Multi-session briefs: Briefs 06-08 spanned 1-8 sessions each
- Minimal context loss across sessions (explicit resume markers)
- Natural phase breakpoints for session boundaries
- Clean git history (one commit per phase)
- Natural error recovery: When phases needed adjustment, brief provided resumption context without session loss

**What this proves:** AI can handle 100% of implementation (18k lines of code + 12k lines tests) while human provides strategic guidance only. The workflow is validated by clean metrics (100% test pass rate, one commit per phase) and scales across 23 distinct features without human touching implementation code.