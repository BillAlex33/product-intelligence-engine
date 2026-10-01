# Agent Orchestration

## Objective
Operate the project from one control surface. The user should not need separate Claude and Grok chat windows.

## Architecture

Node-RED
→ Job API (FastAPI)
→ Orchestrator
→ specialist agent/API calls
→ validation layer
→ PostgreSQL/GitHub
→ next event

### Agent roles

**Grok Researcher**
- live web/category research
- new product discovery
- competitor/source discovery
- returns evidence + URLs as structured JSON

**Claude Builder**
- codebase implementation
- schema/architecture changes
- tests and code review
- works from GitHub context

**Python services**
- deterministic extraction
- validation
- normalization
- formulas
- provenance
- DB writes

## Node-RED flows

### 1. Daily product discovery
Inject/Cron
→ POST /jobs/discover
→ orchestrator
→ Grok only if web research is required
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
→ Claude Builder API
→ branch/PR
→ CI
→ merge/review gate
→ update progress

### 4. Content refresh
changed-product event
→ identify affected comparison pages
→ regenerate structured blocks
→ validation
→ WordPress draft/update

## Human review gates
Only interrupt the user for:
- unresolved product identity
- conflicting authoritative specs
- new category schema approval
- risky publishing/legal issue
- code changes failing CI repeatedly

Everything else should continue automatically.

## API adapters
Create provider adapters behind one interface:
- Anthropic/Claude adapter
- xAI/Grok adapter

The rest of the system should not know provider-specific details.

Suggested internal method:
run_agent(provider, role, job_payload) -> AgentResult

Store:
- provider
- model
- job_id
- prompt_version
- started_at
- completed_at
- tokens/cost
- result JSON
- status

## Security
API keys live in Node-RED/Docker secrets or environment variables, never Git.
Use separate keys/budgets for research and implementation agents.
Set per-job token/cost ceilings.
