# Trust Index Data

Open-core dataset and community corrections for [Trust Index](https://synergetic.solutions/trust-index), a directory of companies with a public compliance footprint: organizations that publicly advertise security and compliance posture through trust centers, security.txt files, and public registries.

**Methodology:** [docs/methodology.md](docs/methodology.md), the public methodology the directory renders.

## What this repo holds

- `data/open/` — the **open-core dataset** (org identity, market segment, publicly advertised frameworks, as-of date, profile URL), released under **CC BY 4.0** (see `LICENSE-DATA`). Each record carries an `evidence` tier: `A` read through the platform's API, `B` trust-center content on the page backed by a second signal, `C` page content alone; filter to `A` and `B` for the headline organization count. Domains that only resolved in discovery (tier `D`) are not published. Records with a profile page carry `profileUrl`. Every record carries `lastChanged` (`YYYY-MM-DD`), the as-of date of the release in which its published content last changed; scan timestamps, a carried-forward read and the order of a list do not count as changes, so a record that stays the same keeps its date from release to release. Every record carries identity, trust-center URL, and as-of date; `segment` (parent level only), `frameworks`, and `access` are omitted when the pipeline found no value.
- `overrides/` — validated community corrections and profile claims, one YAML file per organization, each carrying the evidence URL, verification method, date, and originating issue.
- `docs/methodology.md`: the canonical methodology.
- `docs/RELEASES.md` — one entry per open-core release, including the 2026-10-05 correction to the releases from 2026-09-08 to 2026-10-03.
- The issue form for **requesting a correction** (`.github/ISSUE_TEMPLATE/correction.yml`).

## How data gets here

Everything published is **publicly observable**: what companies themselves advertise. Corrections must cite public evidence; an automated check verifies the evidence before a change is proposed, and a human merges it. Unverifiable posture claims are never accepted; the answer to "we hold X but don't publish it" is "publish it and the next refresh will pick it up."

Compliance timelines, DNS posture scores, the chain-trust ratio and an organization's own subprocessor, AI-provider and open-role counts are shown free on every profile page but are not part of this CC BY dataset. The proprietary layers (subprocessor names and detail, the organizations naming one as a subprocessor and their count, hiring roles and frameworks, historical diffs) are **not** in this repo; they are available through [synergetic.solutions/trust-index](https://synergetic.solutions/trust-index).

## Licensing

- Files under `data/open/`: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) — free to use commercially with attribution to Synergetic Solutions and a link to the Trust Index.
- Everything else in this repo (docs, schemas, workflow code): all rights reserved unless marked otherwise.
