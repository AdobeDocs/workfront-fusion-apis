# Changelog

## October 29, 2026

### Modified

- `GET` **List Executions**
    - `scenarioId` and `dlqId` can be omitted for organization-wide search
    - Added response field: `items[].errorCode`
    - Added response field: `items[].errorMessage`
    - Added response field: `items[].deactivated`
    - Added response field: `items[].deactivationReason`
    - Changed response field type: `items[].modules[]` (now an object with `package`, `module`, `operations`)
- `GET` **Get Execution**
    - Added response field: `errorCode`
    - Added response field: `errorMessage`
    - Added response field: `deactivated`
    - Added response field: `deactivationReason`
    - Changed response field type: `modules[]` (now an object with `package`, `module`, `operations`)

## October 23, 2026

### Added

- `POST` **Validate a blueprint**
- `POST` **Clone a connection**
- `GET` **Get a connector asset**
- `GET` **Get a key type asset**
- `GET` **Get a hook asset**
- `GET` **Get Execution Details**
- `GET` **Get Execution Bundles**
- `DELETE` **Delete DLQs for a scenario**
- `PATCH` **Update DLQ blueprint or module**
- `GET` **Get DLQ blueprint**
- `GET` **Get DLQ data bundle**

## October 12, 2026

### Added

- `GET` **List scenarios that depend on a resource**
- `DELETE` **Delete scenario**
- `DELETE` **Delete connection**
- `DELETE` **Delete key**
- `GET` **List hooks that depend on a resource**
- `POST` **Clone a hook**
- `DELETE` **Delete hook**
- `GET` **Get hook dependencies**
- `GET` **List data stores that depend on a resource**
- `DELETE` **Delete data store**
- `DELETE` **Delete data store records**
- `DELETE` **Delete data structure**
- `POST` **Clone a data structure**
- `GET` **Get the authorised user**
- `GET` **Get user by ID**
- `GET` **List users**
- `GET` **List teams in an organization**
- `GET` **Get a team by ID**
- `DELETE` **Delete team**
- `GET` **List organizations**
- `GET` **Get the current organization**
- `GET` **List DLQs for a scenario**
- `GET` **Get DLQ by ID**

### Modified

- `GET` **Get scenario by ID**
    - Added parameter: `fields`
- `GET` **List scenarios**
    - Added parameter: `fields`
- `GET` **Get scenario dependencies**
    - Changed response field type: `items[].kind` (added allowed value: `scenario`)


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


## February 1, 2026

### Added

- `GET` **Get activity logs**
- `GET` **Export activity logs**
- `GET` **Get operations count**
- `GET` **Get operations summary**