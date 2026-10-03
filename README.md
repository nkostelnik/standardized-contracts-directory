# Standardized Contracts Directory

A single-page, jurisdiction- and category-tagged register of widely-used **standardized contracts** — jointly-drafted, openly-licensed paper that a whole market negotiates from, not one party's take-it-or-leave-it "standard contract."

Covers cover-page templates (Bonterms, Common Paper, oneNDA), regulator-issued instruments (EU SCCs, UK IDTA), and industry-association forms (ISDA, FIDIC, AIA, ACORD, and more), with search, filters, and sorting.

Also includes a small easter egg: pick your favorite NHL team from the "Change the Look" section and the whole page recolors to match.

## Running locally

This is a static page (`index.html`) that loads its data from `contracts.json`, with no build step and no dependencies. Because the page fetches that file, serve the folder over HTTP rather than opening `index.html` directly:

```bash
# any static file server works, e.g.:
npx serve .
# or
python3 -m http.server
```

## Data

Every standard is one entry in [`contracts.json`](contracts.json), checked against [`contracts.schema.json`](contracts.schema.json) (JSON Schema 2020-12). To add a standard, append an object with these fields:

| Field | Type | Notes |
| --- | --- | --- |
| `name` | string | Display name |
| `publisher` | string | Who publishes or maintains it |
| `category` | string[] | First entry is the primary category used for grouping |
| `jurisdiction` | string[] | Any of `US`, `UK`, `EU`, `Global` |
| `year` | integer | First published or last revised |
| `access` | string | `free`, `membership`, or `paid` |
| `license` | string | Short label shown on the card |
| `blurb` | string | One or two sentences |
| `url` | string | Official source link |

To validate your changes:

```bash
npx ajv-cli validate --spec=draft2020 -s contracts.schema.json -d contracts.json
```

## Deploying

Ready to deploy as-is to Vercel, Netlify, GitHub Pages, or any static host — no build command needed.
