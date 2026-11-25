---
description: Verify and wrap up a feature before opening a PR
---

1. Run `./gradlew assembleDebug testDebugUnitTest lint` and fix failures.
2. Check the must-handle cases in `AGENTS.md` for this feature.
3. Update `docs/product-spec.md` or add an ADR in `docs/adr/` if scope or a decision changed.
4. Commit with a conventional message.
5. Write the PR description in Vietnamese: what changed, how to test it on the emulator,
   which shared files were touched, and the main flow the student must be able to explain.
