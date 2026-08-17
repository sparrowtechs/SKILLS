# Storage Security

## Purpose

Use this guide to review object storage, file uploads, download links, asset buckets, blob stores, and backup storage before deployment.

## Use This When

Use this guide when:

- reviewing object storage and bucket exposure
- checking upload and download behavior
- deciding whether signed URL usage and public asset serving are safe enough
- tightening storage controls before launch

## Core Rules

### 1. Storage Should Be Private by Default

Public access should be a deliberate product decision, not a leftover configuration state.

### 2. Uploaded Files Are Untrusted

Every upload flow needs controls around type, size, serving origin, and active content risk.

### 3. Temporary Access Must Actually Be Temporary

Signed URLs, scoped tokens, and shared credentials lose their value when they are broad or long-lived.

### 4. Copies and Replicas Carry the Same Risk

Backups, replicated buckets, exports, and CDN-backed origins need the same scrutiny as the primary storage path.

## Review Areas

### Access Control

- `Critical` Public access is disabled by default for buckets, containers, and object paths unless the system is intentionally serving public files.
- `Critical` Bucket policies, IAM roles, and ACLs do not grant broader access than the application requires.
- `High` Shared keys and long-lived broad credentials are replaced with narrower identity-based access or short-lived scoped credentials where the platform supports them.
- `High` Cross-account or vendor access is scoped narrowly and reviewed.

### Upload and Download Safety

- `Critical` Upload flows enforce type and size limits.
- `Critical` Signed upload and download URLs are short-lived and scoped to one object or narrowly defined path.
- `High` Uploaded files are treated as untrusted content.
- `High` User files that can carry active content are not served from the main application origin without isolation or explicit content-serving controls.
- `High` Content disposition and rendering behavior are chosen intentionally to reduce stored XSS and content-sniffing risk.

### Encryption and Transport

- `High` Encryption at rest is enabled for stored objects.
- `High` TLS is required in transit.
- `High` Key management configuration is documented, especially when customer-managed keys are used.

### Logging, Versioning, and Recovery

- `High` Access logging or audit logging is enabled for buckets that store customer data, backups, uploads, or sensitive internal files.
- `High` Versioning, retention, or object-lock style controls are enabled when accidental deletion or tampering would be high impact.
- `High` Backups, exports, and replicated buckets are reviewed for the same exposure risks as primary storage.
- `High` Monitoring or alerts exist for public exposure, policy changes, and unusual access patterns where the platform supports them.

### Operational Guardrails

- `High` Static website hosting or CDN exposure is configured intentionally, not by accident.
- `High` Policy-as-code checks, public-access blocks, or equivalent guardrails are enabled where the platform supports them.
- `Medium` Old test buckets, orphaned uploads, and expired vendor access are cleaned up.

## Output Format

When using this guide, respond with:

1. Storage surface reviewed
2. Blocking issues
3. Other storage findings
4. Specific fixes
5. Storage ship verdict: `Block`, `Revise`, or `Ready`

## Durability Checks

Use these checks to keep storage security strong after the first bucket policy review.

### 1. Treat Every Access Link as a Credential

Signed URLs, upload tokens, shared access signatures, and temporary links are bearer credentials.

Review them as if leaked links will be copied, cached, forwarded, and logged.

### 2. Keep User-Controlled Content Away From Trusted Origins

Storage becomes dangerous when untrusted files are served in a way that lets the browser treat them like trusted app content.

Re-check origin separation, content disposition, content type handling, and whether active content can run where it should only be downloaded.

### 3. Secure the Entire File Lifecycle

Uploads are only the start.

Check:

- pre-upload authorization
- post-upload scanning or validation
- download authorization
- retention and deletion behavior
- backup and replication exposure

### 4. Continuously Look for Forgotten Exposure

Storage leaks often come from drift:

- old test buckets
- stale vendor access
- expired-but-still-valid sharing patterns
- replicated buckets with weaker policy

If storage review only checks the primary happy path, it will miss where real leaks happen.

## References Used To Shape This Guide

- OWASP File Upload Cheat Sheet
- OWASP ASVS file handling requirements
- vendor-neutral object storage access-control and signed URL guidance
