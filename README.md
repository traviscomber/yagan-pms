# Yagán PMS

> **Hospitality Operating System Foundation**

Yagán is an original N3uralia hospitality-platform foundation for short-term rentals. It evolved from a front-end PMS experiment into a multi-tenant application architecture with reservations, units, guests, roles, protected workspaces and persistent data flows.

The repository is still a **product foundation**, not a finished production hospitality suite.

`Property → Unit → Guest → Reservation → Task → Operational History`

---

## What exists today

- Yagán-branded product shell;
- dashboard and calendar surfaces;
- reservation create/delete workflows;
- units, guests and reservation domain objects;
- validation for dates, capacity and overlapping stays;
- API-backed PMS operations;
- PostgreSQL repository adapter with local fallback;
- optional Supabase authentication;
- organization/property-scoped workspaces;
- multi-tenant roles and onboarding foundation;
- RLS-oriented schema and audit-log foundation;
- responsive navigation and operational views.

---

## Canonical model

```text
Organization
    ↓
Property
    ↓
Unit ───────────────┐
    ↓               │
Reservation ← Guest │
    ↓               │
Operational task    │
    ↓               │
History / reporting ┘
```

The architecture is designed so reservations are not isolated calendar blocks: they belong to a property, unit, guest and tenant context that can later support housekeeping, finance, messaging and other hospitality workflows.

---

## Architecture

- Next.js / React / TypeScript application;
- App Router UI under `app/pms/*`;
- server API routes under `app/api/pms/*`;
- PMS domain logic in `lib/pms/*`;
- authentication/session boundaries in `lib/auth/*` and `lib/supabase/*`;
- PostgreSQL persistence adapter;
- Supabase migration for organization, property, unit, guest, reservation, task and audit structures;
- local file-backed fallback retained for development/demo use.

### Protected mode

When authentication is configured:

- application routes require login;
- users enter an organization/property workspace;
- API operations are scoped to the active workspace;
- tenant-aware reservation data maps to canonical organization/property structures.

### Development / demo mode

A local fallback remains available for UI and engineering work when cloud authentication or database infrastructure is not configured.

Demo state must not be confused with production customer state.

---

## Current boundary

Implemented foundation:

- reservations;
- units;
- guests;
- calendar;
- dashboard/report surfaces;
- tenant-aware persistence;
- workspace onboarding;
- authentication shell;
- overlap/capacity validation.

Not yet a complete hospitality OS:

- payments, folios and invoices;
- accounting workflows;
- advanced staff/owner permissions;
- OTA/channel synchronization;
- housekeeping automation;
- guest messaging;
- richer operational audit tooling.

---

## Portfolio position

Yagán is retained publicly as an original hospitality-system line showing the move from a UI prototype toward a real multi-tenant domain architecture.

It is distinct from **Black Swan Facility Core**, which models a much broader facility and hospitality operation.

---

## Development

```bash
pnpm dev
pnpm lint
pnpm typecheck
pnpm build
```

Environment values belong in local/deployment configuration and must never be committed as real credentials.
