# trust-index-data

Public repo: open-core dataset (`data/open/`, CC BY 4.0), community corrections (`overrides/`), and the canonical spec (`docs/trust-index.spec.md`). Read the spec's decision log (DEC-xx) before changing scope or wording.

## Rules

- **Public repo.** No secrets, no self-hosted runner, nothing proprietary. Enriched layers (timelines, hiring, subprocessor graph, diffs) stay out.
- **Overrides are data, never code.** The pipeline reads `overrides/*.yml` as files only.
- **Wording is a legal shield.** Say a company "publicly advertises" a framework. HIPAA is a claim, never a certification. Corrections need public evidence; unverifiable claims are refused.
- **`data/open/` arrives by PR from the pipeline** (refresh workflow, one PR per release with `changes.md` as the body). Do not hand-edit it. The same PR adds the release's entry to `docs/RELEASES.md`; hand-edit that file only for correction entries. A newer release PR supersedes older open ones; close the stale ones.
- Correction flow: issue form `correction.yml` → `verify-correction.yml` checks the evidence and opens an overrides PR → a human merges.

## Commands

```bash
gh pr list                 # pending open-core release PRs
gh issue list              # incoming corrections
```
