# Michelin Scraper

Python scraper for collecting Michelin Guide restaurant data for one country at a time and exporting the result as CSV.

The scraper reads country metadata from `countries/Countries.json`, crawls Michelin Guide listing pages, follows each restaurant detail page, and writes a normalized CSV under `results/`. HTML responses are cached locally so repeated runs do not re-fetch every page.

## Repository Layout

- `scraper.py` - command-line entry point.
- `countries/` - supported country labels, shortcodes, and country lookup helpers.
- `web_crawler/` - crawler, page cache, restaurant model, and HTML processors.
- `requirements.txt` - direct runtime dependencies.
- `requirements.lock.txt` - resolved dependency snapshot for the local `.venv`.
- `cached_countries/` - local HTML cache, ignored by Git.
- `results/` - generated CSV output, ignored by Git.

## Local Setup

```bash
source .venv/bin/activate
python --version
pip install -r requirements.lock.txt
```

If `.venv` is missing:

```bash
uv venv --python 3.12
source .venv/bin/activate
uv pip install -r requirements.lock.txt
```

## Usage

```bash
python scraper.py --country "Luxembourg"
```

The country name must exist in `countries/Countries.json`. Output is written to:

```text
results/<country-shortcode>.csv
```

## Notes

- The crawler includes a small delay between requests to reduce throttling risk.
- Cached HTML and generated CSV files are intentionally excluded from Git.
- The output format is useful for import into tools such as Google My Maps.
