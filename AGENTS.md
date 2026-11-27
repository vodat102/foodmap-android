# FoodMap — Agent Instructions

Shared instructions for every coding agent on this repo (Claude Code, Antigravity, ...).
Claude Code reads this through `CLAUDE.md`; Antigravity reads it directly.

## Project
- Android **native** app, final project for course SE114 (UIT). Team of 2.
- Helps users decide "what to eat and where": search dish → filter → compare → decide.
- Signature feature: **Food Check-in** (Locket-style) — photo taken in-app at the restaurant, GPS + time recorded automatically.
- Full spec: `docs/product-spec.md`. Course requirements: `docs/course-requirements.md`. Decisions: `docs/adr/`.

## Hard constraints (do not change without an ADR)
- Language: **Java** only. No Kotlin files.
- UI: **XML layouts** (View system). No Jetpack Compose.
- No cross-platform frameworks (React Native, Flutter, ...) — forbidden by the course.
- Data: JSON seed (`app/src/main/assets/foodmap_seed.json`) → Repository → **Room**.
- MVP is **offline**: no login, no REST API, no Firebase. Firebase is Phase 2 only.
- MVP scope v0.3 (ADR-002): no Google Maps SDK (the "Chỉ đường" button opens the Maps app via Intent);
  filters are distance, price and rating only; no Review entity; restaurant detail does not show check-ins.
- Check-in photo comes **only** from the in-app camera (CameraX), never from the gallery.
  `latitude`, `longitude`, `capturedAt` are set at capture time and are never user-editable.

## Architecture
```
UI (Activity/Fragment + XML)
  → ViewModel (one package per feature)
    → Repository
        → DAO (Room)
        → util/LocationHelper → util/DistanceCalculator
```
- No business logic or DB access in Activity/Fragment.
- Repositories return `Resource<T>` (LOADING / SUCCESS / ERROR) wrapped in LiveData.
- Room work runs off the main thread.
- Food ↔ Restaurant is many-to-many through `RestaurantFood` (restaurantId, foodId, price, isAvailable).

## Package layout
```
app/src/main/java/com/example/foodmap/  (package com.example.foodmap)
  data/local/entity/     Restaurant, Food, RestaurantFood, Favorite, CheckIn
  data/local/dao/        one DAO per entity
  data/local/            AppDatabase, SeedLoader
  data/repository/       RestaurantRepository, FoodRepository, CheckInRepository, ...
  ui/<feature>/          Activity/Fragment + its ViewModel + adapters
                         features: home, search, restaurant, favorite, checkin
  util/                  Resource, LocationHelper, DistanceCalculator
```

## Feature ownership
- Member A: `ui/checkin`, `CheckInRepository`, CameraX, location for check-in.
- Member B: `ui/home`, `ui/search`, `ui/restaurant`, `ui/favorite`, filtering.
- Shared foundation (entities, DAOs, AppDatabase, Resource, util/): change only when the task says so,
  and say clearly in the summary that a shared file was touched.

## Commands
- Build: `./gradlew assembleDebug` (Windows: `gradlew.bat assembleDebug`)
- Unit tests: `./gradlew testDebugUnitTest`
- Lint: `./gradlew lint`
Run build + unit tests before saying a task is done.

## Must-handle cases (graded by the course)
- Location or camera permission denied → app still works (manual restaurant pick / message + open Settings).
- Empty lists show an empty state, never a blank screen.
- Validate every user input (caption length, rating 1–5).
- Destructive actions (delete check-in, remove favorite) ask for confirmation.

## Working rules
- Small, focused changes. One feature per branch: `feature/<short-name>`.
- Never commit secrets: `local.properties`, API keys, `google-services.json`.
- The course requires each student to explain their own code. After every change, end with a short
  summary in Vietnamese: files changed, the flow, and anything the student should read to understand it.
- When a decision changes the constraints above, propose an ADR in `docs/adr/` instead of silently diverging.
