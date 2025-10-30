# AI Workflow System

**Structured workflow for AI-assisted development. Prevents chaos, maintains discipline.**

For detailed context on the workflow system, validation evidence, and comparison to traditional artifacts, see [What Is This Repo?](z_WHAT_IS_THIS_REPO.md)

---

## Three Modes (Don't Mix)

**Exploration** → Are we building the right thing?
- Question architecture, make decisions
- Output: What to build

**Planning** → How do we build it?
- Break into atomic tasks with TDD
- Output: Implementation roadmap

**Implementation** → Build it
- Test-first workflow, commit per phase
- Output: Working, tested code

---

## Quick Start

**For Humans:**
1. Create brief: `docs/workflow/brief-creation.md`
2. Work with AI through modes
3. Brief tracks progress

**For AI:**
1. Read `docs/workflow/session-start.md` first
2. Follow mode-specific workflow
3. Update brief as you go

---

## File Structure

```
docs/
  ├── workflow/        # Process docs (AI reads these)
  ├── briefs/          # Work packages (active/completed)
  ├── context/         # Mission, architectural context
  ├── standards/       # Code/process standards
  └── TAG_INDEX.json   # Doc navigation
```

---

## Key Principle

**Mode discipline prevents context collapse.** Don't code during exploration. Don't debate architecture during implementation.

---

## Customization

**Adapt:** Constraints, tags, project specifics
**Keep:** Core mode structure, TDD workflow, phase boundaries

See change protocol in workflow docs before modifying process.
