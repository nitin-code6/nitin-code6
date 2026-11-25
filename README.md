<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0f1c3f,50:1e3a6e,100:2b5797&height=190&section=header&text=Nitin%20Kumar&fontSize=48&fontColor=eaf2fb&animation=fadeIn&fontAlignY=36" width="100%" alt="Nitin Kumar" />

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=500&size=22&duration=3500&pause=1500&color=5B9BD5&center=true&vCenter=true&width=600&height=45&lines=Backend+Engineer;AI+Engineer;Full-Stack+Developer;Building+systems+that+handle+failure" alt="Backend Engineer, AI Engineer, Full-Stack Developer" />

**I build backend-heavy products and AI systems that keep working when things fail.**

MERN &nbsp;|&nbsp; Python and FastAPI &nbsp;|&nbsp; RAG and LLM Systems &nbsp;|&nbsp; Distributed Backend Design &nbsp;|&nbsp; C++ and DSA

[![Portfolio](https://img.shields.io/badge/Portfolio-2b5797?style=for-the-badge)](https://nitincode.vercel.app/)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-3a6ea5?style=for-the-badge)](https://linkedin.com/in/nitbit07)
[![Email](https://img.shields.io/badge/Email-5288bd?style=for-the-badge)](mailto:nitbit710@gmail.com)
[![X](https://img.shields.io/badge/X-1e3a6e?style=for-the-badge)](https://x.com/Nitin_5432)

</div>

---

## At a Glance

<table align="center">
  <tr>
    <td align="center" width="25%"><h2>282x</h2>API ingestion throughput gain after moving to an async queue (CodeArena)</td>
    <td align="center" width="25%"><h2>108+</h2>Automated tests across SupportDesk and ReelFinder AI alone</td>
    <td align="center" width="25%"><h2>4</h2>Live deployed applications you can open and try</td>
    <td align="center" width="25%"><h2>700+</h2>Data structures and algorithms problems solved</td>
  </tr>
</table>

> [!NOTE]
> **Open to full-stack and applied AI roles.** I am strongest where backend engineering meets AI: reliable pipelines, queues and events, LLM fallbacks, and measurable performance work.

---

## What I Bring

<table>
  <tr>
    <td width="33%" valign="top">

**Backend and distributed systems**

Queue and event-driven design with Bull, Redis, and Kafka. Idempotent APIs, rate limiting, circuit breakers, and JWT security. Load testing to prove results.

  </td>
    <td width="33%" valign="top">

**Applied AI**

RAG with pgvector, multi-provider LLM routing with failover, PII scrubbing, and pipelines where models handle judgment and code enforces the rules.

  </td>
    <td width="33%" valign="top">

**Engineering fundamentals**

C++, data structures and algorithms, OOP, SOLID, and design patterns. Documentation of trade-offs, limits, and test coverage on every major project.

  </td>
  </tr>
</table>

---

## Featured Projects

| Project | What it does | Standout detail | Links |
| :--- | :--- | :--- | :--- |
| **CodeArena** | Online judge plus developer social platform | Async submissions: 4,748 ms down to 176 ms, 0.2 to 56.4 req/s | [Code](https://github.com/nitin-code6/codearena) |
| **SupportDesk** | Support triage and escalation platform | Multi-provider AI with deterministic fallback, 22 tests | [Code](https://github.com/nitin-code6/SupportDesk) / [Live](https://supportdesk-frontend-ecgs.onrender.com/) |
| **ReelFinder AI** | Finds and ranks promo clips in screenplays | LLM judges, code enforces bounds, 86 tests | [Code](https://github.com/nitin-code6/reelfinder-ai) / [Live](https://reelfinder-frontend.onrender.com/) |
| **BatteryLife AI** | EV battery health and degradation modeling | LSTM-VAE with hybrid anomaly scoring, 3-tier stack | [Code](https://github.com/nitin-code6/BatteryLife-AI) |
| **FerryFlow** | Real-time ferry booking and operations | Atomic seat locking, Redis refresh tokens, Razorpay | [Code](https://github.com/nitin-code6/ferryflow) / [Live](https://ferryflow.netlify.app/) |
| **CogniVault** | Document Q&A over PDFs with RAG | LLM query router, pgvector retrieval, eval script | [Code](https://github.com/nitin-code6/cognivault) |

Detailed case studies below. Expand any project for the problem, approach, and engineering decisions.

<br/>

<details open>
<summary><h3>CodeArena: asynchronous online judge and developer platform</h3></summary>

![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white) ![Express](https://img.shields.io/badge/Express-404D59?style=flat-square&logo=express&logoColor=white) ![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white) ![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white) ![Bull Queue](https://img.shields.io/badge/Bull_Queue-D9381E?style=flat-square) ![Kafka](https://img.shields.io/badge/Kafka-231F20?style=flat-square&logo=apachekafka&logoColor=white) ![SSE](https://img.shields.io/badge/SSE-0EA5E9?style=flat-square) ![Judge0](https://img.shields.io/badge/Judge0-1F2937?style=flat-square) ![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB) ![Redux](https://img.shields.io/badge/Redux-764ABC?style=flat-square&logo=redux&logoColor=white) ![Gemini API](https://img.shields.io/badge/Gemini_API-4285F4?style=flat-square)

[![Source](https://img.shields.io/badge/Source-1e3a6e?style=for-the-badge)](https://github.com/nitin-code6/codearena)

**Problem.** Running user code through an external sandbox inside the HTTP request kept each submission open for several seconds, limiting throughput and slowing unrelated API traffic.

**Approach.** Separated request ingestion from execution. Submissions are validated, deduplicated, and queued, and the API returns `202 Accepted` while workers run the code. Social actions flow through Kafka to independent consumers, and a dedicated service delivers notifications over Server-Sent Events.

**Engineering highlights**
- Bull and Redis queue with idempotency keys, SHA-256 payload conflict detection, exponential backoff retries, and bounded worker concurrency
- Kafka pipeline with separate feed and notification consumer groups
- Atomic Redis Lua scripts for rate limiting and vote state, plus a Redis JWT revocation blocklist
- Circuit breakers around Judge0 and Gemini, with a resilience test suite
- Sandboxed execution for C++, Java, and JavaScript, and an AI assistant that gives hints without full solutions

**Measured result** (autocannon, submission endpoint)

| Metric | Synchronous baseline | Asynchronous design |
| :--- | ---: | ---: |
| Throughput | 0.2 req/s | **56.4 req/s** |
| Request latency | 4,748 ms | **175.93 ms** |

> [!NOTE]
> This is an API ingestion improvement (about 282x). Code execution still takes seconds in the background. The repository documents its own limits, including in-memory SSE state and a single Kafka partition.

</details>

<details>
<summary><h3>SupportDesk: support operations and diagnostic platform</h3></summary>

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white) ![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white) ![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-D71F00?style=flat-square) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white) ![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB) ![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white) ![Vite](https://img.shields.io/badge/Vite-646CFF?style=flat-square&logo=vite&logoColor=white) ![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white) ![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white) ![pytest](https://img.shields.io/badge/pytest-0A9EDC?style=flat-square&logo=pytest&logoColor=white)

[![Source](https://img.shields.io/badge/Source-1e3a6e?style=for-the-badge)](https://github.com/nitin-code6/SupportDesk)
[![Live App](https://img.shields.io/badge/Live_App-3a6ea5?style=for-the-badge)](https://supportdesk-frontend-ecgs.onrender.com/)
[![API Docs](https://img.shields.io/badge/API_Docs-5288bd?style=for-the-badge)](https://supportdesk-backend-ypdr.onrender.com/docs)

**Problem.** In a case-study dataset of 1,444 tickets, one third were escalated to engineering and about 36% of those bounced back for configuration errors or missing information. Bounced tickets took roughly 7x longer to resolve, and customer satisfaction fell from 4.01 to 2.43 out of 5.

**Approach.** A diagnostic workbench for first-line agents: category-specific checklists, an Escalation Quality Gate that requires a complete handoff, a direct resolution workflow, and analytics on escalation variance across agents.

**Engineering highlights**
- AI triage copilot rotating between Gemini and Groq, with in-memory PII scrubbing before any request leaves the system
- Failover to the second provider and then to a deterministic rule engine, so the product works with no AI keys configured
- Optimistic concurrency locking, audit logs, and a documented PostgreSQL schema and indexing strategy
- 22 automated tests, including golden-dataset invariants and chaos tests for provider failure
- Deployed on Render with static site, Docker service, and managed PostgreSQL

</details>

<details>
<summary><h3>ReelFinder AI: promo discovery for microdrama screenplays</h3></summary>

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white) ![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white) ![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-D71F00?style=flat-square) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white) ![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB) ![Vite](https://img.shields.io/badge/Vite-646CFF?style=flat-square&logo=vite&logoColor=white) ![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white) ![Groq](https://img.shields.io/badge/Groq-F55036?style=flat-square) ![Gemini API](https://img.shields.io/badge/Gemini_API-4285F4?style=flat-square) ![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)

[![Source](https://img.shields.io/badge/Source-1e3a6e?style=for-the-badge)](https://github.com/nitin-code6/reelfinder-ai)
[![Live App](https://img.shields.io/badge/Live_App-3a6ea5?style=for-the-badge)](https://reelfinder-frontend.onrender.com/)
[![API Docs](https://img.shields.io/badge/API_Docs-5288bd?style=for-the-badge)](https://reelfinder-backend.onrender.com/docs)

**Problem.** Editors watch every episode to find 20 to 60 second moments that work as social ads. A good clip needs a strong hook, a cut at an unresolved peak, and enough context for a new viewer. Built for an AI generalist assignment.

**Approach.** Split responsibilities on purpose: the LLM judges narrative quality, and deterministic code enforces what LLMs are unreliable at.

| Task | LLM | Deterministic code |
| :--- | :--- | :--- |
| Narrative comprehension | Judges stakes, curiosity gaps, tension | None |
| Timecodes and bounds | Proposes candidate anchors | Enforces 20 to 60 second limits and source grounding; rejects invented timestamps |
| Deduplication | Identifies themes | Temporal overlap and similarity thresholds |
| Ranking | Scores raw qualitative factors | Weighted 0 to 100 composite of hook, cliffhanger, clarity, impact, continuity |

**Engineering highlights**
- Screenplay parser (regex state machine, PDF support) feeding a three-tier chain: Groq, then Gemini, then a heuristic fallback
- Human-in-the-loop review station with CSV and JSON export
- 86 automated tests, a reconciliation audit between database and exports, and a batch evaluation script
- Honest documentation of limitations and of where AI tools were used

</details>

<details>
<summary><h3>BatteryLife AI: EV battery health and degradation modeling</h3></summary>

![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white) ![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white) ![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white) ![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white) ![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB) ![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white) ![Express](https://img.shields.io/badge/Express-404D59?style=flat-square&logo=express&logoColor=white) ![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white) ![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)

[![Source](https://img.shields.io/badge/Source-1e3a6e?style=for-the-badge)](https://github.com/nitin-code6/BatteryLife-AI)

**Problem.** Estimating battery State of Health and remaining life from raw cycling telemetry, and spotting abnormal cells early.

**Approach.** An LSTM Variational Autoencoder learns a latent representation of degradation. That latent space powers anomaly scoring, synthetic degradation generation, and health reports.

**Engineering highlights**
- Three tiers: Next.js dashboard, Express and TypeScript gateway with JWT and experiment tracking, and a FastAPI and PyTorch AI engine
- ETL for NASA (`.mat`) and CALCE (Excel) datasets, recovering missing capacity by numerically integrating current
- Hybrid anomaly score combining reconstruction error with latent distance (Mahalanobis and Euclidean)
- PCA and t-SNE latent views, drift analysis, and SOH, remaining-life, and maintenance reports
- One-command Docker Compose stack, CI workflow, and API and architecture docs

</details>

<details>
<summary><h3>FerryFlow: real-time ferry operations and booking</h3></summary>

![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB) ![Vite](https://img.shields.io/badge/Vite-646CFF?style=flat-square&logo=vite&logoColor=white) ![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white) ![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white) ![Express](https://img.shields.io/badge/Express-404D59?style=flat-square&logo=express&logoColor=white) ![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white) ![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white) ![Socket.IO](https://img.shields.io/badge/Socket.IO-010101?style=flat-square&logo=socketdotio&logoColor=white) ![Razorpay](https://img.shields.io/badge/Razorpay-0C2451?style=flat-square) ![Playwright](https://img.shields.io/badge/Playwright-2EAD33?style=flat-square&logo=playwright&logoColor=white)

[![Source](https://img.shields.io/badge/Source-1e3a6e?style=for-the-badge)](https://github.com/nitin-code6/ferryflow)
[![Live App](https://img.shields.io/badge/Live_App-3a6ea5?style=for-the-badge)](https://ferryflow.netlify.app/)

**Engineering highlights**
- Role-based access for admin, staff, and passengers
- Seat booking that prevents double reservation with atomic MongoDB operations, plus Socket.IO broadcasts to keep clients in sync
- Dual-token auth: short-lived access tokens and Redis-backed refresh tokens in HttpOnly cookies, with Google sign-in and email OTP
- Redis-backed rate limiting on auth routes and Zod validation on request bodies
- Razorpay payments with server-side signature verification and reconciliation when a user abandons checkout
- Playwright end-to-end tests for booking and authentication

</details>

<details>
<summary><h3>CogniVault: multi-project document question answering</h3></summary>

![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB) ![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white) ![Express](https://img.shields.io/badge/Express-404D59?style=flat-square&logo=express&logoColor=white) ![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white) ![pgvector](https://img.shields.io/badge/pgvector-336791?style=flat-square) ![Gemini API](https://img.shields.io/badge/Gemini_API-4285F4?style=flat-square) ![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)

[![Source](https://img.shields.io/badge/Source-1e3a6e?style=for-the-badge)](https://github.com/nitin-code6/cognivault)

**Approach.** PDFs are chunked (500 characters, 50 overlap), embedded, and stored in PostgreSQL with pgvector. An LLM router decides whether a query needs retrieval, a tool call, or a direct answer, and retrieved chunks ground the Gemini response.

**Engineering highlights**
- Node.js gateway with input guardrails, separated from a Python and FastAPI AI service
- Cosine-similarity retrieval (top 3 chunks) inside PostgreSQL, avoiding a separate vector database at this scale
- Automated evaluation script for relevance and faithfulness, pytest unit tests, and Docker Compose setup
- Documented limits: PDF only, fixed-size chunking, string-match injection guardrails. Source citations and streaming are in progress

</details>

---

## More Projects

| Project | Description | Status |
| :--- | :--- | :--- |
| [DevConnector](https://github.com/nitin-code6/devconnector) | Developer networking platform with profiles, posts, and JWT auth | Complete |
| [OS Visualizer](https://github.com/nitin-code6/OS-VISUALIZER) ([live](https://cpulab.vercel.app)) | CPU scheduling simulator with Round Robin, SJF, FCFS, and live Gantt charts | Complete |
| [Dialysis Session Dashboard](https://github.com/nitin-code6/dialysis-session-dashboard) | Patient session tracking with anomaly detection | Complete |
| [AlgoCore](https://github.com/nitin-code6/AlgoCore) | Modular C++ DSA library with an interactive CLI | Complete |
| [ParkingLotManager](https://github.com/nitin-code6/ParkingLotManager) | C++ low-level design with polymorphic pricing and slot management | Complete |
| [DocumentEditor](https://github.com/nitin-code6/DocumentEditor) | C++ editor built to practice SOLID and design patterns | Complete |
| [LearnFlow MCP](https://github.com/nitin-code6/LearnFlow-MCP) | Moodle-style LMS; Prisma and a FastMCP server are planned | In progress |
| [DocuLens](https://github.com/nitin-code6/DocuLens) | RAG document analyzer | In progress |
| [RAG Debugging Lab](https://github.com/nitin-code6/RAG-Debugging-Lab) | Intentionally broken RAG pipelines for practice | In progress |

---

## Tech Stack

**Languages** &nbsp; ![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white) ![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white) ![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black) ![C++](https://img.shields.io/badge/C%2B%2B-00599C?style=flat-square&logo=cplusplus&logoColor=white) ![C](https://img.shields.io/badge/C-A8B9CC?style=flat-square&logo=c&logoColor=black) ![SQL](https://img.shields.io/badge/SQL-4479A1?style=flat-square&logo=mysql&logoColor=white)

**Frontend** &nbsp; ![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB) ![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white) ![Redux](https://img.shields.io/badge/Redux-764ABC?style=flat-square&logo=redux&logoColor=white) ![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white) ![Vite](https://img.shields.io/badge/Vite-646CFF?style=flat-square&logo=vite&logoColor=white)

**Backend** &nbsp; ![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white) ![Express](https://img.shields.io/badge/Express-404D59?style=flat-square&logo=express&logoColor=white) ![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white) ![Socket.IO](https://img.shields.io/badge/Socket.IO-010101?style=flat-square&logo=socketdotio&logoColor=white) ![GraphQL](https://img.shields.io/badge/GraphQL-E10098?style=flat-square&logo=graphql&logoColor=white)

**Data and messaging** &nbsp; ![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white) ![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white) ![Kafka](https://img.shields.io/badge/Kafka-231F20?style=flat-square&logo=apachekafka&logoColor=white) ![pgvector](https://img.shields.io/badge/pgvector-336791?style=flat-square) ![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white) ![SQLite](https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white)

**AI** &nbsp; ![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white) ![Gemini API](https://img.shields.io/badge/Gemini_API-4285F4?style=flat-square) ![Groq](https://img.shields.io/badge/Groq-F55036?style=flat-square) ![RAG](https://img.shields.io/badge/RAG-7C3AED?style=flat-square) ![MCP](https://img.shields.io/badge/MCP-111827?style=flat-square)

**DevOps and testing** &nbsp; ![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white) ![pytest](https://img.shields.io/badge/pytest-0A9EDC?style=flat-square&logo=pytest&logoColor=white) ![Playwright](https://img.shields.io/badge/Playwright-2EAD33?style=flat-square&logo=playwright&logoColor=white) ![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white) ![Jest](https://img.shields.io/badge/Jest-C21325?style=flat-square&logo=jest&logoColor=white) ![Render](https://img.shields.io/badge/Render-46E3B7?style=flat-square&logo=render&logoColor=black) ![Vercel](https://img.shields.io/badge/Vercel-000000?style=flat-square&logo=vercel&logoColor=white) ![Netlify](https://img.shields.io/badge/Netlify-00C7B7?style=flat-square&logo=netlify&logoColor=black)

---

## How I Work

- **Design for failure.** Fallback providers, circuit breakers, idempotent endpoints, and graceful degradation come before polish.
- **Let code do what code is good at.** In AI features, models handle judgment and deterministic logic enforces constraints.
- **Measure, then claim.** I benchmark changes and document limitations next to results.
- **Document decisions.** Projects ship with architecture notes, trade-offs, and test documentation.

Currently learning system design, MCP, agentic AI workflows, and CI/CD. Outside of coding, I play chess and cricket.

---

<div align="center">

## Let's Connect

Open to opportunities and collaborations in full-stack development and applied AI.

[![Portfolio](https://img.shields.io/badge/Portfolio-2b5797?style=for-the-badge)](https://nitincode.vercel.app/)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-3a6ea5?style=for-the-badge)](https://linkedin.com/in/nitbit07)
[![Email](https://img.shields.io/badge/Email-5288bd?style=for-the-badge)](mailto:nitbit710@gmail.com)

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0f1c3f,50:1e3a6e,100:2b5797&height=110&section=footer" width="100%" alt="" />

</div>
