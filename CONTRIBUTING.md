<p align="center">
  <picture><source media="(prefers-color-scheme: dark)" srcset="https://global.media.stux.games/logo-light.png"><source media="(prefers-color-scheme: light)" srcset="https://global.media.stux.games/logo-dark.png"><img src="https://global.media.stux.games/logo-dark.png" height="80" alt="Stux.Games Logo"></picture>
</p>

# Contributing to Stux.Games Status

Stux.Games Status is Stux.Games' status page, [status.stux.games](https://status.stux.games), built with
[GitHup](https://githup.stux.group). To report an outage, open an Issue. Bugs or ideas for the
status page software belong in [StuxGroup/GitHup](https://github.com/StuxGroup/GitHup/issues).

## Local setup

You need Python 3.11+ and nothing else.

```bash
./dev-server.sh [--no-dev-mode] [--lan] [port]   # or dev-server.bat on Windows
```

`--lan` listens on all interfaces (`0.0.0.0`) instead of `127.0.0.1`, so a phone or another
device on your network can open it: it prints one URL per IPv4 address (usually the
`192.168.x.x` one). Allow Python through the firewall if asked.

## Project conventions

- **Monitors live in `.githup.yml`.** Its syntax is documented in the
  [GitHup docs](https://githup.stux.group/docs/). Only add sites Stux.Games runs, and only
  monitor a site once it answers; list it under `links:` until then.
- **The status page itself is GitHup's**, including the legal pages and 404. Change how it
  looks or works in GitHup, not here.
- **Brand.** The Stux.Games accent is `#FFBA1A`, set as `site.accent`; GitHup derives the
  readable light-theme shade (Stux.Games' `#855D00` family) from it.
- **Legal pages.** The `legal:` block in `.githup.yml` drives **Boring Legal Stuff** at `/legal/`.
  Keep it accurate.
- **Don't edit `data/` by hand.** It belongs to GitHup and the workflow.

## Branches and going live

- Work and releases happen on `test`, or on a feature branch merged back into it. The commit scripts refuse to run on `staging` or `main`; push a release with `git push origin test --tags`
- `staging` is pre-production. It changes only through a merged pull request from `test` (`gh pr create --base staging --head test`). There's no staging deployment: a release waits there, checked, before going live
- `main` is live. It changes only through a merged pull request from `staging` (`gh pr create --base main --head staging`). Merging into `main` rebuilds status.stux.games when `.githup.yml` or the workflow changed
- Nothing is pushed straight to `staging` or `main`. Pull requests need CI to pass, and Leo merges them
- GitHup commits monitoring data straight to `main` after each check (that's the one exception, made by the workflow, not by people), so merge `main` into `test` before starting new work

## Versioning

This project uses [Date Versioning](https://datevers.ing). To release:

1. Add a `## vYY.MM.DD` entry at the top of `CHANGELOG.md`, with its sections in this order: Added, Changed, Fixed, Removed, Security, Deprecated.
2. Set `VERSION.md` to the same bare version (no `v`): today's **UTC** date as `YY.MM.DD`, or `YY.MM.DD-1`, `-2`… for later releases the same UTC day. Never a future date. Use UTC, not local time: just after midnight in the UK it is still the previous day in UTC.
3. Run `bash tests/version.sh`.
4. Run `./commit.sh` (or `commit.bat` on Windows). It checks the version, commits and tags `vYY.MM.DD`, and never pushes.
