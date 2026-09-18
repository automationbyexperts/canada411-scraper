# Canada411 Scraper: Business Phones, Addresses

Our canada411.ca scraper effortlessly gathers URLs from all pages and extracts contact information from each listing.

This repo shows how to call the [Canada411 Scraper: Business Phones, Addresses](https://apify.com/fayoussef/canada411-ca?fpr=youssef) Apify Actor from your own code: a Python and a JavaScript example, the input they send, and a sample of the output. Everything runs in the Apify cloud, so there is nothing to host, scale or maintain on your side.

- **Run it in the browser:** [fayoussef/canada411-ca on Apify](https://apify.com/fayoussef/canada411-ca?fpr=youssef)
- **Guide and docs:** [automationbyexperts.com/apify/canada411-ca](https://automationbyexperts.com/apify/canada411-ca)
- **Actor ID for the API:** `fayoussef/canada411-ca`

## Use cases

- [Find business phone numbers in Toronto](https://apify.com/fayoussef/canada411-ca/examples/find-business-phone-numbers-toronto?fpr=youssef): Looks up every plumber listed on Canada411 in Toronto and returns name, phone number and street address for each. Change the business type or the city and the same task becomes a local B2B calling list for any trade in any Canadian city. Output is clean CSV or JSON.
- [Look up people by name and city on Canada411](https://apify.com/fayoussef/canada411-ca/examples/lookup-people-by-name-canada411?fpr=youssef): Searches Canada411's residential listings for a surname in a city and returns each match with phone number and address. Skip tracers, genealogists and recruiters use it to find listed contacts without paying per lookup. Only what Canada411 publishes is returned.
- [Reverse address lookup on Canada411](https://apify.com/fayoussef/canada411-ca/examples/reverse-address-lookup-canada411?fpr=youssef): Leave the name empty and put a full street address in Where to get everyone Canada411 lists at that address, with their phone numbers. Property managers, process servers and door to door teams use it to know who is listed at a building before they visit.

## Quick start

1. Create a free [Apify account](https://console.apify.com/sign-up?fpr=youssef) and copy your API token from [Settings > Integrations](https://console.apify.com/settings/integrations).
2. Set it as an environment variable: `export APIFY_TOKEN=...` (PowerShell: `$env:APIFY_TOKEN="..."`).
3. Edit [`input.json`](input.json) and run one of the examples below.

### Python

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

### JavaScript / Node.js

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

### cURL (plain HTTP)

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

## Pricing

Pay per use on Apify: you are charged per event (results produced), with no subscription to this Actor. The current rate is shown on the [Actor's Store page](https://apify.com/fayoussef/canada411-ca?fpr=youssef). Free-plan runs are capped; an [Apify plan](https://apify.com/pricing?fpr=youssef) unlocks full runs.

## More Actors by AutomationByExperts

- [Whop Content Rewards Scraper: Clipping & UGC Campaigns](https://github.com/automationbyexperts/whop-clipping-campaigns-scraper)
- [thebluebook.com Scraper](https://github.com/automationbyexperts/thebluebook-scraper)
- [Bulk AI Image Generator (NO API KEY)](https://github.com/automationbyexperts/bulk-ai-image-generator)
- [Bulk LLM Runner GPT, Claude, Perplexity, Kimi (No API Key)](https://github.com/automationbyexperts/bulk-llm-runner)
- [AutoTrader Canada Car Scraper: Prices, VIN, Mileage & Dealers](https://github.com/automationbyexperts/autotrader-canada-scraper)
- [Spitogatos.gr Scraper: Greek Property Listings & Agent Phones](https://github.com/automationbyexperts/spitogatos-scraper)
- [Full catalog of our web scraping APIs](https://github.com/automationbyexperts/web-scraping-apis)

## Support

Questions, bugs or a custom scraper: open an issue here, use the Issues tab on the [Apify page](https://apify.com/fayoussef/canada411-ca?fpr=youssef), or email youssefarhan24@gmail.com.

## License

The example code in this repo is MIT licensed. The Actor itself runs on Apify under its own terms.
