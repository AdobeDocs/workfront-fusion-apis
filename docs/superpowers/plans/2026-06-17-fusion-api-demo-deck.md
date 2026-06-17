# Fusion API Demo Deck Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Produce a fully written slide deck (Markdown) covering 6 problem-first Fusion API vignettes, ready for partners to present to customers or import into PowerPoint/Google Slides.

**Architecture:** Single output file `docs/demo/fusion-api-demo-deck.md` using `---` as slide separators. Cover + intro slides first, then 6 vignettes × 2 slides each (14 slides total). Each slide includes speaker notes in a `> **Notes:**` block so partners have full talking points without a separate document.

**Tech Stack:** Markdown (compatible with Marp, Slidev, or manual import to PowerPoint/Google Slides). No build tooling required.

## Global Constraints

- All API paths must match exactly what is in `static/fusion.json` — no invented endpoints.
- Base URL is `https://fusion.adobe.io` — include it only on the intro slide.
- Every API call annotation must include: HTTP method + path, one sentence on what it returns, one sentence on why it matters for that vignette.
- No full JSON request/response payloads in slides — link to API reference instead.
- Each vignette is labeled with a customer archetype (e.g., "IT Admin / Enterprise") in the top-right corner of Slide 1.
- Slide 1 of each vignette: archetype label + pain quote + "what they can't do today" bullet.
- Slide 2 of each vignette: annotated API call table + outcome statement.
- Speaker notes go in `> **Notes:**` block at the bottom of each slide.
- Spec: `docs/superpowers/specs/2026-06-17-fusion-api-demo-deck-design.md`

---

### Task 1: Deck Scaffold + Cover + Intro Slides

**Files:**
- Create: `docs/demo/fusion-api-demo-deck.md`

**Interfaces:**
- Produces: The deck file all subsequent tasks append slides to. Establishes the `---` slide separator convention and speaker notes format.

- [ ] **Step 1: Create the deck file with cover slide**

Create `docs/demo/fusion-api-demo-deck.md` with this exact content:

```markdown
<!--
  Workfront Fusion API — Partner Demo Deck
  Format: Markdown slides (--- separator). Compatible with Marp, Slidev, or manual copy-paste to PowerPoint/Google Slides.
  Usage: Pick the vignettes relevant to your customer. Each vignette is 2 slides.
-->

# Workfront Fusion API
## Automating Automation Management

**For Adobe Partners and Solution Engineers**

*Pick the vignettes that match your customer's pain. Each is self-contained.*

> **Notes:** This deck is a menu, not a script. Before the meeting, identify which 2–3 vignettes map to the customer's known problems and present only those. The full deck runs ~30 minutes; a 3-vignette selection fits a 15-minute discovery conversation.

---

## What the Fusion API Does Today

The Fusion API (v3) gives you programmatic access to **8 resource types** and **22 endpoints** — everything you need to manage, monitor, and govern automation at scale.

| Resource | What You Can Do |
|----------|----------------|
| **Scenarios** | List, inspect, export blueprints, clone across environments |
| **Folders** | Create and organize scenario libraries |
| **Connections** | Inventory integrations, map them to scenarios |
| **Hooks** | Discover and audit webhooks across teams |
| **Data Stores** | Monitor capacity and usage |
| **Activity Logs** | Full audit trail — who did what, when |
| **Operations** | Track and allocate automation consumption |
| **Execution Logs** | Query run history, inspect failures |

**Base URL:** `https://fusion.adobe.io`
**Auth:** OAuth Server-to-Server via Adobe Developer Console

*All vignettes below use real endpoints from this surface.*

> **Notes:** This slide sets expectations — the API is in experimental phase, focused on visibility and management today, with full lifecycle management (create/update/delete) coming. Mention that endpoints and response shapes may evolve, so advise customers to pin to the docs. Link: developer.adobe.com/workfront-fusion-apis

---
```

- [ ] **Step 2: Verify file was created and slide separators are correct**

```bash
grep -c "^---$" docs/demo/fusion-api-demo-deck.md
```
Expected output: `2` (one after cover, one after intro)

- [ ] **Step 3: Commit**

```bash
git add docs/demo/fusion-api-demo-deck.md
git commit -m "feat: scaffold demo deck with cover and intro slides"
```

---

### Task 2: Vignette 1 — Automation Inventory

**Files:**
- Modify: `docs/demo/fusion-api-demo-deck.md`

**Interfaces:**
- Consumes: Deck file from Task 1 (append after the last `---`)
- Produces: Slides 3–4 covering the Automation Inventory use case

- [ ] **Step 1: Append Vignette 1 Slide 1 (Pain slide)**

Append to `docs/demo/fusion-api-demo-deck.md`:

```markdown
<!-- VIGNETTE 1: Automation Inventory -->
<!-- Slide 3 of 14 -->

*IT Admin / Enterprise* <!-- archetype: top-right label in your slide tool -->

## "We have 600 scenarios and no idea what's running."

### The Pain

> *"We've been using Fusion for three years. We have scenarios owned by people who left the company, connections to systems we've decommissioned, and no way to audit any of it without clicking through the UI one by one."*
> — IT Admin, 2,000-person enterprise

**What they can't do today:**
- Generate a full inventory of all scenarios without manual UI navigation
- Know which external systems each scenario depends on
- Identify orphaned or stale automations at scale

> **Notes:** This resonates with any customer who has grown their Fusion footprint organically. Ask: "How many scenarios do you have today? Do you know which ones are still active?" If they pause, this vignette is for them. The problem is governance — not a Fusion limitation, but a scale problem the API solves.

---

<!-- Slide 4 of 14 -->

*IT Admin / Enterprise*

## Automation Inventory: The API Sequence

| Step | Call | Returns | Why It Matters |
|------|------|---------|----------------|
| 1 | `GET /api/v3/scenarios` | Paginated list of all scenarios with status, team, and folder | Build the full portfolio — filter by `status==active` or `status==inactive` to separate live from stale |
| 2 | `GET /api/v3/scenarios/{scenarioId}/dependencies` | All connections, hooks, data stores, and keys linked to a scenario | Know the full dependency graph before touching anything |
| 3 | `GET /api/v3/connections` | All connections in the org with service name and status | Cross-reference against decommissioned systems to find orphaned integrations |

**Outcome:** A complete automation portfolio map — exportable, queryable, and always current. Replaces days of manual UI auditing with a script that runs in minutes.

*Combine with `GET /api/v3/hooks` and `GET /api/v3/data-stores` for a full resource inventory.*

> **Notes:** Walk through the call sequence left to right. Emphasize that Step 1 is paginated (up to 1,000 per page, cursor-based) so it scales to thousands of scenarios. Step 2 is the power move — the dependency graph prevents "unknown unknowns" when planning changes. The typical ask after seeing this: "Can we schedule this to run weekly?" — answer is yes, via a cron job or a Fusion scenario that calls the Fusion API.

---
```

- [ ] **Step 2: Verify slide count**

```bash
grep -c "^---$" docs/demo/fusion-api-demo-deck.md
```
Expected output: `4`

- [ ] **Step 3: Commit**

```bash
git add docs/demo/fusion-api-demo-deck.md
git commit -m "feat: add vignette 1 - automation inventory slides"
```

---

### Task 3: Vignette 2 — Safe Credential Rotation

**Files:**
- Modify: `docs/demo/fusion-api-demo-deck.md`

**Interfaces:**
- Consumes: Deck file after Task 2 (append after last `---`)
- Produces: Slides 5–6 covering the Safe Credential Rotation use case

- [ ] **Step 1: Append Vignette 2 Slide 1 (Pain slide)**

Append to `docs/demo/fusion-api-demo-deck.md`:

```markdown
<!-- VIGNETTE 2: Safe Credential Rotation -->
<!-- Slide 5 of 14 -->

*IT Admin / Security*

## "Our Salesforce API key expires Friday. We don't know what breaks."

### The Pain

> *"Every time we rotate a credential, we get Slack messages an hour later saying 'my automation stopped working.' We have no way to know which scenarios use a given connection before we touch it."*
> — IT Security Lead, financial services firm

**What they can't do today:**
- Identify every scenario that depends on a specific connection before rotating it
- Assess the full blast radius of a credential change
- Plan a maintenance window with confidence

> **Notes:** This is a high-anxiety problem — credential rotation is non-negotiable for security compliance, but it breaks things unpredictably. The cost of "just try it" is real business impact. Ask: "How do you currently handle credential rotation for shared connections?" If the answer involves Slack or prayer, this vignette lands.

---

<!-- Slide 6 of 14 -->

*IT Admin / Security*

## Safe Credential Rotation: The API Sequence

| Step | Call | Returns | Why It Matters |
|------|------|---------|----------------|
| 1 | `GET /api/v3/connections/{connectionId}` | Full connection metadata: name, service, status, team | Confirm you have the right connection before any changes |
| 2 | `GET /api/v3/connections/{connectionId}/scenarios` | All scenarios that use this connection | Complete list of what breaks if the credential is invalid |
| 3 | `GET /api/v3/scenarios/{scenarioId}/dependencies` | Full dependency graph for each affected scenario | Catch cascading dependencies — hooks, data stores, keys that also rely on this connection |

**Outcome:** A pre-rotation impact report. Know exactly which scenarios are affected, who owns them, and what depends on them — before touching the credential. Enables a planned maintenance window with targeted owner notifications.

> **Notes:** The key insight is Step 2 → Step 3 chaining. Step 2 gives the surface area; Step 3 gives the depth. A scenario might depend on a connection through a module that also triggers a webhook — Step 3 surfaces that. Emphasize that this is a read-only operation: the partner/customer is gathering information, not changing anything yet.

---
```

- [ ] **Step 2: Verify slide count**

```bash
grep -c "^---$" docs/demo/fusion-api-demo-deck.md
```
Expected output: `6`

- [ ] **Step 3: Commit**

```bash
git add docs/demo/fusion-api-demo-deck.md
git commit -m "feat: add vignette 2 - safe credential rotation slides"
```

---

### Task 4: Vignette 3 — Environment Promotion

**Files:**
- Modify: `docs/demo/fusion-api-demo-deck.md`

**Interfaces:**
- Consumes: Deck file after Task 3
- Produces: Slides 7–8 covering the Environment Promotion use case

- [ ] **Step 1: Append Vignette 3 Slide 1 (Pain slide)**

Append to `docs/demo/fusion-api-demo-deck.md`:

```markdown
<!-- VIGNETTE 3: Environment Promotion -->
<!-- Slide 7 of 14 -->

*DevOps / Agency*

## "Promoting scenarios from staging to prod takes days and always drifts."

### The Pain

> *"We build and test in a staging org, then manually recreate everything in production — wrong connections, missing folders, mismatched webhooks. We've shipped broken scenarios because of copy-paste errors."*
> — DevOps Engineer, Adobe partner agency

**What they can't do today:**
- Programmatically promote tested scenarios between environments
- Automatically substitute staging connections/hooks for production equivalents
- Onboard a new client tenant with pre-built templates without manual recreation

> **Notes:** This is the DevOps / platform engineering audience — teams that think in pipelines, not UIs. The magic word is "drift." Ask: "How many times has a scenario worked in staging but failed in prod because of a configuration difference?" If they know the number, this vignette is for them. Also resonates with agencies that spin up Fusion for multiple clients.

---

<!-- Slide 8 of 14 -->

*DevOps / Agency*

## Environment Promotion: The API Sequence

| Step | Call | Returns | Why It Matters |
|------|------|---------|----------------|
| 1 | `GET /api/v3/scenarios` | Filtered list of scenarios in the staging team | Identify which scenarios are promotion candidates (filter by team, folder, or status) |
| 2 | `POST /api/v3/scenarios/export` | Full blueprints for up to 100 scenarios in one request | Capture the source-of-truth configuration for archival or diff comparison |
| 3 | `POST /api/v3/scenarios/{scenarioId}/clone` | New scenario in the target team with automatic connection/hook/data store substitution | One call per scenario promotes it to prod with the right prod credentials — no manual rewiring |
| 4 | `POST /api/v3/folders` + `PATCH /api/v3/folders/{folderId}` | New folder / updated folder name | Recreate the staging folder structure in production for organizational consistency |

**Outcome:** A repeatable, scriptable promotion pipeline. Staging → production in a single script run, zero manual configuration, zero drift. Agencies can onboard new client tenants from a template library in minutes.

> **Notes:** Step 3 is the headline feature — the clone endpoint performs automatic substitution of connections, webhooks, data stores, and data structures when you provide a mapping. The customer pre-defines a staging→prod connection map once; every subsequent promotion uses it automatically. This is what makes multi-tenant agency workflows viable at scale.

---
```

- [ ] **Step 2: Verify slide count**

```bash
grep -c "^---$" docs/demo/fusion-api-demo-deck.md
```
Expected output: `8`

- [ ] **Step 3: Commit**

```bash
git add docs/demo/fusion-api-demo-deck.md
git commit -m "feat: add vignette 3 - environment promotion slides"
```

---

### Task 5: Vignette 4 — Compliance & Audit Trail

**Files:**
- Modify: `docs/demo/fusion-api-demo-deck.md`

**Interfaces:**
- Consumes: Deck file after Task 4
- Produces: Slides 9–10 covering the Compliance & Audit Trail use case

- [ ] **Step 1: Append Vignette 4 Slide 1 (Pain slide)**

Append to `docs/demo/fusion-api-demo-deck.md`:

```markdown
<!-- VIGNETTE 4: Compliance & Audit Trail -->
<!-- Slide 9 of 14 -->

*Compliance Officer / Regulated Industry*

## "Auditors want every change to our automations for the past quarter."

### The Pain

> *"We had an audit finding because we couldn't produce a complete record of who modified our data integration workflows. Reconstructing it from memory and screenshots took two weeks."*
> — Compliance Manager, healthcare organization

**What they can't do today:**
- Programmatically extract a complete, timestamped change history for the automation environment
- Export audit data in formats required for submissions (CSV, XLSX)
- Feed Fusion activity into their existing SIEM or governance platform

> **Notes:** Regulated industries — healthcare, financial services, government — have hard requirements here. The question is not "would this be useful" but "this is required." Ask: "Are your Fusion automations in scope for any compliance framework?" SOC 2, HIPAA, and FedRAMP all require change audit trails. The answer determines urgency.

---

<!-- Slide 10 of 14 -->

*Compliance Officer / Regulated Industry*

## Compliance & Audit Trail: The API Sequence

| Step | Call | Returns | Why It Matters |
|------|------|---------|----------------|
| 1 | `GET /api/v3/activity-logs` | Cursor-paginated activity log filtered by date range — who did what and when | Query any time window (e.g., last 90 days) with full actor, action, and timestamp detail |
| 2 | `GET /api/v3/activity-logs/export` | CSV or XLSX file of the filtered activity log | Produces the submission artifact directly — no intermediate transformation needed |

**Outcome:** An audit-ready evidence package generated in minutes. Covers every create, update, delete, and access event in the Fusion org for any requested time window. Supports SIEM integration via the paginated API, and offline submission via the export endpoint.

*Note: Activity log access requires Fusion administrator role on the technical account.*

> **Notes:** Emphasize the two-step pattern — query first to validate the data, export second to produce the artifact. The export endpoint returns a file, not JSON, so it's a direct download. For SIEM integration, the paginated `GET /api/v3/activity-logs` is the right tool — the customer can poll it on a schedule and push events to Splunk, Sentinel, or their platform of choice.

---
```

- [ ] **Step 2: Verify slide count**

```bash
grep -c "^---$" docs/demo/fusion-api-demo-deck.md
```
Expected output: `10`

- [ ] **Step 3: Commit**

```bash
git add docs/demo/fusion-api-demo-deck.md
git commit -m "feat: add vignette 4 - compliance and audit trail slides"
```

---

### Task 6: Vignette 5 — Operations Cost Allocation

**Files:**
- Modify: `docs/demo/fusion-api-demo-deck.md`

**Interfaces:**
- Consumes: Deck file after Task 5
- Produces: Slides 11–12 covering the Operations Cost Allocation use case

- [ ] **Step 1: Append Vignette 5 Slide 1 (Pain slide)**

Append to `docs/demo/fusion-api-demo-deck.md`:

```markdown
<!-- VIGNETTE 5: Operations Cost Allocation -->
<!-- Slide 11 of 14 -->

*Operations Manager / Finance*

## "Finance wants to know which teams are burning our automation quota."

### The Pain

> *"We're approaching our operations limit and we have no idea which team or scenario is responsible. We can see the total in the UI but can't break it down for chargeback or optimization."*
> — Operations Manager, enterprise retail company

**What they can't do today:**
- Break down operation consumption by team or scenario programmatically
- Allocate automation costs to business units for chargeback reporting
- Identify runaway scenarios before they exhaust the org quota

> **Notes:** "Operations" in Fusion = the unit of billing. Every module execution is an operation. Customers on large plans often have multiple teams sharing a quota, and finance wants accountability. Ask: "Do different business units own different teams in Fusion? Do they share a quota?" If yes, this is a chargeback enablement story.

---

<!-- Slide 12 of 14 -->

*Operations Manager / Finance*

## Operations Cost Allocation: The API Sequence

| Step | Call | Returns | Why It Matters |
|------|------|---------|----------------|
| 1 | `GET /api/v3/operations` | Operation counts filterable by team, scenario, or package over a custom date range (up to 1 year) | Granular consumption data per cost center — queryable for any billing period |
| 2 | `GET /api/v3/operations/summary` | Org-wide breakdown by scenario and team, ranked by consumption | Identifies the top consumers at a glance — spot runaway automations before they hit quota |

**Outcome:** Accurate cost allocation data surfaced programmatically. Powers chargeback reporting to finance, capacity planning for the next contract period, and proactive quota management. Identifies the 20% of scenarios consuming 80% of operations.

> **Notes:** The date range on `GET /api/v3/operations` is flexible — customers can query a calendar month to match billing periods, or a rolling 30 days for operational monitoring. The summary endpoint is the fast path for "give me the top 10 offenders." Combine both in a weekly report to finance and operations teams.

---
```

- [ ] **Step 2: Verify slide count**

```bash
grep -c "^---$" docs/demo/fusion-api-demo-deck.md
```
Expected output: `12`

- [ ] **Step 3: Commit**

```bash
git add docs/demo/fusion-api-demo-deck.md
git commit -m "feat: add vignette 5 - operations cost allocation slides"
```

---

### Task 7: Vignette 6 — Incident Investigation

**Files:**
- Modify: `docs/demo/fusion-api-demo-deck.md`

**Interfaces:**
- Consumes: Deck file after Task 6
- Produces: Slides 13–14 covering the Incident Investigation use case. Completes the deck.

- [ ] **Step 1: Append Vignette 6 Slide 1 (Pain slide)**

Append to `docs/demo/fusion-api-demo-deck.md`:

```markdown
<!-- VIGNETTE 6: Incident Investigation -->
<!-- Slide 13 of 14 -->

*DevOps / SLA-sensitive Operations*

## "Something failed at 3am. By morning no one knows why."

### The Pain

> *"We have SLAs on our automation pipelines. When something fails overnight, we spend the first hour of the morning figuring out what happened instead of fixing it. We need a programmatic way to get to the failure context immediately."*
> — Platform Engineer, logistics company

**What they can't do today:**
- Query execution history by failure status without logging into the Fusion UI
- Correlate a runtime failure with a recent configuration change programmatically
- Build an operations dashboard that surfaces failure rates and SLA breaches

> **Notes:** This is the on-call engineer story. The pain is time-to-context, not time-to-fix. Once they have the execution detail and change history, they usually know what happened within minutes. Ask: "Do you have on-call rotations for automation failures? What does your current investigation process look like?" If it involves the Fusion UI and Slack, this vignette shows a better path.

---

<!-- Slide 14 of 14 -->

*DevOps / SLA-sensitive Operations*

## Incident Investigation: The API Sequence

| Step | Call | Returns | Why It Matters |
|------|------|---------|----------------|
| 1 | `GET /api/v3/logs` | Paginated execution history for a scenario, filterable by status (warnings, failures) | Immediately surfaces failed/warned runs — no UI required, scriptable in a monitoring pipeline |
| 2 | `GET /api/v3/logs/{executionId}` | Full execution detail including per-module object context | The failure detail: which module failed, what data it was processing, what error was returned |
| 3 | `GET /api/v3/activity-logs` | Recent change history filtered by date/time near the failure | Catches configuration-induced failures — "someone changed something" — by correlating the failure timestamp with recent activity |

**Outcome:** A structured, scriptable investigation path. Mean-time-to-context drops from 30–60 minutes to under 5. Enables operations teams to build automated alerting pipelines that attach failure context before the on-call engineer is even paged.

> **Notes:** The three-step sequence mirrors the mental model engineers already have: what failed (Step 1), why it failed (Step 2), and what changed (Step 3). Step 3 is the "human error" check — it's surprising how often a 3am failure traces back to a scenario edit at 11pm. Emphasize that all three calls can be chained in an incident-response script that runs automatically on any failure webhook.

---
```

- [ ] **Step 2: Verify final slide count**

```bash
grep -c "^---$" docs/demo/fusion-api-demo-deck.md
```
Expected output: `14`

- [ ] **Step 3: Verify all 8 resource types are represented across the deck**

```bash
grep -oE "GET /api/v3/[a-z-]+" docs/demo/fusion-api-demo-deck.md | sort -u
```
Expected: at least one entry for each of `scenarios`, `connections`, `activity-logs`, `operations`, `logs`, `hooks`, `data-stores`, `folders`

- [ ] **Step 4: Verify no invented endpoints (all paths exist in the spec)**

```bash
grep -oE "(GET|POST|PATCH|DELETE) /api/v3/[a-zA-Z0-9/{}-]+" docs/demo/fusion-api-demo-deck.md | sort -u
```
Cross-check each path against `static/fusion.json`. Every path must appear in that file.

- [ ] **Step 5: Final commit**

```bash
git add docs/demo/fusion-api-demo-deck.md
git commit -m "feat: add vignette 6 - incident investigation slides, complete demo deck"
```
