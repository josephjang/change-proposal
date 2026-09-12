# Product Requirements: Note trash and 30-day restoration

Technical Design: [Note trash and 30-day restoration](2026-09-12-note-trash.design.md)

English | [한국어](2026-09-12-note-trash.requirements.ko.md)

> Worked example — This Split Change Proposal describes a fictional personal-notes app. It is not a real product requirement, user-research result, or approved implementation plan. This document and Technical Design together are one proposal, separate from this repository's actual change records. [Reading guide](README.md)

## Summary

Add trash so users can restore notes they deleted by mistake. Deleted notes disappear from the ordinary list and search, but can be restored from trash for 30 days after deletion. Restoration preserves the content and the original note address. Restoring expired notes and editing notes inside trash are not provided.

## Problem

The example's current product is a web app where signed-in users write and search their own notes. Deleting a note removes it immediately with no way back, so one mistaken deletion can lose the user's work. A confirmation dialog may reduce mistakes but cannot reverse one that has already happened.

The users are individuals managing notes in several browser tabs under the same account. The product is assumed to have no shared documents, attachments, or offline editing. There are no real support-request counts or churn measurements, so no numerical improvement is claimed: completion is judged by the restoration scenarios below. The 30-day period is a product policy chosen for this example, not one confirmed in an existing service.

## Goals

- Users can restore recently deleted notes without someone else's help.
- Deleted notes do not clutter everyday browsing, and restoration availability is clear.
- Adding trash does not accidentally expose another user's notes or previously deleted content.

## Non-Goals

- Restoring shared notes, attachments, or folders together. This example's product has none of those features.
- Editing inside trash, deleting permanently on demand, or configuring retention per user.
- Recovering notes deleted before this feature ships or more than 30 days ago.
- Changing existing backup policies or guaranteeing immediate deletion of every backup copy. Expiry here concerns access and restoration through the app.

## Requirements

- **R1: Deletion and screen updates.** After a successful deletion, subsequent ordinary list, search, and original-address requests do not show or open the note. Do not display deletion as complete without confirmation; if a lost connection leaves the result unknown, users can refresh to establish the current state.
- **R2: Trash and deadline display.** Users can see the title, deletion time, and restoration deadline of their own restorable notes in trash. The deadline is exactly 30×24 hours after deletion is processed, displayed in the user's local time with the time zone. Expired entries disappear on the next list request.
- **R3: Restore the original note.** If the server processes restoration before the deadline, restore the title, body, original creation time, and original note address unchanged. The note reappears in the ordinary list and search and disappears from trash. Restoration does not create a copy.
- **R4: Expiry behavior.** At or after the deadline, the note cannot be opened or restored. Trying to restore an expired note from a trash screen that was already open shows that restoration is unavailable and offers a refresh. Delayed background cleanup must not extend the restoration period.
- **R5: Access and editing boundaries.** Users cannot open or restore another user's trash or notes. Saving from an editor opened before deletion must neither change the trashed content nor revive the note. The note must be restored before it can be edited again.
- **R6: Repeated requests.** Deleting a note already in trash does not change its original deletion time or deadline. Repeating restoration for an already restored note does not create a copy. If the user deletes the note anew after restoring it, that deletion starts a new retention period.

Representative flow: delete a note → confirm it is absent from search → find its title and deadline in trash → restore it → open the same content at its original address. Restoration near the deadline and a save from another tab must satisfy the same requirements.

## Product Decisions

- **PD1: Provide 30-day trash rather than only a confirmation dialog.** A dialog does not help users who discover a mistaken deletion afterward. Indefinite retention is rejected because it keeps content users believe they deleted. For a real adoption, revisit the period using recovery demand and retention costs.
- **PD2: Trash offers title and deadline inspection and restoration only.** Adding body previews, editing, and immediate permanent deletion would expand the recovery feature's scope. The first version focuses on restoring a note and returning to the existing editor. Revisit previews if usage shows that titles are insufficient to distinguish notes.
- **PD3: Restoration brings back the original note rather than copying it.** Creating a new note breaks existing addresses and makes repeated clicks more likely to produce duplicates. R3's preservation of address and content therefore constrains the technical choice. The storage mechanism belongs in [Technical Decisions](2026-09-12-note-trash.design.md#technical-decisions).

## Risks

- Deleted bodies remain stored for 30 days. This is accepted for mistake recovery, with retention explained in the deletion UI and app access denied after expiry. Keep the Non-Goals boundary clear so this is not mistaken for a change to backup policy.
- Showing only titles may make similarly named notes hard to distinguish. Displaying deletion times alongside titles is accepted for the first version.
- A click just before the deadline may be processed after expiry. Rather than promising restoration based on click time, provide the failure behavior in R4.
- A short maintenance window is allowed at launch. This example prioritizes preventing accidental exposure of deleted data over a zero-downtime transition.
