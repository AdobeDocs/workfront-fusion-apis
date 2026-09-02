# Changelog

## September 2, 2026

### Added

- `GET` **List data store records**
- `GET` **List data structures**
- `GET` **Get a data structure by ID**
- `GET` **List hook queue**
- `DELETE` **Delete a hook queue**
- `GET` **Get hook queue statistics**
- `GET` **Get a hook queue item by ID**
- `GET` **List keys**
- `GET` **Get a key by ID**
- `GET` **List scenario versions**
- `GET` **Get scenario version blueprint**
- `GET` **Get user regions, organizations**

### Modified

- **All endpoints** — Error response field renamed: `report.x-gw-ims-org-id` → `report.x-organization-id`
- `GET` **Get scenario by ID**
    - Added response field: `deleted`
    - Added response field: `deletedBy`
- `GET` **List scenarios**
    - Added response field: `deleted`
    - Added response field: `deletedBy`
- `POST` **Clone scenario**
    - Added request body field: `continueFromLastProcessed`
    - `teamId` is no longer required in request body
- `GET` **Get folders**
    - Removed parameter: `teamId`
    - Added response field: `teamId`
- `PATCH` **Update folder**
    - Added response field: `teamId`
- `GET` **List hooks**
    - Removed parameter: `teamId`
    - Added response field: `data`
- `GET` **List data stores** and **Get a data store by ID**
    - Added response field: `spec`
    - Added response field: `strict`
    - Added response field: `dataStructureId`
    - Removed response field: `datastructureId`

---

## June 17, 2026

### Added

- `GET` **List connections**
- `GET` **Get connection by ID**
- `GET` **List scenarios for a connection**
- `GET` **List data stores by team**
- `GET` **Get a single data store by ID**
- `GET` **Get folders**
- `POST` **Create a folder**
- `DELETE` **Delete folder**
- `PATCH` **Update folder**
- `GET` **List and search hooks**
- `GET` **Get a hook by ID**
- `GET` **List Executions**
- `GET` **Get Execution**
- `GET` **List scenarios**
- `POST` **Export scenario blueprints**
- `GET` **Get scenario by ID**
- `POST` **Clone scenario**
- `GET` **Get scenario dependencies**

### Modified

- `GET` **Get operations count**
    - Removed parameter: `groupBy`
    - Removed parameter: `orderBy`
    - Added parameter: `groupby`
    - Added parameter: `orderby`
    - Added parameter: `x-organization-id`
    - `organizationId` parameter is no longer required
- `GET` **Get operations summary**
    - Removed parameter: `orderBy`
    - Added parameter: `orderby`
    - Added parameter: `x-organization-id`
    - `organizationId` parameter is no longer required
- `GET` **Get activity logs**
    - Removed path parameter: `orgId`
    - Added parameter: `x-organization-id`
- `GET` **Export activity logs**
    - Removed path parameter: `orgId`
    - Added parameter: `x-organization-id`

---

## February 1, 2026

### Added

- `GET` **Get activity logs**
- `GET` **Export activity logs**
- `GET` **Get operations count**
- `GET` **Get operations summary**

---
