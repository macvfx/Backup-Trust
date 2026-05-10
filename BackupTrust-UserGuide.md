# BackupTrust — User Guide

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

## Useful Behaviors

- BackupTrust copies only files that are new or changed
- Destination files missing from the manifest check are re-copied automatically
- Duplicate destination paths are blocked
- Offline destinations are handled gracefully
- Large files can show byte-level progress during copy

## Overflow Destination

An overflow destination is optional. When configured, files that exceed the size limit or exceed filename limits on a destination can be routed to a separate folder instead of being skipped.

BackupTrust writes overflow manifests to `_OverflowManifests/` so you can see what was diverted and why.

## Good Defaults

- Use `Overwrite if newer` for most plans
- Use `Copy if newer` unless you truly want destination deletions
- Turn on verification for critical backups or new storage
- Start with narrow exclusions and add more only when you are sure the folders are disposable

## More Docs

- Overview: [BackupTrust-README.md](BackupTrust-README.md)
- Workflows: [BackupTrust-Workflows.md](BackupTrust-Workflows.md)
- Full guide: [USERGUIDE.md](USERGUIDE.md)
