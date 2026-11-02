# trust-index-data

Public repo: open-core dataset (`data/open/`, CC BY 4.0), community corrections (`overrides/`), the release log (`docs/RELEASES.md`) and the canonical public methodology (`docs/methodology.md`). The internal specification is no longer kept here.

## Rules

- **Public repo.** No secrets, no self-hosted runner, nothing proprietary. Only the CC BY open-core fields go here. Free-tier fields (timelines, posture, counts) and the proprietary layers (subprocessor lists and edges, hiring roles, diffs) stay out.
- **Overrides are data, never code.** The pipeline reads `overrides/*.yml` as files only.
- **Wording is a legal shield.** Say a company "publicly advertises" a framework. HIPAA is a claim, never a certification. Corrections need public evidence; unverifiable claims are refused.
- **`data/open/` arrives by PR from the pipeline** (refresh workflow, one PR per release with `changes.md` as the body). Do not hand-edit it. The same PR adds the release's entry to `docs/RELEASES.md`; hand-edit that file only for correction entries. A newer release PR supersedes older open ones; close the stale ones.
- **`docs/methodology.md` is the canonical public methodology and the only place it is written.** The site's methodology page renders a fetched copy, so a method change goes here, never in the site repo. Keep release numbers out of it (the site adds the live counts) and keep the wording rules above.
- Correction flow: issue form `correction.yml` → `verify-correction.yml` checks the evidence and opens an overrides PR → a human merges.

## Commands

```bash
gh pr list                 # pending open-core release PRs
gh issue list              # incoming corrections
```
