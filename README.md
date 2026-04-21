# Adzuna Job Scraper

Extract structured data from [adzuna.com](https://adzuna.com) — the global job board with 20+ country markets. Structured salary (min/max/currency), location coordinates, and job change monitoring.

**[Adzuna Job Scraper on Apify →](https://apify.com/blackfalcondata/adzuna-scraper?fpr=1h3gvi)**

---

## Key features




**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

**Change classification** — Track cross-run repost detection across runs. Build audit trails of how listings evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Description truncation** — Cap description length per listing to control output size and cost.

**Result cap** — Stop after N listings (up to 10.000). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every listing returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases




**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from adzuna.com on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from adzuna.com.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired listings. Perfect for price-tracking, churn analysis, and alerting pipelines.

**Compensation benchmarking**
Aggregate salary ranges across roles, industries, and locations on adzuna.com to inform pricing decisions, hiring plans, or candidate negotiations.

**AI / LLM training data**
Structured JSON per listing is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

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


## Output fields

Every listing returns the same 24-field schema. Missing values are `null` — never omitted.

- `jobId`
- `adzunaId`
- `title`
- `company`
- `location`
- `locationArea`
- `latitude`
- `longitude`
- `salaryMin`
- `salaryMax`
- `salaryIsPredicted`
- `salaryCurrency`
- `category`
- `categoryTag`
- `contractType`
- `contractTime`
- `description`
- `url`
- `portalUrl`
- `postedAt`
- `country`
- `scrapedAt`
- `source`
- `changeType`


## Sample output

One object per listing. Here is a real example from a production run:

```json
{
  "jobId": "a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2",
  "adzunaId": "5000000001",
  "title": "Senior Software Engineer",
  "company": "TechCorp Ltd",
  "location": "London",
  "locationArea": [
    "UK",
    "London"
  ],
  "latitude": 51.5074,
  "longitude": -0.1278,
  "salaryMin": 70000,
  "salaryMax": 90000,
  "salaryIsPredicted": false,
  "salaryCurrency": "GBP"
}
```

*Truncated — full records contain 24 fields. See Output fields for the complete schema.*


**[Try Adzuna Job Scraper now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/adzuna-scraper?fpr=1h3gvi)**


## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.005 |
| Result | $0.0025 |

See the [actor on Apify](https://apify.com/blackfalcondata/adzuna-scraper?fpr=1h3gvi) for current pricing.

---

## Related products by Black Falcon Data




- [StepStone Scraper](https://apify.com/blackfalcondata/stepstone-scraper?fpr=1h3gvi) — Job listings from 18 European portals
- [Indeed Job Scraper](https://apify.com/blackfalcondata/indeed-job-scraper?fpr=1h3gvi) — Indeed job listings with salary data
- [Glassdoor Job Scraper](https://apify.com/blackfalcondata/glassdoor-job-scraper?fpr=1h3gvi) — Glassdoor listings with company ratings
- [Arbeitsagentur Scraper](https://apify.com/blackfalcondata/arbeitsagentur-scraper?fpr=1h3gvi) — Germany's official job portal (1M+ listings)
- [SEEK Scraper](https://apify.com/blackfalcondata/seek-scraper?fpr=1h3gvi) — Australia & NZ's largest job board
- [Naukri Scraper](https://apify.com/blackfalcondata/naukri-scraper?fpr=1h3gvi) — India's largest job portal

---


## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---

## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. [Sign up free](https://console.apify.com/sign-up?fpr=1h3gvi) — $5 credit included
2. Open the actor and paste your input
3. Click Start — results download as JSON, CSV, or Excel

Need more volume? [See pricing](https://apify.com/pricing?fpr=1h3gvi).

---

---

*Last updated: 2026-03-30*
