# Canada411 Scraper: Canadian Phone Numbers, Names & Addresses (Reverse Address Lookup)

[![Run on Apify](https://img.shields.io/badge/Apify-Run%20the%20Actor-00A67E?logo=apify&logoColor=white)](https://apify.com/fayoussef/canada411-ca?fpr=youssef)
![Search](https://img.shields.io/badge/Search-name%20%7C%20address%20%7C%20URL-2ea44f)
![Reverse](https://img.shields.io/badge/Reverse-address%20lookup-1C7ED6)
![Language](https://img.shields.io/badge/Language-English%20%7C%20French-8B5CF6)
![Export](https://img.shields.io/badge/Export-JSON%20%7C%20CSV%20%7C%20Excel-F59E0B)

> ### ▶️ [Run the Canada411 Scraper on Apify](https://apify.com/fayoussef/canada411-ca?fpr=youssef)
> Scrape **Canada411.ca**, Canada's phone book, for the **name, phone number and address** of businesses and people. Search by name and city, **by street address** (reverse address lookup), or by URL.

**Canada411 Scraper** extracts contact data from Canada411.ca, Canada's largest online white pages and business directory. Give it a name and a city, a street address or a Canada411 URL, and it returns every matching listing across all result pages. It is built for B2B lead generation, sales teams, marketing agencies, recruiters and researchers. This repository documents the Apify Actor and gives working Python, JavaScript and cURL examples for calling it through the API.

- **Run it in the browser:** [fayoussef/canada411-ca on Apify](https://apify.com/fayoussef/canada411-ca?fpr=youssef)
- **Guide and docs:** [automationbyexperts.com/apify/canada411-ca](https://automationbyexperts.com/apify/canada411-ca)
- **Actor ID for the API:** `fayoussef/canada411-ca`

## What the Canada411 scraper does

- **Business and people search**: type who (`dentist`, `plumber`, a person's name) and where (`Calgary`, `Toronto, ON`).
- **Reverse address lookup**: leave **Who / What** empty and put a street address in **Where** to get every phone line registered at that address, whatever name it is under.
- **Canada-wide or local**: leave **Where** empty for a national search.
- **Direct URLs**: paste Canada411 search URLs to control exactly what is scraped.
- **Every result page** is followed automatically.

## Output fields: what data you get

One row per listing:

| Field | Description |
|---|---|
| `name` | Full name of the person or business |
| `phone` | Phone number as listed on Canada411 |
| `address` | Street address with city, province and postal code |
| `source_url` | Canada411 profile page |

## Input

Search by name, by address, or by URL:

| Field | What it does |
|---|---|
| `what` | Name or business type, e.g. `dentist`. Leave empty for an address search |
| `where` | City, province or full street address |
| `start_urls` | Canada411 search URLs |
| `max_pages` | Result pages per search; leave empty for all |

## Use cases

- **B2B prospect lists**: doctors, lawyers, accountants, contractors by city.
- **Local service outreach**: cleaning, plumbing, HVAC and trades leads by region.
- **Reverse address lookup**: find the phone number registered at an address.
- **Skip tracing and data enrichment**: add phone numbers to a list of names or addresses.
- **Market research**: map professional services across Canadian cities.

Ready-made examples you can run in one click:

- [Find business phone numbers in Toronto](https://apify.com/fayoussef/canada411-ca/examples/find-business-phone-numbers-toronto?fpr=youssef): Looks up every plumber listed on Canada411 in Toronto and returns name, phone number and street address for each. Change the business type or the city and the same task becomes a local B2B calling list for any trade in any Canadian city. Output is clean CSV or JSON.
- [Look up people by name and city on Canada411](https://apify.com/fayoussef/canada411-ca/examples/lookup-people-by-name-canada411?fpr=youssef): Searches Canada411's residential listings for a surname in a city and returns each match with phone number and address. Skip tracers, genealogists and recruiters use it to find listed contacts without paying per lookup. Only what Canada411 publishes is returned.

## Quick start

### 1. In the browser (no code)

1. Open the Actor on Apify and click **Try for free**.
2. Type a name or business in **Who / What** and a city in **Where**, or leave **Who / What** empty and put a street address in **Where**.
3. Click **Start**, then download Excel, CSV or JSON from the **Output** tab.

### 2. Through the API

1. Create a free [Apify account](https://console.apify.com/sign-up?fpr=youssef) and copy your API token from [Settings > Integrations](https://console.apify.com/settings/integrations).
2. Set it as an environment variable: `export APIFY_TOKEN=...` (PowerShell: `$env:APIFY_TOKEN="..."`).
3. Edit [`input.json`](input.json) and run one of the examples below.

#### Python

```bash
pip install apify-client
python examples/python/run_actor.py
```

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("fayoussef/canada411-ca").call(run_input={'what': 'plumber', 'where': 'Toronto, ON', 'max_pages': 5})

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

#### JavaScript / Node.js

```bash
npm install apify-client
node examples/javascript/run_actor.mjs
```

```javascript
import { ApifyClient } from "apify-client";

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor("fayoussef/canada411-ca").call({
    "what": "plumber",
    "where": "Toronto, ON",
    "max_pages": 5
});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

#### cURL (plain HTTP)

Runs the Actor and returns the dataset items in one synchronous call:

```bash
curl -X POST "https://api.apify.com/v2/acts/fayoussef~canada411-ca/run-sync-get-dataset-items?token=$APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d @input.json
```

Synchronous calls time out after 300 seconds. For larger runs use the client libraries above, or start the run with `POST /v2/acts/fayoussef~canada411-ca/runs` and read the dataset when it finishes.

## Sample output

One record, from [`sample-output.json`](sample-output.json). Export the full dataset as JSON, CSV, Excel or HTML from the Apify Console, or read it through the API as shown above.

```json
{
  "name": "Alex Tremblay",
  "phone": "416-555-1234",
  "address": "123 Example St, Toronto, ON",
  "source_url": "https://www.canada411.ca/res/1234567890.html"
}
```

## Integrations and automation

- **Schedule it** weekly to keep a lead list up to date.
- **Send results** to Google Sheets, Airtable, Slack, a webhook, Make, Zapier or n8n with Apify integrations.
- **Use it from AI agents** through the Apify MCP server.

## FAQ

### Does Canada411 have an API?
No public API. This Actor is a Canada411 API alternative: one Apify API call returns structured JSON.

### How do I do a reverse address lookup on Canada411?
Leave **Who / What** empty and put the full street address in **Where** (civic number, street, city, province). Leave out apartment numbers.

### Why doesn't a person's name return anything?
Canada411 lists a phone line under whoever registered it, which is often someone else in the household. Search the address instead.

### Can I search the whole of Canada?
Yes. Leave **Where** empty for a national search.

### Can I scrape businesses by category and city?
Yes. Put the category in **Who / What** (e.g. `dentist`) and the city in **Where**.

### What output formats are available?
JSON, CSV, Excel, XML and JSONL from the Apify dataset, or through the API.

## Canada411 Scraper en français

Le **Canada411 Scraper** extrait les **noms, numéros de téléphone et adresses** de Canada411.ca, l'annuaire téléphonique canadien. Recherchez par nom et ville, **par adresse** (recherche inversée) ou par URL, et exportez les résultats en Excel, CSV ou JSON. [Essayer sur Apify](https://apify.com/fayoussef/canada411-ca?fpr=youssef).

## Pricing

Pay per use on Apify: you are charged per event (results produced), with no subscription to this Actor. The current rate is shown on the [Actor's Store page](https://apify.com/fayoussef/canada411-ca?fpr=youssef). Free-plan runs are capped; an [Apify plan](https://apify.com/pricing?fpr=youssef) unlocks full runs.

## Related scrapers by AutomationByExperts

- [Whop Content Rewards Scraper: Clipping Campaigns](https://github.com/automationbyexperts/whop-clipping-campaigns-scraper)
- [Bulk AI Image Generator: Nano Banana & GPT Image](https://github.com/automationbyexperts/bulk-ai-image-generator)
- [Bulk LLM Runner: ChatGPT, Claude & Gemini in Bulk](https://github.com/automationbyexperts/bulk-llm-runner)
- [AutoTrader.ca Scraper: Canada Car Listings, VIN & Dealers](https://github.com/automationbyexperts/autotrader-canada-scraper)
- [Spitogatos.gr Scraper: Greek Real Estate Listings](https://github.com/automationbyexperts/spitogatos-scraper)
- [Wallapop Scraper: Spain, France, Italy, Portugal & UK](https://github.com/automationbyexperts/wallapop-scraper)
- [Full catalog of our web scraping APIs](https://github.com/automationbyexperts/web-scraping-apis)

## Support

Questions, bugs or a custom scraper: open an issue here, use the Issues tab on the [Apify page](https://apify.com/fayoussef/canada411-ca?fpr=youssef), or email youssefarhan24@gmail.com.

## License

The example code in this repo is MIT licensed. The Actor itself runs on Apify under its own terms.
