# Project Tasks

Define your project's tasks here. Each task enforces the READ → PLAN → APPROVE → IMPLEMENT → VERIFY → REPORT loop and validates alignment with your seed document (if present).

Copy this template for each task and fill in the fields. When executing a task in Claude Code, reference it by name:

```
Execute task: [task-name]
```

The agent will read this file, load the task definition, validate it against your seed document and project.yaml, then guide you through each step.

---

## Task Template

```markdown
### [Task Name]

**Type:** doc | app
**Subtype:** [gap-analysis | policy | mapping | assessment-report | executive-summary | cli | api | web]
**Description:** [One sentence: what this task produces and who it's for]

**Inputs:**
- [What the agent needs from you before starting]
- [Data, decisions, or approvals required]

**Outputs:**
- [What the agent will produce]
- [Where it will be written (docs/, src/, etc.)]

**Seed Document Alignment:**
Controls addressed: [list of control IDs from your seed document, or "all"]
Sections referenced: [which sections of seed-document.md this task uses, e.g., "section 3: Interface Contracts, section 8: CSFLite Interface"]
Architecture patterns: [which patterns from your seed document this implements]

**Acceptance Criteria:**
- [Verifiable criteria from project.yaml or task-specific criteria]
- [How the agent will validate the output]

**Execution Flow:**
1. READ — agent summarizes seed document scope, project.yaml constraints, and task definition
2. PLAN — agent proposes structure, data sources, and validation approach
3. APPROVE — you review plan, request changes, or approve
4. IMPLEMENT — agent builds the output
5. VERIFY — agent validates control references and alignment with seed document
6. REPORT — agent presents output with verification results
```

---

## Your Tasks

Define your project's tasks below. Remove this section once you've added your own tasks.

### Example: Baseline Assessment Report

**Type:** doc
**Subtype:** assessment-report
**Description:** Full 25-control CSFLite coverage assessment with scoring, evidence notes, and per-control findings for leadership review.

**Inputs:**
- Completed assessment questionnaire (responses to control questions in controls.json)
- Client context (organization size, industry, critical systems)

**Outputs:**
- `docs/assessment-report.md` — detailed findings with Yes/Partial/No scores and evidence

**Seed Document Alignment:**
Controls addressed: all
Sections referenced: section 1 (project scope), section 2 (architecture)
Architecture patterns: assessment-only (no implementation)

**Acceptance Criteria:**
- All 25 control IDs validated against csflite/controls.json
- Each control has documented evidence or rationale
- No maturity scoring language — coverage only
- Assessment report is under 10 pages

**Execution Flow:**
1. READ — agent loads assessment scope from project.yaml and seed document
2. PLAN — agent proposes assessment structure (per-function heatmap, control-level detail, gap identification)
3. APPROVE — you confirm scope and detail level
4. IMPLEMENT — agent generates assessment-report.md
5. VERIFY — agent validates control IDs and checks for anti-patterns (maturity language, compliance claims)
6. REPORT — agent presents report with verification results
