---
description: Start a new feature or user story safely
---

1. Ask which user story (US-xxx in `docs/product-spec.md`) this task covers, if not given.
2. Read that story, its section in the spec, and `docs/course-requirements.md`.
3. Check `git status`; if there are uncommitted changes, stop and ask.
4. Create a branch `feature/<short-name>` from an up-to-date `main`.
5. Write a short plan: screens, classes to add/change, shared files touched, edge cases
   (permission denied, empty list, invalid input). Wait for the student to approve the plan.
6. Implement in small steps; build after each step.
