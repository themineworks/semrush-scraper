# Semrush Scraper: Authority Score, Backlinks & Traffic

Get Semrush Authority Score, backlink count, referring domains, and estimated organic traffic for any domain, pulled from Semrush's own free Website Authority Checker. Includes up to 13 months of historical trend, top pages, and up to 5 organic competitors. No Semrush account, login, or paid API required.

**Run it on Apify:** [apify.com/themineworks/semrush-scraper](https://apify.com/themineworks/semrush-scraper)
**Docs, FAQ and pricing:** [themineworks.com/actors/semrush-scraper](https://themineworks.com/actors/semrush-scraper/)

**Price:** From $9.00 per 1,000 domains on Apify's higher plans ($15.00 on the free plan), plus a $0.005 start fee per run. Failed and empty results are never charged.

## What it returns

* Authority Score (1-100) with trend
* Backlink count and referring domains with trend
* Estimated monthly organic traffic
* Up to 13 months of historical trend data
* Top pages and up to 5 organic competitors
* Blocked or failed checks are never charged

## Quick start

You need a free [Apify account](https://console.apify.com/sign-up) and its API token (Settings, API & Integrations).

### Python

```bash
pip install apify-client
```

```python
from apify_client import ApifyClient

client = ApifyClient("YOUR_APIFY_TOKEN")
run = client.actor("themineworks/semrush-scraper").call(run_input={
    "domains": [
        "hubspot.com"
    ],
    "maxDomains": 1
})

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

### Node.js

```bash
npm install apify-client
```

```javascript
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: 'YOUR_APIFY_TOKEN' });
const run = await client.actor('themineworks/semrush-scraper').call({
    "domains": [
        "hubspot.com"
    ],
    "maxDomains": 1
});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

### cURL

One request that runs the actor and returns the results in the response (for runs under 5 minutes):

```bash
curl -X POST "https://api.apify.com/v2/acts/themineworks~semrush-scraper/run-sync-get-dataset-items?token=YOUR_APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"domains": ["hubspot.com"], "maxDomains": 1}'
```

### Command line

This repo includes ready-made clients that save results to JSON and CSV:

```bash
python3 semrush_scraper.py --token YOUR_APIFY_TOKEN --domains "hubspot.com" --max-domains "1"
node semrush_scraper.mjs --token YOUR_APIFY_TOKEN --domains "hubspot.com" --max-domains "1"
```

## Input

| Field | Type | Default | Description |
|---|---|---|---|
| `domains` (required) | array |  | Website domains to look up on Semrush's free Website Authority Checker (for example "hubspot.com") |
| `maxDomains` | integer | `20` | Safety cap on how many domains from the list above are actually checked in one run |

## Output

One row per result, as JSON, CSV, Excel or through the API.

| Field | Type | Description |
|---|---|---|
| `domain` | string | The domain that was checked |
| `data_as_of` | string | Date Semrush's data snapshot is dated (Authority Scores refresh roughly every two weeks) |
| `authority_score` | number | Semrush Authority Score, 1-100 |
| `authority_score_change_pct` | number | Authority Score change vs |
| `backlinks` | number | Total backlinks pointing to the domain |
| `backlinks_change_pct` | number | Backlink count change vs |
| `referring_domains` | number | Number of unique referring domains |
| `referring_domains_change_pct` | number | Referring domain count change vs |
| `organic_traffic_monthly` | number | Semrush's estimated monthly organic search traffic |
| `organic_traffic_change_pct` | number | Organic traffic change vs |
| `health_label` | string | Semrush's qualitative label for the backlink profile's health (for example "Very good") |
| `link_power_score` | number | Sub-score: strength/quality of the backlink profile |
| `natural_profile_score` | number | Sub-score: how natural (non-manipulated) the backlink profile looks |
| `organic_traffic_score` | number | Sub-score: organic traffic's contribution to the Authority Score |
| `top_pages_by_backlinks` | array | Up to 5 pages on the domain with the most raw backlinks |
| `most_linked_pages` | array | Up to 5 pages on the domain with the most unique referring domains |
| `top_competitors` | array | Up to 5 competing domains with their own Authority Score and shared organic keyword count |
| `authority_score_history` | array | Up to 13 months of historical Authority Score snapshots |
| `checked_at` | string | ISO-8601 timestamp when this record was scraped |

## Use it from an AI agent

The actor works as a tool in Claude, Cursor or any MCP client through Apify's MCP server:

```
https://mcp.apify.com/?tools=themineworks/semrush-scraper
```

## FAQ

### Do I need a Semrush account or subscription?

No. This reads the same free Website Authority Checker tool Semrush publishes for anyone to use. No login, no paid Semrush seat, no API key.

### What is Semrush Authority Score?

A 1-100 score Semrush calculates from a domain's backlink profile and organic search visibility. It's one of the more commonly cited domain-strength metrics in SEO, used as a quick proxy for site authority.

### Does it return backlink data, not just the score?

Yes. Total backlinks, referring domain count, and their recent trend direction come back alongside the Authority Score, plus a domain's top pages by backlinks and referring domains.

### Can I see competitors for a domain?

Yes. Up to 5 organic competitors are returned with their own Authority Scores and the number of keywords they share with the target domain.

### What does it cost?

Pay per result: from $9.00 per 1,000 domains on Apify's higher plans, $15.00 on the free plan, plus a $0.005 start fee per run. Blocked, rate-limited, or failed checks are never charged.

### Can I export the results to CSV or Excel?

Yes. Every run saves to an Apify dataset you can download as JSON, CSV, Excel or XML, or read through the API. The Python and Node clients in this repo also write the results to local files.

### Can I run it on a schedule?

Yes. Save your input as a task on Apify and attach a schedule, or call the API from your own cron job. Scheduled runs are billed the same way as manual ones.

## Related scrapers

* [Similarweb Scraper](https://themineworks.com/actors/similarweb-scraper/): Website traffic, rank, and channel mix, no Similarweb login
* [Backlink Building Agent](https://themineworks.com/actors/backlink-building-agent/): 3-stage pipeline: discover, contact, draft. Pay per outcome
* [ASO Keyword Rank Tracker](https://themineworks.com/actors/aso-keyword-rank-tracker/): App Store and Google Play rank tracking, one dataset

Part of [The Mine Works](https://themineworks.com/): 151 pay-per-result scrapers with no login and no browser setup on your side.

## License

MIT © The Mine Works
