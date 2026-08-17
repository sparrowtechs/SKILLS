# Frontend Security

## Purpose

Use this guide to review browser-facing applications, server-rendered UI, SPA frontends, and client-side flows before deployment.

## Use This When

Use this guide when:

- reviewing browser-facing token handling and session behavior
- checking XSS, markup rendering, and third-party script exposure
- deciding whether the UI creates false security assumptions
- reviewing cache, CSP, and browser policy behavior

## Core Rules

### 1. The Frontend Is Not a Security Boundary

Hiding a button, route, or field is not authorization.

### 2. Browsers Need Explicit Safety Controls

CSP, origin separation, cache behavior, and content-serving decisions need to match the actual app behavior, not generic defaults.

### 3. Rendered Content Is a Security Surface

Any HTML, markdown, upload, or third-party script that reaches the browser should be treated as an active attack surface.

### 4. Sensitive Data Should Leave as Little Trace as Possible

URLs, local storage, client bundles, logs, and browser caches all expand exposure if you let them.

### 5. Browser Controls Are a Second Layer, Not the First

CSP, cookie settings, origin policy, and headers can reduce damage, but they do not excuse unsafe rendering or weak server-side authorization.

## Review Areas

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

## Durability Checks

Use these checks to keep frontend security grounded in durable browser realities instead of framework fashion.

### 1. Keep Trust Decisions on the Server

If a flow is only safe because the client hides, filters, or disables something, the safety is cosmetic.

Re-check whether the server still holds if the browser is bypassed entirely.

### 2. Separate Trusted and Untrusted Content Deliberately

Do not mix first-party application code, third-party scripts, and user-supplied content on the same assumptions.

Review whether:

- user content is isolated from the main app origin when needed
- rich content is sanitized before rendering
- third-party scripts are limited to vendors you would explicitly trust in an incident review

### 3. Minimize What JavaScript Can Reach

If a token, secret, or sensitive value can be read from browser JavaScript, injected code may be able to read it too.

Prefer designs that reduce long-lived browser-visible credentials and keep sensitive session material out of URLs and unnecessary client storage.

### 4. Test Real Browser Failure Modes

Do not stop at happy-path page loads.

Check what happens when:

- CSP blocks a resource
- a session expires mid-flow
- a cached page is revisited on a shared machine
- untrusted markup or uploads are rendered in the browser

Frontend security should remain understandable and safe when the browser behaves like a hostile environment, not a cooperative one.

## References Used To Shape This Guide

- OWASP ASVS web frontend requirements
- OWASP Content Security Policy Cheat Sheet
- OWASP HTTP Security Response Headers Cheat Sheet
- OWASP Cross Site Scripting Prevention Cheat Sheet
