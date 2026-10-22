# BookLeaf Author Support & Communication Portal

A two-sided support and communication portal for BookLeaf, a self-publishing company.

- **Authors** can log in, view their books and royalties, create support tickets, reply, reopen resolved tickets, and read public replies.
- **Support admins** get a prioritized queue, AI-assisted category and priority suggestions, a grounded AI draft, public replies, internal notes, assignment, and status management.
- **AI is optional and human-approved.** It never sends a response automatically and never blocks ticket creation or manual support.
- **Real-time updates** are delivered to the browser over Server-Sent Events (SSE).

> **Status:** planning is complete; implementation has not started. This repository currently contains documentation only. There are 111 tasks across 9 phases and 9 milestones, all marked `TODO`. The first task is `T001`.

---

## How to Read This Repository

If you are new to the project, read in this order:

1. [AGENTS.md](AGENTS.md) — canonical instructions for coding agents, architecture constraints, and working conventions.
2. [docs/Requirements.md](docs/Requirements.md) — the assignment requirements.
3. [docs/companyOverview.md](docs/companyOverview.md) — BookLeaf context.
4. [docs/SOLUTION_PLAN.md](docs/SOLUTION_PLAN.md) — architecture, data model, API, AI design, security, testing, and delivery plan.
5. [docs/TASKS.md](docs/TASKS.md) — task inventory, current status, phases, milestones, and Definition of Done.
6. [docs/ACTION_PLAN.md](docs/ACTION_PLAN.md) — priority, dependencies, execution waves, and critical path.
7. [docs/TOOLING.md](docs/TOOLING.md) — approved libraries, tools, versions, and rejected alternatives.
8. [docs/policy_docs/](docs/policy_docs/) and [docs/examples/](docs/examples/) — policy content and demo/calibration examples, only when relevant to the task.

**Short review path:** README → Requirements → Solution Plan sections 1-6 and 18 → Tasks summary → Action Plan critical path.

**Implementation path:** AGENTS → Tasks → Action Plan → relevant Solution Plan section → Tooling.

---

## Source of Truth

| Topic | Document |
|---|---|
| Architecture and design | [docs/SOLUTION_PLAN.md](docs/SOLUTION_PLAN.md) |
| Task status and Definition of Done | [docs/TASKS.md](docs/TASKS.md) |
| Priority and dependencies | [docs/ACTION_PLAN.md](docs/ACTION_PLAN.md) |
| Approved stack | [docs/TOOLING.md](docs/TOOLING.md) |
| BookLeaf policies | [docs/policy_docs/](docs/policy_docs/) |
| Demo data and AI calibration | [docs/examples/](docs/examples/) |
| Coding-agent instructions | [AGENTS.md](AGENTS.md) |

If documents disagree, stop and reconcile them. Policy documents describe BookLeaf’s actual rules; do not rewrite them to fit the implementation.

---

## Planned Architecture

| Area | Choice |
|---|---|
| Frontend | Angular, standalone components, Angular Material, signals plus RxJS |
| Backend | NestJS modular monolith with domain/application/infrastructure boundaries |
| Operational data | SQLite `:memory:` with Drizzle ORM |
| Semantic search | In-memory LangChain vector store |
| AI orchestration | LangGraph/LangChain behind an internal `LlmPort` |
| Cache and jobs | In-process `lru-cache` and an in-process AI queue |
| Real-time | Server-Sent Events (SSE) with replay and polling fallback |
| Auth | Short-lived JWT in memory, rotating refresh token in an HttpOnly cookie, single-use SSE stream token |
| Deployment | One persistent, single-instance container behind Nginx |

The in-memory database makes this deliberately a single-instance application. The repository and event interfaces keep a PostgreSQL/Redis production path open without introducing those dependencies now.

---

## Repository Layout

```text
bookleaf/
  AGENTS.md                 coding-agent instructions
  README.md                 this file
  docs/
    Requirements.md         assignment requirements
    companyOverview.md      company context
    SOLUTION_PLAN.md        architecture and decisions
    TASKS.md                tasks, phases, milestones, status
    ACTION_PLAN.md          priorities and dependencies
    TOOLING.md              approved stack inventory
    policy_docs/            BookLeaf policy content
    examples/               demo seed data and AI calibration examples
  apps/                     Angular web app and NestJS API (to be scaffolded)
  packages/                 shared contracts (to be scaffolded)
  infra/                    Docker and Nginx files (to be scaffolded)
```

Only `AGENTS.md`, `README.md`, and `docs/` exist today.

---

## Current Status

- Documentation and planning are complete.
- Application code, package manifests, and infrastructure files do not exist yet.
- All 111 tasks are `TODO`; none are in progress.
- Start with `T001` in [docs/TASKS.md](docs/TASKS.md), following [docs/ACTION_PLAN.md](docs/ACTION_PLAN.md).
- Do not invent setup or verification commands before the workspace is scaffolded.

---

## Running, Testing, Building, and Shipping

These sections will be completed once the workspace exists.

### Local Development

To be added after `T001` and the initial workspace scaffold.

### Testing

To be added when the API and web test runners are configured.

### Build

To be added when the production build scripts exist.

### Shipping

To be added with the Docker, Nginx, CI, and deployment steps in phases 7-8.

---

## Important Constraints

- Use demo data only. Do not add real author, bank, or personal data.
- AI output always requires human review; never auto-send.
- Authors must never receive another author’s data, internal notes, or admin-only fields.
- Money is stored as integer paise, never floating point.
- Access and refresh tokens must never be stored in `localStorage` or `sessionStorage`.
- The application must remain usable with `AI_ENABLED=false`.
- Follow [AGENTS.md](AGENTS.md) for all implementation work.
