# Action Plan — Priorities, Dependencies & Execution Order

**Companion documents:** `../AGENTS.md` (coding agent instructions), `../README.md` (project overview), `SOLUTION_PLAN.md` (architecture), `TASKS.md` (task inventory), `TOOLING.md` (stack inventory)

**Current state:** All 111 tasks are `TODO`. Start with `T001`.

---

## 1. How to Use This Plan

1. Pick the highest-priority task whose dependencies are all `DONE`.
2. If the highest-priority task is blocked, choose the next ready task at the same priority.
3. Never start a task whose dependency is incomplete; priority does not override a hard dependency.
4. Update `TASKS.md` to `IN_PROGRESS` when starting and `DONE` only when its Definition of Done is met.
5. Re-check the milestone gate at the end of each phase before moving to the next phase.

**Dependency notation:** task IDs separated by commas. `—` means no dependency.
**Waves:** W0-W8 are the recommended single-developer order. Some tasks can run in parallel, as noted later.

---

## 2. Priority Legend

| Priority | Meaning | Rule |
|---|---|---|
| **P0** | Release blocker or critical-path enabler. The vertical slice, security boundary, or deployment cannot work without it. | Do first among ready tasks in its phase. Escalate if blocked. |
| **P1** | Required assignment functionality or quality gate. Needed for the complete submission, but a P0 milestone can proceed briefly with a stub or manual workaround. | Do after P0 work in the same phase. |
| **P2** | Bonus, optional, or deliberately deferred. Nice to demonstrate, but cut first under time pressure. | Only after all P0 and P1 work is stable. |

**Priority summary**

| Phase | P0 | P1 | P2 | Total |
|---|---|---|---|---|
| 0 — Foundation | 5 | 3 | 0 | 8 |
| 1 — Data | 8 | 6 | 0 | 14 |
| 2 — Auth | 3 | 4 | 0 | 7 |
| 3 — Author portal | 7 | 5 | 1 | 13 |
| 4 — Admin portal | 9 | 5 | 0 | 14 |
| 5 — AI | 15 | 6 | 1 | 22 |
| 6 — Real-time | 8 | 2 | 0 | 10 |
| 7 — Quality | 5 | 7 | 1 | 13 |
| 8 — Delivery | 8 | 2 | 0 | 10 |
| **Total** | **68** | **40** | **3** | **111** |

The P0 count is high because this is a full-stack assignment where the foundation, core workflows, AI path, real-time path, and deployment are all part of the required vertical slice.

---

## 3. Execution Waves

| Wave | Goal | Tasks | Milestone |
|---|---|---|---|
| W0 | Foundation and reproducible workspace | T001-T008 | M0 |
| W1 | Domain, in-memory data layer, seed, API errors | T009-T022 | M1 |
| W2 | Authentication, RBAC, frontend session handling | T023-T029 | M2 |
| W3 | Author books, royalties, tickets, replies | T030-T042 | M3 |
| W4 | Admin queue, lifecycle, notes, assignment, manual reply | T043-T056 | M4 |
| W5 | Knowledge base, classification, priority, drafting, fallbacks | T057-T078 | M5 |
| W6 | SSE, stream tokens, replay, live frontend updates | T079-T088 | M6 |
| W7 | Security, authorization tests, e2e, performance, accessibility | T089-T101 | M7 |
| W8 | Docker, CI, docs, deployment, demo, release | T102-T111 | M8 |

**Parallelization guidance**

- With two developers: split frontend and backend at W3. Backend continues T030-T034 while frontend starts T035, T038, T039 against agreed DTOs.
- AI knowledge-base tasks T057-T064 can begin after T006 and T009 while W3 or W4 is in progress, provided the AI module does not block the author or admin milestones.
- Real-time work T079-T084 can begin after T049 while the AI panel T075 is being finished.
- Do not parallelize schema changes with repository implementation unless interfaces are already fixed.

---

## 4. Critical Path

The shortest path to a demonstrable end-to-end product, ignoring polish:

```text
T001 -> T002 -> T006 -> T009 -> T011 -> T013 -> T016 -> T019
     -> T024 -> T026 -> T031 -> T032 -> T035 -> T038 -> T039
     -> T043 -> T046 -> T048 -> T049
     -> T057 -> T058 -> T059 -> T061 -> T064 -> T065 -> T067
     -> T068 -> T069 -> T070 -> T071 -> T072 -> T075
     -> T079 -> T080 -> T081 -> T083 -> T084 -> T085 -> T086
     -> T089 -> T094 -> T095 -> T096 -> T099
     -> T102 -> T105 -> T106 -> T108 -> T110 -> T111
```

**Interpretation:** if a task is not on this chain, it is still required for the full assignment, but it can be scheduled around the critical path. The chain prioritizes a working author-to-admin-to-author loop with grounded AI and safe real-time delivery.

---

## 5. First 15 Tasks

| Order | Task | Why now |
|---|---|---|
| 1 | T001 | Nothing can be committed or reproduced without the workspace. |
| 2 | T002 | The backend must boot before data, auth, or AI work can start. |
| 3 | T003 | The frontend can be scaffolded in parallel with T002. |
| 4 | T005 | Lint, formatting, and CI must exist before the codebase grows. |
| 5 | T006 | Validated configuration is required by the database and AI layers. |
| 6 | T004 | Shared enums prevent frontend/backend drift. |
| 7 | T009 | Domain entities drive the schema and repository contracts. |
| 8 | T011 | The in-memory database is the foundation of every feature. |
| 9 | T012 | Users, books, and royalty data are the first read model. |
| 10 | T013 | Tickets and events are the core operational model. |
| 11 | T014 | Indexes and constraints must exist before queue queries. |
| 12 | T015 | User/book/royalty repositories enable seed and author views. |
| 13 | T016 | Ticket repositories enable the core support workflow. |
| 14 | T018 | Transactions and error mapping are needed before write endpoints. |
| 15 | T019 | Consistent validation and Problem Details apply to every route. |

After T019, proceed to T021 and T022 for seed data, then W2 authentication.

---

## 6. Full Priority and Dependency Table

### Phase 0 — Foundation

| ID | Task | Priority | Depends on | Wave |
|---|---|---|---|---|
| T001 | Initialize Git, workspace folders, ignore/editor config | P0 | — | W0 |
| T002 | Scaffold NestJS API with strict TypeScript | P0 | T001 | W0 |
| T003 | Scaffold Angular app with strict TypeScript | P0 | T001 | W0 |
| T004 | Add shared contracts package and path config | P1 | T001, T002, T003 | W0 |
| T005 | Configure ESLint, Prettier, root scripts, CI skeleton | P0 | T002, T003 | W0 |
| T006 | Add validated env config and `.env.example` | P0 | T002 | W0 |
| T007 | Add Docker, Compose, and Nginx skeleton | P1 | T002, T003 | W0 |
| T008 | Add README skeleton and PR template | P1 | T001 | W0 |

### Phase 1 — Data and Backend Foundation

| ID | Task | Priority | Depends on | Wave |
|---|---|---|---|---|
| T009 | Define domain entities, value objects, and errors | P0 | T002 | W1 |
| T010 | Define repository ports and unit-of-work interfaces | P1 | T009 | W1 |
| T011 | Configure SQLite `:memory:` with Drizzle | P0 | T002, T006 | W1 |
| T012 | Define schema for users, tokens, books, royalties | P0 | T011, T009 | W1 |
| T013 | Define schema for tickets, messages, notes, events, AI | P0 | T011, T009 | W1 |
| T014 | Add indexes, foreign keys, and constraints | P1 | T012, T013 | W1 |
| T015 | Implement user, book, and royalty repositories | P1 | T012, T010 | W1 |
| T016 | Implement ticket, message, note, and event repositories | P0 | T013, T010 | W1 |
| T017 | Implement refresh-token, AI-artifact, and feedback repositories | P1 | T013, T010 | W1 |
| T018 | Implement transaction helper and error mapping | P0 | T010, T009 | W1 |
| T019 | Add validation pipe, exception filter, Problem Details, trace IDs | P0 | T002, T009 | W1 |
| T020 | Add Pino logging with redaction and health endpoints | P1 | T002, T006 | W1 |
| T021 | Create deterministic seed data | P0 | T012, T013, T015, T016 | W1 |
| T022 | Add idempotent seed-on-boot, demo reset, and repository tests | P1 | T021, T018 | W1 |

### Phase 2 — Authentication and RBAC

| ID | Task | Priority | Depends on | Wave |
|---|---|---|---|---|
| T023 | Implement Argon2id password service | P0 | T015 | W2 |
| T024 | Implement login, access JWT, and auth guard | P0 | T023, T019, T006 | W2 |
| T025 | Implement refresh rotation, reuse detection, refresh/logout/me | P1 | T024, T017 | W2 |
| T026 | Implement role/public/current-user guards and ownership checks | P0 | T024, T010 | W2 |
| T027 | Add auth rate limiting and login lockout | P1 | T024 | W2 |
| T028 | Add auth, RBAC, and IDOR integration tests | P1 | T024, T025, T026 | W2 |
| T029 | Build Angular login, AuthStore, auth interceptor, and guards | P1 | T003, T024, T025 | W2 |

### Phase 3 — Author Portal

| ID | Task | Priority | Depends on | Wave |
|---|---|---|---|---|
| T030 | Implement `/me/books` and book detail with royalty breakdown | P0 | T015, T026 | W3 |
| T031 | Implement ticket creation with validation, idempotency, ownership | P0 | T016, T018, T026 | W3 |
| T032 | Implement author ticket list and detail with public messages only | P0 | T016, T026 | W3 |
| T033 | Implement author reply and reopen endpoints | P1 | T032, T018 | W3 |
| T034 | Implement attachment metadata endpoint and validation (bonus) | P2 | T031 | W3 |
| T035 | Build app shell, navigation, theme, and role-based routes | P0 | T003, T029 | W3 |
| T036 | Build author dashboard summary and books views | P0 | T035, T030 | W3 |
| T037 | Build book detail and royalty breakdown view | P1 | T036, T030 | W3 |
| T038 | Build ticket creation form with book dropdown and attachment UI | P0 | T035, T031 | W3 |
| T039 | Build My Tickets list and ticket detail thread | P0 | T035, T032 | W3 |
| T040 | Wire author reply/reopen and loading/error/empty states | P1 | T038, T039, T033 | W3 |
| T041 | Add author responsive layout and accessibility pass | P1 | T036, T037, T038, T039, T040 | W3 |
| T042 | Add author portal e2e happy path | P1 | T040 | W3 |

### Phase 4 — Admin Portal and Ticket Lifecycle

| ID | Task | Priority | Depends on | Wave |
|---|---|---|---|---|
| T043 | Implement admin queue filters, sorting, pagination, and search | P0 | T016, T014, T026 | W4 |
| T044 | Implement priority/SLA ordering and needs-attention preset | P1 | T043 | W4 |
| T045 | Implement admin ticket detail with notes and AI artifacts | P0 | T016, T017, T026 | W4 |
| T046 | Implement ticket status state machine and update endpoint | P0 | T016, T018, T026 | W4 |
| T047 | Implement category/priority overrides and assignment with audit | P0 | T046 | W4 |
| T048 | Implement admin public reply and internal notes endpoints | P0 | T046, T016 | W4 |
| T049 | Implement audit event writer for ticket mutations | P0 | T016, T018 | W4 |
| T050 | Add admin backend integration tests | P1 | T043, T044, T045, T046, T047, T048, T049 | W4 |
| T051 | Build admin queue page with filters, SLA highlights, pagination | P0 | T035, T043, T044 | W4 |
| T052 | Build admin ticket detail layout and metadata panel | P0 | T045, T051 | W4 |
| T053 | Build status/category/priority/assignee controls with version checks | P1 | T046, T047, T052 | W4 |
| T054 | Build public reply composer and internal notes panel | P0 | T048, T052 | W4 |
| T055 | Build AI panel placeholder and admin loading/error/conflict states | P1 | T052 | W4 |
| T056 | Add admin responsive/accessibility pass and manual-reply e2e | P1 | T051, T052, T053, T054, T055 | W4 |

### Phase 5 — AI and Knowledge Base

| ID | Task | Priority | Depends on | Wave |
|---|---|---|---|---|
| T057 | Implement policy document loader for six policies | P0 | T002, T006 | W5 |
| T058 | Implement heading/bullet splitter, metadata, and KB version hash | P0 | T057 | W5 |
| T059 | Implement embeddings and in-memory vector store at boot | P0 | T058, T006 | W5 |
| T060 | Implement keyword fallback and hybrid category-filtered retrieval | P1 | T058, T059 | W5 |
| T061 | Define `LlmPort`, provider-neutral contracts, and mock provider | P0 | T009, T006 | W5 |
| T062 | Implement OpenAI adapter with timeout and token telemetry | P0 | T061 | W5 |
| T063 | Implement Anthropic fallback adapter | P2 | T061 | W5 |
| T064 | Define classification/priority schema and prompt v1 | P0 | T061 | W5 |
| T065 | Implement classification/priority node with validation and repair | P0 | T062, T064 | W5 |
| T066 | Implement rule-based classifier fallback | P1 | T061 | W5 |
| T067 | Implement deterministic priority guardrails and SLA calculation | P0 | T009, T066 | W5 |
| T068 | Write draft prompt v1 with tone, facts, policy, and safety rules | P0 | T060, T061 | W5 |
| T069 | Implement draft generation node and template fallback | P0 | T065, T068 | W5 |
| T070 | Implement grounding, numeric, and tone validator with repair | P0 | T069 | W5 |
| T071 | Build LangGraph enrichment graph | P0 | T065, T067, T069, T070 | W5 |
| T072 | Persist AI artifacts/telemetry and add feedback endpoint | P0 | T071, T017, T045 | W5 |
| T073 | Implement async AI queue with concurrency, retries, timeout, breaker | P1 | T071, T016 | W5 |
| T074 | Implement AI-disabled mode and fallback UX states | P0 | T061, T071 | W5 |
| T075 | Wire AI recommendations and draft panel into admin ticket view | P0 | T055, T072 | W5 |
| T076 | Implement draft regeneration with guidance and rate limit | P1 | T075 | W5 |
| T077 | Create golden-set fixtures and AI evaluation script | P1 | T064, T070 | W5 |
| T078 | Add AI unit/contract tests and record golden-set baseline | P1 | T061, T071, T077 | W5 |

### Phase 6 — Real-Time Communication

| ID | Task | Priority | Depends on | Wave |
|---|---|---|---|---|
| T079 | Define domain event types and event-bus port | P0 | T016 | W6 |
| T080 | Append ticket mutations to event log with monotonic IDs | P0 | T049, T079 | W6 |
| T081 | Implement SSE hub with per-user and admin channels | P0 | T079 | W6 |
| T082 | Implement stream-token endpoint with single-use validation | P0 | T024, T081 | W6 |
| T083 | Implement SSE controller with heartbeat and replay | P0 | T080, T081, T082 | W6 |
| T084 | Enforce channel authorization and note exclusion | P0 | T081, T083 | W6 |
| T085 | Build frontend SSE service with token refresh, reconnect, dedupe | P0 | T029, T082, T083 | W6 |
| T086 | Integrate live updates into author and admin stores | P0 | T085, T039, T052 | W6 |
| T087 | Add polling fallback, connection caps, and cleanup | P1 | T085, T081 | W6 |
| T088 | Add real-time integration/e2e tests and note-leak test | P1 | T084, T086 | W6 |

### Phase 7 — Security, Quality, and Testing

| ID | Task | Priority | Depends on | Wave |
|---|---|---|---|---|
| T089 | Add Helmet, CSP, CORS allowlist, and compression | P0 | T002, T006 | W7 |
| T090 | Add global, ticket-creation, and AI-regeneration rate limits | P1 | T027, T076 | W7 |
| T091 | Add PII redaction to logs and AI telemetry | P1 | T020, T072 | W7 |
| T092 | Validate attachment upload type, size, and magic bytes (bonus) | P2 | T034 | W7 |
| T093 | Add prompt-injection and output-safety tests | P1 | T070, T078 | W7 |
| T094 | Complete RBAC/IDOR authorization matrix tests | P0 | T028, T050 | W7 |
| T095 | Add internal-note leakage tests across API and SSE | P0 | T084, T088 | W7 |
| T096 | Add ticket lifecycle, idempotency, and state-transition tests | P0 | T046, T047, T048, T049 | W7 |
| T097 | Add OpenAPI contract validation tests | P1 | T019, T043 | W7 |
| T098 | Add frontend unit tests for auth, guards, stores, and SSE | P1 | T029, T085 | W7 |
| T099 | Write Playwright e2e for full AI and AI-disabled flows | P0 | T075, T088 | W7 |
| T100 | Add load scripts, accessibility audit, and dependency/secret scans | P1 | T056, T083, T089 | W7 |
| T101 | Verify demo reset/seed determinism and run final bug bash | P1 | T022, T099 | W7 |

### Phase 8 — Deployment, Documentation, and Demo

| ID | Task | Priority | Depends on | Wave |
|---|---|---|---|---|
| T102 | Finalize Nginx SPA, proxy, and SSE buffering config | P0 | T007, T083 | W8 |
| T103 | Finalize API Dockerfile with non-root user and healthcheck | P0 | T007, T002 | W8 |
| T104 | Finalize web Dockerfile | P0 | T007, T003 | W8 |
| T105 | Finalize Docker Compose with healthchecks and env wiring | P0 | T102, T103, T104 | W8 |
| T106 | Complete CI: tests, golden eval, builds, Docker, scans | P0 | T005, T100 | W8 |
| T107 | Add OpenAPI generation and Angular client drift check | P1 | T097, T106 | W8 |
| T108 | Complete README, env/credentials, architecture links, limitations | P0 | T008, T106 | W8 |
| T109 | Deploy single-instance demo with secrets and health checks | P1 | T105, T106 | W8 |
| T110 | Verify deployed flows and rehearse the demo script | P0 | T109, T099 | W8 |
| T111 | Tag `v1.0.0` and complete submission checklist | P0 | T108, T110 | W8 |

---

## 7. Milestone Gates

| Gate | Must pass before leaving the phase | Exit signal |
|---|---|---|
| M0 | T001-T008; install, lint, typecheck, API boot, Angular build, CI skeleton | Clean clone builds |
| M1 | T009-T022; schema, repositories, seed, reset, validation/errors, health, repository tests | Data layer demoable without HTTP |
| M2 | T023-T029; login, refresh/logout, RBAC, IDOR tests, frontend auth | Two roles isolated |
| M3 | T030-T042; books/royalties, create/list/read/reply tickets, author e2e | Author workflow complete |
| M4 | T043-T056; queue, overrides, status, notes, assignment, manual reply, admin e2e | Manual support workflow complete |
| M5 | T057-T078; KB, classify, priority, draft, validators, graph, admin AI panel, fallback | AI draft reviewable and grounded |
| M6 | T079-T088; SSE, tokens, replay, authorization, live stores, real-time tests | Reply appears without refresh |
| M7 | T089-T101; security, authorization, lifecycle, e2e, accessibility, load, scans | Quality evidence complete |
| M8 | T102-T111; Compose, CI, docs, deployment, demo, release | Submission ready |

---

## 8. Scope Cut Order

If time runs short, cut in this order. Never cut security isolation, internal-note protection, or the end-to-end test.

1. **P2 first:** T034 (attachment metadata), T063 (Anthropic fallback), T092 (attachment validation).
2. **P1 polish:** T041, T056 (accessibility passes), T100 (load test), T107 (client drift check), T109 (hosted deploy if local Docker demo is acceptable).
3. **P1 extras:** T076 (regeneration guidance) and T087 (polling fallback if SSE is stable in the demo environment).
4. **Do not cut:** T089, T094, T095, T096, T099, T102-T106, T108, T110, T111.

If the AI provider is unavailable, keep T061/T072 and use the deterministic mock provider; do not remove the AI pipeline to save time.

---

## 9. Dependency Risks to Watch

| Risk | Affected tasks | Mitigation |
|---|---|---|
| Schema churn after repositories are written | T012-T017, T030-T054 | Freeze entities in T009 and review schema before T015. Add new columns through a small follow-up task. |
| Auth changed after frontend interceptor is built | T024-T029, T085 | Finalize token/cookie contract in T024 before T029. |
| AI prompt changes break the admin panel DTO | T064-T075 | Define the AI artifact response shape in T072 before T075. |
| SSE token design changes after frontend work | T082-T085 | Implement T082 before T085. |
| OpenAPI drift discovered late | T097, T107 | Generate the spec after admin endpoints stabilize at M4; run drift check in CI. |
| AI key unavailable | T062-T078 | Mock provider T061 is P0; AI-disabled mode T074 is P0. |
| Docker build fails on native SQLite | T103, T105 | Validate the API image at W8 before deploying; keep the container as the primary run path. |
| Demo state lost on platform restart | T109, T110 | Seed on boot T022; rehearse the reset flow T101. |

---

## 10. Status Update Rule

When a task is finished, update both documents:

- `TASKS.md`: set the task status to `DONE`, update the phase Done count, and update the milestone status if the gate passes.
- `ACTION_PLAN.md`: no status column is maintained here; the task inventory is the source of truth.

If a task is blocked, set it to `BLOCKED` in `TASKS.md` and record the blocking task ID in the task name or a short note. Resolve the blocker before starting dependent work.

