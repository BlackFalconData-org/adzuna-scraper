# Adzuna Job Scraper

Extract structured data from [adzuna.com](https://adzuna.com) — the global job board with 20+ country markets. Structured salary (min/max/currency), location coordinates, and job change monitoring.

**[Adzuna Job Scraper on Apify →](https://apify.com/blackfalcondata/adzuna-scraper)**

---

## Key features


**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

**Structured data** — 30 fields per listing. Clean JSON output with consistent field naming. All fields always present — null when unavailable, never omitted.

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
  "maxResults": 50
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
| `distanceMiles` | integer | — | Search radius in miles from the specified location. Only used when Location is set. |
| `maxResults` | integer | `50` | Maximum number of jobs to return (0 = unlimited, up to Adzuna's limit). |
| `descriptionMaxLength` | integer | `0` | Truncate description to N characters. 0 = no truncation. |
| `compact` | boolean | `false` | Return core fields only (jobId, title, company, salary, url). Ideal for AI-agent and MCP workflows. |
| `incrementalMode` | boolean | `false` | Only return new or changed jobs compared to the previous run. |
| `stateKey` | string | — | Unique identifier for the tracked job universe (e.g. "developer-london"). Required when Incremental Mode is enabled. |

---

## FAQ

**Do I need an Adzuna account?**
Yes — a free API key is required. Register at [developer.adzuna.com](https://developer.adzuna.com) and pass `appId` and `appKey` as input. Registration is free and takes under a minute.

**How many results can I fetch?**
Up to the total available for your query (typically thousands per market). Set `maxResults` to control the cap. For broad queries like "software engineer" in GB, 10,000+ results are available.

**Are descriptions full-length?**
Adzuna's API truncates descriptions to ~500 characters at the source — this is an API limitation, not a scraper limitation. Full descriptions are not available via the API.

**Which countries are supported?**
20+ markets including GB, US, AU, CA, DE, FR, NL, BE, AT, IT, ES, BR, IN, MX, SG, PL, NZ, ZA, RU, and AR.

**Is it legal to use this data?**
This actor uses Adzuna's official public API. All data accessed is publicly available. Review Adzuna's API terms of service for your specific use case.

**How does incremental mode work?**
Each listing gets a content hash. On subsequent runs, only new or changed listings are emitted — saving time, compute, and storage.

---

## Known limitations

- Descriptions are truncated to ~500 characters — this is enforced by Adzuna's API, not this scraper
- No contact details (email/phone) — Adzuna does not expose employer contact data via their API
- No company website or headcount — not available in the Adzuna API response
- No direct apply URL — `url` is Adzuna's redirect link, not the employer's direct application page
- No job expiry date — not provided by the Adzuna API

---

## Related products by Black Falcon Data


- [StepStone Scraper](https://github.com/BlackFalconData-org/stepstone-scraper) — Job listings from 18 European portals
- [Indeed Job Scraper](https://github.com/BlackFalconData-org/indeed-job-scraper) — Indeed job listings with salary data
- [Glassdoor Job Scraper](https://github.com/BlackFalconData-org/glassdoor-job-scraper) — Glassdoor listings with company ratings

---

*Last updated: 2026-03-30*
