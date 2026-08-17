# Deployment Security

## Purpose

Use this guide before deploying any public-facing product, internal tool, API, backend, database-connected app, or storage-backed workflow.

The goal is not to produce security theater.

The goal is:

> **Catch the security mistakes that most often reach production because teams assume they are already handled.**

This guide stays practical. It focuses on controls that can be verified before release.

## Use This When

Use this guide when:

- preparing for a production release
- reviewing a staging environment before launch
- checking whether a feature is safe to ship
- auditing a project that was built quickly and needs a deployment gate
- verifying security across frontend, backend, database, and storage boundaries

Do not use this guide as a substitute for:

- threat modeling for high-risk systems
- a full penetration test
- incident response
- compliance-specific legal advice

## Core Rules

### 1. Verify the Deployed Reality

Do not decide security readiness only from repository code or a local story about how production works.

Check the deployed or deployable environment directly.

### 2. Remove Unsafe Defaults Before Launch

Debug mode, broad CORS, public buckets, default credentials, sample data, and development shortcuts should be removed before they become the production baseline.

### 3. Treat Launch as a Privilege Check

A system is not ready to ship if it still has:

- broken access control
- exposed secrets
- over-broad runtime privileges
- unsafe upload or storage behavior
- production data handling gaps

### 4. Exceptions Must Be Explicit

If a high-risk issue is accepted temporarily, document the owner, reason, and follow-up plan before launch.

## Severity

- `Critical`: do not ship until fixed
- `High`: fix before public launch unless there is a documented exception
- `Medium`: fix soon, but does not always block launch

## Review Areas

### 1. Secrets and Credentials

- `Critical` No secrets, service-role keys, database passwords, or signing keys are committed to the repository.
- `Critical` Production secrets are stored in a secrets manager or protected deployment environment, not in source control or client code.
- `Critical` Exposed or previously leaked keys have been rotated.
- `High` Different environments use different secrets.
- `High` Access to deployment secrets is limited to the minimum set of people and systems.

### 2. Authentication and Session Security

- `Critical` All non-public routes and actions require authentication.
- `Critical` Authentication checks are enforced on the server, not only in the UI.
- `Critical` Sessions or tokens expire and support server-side invalidation or immediate revocation.
- `High` Sensitive actions such as password change, payout change, admin actions, or account recovery require re-authentication or a step-up check.
- `High` Cookies, if used for authenticated sessions, are configured with `Secure`, `HttpOnly`, and an intentional `SameSite` policy.
- `High` Credentials are never accepted through query parameters or stored in logs.

### 3. Authorization and Access Control

- `Critical` Every request that accesses user or tenant data verifies the caller is allowed to access that exact resource.
- `Critical` Admin-only and staff-only actions are enforced server-side.
- `Critical` Hidden UI controls are not treated as authorization.
- `High` Object-level access checks are tested by changing IDs, tenant IDs, or route parameters.
- `High` Sensitive fields such as roles, prices, flags, and ownership cannot be mass-assigned by the client.

### 4. Input, Output, and File Handling

- `Critical` All untrusted input is validated on the server with explicit type, format, length, and range checks.
- `Critical` Database queries use parameterized queries or ORM patterns that do not concatenate untrusted input into queries.
- `Critical` Dangerous output is escaped or encoded for its rendering context.
- `High` File uploads enforce allowed types, file size limits, storage isolation, and server-side verification of the uploaded content type.
- `High` User-supplied content is not executed as code or rendered from a privileged origin without protection.

### 5. Transport and Browser-Facing Security

- `Critical` HTTPS is enforced for all production traffic.
- `High` HSTS is enabled on production HTTPS responses unless the deployment has a documented reason not to use it.
- `High` CORS is restricted to known origins and does not use wildcard settings on authenticated endpoints.
- `High` Security headers are set intentionally for the app type, including `Content-Security-Policy`, `X-Content-Type-Options`, `Referrer-Policy`, and clickjacking protection for browser-rendered pages.
- `Medium` Mixed-content and insecure third-party asset loading have been checked.

### 6. Error Handling and Logging

- `Critical` Production errors shown to users do not reveal stack traces, SQL, secrets, internal URLs, or filesystem paths.
- `High` Security-relevant events are logged, including login failures, privilege changes, sensitive configuration changes, and access denials.
- `High` Logs do not store passwords, tokens, session IDs, raw secrets, or full sensitive personal records.
- `High` Monitoring and alerting exist for unusual spikes in auth failures, access denials, or server errors.

### 7. Dependencies, Configuration, and Deployment Safety

- `Critical` Debug mode, test endpoints, admin backdoors, and development-only tools are disabled in production.
- `Critical` Default credentials are not in use anywhere in the deployed stack.
- `High` Dependencies and base images are checked for known critical vulnerabilities before release.
- `High` Environment-specific configuration is checked so development settings do not leak into production.
- `High` Branch protections, review requirements, or equivalent release controls protect the deployment path.

### 8. Data Protection

- `Critical` Sensitive data is only collected if it is actually needed.
- `High` Sensitive data is encrypted in transit and encrypted at rest when stored in databases, object storage, backups, or managed services.
- `High` Backups, exports, and replicas use access controls and encryption comparable to the primary system.
- `High` Test and staging environments do not contain unmasked production data unless there is an approved exception.
- `High` Retention and deletion behavior for sensitive data is documented and implemented in operations or code.

### 9. Database and Storage Boundaries

- `Critical` The application does not connect to the database or storage layer with unnecessarily broad privileges.
- `Critical` Public storage access is disabled unless the system is intentionally serving public files and that exposure is documented.
- `High` Database and storage access is restricted by network rules, IAM, policy, service identity, or role.
- `High` Signed URLs, tokens, or temporary access links are short-lived and scoped narrowly.
- `High` Backup files, exports, and object storage buckets are checked for accidental exposure.

### 10. Verification Before Launch

- `Critical` The production or staging deployment has been checked directly, not only the code.
- `High` Security-sensitive flows have been tested with real negative cases, not only happy paths.
- `High` Known exceptions are documented with owner, rationale, and follow-up plan.
- `Critical` If critical items fail, deployment is blocked.

## Output Format

When using this guide, respond with:

1. Scope
   - product or system being checked
   - deployment target
   - relevant surfaces: frontend, backend, database, storage
2. Failed Critical Items
   - list each blocking issue clearly
3. Other Findings
   - high and medium issues
4. Deployment Decision
   - `Block`
   - `Revise Before Launch`
   - `Ready To Ship`
5. Next Actions
   - concrete fixes in priority order

## References Used To Shape This Guide

This guide is informed primarily by OWASP ASVS, OWASP Secure Coding Practices, OWASP database and HTTP header guidance, and deployment-focused CI/CD security practices. It is intentionally shorter and more operational than those source materials.
