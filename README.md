# Cursor Command Files Guide

This repository contains reusable prompt files for a feature workflow in Cursor.

## Command Files

- `commands/create_brief_01.md`: Create a concise product brief in `docs/PRODUCT_BRIEF.md`.
- `commands/plan_feature_02.md`: Create a technical implementation plan in `docs/features/<number>_PLAN.md`.
- `commands/implement_feature_03.md`: Implement the feature from the plan, without creating redundant planning artifacts.
- `commands/validate_feature_04.md`: Run checks and report concise readiness/blockers.
- `commands/code_review_05.md`: Review implementation quality and plan alignment, then write `docs/features/<number>_REVIEW.md`.
- `commands/write_docs_06.md`: Update codebase docs to match the real implementation.

## Recommended Usage Order

1. Run `create_brief_01.md` with the product/problem description.
2. Run `plan_feature_02.md` with the approved feature details.
3. Run `implement_feature_03.md` for that exact plan file (one plan = one feature).
4. Run `validate_feature_04.md` to check quality gates.
5. Run `code_review_05.md` against implementation and plan.
6. If validation/review finds issues, re-run `implement_feature_03.md` for the same feature plan and repeat steps 4-5.
7. Run `write_docs_06.md` after code is stable.

## Why This Is Minimal

This six-command setup keeps each step focused on one outcome while avoiding redundant artifacts:

- `brief` defines product context once.
- `plan` defines implementation scope for one feature.
- `implement` executes that one feature scope without rewriting plan/brief.
- `validate` checks readiness without creating extra docs by default.
- `review` records quality findings.
- `docs` updates user-facing documentation based on actual code.

## Effective Prompting Tips

- Always attach or reference the relevant plan/review/doc files.
- Include exact feature scope and constraints (performance, security, compatibility).
- Ask for explicit output locations (`docs/...`) to keep artifacts organized.
- Ask for concise output unless you need deep analysis.
- For multi-step work, request checkpoints (for example: "stop after plan for approval").

## Minimal Example

Use this pattern when invoking each command:

1. "Use `commands/create_brief_01.md` for: <idea/feature description>"
2. "Use `commands/plan_feature_02.md` for: <approved brief + scope>"
3. "Use `commands/implement_feature_03.md` with plan `<file>`."
4. "Use `commands/validate_feature_04.md` with plan `<file>`."
5. "Use `commands/code_review_05.md` with plan `<file>`."
6. "Use `commands/write_docs_06.md` with plan `<file>` and review `<file>`."

## Reuse In A New Repo

If you want to start from this repo, keep the commands, and connect to a different project remote:

1. Clone this repo locally.
2. Remove the current `origin` remote.
3. Add your new project repo as `origin`.
4. Push to the new remote.

```powershell
git clone <this-commands-repo-url> my-new-project
cd my-new-project
git remote remove origin
git remote add origin <new-project-repo-url>
git push -u origin main
```

Optional (recommended): keep this commands repo as `upstream` so you can pull future command updates.

```powershell
git remote add upstream <this-commands-repo-url>
git fetch upstream
```

When you want command updates later, selectively copy or merge from `upstream`.

## Notes

- Prefer code as source of truth when plan/review/docs conflict.
- Keep plan and review files as historical artifacts; keep user-facing docs in main docs locations.
- For numbered plan/review files, keep a consistent feature ID across implementation artifacts.
