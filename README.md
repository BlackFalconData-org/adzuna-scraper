# Adzuna Job Scraper

Extract structured data from [adzuna.com](https://adzuna.com) — the global job board with 20+ country markets. Structured salary (min/max/currency), location coordinates, and job change monitoring.

**[Adzuna Job Scraper on Apify →](https://apify.com/blackfalcondata/adzuna-scraper)**

---

## Key features



**Detail enrichment** — Fetch full job descriptions, salary data for each listing.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

**Structured data** — 24 fields per listing. Clean JSON output with consistent field naming. All fields always present — null when unavailable, never omitted.

---

## Use cases



**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from adzuna.com on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from adzuna.com.

---

## Quick start

```json
{
  "maxResults": 50,
  "includeDetails": true
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `appId` | string | — | Your Adzuna app_id. Register for free at developer.adzuna.com. |
| `appKey` | string | — | Your Adzuna app_key. Register for free at developer.adzuna.com. |
| `keyword` | string | — | Job search keywords (e.g. "software engineer", "nurse"). |
| `country` | enum | `"gb"` | Which Adzuna market to search. |
| `location` | string | — | City, region, or postcode (e.g. "London", "Berlin", "SW1"). |
| `category` | string | — | Adzuna category tag (e.g. "it-jobs", "engineering-jobs"). Leave blank for all categories. |
| `contractType` | enum | — | Filter by contract type. |
| `contractTime` | enum | — | Filter by working hours. |
| `sortBy` | enum | `"default"` | Sort results by relevance, date, or salary. |
| `salaryMin` | integer | — | Filter jobs with salary above this value (in local currency). |
| `salaryMax` | integer | — | Filter jobs with salary below this value (in local currency). |
| `distanceMiles` | integer | `10` | Search radius in miles from the specified location. |
| `maxResults` | integer | `50` | Maximum number of jobs to return (0 = unlimited, up to Adzuna's limit). |
| `includeDetails` | boolean | `true` | Fetch full job description from the detail endpoint. Doubles API calls but provides complete descriptions. |
| `descriptionMaxLength` | integer | `0` | Truncate description to N characters. 0 = no truncation. |
| `compact` | boolean | `false` | Return core fields only (jobId, title, company, salary, url). Ideal for AI-agent and MCP workflows. |
| `incrementalMode` | boolean | `false` | Only return new or changed jobs compared to the previous run. |
| `stateKey` | string | — | Unique identifier for the tracked job universe (e.g. "developer-london"). Required when Incremental Mode is enabled. |

---

## FAQ

<!-- WRITE: 4-6 Q&A pairs relevant to this product -->

**Is it legal to scrape adzuna.com?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check the target site's terms of service for your specific use case.

**How does incremental mode work?**
Each listing gets a content hash. On subsequent runs, only new or changed listings are emitted — saving time, compute, and storage.

---

## Known limitations

<!-- WRITE: 4-6 honest limitations -->

- <!-- WRITE: limitation 1 -->
- <!-- WRITE: limitation 2 -->

---

## Related products by Black Falcon Data



- [StepStone Scraper](https://github.com/BlackFalconData-org/stepstone-scraper) — Job listings from 18 European portals
- [Indeed Job Scraper](https://github.com/BlackFalconData-org/indeed-job-scraper) — Indeed job listings with salary data
- [Glassdoor Job Scraper](https://github.com/BlackFalconData-org/glassdoor-job-scraper) — Glassdoor listings with company ratings

---

*Last updated: 2026 03*
