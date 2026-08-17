# Database Security

## Purpose

Use this guide to review relational and non-relational databases, data stores, caches, and database-connected deployment choices before launch.

## Use This When

Use this guide when:

- reviewing database privileges and exposure
- checking whether production data handling is actually safe
- deciding whether migrations, backups, and restore paths are secure enough
- tightening database access before launch

## Core Rules

### 1. The Database Should Not Trust the Application More Than Necessary

Do not let runtime applications operate as superusers or broad administrative roles by default.

### 2. Exposure Must Stay Deliberate

A database that is casually reachable, broadly credentialed, or copied freely into lower environments is already weak before any injection bug appears.

### 3. Backups and Replicas Count Too

Security posture is not limited to the primary database instance.

### 4. Sensitive Data Handling Includes Lifecycle

Collection, masking, retention, restore, and deletion are all part of database security.

## Review Areas

### Access and Network Exposure

- `Critical` The database is not publicly reachable from the internet unless there is a documented and approved reason.
- `Critical` Access is restricted to the minimum required hosts, networks, roles, or service identities.
- `Critical` Applications do not connect as database superusers for normal runtime operations.
- `High` Admin tools such as phpMyAdmin, pgAdmin, or vendor consoles are protected and not casually internet-exposed.

### Authentication and Permissions

- `Critical` Default database credentials are not in use.
- `Critical` Application roles use least privilege.
- `Critical` Different services or jobs use separate credentials when they need different access levels.
- `High` Sensitive administrative actions require stronger access controls than normal application traffic.
- `High` Rotation and revocation of credentials are possible without prolonged downtime.

### Transport, Encryption, and Data Protection

- `Critical` Database traffic uses encrypted transport where traffic leaves a trusted local boundary.
- `High` Sensitive data at rest is encrypted using platform or engine controls.
- `High` Especially sensitive columns or fields use additional controls such as column encryption, masking, tokenization, or strict access separation when needed.
- `High` Production data is not copied into lower environments without masking, minimization, or anonymization.

### Queries, Integrity, and Operations

- `Critical` Queries are parameterized and do not concatenate untrusted input into executable statements.
- `High` Migrations and schema changes are reviewed for security impact, not only correctness.
- `High` Audit or activity logging exists for administrative actions and sensitive data access where the platform supports it.
- `High` Backup, restore, and replication paths are protected like the primary database.
- `High` Restore procedures are tested rather than assumed to work.

### Hardening and Lifecycle

- `High` Unused features, extensions, and default sample data are removed or disabled.
- `High` Database version support status and pending security patches are checked before launch.
- `Medium` Retention, archival, and deletion behavior for sensitive records is documented.

## Output Format

When using this guide, respond with:

1. Database surface reviewed
2. Blocking issues
3. Other database findings
4. Specific fixes
5. Database ship verdict: `Block`, `Revise`, or `Ready`
