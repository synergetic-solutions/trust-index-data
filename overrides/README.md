# Overrides

One file per domain: a validated correction to a Trust Index profile, applied
with highest precedence (per field) when the pipeline publishes a release.
The issue tracker is an inbox, never a store — a correction is real only once
its file is merged here.

- **Machine-created** files are `<domain>.json`, opened as PRs by the
  [verify-correction workflow](../.github/workflows/verify-correction.yml)
  after an automated evidence check. A maintainer always merges.
- **Hand-maintained** files may be `<domain>.yml`/`.yaml`; the workflow will
  not touch a domain that has one.

Fields the pipeline honors: `name, segment, frameworks, crunchbase, linkedin,
founded, industry, summary, summarySource, firstObserved, hiring`. Everything
else in the file (`evidence`, `method`, `verifiedAt`, `issue`) is provenance
and is ignored by the merge.

`acceptRedirect: <registered domain>` records a review decision. A trust
center that redirects to another registered domain is held as a tier-D
candidate until someone checks it, so an acquirer's trust center is never
credited to the company it bought. Setting `acceptRedirect` to the target
domain admits the record at the tier its read earns. If the redirect later
points at a different domain, the record is held again. The pipeline never
copies this field onto the published record.

Example:

```json
{
  "domain": "acme.io",
  "founded": 2016,
  "evidence": "https://acme.io/about",
  "method": "evidence-presence-check",
  "verifiedAt": "2026-08-31",
  "issue": 47
}
```

The automated check verifies the corrected value appears on the cited public
page — presence, not comprehension. The PR reviewer makes the judgment call.
Unverifiable claims ("we hold X but don't publish it") are declined by
policy: publish it and the next refresh picks it up.
