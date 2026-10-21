---
name: handoff
description: Smart session handoff. Reads AGENTS.md to discover the project's planning/tracking documents, updates them, and writes a focused handoff doc. Use before ending a session or when saying "we'll continue later."
argument-hint: "What to focus on next session (e.g., we'll continue later, or focus on the auth module)"
---

This skill is project-agnostic. It discovers the project's organization by
reading `AGENTS.md` (or `CLAUDE.md`) from the working directory (walking up
to find it), then acts on whatever planning and tracking documents the project
defines.

## Process

1. **Discover project organization.** Read the project's `AGENTS.md` or
   `CLAUDE.md`. Identify:
   - What file(s) track work units and progress (e.g., a `PLAN.md` with
     checkboxes, a GitHub project board, a `TODO.md`, a linear.app link)
   - What file(s) track history and decisions (e.g., a `HISTORY.md`, a
     `CHANGELOG.md`, ADRs in `docs/adr/`, an `DECISIONS.md`)
   - What the project's conventions are for checkboxes, status, naming

2. **Update progress tracking.** Using the conventions discovered in step 1,
   update the project's planning documents to reflect what was accomplished
   in this session. Mark done items, add notes for in-progress work, update
   status tables. If the tracking document uses checkboxes, update them. If
   it uses labels on a board, describe what should change. Do NOT invent
   status conventions — use whatever the AGENTS.md tells you.

3. **Log to history.** Append to the project's history document (if one is
   defined in AGENTS.md). Record key decisions, roadblocks, and meaningful
   events from this session.

4. **Determine next steps.** From the planning documents, identify what
   remains to be done and what the next session should focus on. Use the
   user's argument (if any) as a focus hint, but let the planning documents
   be the primary source of truth.

5. **Write the handoff document.** Save to `~/.pi/handoffs/YYYY-MM-DD-<slug>.md`.
   The filename slug should reflect the project and next focus area.
   Structure the document with:
   - Current project state (which tracking items are done, which are active)
   - What was accomplished this session (concrete, not conversational replay)
   - Roadblocks and open questions
   - Key files and context the next agent needs (so it doesn't re-read everything)
   - Recommended skills for the next session
   - Exactly what to do first

6. **Output the absolute path** of the handoff file so the user can copy-paste it.

## Example

A project's `AGENTS.md` might define:
```
PLAN.md   → work units as [ ]→[~]→[x]→[v] checkboxes
HISTORY.md → append-only decision log
```
Another project might use a GitHub project board and ADRs. The skill adapts
to whatever AGENTS.md describes. PLAN.md and HISTORY.md are examples, not
requirements.

## Resuming

When the user says "resume from handoff" or provides a path, read the
handoff file and pick up where it left off. Discover the project organization
from AGENTS.md just as you did when creating the handoff. Do NOT write
a new handoff document in this case.
