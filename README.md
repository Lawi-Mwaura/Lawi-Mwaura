# Lawi Mwaura

**Full-stack & mobile engineer · Kenya**

TypeScript · Next.js · React Native · PostgreSQL

I build web and mobile applications with particular attention to what happens when requests repeat, data ingestion stops, or a session changes. **I-soco** and **Maly** are my flagship projects; their case studies explain the implementation, failure cases, and verification behind the interfaces.

**Seeking senior full-stack and product engineering roles at startups.**

[Email me](mailto:lawimwaura@gmail.com) · [Technical documentation](case-studies/README.md) · [Public source: Shenachafiber](https://github.com/Lawi-Mwaura/shenachafiber)

## Technologies used

| Area | Technologies used in these projects |
| :--- | :--- |
| Web | TypeScript, React, Next.js, Tailwind CSS |
| Mobile | React Native, Expo, Expo Router |
| Data & state | PostgreSQL, Supabase, Neon, TanStack Query, Zustand |
| Integrations & quality | Resend, Zod, Vitest, Jest, Node test runner |

## Selected engineering work

### 01 · I-soco — reliable asynchronous workflows

[![I-soco product discovery interface](assets/isoco-discovery.jpg)](https://github.com/Lawi-Mwaura/I-soco-showcase)

<sub>Actual web interface with real product images. Sanitized excerpt; private commercial details are excluded.</sub>

**Problem statement.** External events can repeat, arrive late, or contradict an earlier response. Persisted state and the user interface must converge without applying a durable effect twice.

**Technologies.** TypeScript · Next.js · React · Supabase · PostgreSQL

| Challenge | System design decision | Implemented outcome |
| :--- | :--- | :--- |
| Duplicate events and concurrent writes | Transactional updates, row locks, event and effect uniqueness | Replays follow an already-applied path. |
| Late or contradictory responses | Server verification and guarded state transitions | Confirmed state is protected from downgrade. |
| Timeouts and incomplete operations | Reconciliation and explicit recovery states | The interface distinguishes uncertainty from a terminal result. |

<details>
<summary><strong>System architecture · Next.js and Supabase</strong></summary>

![I-soco architecture with Supabase Auth, Edge Functions, PostgreSQL and Storage](assets/isoco-architecture.svg)

**Tradeoff:** database coordination keeps correctness in one boundary, but can introduce contention. Lock waits and reconciliation latency should be measured before changing that boundary.

</details>

**Metrics & evidence.** **13 selected tests passed** for reliability, recovery, security contracts, and release compatibility. These are regression checks; production latency, throughput, and availability have not been established by this review.

**[Read the engineering case study →](https://github.com/Lawi-Mwaura/I-soco-showcase)**

### 02 · Maly — mobile ingestion and session isolation

<p align="center">
  <a href="https://github.com/Lawi-Mwaura/Maly-showcase"><img src="assets/maly-welcome-native.png" width="38%" alt="Maly welcome screen running in an Android phone emulator." /></a>
  &nbsp;&nbsp;
  <a href="https://github.com/Lawi-Mwaura/Maly-showcase"><img src="assets/maly-budget-native.png" width="38%" alt="Maly spending plan running in an Android phone emulator with labeled sample data." /></a>
</p>

<sub>Native Android emulator captures of actual application components. Sample data and isolated backend fixtures.</sub>

**Problem statement.** Device messages are inconsistent, inbox reads can stop midway, and cached financial data must be cleared when sessions change.

**Technologies.** TypeScript · React Native · Expo · Supabase · TanStack Query · Zustand

| Challenge | System design decision | Implemented outcome |
| :--- | :--- | :--- |
| Inconsistent or unrelated messages | Recognition, normalization, and parser fixtures | Supported transactions are separated from unrelated messages. |
| Interrupted and repeated inbox reads | Paginated scanning, overlap, deduplication, guarded cursor advancement | Failed reads preserve the previous scan cursor. |
| Stale state across sessions | Explicit cleanup of queues, user storage, and query cache | Data cleanup has a separate lifecycle from authentication and PIN state. |

<details>
<summary><strong>System architecture · Expo and Supabase</strong></summary>

![Maly native architecture with Supabase Auth, PostgreSQL and device persistence](assets/maly-architecture.svg)

**Tradeoff:** bounded scans limit device work; page-cap exhaustion needs further validation before claiming complete ingestion of any inbox size. Overlap requires reliable deduplication.

</details>

**Metrics & evidence.** **55 tests passed across five selected suites:** parsing, inbox recovery, user-state cleanup, authentication routing, and PIN storage. Device and storage boundaries are mocked in these tests; emulator images demonstrate native rendering, not end-to-end ingestion or production performance.

**[Read the engineering case study →](https://github.com/Lawi-Mwaura/Maly-showcase)**

## More project work

| Project | Problem & implemented outcome | Technologies | Evidence |
| :--- | :--- | :--- | :--- |
| [Shenachafiber](https://github.com/Lawi-Mwaura/shenachafiber) | Enquiries must survive notification failures. Storage determines success; delivery errors are handled separately. | Next.js, TypeScript, React, Neon / PostgreSQL, Resend, Vitest | Public source; **27 tests passed** across three selected suites. |
| [Catherine Gathoni](https://github.com/Lawi-Mwaura/Catherine-Gathoni-showcase) | Public forms and administration need different trust boundaries. Input validation, persistence-first contact handling, and server-side admin checks. | Next.js, TypeScript, React, Tailwind CSS, Supabase, Resend, Tiptap, Zod, Sentry | Source-reviewed design and public web captures; no complete test run in this review. |
| [Always Organic](https://github.com/Lawi-Mwaura/Always-Organic-showcase) | Storefront state and external-service results need separate lifecycles. Cart state, server queries, runtime validation, and empty-state behavior. | Next.js, TypeScript, React, Tailwind CSS, Supabase, TanStack Query, Zod, Resend, Framer Motion | Source-reviewed design and public web captures; existing component tests were not run in this review. |

Each project README includes interface screenshots, a system diagram, challenges, outcomes, and a clearly scoped evidence section.

## Technical conversations

The case studies support discussions about **idempotency, database transactions, state machines, recovery UX, ingestion correctness, authentication boundaries, and partial failure**. Test counts describe selected runs on **1 October 2026**, not production impact. Production usage, business outcomes, and team leadership are not asserted without supporting evidence.

I-soco, Maly, Catherine Gathoni, and Always Organic retain private source repositories. Their public repositories contain sanitized technical documentation and screenshots. Shenachafiber provides public source. Proprietary commercial logic is omitted.

**[Get in touch](mailto:lawimwaura@gmail.com)**
