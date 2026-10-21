# handoff-skill

Agent skill: smart session handoff. Reads the project's `AGENTS.md` (or
`CLAUDE.md`, walking up the tree) to discover its planning/tracking documents,
updates them, and writes a focused handoff doc for the next session.

## Provenance

This is a fork ("ripoff") of Matt Pocock's `handoff` skill:

- Upstream: https://github.com/mattpocock/skills (`skills/productivity/handoff`)
- Upstream license: MIT

The fork diverges deliberately: upstream compacts the raw conversation into a
generic handoff document; this version is project-organization-aware. It
discovers the project's own planning surface from `AGENTS.md`/`CLAUDE.md`
(HISTORY.md, ADR.md, REQUIREMENTS.md, whatever the project declares), updates
those documents, and references existing artifacts by path instead of
duplicating them. The skill body in `SKILL.md` is the pi-target adaptation.

## Install

Managed by [pf](https://github.com/rachidbch/pluginfountain) via the
`pf-profiles` fleet (`dev` profile, target `pi`).
