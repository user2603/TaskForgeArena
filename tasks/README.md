# TaskForgeArena Rulebook

This rulebook governs how task folders on developer branches are scored,
recorded in the Notion `Task Registry`, and promoted to the release pool.

## Registry conventions

- Each developer works on their own branch. Task folders live under
  `tasks/<dev>/` on that branch.
- A commit titled `Add N tasks: <name-1>, <name-2>, ...` introduces exactly the
  task folders named in its message. Entries under `tasks/<dev>/` that are not
  named in any `Add N tasks` commit are not registry tasks and are ignored.
- Each registry task is recorded in the Notion `Task Registry` database with
  three columns: `Task Name`, `Maturity Tier`, and `Owner` (the owning
  developer branch).

## Maturity tiers

- The maturity tier of a task is the number of files inside the task folder in
  the commit that introduced the task (all files, at any depth). Later commits
  never touch existing task folders, so this number is stable.
- The tier boundaries are defined in the authoritative table referenced below
  (R2). The boundaries are deliberately spaced by a factor of two so that each
  tier is clearly separated from its neighbours.

## Release promotion (goldpool)

- A registry task qualifies for release when it satisfies both conditions:
  1. its maturity tier is `gold`, and
  2. its `docs/task.md` satisfies the wording rule referenced below (R4).
- Qualifying tasks are copied into the `goldpool` branch under
  `tasks/goldpool/<task>/`, with at least `docs/task.md` and
  `evaluation/main.py` preserved verbatim from the owning branch.

## References

- R1: The canonical task layout used for counting, containing the full nine-file layout: `tasks/examples/example-task/`
- R2: The authoritative tier boundary table that maps file counts to tiers: `tasks/examples/tier-thresholds.md`
- R3: A worked example of a gold-tier task that demonstrates the counting rule end to end: `tasks/examples/example-task-minimal/`
- R4: The wording rule that every `docs/task.md` must satisfy before its task can be promoted: `tasks/examples/example-task/docs/agent_system_prompt.md`
