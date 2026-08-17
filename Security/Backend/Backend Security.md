# Backend Security

## Purpose

Use this guide to review backend services, APIs, server actions, worker processes, and privileged server-side logic before deployment.

## Use This When

Use this guide when:

- reviewing backend auth and authorization behavior
- checking server-side validation and injection resistance
- reviewing webhook, queue, cron, or admin surfaces
- deciding whether a backend is safe enough to expose or ship

## Core Rules

### 1. The Server Must Be the Real Gatekeeper

Every protected action must be enforceable at the backend boundary, not merely suggested by the UI.

### 2. Resource Access Must Be Checked Per Request

Do not trust route structure, hidden IDs, tenant assumptions, or controller wiring to preserve object-level authorization automatically.

### 3. Validation Must Happen Before Dangerous Use

Validate request structure, content types, and limits before the request reaches query execution, shell execution, file handling, or outbound calls.

### 4. Outbound Trust Must Be Narrow

Webhooks, callbacks, signed requests, server-side fetches, and third-party integrations must be treated as untrusted until verified.

### 5. Production Hardening Is Part of Backend Security

If debug routes, metrics endpoints, or broad admin surfaces are exposed carelessly, the backend is not secure even if the application logic is correct.

## Review Areas

### Authentication and Session Handling

- `Critical` Every non-public endpoint rejects unauthenticated requests.
- `Critical` Authentication is enforced server-side for every protected route.
- `Critical` Session or token verification checks signature, expiry, and required issuer or audience constraints.
- `High` Refresh tokens, session invalidation, and logout behavior are implemented and tested.
- `High` Sensitive operations such as password changes, payout changes, account recovery, and admin actions require a fresh auth check or step-up verification.

### Authorization

- `Critical` Object-level authorization is enforced for every request that reads or mutates a specific resource.
- `Critical` Role or permission checks exist for privileged actions.
- `Critical` Multi-tenant isolation is enforced in queries, service logic, and background jobs.
- `High` ID tampering tests have been run against representative endpoints.
- `High` Protected fields cannot be overwritten through mass assignment.

### Input Validation and Injection

- `Critical` Request bodies, query params, headers, and path params are validated server-side.
- `Critical` Request content types are validated and unsupported content types are rejected.
- `Critical` SQL, NoSQL, shell, template, and command injection risks are prevented by parameterized APIs, strict validation, and no unsafe string-built execution paths.
- `High` Request body size, pagination, and expensive query paths have sane limits.
- `High` Redirect targets, callback URLs, and webhook destinations are validated rather than trusted blindly.

### Secrets and Sensitive Data

- `Critical` Secret keys and database credentials stay on the server and never reach the client bundle or logs.
- `High` Secrets are injected through environment or secret-management tooling, not hardcoded.
- `High` Credentials, tokens, and other sensitive values are not placed in URLs or query strings.
- `High` Sensitive responses are minimized to the fields the client actually needs.
- `High` Internal admin routes, cron endpoints, and webhook endpoints are protected by authentication, network restriction, shared secret verification, or equivalent server-side controls.

### API and Protocol Controls

- `High` Allowed HTTP methods are defined per route, and unsupported methods fail clearly.
- `High` Response content types are set deliberately and do not leave browsers or clients guessing.
- `High` State-changing endpoints that may be retried define idempotency or duplicate-delivery handling.
- `High` Management, health, metrics, and admin endpoints are protected according to their exposure risk.

### Outbound Calls and Integrations

- `Critical` Server-side URL fetching is protected against SSRF with URL validation, host allowlists, or blocked access to private network targets.
- `High` Third-party webhooks are verified with signatures or another cryptographic authenticity check before processing.
- `High` Timeouts, retry limits, and failure behavior are defined so integrations fail safely.

### Errors, Logging, and Production Hardening

- `Critical` Production responses do not expose stack traces, SQL statements, tokens, or internal paths.
- `High` Security-relevant events are logged without leaking secrets.
- `High` Audit logs exist for authentication failures, privilege changes, sensitive configuration changes, and access denials.
- `High` Debug tooling, test routes, and development shortcuts are disabled in production.
- `High` Rate limiting or equivalent anti-abuse controls exist for login, signup, password reset, search, and other expensive endpoints.

## Output Format

When using this guide, respond with:

1. Backend surface reviewed
2. Blocking issues
3. Other backend findings
4. Specific fixes
5. Backend ship verdict: `Block`, `Revise`, or `Ready`

## Durability Checks

Use these checks to keep backend security durable under real production behavior rather than clean demo traffic.

### 1. Derive Authority From Verified Server Context

Do not let the backend decide access from client-supplied IDs, roles, tenant hints, or hidden fields when a verified server-side identity should be the source of truth.

### 2. Treat Retries and Replays as Normal Conditions

Queued jobs, webhook deliveries, browser retries, and mobile reconnects all create repeated execution.

Security-sensitive operations should remain correct when requests arrive twice, out of order, or after partial failure.

### 3. Narrow Outbound Trust

Every webhook source, callback target, fetch target, and integration credential expands the backend trust boundary.

Prefer allowlists, signature verification, short-lived credentials, and explicit failure handling over broad network trust.

### 4. Protect the Operational Surfaces Too

Health checks, admin routes, task runners, cron endpoints, metrics, and debug paths are often easier to abuse than the main API.

If those surfaces are weak, the backend is still weak.

## References Used To Shape This Guide

- OWASP ASVS API and authorization requirements
- OWASP SSRF Prevention Cheat Sheet
- OWASP Input Validation and SQL Injection guidance
