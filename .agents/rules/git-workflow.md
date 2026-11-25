# Git workflow (2-person team)

- `main` always builds. Work on `feature/<short-name>` branches and merge through a Pull Request.
- The other member reviews every PR touching shared foundation (entity/, dao/, AppDatabase, util/).
- Commit messages: `<type>(<scope>): <summary>` — types: feat, fix, refactor, docs, test, chore.
  Example: `feat(checkin): capture GPS and time when photo is taken`.
- Commit often: the course grades the commit history, and each member must show their own commits.
- Do not rewrite shared history (no force-push to `main`).
