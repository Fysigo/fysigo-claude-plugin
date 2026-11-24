# Changelog — fysigo-mcp

## 1.10.0 — 2026-10-22

Written against tool catalog `39a4cb2c4e1f` (39 tools). `list_my_clients` (Coach package, read-only) lists the clients the coach actively coaches, with `id` (the `clientId` the other tools take), `name`, `engagement_status` and `self`. Jobs 2 and the client-supplements section now take the `clientId` from it instead of asking the coach to copy it from a Fysigo page. Paused, pending and ended engagements and archived clients are not listed; no email or health data comes back.

## 1.9.1 — 2026-10-22

Written against tool catalog `4ac57c46f8bc`. `archive_program` is now marked destructive (it can still be restored), so clients that honor the hint confirm before archiving. No tool or argument changed.

## 1.9.0 — 2026-10-21

Written against tool catalog `4fa8f2aba753`. Dose lines: a peptide schedule rule may carry its own `amount` and `unit`, so one compound (one vial) can hold several doses, e.g. 0.5 mg every evening and 2.5 mg Tue/Fri mornings. `get_my_doses_today` lists one entry per line with that line's amount. The same compound twice in one protocol is refused with `duplicate_compound` and nothing is saved (it used to save and give the second item the first item's schedule).

## 1.8.1 — 2026-10-19

Written against tool catalog `5ce684e2b954`. `save_my_peptide_protocol` takes `resume: true`, sent only when the person asked to resume a paused protocol. Without it, a snapshot that would turn a paused protocol back to active is refused with `protocol_snapshot_stale`. An ended or completed protocol never re-opens.

## 1.8.0 — 2026-10-18

Written against tool catalog `d659379d4407` (37 tools). Job 8, my activities: `get_my_activities`, `get_my_activity`, `log_my_activity`, `update_my_activity` (merges: send only what changes), `delete_my_activity`. GPS routes never come back through the MCP. Saving details keeps Watch readings (heart rate, distance, energy); a type with no detail fields only changes notes.

## 1.7.0 — 2026-10-18

Written against tool catalog `1efa5f327db4` (32 tools). Job 6 gains the training record: `get_my_workout_history` and `set_my_session_effort` (a recorded session's effort, replaces). Corrected: effort given at finish is stored with the workout and is a separate record from a session's effort.

## 1.6.0 — 2026-10-18

Written against tool catalog `fb5bf65f881c` (30 tools). Job 5 gains bedtime setup: `save_my_sleep_answers` (questionnaire + homes, replaces) and `lock_my_bedtime` (solar minutes, or null to unlock). Any unexpected server error now comes back as a plain `internal_error`; read back before retrying a write.

## 1.5.0 — 2026-10-18

Written against tool catalog `869acd2f6e7a` (28 tools). Job 7, my settings: `get_my_settings`, `set_my_time_zone` (IANA name), `update_my_settings` (display units, weight unit). A null time zone means doses and reminders follow UTC and the app falls back to New York: ask and set it.

## 1.4.0 — 2026-10-18

Written against tool catalog `52f271600247` (25 tools). Job 6, my workout today: `get_my_today_workout`, `log_my_set`, `remove_my_set`, `complete_my_workout`, `add_my_workout_note`. Every write takes the `workoutId` from today's read and is refused once that workout is no longer next. Loads are in kg. Hard rule 1 now lists every write and counts a set the person dictates as their yes.

## 1.3.0 — 2026-10-18

Written against tool catalog `7d1b24c8c36e` (20 tools). Job 5, sleep: `sync_my_oura`, `get_my_sleep`, `log_my_sleep_rating`, `tag_my_night`. Sync before reading or rating last night. Never interpret sleep medically.

## 1.2.1 — 2026-10-18

Written against tool catalog `7926c75148f6`. The tools now return only your own records and those of clients you actively coach, whatever role the account has. An admin connected through this server sees what a coach sees, not the whole tenant. `get_program` states it in its unknowns.

## 1.2.0 — 2026-10-17

Written against tool catalog `699bfa3f784d` (16 tools). Job 4: the person's own peptide protocols and supplement stack (`get_my_protocols`, `save_my_peptide_protocol`, `save_my_supplement_stack`, `get_my_doses_today`, `log_my_dose`). Read first, send the whole protocol, confirm before saving, never suggest a dose.

## 1.1.1 — 2026-10-12

Written against tool catalog `86fb279bb5d9`. The tools now carry MCP annotations (read-only, replaces existing content, safe to repeat). The skill names the two writes that replace what was there and the three that are not safe to repeat.

## 1.1.0 — 2026-10-12

Written against tool catalog `90b68c942796`. Changes after a dry run in which an agent holding only this skill did the three jobs against a real account:

- What to do when `fysigo-program-builder` is not installed (copy the shape of an existing program; let `validate_program` name the gaps), and that `validate_program` returns `warnings`.
- Read the program back after `edit_program`, and check the program's own prose after adding or removing a drill.
- Assignments carry a client id, not a name. Which assignment to pick for adherence.
- `history` percentages use a different base than `completionPct` and must not be compared with it.
- `marketplace` visibility exists and cannot be set here.

## 1.0.0 — 2026-10-12

Initial release. Written against tool catalog `f1a74bd8b103` (11 tools).

- The three jobs: build or change a program, give a program to someone and see who has what, review the week and log drills.
- How to read `evidence` and `unknowns`, and how to report them to the coach.
- What each error code means and what to do next.
- `references/tools.md` is generated from the server's code (`npm run gen:mcp-catalog` in the Fysigo repo). Do not edit it by hand.

## How this skill stays true

`metadata.catalog_version` in `SKILL.md` is set by hand. When a tool changes, the catalog version changes and CI fails until someone re-reads this skill against the new tools and updates that line.
