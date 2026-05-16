# BackupTrust — Workflows

This document shows a few compact setup patterns for the sandboxed BackupTrust app.

## Workflow 1: Project Folder to NAS and External SSD

Best when you want one network backup and one fast local restore target.

- Source: active project folder
- Destinations: NAS backup folder and external SSD backup folder
- Schedule: hourly or daily
- Conflict mode: `Overwrite if newer`
- Sync mode: `Copy only`

Why it works:

- The SSD gives you fast restores
- The NAS gives you a second copy on separate storage
- One plan can write to both destinations in parallel

## Workflow 2: LucidLink Folder to NAS

Best when your live project is mounted through LucidLink and you want a traditional backup target.

- Source: LucidLink-mounted project folder
- Destination: NAS backup folder
- Schedule: hourly
- Conflict mode: `Overwrite if newer`
- Sync mode: `Copy only`

Recommended options:

- Enable only the exclusions you are sure are disposable
- Turn on verification for important runs
- Watch for `Re-select…` warnings if saved folder access expires

## Workflow 3: Code Folder to SSD and NAS

Best when you want to protect development work without copying disposable build output.

- Source: local code root
- Destinations: SSD backup folder and NAS backup folder
- Schedule: hourly
- Exclusions: `Xcode & Swift`, optionally `Node / Web`
- Conflict mode: `Overwrite if newer`
- Sync mode: `Copy only`

Why it works:

- Excluding `DerivedData`, `.build`, and `node_modules` reduces scan time and copy churn
- The SSD gives quick rollback and restore
- The NAS gives a second backup target

## Workflow 4: Large Media with Overflow Destination

Best when some files are too large for your main policy or hit destination filename limits.

- Source: media or archive folder
- Primary destination: normal backup target
- Overflow destination: separate drive or folder
- Schedule: daily or weekly

What happens:

- Normal files go to the primary destination
- Oversized or long-filename files are routed to the overflow destination
- BackupTrust writes JSON and TXT overflow manifests so nothing is lost silently

## Setup Tips

- Use one plan when the same source should go to multiple destinations on the same schedule
- Use separate plans when schedules or rules should differ
- Stagger heavy plans if they write to the same NAS at the same time
- If a source or destination shows `Re-select…`, refresh folder access before the next run

## More Docs

- Overview: [BackupTrust-README.md](BackupTrust-README.md)
- User guide: [BackupTrust-UserGuide.md](BackupTrust-UserGuide.md)
- Full workflows: [WORKFLOWS.md](WORKFLOWS.md)
