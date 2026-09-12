# Technical Design: Note trash and 30-day restoration

Product Requirements: [Note trash and 30-day restoration](2026-09-12-note-trash.requirements.md)

English | [한국어](2026-09-12-note-trash.design.ko.md)

> Worked example — The structure and behavior below are design assumptions for a fictional app. They do not imply that this repository contains a notes app or that tests have passed. Product scope and completion criteria are defined only in the linked Product Requirements. [Reading guide](README.md)

## Summary

Record a deletion time on the existing note instead of removing it immediately. Ordinary queries return only active notes; trash returns only entries still eligible for restoration. Restoration and expired-data cleanup check the same note's state under a lock to handle races. Restoration eligibility is determined independently of whether cleanup has run.

## Non-Goals

- Do not introduce a separate trash store, search engine, or message queue. This example assumes queries against one database and an existing scheduled-job runner.
- Do not change note body structure, authentication, or backup retention policy.
- Do not create a complete operation history or permanent deduplication records for every request. R6 covers repeated requests against the current state, not collapsing distinct deletion and restoration operations.
- Do not guarantee immediate removal of all physical copies at expiry. Follow the product boundaries in [Non-Goals](2026-09-12-note-trash.requirements.md#non-goals) and [R4](2026-09-12-note-trash.requirements.md#requirements).

## Context

The document format was checked against this repository's [Split guide](../docs/split-proposals.md) and [product](../templates/product-requirements.md) and [technical](../templates/technical-design.md) templates at documentation revision `c02b5fa0ed03dea431862bec690abb091ed5898f`. This is a documentation-repository baseline, not a verified code revision of the fictional app.

The current-system assumptions for the example follow. A real adoption must replace them with the app's code paths, symbols, tests, and inspected commit.

- The server checks the signed-in user and note owner. Notes have a stable ID, owner, title, body, and creation and modification times. There is no sharing, attachment, folder, or offline-write functionality.
- The web UI and API can be deployed together, with new requests blocked during maintenance. Lists, search, and detail requests read the same relational database, without a separate search index or server cache.
- The database supports transactions and row locks. Current deletion physically removes the note row. An existing scheduled-job runner can clean up expired entries.

No product or technical choice beyond these assumptions is left unresolved in the example. The empty Open Questions section is therefore omitted.

## Design

### State and storage — R2, R3, R4, R6

Add nullable `deleted_at` to the existing note. A missing value means active. A deletion time means trashed, with `restore_until = deleted_at + 30×24 hours`. Do not store a separate state or deadline column that could disagree with those values. Deletion and restoration do not change the ID, owner, title, body, or creation time. They also leave the body's modification time unchanged because they are not content edits.

```text
Active ── delete ──> Trash ── restore before deadline ──> Active
                      │
                      └── deadline reached ──> Access/restore denied ── cleanup ──> Row removed
```

Reaching the deadline changes read and restoration eligibility; cleanup does not record a separate expired state. Compare times using the server-side database's UTC clock, converting to local time only for display. List deadline calculations and restoration checks use the same 30×24-hour rule.

### Read and edit boundaries — R1, R2, R4, R5

Apply owner matching and `deleted_at IS NULL` consistently to ordinary lists, search, detail reads, and saves. Trash lists only notes belonging to the user that have a deletion time and whose deadline is later than the query time, newest deletion first. Return the title, deletion time, restoration deadline, and target ID, but not the body.

Treat a trashed note as not found at its original detail address and on save requests. Missing notes and notes owned by someone else receive the same generic error. Error content must not expose the title, body, or deletion status to unauthorized users. Content already delivered to another tab before deletion cannot be retroactively erased from that screen, but subsequent saves and reads must enforce these conditions.

### State transitions and request results — R1, R3, R4, R5, R6

Deletion, restoration, and editing acquire the note's row lock and then reread its current state. User operations also verify ownership after acquiring the lock. The time used to check expiry is the **database time read after acquiring the lock**, not the request-arrival or transaction-start time.

| Request | Processing | Result presented to the user |
|---|---|---|
| Delete an active note | Set `deleted_at` to the current time under the lock and commit | Refresh the list, search, and editor after success |
| Repeat deletion of a restorable trashed note | Preserve the existing deletion time | Return success for the already deleted state |
| Restore before the deadline | Clear only `deleted_at` and commit | Return the existing ID and open the original note |
| Repeat restoration of an active note | Leave content and ID unchanged | Return the same note |
| Restore an expired, missing, or other user's note | Make no change | Return the same “This note cannot be restored” error and refresh guidance |
| Edit a trashed note | Make no change | Report save failure and offer a return to the list |

An expired note is also inaccessible to repeated deletion requests. If **distinct operations**, such as restoration and deletion, overlap, their lock-acquisition and processing order determines the result. A new deletion after restoration starts a new period; repeated deletion while the note remains in trash does not extend it.

Commit before sending a success response. Database errors roll back the transaction. If a response is lost, the client neither assumes success nor automatically resends deletion; it refreshes the ordinary list and trash. Users can retry after checking the state. A successful operation refreshes relevant query results in that tab; other tabs check server state on their next read or save.

### Expired-data cleanup and operations — R4, R5

Use the existing scheduled-job runner to find small batches of expired candidates each hour. After acquiring each note's lock, recheck its deletion time and deadline and remove the row only if it is still expired. Skip notes restored after candidate selection. If the job stops, the next run processes remaining candidates; no separate completion marker is needed.

Cleanup failure does not extend the restoration deadline because read and restoration paths enforce expiry independently. Record removal counts, failure counts, and the last successful run, and connect failures to existing job alerts. User-request logs record operation type and outcome or failure reason, but not note titles or bodies. Operational logs and cleanup jobs are not additional paths for granting users access.

## Technical Decisions

- **TD1: Keep the existing row and record its deletion time.** Moving rows to a separate trash table would add concerns around preserving IDs and content and transitioning between two storage locations. Retaining one row directly serves [PD3](2026-09-12-note-trash.requirements.md#product-decisions) and R3. Accept the risk that every ordinary read and edit path needs the filter. Revisit when introducing a separate search store.
- **TD2: Separate expiry checks from physical cleanup.** If restoration eligibility depended on whether cleanup had removed the row, job delays would change the policy in R4. Check the deadline on requests and perform cleanup later. Redesign together with product policy if deletion deadlines for all copies become a requirement.
- **TD3: Serialize state transitions with row locks.** Reading and then saving unconditionally could let a stale edit overwrite the trashed state, or let cleanup remove a just-restored note. Under the single-database assumption, choose locking followed by a state recheck. Distributed event processing or a separate search engine is unnecessary for this scope.

## Test Strategy

These are **planned checks and expected observations** for implementation, not executed results. Use fixtures with fixed note IDs, titles, and bodies, two different users, and a controllable server clock.

| Requirements | Method | Expected observation |
|---|---|---|
| R1 | Delete, then reread the list, search, and original address. Inject commit failure and loss of a response after commit separately | Only successfully deleted notes leave ordinary queries. Failure is not reported as success; refreshing resolves an uncertain outcome |
| R2 | Query two users' trash and inspect display in different time zones | Only the user's own titles and times appear. Different display zones identify the same deadline instant |
| R3, PD3 | Compare ID, title, body, and creation time across deletion and restoration; check the original address and search afterward | The original note returns unchanged and leaves trash |
| R4, PD1 | Restore just before, exactly at, and after expiry. Query expired entries with cleanup stopped. Start a request before expiry but acquire its lock afterward | Only processing before expiry permits restoration. Expired rows are inaccessible even while stored. A stale trash screen reports failure and refreshes |
| R5, PD2 | Attempt reads, deletion, restoration, and saves using another user's ID. Save from a pre-deletion tab. Inspect trash responses and logs | No unauthorized content or existence disclosure. Post-deletion saves are rejected. Trash responses omit bodies; logs omit titles and bodies |
| R6 | Repeat deletion and restoration, race deletion against restoration on two connections, and delete again after restoration | Repeated deletion in trash leaves the deadline unchanged. Repeated restoration returns the same ID. Distinct operations follow processing order; only a new deletion restarts the period |
| R3, R4 and TD3 | Start cleanup while restoration holds a lock acquired just before expiry and commits afterward. Also recheck a candidate list containing an already restored row. Separately race a save against deletion | An already permitted restoration completes; cleanup skips the active row. If save wins, its content enters trash; if deletion wins, saving is rejected |

Transition checks cover preserving existing notes as active, applying deletion filters to every read path in the new version, and keeping the restoration deadline unchanged when cleanup stops. Also manually inspect messages, time-zone display, and network-error behavior in a browser. Unit tests alone do not establish concurrent-request ordering or the screen experience.

## Verification

- Checked: None. The app is fictional; there is no implementation code, test command, tested revision, or passing result.
- Not checked: All of Test Strategy, data transition, concurrency, and actual browser behavior. Reviewing this example's documents does not substitute for feature verification.
- In a real change record, identify the tested commit or run, observations, and omitted checks with reasons. Do not copy the plan and present it as passing results.

## Risks & Migration

- Give existing data `deleted_at = NULL` so all existing notes remain active. There is no data to restore already physically deleted notes, matching the product Non-Goals. Add indexes needed for per-owner trash queries and expired-candidate scans at this point.
- Use a short maintenance window at launch, blocking incoming requests and draining in-flight writes. Extend the schema, then move both web UI and API to versions that understand deletion state. Check every ordinary read and edit path and the restoration flow before reopening the service and enabling cleanup. Mixed old/new-version writes during transition are outside this example's scope.
- Rolling back to a version that does not exclude deleted rows could expose notes again. Do not simply roll back the code or drop the new column. If a problem occurs, stop cleanup first and ship a fix while preserving deletion filters and retained data. Physically removed rows cannot be recovered through this feature.
- The largest implementation risk is missing the filter in a list, search, detail, or edit path. Run the R1/R5 integration checks before release. A real product with a separate search index, cache, or sharing breaks the Context assumptions and must not adopt this design unchanged.
- A cleanup outage can retain expired data longer. Detect it through existing operational alerts, without conflating the user-facing access/restoration deadline with physical retention. The accepted product consequences of retention, deadlines, and maintenance are collected in [Risks](2026-09-12-note-trash.requirements.md#risks).
