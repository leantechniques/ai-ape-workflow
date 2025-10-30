# Mission

**READ THIS FIRST. If you are ever confused about what this project is or does, come back to this file.**

---

## The Core Truth

**[Project Name] is [one-sentence definition of what this is].**

**The fundamental problem**: [What problem does this solve?]

**The fundamental solution**: [How does this solve it?]

[Expand on the core concept - what makes this different? Why does this approach work?]

---

## Primary User(s)

**The primary user is [who uses this and how].**

**Why this matters**:
- [How does this affect architecture decisions?]
- [How does this affect development workflow?]
- [How does this affect validation and testing?]
- [How does this affect success metrics?]

---

## What This Means for Development

### Core Deliverable

[What does this project actually produce? What is the output?]

### Key Components

[What are the main pieces that make this work?]

### Why These Constraints Exist

[What constraints guide development? Why do they exist?]

**Example constraints**:
- **[Constraint name]**: [Why it matters]
- **[Constraint name]**: [Why it matters]
- **[Constraint name]**: [Why it matters]

---

## Core Principles (Non-Negotiable)

**Note**: These are the rules that prevent quality degradation over time. Focus on what matters most for THIS product.

### Architectural Principles

**What architectural patterns/decisions are sacred?**

Examples for different product types:
- **E-commerce**: "Single source of truth for inventory" (prevents overselling)
- **SaaS**: "Multi-tenant data isolation" (security requirement)
- **Real-time app**: "Offline-first architecture" (user experience requirement)
- **Dev tool**: "Zero breaking changes to public API" (developer trust)

**Your principles** (keep 2-4 most critical):
1. **[Principle name]**
   - What: [One sentence - what does this mean in practice?]
   - Impact: [What breaks if we violate this?]
   - **Why non-negotiable**: [Business/technical reason this can't be compromised]

### Technical Standards

**What technical quality bars can't slip?**

Examples for different product types:
- **Mobile app**: "App bundle < 50MB" (user acquisition)
- **Dashboard**: "Initial load < 2s" (user retention)
- **API service**: "99.9% uptime SLA" (customer contracts)
- **Web app**: "WCAG AA compliance" (accessibility requirement)

**Your standards** (pick what actually matters):
1. **[Standard name]**: [Specific measurable requirement]
   - Why: [User impact or business requirement]

### Development Process

**What process rules keep quality high?**

Examples:
- **Testing**: "All features require integration tests" (prevent regressions)
- **Reviews**: "Security changes require two approvals" (reduce risk)
- **Deployment**: "Staging validation required before production" (catch issues early)
- **Documentation**: "API changes update docs before merge" (keep docs accurate)

**Your process rules** (2-3 that prevent quality issues):
1. **[Process rule]**
   - What: [When does this apply?]
   - Why: [What problem does this prevent?]

---

## Success Criteria

**How do we know if this product is succeeding?** (Pick metrics you can actually measure)

### User Success
1. **[User outcome metric]**
   - Measure: [How to track this - analytics, feedback, usage data?]
   - Target: [What number/state indicates success?]
   - Example: "Users complete core workflow in < 5 minutes" (measure via analytics)

### Business Success
2. **[Business metric]**
   - Measure: [Revenue, retention, growth - what matters?]
   - Target: [Specific goal]
   - Example: "Month-over-month active user growth > 10%"

### Quality Success
3. **[Quality metric]**
   - Measure: [Error rates, performance, uptime - what can't degrade?]
   - Target: [Acceptable threshold]
   - Example: "< 1% error rate on critical paths" (measure via monitoring)

---

## Non-Goals

**What [Project Name] is NOT**:

- **Not [misconception 1]** - [Clarification]
- **Not [misconception 2]** - [Clarification]
- **Not [misconception 3]** - [Clarification]
- **Not [misconception 4]** - [Clarification]

These are explicit rejections that prevent scope creep and mission drift.

---

## Reset Protocol: When You're Confused

If you find yourself asking:
- "[Common confusion 1]?"
- "[Common confusion 2]?"
- "[Common confusion 3]?"
- "[Common confusion 4]?"

**STOP. Come back to this file.**

**The answer is always**:
- [Core truth 1]
- [Core truth 2]
- [Core truth 3]
- [Core truth 4]

**When confused, ask**:
1. Does this serve [core goal 1]?
2. Does this align with [core principle]?
3. Does this prioritize [wrong thing] over [right thing]? (If yes, reject it)
4. Does this add complexity without serving the mission? (If yes, reject it)

---

## Implementation Principles

These principles guide all development work:

1. **[Development principle 1]**
   - [What to test/measure]
   - [What to validate]

2. **[Development principle 2]**
   - [What to enforce]
   - [How to enforce it]

3. **[Development principle 3]**
   - [What to maintain]
   - [Why it matters]

---

## When This File Changes

This file should almost NEVER change. The core mission is:

**[One sentence core mission]**

If you're tempted to change this file, you're probably drifting. Come back to the core truth.

---

## 🚨 CHANGE PROTOCOL 🚨

**If you think MISSION.md needs to change**:

1. **STOP immediately**
2. Create ghost file documenting:
   - What you want to change
   - Why you think it needs changing
   - What problem this solves
   - What evidence supports the change
3. **DO NOT make the change**
4. Wait for human review
5. Human decides if mission should evolve or if drift is happening

**This file defines the north star. Changing it without review means losing direction.**

---

## Decision Framework

**All decisions trace back to this mission:**
- Does this [positive criterion 1]? → Pursue it
- Does this [positive criterion 2]? → Pursue it
- Does this [negative criterion 1]? → Reject it
- Does this [negative criterion 2]? → Reject it

Without a single north star, decisions become arbitrary. With one, every choice has a clear evaluation criterion.

---

## How This Integrates

- **docs/standards/**: Quality standards must align with mission
- **docs/workflow/**: Workflow processes serve mission goals
- **briefs/**: Include mission alignment in Constraints section
- **docs/workflow/session-start.md**: References this as "read first" document

**When confused, return to first principles.** The answer is always in this file.

---

**Last Updated**: [YYYY-MM-DD]
**Status**: Sacred document - Read first, change never
