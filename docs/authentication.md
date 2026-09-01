# ePublication – Authentication

> This document is the single source of truth for authentication across the
> external ePublication API. It is referenced from both the
> [Announcement Import](announcement-import.md) and
> [Announcement Export](announcement-export.md) documentation instead of
> being duplicated in each.

---

## Overview

The external API has two zones, both using the same wire format
(`Authorization: Bearer <token>`) but with different credential types:

| Zone | Path prefix | Credential | Auth in requests |
|---|---|---|---|
| Public | `/public/interface/v1/**` | Personal API key issued to a registered user (personal-access-token style; no expiry, revocable) | `Authorization: Bearer <api-key>` |
| Restricted | `/interface/v1/**` | M2M OAuth2 client-credentials token (Cognito) | `Authorization: Bearer <jwt>` |

Both zones use the same header, which lets third parties integrate against
either with a single, uniform pattern (one place to configure the secret in
any HTTP client) — mirroring the GitHub/GitLab personal-access-token model.

### Planned mechanism: Technical Users (Publishing Entity self-service)

> **Status: planned, not yet live.** Target: **early October 2026**. Until this ships, the current process (request credentials via Helpcenter form) should be used.

Once released, a **Publisher** of a Publishing Entity will be able to
self-service create and manage **Technical Users** — M2M clients scoped to
that Publishing Entity:

| Attribute | Value |
|---|---|
| Created by | Publisher (of the owning Publishing Entity) |
| Credential | `clientId` + `clientSecret` (OIDC app client in Cognito) |
| Token endpoint | `https://login.preview.epublication.ch/oauth2/token` — **the same endpoint for every Publishing Entity**, not entity-specific |
| Role | `Data Supplier` |
| Scope | The full **restricted zone** — i.e. one Technical User can be used both for announcement submission and for the authenticated search/detail endpoints described in [Announcement Export](announcement-export.md); no separate credential is needed per capability |
| Cardinality | **One Technical User per Publishing Entity.** A third-party application that submits on behalf of multiple Publishing Entities (e.g. multiple cantons) needs a separate Technical User — and separate `clientId`/`clientSecret` — per entity |
| Visibility of secret | Shown only once, at creation time; cannot be retrieved afterwards. If it's lost, a new Technical User must be created |
| Limits | up to 100 Technical Users per Publishing Entity; 10,000 system-wide |

```http
POST /interface/v1/announcements/submission
Authorization: Bearer <jwt-from-technical-user-client-credentials>
Content-Type: application/json
```

> **Note:** Provider-Admin/Provider-Supporter roles will only be able to
> view and delete Technical Users, not create them — creation is
> Publisher-only, so that only the Publisher ever sees the client secret.

> **Before this ships — demo credentials on request:** A shared, static
> `clientId`/`clientSecret` pair for the preview environment is available
> on request via this [form](https://helpcenter-epublication.zendesk.com/hc/de/requests/new?ticket_form_id=25547817106076&tf_subject=F%C3%BCr%20MVP%20registrieren).
> This is a shared demo credential, not a personal one — treat it
> accordingly (don't commit it to version control, and expect it to be
> rotated periodically).

## Public zone: personal API key (announcement export)

For the public zone, a **per-user personal API key** is planned for
announcement export as well, so that individual registered users (not just
anonymous public access) can authenticate for export use cases. The
detailed specification for this is not yet available.

| Attribute | Value |
|---|---|
| Header | `Authorization: Bearer <api-key>` |
| Validity | not yet confirmed |
| Server-side storage | hashed |
| Revocable | yes |
| Issuance (current) | by the administrator, requested via [helpcenter ticket](https://helpcenter-epublication.zendesk.com/hc/de/requests/new?ticket_form_id=25547817106076&tf_subject=F%C3%BCr%20MVP%20registrieren) |
| Issuance (planned) | self-service, via a dedicated portal — spec not yet available |

```http
POST /public/interface/v1/announcements
Authorization: Bearer <your-personal-api-key>
Content-Type: application/json
```

## Search and reference-data endpoints: no auth required

All search, detail, and reference-data endpoints under
`/public/interface/v1/**` are unauthenticated by design (see the
Announcement Export documentation) — this is separate from the open item
above, which concerns only the submission endpoint's actual credential
requirement.
