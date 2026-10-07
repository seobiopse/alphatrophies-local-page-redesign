# Alpha Trophies: State and City local pages (draft for review)

First pair of the State → City page set Tom asked for (VIC, NSW, SA only).

| Page | File | Canonical URL |
|---|---|---|
| State: Victoria | `trophies/victoria/index.html` | `https://alphatrophies.com.au/trophies/victoria/` |
| City: Melbourne | `trophies/victoria/melbourne/index.html` | `https://alphatrophies.com.au/trophies/victoria/melbourne/` |

Preview locally (links use clean folder URLs, so serve over HTTP):

```bash
python -m http.server 8765
# open http://localhost:8765/trophies/victoria/
```

## Internal link map

State → City
- State page "Find trophies near you" grid links to `melbourne/`
- State hero button "Melbourne store & directions" → `melbourne/`
- State store block "See how to find us" → `melbourne/#how-to-find-us`
- State footer strip "Browse: Melbourne" → `melbourne/`

City → State
- City breadcrumb "Victoria" → `../`
- City bottom bar "All Victoria trophies" → `../`

Rule: a city appears as a link on its state page only when that city page exists. Unbuilt cities (Geelong, Ballarat, Bendigo) are plain "Coming soon" text, so nothing links to a 404. NSW and SA hub links are added when those pages are published.

## Where each part of a page comes from

| Section | Source | Unique per page? |
|---|---|---|
| Header, nav, footer, store addresses, phone, hours, ABN | Live alphatrophies.com.au | Common (keep small) |
| Delivery, pickup and rush pricing | Live `/delivery-information` (updated 18 Sep 2026) | Common facts, reworded per page |
| Product names, prices, images, URLs | Live category pages (Product JSON-LD) | **Unique set per page** (see below) |
| Directions, drive times, landmarks | Google Maps (store at -37.68788, 145.0257629) | Unique to the city |
| Suburb guide | Suburb list from `Top towns and suburbs.xlsx` | Unique to the city |
| Customer logos | Live `/about-us` | Common |
| FAQ | Written per page; visible text matches FAQPage schema | Unique per page |

## Product cards: how to keep them unique across pages

- State page uses category tiles (6 categories, representative image, "From $x" taken from the cheapest item in that live category).
- City page uses 8 specific products, none of which repeat the state-page tile images.
- Next city/state: choose a different local-sport mix (for example NSW leans rugby league and union; SA leans AFL and netball) and pick different products from the same live category lists. Never reuse the same 8.
- Prices are the listed price on the live category pages when built. Re-pull before publishing.

## Common vs unique content (quality)

Header, footer, nav and the trust bar repeat across all pages. That is normal and does not hurt quality, as long as the main body is unique. Keep the repeated parts small and keep at least the hero copy, store and directions block, suburb guide, product set and FAQ distinct on each page.

## For Tom to confirm before publishing

1. Rating and review count (232) in the trust bar. The live site shows both "232" and "200+" in different places.
2. Whether any in-stock items can be collected the same day. The live Adelaide page says "same-day pickup on in-stock lines"; the delivery policy says 5 working days. These pages promise only the policy.
3. Whether metro Melbourne is one carrier delivery zone (pages say timing is the same across metro).
4. Directions: check each direction card against live Google Maps (exit names, turns).
5. Parking at Unit 11 (not mentioned on the page).
6. Brisbane page currently shows the Thomastown address and schema, and the store schema longitude on live pages is wrong (145.0097; correct value is 145.0257629).
7. Thomastown address format: "11/8–20 Brock Street" here vs "Factory 8/5 Brock St" in one live footer.

## Before go-live

- Remove the `review-banner` div from both pages.
- Add the 301 redirect `/buy-trophies-in-melbourne` → `/trophies/victoria/melbourne/`.
- Add both URLs to the sitemap (`sitemap-local.xml`).
- Self-host or defer Font Awesome and Google Fonts if page speed matters.
- Request indexing in Search Console after the pages are live.

## Git

```bash
git init
git add .
git commit -m "Add Victoria state page and Melbourne city page (draft)"
```
