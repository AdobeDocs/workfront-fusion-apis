# Changelog

## June 17, 2026

### Added

- `GET` **List connections** — List connections
- `GET` **Get connection by ID** — Get connection by ID
- `GET` **List scenarios for a connection** — List scenarios for a connection
- `GET` **List data stores by team** — List data stores by team
- `GET` **Get a single data store by ID** — Get a single data store by ID
- `GET` **Get folders** — Get folders
- `POST` **Create a folder** — Create a folder
- `DELETE` **Delete folder** — Delete folder
- `PATCH` **Update folder** — Update folder
- `GET` **List and search hooks** — List and search hooks
- `GET` **Get a hook by ID** — Get a hook by ID
- `GET` **List Executions** — List Executions
- `GET` **Get Execution** — Get Execution
- `GET` **List scenarios** — List scenarios
- `POST` **Export scenario blueprints** — Export scenario blueprints
- `GET` **Get scenario by ID** — Get scenario by ID
- `POST` **Clone scenario** — Clone scenario
- `GET` **Get scenario dependencies** — Get scenario dependencies

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

- `GET` **Get activity logs** — Get activity logs
- `GET` **Export activity logs** — Export activity logs
- `GET` **Get operations count** — Get operations count
- `GET` **Get operations summary** — Get operations summary

---
