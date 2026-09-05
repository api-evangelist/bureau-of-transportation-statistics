---
name: Find and query a BTS dataset
description: >-
  Locate a Bureau of Transportation Statistics dataset by keyword, read its column schema,
  then pull rows with SoQL filters and correct paging.
api: openapi/bureau-of-transportation-statistics-resource-api-openapi.yml
operations: [searchCatalog, getDatasetMetadata, queryDataset]
generated: '2026-09-05'
method: generated
source: >-
  openapi/bureau-of-transportation-statistics-metadata-api-openapi.yml,
  openapi/bureau-of-transportation-statistics-resource-api-openapi.yml,
  conventions/bureau-of-transportation-statistics-conventions.yml
---

# Find and query a BTS dataset

Base URL `https://data.bts.gov`. No credential is required. Send `X-App-Token: <token>` if
you have one — register free at https://data.bts.gov/profile/edit/developer_settings — it
grants no extra data, it only moves you out of the shared anonymous throttling pool.

## 1. Find the dataset — `searchCatalog`

```
GET /api/catalog/v1?domains=data.bts.gov&q=bikeshare&only=datasets&limit=10
```

Read `results[].resource.id` — that four-by-four (`^[a-z0-9]{4}-[a-z0-9]{4}$`, e.g.
`bw6n-ddqk`) is the only identifier you need for every other call. `resultSetSize` tells you
how many matched.

Alternative: the whole catalog is one document at https://data.bts.gov/data.json (DCAT-US
1.1, 418 datasets). Fetch it once and search offline if you are doing many lookups.

## 2. Read the columns before you write a filter — `getDatasetMetadata`

```
GET /api/views/{datasetId}.json
```

**Do this first, always.** The OpenAPI describes a row as `additionalProperties: true`
because every dataset has its own columns; the column names are only knowable at runtime.
Use `columns[].fieldName` — those are the names SoQL expects, not the human labels.

If you would rather have typed columns, the OData CSDL at
`https://data.bts.gov/api/odata/v4/$metadata` declares an `EntityType` per tabular dataset
with real EDM types (184 of them).

## 3. Pull rows — `queryDataset`

```
GET /resource/{datasetId}.json?$select=obs_date,rpm&$where=obs_date>'2024-01-01'&$order=obs_date&$limit=1000&$offset=0
```

Rules that matter:

- **Always pass `$order`.** Paging without a stable sort can repeat or skip rows. `:id` works
  on any dataset.
- `$limit` defaults to 1000 and maxes at 50000.
- The response is a bare JSON array — no envelope, no total. An empty array means you have
  reached the end; that is your loop termination condition.
- Numbers come back as JSON strings on the SODA surface. The OData surface returns them typed.

Need CSV or geospatial instead? Same query, different extension: `queryDatasetCsv`
(`/resource/{id}.csv`) and `queryDatasetGeoJson` (`/resource/{id}.geojson`). Format is chosen
by file extension, not by an `Accept` header.

## 4. Handle the failures you will actually meet

| Status | What it means here | What to do |
|---|---|---|
| 202 | Long query still running | Retry; 202 is **not** success |
| 400 | Bad SoQL | Read `source` in the body — it carries the parse position |
| 403 | Non-tabular asset | `"no row or column access to non-tabular tables"` — this id is a story/map/chart, not a dataset |
| 404 | No such dataset | Re-run step 1 |
| 429 | Throttled | Back off exponentially. **No `Retry-After` or `RateLimit-*` header is sent** — you get no forward signal, only the 429 |

Error bodies are `{code, error, message, status, data, source}`. This is **not** RFC 9457 —
do not look for `type` or `application/problem+json`.

## 5. Be a good citizen

- `robots.txt` on data.bts.gov sets `Crawl-delay: 1`.
- Responses carry `ETag` and `Last-Modified` — use conditional GET when polling.
- Know when to poll at all: https://data.bts.gov/catalog.rss is a dated feed of every dataset
  created or updated.
- Quote `X-Socrata-RequestId` from the response headers if you report a problem.

Everything on this API is a `GET`. There is nothing to undo, nothing to make idempotent, and
no dry-run mode is needed — `$limit=1` is your rehearsal.
