AI x Law Hackathon

Project Injenium is a federal bill monitoring and client impact prototype.

The project starts with LEGISinfo bill metadata in JSON, ranks bills by likely client relevance, retrieves official bill text XML, and keeps the data easy to refresh when new bills appear.

## Current Data Files

```text
data/raw/legisinfo/45-1/bills.json
```

Raw LEGISinfo bill inbox for the 45th Parliament, 1st session.

```text
data/normalized/bills.45-1.json
```

Normalized bill list sorted by latest activity date.

```text
data/normalized/recommended-bills.45-1.json
```

High-priority bills scored for demo/client relevance.

```text
data/bills/45-1/
```

Official Parliament bill text for the recommended bills. Each bill folder contains source metadata, official XML, and normalized JSON for app/search/AI use.

```text
data/laws/food-and-drugs-act/
```

Current consolidated Food and Drugs Act from Justice Laws, stored as official XML and normalized JSON. This is the first current-law baseline for bill-to-law comparison.

```text
data/clients/demo/
```

Three fake client profiles for demo impact analysis.

## Update Flow

When new bills show up:

1. Download the latest JSON from:

```text
https://www.parl.ca/legisinfo/en/bills/json?parlsession=45-1
```

2. Replace:

```text
data/raw/legisinfo/45-1/bills.json
```

3. Regenerate the normalized/recommended JSON using the same scoring rules described in `data/README.md`.

4. Retrieve the actual text for the recommended bills:

```text
node --use-system-ca scripts/retrieve-bill-texts.mjs
```

5. Refresh a current law baseline:

```text
node --use-system-ca scripts/retrieve-law.mjs food-and-drugs-act
```

The app should use JSON for bill metadata. For actual bill text and current laws, retrieve official XML, then convert it into normalized JSON.
