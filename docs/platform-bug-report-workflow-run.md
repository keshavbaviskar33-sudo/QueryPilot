# Bug report: workflow runs fail with missing `tool_calls` column

**Platform:** agenticorg.hackathon.pinelabs.com (v4.8.0)
**Org:** The Thinking Company
**When:** 2026-10-07 19:44:52 UTC (2026-10-08 01:14 IST)
**Workflow:** "ThinkCart Support Desk" (`045aab38-581b-46ec-a7ff-2e8ae50cdad1`), trigger: manual
**Run ID:** `ff6a8eea-07d2-41c1-9d5d-2e75021f229a` (engine run `wfr_c2ebe2062fa4`)

## What happened
The run status is `failed` with `steps_completed: 0`. The first agent step (`triage_message`) produced output, but saving that step crashed:

```
(sqlalchemy.dialects.postgresql.asyncpg.ProgrammingError)
column "tool_calls" of relation "step_executions" does not exist
[SQL: INSERT INTO step_executions (..., reasoning_trace, tool_calls, error, ...)]
```

It looks like a database migration that adds `step_executions.tool_calls` hasn't been applied.

## Side effects
- `GET /api/v1/workflows/runs/{run_id}` returns 500/502 continuously for this run, so the workflow page stays on "Running…".
- Running individual agents (`/api/v1/agents/{id}/run`) works fine. Only workflow runs are affected.

## Also observed
The step had `agent_type: "thinkcart_ticket_triage"` (a custom agent type in our tenant), but the step execution shows `agent_id: None` and a generic output. It seems the custom agent was not resolved from `agent_type`. Is `agent_id` the supported way to bind a workflow step to a specific agent?
