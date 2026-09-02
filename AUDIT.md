# Live-site cross-reference audit — artwork products
*Run against avantiprint.com.au · September 2026 round*

## How this was checked
Pull-up banners (category + product page) and corflute custom dimensions were re-fetched
live this round. The remaining categories were checked against the option/price data
scraped from the live store when this rebuild was first built, plus the site-wide
behaviour confirmed on the pages fetched live (the artwork-supply widget is the same
WooCommerce component on every artwork product).

## Verified correct — no gaps
| Category | Checked | Result |
|---|---|---|
| Pull-up banners ×4 | live fetch | Quantity tier boundaries and prices match exactly (Std 1/3/6/16+ · Prem &amp; DS 1/5/15/30+). 850 × 2000 mm print face confirmed. |
| Mailer boxes / shipping cartons | earlier scrape | Material, size (per dieline) and printed/blank options present; per-size pricing matches. |
| A-frames | earlier scrape | Style + size options present with correct price range. |
| Foam PVC | earlier scrape | Size + thickness options present. |
| Enviroboard, foamboard, floor decals, posters, window graphics (standard products) | earlier scrape | Size/stock/type/shape options present. |
| Wallpaper, cake toppers | n/a | Customer-artwork upload does not apply (wall dimensions / personalisation already captured). |

## Gaps found → fixed this round
| Product | Gap vs live | Fix |
|---|---|---|
| Corflute Signs | Live variants include **thickness (3/5 mm)** and **eyelets**; we only had size + sides | Added Thickness and Eyelets (none / corners / centre-top) options |
| Corflute – Custom Dimensions | Live has **material combos (3/5 mm × single/double)**, **eyelets**, and **Width/Height (mm) inputs, max 1200 × 2400** | Added all three; width/height now required at add-to-cart with max validation; copy updated with contour cutting + turnaround |
| ACM / Foamboard – custom | No width/height capture | Added Width/Height mm inputs (max 1200 × 2400) |
| Posters / Window graphics / Floor decals – custom | No width/height capture | Added Width/Height mm inputs |
| Pull-up banners ×4 | Live has the full **artwork-supply flow**: print-ready upload (32 MB) *or* design-assistance package chooser, plus artwork template PDFs | Built in full, with live mockup preview, DPI check and cart integration (this round's Task 2) |

## Known remaining gaps (next rounds)
- **Artwork upload on non-banner products** — the live site's upload/design-package widget
  exists on every artwork product (corflute, A-frames, ACM, posters, etc.). The new studio
  component is built to be reusable; rolling it out with a flat-panel mockup is next.
- Live per-variant pricing for the new corflute thickness/eyelet combinations is quoted
  after order in our static build (base price shown, "final price by size" note) — real
  variant price tables can be scraped in a future round.
