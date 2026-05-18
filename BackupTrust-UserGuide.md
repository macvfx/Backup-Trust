# BackupTrust — User Guide

Current release: `1.5 (4)`.

## Getting Started

BackupTrust lives in the menu bar. Click the icon to see plan status, run backups, open settings, and review recent results.

To create your first plan:

1. Open **Settings**
2. Go to **Plans**
3. Click **+**
4. Choose a source folder
5. Add one or more destination folders
6. Pick a schedule
7. Save the plan

## Folder Access

BackupTrust is sandboxed, so it stores access to your source and destination folders as security-scoped bookmarks.

If a plan later shows `Re-select…` or a saved-access warning:

1. Open **Settings**
2. Select the plan
3. Re-select the affected source or destination
4. Save and run the plan again

## Daily Use

From the menu bar you can:

- Run one plan immediately with **Back Up Now**
- Run all enabled plans at once
- Cancel an in-progress backup
- Open logs
- Check the next scheduled run

From **Settings → Schedule**, you can also:

- Review upcoming runs for every enabled plan
- Click **Run Now** beside **Edit Plan** without leaving the schedule view

Status colors:

- Blue: backup running
- Green: last run succeeded
- Orange: warning, offline source, or access needs attention
- Red: run finished with errors

## Plan Settings

Each plan can include:

- Hourly, daily, or weekly scheduling
- Busy windows to skip working hours
- Include-only and exclude file-extension filters
- Hidden-file support
- Excluded-directory presets and custom rules
- Conflict handling: overwrite if newer, overwrite always, skip, or version and keep
- Sync mode: copy if newer or mirror
- Optional post-copy verification
- Optional overflow destination
- Built-in diagnostics for source, destination, and overflow health

## Useful Behaviors

- BackupTrust copies only files that are new or changed
- Destination files missing from the manifest check are re-copied automatically
- Duplicate destination paths are blocked
- Offline destinations are handled gracefully
- LucidLink-backed plans can use client-aware diagnostics for either `lucid` or `lucid2`
- Large files can show byte-level progress during copy
- The full `macOS System` exclusion preset is enabled by default for every plan
- `.DS_Store` stays excluded even when hidden files are included, so useful hidden content like `.git` can still be backed up without Finder metadata noise

## Diagnostics And Lucid Troubleshooting

Use **Run Diagnostics** in the plan editor when a source, destination, or overflow path behaves unexpectedly.

For Lucid-backed plans, BackupTrust can:

- detect whether the machine has `lucid` or `lucid2`
- run a Lucid CLI sanity check from diagnostics
- optionally append safe Lucid CLI state to the normal session log
- open Terminal for an intentional interactive Lucid support upload when support asks for `support --all` at failure time

## Excluded Directories

BackupTrust can skip whole folder trees by name before scanning inside them.

Preset categories include:

- `Xcode & Swift`
- `Final Cut Pro`
- `Adobe Creative Suite`
- `Node / Web`
- `macOS System`

The full `macOS System` category is enabled by default for new plans, and older plans automatically pick up those rules when they load or import. That preset includes Synology `@eaDir` metadata and other macOS/system-generated directories that usually do not belong in backups.

Even if you enable hidden files, BackupTrust still excludes `.DS_Store` by default so Finder metadata does not get copied accidentally. If you need a special-case system folder, expand the preset and uncheck just that one rule.

## Overflow Destination

An overflow destination is optional. When configured, files that exceed the size filter or have filename components too long for encrypted NAS volumes (>143 bytes) are copied to the overflow folder instead of being skipped. The original folder structure is mirrored on the overflow destination.

Each run writes a pair of manifests to `_OverflowManifests/` on the overflow destination: a JSON manifest with per-file checksums and provenance, and a human-readable TXT summary.

**Space threshold** — a configurable limit (default 90%) prevents the overflow destination from filling up. When disk usage reaches the threshold, overflow copying pauses and remaining files are skipped. Adjust with the **Space threshold** stepper in the overflow settings, or set to 0% to disable.

**Staleness detection & reclaim** — after overflow copying, the engine scans for overflow files that also exist on primary destinations. These are reported in the menu bar as reclaimable space. This typically happens when you raise the size filter so files that were previously overflow-routed now go to primary destinations directly.

When reclaimable files are detected, a **Reclaim Space…** button appears in the Overflow Destination section of the plan editor. Clicking it opens a sheet listing every reclaimable file with its size and which primary destination(s) it was found on. Select files individually or all at once, then click **Verify & Delete** — the app re-confirms each file exists on both overflow and primary before deleting only the verified-safe overflow copies.

## Good Defaults

- Use `Overwrite if newer` for most plans
- Use `Copy only` unless you truly want destination deletions
- Turn on verification for critical backups or new storage
- Start with narrow exclusions and add more only when you are sure the folders are disposable
