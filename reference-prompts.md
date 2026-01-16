# How to start:

```mermaid
graph TD
    %% --- Nodes ---
    EPIC[Start: EPIC PLAN]

    %% Branch 1
    GP1[General Plan A]
    SP1_A[Specific Plan A.1]
    SP1_B[Specific Plan A.2]
    T1[Task: Setup Env]
    T2[Task: Config DB]
    T3[Task: Create API]

    %% Branch 2
    GP2[General Plan B]
    SP2_A[Specific Plan B.1]
    SP2_B[Specific Plan B.2]
    T4[Task: UI Mockups]
    T5[Task: Frontend Auth]
    T6[Task: Landing Page]

    %% --- Connections ---
    EPIC --> GP1
    EPIC --> GP2

    %% General Plan A Breakdown
    GP1 --> SP1_A
    GP1 --> SP1_B
    SP1_A --> T1
    SP1_A --> T2
    SP1_B --> T3

    %% General Plan B Breakdown
    GP2 --> SP2_A
    GP2 --> SP2_B
    SP2_A --> T4
    SP2_B --> T5
    SP2_B --> T6

    %% --- Styling ---
    classDef epic fill:#212121,stroke:#000,stroke-width:2px,color:#fff
    classDef general fill:#1565C0,stroke:#0D47A1,stroke-width:2px,color:#fff
    classDef specific fill:#43A047,stroke:#1B5E20,stroke-width:2px,color:#fff
    classDef task fill:#FAFAFA,stroke:#333,stroke-width:1px,color:#000

    class EPIC epic
    class GP1,GP2 general
    class SP1_A,SP1_B,SP2_A,SP2_B specific
    class T1,T2,T3,T4,T5,T6 task
```

# Reference Prompts for AI Agents (Django, Celery, DRF)

## Architecture Sanity Before You Code
"Read @file:docs/api.md and the `urls.py` files in each Django app. List 3–5 design risks (coupling, caching, auth). For each, show the minimal change that reduces risk and link to lines by @file#line. Return a prioritized plan and an estimate of touched files."

*Why it works:* scopes the assistant to concrete files + a small, ranked plan. Review diffs in the VS Code panel before applying.

## API Contract → Server + Client Glue
"From @file:api/users/openapi.yaml, generate Django REST Framework serializers and viewsets, and a typed client. Include validation, error mapping, and tests. Keep each change in a separate patch."

*Keeps PRs readable:* pair with a slash command like `/api-from-openapi users`.

## DB Migration with Guardrails
"Audit `users/migrations/0001_initial.py` for encoding, indexing, and rollback risks. If safe, propose a patch; else output a checklist. Generate a verification script that samples rows and asserts invariants."

*Store this as* `/scan-migration`. I approve the verification script first, then the patch.

## Security Pass (Fast)
"Run a security review on the current diff. Flag auth boundaries (e.g., `permissions.py`, custom authentication classes), cookie/CSRF settings, header parsing, and secret exposure. Provide line-anchored fixes with rationale."

*Note:* There’s also an official security reviewer and GitHub Action if you want CI comments on PRs with suggested remediations.

## Tests That Pay Rent
"Given changes in `payments/` (e.g., `models.py`, `views.py`, `tasks.py`), propose table-driven tests that cover nulls, timeouts, idempotency, and retries for both synchronous and Celery asynchronous operations. Prefer failing first, then provide patches to make them pass."

*Bundle as* `/write-tests payments`.

## Perf Triage Without Yolo Optimizations
"Profile the hot path in `orders/views.py` or a critical Celery task in `orders/tasks.py`. Identify 2 bottlenecks with line refs, estimate complexity, and propose the smallest safe improvement. Don’t micro-optimize; aim for p95 wins."

## Frontend Event Hygiene
"Scan modified React components. Ensure analytics events map to @file:analytics/events.md. Generate a diff to add missing events and assert payload shapes in tests."

## PR Ready-to-Merge Summary
"Summarize this PR in 5 bullets: problem, approach, risks, tests, rollout. If risky, suggest a feature flag and rollback plan."