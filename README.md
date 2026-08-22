# Bureau of Transportation Statistics (bureau-of-transportation-statistics)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

The Bureau of Transportation Statistics (BTS), part of the Department of Transportation (DOT) is the preeminent source of statistics on commercial aviation, multimodal freight activity, and transportation economics, and provides context to decision makers and the public for understanding statistics on transportation.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/bureau-of-transportation-statistics/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/bureau-of-transportation-statistics/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Consumer
- **Access:** 3rd-Party

## Tags

- Federal Government
- Statistics
- Transportation
- Aviation
- Freight
- Open Data

## Timestamps

- **Created:** 2024-11-30
- **Modified:** 2026-04-23

## APIs

### BTS Open Data SODA API

The BTS Open Data portal powered by Socrata provides programmatic access to transportation datasets via the Socrata Open Data API (SODA). Supports filtering, querying, and aggregation across aviation, freight, and transportation economics datasets. Also supports OData V2/V4 for tools like Tableau and Excel.

- **Human URL:** [https://data.bts.gov/](https://data.bts.gov/)
- **Base URL:** `https://data.bts.gov/resource/`

#### Tags

- Federal Government
- Transportation
- Open Data
- Statistics

#### Properties

- [Portal](https://data.bts.gov/)
- [Documentation](https://dev.socrata.com/)
- [Data A P I](https://catalog.data.gov/dataset?organization=dot-gov&q=bts)
- [Postman Collection](collections/bureau-of-transportation-statistics.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/bureau-of-transportation-statistics.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### TranStats - Airline On-Time Performance Data

TranStats is BTS's aviation and transportation statistics database providing flight on-time performance data, carrier and airport snapshots, fuel consumption data, and comprehensive airline statistics. Enables custom queries and downloads across hundreds of aviation data tables.

- **Human URL:** [https://www.transtats.bts.gov/](https://www.transtats.bts.gov/)

#### Tags

- Federal Government
- Transportation
- Aviation
- Statistics

#### Properties

- [Portal](https://www.transtats.bts.gov/)
- [Tool](https://www.transtats.bts.gov/ONTIME/)
- [Postman Collection](collections/bureau-of-transportation-statistics.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/bureau-of-transportation-statistics.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### BTS Freight Analysis Framework (FAF)

The Freight Analysis Framework integrates data from multiple sources to create a comprehensive picture of freight flows to, from, within, and through the United States. Includes volume, value, and mode of shipment data for domestic and international freight.

- **Human URL:** [https://www.bts.gov/faf](https://www.bts.gov/faf)

#### Tags

- Federal Government
- Freight
- Transportation
- Statistics

#### Properties

- [Documentation](https://www.bts.gov/faf)
- [Postman Collection](collections/bureau-of-transportation-statistics.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/bureau-of-transportation-statistics.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [GitHub Organization](https://github.com/dotbts)
- [LinkedIn](https://www.linkedin.com/company/bureau-of-transportation-statistics-bts)
- [Website](https://www.bts.gov)
- [Portal](https://data.bts.gov/)
- [Privacy Policy](https://www.bts.gov/privacy-policy)
- [Tran Stats](https://www.transtats.bts.gov/)
- [Data  Portal](https://catalog.data.gov/dataset?organization=dot-gov&q=bts)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
