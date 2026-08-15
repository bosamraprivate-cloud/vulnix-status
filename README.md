# vulnix-status

Data + static site for [status.vulnix.dev](https://status.vulnix.dev), the
public status page for the Vulnix platform.

This repo is intentionally separate from the main Vulnix codebase and hosted
on GitHub Pages (not Vulnix's own AWS infrastructure), so the status page and
its uptime history keep working - and keep telling the truth - even during a
real Vulnix outage.

## How it's updated

`history.jsonl`, `summary.json`, and `incidents.json` are written by a
scheduled GitHub Actions workflow in the main (private) Vulnix repo
(`.github/workflows/status-check.yml`), which runs
`scripts/status-check/run_checks.py` every 5 minutes against Vulnix's public
endpoints and pushes the result here.

Nothing in this repo should be hand-edited except `index.html` and this
README - the JSON/JSONL files are machine-generated and will be overwritten
on the next check.

## Files

- `history.jsonl` - append-only log, one line per (component, check run)
- `summary.json` - current state + 90-day daily uptime per component
- `incidents.json` - auto-derived outage timeline per component
- `index.html` - the static page rendering the above, fetched client-side
- `CNAME` - GitHub Pages custom domain (`status.vulnix.dev`)
