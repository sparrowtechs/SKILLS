# Backend Security Checklist

## Purpose

Use this checklist to review backend services, APIs, server actions, worker processes, and privileged server-side logic before deployment.

## Focus

This guide is especially concerned with:

- broken access control
- unsafe authentication and session handling
- injection risks
- insecure outbound requests
- unsafe file handling
- dangerous production misconfiguration

## Checklist

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
- `Critical` SQL, NoSQL, shell, template, and command injection risks are prevented by parameterized APIs, strict validation, and no unsafe string-built execution paths.
- `High` Request body size, pagination, and expensive query paths have sane limits.
- `High` Redirect targets, callback URLs, and webhook destinations are validated rather than trusted blindly.

### Secrets and Sensitive Data

- `Critical` Secret keys and database credentials stay on the server and never reach the client bundle or logs.
- `High` Secrets are injected through environment or secret-management tooling, not hardcoded.
- `High` Sensitive responses are minimized to the fields the client actually needs.
- `High` Internal admin routes, cron endpoints, and webhook endpoints are protected by authentication, network restriction, shared secret verification, or equivalent server-side controls.

### Outbound Calls and Integrations

- `Critical` Server-side URL fetching is protected against SSRF with URL validation, host allowlists, or blocked access to private network targets.
- `High` Third-party webhooks are verified with signatures or another cryptographic authenticity check before processing.
- `High` Timeouts, retry limits, and failure behavior are defined so integrations fail safely.

### Errors, Logging, and Production Hardening

- `Critical` Production responses do not expose stack traces, SQL statements, tokens, or internal paths.
- `High` Security-relevant events are logged without leaking secrets.
- `High` Debug tooling, test routes, and development shortcuts are disabled in production.
- `High` Rate limiting or equivalent anti-abuse controls exist for login, signup, password reset, search, and other expensive endpoints.

## Output Format

When using this guide, respond with:

1. Backend surface reviewed
2. Blocking issues
3. Other backend findings
4. Specific fixes
5. Backend ship verdict: `Block`, `Revise`, or `Ready`
