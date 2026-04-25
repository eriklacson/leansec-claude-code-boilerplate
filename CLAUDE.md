# Lean Security — Claude Code Project

This is a Lean Security project powered by CSFLite.

## Operating Context
- CSFLite is a 25-control governance framework derived from NIST CSF v2.0
- It measures coverage (does this exist?), not maturity or risk
- All outputs must trace to CSFLite controls in `csflite/controls.json`
- Read `csflite/scoring.md` for scoring methodology
- Read `project.yaml` for project scope, acceptance criteria, and constraints
- Read `decisions/` for architecture decisions before planning any work

## Execution Loop
All tasks follow this loop — no exceptions:
1. READ — project.yaml + controls.json + decisions/ + protocols/ + seed-document.md (if present) + .claude/tasks.md
2. PLAN — propose what to build, present to architect for review
3. APPROVE — architect reviews, adjusts, records significant decisions as ADRs
4. IMPLEMENT — build it
5. VERIFY — validate control IDs against controls.json, check acceptance criteria, run tests, validate alignment with seed document
6. REPORT — present output + verification results, flag unresolved items honestly

Every task is defined in `.claude/tasks.md`. Reference a task by name instead of writing long prompts:

```
Execute task: gap-analysis
```

The agent loads the task definition, validates alignment with your seed document, then walks through the loop. Never skip the PLAN step. Never silently deliver unverified output.

## Stack Conventions
- Python: Poetry, FastAPI (API), Typer (CLI)
- Frontend: React via Vite
- Documents: Markdown
- Data: JSON for machine-readable, YAML for human-editable

## Hard Prohibitions
- No maturity scoring — coverage only
- No compliance certification claims — CSFLite is not a compliance framework
- No tool accumulation — governance clarity over tool sprawl
- No speculative scope expansion — build what the spec says
- Never push to remote — architect controls what leaves the repo
