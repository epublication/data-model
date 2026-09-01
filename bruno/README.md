# ePublication API — Bruno Examples

Runnable [Bruno](https://www.usebruno.com/) requests that accompany the
written documentation in [`../docs`](../docs). These are examples to learn
from and adapt, not a production client library.

## Setup

1. Install [Bruno](https://www.usebruno.com/downloads).
2. Open this `bruno/` folder as a collection (**File → Open Collection**).
3. Select the **preview** environment (top-right environment selector).
4. Fill in your own credentials in the environment — do not commit real
   values:
   - `CLIENT_ID` / `CLIENT_SECRET`: from your Technical User, see
     [`../docs/authentication.md`](../docs/authentication.md). This
     mechanism is planned but **not yet live** (target: early October
     2026) — see that document for current status.
5. Run the requests in `announcement-import/` in order (`01`, `02`, `03`).

## What's included

| Folder | Contents |
|---|---|
| `announcement-import/` | Validating and submitting announcements — see [`../docs/announcement-import.md`](../docs/announcement-import.md) |

| Request | Purpose |
|---|---|
| `01 Validate Announcement` | Checks a payload's shape without publishing anything. Public zone, no auth. |
| `02 Submit - Work Permit (403-FEDE1000)` | A real, working submission against the `FEDE1000` test gazette (which accepts all standard announcement types — safe for repeated testing). Requires auth. |
| `03 Submit - Invalid (missing content)` | Deliberately incomplete request, to show what an error response looks like. |

## Requesting credentials

Credentials can currently be requested via this [form](https://helpcenter-epublication.zendesk.com/hc/de/requests/new?ticket_form_id=25547817106076&tf_subject=F%C3%BCr%20MVP%20registrieren).

## Known open items

These requests surface (and, in `03`'s case, deliberately test) some
points that are still unconfirmed in the written documentation — see the
`docs {}` block inside each `.bru` file.
