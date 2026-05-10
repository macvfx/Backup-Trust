# BackupTrust

BackupTrust is a macOS menu bar app for scheduled, incremental folder backup.

It copies new or changed files from a source folder to one or more destinations on an hourly, daily, or weekly schedule, then stays out of the way in the menu bar.

## Highlights

- Incremental backup for new and changed files only
- Multiple destinations per plan
- Optional post-copy verification
- Mirror mode to remove destination-only files
- Version-and-keep conflict handling with retention cleanup
- File filters, hidden-file support, and excluded-directory presets
- Busy windows to defer runs during working hours
- Preflight space warnings, notifications, and logs
- Optional overflow destination for oversized or long-filename files

## Requirements

- macOS 14 or later
- Apple Silicon or Intel Mac

## Build and Run

1. Open `BackupTrust.xcodeproj` in Xcode 16 or later
2. Set your development team in Signing & Capabilities
3. Build and run the `BackupTrust` target

BackupTrust launches as a menu bar app with no Dock icon.

## How It Works

Each backup plan contains:

- One source folder
- One or more destination folders
- A schedule
- Optional filters, exclusions, conflict rules, sync mode, and verification

BackupTrust stores sandboxed folder access using security-scoped bookmarks. If macOS invalidates saved access after a rebuild, system change, or path update, the affected plan shows a `Re-select…` prompt so you can refresh access to that folder.

## Common Uses

- Back up a project folder to a NAS and an external SSD
- Protect a LucidLink-mounted folder with local and network copies
- Back up a code archive while excluding `DerivedData`, `.build`, and `node_modules`

## More Docs

- User guide: [BackupTrust-UserGuide.md](BackupTrust-UserGuide.md)
- Workflows: [docs/BackupTrust-Workflows.md](docs/BackupTrust-Workflows.md)
- Full reference: [README.md](README.md), [USERGUIDE.md](USERGUIDE.md), [docs/WORKFLOWS.md](docs/WORKFLOWS.md)
