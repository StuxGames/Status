# Changelog

All notable changes to Stux.Games' status page (status.stux.games) are documented here.

Since v26.10.23 this project uses [Date Versioning](https://datevers.ing) (`YY.MM.DD`, the UTC release date, with `-1`, `-2`… for later releases the same day); earlier releases used Semantic Versioning.

## v26.11.15-1

### Changed

- **Branches: `test` → `staging` → `main`.** Work and releases happen on `test`. The new `staging` branch is
  pre-production and changes only through a pull request from `test`. `main` is live and changes only through a
  pull request from `staging`. `commit.sh`/`.bat` refuse to run on `staging` as well as `main`, and print the push
  command plus both `gh pr create` commands after tagging. CONTRIBUTING's "Branches and going live" section and the
  README's Versioning section describe the flow
- The `*/5` schedule's comment in `.github/workflows/status.yml` says it asks GitHub for a check every 5 minutes,
  best-effort, since GitHub often runs it less often. The schedule itself is unchanged

## v26.11.15

### Added

- `dev-server.sh`/`.bat` take `--lan`: it listens on all interfaces (`0.0.0.0`) instead of `127.0.0.1`, so phones and
  other devices on the local network can open the dev server, and prints one URL per IPv4 address (usually the
  `192.168.x.x` one) with a firewall hint. Without it the server stays on `127.0.0.1`. README and CONTRIBUTING
  describe it

## v26.11.13

### Changed

- The imprint GitHup generates (`legal.company` in `.githup.yml`) gives Stux Group Ltd's new registered office, 124 City Road, London, EC1V 2NX, England, United Kingdom. The company
  number (13160574) and "registered in England and Wales" are unchanged

## v26.11.08

### Changed

- **Status checks are described as "checked regularly", not "every 5 minutes".** GitHub runs the `*/5` schedule
  best-effort, often much less often. The site description in `.githup.yml` says "checked regularly" and its comment
  says the 5-minute request is best-effort. The README says the page shows the real check rhythm over the last
  24 hours, and CONTRIBUTING no longer says data lands every 5 minutes. The cron itself is unchanged

## v26.11.06-2

### Added

- A `test` branch: work happens on `test` (or a branch off it), and reaches `main` only through a pull request from
  `test` that Leo reviews and merges. Release commits and tags are made on `test`. CONTRIBUTING has a Branches section
  and the README's Versioning section says so

### Changed

- `commit.sh` and `commit.bat` suggest `git push origin test --tags`

## v26.11.06-1

### Added

- **Stux.Games Games** (games.stux.games) is now monitored, in the Stux.Games group, and a new **Templates** group
  monitors Stux.Games Gamepage, Soonpage and Maintenancepage. All four sites are live, so they move out of the
  "Coming online" links (which are removed)

### Changed

- The README's "What's monitored" list matches, and CONTRIBUTING is titled Stux.Games Status

### Fixed

- The CHANGELOG intro no longer says the project follows Semantic Versioning; it has used Date Versioning since v26.10.23

## v26.11.06

### Changed

- The page's logo and favicon are now its own badge icon (the Stux.Games mark with a heartbeat badge, built by
  StuxGames/Games' `scripts/badge-icons.py`) rather than the plain Stux.Games logo. The README's header too, now titled
  Stux.Games Status
- The "Coming online" links use their full names: Stux.Games Gamepage, Stux.Games Soonpage and Stux.Games
  Maintenancepage, not bare "Gamepage", "Soonpage" and "Maintenancepage"

## v26.10.23

### Added

- `tests/version.sh`, which checks that `VERSION.md` is a valid Date Version, a real calendar date not in the future, and the same as the newest entry in this changelog

### Changed

- Switched from Semantic Versioning to [Date Versioning](https://datevers.ing): releases are numbered by their UTC release date as `YY.MM.DD`, with `-1`, `-2`… for later releases the same day. This release follows v1.0.2
- `commit.sh` and `commit.bat` refuse a `VERSION.md` that isn't a valid Date Version or is dated in the future (UTC), and warn when it's dated before today
- `README.md` and `CONTRIBUTING.md` describe Date Versioning and the release steps

## v1.0.2

### Changed

- The logos and icons in the Markdown docs (README and the like) follow GitHub's light or dark theme, using each brand's `logo-light`/`logo-dark` and `icon-light`/`icon-dark` files

## v1.0.1

### Changed

- The logos and icons in the Markdown docs (README and the like) follow GitHub's light or dark theme, using each brand's `logo-light`/`logo-dark` and `icon-light`/`icon-dark` files

## v1.0.0

### Added

- The Stux.Games status page, built with GitHup and deployed to GitHub Pages at status.stux.games, in Stux.Games gold (`#FFBA1A`)
- Monitors for the stux.games homepage and the Stux.Games media CDN, plus a "Coming online" group linking games.stux.games, gamepage.stux.games, soonpage.stux.games and maintenancepage.stux.games until they go live
- Boring Legal Stuff hub with its six sub-pages, a 404 page, a sitemap and `robots.txt`, generated by GitHup
- A 5-minute check with `fill-gaps` (up to 4 checks, 5 minutes apart, when GitHub runs the schedule late), incident Issues, and an hourly rebuild
- `dev-server` (with `DEV_MODE` on by default and `--no-dev-mode`) and `commit` scripts
