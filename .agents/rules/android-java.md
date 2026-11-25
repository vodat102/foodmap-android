# Android / Java conventions

- Java 17 language level; follow standard Android naming (`RestaurantDetailActivity`, `item_restaurant.xml`).
- Strings, colors and dimensions go in `res/values/` — no hard-coded user-facing text in Java or XML.
- Use ViewBinding, not `findViewById`.
- Lists use RecyclerView + ListAdapter with DiffUtil.
- Observe LiveData with `getViewLifecycleOwner()` in Fragments.
- Request runtime permissions with the Activity Result API (`registerForActivityResult`).
- Never block the main thread: Room and file I/O run on an executor.
- Log with a class-level `TAG`; no `printStackTrace()`.
