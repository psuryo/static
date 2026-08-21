# 📱 Final Exam: Integrated Mobile Application Project
### Flutter × Spring Boot × Object-Oriented Analysis and Design
#### Group Assignment (3 Members) — Industry-Grade Level

---

## Overview

This final exam requires your group to design, develop, and deliver a **fully integrated mobile application system** consisting of:

- A **Flutter mobile frontend** that consumes a RESTful API
- A **Spring Boot backend** that exposes the API with proper layering, security, and persistence
- A rigorous **OOAD process** — designed before coding, then verified against the final implementation

The project is evaluated across three distinct dimensions with different grade weights. This is intentional: **design thinking (OOAD) is the foundation**, engineering quality (Flutter + Spring Boot) is the execution.

---

## Group Formation & Role Distribution

Each group consists of **exactly 3 members**. Each member owns one primary pillar but all members must understand and contribute to all three.

| Role | Primary Pillar | Core Responsibilities |
|---|---|---|
| **OOAD Lead** | Object-Oriented Analysis & Design | Leads all design artifacts (use case, class, sequence, state diagrams), enforces design pattern compliance across both codebases, owns the design traceability matrix |
| **Flutter Engineer** | Mobile Frontend | Clean Architecture implementation, state management, UI/UX, performance benchmarking |
| **Backend Engineer** | Spring Boot API | REST API design, service/repository layers, database schema, security (JWT), API documentation, backend testing |

> **Important:** Role ownership means accountability, not isolation. All members must commit code to both repositories. The OOAD Lead reviews both codebases for pattern compliance — this is a graded responsibility.

---

## Project Topic

Your group is free to choose any application domain, provided it:

- Models a real-world problem with identifiable actors, use cases, and entities
- Requires meaningful backend logic (not just CRUD — include at least one business rule or workflow)
- Has a clear primary user and at least one secondary actor (admin, system, or external service)

**Example domains** *(create your own — do not copy)*:
- Hospital appointment and queue management
- Campus asset borrowing and return tracking
- Community marketplace with seller verification flow
- Event ticketing with seat allocation logic
- Employee attendance with approval workflow

---

## Pillar 1 — Object-Oriented Analysis & Design (OOAD)

OOAD is evaluated in **two phases**: design artifacts produced before coding, and a traceability audit conducted against the final code.

### Phase 1A: Pre-Development Design Artifacts

All diagrams must be produced using **PlantUML, draw.io, or StarUML** and submitted as part of the Week 2–3 checkpoint. Diagrams drawn by hand are not accepted.

| Artifact | Diagram Type | Requirement |
|---|---|---|
| Requirements model | Use Case Diagram | All actors, use cases, include/extend relationships |
| Structural model | Class Diagram | All domain classes with attributes, methods, visibility, and relationships (association, aggregation, composition, inheritance) |
| Behavioral model | Sequence Diagrams | At least 3 key interactions (e.g., login, create resource, approval flow) showing object collaboration |
| State model | State Machine Diagram | At least 1 entity with meaningful state transitions (e.g., Order: PENDING → CONFIRMED → COMPLETED → CANCELLED) |
| Data model | ERD (Crow's Foot notation) | All entities, PKs/FKs, cardinality — must align with the class diagram |
| Architecture model | Component Diagram | Flutter app, Spring Boot layers, database, and external services as components with interfaces |

### Phase 1B: Design Pattern Compliance

Your system must implement **at least 4 GoF design patterns** across the full stack, with at least 1 from each category:

| Category | Required Count | Examples |
|---|---|---|
| Creational | ≥ 1 | Factory Method, Builder, Singleton |
| Structural | ≥ 1 | Adapter, Facade, Decorator, Proxy |
| Behavioral | ≥ 2 | Strategy, Observer, Command, Template Method, Chain of Responsibility |

Each pattern must be documented with:
1. Pattern name and category
2. Which class/component implements it (with file path)
3. UML class diagram showing the pattern in context
4. Justification — why this pattern was chosen over alternatives

### Phase 1C: Design Traceability Audit (Post-Development)

After development is complete, the OOAD Lead conducts a **traceability audit** comparing the pre-development design to the final code:

- For each class in the original class diagram: does it exist in code? If not, explain why.
- For each design pattern: show the exact code that implements it (file + line reference).
- For each sequence diagram: trace the method call chain in the actual code.
- Document all **design deviations** — cases where implementation diverged from design — with a written rationale for each deviation.

> A perfect match between design and code is not required. Thoughtful, documented deviations are acceptable. Undocumented deviations are penalized.

---

## Pillar 2 — Flutter Mobile Frontend

### Technical Requirements

| Category | Requirement |
|---|---|
| **Flutter Version** | Flutter 3.x (Stable channel) |
| **Architecture** | Clean Architecture — strict 4-layer separation: `domain / data / application / presentation` |
| **State Management** | BLoC or Riverpod (consistent throughout; mixing is not allowed) |
| **Navigation** | Go Router with at least 6 distinct screens and route guards for authenticated routes |
| **API Communication** | `Dio` with interceptors for JWT token injection, refresh token handling, and error normalization |
| **Local Persistence** | Hive or SQLite for offline caching of at least one core data entity |
| **Authentication** | JWT-based login/register consuming the Spring Boot auth endpoint |
| **UI/UX** | Custom widget library (min. 5 reusable widgets), responsive layout, consistent design system |
| **Error Handling** | Typed failure classes using `Either` (dartz) or equivalent; no raw `try/catch` in UI layer |

### Folder Structure (Enforced)

```
lib/
├── core/              # shared utilities, theme, constants, error types
├── features/
│   └── [feature]/
│       ├── domain/    # entities, repository interfaces, use cases
│       ├── data/      # repository implementations, DTOs, data sources
│       └── presentation/  # BLoC/Cubit, pages, widgets
└── main.dart
```

Any structure deviating from feature-first modular layout must be approved in writing before Week 4.

### Advanced Features (Choose at least 2)

- Real-time updates via WebSocket or Server-Sent Events from Spring Boot
- Push notifications triggered by backend events (FCM)
- Offline-first with background sync to Spring Boot API
- Animated transitions using custom `PageRouteBuilder` or Lottie
- Internationalization (i18n) with at least 2 languages
- Biometric authentication (fingerprint/face ID) as second factor

### Flutter Testing & Benchmarking

#### Functional Testing

| Type | Tool | Minimum |
|---|---|---|
| Unit Testing | `flutter_test` | All use cases and repository implementations |
| Widget Testing | `flutter_test` | At least 5 core UI components |
| Integration Testing | `integration_test` | At least 3 end-to-end flows against the live Spring Boot API |

#### Performance Benchmarking

Run all benchmarks on a **physical Android device in profile mode** (`flutter run --profile`). Emulator results alone are not accepted.

| Metric | Tool | Pass Threshold |
|---|---|---|
| Memory — baseline | DevTools → Memory tab | Report heap at launch (MB) |
| Memory — leak check | DevTools → Memory tab | No steady growth over 10 repeated navigations |
| Frame rate / jank | DevTools → Performance tab | ≥ 90% frames < 16ms (60fps target) |
| CPU profile | DevTools → CPU Profiler | Flame graph for top 3 CPU-heavy operations |
| API latency (client-side) | Dio interceptor logs | All core endpoints < 1500ms |
| Cold start time | `--trace-startup --profile` | `timeToFirstFrame` < 3000ms |
| APK size | `flutter build apk --analyze-size` | Release APK < 50MB |

Each benchmark must be reported with: objective, tool, method, results table, threshold comparison, and DevTools screenshot.

**Regression requirement:** Run benchmarks at Week 5 (mid-sprint) and at Week 7 (final). Submit a delta table comparing both runs. Any metric that degrades > 20% must include a root cause analysis and remediation.

---

## Pillar 3 — Spring Boot Backend

### Technical Requirements

| Category | Requirement |
|---|---|
| **Java Version** | Java 17+ |
| **Framework** | Spring Boot 3.x |
| **Architecture** | Layered: `Controller → Service → Repository` (no logic in Controller, no DB calls in Service) |
| **Database** | PostgreSQL or MySQL with JPA/Hibernate; schema migrations via Flyway |
| **Security** | Spring Security with JWT (access token + refresh token); role-based access control (RBAC) |
| **API Design** | RESTful conventions; versioned endpoints (`/api/v1/...`); proper HTTP status codes |
| **Validation** | Bean Validation (`@Valid`) on all request DTOs; global exception handler via `@ControllerAdvice` |
| **Documentation** | Swagger/OpenAPI 3.0 via `springdoc-openapi`; all endpoints documented with schemas |
| **Configuration** | Environment-separated configs (`application-dev.yml`, `application-prod.yml`); no hardcoded secrets |

### API Contract Requirements

- Minimum **10 distinct REST endpoints** covering the full application domain
- All endpoints must return a **consistent response envelope**:

```json
{
  "success": true,
  "data": {},
  "message": "Operation successful",
  "timestamp": "2025-01-01T00:00:00Z"
}
```

- Error responses must include: `success: false`, `errorCode`, `message`, and `timestamp`
- API contract must be defined as an **OpenAPI 3.0 YAML file** committed to the repository before development begins (design-first)

### Backend Testing & Benchmarking

#### Functional Testing

| Type | Tool | Minimum |
|---|---|---|
| Unit Testing | JUnit 5 + Mockito | All service classes; mock repository layer |
| Integration Testing | `@SpringBootTest` + MockMvc | All controller endpoints; test DB via Testcontainers |
| Code Coverage | JaCoCo | ≥ 70% line coverage on `service` and `controller` packages |

#### Load Benchmarking

| Metric | Tool | Pass Threshold |
|---|---|---|
| API throughput | Apache JMeter or k6 | ≥ 100 req/s under 50 concurrent users |
| p95 latency | JMeter or k6 | < 500ms under load |
| Error rate under load | JMeter or k6 | < 1% at 50 concurrent users |
| DB query performance | Spring Actuator + slow query log | No query > 200ms for standard operations |
| JVM memory under load | Actuator `/actuator/metrics` | No heap exhaustion during 5-min load test |

Load test scenario: simulate 50 concurrent users performing a realistic user journey (login → fetch list → create resource → logout) for 5 minutes. Export JMeter `.jtl` report or k6 summary as evidence.

---

## Deliverables

### 1. 📁 GitHub Repositories (2 repos)

**Flutter Repository** (`[GroupName]-[AppName]-mobile-final`):
- Feature-first clean architecture folder structure
- GitHub Actions workflow (`.github/workflows/flutter.yml`) — green at submission
- `README.md`: setup instructions, environment variables, APK download link
- All 3 members must have commits; branching strategy enforced

**Spring Boot Repository** (`[GroupName]-[AppName]-backend`):
- Layered package structure (`controller`, `service`, `repository`, `domain`, `dto`, `config`)
- Flyway migration scripts in `resources/db/migration/`
- OpenAPI YAML committed before Week 4
- `README.md`: setup instructions, environment variables, how to run locally
- JaCoCo HTML coverage report committed or published via CI

### 2. 📦 APK File

- Release build named `[GroupName]_[AppName]_FinalExam.apk`
- Must connect to a **live, publicly deployed** Spring Boot backend (not localhost)
- Acceptable deployment platforms: Railway, Render, Fly.io, or any public URL

### 3. 📄 Written Report

Format: PDF, minimum **25 pages** (excluding cover and references). Language: English or Bahasa Indonesia.

| # | Section | Description |
|---|---|---|
| 1 | Cover Page | System name, group name, member names & student IDs, course name, date |
| 2 | Abstract | 200–250 words covering the system, tech stack, and key findings |
| 3 | Introduction | Problem background, objectives, target users, scope and limitations |
| 4 | OOAD — Pre-Development | All design artifacts (use case, class, sequence, state, ERD, component diagrams) |
| 5 | OOAD — Design Patterns | Documentation of all 4+ patterns with UML and code references |
| 6 | OOAD — Traceability Audit | Design-to-code mapping table; documented deviations with rationale |
| 7 | System Architecture | Flutter Clean Architecture, Spring Boot layers, API communication flow diagram |
| 8 | API Contract | OpenAPI summary, endpoint table, request/response examples |
| 9 | Flutter Implementation | Key features, state management flow, custom widgets, advanced features |
| 10 | Spring Boot Implementation | Service layer logic, security config, DB schema, Flyway migrations |
| 11 | Flutter Testing & Benchmarking | Test results, all 7 benchmark metrics with evidence and delta table |
| 12 | Backend Testing & Benchmarking | JUnit/integration test results, JMeter/k6 load test report |
| 13 | Team Contribution | Per-member task table with percentage, cross-verified with Git commit history |
| 14 | Conclusion | Achievements, design lessons learned, challenges, future improvements |
| 15 | References | IEEE format |

### 4. Presentation

- Duration: **15–20 minutes**
- Structure:
  - Team introduction + system overview (2 min)
  - OOAD design walkthrough — diagrams and pattern explanation (4–5 min)
  - Flutter app live demo — all major flows (5–6 min)
  - Spring Boot API demo — Swagger UI + one live API call (3 min)
  - Benchmark results summary (2 min)
- All 3 members must present a section
- Upload to YouTube (unlisted) or Google Drive

> **Live Session:** Each member will be questioned individually on the section they presented and on OOAD concepts. Individual scores may differ from the group score.

---

## Timeline

| Phase | Activity | Deadline |
|---|---|---|
| Week 1 | Group registration + topic proposal + actor/use case list | Day 7 |
| Week 2–3 | All OOAD Phase 1A artifacts submitted + OpenAPI YAML drafted | Day 21 |
| Week 4 | Architecture approved; development sprint begins | Day 28 |
| Week 5 | Mid-sprint benchmark run (Flutter + Backend) submitted | Day 35 |
| Week 6–7 | Feature freeze; Flutter ↔ Spring Boot integration testing | Day 49 |
| Week 7 | Final benchmark run; delta table completed | Day 49 |
| Week 8 | OOAD traceability audit completed; report writing + video | Day 56 |
| **Final** | **All deliverables submitted** | **Day 60, 23:59** |
| Final+1 | Live presentation & individual Q&A | Scheduled by lecturer |

---

## Grading Rubric

Each pillar is graded **independently out of 100 points**. Students receive three separate scores — one per pillar. There is no combined final grade: each score stands on its own and is recorded separately.

---

### 🥇 Pillar 1 — OOAD Score (/ 100)

| Component | Points | Criteria |
|---|---|---|
| Pre-development design artifacts | 35 | Completeness of all 6 required diagrams, correctness of notation, diagram tool used (no hand-drawn), submitted before coding begins |
| Design pattern implementation | 25 | Correct application of ≥ 4 GoF patterns (min 1 per category), UML documented per pattern, each traceable to code with file path |
| Traceability audit | 25 | Coverage of class-to-code mapping, quality and honesty of deviation documentation, sequence diagram trace accuracy |
| Cross-pillar design consistency | 15 | Alignment between class diagram, ERD, Flutter domain layer entities, and Spring Boot domain/entity classes |

**OOAD Penalty:**

| Violation | Deduction |
|---|---|
| OOAD artifacts submitted after Week 3 (after coding begins) | −20 points |
| Diagram produced with unpermitted tool (e.g., hand-drawn, screenshot of AI output) | −15 points |
| Design pattern claimed but not traceable in code | −8 points per pattern |
| Traceability audit missing for > 30% of class diagram classes | −10 points |

---

### 🥈 Pillar 2 — Flutter Mobile Score (/ 100)

| Component | Points | Criteria |
|---|---|---|
| Clean Architecture compliance | 25 | Strict 4-layer separation enforced, no cross-layer violations, feature-first folder structure correct, dependency direction correct |
| Features & UX quality | 20 | All required screens functional, JWT auth flow works against live API, custom widget library present, error states handled |
| Testing — unit & widget | 15 | All use cases and repositories covered, at least 5 widget tests, test quality (meaningful assertions, not just coverage padding) |
| Testing — integration | 10 | At least 3 end-to-end flows tested against live Spring Boot API, not mocked |
| Performance benchmarking | 20 | All 7 metrics reported on physical device in profile mode, DevTools screenshots provided, delta table (mid vs final), root cause for any regression > 20% |
| Report clarity | 10 | Report is complete and have clear explanation |

**Flutter Penalty:**

| Violation | Deduction |
|---|---|
| Responsive Design fail | −10 points |
| Benchmarks run on emulator only (no physical device) | −10 points |
| Missing delta table (mid-sprint vs final benchmark) | −8 points |
| State management inconsistency (mixing BLoC and Riverpod) | −10 points |
| Raw `try/catch` found in presentation layer | −5 points per occurrence (max −15) |
| APK connects to localhost instead of deployed backend | −15 points |

---

### 🥉 Pillar 3 — Spring Boot Score (/ 100)

| Component | Points | Criteria |
|---|---|---|
| API design & OpenAPI contract | 25 | ≥ 10 endpoints, consistent response envelope, versioned routes, OpenAPI 3.0 YAML committed before Week 4, Swagger UI accessible |
| Layered architecture & security | 25 | Strict Controller → Service → Repository separation, JWT with access + refresh token, RBAC with at least 2 roles, no hardcoded secrets |
| Testing — unit & integration | 25 | JUnit 5 + Mockito for all service classes, MockMvc + Testcontainers for all controllers, JaCoCo ≥ 70% on `service` and `controller` packages |
| Load benchmarking | 25 | All 5 metrics reported (throughput, p95 latency, error rate, DB query time, JVM heap), JMeter `.jtl` or k6 summary exported, analysis against pass thresholds |

**Spring Boot Penalty:**

| Violation | Deduction |
|---|---|
| Hardcoded secrets (API keys, DB passwords) in any file | −15 points |
| JaCoCo coverage below 70% | −10 points |
| No Flyway migrations (schema managed manually) | −8 points |
| OpenAPI YAML committed after Week 4 | −10 points |
| Load test run with < 50 concurrent users | −10 points |
| Business logic found directly in Controller class | −8 points per occurrence (max −16) |

---

### Universal Penalty (Applied to All Three Pillar Scores)

| Violation | Deduction |
|---|---|
| Late submission (per day, applied to all pillars) | −5 points per pillar |
| Missing deliverable | −15 points from the relevant pillar |
| Plagiarized code (any source) | 0 on all three pillars |
| Member with < 10% commits and no other contribution evidence | That member's individual pillar scores reduced by 20 points each |

---

## Academic Integrity

- All code must be original. Open-source libraries are permitted with proper attribution in both READMEs and the report.
- Use of AI coding assistants is **permitted but must be disclosed** in a dedicated "AI Tool Usage" section in the report, listing which tools were used, for which tasks, and how outputs were reviewed and understood.
- Design artifacts must be produced by the group. AI-generated diagrams submitted without annotation will be identified during the live Q&A.
- Plagiarism between groups or from public repositories results in **zero marks for all involved groups**.

---

## Submission Checklist

- [ ] Flutter GitHub repository (Actions pipeline green, branch protection active, 3+ merged PRs)
- [ ] Spring Boot GitHub repository (JaCoCo report committed, OpenAPI YAML present, Flyway migrations included)
- [ ] APK file connecting to live deployed backend (`[GroupName]_FinalExam.apk`)
- [ ] Written report PDF (≥ 25 pages, all 16 sections complete, benchmark delta table included)
- [ ] Demo video link (YouTube unlisted or Google Drive, all 3 members presenting)
- [ ] OOAD traceability matrix (Section 6 of report)
- [ ] Mid-sprint benchmark results (Sections 11 & 12 of report)
- [ ] JMeter/k6 load test export (appendix or Drive link)

---

## Contact & Questions

All questions must be submitted through the official course channel. Questions submitted at least **48 hours before any deadline** are guaranteed a response. Design artifact reviews (Week 2–3) require a scheduled appointment — contact the lecturer by Week 1 to book a slot.

---

*Build systems you can defend, designs you can explain, and code that reflects your thinking. 🚀*
