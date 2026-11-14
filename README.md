# NZRT-Activity-Dashboard

https://status.nzrtnetwork.com

Single-page activity board aggregating NZRT sources into one live timeline.

## How it works

```
aggregator.py  ──pulls feeds──►  activity.json  ──SSH push──►  status.nzrtnetwork.com  ◄──fetched every 60s──  index.html
```

- **Source:** `C:\RPO-SAI\SYS\PLA\WIN\RPO-win\NZT-dsh` (repo `000WIN`)
- **aggregator.py** runs on SYS (Task Scheduler `\NZT\NZT-activity-feed`), writes `activity.json` and pushes it to `/home/nzrtnetw/status.nzrtnetwork.com/` over SSH.
- **index.html** is self-contained; one same-origin fetch of `activity.json`, filterable timeline.

## Sources

| Source | Feed |
|--------|------|
| WOR | `/wp-json/wp/v2/posts` |
| FLA | `/public/api/discussions` |
| DOL | agenda RSS + REST ticket backfill |
| GIT | `gh` CLI — commits from the 5 most-recently-pushed `NZRTnetwork` repos, private repos included (000OBS, 000LLM) |
| OBS | `C:\VLT-SAI` `*.md` mtime scan |
| CLA | Claude Code session transcripts |
| NCL | Activity OCS API |
