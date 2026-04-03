# Immowelt Scraper

Extract structured data from [immowelt.de](https://immowelt.de) — immowelt.de — Germany's major residential property portal. Apartment-buy pagination, expose details, and structured broker data.

**[Immowelt Scraper on Apify →](https://apify.com/blackfalcondata/immowelt-scraper)**

---

## Key features

**Search with filters** — Search by keyword, location, or direct Immowelt URLs. Supports compact runs, result caps, and browser mode for tougher pages.

**Detail enrichment** — Fetch expose descriptions, broker details, contact phone numbers, room counts, living area, and price metadata.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing means no duplicates and cleaner monitoring workflows.

---

## Use cases

**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from immowelt.de on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from immowelt.de.

---

## Quick start

```json
{
  "query": "altbau balkon",
  "maxResults": 50,
  "includeDetails": true
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | Property search keywords. Use JSON array for multi-query. Leave empty when using startUrls only. |
| `country` | enum | `"DE"` | Which immowelt.de market to search. |
| `location` | string | — | City, district, or region. Use JSON array for multi-location. |
| `startUrls` | array | — | Direct Immowelt search URLs or expose URLs. |
| `maxResults` | integer | `25` | Maximum total property listings to return (0 = unlimited). Dynamic memory profile: up to 25 results uses 1024 MB, 26+ results uses 2048 MB. |
| `maxPages` | integer | `5` | Maximum search-result pages to scrape per search source. |
| `includeDetails` | boolean | `true` | Fetch each expose page for full description, price data, and provider info. |
| `transport` | enum | `"scrapedo"` | Choose the standard fetch mode or browser mode for tougher pages. |
| `proxyCountryCode` | string | — | Country code to use for browser-mode sessions. |
| `includeCompanyProfile` | boolean | `false` | Fetch provider profile pages for broker metadata when available. |
| `descriptionMaxLength` | integer | `0` | Truncate description to this many characters. 0 = no truncation. |
| `compact` | boolean | `false` | Output only core fields (for AI-agent/MCP workflows). |
| `incrementalMode` | boolean | `false` | Compare against previous run state. Requires stateKey. |
| `stateKey` | string | — | Stable identifier for the tracked search universe (for example "buy-berlin-apartment"). |
| `emitUnchanged` | boolean | `false` | When incremental, also emit records that haven't changed. |
| `emitExpired` | boolean | `false` | When incremental, also emit records no longer found. |

---

## FAQ

**What kind of properties can it scrape?**
The actor is built for Immowelt residential listings and works well for apartment and house searches where expose pages contain the richest structured data.

**Can I start from my own search URL?**
Yes. Use `startUrls` to pass a ready-made Immowelt search URL or a specific expose URL when you want deterministic coverage.

**Is it legal to scrape immowelt.de?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check the target site's terms of service for your specific use case.

**How does incremental mode work?**
Each listing gets a content hash. On subsequent runs, only new or changed listings are emitted — saving time, compute, and storage.

**What output fields are included?**
Core fields include title, location, rooms, area, price, price per square meter, broker/provider data, detail URL, coordinates, and scrape timestamps.

**Is browser mode required?**
No. The default mode works for standard runs, while browser mode is available for tougher sessions and anti-blocking scenarios.

---

## Known limitations

- Immowelt changes search and expose layouts periodically, so selector maintenance is occasionally required.
- Some contact and provider fields are only visible on detail pages, not on the search-result cards.
- Browser mode is slower and more resource-intensive than standard mode, so it is best reserved for tougher sessions.
- Pagination and anti-blocking behavior can vary by query, geo, and traffic pattern over time.

---

## Related products by Black Falcon Data

- [StepStone Scraper](https://github.com/BlackFalconData-org/stepstone-scraper) — Job listings from 18 European portals
- [Indeed Job Scraper](https://github.com/BlackFalconData-org/indeed-job-scraper) — Indeed job listings with salary data
- [Glassdoor Job Scraper](https://github.com/BlackFalconData-org/glassdoor-job-scraper) — Glassdoor listings with company ratings

---

*Last updated: 2026 04*
