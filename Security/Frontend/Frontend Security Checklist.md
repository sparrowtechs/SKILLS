# Frontend Security Checklist

## Purpose

Use this checklist to review browser-facing applications, server-rendered UI, SPA frontends, and client-side flows before deployment.

## Focus

This guide is especially concerned with:

- unsafe handling of tokens and sensitive data
- XSS and script injection risk
- dangerous CORS and browser policy gaps
- insecure frontend assumptions about authorization
- accidental exposure through URLs, local storage, or client bundles

## Checklist

### Client Data and Secrets

- `Critical` No secret keys, admin credentials, service-role keys, or private tokens are shipped to the client.
- `Critical` The client bundle is checked for accidental secret exposure.
- `High` Password reset tokens, session tokens, private keys, and sensitive identifiers are not placed into URLs, query strings, or fragments.
- `High` Sensitive session material is not persisted in local storage or session storage unless there is a documented exception.

### Auth and Authorization Boundaries

- `Critical` The UI does not assume hiding a button is equivalent to enforcing authorization.
- `High` Authenticated flows redirect, refresh, or fail closed when the session expires.
- `High` Sensitive routes, actions, and data fetching paths behave correctly for unauthenticated and unauthorized users.

### Script and Markup Safety

- `Critical` Untrusted HTML, markdown, or rich text is sanitized or isolated before rendering.
- `Critical` Dangerous direct DOM injection patterns are avoided, or the content is sanitized with a vetted sanitizer before rendering.
- `High` Third-party scripts are limited to required vendors and loaded with a deliberate trust decision.
- `High` User-uploaded or user-generated files are served from a separate origin or with controls that prevent active content from running in the main app origin.

### Browser Security Controls

- `High` `Content-Security-Policy` is defined for the app’s actual script and asset model.
- `High` `X-Content-Type-Options`, `Referrer-Policy`, and clickjacking protections are set for browser-rendered pages.
- `High` CORS settings are not treated as an authentication mechanism.
- `High` Sensitive pages and responses use appropriate cache behavior.

### Product and UX Safety

- `High` Error states shown to users do not leak internal technical detail.
- `High` Sensitive forms, uploads, and destructive actions fail clearly without exposing internal error details or leaving the UI in an ambiguous state.
- `Medium` The frontend does not over-collect user data that the system does not need.

## Output Format

When using this guide, respond with:

1. Frontend surface reviewed
2. Blocking issues
3. Other frontend findings
4. Specific fixes
5. Frontend ship verdict: `Block`, `Revise`, or `Ready`
