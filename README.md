# Shikoku Akiya Database (v1)

English-language static database of municipal akiya-bank listings in Kochi, Ehime and Tokushima (Shikoku, Japan), built for overseas buyers who cannot read the Japanese-only source sites.

## Contents
- `index.html` — self-contained static site (search + filters by prefecture / municipality / type / price, price & land-area sorting). Listing data is embedded as JSON, so it deploys as-is to GitHub Pages.
- `data/listings.json` / `data/listings.csv` — the dataset (341 records; v2, 2026-11-20).
- `tools/build.py` — generator. Re-running it rebuilds the JSON, CSV and HTML from the collected source data held in the script.

## Data model (per record)
`id, title_en, prefecture, municipality_en/ja, district_en/ja, type (sale_house/sale_land/rent_house/rent_land), price_jpy, price_usd_approx (¥155/$), rent_jpy_month, price_negotiable, land_area_m2, building_area_m2, layout, year_built, photo_url, bank_ref, summary_en, notes_en, source_name, source_url, detail_verified, fetched_at`

## Auto-update path (v2)
Same pattern as the stock meter / LWN: re-fetch the LIFULL list pages
(`https://www.homes.co.jp/akiyabank/chugoku/kochi/`, `.../ehime/`, `.../tokushima/`, 4–5 pages each),
parse listings, merge into `tools/build.py`'s dataset keyed by
(municipality, bank_ref, type), regenerate, and publish. Detail pages
(`https://www.homes.co.jp/akiyabank/b-<id>/`) add layout / building area / year built.

## Notes
- Summaries and caveats in English are generated per property from the source
  listing text plus a municipality profile — they are orientation, not a
  condition report. Always confirm on the source page before acting.
- Photos are hot-linked to the source CDN (LIFULL). If hot-linking becomes a
  problem, mirror the images and rewrite `photo_url`.
