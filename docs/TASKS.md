# BookLeaf Author Support Portal — Tasks, Phases & Milestones

**Companion documents:** `../AGENTS.md` (coding agent instructions), `../README.md` (project overview), `SOLUTION_PLAN.md` (architecture), `ACTION_PLAN.md` (priorities and dependencies), `TOOLING.md` (stack inventory)

**Status:** All tasks are `TODO`. Nothing is marked in progress or done yet.

---

## 1. How to Use This Document

- Tasks are intentionally small: **S** = under 2 hours, **M** = 2-4 hours, **L** = 4-6 hours.
- Task IDs are stable. Do not renumber them; the action plan references these IDs.
- Work is organized into phases with a milestone at the end of each phase.
- A milestone is complete only when all of its tasks are `DONE` and its acceptance criteria pass.
- Dependencies and priority are maintained in `ACTION_PLAN.md`. This document is the task inventory.
- Mark a task `DONE` only after its acceptance is met, lint/typecheck/tests pass, and any affected documentation is updated.

**Status values:** `TODO`, `IN_PROGRESS`, `BLOCKED`, `DONE`, `CANCELLED`

---

## 2. Progress Summary

| Phase | Milestone | Task range | Tasks | Done | Status |
|---|---|---|---|---|---|
| 0 | M0 — Foundation Ready | T001-T008 | 8 | 0 | TODO |
| 1 | M1 — Data Layer Ready | T009-T022 | 14 | 0 | TODO |
| 2 | M2 — Auth Ready | T023-T029 | 7 | 0 | TODO |
| 3 | M3 — Author Portal MVP | T030-T042 | 13 | 0 | TODO |
| 4 | M4 — Admin Portal MVP | T043-T056 | 14 | 0 | TODO |
| 5 | M5 — AI Pipeline Ready | T057-T078 | 22 | 0 | TODO |
| 6 | M6 — Real-Time Ready | T079-T088 | 10 | 0 | TODO |
| 7 | M7 — Quality Gate | T089-T101 | 13 | 0 | TODO |
| 8 | M8 — Submission Ready | T102-T111 | 10 | 0 | TODO |
| **Total** | | **T001-T111** | **111** | **0** | **TODO** |

---

## 3. Milestones

| Milestone | Name | Exit criteria | Status |
|---|---|---|---|
| M0 | Foundation Ready | Workspace installs; API boots; Angular builds; lint and typecheck pass; CI skeleton runs; `.env.example` is complete; Docker/Compose skeleton exists. | TODO |
| M1 | Data Layer Ready | All operational tables and indexes exist in memory; repositories work; deterministic seed data loads; demo reset works; Problem Details and trace IDs are consistent; repository tests pass. | TODO |
| M2 | Auth Ready | Author and admin can log in; refresh rotation and logout work; protected routes reject anonymous users; authors cannot read other authors' data; frontend auth and route guards work. | TODO |
| M3 | Author Portal MVP | Author sees books and royalties; creates a ticket against a book or account; sees own tickets; reads public admin replies; replies and reopens; author e2e happy path passes. | TODO |
| M4 | Admin Portal MVP | Admin sees a filtered, prioritized queue; opens a ticket; changes status, category, priority, assignee; sends a public reply; adds an internal note; audit events are recorded; manual-reply e2e passes. | TODO |
| M5 | AI Pipeline Ready | Policies are indexed; classification and priority work with fallback; draft is grounded and tone-compliant; AI artifacts and telemetry persist; AI-disabled mode works; golden-set baseline is recorded. | TODO |
| M6 | Real-Time Ready | Admin reply reaches the author without refresh; author events are isolated; internal notes never reach authors; reconnect and replay work; polling fallback works; real-time tests pass. | TODO |
| M7 | Quality Gate | Security headers, rate limits, redaction, and authorization tests pass; prompt-injection tests pass; unit/integration/e2e suites pass; accessibility and load checks are recorded; no high/critical dependency or secret findings. | TODO |
| M8 | Submission Ready | Docker Compose runs the full stack; CI is green; OpenAPI and generated client are validated; README and docs are complete; demo deployment works; demo script is rehearsed; release is tagged. | TODO |

---

## 4. Phase 0 — Foundation

**Goal:** Create a reproducible monorepo that both applications and the delivery pipeline can build from.

| ID | Task | Size | Status |
|---|---|---|---|
| T001 | Initialize Git repository, workspace folders, `.gitignore`, `.editorconfig`, and line-ending rules | S | TODO |
| T002 | Scaffold NestJS API with strict TypeScript and baseline module structure | M | TODO |
| T003 | Scaffold Angular app with strict TypeScript, standalone components, routing, and SCSS | M | TODO |
| T004 | Add shared contracts package for enums, constants, and shared API types plus TypeScript path config | S | TODO |
| T005 | Configure ESLint, Prettier, root scripts, and GitHub Actions CI skeleton | M | TODO |
| T006 | Add validated environment configuration and a complete `.env.example` | S | TODO |
| T007 | Add Dockerfile, Compose, and Nginx skeleton files | M | TODO |
| T008 | Add README skeleton, local setup steps, and PR template | S | TODO |

---

## 5. Phase 1 — Data and Backend Foundation

**Goal:** Establish the domain model, in-memory database, repositories, seed data, and consistent API error handling.

| ID | Task | Size | Status |
|---|---|---|---|
| T009 | Define domain entities, value objects, and domain error types | M | TODO |
| T010 | Define repository ports and unit-of-work interfaces | S | TODO |
| T011 | Configure SQLite `:memory:` with Drizzle ORM and required pragmas | S | TODO |
| T012 | Define schema for users, refresh tokens, books, and royalty entries | M | TODO |
| T013 | Define schema for tickets, messages, notes, events, AI artifacts, feedback, and attachments | M | TODO |
| T014 | Add indexes, foreign keys, and constraints for queue and ownership queries | S | TODO |
| T015 | Implement user, book, and royalty repositories | M | TODO |
| T016 | Implement ticket, message, note, and event repositories | M | TODO |
| T017 | Implement refresh-token, AI-artifact, and feedback repositories | M | TODO |
| T018 | Implement transaction helper and domain-error-to-HTTP mapping | M | TODO |
| T019 | Add global validation pipe, exception filter, Problem Details shape, and trace IDs | M | TODO |
| T020 | Add Pino structured logging with redaction and health endpoints | M | TODO |
| T021 | Create deterministic seed data for users, books, royalty ledgers, and tickets | M | TODO |
| T022 | Add idempotent seed-on-boot, demo reset, and repository/seed tests | M | TODO |

---

## 6. Phase 2 — Authentication and RBAC

**Goal:** Secure the API and establish author/admin identity, isolation, and frontend session handling.

| ID | Task | Size | Status |
|---|---|---|---|
| T023 | Implement Argon2id password hashing and verification service | S | TODO |
| T024 | Implement login endpoint, auth DTOs, access JWT service, and auth guard | M | TODO |
| T025 | Implement refresh-token rotation, reuse detection, and refresh/logout/me endpoints | M | TODO |
| T026 | Implement public/role/current-user decorators, role guard, and ownership checks | M | TODO |
| T027 | Add auth rate limiting and login lockout | S | TODO |
| T028 | Add auth, RBAC, and IDOR integration tests | M | TODO |
| T029 | Build Angular login page, AuthStore, auth interceptor with queued refresh, and route guards | M | TODO |

---

## 7. Phase 3 — Author Portal

**Goal:** Deliver the complete author-facing experience for books, royalties, ticket submission, and ticket tracking.

| ID | Task | Size | Status |
|---|---|---|---|
| T030 | Implement `GET /me/books` and `GET /me/books/:id` with derived royalty totals and breakdown | M | TODO |
| T031 | Implement `POST /tickets` with validation, idempotency, and book ownership | M | TODO |
| T032 | Implement `GET /tickets` and `GET /tickets/:id` returning public messages only | M | TODO |
| T033 | Implement author reply and reopen endpoints | M | TODO |
| T034 | Implement attachment metadata endpoint and validation (bonus) | S | TODO |
| T035 | Build app shell, navigation, theme, and role-based routes | M | TODO |
| T036 | Build author dashboard summary and books views | M | TODO |
| T037 | Build book detail and royalty breakdown view | S | TODO |
| T038 | Build ticket creation form with book dropdown and attachment UI | M | TODO |
| T039 | Build My Tickets list and ticket detail message thread | M | TODO |
| T040 | Wire author reply/reopen and add loading, empty, and error states | M | TODO |
| T041 | Add responsive layout and accessibility pass for author pages | S | TODO |
| T042 | Add author portal end-to-end happy-path test | M | TODO |

---

## 8. Phase 4 — Admin Portal and Ticket Lifecycle

**Goal:** Give the operations team a complete triage and response workspace, with manual response working before AI is introduced.

| ID | Task | Size | Status |
|---|---|---|---|
| T043 | Implement admin ticket queue with filters, sorting, pagination, and search | L | TODO |
| T044 | Implement priority/SLA ordering and the needs-attention preset | S | TODO |
| T045 | Implement admin ticket detail with internal notes and AI artifact placeholders | M | TODO |
| T046 | Implement ticket status state machine and status update endpoint | M | TODO |
| T047 | Implement category/priority overrides and assignment/self-assign with audit | M | TODO |
| T048 | Implement admin public reply and internal notes endpoints | M | TODO |
| T049 | Implement audit event writer for all ticket mutations | M | TODO |
| T050 | Add admin backend integration tests for queue, lifecycle, and RBAC | M | TODO |
| T051 | Build admin queue page with filters, SLA highlights, and pagination | L | TODO |
| T052 | Build admin ticket detail layout and metadata panel | M | TODO |
| T053 | Build status, category, priority, and assignee controls with version checks | M | TODO |
| T054 | Build public reply composer and internal notes panel | M | TODO |
| T055 | Build AI panel placeholder and admin loading/error/conflict states | M | TODO |
| T056 | Add admin responsive/accessibility pass and manual-reply end-to-end test | M | TODO |

---

## 9. Phase 5 — AI and Knowledge Base

**Goal:** Deliver grounded, human-reviewed AI classification, priority, and draft generation with deterministic fallbacks.

| ID | Task | Size | Status |
|---|---|---|---|
| T057 | Implement policy document loader for the six BookLeaf policy documents | S | TODO |
| T058 | Implement heading/bullet-aware splitter, metadata, and KB version hash | M | TODO |
| T059 | Implement embeddings and in-memory vector store initialization at boot | M | TODO |
| T060 | Implement keyword fallback and hybrid category-filtered retrieval with token cap | M | TODO |
| T061 | Define `LlmPort`, provider-neutral request/response types, and deterministic mock provider | M | TODO |
| T062 | Implement OpenAI adapter with timeout and token telemetry | M | TODO |
| T063 | Implement Anthropic fallback adapter | M | TODO |
| T064 | Define classification/priority Zod schema and prompt v1 | M | TODO |
| T065 | Implement classification/priority node with schema validation and repair retry | M | TODO |
| T066 | Implement rule-based classifier fallback | M | TODO |
| T067 | Implement deterministic priority guardrails and SLA calculation | M | TODO |
| T068 | Write draft prompt v1 with tone, facts, policy excerpts, and safety rules | M | TODO |
| T069 | Implement draft generation node and template fallback | M | TODO |
| T070 | Implement grounding, numeric, and tone validator with repair pass | M | TODO |
| T071 | Build LangGraph enrichment graph from classify through persist | L | TODO |
| T072 | Persist AI artifacts and telemetry, and add the feedback endpoint | M | TODO |
| T073 | Implement async AI queue with bounded concurrency, retries, timeout, and circuit breaker | L | TODO |
| T074 | Implement AI-disabled mode and fallback UX states | M | TODO |
| T075 | Wire AI recommendations and draft panel into the admin ticket view | L | TODO |
| T076 | Implement draft regeneration with admin guidance and rate limit | M | TODO |
| T077 | Create golden-set fixtures and the AI evaluation script | M | TODO |
| T078 | Add AI unit/contract tests and record the golden-set baseline | M | TODO |

---

## 10. Phase 6 — Real-Time Communication

**Goal:** Push ticket changes to the correct author or admin immediately, with safe authorization, replay, and fallback.

| ID | Task | Size | Status |
|---|---|---|---|
| T079 | Define domain event types and event-bus port | S | TODO |
| T080 | Append all ticket mutations to the event log with monotonic event IDs | M | TODO |
| T081 | Implement SSE hub with per-user and admin channels | M | TODO |
| T082 | Implement stream-token endpoint with single-use validation | S | TODO |
| T083 | Implement SSE controller with heartbeat and `Last-Event-ID` replay | M | TODO |
| T084 | Enforce channel authorization and exclude internal notes from author streams | M | TODO |
| T085 | Build frontend SSE service with token refresh, reconnect, and dedupe | M | TODO |
| T086 | Integrate live updates into author and admin stores | M | TODO |
| T087 | Add polling fallback, connection caps, and cleanup | M | TODO |
| T088 | Add real-time integration/e2e tests and an internal-note leak test | M | TODO |

---

## 11. Phase 7 — Security, Quality, and Testing

**Goal:** Prove the system is safe, isolated, reliable, accessible, and measurable before submission.

| ID | Task | Size | Status |
|---|---|---|---|
| T089 | Add Helmet, CSP, CORS allowlist, and compression configuration | S | TODO |
| T090 | Add global, ticket-creation, and AI-regeneration rate limits | S | TODO |
| T091 | Add PII redaction to logs and AI telemetry | S | TODO |
| T092 | Validate attachment upload type, size, and magic bytes (bonus) | S | TODO |
| T093 | Add prompt-injection and output-safety tests | M | TODO |
| T094 | Complete the RBAC/IDOR authorization matrix tests | M | TODO |
| T095 | Add internal-note leakage tests across API and SSE | S | TODO |
| T096 | Add ticket lifecycle, idempotency, and state-transition tests | M | TODO |
| T097 | Add OpenAPI contract validation tests | S | TODO |
| T098 | Add frontend unit tests for auth, guards, stores, and SSE | M | TODO |
| T099 | Write Playwright e2e for the full AI flow and the AI-disabled flow | L | TODO |
| T100 | Add load-test scripts, accessibility audit, and dependency/secret scans | M | TODO |
| T101 | Verify demo reset/seed determinism and run a final bug bash | M | TODO |

---

## 12. Phase 8 — Deployment, Documentation, and Demo

**Goal:** Package, document, deploy, and rehearse the complete submission.

| ID | Task | Size | Status |
|---|---|---|---|
| T102 | Finalize Nginx SPA fallback, reverse proxy, and SSE buffering settings | S | TODO |
| T103 | Finalize multi-stage API Dockerfile with non-root user and healthcheck | M | TODO |
| T104 | Finalize multi-stage web Dockerfile | S | TODO |
| T105 | Finalize Docker Compose with healthchecks and environment wiring | S | TODO |
| T106 | Complete CI: tests, AI golden-set run, builds, Docker, and scans | M | TODO |
| T107 | Add OpenAPI generation and Angular client drift check | M | TODO |
| T108 | Complete README, environment/credentials, architecture links, and limitations | M | TODO |
| T109 | Deploy the single-instance demo and configure secrets and health checks | M | TODO |
| T110 | Verify deployed flows and rehearse the five-minute demo script | M | TODO |
| T111 | Tag `v1.0.0` and complete the submission checklist | S | TODO |

---

## 13. Definition of Done

A task is `DONE` only when all applicable conditions are true:

- The task's described behavior works locally and matches its acceptance criteria.
- TypeScript compiles with strict mode; lint and formatting pass.
- Relevant unit, integration, or e2e tests pass.
- API changes are reflected in Swagger/OpenAPI and the generated client.
- AI changes have mock/contract tests and do not break the golden-set baseline.
- UI changes include loading, empty, error, and unauthorized states where relevant.
- Security and authorization checks are enforced server-side.
- Logs do not contain secrets or unnecessary PII.
- Documentation is updated if setup, configuration, API, or behavior changed.
- The task status is changed to `DONE` in this document.

## 14. Working Rules

1. Follow the dependency order in `ACTION_PLAN.md`; do not start a blocked task.
2. Prefer the highest-priority ready task. P0 before P1 before P2.
3. Keep tasks small. If a task grows beyond one focused day, split it and add new stable IDs.
4. End every phase with its milestone checks; do not carry unverified foundation work forward.
5. Never mark a milestone done because the calendar says so. Mark it done only when its exit criteria pass.
6. Keep the manual workflow working at all times: ticket creation, admin reply, and author visibility must survive AI and real-time failures.
7. Update this document and `ACTION_PLAN.md` together when scope changes.

