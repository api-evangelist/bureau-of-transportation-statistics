---
name: Search the BTS geospatial catalog (NTAD)
description: >-
  Discover National Transportation Atlas Database layers through the OGC API - Records
  surface on geodata.bts.gov and follow a record to its live ArcGIS feature service.
api: openapi/bureau-of-transportation-statistics-geodata-search-openapi.json
operations:
  - OgcRootController_getSiteRoot_api/search/v1
  - OgcRootConformanceController_getApiConformance_api/search/v1
  - CollectionController_getSiteCollections_api/search/v1
  - OgcItemController_getSiteCollectionItems_api/search/v1
  - OgcItemController_getSiteCollectionItemById_api/search/v1
  - QueryableController_getSiteCollectionQueryables_api/search/v1
  - OgcItemController_getRelatedOgcItemsById_api/search/v1
generated: '2026-09-05'
method: generated
source: >-
  openapi/bureau-of-transportation-statistics-geodata-search-openapi.json (harvested
  verbatim from https://geodata.bts.gov/api/search/definition/?f=json on 2026-09-05)
---

# Search the BTS geospatial catalog (NTAD)

Base URL `https://geodata.bts.gov`. Anonymous. This is a real OGC API - Records
implementation, so if you already speak OGC API you need no bespoke connector.

The published OpenAPI ships with an **empty `servers[]` array**. The base above is the host
the document was fetched from; every path in the spec is already absolute from the host root.

## 1. Start at the landing page

```
GET /api/search/v1
```

Returns `links[]` with `rel=data` (collections), `rel=conformance`, and `rel=service-desc`
pointing at the OpenAPI itself (`/api/search/definition/?f=json`).

## 2. Confirm what it supports

```
GET /api/search/v1/conformance
```

Returns nine `opengis.net` conformance classes: OGC API - Common Parts 1 and 2, OGC API -
Features Part 1 (core, geojson, oas30) and OGC API - Records Part 1 (core, json). Check this
rather than guessing which OGC verbs are available.

## 3. List collections, then query items

```
GET /api/search/v1/collections
GET /api/search/v1/collections/dataset/items?q=freight&limit=20
```

There is one collection, `dataset` (~142 NTAD records). Before building a filter, ask what is
filterable:

```
GET /api/search/v1/collections/dataset/queryables
```

Page with `limit` and `startindex`; follow `links[]` with `rel=next` rather than incrementing
blindly.

## 4. Follow a record to the live service

```
GET /api/search/v1/collections/dataset/items/{itemId}
```

`itemId` is a 32-hex ArcGIS item id, **not** a Socrata four-by-four — the geospatial catalog
and the open-data portal use different identifier spaces. A record's distributions include:

- `ArcGIS GeoServices REST API` → e.g.
  `https://services.arcgis.com/xOi1kZaI0eWDREZv/arcgis/rest/services/{Service}/FeatureServer/0`
  — the live queryable layer (1,079 feature services in the tenant)
- `GeoJSON` / `CSV` / `Shapefile` / `KML` / `GPKG` → `https://geodata.bts.gov/api/download/v1/items/{itemId}/{format}?layers=0`

`/items/{recordId}/related` and `/items/{recordId}/connected` walk to sibling records.

Bulk alternative: the whole catalog as one DCAT-US 1.1 document at
`https://geodata.bts.gov/api/feed/dcat-us/1.1.json`.

## 5. Watch out

- The spec declares **only 200 responses** on all 17 operations. The 400/404/429 you will
  meet are undocumented — handle them defensively.
- `robots.txt` on geodata.bts.gov sets `Crawl-delay: 60`. Respect it; prefer the bulk DCAT
  feed over crawling item by item.
- Not every NTAD record is BTS-authored — publishers include FHWA, FRA, NHTSA, EPA and USACE.
  Read `publisher.name` before attributing data to BTS.
