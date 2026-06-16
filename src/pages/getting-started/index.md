---
title: Getting Started
description: Learn what is Workfront Fusion APIs and how to use
keywords:
  - Workfront Fusion API
contributors:
  - 'https://github.com/annieTechno'
hideBreadcrumbNav: true
---

# Getting Started   

## Introducing the Workfront Fusion API

The **public API release** for the Workfront Fusion API marks an exciting milestone for programmatically managing and automating Fusion workflows. Built on **API version 3**, the Fusion API will enable developers to integrate Fusion capabilities directly into their applications, automate scenario management, and build custom automation solutions.

## Experimental Phase

<InlineAlert variant="info" slots="text" />

The Fusion API is currently in an **experimental phase** as we actively develop and refine the capabilities. This designation means that while the API is functional and ready for integration, endpoints, request/response structures, and features may evolve based on user feedback and technical requirements. We recommend staying updated with the latest documentation.

## Getting Started with Integration

To begin integrating with the Workfront Fusion API, follow these steps:

1. **[Credentials](./credentials/index.md)** - Set up OAuth Server-to-Server authentication through the Adobe Developer Console

2. **[Authentication Guide](./authentication/index.md)** - Learn how to generate and use access tokens to securely call the Fusion API

3. **[API Headers](./api_headers/index.md)** - Understand the required headers for properly formatting your API requests

4. **[Technical Accounts](./technical_accounts/index.md)** - Configure permissions for technical accounts to control access

5. **[Usage Notes](./usage_notes/index.md)** - Review API usage guidelines and best practices

## Current Features

The Fusion API currently supports the following capabilities, enabling enterprise teams to build powerful integrations and automation management tools:

### Scenario Management
- **Discover and audit your automation portfolio** — List and search all scenarios across your organization, making it easy to inventory thousands of automations across departments or business units
- **Export scenario blueprints at scale** — Download full configuration blueprints for up to 100 scenarios per request, enabling backup pipelines, compliance reviews, and cross-environment migration workflows
- **Clone scenarios programmatically** — Replicate any scenario into a target team with automatic substitution of connections, webhooks, data stores, and data structures — ideal for provisioning new client environments or onboarding teams with pre-built templates
- **Inspect scenario dependencies** — Retrieve the full dependency graph for any scenario, including all linked connections, data stores, hooks, and keys, to support impact analysis before making infrastructure changes

### Organization and Folder Structure
- **Manage scenario folders** — Create, rename, and delete folders to keep large automation libraries organized by project, team, or function
- **Query folder metadata** — Retrieve folder lists with scenario counts, supporting dashboards that reflect your organization's automation structure

### Connection Visibility
- **Inventory all integration connections** — List and retrieve details for every connection in your organization, enabling governance workflows that track which external systems are integrated
- **Map connections to scenarios** — Identify every scenario that depends on a given connection, so you can assess risk before rotating credentials or deprecating an integration

### Hook Management
- **Discover and inspect webhooks** — List all configured webhooks across teams, or retrieve full configuration details for a specific hook, supporting security audits and documentation generation

### Data Store Oversight
- **Monitor data store usage** — List all data stores with size and record count metrics, supporting capacity planning and cost optimization across enterprise tenants
- **Retrieve data store details** — Access metadata for individual data stores to support governance, lifecycle management, and data residency reviews

### Execution Logs and Monitoring
- **Query execution history** — Retrieve paginated execution records for any scenario, filtered by status (warnings, failures), to power operational dashboards and SLA reporting
- **Inspect individual executions** — Get detailed summaries for specific scenario runs, including the object context, to accelerate incident investigation and root cause analysis

### Operations Reporting
- **Track API operation consumption** — Retrieve operation counts filtered by team, scenario, or package over any custom date range (up to one year), enabling accurate cost allocation and quota management
- **Get organization-wide summaries** — Access high-level operation breakdowns by scenario and team to identify automation hotspots and optimize usage across your organization

### Activity Logs and Compliance
- **Audit organization activity** — Access a full, cursor-paginated activity log for your organization, giving compliance and security teams the visibility they need for regulatory reporting
- **Export audit logs** — Export activity data as CSV or XLSX for offline analysis, audit submissions, or integration with SIEM and governance platforms

## What's Next

The current API focuses on visibility and reporting. Future work is oriented around:

- **Full lifecycle management** — Create, update, and delete automation resources through code
- **Enterprise governance** — Consistent, auditable automation management across teams and environments

## Next Steps

Once you've completed the setup process, you'll be ready to explore available endpoints in the [API Reference](../api/index.md). Additional capabilities for building automations, integrating Fusion into your applications, and creating custom tooling will become available as the API continues to evolve.

Let's get started building with the Workfront Fusion API!
