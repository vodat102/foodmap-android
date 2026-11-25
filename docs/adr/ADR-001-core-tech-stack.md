# ADR-001: Core tech stack and MVP scope

- Status: Accepted
- Date: 2026-11-25

## Decision
- Java, XML layouts (View system), MVVM: UI → ViewModel → Repository → DAO (Room).
- Data from a self-built JSON seed loaded into Room; no external restaurant API.
- Many-to-many Food ↔ Restaurant via `RestaurantFood`.
- MVP is offline with no account. Food Check-in (CameraX + location) is the main user-owned entity (CRUD).
- Phase 2 (only after MVP is stable): Firebase login, friends, feed, reactions, comments.

## Why
- Matches what the course teaches (Activity, views, events, Intent, storage) and its minimum requirements.
- Offline MVP removes dependency risk for the demo; the course advises against relying on external services
  without a fallback.
- Check-in gives a real CRUD entity plus two Android-specific features (camera, location).

## Consequences
- No login screens in MVP; Epic 1 (Account) moves to Phase 2.
- Maps: Google Maps SDK if an API key is configured, otherwise open the Maps app via Intent.
