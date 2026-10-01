# Agent Orchestration

## Objective
Operate the project from one control surface. The user should not need separate Claude and Grok chat windows.

## Architecture

Node-RED
→ FastAPI Job API
→ Orchestrator
→ Claude Code CLI / Grok API / deterministic Python
→ validation layer
→ PostgreSQL + GitHub
→ next event

### Agent roles

**Grok Researcher (API)**
- live web/category research
- new product discovery
- competitor/source discovery
- returns evidence + URLs as structured JSON
- does not directly mutate canonical product facts

**Claude Builder (CLI)**
- runs inside the repository checkout
- reads CLAUDE.md and job context
- codebase implementation
- schema/architecture changes
- tests and code review
- creates branch/commit/PR where appropriate

**Python services**
- deterministic extraction
- validation
- normalization
- formulas
- provenance
- DB writes
- job state transitions

## Node-RED flows

### 1. Daily product discovery
Inject/Cron
→ POST /jobs/discover
→ orchestrator
→ Grok API only when fresh web research is required
→ validate candidates
→ store candidates
→ trigger ingestion jobs

### 2. Product ingestion
candidate event
→ manufacturer extractor
→ normalization/validation
→ PostgreSQL
→ retailer offer discovery
→ metrics
→ changed-product event

### 3. Engineering task
failed pipeline / schema request / backlog item
→ create engineering job
→ controlled Claude CLI worker
→ branch/commit/PR
→ CI
→ merge/review gate
→ update progress

### 4. Content refresh
changed-product event
→ identify affected comparison pages
→ regenerate structured blocks
→ validation
→ WordPress draft/update

## Claude CLI execution model

Node-RED must not execute arbitrary shell text directly.

Use a controlled worker:
- receives job_id
- loads approved task from PostgreSQL
- checks out/updates repository
- launches Claude Code CLI with a fixed wrapper prompt
- captures stdout/stderr/exit status
- records agent run
- enforces timeout and budget
- never exposes arbitrary incoming text as raw shell

Example conceptual job:
```json
{
  "job_id": "ENG-184",
  "task_type": "engineering",
  "repo": "BillAlex33/product-intelligence-engine",
  "acceptance_criteria": ["tests pass", "progress updated"]
}
```

## Grok execution model
Grok is called through API with:
- explicit research question
- known products/sources
- output JSON schema
- time/token budget

All findings go through provenance/validation before canonical storage.

## Human review gates
Only interrupt the user for:
- unresolved product identity
- conflicting authoritative specs
- new category schema approval
- risky publishing/legal issue
- code changes failing CI repeatedly

Everything else should continue automatically.

## Security
- API keys in secrets/env vars, never Git.
- Claude CLI credentials stay on the worker host.
- Grok API key stays in secret storage.
- Separate budgets for research and engineering.
- Per-job timeout/token/cost ceilings.
- Restricted working directory for Claude.
- No arbitrary shell from Node-RED payloads.
