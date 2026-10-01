# Implement Agent Orchestration

Implement the first orchestration skeleton.

## Goal
The user should be able to operate the system from Node-RED without manually opening Claude or Grok chats.

## Build
1. AgentProvider interface.
2. Anthropic/Claude provider adapter.
3. xAI/Grok provider adapter.
4. Orchestrator service that selects an agent by job type.
5. AgentRun persistence in PostgreSQL.
6. JSON input/output validation with Pydantic.
7. Per-provider timeout, retry and cost/token limits.
8. FastAPI endpoints:
   - POST /jobs/research
   - POST /jobs/engineering
   - GET /jobs/{id}
9. Node-RED example flows for both job types.
10. Mock provider for tests so CI never requires live API keys.

## Routing policy
- fresh market/product/source research -> Grok Researcher
- code/schema/architecture/tests -> Claude Builder
- deterministic extraction/math/DB work -> Python only
- ambiguous mixed task -> orchestrator decomposes into research then engineering

## Important
Do not let Grok directly mutate canonical product facts.
Do not let Claude silently alter production data.
All external findings pass through provenance/validation.

Document required environment variables without committing secrets.
