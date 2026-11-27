# ADR-002: Narrow MVP scope to match the approved proposal (spec v0.3)

- Status: Accepted
- Date: 2026-11-26
- Supersedes: the Maps consequence of ADR-001

## Decision
- No Google Maps SDK in the MVP. The restaurant detail "Chỉ đường" button opens the Google Maps app
  via Intent; if no map app is installed, fall back to the browser or show an error.
- Filters: distance, price range and rating only. Category and open-now filters move to extensions.
  Categories are still used to browse restaurants on the home screen.
- No Review entity and no text reviews in the MVP. Restaurants show the rating from the JSON seed;
  user ratings come from Food Check-in.
- Restaurant detail does not show check-ins (US-029 moves to Later).
- Favorite stays in the MVP.

## Why
- Keeps the MVP in line with the proposal `24520300_24520296_SE114_FoodMap` and the 5-week plan.
- Removes the API key / billing setup and the main external-service risk from the demo.
- Leaves enough room to finish the graded must-handle cases (permissions, empty states, validation).

## Consequences
- No `MAPS_API_KEY` in `local.properties`; the app builds and runs with no keys.
- Entities in the MVP: Restaurant, Food, RestaurantFood, CheckIn, Favorite.
- In-app map (US-034), category/open-now filter (US-035), check-ins on restaurant detail (US-029)
  and reviews (US-013, US-015) are extensions after the MVP.
