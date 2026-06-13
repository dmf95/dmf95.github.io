# Changelog

All notable changes to this site are documented here. The format is based on
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/); dates are `YYYY-MM-DD`.

## [Unreleased]
### Added
- Blog post announcing the **Data + AI Summit 2026** talk.

### Changed
- Updated the **datarena flagship** for datarena-app **v3.0.0**: the app is now a typed
  **FastAPI** API + mobile-first **Next.js** web (two Cloud Run services) instead of a single
  Dash app; shot-plot assets moved to private object storage; per-service CI/CD; cost ~$2–5/mo;
  added a public API (`api.datarena.app/docs`) reference and a "typed all the way to the browser"
  note. Project tags swapped `dash` → `fastapi`, `nextjs`.

## [2026-06-12]
### Added
- `.gitignore` covering Jekyll build output, Ruby/Bundler artifacts, and OS cruft.
- This `CHANGELOG.md` and an expanded `README.md` (local-dev setup, structure, authoring guide).

### Changed
- Untracked the generated `_site/` directory - GitHub Pages rebuilds from source, so it never
  belonged in version control.

### Removed
- Committed `.DS_Store` files.

## [2026-06-11]
### Added
- **datarena.app** flagship case study (`/work/datarena`) - an end-to-end NHL analytics platform:
  the four-repo data stack (dlt → dbt → ml → app), the dev/PR/deploy workflow, and honest caveats.
- **Calibrated NHL xG model** deep-dive (`/work/nhl-xg-model`) - temporal validation, isotonic
  calibration, the unified-vs-split A/B, and walk-forward scoring.
- Cover image and shot-plot assets under `images/datarena/`.

### Changed
- Recast the 2022 *Public NHL data modeling* post as the v1 origin story, replacing dead
  Meltano/BigQuery/`bicks-bapa-roob` references with pointers to the rebuilt stack.
- Refreshed the **About** page - decision-intelligence framing, Georgia Tech OMSA, and the
  Data + AI Summit 2026 talk; tightened the tone toward curiosity and growth.
- Bumped Jekyll `4.3.2 → 4.4.1` for Ruby 3.3 compatibility.

### Removed
- The outdated 2023 `datarena.io` marketing post (superseded by the flagship case study).

---

Changes prior to this changelog are recorded in the
[git history](https://github.com/dmf95/dmf95.github.io/commits/main).
