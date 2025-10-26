# API Documentation (Draft)

> **Status:** This document captures the planned API surface for the Super Data Viewer platform. Detailed schemas and examples will be iterated alongside implementation.

## Authentication & Authorization
- OAuth2 authorization code flow issues JWT access and refresh tokens.
- All endpoints require HTTPS and expect a `Bearer` token in the `Authorization` header.
- Role-based scopes control access to ingestion pipelines, analysis execution, configuration, and administration APIs.

## REST API Overview
| Domain | Base Path | Description |
|--------|-----------|-------------|
| Authentication | `/api/v1/auth` | Token issuance, refresh, password reset, and multi-factor endpoints |
| Users & Roles | `/api/v1/users` | User CRUD, role assignments, invitation workflows, audit retrieval |
| Data Sources | `/api/v1/data-sources` | Registration of local/remote sources, credential management |
| Imports | `/api/v1/imports` | Launch import jobs, monitor status, preview data, rollback versions |
| Datasets | `/api/v1/datasets` | Browse datasets, metadata updates, permissions, version history |
| Pipelines | `/api/v1/pipelines` | Create/update analytic workflows, parameter templates, execution runs |
| Scripts | `/api/v1/scripts` | Upload/manage sandboxed scripts, execution results, resource quotas |
| Visualizations | `/api/v1/visualizations` | Chart configuration, layout persistence, export jobs |
| Monitoring | `/api/v1/monitoring` | Metrics snapshots, log queries, alert acknowledgements |

### Sample Endpoint Structure
**Create Import Job**
- `POST /api/v1/imports`
- **Request Body:** multipart/form-data or JSON reference to remote source, optional preprocessing instructions.
- **Response:** Job identifier, detected schema, queued status.

**Execute Pipeline**
- `POST /api/v1/pipelines/{pipeline_id}/runs`
- **Request Body:** Parameter overrides, scheduling options, notification preferences.
- **Response:** Run identifier, estimated completion, tracking URL.

**Download Visualization Export**
- `GET /api/v1/visualizations/{viz_id}/exports/{export_id}`
- **Response:** Binary file (PNG, SVG, PDF) with appropriate content type.

## GraphQL API
- GraphQL endpoint served at `/api/graphql` with persisted queries support.
- Schema exposes types for users, datasets, pipelines, visualizations, and telemetry snapshots.
- Subscriptions stream run progress, alert events, and collaborative session updates.

## Webhooks & Integrations
- Outbound webhook subscriptions notify third-party systems about import completion, pipeline results, and alerts.
- Payloads are signed with rotating secrets managed via Vault.
- Retry policies with exponential backoff ensure reliable delivery.

## Rate Limiting & Throttling
- Tiered rate limits enforced per client ID and user role.
- Bulk operations (batch imports, large exports) require asynchronous workflow IDs to avoid timeouts.

## Error Handling
- REST APIs adopt standardized error envelopes: `{ "error": { "code": "...", "message": "...", "details": [...] } }`.
- GraphQL errors include `extensions` metadata for correlation IDs and remediation hints.
- HTTP status codes follow RFC 7231, with 429 for rate limits and 503 for temporary service unavailability.

## Versioning Strategy
- REST endpoints follow semantic versioning under `/api/v{n}` prefixes.
- Deprecation notices supplied via `Sunset` headers and developer portal announcements.

## API Tooling
- OpenAPI 3 specifications generated automatically and published to the developer portal.
- SDKs (Python, TypeScript) provide typed clients with helpers for authentication and pagination.
