# Engineering Quality Standards: Definition of Done (DoD)

A task, pull request, or feature in Doctor Tracker is only considered done when it satisfies every item in these quality matrices.

---

# 1. Code Quality & Architecture

| Check ID | Requirement | Verification Method |
| :--- | :--- | :--- |
| **CODE-1** | Strict TypeScript typing used throughout. Avoid `any` without documented justification. | `npm run type-check` (passes with zero errors) |
| **CODE-2** | Layered design respected: Controllers call Services; database queries stay in the data layer. | Code review and directory structure inspection |
| **CODE-3** | No duplicated business rules or copy-pasted logic across files. | Domain logic verified in `src/services/` |
| **CODE-4** | Clear, descriptive identifiers for variables, functions, and React components. | ESLint and peer review |
| **CODE-5** | Standard error handling: Promises handle exceptions; API errors return uniform JSON responses. | Manual error injection and automated test assertion |

---

# 2. UI/UX & Accessibility Standards

| Check ID | Requirement | Verification Method |
| :--- | :--- | :--- |
| **UI-1** | Matches color tokens and typography in `docs/UI_UX_DESIGN_SYSTEM.md`. | Visual comparison against clinical teal (`#0D9488`) palette |
| **UI-2** | Implements all five UI states: Loading, Empty, Error, Success, and Disabled. | Tested across network throttling and edge conditions |
| **UI-3** | Full keyboard navigation supported (`Tab`, `Enter`, `Escape`, arrow keys). | Keyboard walkthrough without mouse interaction |
| **UI-4** | Focus rings clearly visible on all interactive buttons and inputs. | Manual inspection of `:focus-visible` styling |
| **UI-5** | Contrast ratio meets WCAG 2.2 Level AA (minimum 4.5:1 for body text). | Automated Lighthouse or axe DevTools audit |
| **UI-6** | Tested across mobile (< 640px), tablet (640px-1024px), and desktop viewports. | Chrome DevTools device mode verification |

---

# 3. Security & Validation

| Check ID | Requirement | Verification Method |
| :--- | :--- | :--- |
| **SEC-1** | All client inputs validated on the server using Zod schemas. | API test sending malformed payloads expecting 400 Bad Request |
| **SEC-2** | Unauthenticated requests to protected endpoints return 401 Unauthorized. | API test sending request without JWT token |
| **SEC-3** | Zero secrets or keys committed to Git or exposed in client bundles. | `git status` check, `.gitignore` validation, and secret scanner |
| **SEC-4** | Rate limits and security headers (Helmet, CORS) active on the API server. | Header inspection via curl or Postman |

---

# 4. Performance & Database Optimization

| Check ID | Requirement | Verification Method |
| :--- | :--- | :--- |
| **PERF-1** | Database queries utilize indexes. Verified with MongoDB `explain("executionStats")`. | Confirmed index scans (`IXSCAN`) and zero collection scans (`COLLSCAN`) on filtered collections |
| **PERF-2** | Pagination implemented on all collection endpoints (default: 10 per page). | Keyset or limit/offset parameter checks |
| **PERF-3** | Unnecessary React re-renders avoided. Search inputs debounced (300ms). | React Profiler inspection and network timeline verification |
| **PERF-4** | Core Web Vitals targets met: LCP <= 2.5s, INP <= 200ms, CLS <= 0.1. | Lighthouse performance audit |

---

# 5. Testing & Verification

| Check ID | Requirement | Verification Method |
| :--- | :--- | :--- |
| **TEST-1** | Unit tests pass for core service calculations, status transitions, and data mappers. | `npm test` execution (100% passing) |
| **TEST-2** | Integration tests verify API endpoints with valid and invalid payloads. | Automated API test suite execution |
| **TEST-3** | Production build passes cleanly with zero build warnings or errors. | `npm run build` execution |

---

# 6. Documentation & Synchronization

| Check ID | Requirement | Verification Method |
| :--- | :--- | :--- |
| **DOC-1** | README and API tables updated if endpoints, models, or configurations change. | Review diff in `README.md` and `docs/ARCHITECTURE.md` |
| **DOC-2** | `docs/PROJECT_STATE.md` updated with completed milestone and next action. | Inspect project state log before closing task |
| **DOC-3** | Key architectural choices recorded as ADRs in `docs/DECISIONS/`. | Validated ADR markdown file present |
| **DOC-4** | Visual diagrams in `assets/` and Mermaid code blocks updated in sync with code. | Visual inspection of diagrams |
