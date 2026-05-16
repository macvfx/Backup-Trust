# BackupTrust

BackupTrust is a macOS menu bar app for scheduled, incremental folder backup.

It copies new or changed files from a source folder to one or more destinations on an hourly, daily, or weekly schedule, then stays out of the way in the menu bar.

Current release line: `1.4 (18)`.

## Highlights

- Incremental backup for new and changed files only
- Multiple destinations per plan
- Optional post-copy verification
- Mirror mode to remove destination-only files
- Version-and-keep conflict handling with retention cleanup
- File filters, hidden-file support, and excluded-directory presets
- Full `macOS System` exclusion preset enabled by default for every plan, including Synology `@eaDir`
- `.DS_Store` excluded by default even when hidden files are included
- Busy windows to defer runs during working hours
- Preflight space warnings, notifications, and logs
- Optional overflow destination for oversized or long-filename files
- Overflow reclaim UI for verified-safe cleanup of stale overflow copies

## Requirements

- macOS 14 or later
- Apple Silicon or Intel Mac

BackupTrust launches as a menu bar app with no Dock icon.

## How It Works

Each backup plan contains:

- One source folder
- One or more destination folders
- A schedule
- Optional filters, exclusions, conflict rules, sync mode, and verification

`BackupTrust` stores folder access using security-scoped bookmarks; if macOS invalidates saved access after a rebuild, system change, or path update, the affected plan shows a `Re-select…` prompt so you can refresh access to that folder.

New plans automatically start with the full `macOS System` exclusion category enabled. You can still selectively uncheck any rule if you need to include one of those folders for a special case.

## Common Uses

- Back up a project folder to a NAS and an external SSD
- Protect a LucidLink-mounted folder with local and network copies
- Back up a code archive while excluding `DerivedData`, `.build`, and `node_modules`
