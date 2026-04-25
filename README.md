# Lean Security — Claude Code Project Template

A reusable template for building Lean Security projects with Claude Code. Clone it, write a behavior spec, and the agent builds it — documents, CLI tools, or web applications — with CSFLite as the governing framework.

## What's Inside

```
CLAUDE.md                    → Claude Code system prompt (loaded every session)
.claude/settings.json        → Permission guardrails
csflite/controls.json        → 25 CSFLite controls (source of truth)
csflite/scoring.md           → Scoring methodology reference
claude-project/              → Kit for designing specs in Claude conversations
pyproject.toml               → Poetry config + Black/Ruff/Bandit/pytest settings
.pre-commit-config.yaml      → Pre-commit hooks (runs on every git commit)
setup.sh                     → Post-clone local configuration
```

## Quick Start

### 1. Clone

```bash
git clone git@github.com:<your-org>/lean-security-template.git my-project
cd my-project
./setup.sh
```

`setup.sh` does three things:
- Configures `.git/info/exclude` so `.claude/` and local-only files are never pushed from project repos
- Installs Python dev dependencies via Poetry
- Installs pre-commit hooks (Black, Ruff, Bandit, pytest) so every commit is automatically validated

### 2. Design the Spec

Set up a Claude project for spec development:

1. Create a new Claude project (e.g. "My Project — Spec")
2. Paste `claude-project/system-instruction.md` as the project system prompt
3. Upload as project knowledge:
   - `claude-project/project-yaml-schema.md`
   - `claude-project/examples/baseline-assessment.yaml`
   - `csflite/controls.json`
   - `csflite/scoring.md`
4. Upload any seed documents (existing architecture docs, engagement notes)

Then start a conversation. Two modes:

**Greenfield:** "I'm starting a HIPAA alignment engagement for a 40-person healthtech company. Help me write the project.yaml."

**Decomposition:** "Here's our architecture document. Break it into a project.yaml, ADRs, and protocol definitions."

Output: a `project.yaml` and any supporting artifacts.

### 3. Drop Artifacts Into the Repo

Copy the spec and supporting files from the Claude conversation into your project:

```
my-project/
├── project.yaml              ← from Claude conversation
├── decisions/                 ← ADRs if any
│   └── 0001-azure-hosting.md
└── protocols/                 ← protocol definitions if any
    └── edr-telemetry.json
```

### 4. Execute in Claude Code

Open the project in Claude Code. The agent reads `CLAUDE.md`, which points it to `project.yaml` and `csflite/`. Every task follows the execution loop:

1. **READ** — project.yaml + controls.json + decisions/ + protocols/
2. **PLAN** — agent proposes what to build, presents to you
3. **APPROVE** — you review and adjust
4. **IMPLEMENT** — agent builds it
5. **VERIFY** — agent validates against CSFLite controls and acceptance criteria
6. **REPORT** — agent presents output with verification results

Or for simple projects, skip the Claude project step and initialize directly:

```
/project:new-project <domain>
```

## CSFLite

CSFLite is a 25-control governance framework derived from NIST CSF v2.0. It measures **coverage** (does this capability exist?), not maturity or risk.

Scoring: Yes (1.0) / Partial (0.5) / No (0.0) × weight per control.

See `csflite/controls.json` for the full control set and `csflite/scoring.md` for methodology.

## Project Structure After Setup

As you work, the repo grows:

```
my-project/
├── CLAUDE.md                  → system prompt (from template)
├── .claude/                   → settings, agents, commands (local only after setup.sh)
├── csflite/                   → framework data (from template)
├── claude-project/            → spec development kit (from template)
├── project.yaml               → your behavior spec
├── decisions/                 → architecture decision records
├── protocols/                 → domain-specific data contracts
├── docs/                      → generated documents (gitignored)
├── setup.sh
├── .gitignore
└── README.md
```

## What This Template Does NOT Include

These are added per-project as needed, not baked into the template:

- Compliance crosswalks (SOC 2, HIPAA, ISO 27001 mappings)
- Application scaffolds (added via `/project:gen-app` when ready)
- CI/CD pipelines
- Docker/deployment configs
- Infrastructure-as-Code

## License

Lean Security IP. Not for redistribution.
