---
name: Query BTS data with OData 4.0
description: >-
  Use the typed OData 4.0 surface on data.bts.gov when you need a real schema, typed values,
  or a BI tool that speaks OData rather than SoQL.
api: openapi/bureau-of-transportation-statistics-resource-api-openapi.yml
operations: [queryDataset]
generated: '2026-09-05'
method: generated
source: >-
  https://data.bts.gov/api/odata/v4/$metadata (fetched verbatim to
  odata/bureau-of-transportation-statistics-odata-metadata.xml on 2026-09-05),
  conformance/bureau-of-transportation-statistics-conformance.yml
---

# Query BTS data with OData 4.0

data.bts.gov exposes the same datasets a second way, as a standards-conformant OData 4.0
service. Use this surface when you want types, or when the consumer is Excel, Power BI or
Tableau. Use the SoQL surface when you want expressive filtering.

## 1. Get the schema for everything, once

```
GET https://data.bts.gov/api/odata/v4/$metadata
```

Returns a CSDL/EDMX 4.0 document (`edmx:Edmx Version="4.0"`, OASIS namespace) declaring
**184 `EntityType`s and 184 `EntitySet`s** — one per tabular BTS dataset. A verbatim copy is
in this repository at `odata/bureau-of-transportation-statistics-odata-metadata.xml`.

Each `EntitySet` `Name` is the dataset's Socrata four-by-four, so `bw6n-ddqk` in SoQL and
`bw6n-ddqk` in OData are the same asset. Each `EntityType` keys on `__id` (Socrata's synthetic
row id, e.g. `row-hsjj_k39w.gbwr`) and types every column with a real EDM type.

## 2. Read a dataset

```
GET https://data.bts.gov/api/odata/v4/bw6n-ddqk
GET https://data.bts.gov/api/odata/v4/bw6n-ddqk?$top=100&$skip=0
```

The response carries `@odata.context` and a `value[]` array. **Numbers come back typed here**
(`"asm": 76146639`), where the SoQL surface returns them as strings (`"asm": "76146639"`) —
that difference alone is often the reason to pick this surface.

## 3. Two things that will bite you

- **Per-dataset `$metadata` is not supported.** `GET /api/odata/v4/{id}/$metadata` returns
  400 `"The URI is malformed."`. Fetch the service-root `$metadata` above instead.
- **Only tabular assets exist here.** A story, map or chart id returns 500 with a diagnostic
  code, not a clean 404. Confirm the asset is a dataset first — via
  `GET /api/views/{id}.json` (`assetType`) or by checking the id appears as an `EntitySet` in
  the CSDL.

## 4. Version note

`/api/odata/v2/{id}` returns `404 not_found — "No service found for this URL."` as of
2026-09-05. The v2 surface Socrata once documented is gone from this deployment and BTS
published no deprecation notice. Target v4 only, and see
`lifecycle/bureau-of-transportation-statistics-lifecycle.yml`.

Errors on this surface use a **different envelope** from the SoQL surface:
`{"error": {"code": ..., "message": ...}}`. Handle both shapes on one host.
