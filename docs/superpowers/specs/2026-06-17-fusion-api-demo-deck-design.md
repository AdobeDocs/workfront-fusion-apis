# Fusion API Demo Deck — Design Spec

**Date:** 2026-06-17
**Author:** Ani Mheryan
**Status:** Approved

---

## Purpose

A slide deck partners can use with customers to demonstrate the business value of the Workfront Fusion public API. Partners are internal technical enablement staff (developer-level) who present to a broad mix of customer contacts — IT admins, compliance officers, DevOps engineers, and operations managers.

The deck is **not** a live runnable demo. It is a narrative with annotated API call sequences that partners can cherry-pick based on the customer problem in the room.

---

## Audience

**Primary:** Adobe internal partners and solution engineers who onboard customers to the Fusion API.

**Secondary (via partner):** Enterprise customers evaluating or expanding Fusion API adoption — spanning regulated industries, agencies managing multiple client tenants, and large IT organizations.

---

## Deck Structure

**Total slides:** ~14
- 1 cover slide
- 1 intro slide (API surface overview: 8 resource types, 22 endpoints)
- 6 vignettes × 2 slides each = 12 slides

Each vignette follows a fixed 2-slide template:

| Slide 1 | Slide 2 |
|---------|---------|
| Customer archetype label | API call sequence (annotated) |
| Customer pain quote | What each call returns and why it matters |
| "What they can't do today" | Outcome: what the customer can now do |

Vignettes are independent — partners present only the ones relevant to the customer.

---

## Vignettes

### Vignette 1 — Automation Inventory
**Archetype:** IT Admin / Enterprise

**Pain:** "We have 600 scenarios. We don't know what's active, what's broken, or who owns what."

**API sequence:**

| Step | Call | Purpose |
|------|------|---------|
| 1 | `GET /api/v3/scenarios` | Paginated list with status and team filters — builds a full org-wide inventory |
| 2 | `GET /api/v3/scenarios/{scenarioId}/dependencies` | For each scenario: surfaces every connection, hook, and data store it touches |
| 3 | `GET /api/v3/connections` | Cross-references which external systems are actively integrated |

**Outcome:** A complete automation portfolio map — what runs, what it touches, and who is responsible. Foundation for governance and decommissioning decisions.

---

### Vignette 2 — Safe Credential Rotation
**Archetype:** IT Admin / Security

**Pain:** "Our Salesforce API key expires Friday. We have no idea which automations will break."

**API sequence:**

| Step | Call | Purpose |
|------|------|---------|
| 1 | `GET /api/v3/connections/{connectionId}` | Identify the specific connection and its metadata |
| 2 | `GET /api/v3/connections/{connectionId}/scenarios` | Get every scenario that depends on this connection |
| 3 | `GET /api/v3/scenarios/{scenarioId}/dependencies` | Validate full blast radius — all linked hooks, data stores, and keys |

**Outcome:** Zero-surprise credential rotation. Know exactly what breaks before touching anything. Enables planned maintenance windows instead of reactive firefighting.

---

### Vignette 3 — Environment Promotion
**Archetype:** DevOps / Agency

**Pain:** "Promoting scenarios from staging to production is copy-paste work that takes days and introduces drift."

**API sequence:**

| Step | Call | Purpose |
|------|------|---------|
| 1 | `GET /api/v3/scenarios` | List staging scenarios filtered by team |
| 2 | `POST /api/v3/scenarios/export` | Export full blueprints (up to 100 at once) |
| 3 | `POST /api/v3/scenarios/{scenarioId}/clone` | Clone into production team with automatic connection, webhook, and data store substitution |
| 4 | `POST /api/v3/folders` + `PATCH /api/v3/folders/{folderId}` | Organize cloned scenarios into the correct folder structure |

**Outcome:** A repeatable, scriptable promotion pipeline. Consistent deployments across every environment — eliminates manual drift and enables agencies to onboard new client tenants at scale.

---

### Vignette 4 — Compliance & Audit Trail
**Archetype:** Compliance Officer / Regulated Industry

**Pain:** "Our auditors want a full record of every change made to our automation environment last quarter."

**API sequence:**

| Step | Call | Purpose |
|------|------|---------|
| 1 | `GET /api/v3/activity-logs` | Cursor-paginated query filtered by date range — returns who did what and when |
| 2 | `GET /api/v3/activity-logs/export` | Export the full log as CSV or XLSX for offline submission |

**Outcome:** Audit-ready evidence package generated in minutes. Supports regulatory reporting, SIEM integration, and internal governance workflows without requiring manual UI reconstruction.

---

### Vignette 5 — Operations Cost Allocation
**Archetype:** Operations Manager / Finance

**Pain:** "Finance wants to know which teams are burning through our automation quota — and why."

**API sequence:**

| Step | Call | Purpose |
|------|------|---------|
| 1 | `GET /api/v3/operations` | Operation counts filtered by team, scenario, or package over a custom date range (up to 1 year) |
| 2 | `GET /api/v3/operations/summary` | Org-wide breakdown by scenario and team — identifies the highest consumers |

**Outcome:** Accurate cost allocation data surfaced programmatically. Enables chargeback reporting, quota planning, and early detection of runaway automations before limits are hit.

---

### Vignette 6 — Incident Investigation
**Archetype:** DevOps / SLA-sensitive Operations

**Pain:** "A critical process failed at 3am. By morning no one knows what happened or where to start."

**API sequence:**

| Step | Call | Purpose |
|------|------|---------|
| 1 | `GET /api/v3/logs` | List executions for the scenario filtered by failure or warning status |
| 2 | `GET /api/v3/logs/{executionId}` | Get full execution detail including module-level context |
| 3 | `GET /api/v3/activity-logs` | Cross-reference with recent config changes — catches "someone changed something" scenarios |

**Outcome:** A structured investigation path that cuts mean-time-to-resolution. Operations teams get full context without needing UI access or waiting on a Fusion admin.

---

## API Reference Summary

All endpoints used in this deck are part of the Fusion API v3 at `https://fusion.adobe.io`.

| Resource | Endpoints Used |
|----------|---------------|
| Scenarios | `GET /scenarios`, `GET /scenarios/{id}`, `GET /scenarios/{id}/dependencies`, `POST /scenarios/export`, `POST /scenarios/{id}/clone` |
| Folders | `GET /folders`, `POST /folders`, `PATCH /folders/{id}` |
| Connections | `GET /connections`, `GET /connections/{id}`, `GET /connections/{id}/scenarios` |
| Hooks | `GET /hooks`, `GET /hooks/{id}` |
| Data Stores | `GET /data-stores`, `GET /data-stores/{id}` |
| Activity Logs | `GET /activity-logs`, `GET /activity-logs/export` |
| Operations | `GET /operations`, `GET /operations/summary` |
| Logs | `GET /logs`, `GET /logs/{id}` |

Authentication uses OAuth Server-to-Server via Adobe Developer Console. All requests require `Authorization`, `x-api-key`, `x-organization-id`, and `x-gw-region` headers.

---

## Slide Annotation Guidelines

Each API call annotation on the deck should include:
- The HTTP method and endpoint path
- One sentence on what it returns
- One sentence on why that matters for the use case

Avoid showing full request/response payloads in the deck — link to the API reference for details.

---

## Out of Scope

- Runnable Postman collection or live demo environment (separate deliverable)
- Hooks and Data Stores vignettes (endpoints exist but no standalone customer problem identified — fold into Vignette 1 as supporting detail)
- Future API capabilities (scenario create/update, full lifecycle management) — note as "coming soon" on the intro slide only
