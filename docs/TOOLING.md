# Tooling & Library Inventory

**Companion documents:** `../AGENTS.md` (coding agent instructions), `../README.md` (project overview), `SOLUTION_PLAN.md` (architecture), `TASKS.md` (task inventory), `ACTION_PLAN.md` (priorities and dependencies)

**Status:** All items below are planned or optional; nothing is installed or configured yet.

---

## 1. Version and Dependency Policy

- **Node.js:** 22 LTS, pinned with `.nvmrc` / `.node-version`.
- **Package manager:** pnpm, pinned through the root `packageManager` field and Corepack.
- **Language:** TypeScript in strict mode everywhere.
- **Framework versions:** latest stable Angular and NestJS at scaffold time. Pin exact versions in `pnpm-lock.yaml`.
- **AI packages:** pin exact versions. LangChain and LangGraph change quickly; upgrades require the golden-set evaluation.
- **Dependency ranges:** exact versions for AI and infrastructure packages; caret ranges are acceptable only for low-risk dev tooling.
- **Lockfile:** committed. CI uses `pnpm install --frozen-lockfile`.
- **No global project dependencies:** everything is declared in the workspace. Only pnpm/Corepack and container tooling are installed globally.
- **Supply chain:** Dependabot, `pnpm audit`, Gitleaks, and optional Trivy/CodeQL in CI.
- **ESM-only utilities:** some packages such as `p-queue` and `file-type` may be ESM-only. Verify the import strategy at scaffold time and pin a compatible major instead of mixing module systems ad hoc.
- **Type definitions:** `@types/node`, `@types/express`, `@types/compression`, `@types/cookie-parser`, `@types/better-sqlite3`, and `@types/supertest` are dev dependencies as needed.

---

## 2. Runtime, Workspace, and Language

| Tool / Library | Purpose | Status |
|---|---|---|
| Node.js 22 LTS | Runtime for API, build tools, and scripts | Planned |
| pnpm workspaces | Monorepo package management and shared scripts | Planned |
| TypeScript 5.x (strict) | Type safety across API, web, contracts, and scripts | Planned |
| Corepack | Pin and invoke the pnpm version | Planned |
| `tsx` | Run seed, migration, and AI evaluation scripts without a full build | Planned |
| `cross-env` | Cross-platform environment variables in scripts | Optional |
| `dotenv` via `@nestjs/config` | Local environment loading | Planned |
| `zod` | Environment validation, AI structured-output schemas, shared runtime validation | Planned |
| `pnpm --parallel` | Run API and web dev servers together | Planned |
| Git + GitHub | Source control, pull requests, protected main branch | Planned |
| `.editorconfig` + Prettier | Consistent formatting, line endings, indentation | Planned |

---

## 3. Frontend — Angular

| Tool / Library | Purpose | Status |
|---|---|---|
| Angular (latest stable) | SPA framework for author and admin portals | Planned |
| Angular core packages (`@angular/core`, `common`, `forms`, `router`, `platform-browser`) | Framework runtime, forms, routing, and browser bootstrap | Planned |
| `@angular/animations` | Material motion and accessible transitions; noop animations in tests | Planned |
| Angular CLI | Scaffolding, build, dev server, budgets | Planned |
| Standalone components | Feature-oriented component composition | Planned |
| Angular Router | Lazy-loaded author/admin routes and guards | Planned |
| Angular Signals | Feature-level view state without a global store | Planned |
| RxJS | HTTP composition, SSE streams, debounce, cancellation | Planned |
| Reactive Forms | Typed ticket, login, and filter forms with validation | Planned |
| Angular HttpClient | REST client and interceptors | Planned |
| `@angular/material` | Accessible tables, dialogs, form fields, chips, menus, snackbars, tooltips | Planned |
| `@angular/cdk` | Virtual scroll, focus management, overlays, accessibility primitives | Planned |
| Angular Material theme + SCSS | BookLeaf visual theme, spacing, typography tokens | Planned |
| Native `EventSource` | SSE client with reconnect orchestration | Planned |
| Angular `DatePipe` / `Intl.NumberFormat` | Date and INR currency display | Planned |
| `ng-openapi-gen` | Generate typed Angular services/models from OpenAPI | Planned |
| `@hey-api/openapi-ts` | Fallback client generator if `ng-openapi-gen` blocks delivery | Optional fallback |
| Vitest + `@analogjs/vitest-angular` | Angular unit/component tests | Planned |
| `jsdom` | DOM environment for frontend unit tests | Planned |
| `@vitest/coverage-v8` | Coverage reporting | Planned |
| `@playwright/test` | Browser end-to-end tests | Planned |
| `@axe-core/playwright` | Automated accessibility checks in e2e | Planned |
| Angular CDK a11y utilities | Focus traps, live announcers, keyboard handling | Planned |
| Material Icons / inline SVG | Interface iconography | Planned |

**Frontend choices deliberately not used:** NgRx (too much boilerplate for this state size), Tailwind (mixing utility CSS with Material theming adds inconsistency), Axios (Angular HttpClient already provides interceptors), Socket.IO client (SSE is sufficient), chart libraries (no analytics requirement).

---

## 4. Backend — NestJS

| Tool / Library | Purpose | Status |
|---|---|---|
| NestJS (latest stable) | Modular API framework with DI, guards, pipes, interceptors | Planned |
| NestJS core packages (`@nestjs/common`, `@nestjs/core`) | Controllers, providers, modules, guards, pipes, interceptors | Planned |
| `@nestjs/platform-express` | HTTP adapter and Multer integration | Planned |
| `multer` | Optional attachment upload handling via the Express adapter | Optional |
| `@nestjs/config` | Environment-based configuration | Planned |
| `@nestjs/swagger` | OpenAPI 3 generation and Swagger UI | Planned |
| `@nestjs/jwt` | Access-token signing and verification | Planned |
| `@nestjs/throttler` | Global and endpoint-level rate limiting | Planned |
| `@nestjs/terminus` | Health and readiness endpoints | Planned |
| `@nestjs/event-emitter` | In-process domain event bus via EventEmitter2 | Planned |
| `@nestjs/testing` | Unit and integration test harness | Planned |
| Nest CLI | Build, watch mode, scaffolding | Planned |
| `class-validator` | DTO validation with whitelist and transformation | Planned |
| `class-transformer` | Request payload transformation and type coercion | Planned |
| `argon2` | Argon2id password hashing | Planned |
| `cookie-parser` | Parse the HttpOnly refresh-token cookie | Planned |
| `helmet` | Security headers and CSP | Planned |
| `compression` | Compress REST responses; disabled for SSE | Planned |
| `pino` + `nestjs-pino` | Structured JSON logging | Planned |
| `pino-pretty` | Readable local development logs | Planned |
| `reflect-metadata` | NestJS decorator/runtime metadata | Planned |
| `rxjs` | NestJS streams, SSE subjects, event composition | Planned |
| `uuidv7` | Sortable unique identifiers | Planned |
| `date-fns` | Quarter, payout, SLA, and date arithmetic | Planned |
| `p-queue` | Bounded concurrency for in-process AI jobs | Planned |
| `cockatiel` | Retry, timeout, and circuit-breaker policies | Planned |
| `js-tiktoken` | Token counting and context/output caps | Planned |
| `file-type` | Magic-byte validation for optional attachments | Optional |
| `sanitize-filename` | Safe attachment filenames | Optional |

**Backend choices deliberately not used:** Passport (a small custom guard over `@nestjs/jwt` is enough), bcrypt (Argon2id is stronger), TypeORM/Prisma (Drizzle gives direct SQL control for the in-memory schema), `@nestjs/serve-static` (Nginx serves the SPA).

---

## 5. Data Layer

| Tool / Library | Purpose | Status |
|---|---|---|
| SQLite `:memory:` | Relational operational database with zero infrastructure | Planned |
| `better-sqlite3` | Synchronous SQLite driver | Planned |
| `drizzle-orm` | Type-safe schema and queries | Planned |
| `drizzle-kit` | Schema generation, SQL inspection, and Studio | Planned |
| Drizzle Studio | Local database inspection during development | Planned |
| `lru-cache` | Classification cache, rate-limit counters, token state | Planned |
| SQLite foreign keys + WAL-independent pragmas | Referential integrity for the session | Planned |
| PostgreSQL + `pg` | Production migration path after the assignment | Deferred |
| pgvector | Production semantic store after the assignment | Deferred |
| Redis | Shared cache, pub/sub, rate limits, durable queues | Deferred |
| BullMQ | Durable AI job queue in production | Deferred |
| `sql.js` | Pure-WASM SQLite fallback if native `better-sqlite3` cannot build | Optional fallback |
| `@faker-js/faker` (fixed seed) | Realistic, deterministic demo data | Planned |

**Data choices deliberately not used:** MongoDB (relational ticket and royalty queries are core), Prisma (extra engine/native step for a small in-memory schema), a separate document database (unnecessary), and an external vector database (the policy corpus is tiny).

---

## 6. AI — LangChain, LangGraph, and Providers

| Tool / Library | Purpose | Status |
|---|---|---|
| `@langchain/core` | Messages, runnable primitives, structured-output interfaces | Planned |
| `@langchain/openai` | Primary chat model and embedding model adapter | Planned |
| `@langchain/anthropic` | Optional fallback chat provider | Optional |
| `@langchain/langgraph` | Explicit enrichment state graph, conditional edges, retries | Planned |
| `langchain` | Document loading, text splitters, and in-memory vector store utilities | Planned |
| `@langchain/textsplitters` | Text splitter package if separate in the installed LangChain version | Verify at scaffold |
| `zod` | Classification/priority schema and provider structured output | Planned |
| `js-tiktoken` | Token caps and cost telemetry | Planned |
| `p-queue` | Bounded AI job concurrency | Planned |
| `cockatiel` | Provider timeout, retry, jitter, and circuit breaker | Planned |
| Custom `MockAiProvider` | Deterministic AI behavior for tests and keyless demos | Planned |
| Custom rule-based classifier | Fallback when AI is disabled or fails | Planned |
| `MemoryVectorStore` | In-process policy embedding index | Planned |
| OpenAI API | Primary LLM and embeddings provider | Planned |
| Anthropic API | Optional fallback provider | Optional |
| LangSmith | Tracing/evaluation platform for LangChain | Deferred |
| OpenAI SDK directly | Direct provider calls outside LangChain | Not used |

**AI choices deliberately not used:** autonomous agents and tool-calling (unnecessary risk for a bounded support workflow), fine-tuning (policies change and labels are scarce), a Python AI microservice (extra runtime and network hop), and a hosted vector database (overkill for six policy documents).

---

## 7. Testing and Quality

| Tool / Library | Purpose | Status |
|---|---|---|
| Vitest | Backend and frontend unit/integration test runner | Planned |
| `@nestjs/testing` | NestJS test module and dependency overrides | Planned |
| `supertest` | HTTP integration tests against the Nest app | Planned |
| `@types/supertest` | Type definitions | Planned |
| `@analogjs/vitest-angular` | Angular unit/component test integration | Planned |
| `jsdom` | Browser-like DOM for frontend unit tests | Planned |
| `@vitest/coverage-v8` | Coverage reports | Planned |
| `@playwright/test` | End-to-end browser tests | Planned |
| `@axe-core/playwright` | Accessibility assertions in e2e | Planned |
| `@faker-js/faker` | Deterministic seed data generation | Planned |
| k6 | Load testing for queue and SSE endpoints | Optional |
| Angular CLI default test runner | Fallback if Angular-Vitest integration is unstable | Fallback |
| Jest + `ts-jest` | Fallback backend test runner if Vitest causes Nest integration friction | Fallback |
| `jest-preset-angular` | Fallback Angular Jest integration | Fallback |
| ESLint | Static analysis | Planned |
| `typescript-eslint` | Type-aware TypeScript rules | Planned |
| `angular-eslint` | Angular-specific lint rules | Planned |
| `eslint-config-prettier` | Disable stylistic lint rules that conflict with Prettier | Planned |
| Prettier | Formatting | Planned |
| `lint-staged` | Run checks on staged files | Optional |
| Husky | Git hooks | Optional |
| `@commitlint/cli` + config-conventional | Conventional commit enforcement | Optional |
| `markdownlint-cli2` | Keep planning documents consistent | Optional |

**Test strategy:** unit tests for domain rules, integration tests for API/RBAC/SSE, contract tests for AI schemas and fallbacks, Playwright for the two critical end-to-end flows, and k6 for capacity evidence.

---

## 8. Security and Privacy Tooling

| Tool / Library | Purpose | Status |
|---|---|---|
| `argon2` | Password hashing | Planned |
| `@nestjs/throttler` | Login, ticket, and AI rate limits | Planned |
| `helmet` | CSP, HSTS, frame and content-type protections | Planned |
| `class-validator` | Request validation and whitelisting | Planned |
| `zod` | Environment and AI schema validation | Planned |
| `cookie-parser` | Refresh-token cookie parsing | Planned |
| `file-type` | Attachment magic-byte checks | Optional |
| `sanitize-filename` | Attachment filename safety | Optional |
| Gitleaks | Secret scanning in CI | Planned |
| Dependabot | Dependency updates and alerts | Planned |
| `pnpm audit` | Dependency vulnerability check | Planned |
| Trivy | Container image scanning | Optional |
| CodeQL | Static security analysis | Optional |
| GitHub secret scanning | Repository-level secret detection | Planned |
| Pino redaction | Remove emails, phones, bank data, tokens, and PII from logs | Planned |

**Privacy practices:** no attachments to the LLM, first-name-only author context, minimal royalty facts, no internal notes in prompts, provider retention settings documented, demo data only, and no real bank credentials.

---

## 9. Observability and Operations

| Tool / Library | Purpose | Status |
|---|---|---|
| `nestjs-pino` + `pino` | Structured logs with request context | Planned |
| `pino-pretty` | Local log readability | Planned |
| `@nestjs/terminus` | Liveness and readiness checks | Planned |
| Request/trace IDs | Correlate API errors, logs, and AI calls | Planned |
| AI telemetry fields | Model, tokens, latency, confidence, fallback, KB version | Planned |
| `prom-client` | Prometheus metrics endpoint | Optional |
| OpenTelemetry | Distributed tracing | Deferred |
| Sentry | Error tracking with PII scrubbing | Deferred |
| Audit event log | Ticket mutation and AI override history | Planned |

---

## 10. API Documentation

| Tool / Library | Purpose | Status |
|---|---|---|
| `@nestjs/swagger` | OpenAPI 3 spec and Swagger UI at `/docs` | Planned |
| OpenAPI 3 JSON | Machine-readable contract at `/docs-json` | Planned |
| `ng-openapi-gen` | Angular client generation from the contract | Planned |
| Postman collection | Optional manual API collection | Optional |
| Mermaid | Architecture and flow diagrams in Markdown | Planned |
| Markdown | README, solution plan, task plan, tooling inventory | Planned |

---

## 11. Git, CI/CD, Containers, and Hosting

| Tool / Library | Purpose | Status |
|---|---|---|
| GitHub | Repository and pull requests | Planned |
| GitHub Actions | CI/CD workflows | Planned |
| `actions/checkout` | Checkout repository | Planned |
| `actions/setup-node` | Node.js setup | Planned |
| `pnpm/action-setup` | pnpm setup | Planned |
| `actions/cache` | Cache pnpm store | Planned |
| `docker/setup-buildx-action` | BuildKit setup | Planned |
| `docker/build-push-action` | Image builds | Planned |
| Docker Engine | Local and production containers | Planned |
| Docker Compose v2 | One-command local stack | Planned |
| Nginx | Static Angular serving, reverse proxy, SSE buffering control | Planned |
| Render | Primary hosted single-instance demo candidate | Candidate |
| Railway | Alternative single-instance host | Alternative |
| Fly.io | Alternative single-instance host | Alternative |
| Azure Container Apps | Alternative single-instance host | Alternative |
| Trivy | Image scanning | Optional |
| Gitleaks | Secret scanning | Planned |
| CodeQL | Static analysis | Optional |
| Dependabot | Dependency maintenance | Planned |

**Deployment decision:** one persistent container instance with `min = max = 1`, because the in-memory database and in-process SSE are single-instance by design. Serverless platforms are explicitly avoided.

---

## 12. Explicitly Not Used

| Tool / Framework | Why not |
|---|---|
| Redis | Adds an external service; in-process cache and jobs are sufficient for the assignment. Documented production path. |
| PostgreSQL / pgvector | Contradicts the in-memory constraint; documented production migration. |
| MongoDB | Ticket queue needs relational filtering, joins, and transactions. |
| Socket.IO / WebSocket | SSE matches one-way ticket notifications with less complexity. |
| NgRx | Feature-level signals are enough; avoids boilerplate. |
| Tailwind CSS | Angular Material theming already provides the design system; mixing both adds inconsistency. |
| Prisma | Extra engine/native layer for a small in-memory schema; Drizzle is leaner. |
| Python AI service | Extra runtime, network hop, auth duplication, and deployment overhead. |
| Autonomous AI agents | Unnecessary autonomy, cost, and unpredictability for a bounded workflow. |
| Serverless functions | Ephemeral instances and poor long-lived SSE support; incompatible with in-memory state. |
| Auth0 / Cognito | Email/password with local JWT and refresh rotation is sufficient. |
| GraphQL | REST is explicitly required and sufficient. |
| Kafka / RabbitMQ | No distributed event requirement; in-process events and an event log suffice. |
| Sentry (primary) | Useful later, but not required and adds a data-processing surface. |
| Axios | Angular HttpClient is built in and handles interceptors cleanly. |
| Chart libraries | No analytics or charting requirement. |

---

## 13. Local Prerequisites

- Node.js 22 LTS
- Corepack enabled and pnpm available
- Git
- Docker Desktop with Compose v2 (primary run path)
- Optional: OpenAI API key for live AI mode
- Optional: Anthropic API key for provider fallback
- Optional: k6 for load testing
- Optional: Playwright browser binaries (`pnpm exec playwright install`)

---

## 14. Package Ownership

| Package / Area | Owns |
|---|---|
| `apps/web` | Angular app, Material theme, SSE client, generated API client |
| `apps/api` | NestJS modules, domain/application/infrastructure layers, AI adapters, SSE hub |
| `packages/contracts` | Shared enums, constants, and contract types |
| Root workspace | Tooling, scripts, CI, Docker, environment templates, README, agent instructions |
| `docs/` | Requirements, architecture, tasks, action plan, tooling inventory, policies, examples |
| `infra/` | Nginx, Dockerfiles, Compose |
| `.github/workflows` | CI/CD, security scans, deployment |

---

## 15. Install and Verification Expectations

- `corepack enable` then `pnpm install` succeeds from a clean clone.
- `pnpm lint`, `pnpm typecheck`, and `pnpm build` succeed for both apps.
- `docker compose up` starts the full stack with seeded data.
- `AI_ENABLED=false` starts the app with no AI key and keeps all core workflows available.
- Swagger is available at `/docs`; the Angular app is served at `/`.
- CI uses a frozen lockfile and does not require an AI key because it uses the deterministic mock provider.
