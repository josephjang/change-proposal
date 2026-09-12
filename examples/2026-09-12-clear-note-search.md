# Change Proposal: Clear note search

English | [한국어](2026-09-12-clear-note-search.ko.md)

> Worked example — This Unified Change Proposal describes a fictional personal-notes app. This document is the complete proposal; there is no separate Product Requirements or Technical Design. It is not a report of real user research, implementation, or test results. [Reading guide](README.md)

## Problem

When a search returns no notes, or users want to find something else, they must manually remove the whole query and run the search again to return to the ordinary note list. There is no action beside the search field to clear the search in one step, making a simple task unnecessarily cumbersome.

This example assumes that signed-in users search their own notes, that an empty query already returns the ordinary list, and that search errors and retries already have a UI. The query appears in both the field and the URL, and existing request handling displays only responses matching the latest search conditions when requests overlap. No usability study or timing measurements are available, so completion is judged by the behavior below rather than an invented improvement metric.

## Goals

- Users can clear a search without manually selecting the entire query.
- Both mouse and keyboard users can return to the ordinary note list.

## Non-Goals

- Changing search behavior, ranking, or sorting, or adding recent searches, autocomplete, or a new shortcut.
- Introducing a new server API, storage structure, or user preference.
- Implementing note trash or restoration at the same time. That is an independent change to the same fictional app.

## Requirements

- **R1: Clear action visibility.** Show a button named “Clear search” when the field contains input or an applied search query exists. Hide it when both are empty. The same visibility condition applies when a search has no results or fails.
- **R2: Clear the search.** Activating the button clears the query from the field and URL, then runs the existing empty-query search to request the ordinary note list. Clear both the input and the applied query even when they differ, while preserving other sort conditions.
- **R3: Loading and failure states.** Use the existing loading indicator while fetching the list. On failure, provide the existing error and retry behavior and keep the query empty. A late response from an earlier search must not return the screen to the results shown before clearing.
- **R4: Keyboard and focus.** The button can be reached by keyboard and activated with Enter or Space, and exposes the name “Clear search” to assistive technology. After activation, focus is in the empty search field so the user can immediately type another query.

## Decisions

- **D1: Put the button beside the search field instead of adding a separate return link to the results screen.** Users can clear the query where they see it and find the same action whether or not there are results. A new keyboard shortcut alone would be difficult to discover, so it is rejected. Revisit the placement if a screen is added that hides the search field.
- **D2: Reuse the existing empty-query search path.** Keeping a separate cache of the full note list could show stale notes or require two lists to be managed independently. R2/R3 use the existing search, error, and response-order handling without new server functionality or persistent state. This is why the change does not need a separate technical design document.

## Risks

- An accidental click can lose the query being typed. The notes themselves do not change and the query can be entered again, so no confirmation dialog or undo action is added.
- Clearing a search can fail over the network just like an ordinary search. The list is not promised to appear immediately; R3 handles loading and retries.
