# Open-core releases

One entry per release of `data/open/trust-index-open.json`, newest first. The refresh workflow adds an entry to every release PR; correction entries are written by hand. Commit hashes are the merge commits on `main`.

<!-- releases:start -->

## Correction 2026-10-06: release 2026-10-06 reverted

The 2026-10-06 release ([PR #17](https://github.com/synergetic-solutions/trust-index-data/pull/17), merged 6f772c2) was reverted the same day. About 99 of its evidence tier B records were Comp AI trust centers read by the generic HTML reader, which took the boilerplate on every Comp AI page ("frameworks like SOC 2, ISO 27001, ISO 9001, and more") as each company's claims, so those records listed frameworks the companies do not publicly advertise. The pipeline's Comp AI client, which reads only frameworks marked Compliant, merged after that run started. The open file is back to the 2026-10-05 release until a release built with the client replaces it; that release's entry appears above this one.

## 2026-10-05

- Release branch `release/2026-10-05`.
- 3,953 records; organizations with a trust center: 3,953; publicly advertising ≥1 framework: 3,111.
- Domains discovered: 9,813; 5,860 discovery candidates kept private (DEC-21).
- Added 0, dropped 7.

## Correction 2026-10-05: DNS-only candidates in the 2026-09-08 to 2026-10-03 releases

Every release up to and including 2026-10-03 published every domain discovery found, not only the organizations with a trust center. The extra records are discovery candidates: a `trust.`, `security.` or `compliance.` hostname that resolved in DNS, with no trust-center platform behind it and nothing read from it. A sample of them found about 19% are real trust or security pages and about 45% exist only because the domain has a wildcard DNS record ([pipeline#16](https://github.com/synergetic-solutions/trust-index-pipeline/issues/16)).

The release summaries (the "Organizations with a trust center" metric in each release PR) already counted only organizations with a trust center; the file did not match them.

| Release | Records in the file | Organizations with a trust center | Candidates in the file |
|---|---:|---:|---:|
| 2026-09-08 | 8,496 | 3,548 | 4,948 |
| 2026-09-15 | 9,137 | 3,629 | 5,508 |
| 2026-09-25 | 9,802 | 3,952 | 5,850 |
| 2026-10-03 | 9,823 | 3,958 | 5,865 |

The 2026-09-08 organization count comes from the comparison in the 2026-09-15 release PR; candidates are records minus organizations.

**Effect.** Candidate records carry a `profileUrl` for a profile page that was never built, so those links return 404. Counts taken from the file overstate the directory by about 2.5×.

**Fix.** From the next release on, the file holds only organizations with a trust center on a recognized platform, the same set that has profile pages ([DEC-21](trust-index.spec.md#2-decision-record)). Candidates stay in the private snapshot until an evidence check admits them. The first corrected release's entry sits above this one.

**If you used an earlier file**, switch to the corrected release, or keep only records whose `profileUrl` resolves.

## 2026-10-03

- Release PR [#13](https://github.com/synergetic-solutions/trust-index-data/pull/13), merged 2026-10-05 (0b0cbbf).
- 9,823 records; organizations with a trust center: 3,958; publicly advertising ≥1 framework: 3,116.
- Includes discovery candidates; see the 2026-10-05 correction.

## 2026-09-25

- Release PR [#9](https://github.com/synergetic-solutions/trust-index-data/pull/9), merged 2026-10-01 (fa06a69).
- 9,802 records; organizations with a trust center: 3,952; publicly advertising ≥1 framework: 3,107.
- Includes discovery candidates; see the 2026-10-05 correction.

## 2026-09-22 (not released)

- Release PR [#8](https://github.com/synergetic-solutions/trust-index-data/pull/8), closed unmerged. Every Vanta host (3,183) came back as "missing", so frameworks fell from 2,882 to 601; the quality gate did not catch a vendor-wide collapse.

## 2026-09-19 (not released)

- Release PR [#7](https://github.com/synergetic-solutions/trust-index-data/pull/7), closed unmerged and superseded by the 2026-09-25 release.

## 2026-09-15

- Release PR [#3](https://github.com/synergetic-solutions/trust-index-data/pull/3), merged 2026-09-15 (0cee5ab).
- 9,137 records; organizations with a trust center: 3,629; publicly advertising ≥1 framework: 2,882.
- Includes discovery candidates; see the 2026-10-05 correction.

## 2026-09-08

- Release PR [#1](https://github.com/synergetic-solutions/trust-index-data/pull/1), merged 2026-09-08 (51e983a). Inaugural release.
- 8,496 records; organizations with a trust center: 3,548.
- Includes discovery candidates; see the 2026-10-05 correction.
