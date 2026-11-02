# Trust Center Directory methodology

How the Trust Center Directory collects, verifies, and corrects its data.

This file is the canonical methodology. It is written and edited only here. The directory's [methodology page](https://synergetic.solutions/resources/trust-center-directory/methodology/) renders it from the second-level heading below onward and adds the latest release's counts.

## What the Trust Center Directory measures

The Trust Center Directory catalogs the **publicly advertised** security and compliance posture of companies that maintain a public compliance footprint. It reports what organizations say about themselves in public: trust center pages and security.txt files. It does not audit companies, review private reports, or assess whether controls actually operate.

## What our language means

- **"Publicly advertises"** means the claim appeared on the organization's public trust center on the observation date shown.
- **A missing framework** means no public claim was observed. It never means an organization is non-compliant. Many compliant companies simply do not publish their posture.
- **"Advertises alignment with"** is used for frameworks that cannot be certified. The organization says it follows the framework; no third party certifies that.
- **HIPAA** entries reflect a public claim of compliance. No HIPAA certification exists; HIPAA compliance is self-attested.
- **"First observed"** dates come from public web archives and reflect the earliest capture we found. Archive coverage is incomplete, so pages may have existed earlier.
- **"Access-gated"** means the trust center exists but its contents require a request-access step (an NDA or an approval), so its framework claims are not publicly visible. We report the gate itself, never what may sit behind it. "Partially gated" means some documents require access while the framework claims are public.
- **"Last read"** appears when a refresh could not re-read a trust center (a network failure, a rate limit, a bot block). The previously observed claims are kept with the date they were last read, and dropped after two consecutive refreshes without a successful read. A trust center that was read and found empty or gated is never carried forward.

## How trust centers are discovered

Trust centers are found, not submitted. Candidate hosts come from three sources: the Common Crawl web index, a sweep of the most-visited domains expanded with the subdomains trust centers use (`trust.`, `security.`, `compliance.`, `trustcenter.`, `trust-center.`), and the subprocessors that trust centers themselves disclose, which are fed back in. Every candidate is resolved in public DNS; hosts that only timed out get a second, slower pass so a published trust center never disappears over one bad second. The DNS record identifies the hosting platform (Vanta, SafeBase, Conveyor, Drata, Secureframe, and others). A candidate whose DNS record names no platform is read in full when its page carries a platform's markup or when the company's own homepage links to it; the rest stay in tier D and are checked again at the next refresh. Every published organization is re-probed on every refresh.

**Domains discovered versus organizations.** The release counts every domain where a trust-style host resolved, including hosts with no recognized platform behind them. Only domains with evidence of a trust center become profiles (see [evidence behind each record](#evidence-behind-each-record)); a domain that merely resolved is never published. That is why "domains discovered" is larger than the number of organizations in the index.

**Correction, 5 October 2026.** The open dataset files released from 8 September to 3 October 2026 included every discovered domain, not only the organizations with a trust center, so their record counts were about two and a half times the size of the index. The site's profiles and counts were not affected. Later releases contain only organizations with a trust center; the [release log](https://github.com/synergetic-solutions/trust-index-data/blob/main/docs/RELEASES.md) lists the affected releases and their counts.

## What is read from a trust center

Framework claims are read from the badges the trust center itself publishes, through each platform's own public page data. Label variants collapse into families (SOC 2 Type I and Type II are both SOC 2; ISO/IEC 27001:2022 is ISO 27001; StateRAMP and its new name, GovRAMP, are one family shown as "StateRAMP / GovRAMP"). Not every badge is the same kind of evidence: a third-party audit or assessment (SOC 1, 2, 3, IRAP, and CMMC at Level 2 or 3) is an independent auditor's or assessor's report on the organization; a certification (the ISO family, HITRUST, TISAX, CSA STAR, Cyber Essentials, C5, FedRAMP and the state programs StateRAMP / GovRAMP and TX-RAMP, PCI DSS, and the audited AI programs: HITRUST AI Security, CSA STAR for AI Level 2, AIUC-1) is issued by an accredited body or program; a self-attested claim (HIPAA, GDPR, CCPA, CPRA, LGPD, PIPEDA, FERPA, COPPA, DORA, NIS2, the EU-US Data Privacy Framework) has no certification behind it. Alignment frameworks with no certificate, such as the NIST CSF, NIST 800-53, NIST 800-171, the CIS Controls and the AI frameworks described below, are labeled claims. The directory labels each family accordingly.

Three families have their own rules. CMMC counts as a third-party assessment only when the badge shows Level 2 or Level 3, the levels an outside assessor checks (a certified third-party assessment organization, or C3PAO, for Level 2, and the government for Level 3). A plain CMMC badge or Level 1 is a self-attested claim, and so is a level the label calls ready or self-assessed, or one the organization is preparing for. A level listed as in progress, or one the organization is working toward, is not counted at all (see below). FIPS 140 is always a claim, worded "uses validated cryptography": the government's Cryptographic Module Validation Program validates cryptographic modules, not companies, so the directory never calls FIPS 140 a certification. IRAP, Australia's government security assessment program, is a third-party assessment and never a certification. IRAP reports are not publicly verifiable, so the directory shows an IRAP badge as what the organization advertises and cannot confirm the report behind it.

Only frameworks the organization holds are counted. A framework the trust center lists as in progress, planned, pending, coming soon or on a roadmap, or one it says it is pursuing or working toward, is not counted among the frameworks it advertises. The same goes for a framework given a future date beside its name ("expected Q3 2027", "audit expected to close November 2026"), unless the date is for the renewal of a report it holds. A short heading such as "Roadmap:" or "Planned certifications:" covers the frameworks listed directly after it and nothing further down the page. A framework the page says the organization does not hold or seek ("not pursuing", "no plans to", "not certified") is not counted, and a page that says so and shows no other claim counts as read, so earlier claims are not carried forward over it. The status can come from the platform's own status field for a badge or from the words next to the framework's name. When a page names a framework both ways, a mention marked certified or compliant beside the name keeps it. PCI DSS named only as a property of the organization's payment provider or processor ("payments are processed by a PCI-compliant provider") is not counted, because it describes the provider's card-data environment. A PCI DSS claim the organization makes for itself, including as a PCI service provider, still counts. A trust center that lists more than 20 frameworks is checked by hand, since a list that long can be a template's full catalog.

Every read records an outcome. A trust center that answered and showed nothing is "empty". One that denied its public report, or whose every document requires a request-access step, is "access-gated". One that could not be read (network failure, rate limit, bot block) is neither; its previous claims are carried forward as "last read" and dropped after two consecutive refreshes without a successful read.

## AI governance frameworks

Some badges cover how an organization governs its use of AI. Four of them can be certified, because a third party audits the organization against them: ISO/IEC 42001, HITRUST AI Security, CSA STAR for AI Level 2 and AIUC-1. Only these get certification wording. The others are described as frameworks an organization advertises alignment with: the NIST AI RMF, the EU AI Act, CSA STAR for AI without a level (the self-assessment), MITRE ATLAS, Google's Secure AI Framework (SAIF) and the OWASP Top 10 for LLM and generative AI applications. Neither the NIST AI RMF nor the EU AI Act can be certified, and no EU AI Act certificate exists today.

Names that other things share count only with their qualifier: "Atlas" needs MITRE, "SAIF" needs Google or the full name, "AI Act" needs EU or European, and "OWASP Top 10" on its own is the web application list.

## When the vocabulary grows

The set of framework families the directory recognizes grows over time. A badge in a new family was often on the trust center before the directory could read it, so the first release that recognizes a family lists those organizations as vocabulary additions, apart from new adopters. Where the platform supplied the badge's own label, the comparison reads it again with the older rules; otherwise the new families are set aside for that one comparison. From the following release on, the new families are compared like any other. Earlier releases are not recounted. A renamed family is read under its new name in older releases too, so StateRAMP becoming StateRAMP / GovRAMP shows as neither a loss nor a gain. When a rule stops counting a kind of label, as the in-progress rule above did, the frameworks that leave the list in the first release under it are reported as a reclassification, as a total, and not as losses. PCI DSS removed by the provider rule in that release is listed apart from losses too.

## Subprocessors and chain trust

Where a trust center discloses its subprocessors, the list is read as published: name, the URL the discloser gave, and its stated purpose. **Chain trust** is the number of those subprocessors that themselves have a trust center in this index, matched only by the disclosed URL's registrable domain, never by name, so a low share can mean private subprocessors or sparse disclosure metadata, while a high share is real signal. It is shown as "N of M", never as a judgment about any vendor. Subprocessor lists appear on profiles; the graph they form is not part of the open dataset.

Each disclosed subprocessor is also assigned a canonical provider, so spellings such as "Amazon Web Services, Inc." and "AWS" count as one provider. The provider comes from a curated alias table matched on the cleaned name, with legal suffixes and bracketed text set aside, and then from the disclosed URL when the name is not in the table. A company that runs distinct products on one domain is split by product: Google Workspace and Google Cloud; Microsoft Azure, Microsoft 365 and Intune; AWS and other Amazon. The name as written is kept.

A subprocessor is flagged as an **AI provider** when it receives model inputs: a model vendor (OpenAI, Anthropic, Google Gemini, Mistral, Cohere and others), a cloud AI service named as such (Amazon Bedrock, Azure OpenAI, Google Vertex AI), or an inference host or router (Hugging Face, OpenRouter, Groq and others). The AI provider counts include only these. Tools built around models form a separate **AI infrastructure** category: LLM tooling and observability, vector databases and AI compute platforms. A cloud provider named on its own (AWS, Azure, Google Cloud) is never AI in either category, because hosting a model there cannot be told apart from ordinary hosting. The AI flag is read from the provider: a subprocessor whose disclosed URL is on an AI vendor's own domain counts even when its name is misspelled, and a cloud AI service named inside a cloud's entry, such as "Amazon Web Services (Bedrock)", counts as that service.

Names are matched on whole words, so a company whose name only begins with a vendor's name is not caught. When an AI vendor shares its name with an unrelated company (Gemini is also a crypto exchange), the entry counts only when its name, URL or stated purpose points to the AI vendor and its URL does not point to the other company. Entries that stay ambiguous are left out. The flag records what the discloser named and says nothing about how either party handles data. The lists are revised over time, and release-to-release comparisons recount both releases with the current lists.

## Segments and names

Each organization is assigned one market segment, chosen by a language model from the organization's own public description and reviewed by hand where we have looked; organizations with no public description are left unsegmented and appear in the directory but on no hub. "Vertical SaaS" is used only for software built for one non-technology industry that no other segment covers. Display names come from Wikidata when an organization is listed there and the label plausibly matches the domain; otherwise the name is derived from the domain, which is why some read like a URL. Corrections to either are welcome.

## Other sources

Identity details (founding year, industry, external profiles) come from Wikidata. Summaries come from Wikipedia where an article exists (CC BY-SA, linked from the profile) and otherwise from the organization's own site description. "First observed" dates come from the Internet Archive. Hiring signals come from the organization's own public job board (Greenhouse, Lever or Ashby; the profile names which). Frameworks named in job descriptions are shown separately from advertised claims: a role that mentions ISO 27001 is a plan, not a badge. Every data point carries the date it was observed.

## Security hygiene score

Every profile carries a hygiene score out of 4 measured on the company domain, not the trust center: a security.txt file with a contact, an SPF record, a DMARC policy at quarantine or reject, and DNSSEC. It is deliberately independent of compliance claims; a SOC 2 report and an unenforced DMARC policy coexist on most trust centers. Segment hubs show the distribution.

## Published controls

Where a platform exposes the controls an organization publishes on its trust center, the profile shows how many, how many the platform marks passing, the categories, and, where the platform maps controls to frameworks, which ones. Platforms let organizations show passing controls only, so the list is the organization's own selection and never a statement of control coverage.

## Business associate agreements

For organizations that advertise HIPAA or sit in the healthcare segment, the profile says whether BAA information was found on the public trust center: a document or FAQ naming a business associate agreement, either publicly readable or behind a request-access step. Not finding one never means an organization will not sign a BAA; many provide one through sales. Publishing BAA information is not a HIPAA compliance claim, and organizations can point us at their BAA page through the correction form.

## The scorecard

The [scorecard](https://synergetic.solutions/resources/trust-center-directory/scorecard/) runs four public checks on any domain, one point each: a security.txt file with a contact, an SPF record, a DMARC record, and DNSSEC. It also reports whether a trust center resolves on the domain, without scoring it. The percentile compares the score with every organization in the index. The directory's own posture score uses the same four checks but counts DMARC only at quarantine or reject; the scorecard accepts any policy and says so.

## Evidence behind each record

Every record carries an evidence tier, and the open dataset publishes it with the record.

- **Tier A**: the trust center was read through its platform's own API (Vanta, SafeBase, Drata, Conveyor and others), including access-gated ones.
- **Tier B**: the trust center's page shows its compliance content, and a second signal backs it: the platform's DNS record or page markup, a link from the company's own website, or the company's security.txt.
- **Tier C**: the page shows trust-center content and nothing else backs it.
- **Tier D**: a trust-style hostname resolved but nothing could be read, or it served the company homepage, a not-found page, a closed trust center, or a page that names frameworks but does not present itself as a trust center. Tier D is never published; it is re-checked every refresh.

Organizations in tiers A and B get a profile and make up the index's counts. The open dataset also includes tier C, labelled as such. A trust center that cannot be read keeps its tier until two consecutive refreshes have passed without a successful read.

## Corrections and claims

Corrections are welcome and are verified against public evidence before publication: use the [correction form](https://github.com/synergetic-solutions/trust-index-data/issues/new/choose), citing the public page that shows the corrected value. Claims of compliance that are not publicly verifiable are not published; the fastest way to update your profile is to publish the claim on your trust center, and the next refresh will pick it up.

## About this dataset

Profiles refresh monthly from an automated pipeline; corrections deploy when they are verified and merged. Coverage and enrichment expand with each refresh, and every release publishes [what changed](https://synergetic.solutions/resources/trust-center-directory/changes/), including how much of any movement is measurement rather than market. Each profile records the date of the release in which its published content last changed; a refresh that finds the same content, or cannot read the trust center, leaves that date alone.
