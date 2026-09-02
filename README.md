# Avanti Print & Design — new storefront (v1)

## Changelog — studio rollout to corflute & A-frames + modern restyle
- **Artwork studio now on corflute and A-frame product pages** using the flat-panel
  mockup: tilted board with a fluted edge for corflute, a framed insert with legs for
  A-frames. The print size is live — corflute follows the selected A-size or the custom
  width/height inputs (aspect ratio and DPI recalculate on change), A-frames parse the
  size option's mm. Corflute gets Front/Back tabs (back = double-sided orders, no
  auto-copy); A-frames get Side A/Side B with one-file-both-sides auto-copy.
- **Modern UI pass**: card elevation with gradient hairline, 1-2-3 step chips that light
  as you progress, icon dropzone with hover/drag micro-interactions, pill segmented
  controls, spotlight stage backdrop, pulsing low-DPI warning.
- Hero "Upload your design" CTAs for corflute and A-frames now land on fully working
  upload studios.

## Changelog — hero slider promotes signage trio
Hero now promotes **Corflute Signs, Pull Up Banners and A-Frame Signs** with supplied
mockup images (hot-linked from imgur for now) and per-product copy, replacing the old
generic tagline. Each slide has two CTAs: **Shop now** (category page) and **Upload your
design** (product page; on the banner it deep-links via `?studio` and auto-scrolls to the
artwork studio). Note: the studio currently exists only on banner pages, so the corflute
and A-frame upload buttons land on their product pages — they'll light up fully when the
studio rolls out to flat signage next round. Consider replacing the imgur hot-links with
files in `assets/` so the hero doesn't depend on a third-party image host.

## Changelog — real delivery pricing + angled banner mockup
- **Delivery pricing wired in from the live WooCommerce table rates** (per client screenshots):
  Cake Toppers standard $13 / express $20; Banner Stands Metro NSW $30 / Regional NSW $50;
  Corflute Metro NSW $40 / Regional NSW $100. Costs are summed per option when multiple
  classes are in the cart (matching the Woo "Sum" rate calculation), the cart shows a
  per-class delivery estimate, product pages show category-accurate delivery lines, and
  NSW courier items carry the "our team will contact to confirm delivery details" note.
  Shipping classes are exported in `products.json` under `shipping`. Other categories
  still show "quoted at checkout" — send their rates through and they slot straight in.
- **Banner mockup restyled to a 3D angled view** (like a product mockup photo): perspective
  tilt, artwork running edge-to-edge under a clamping top rail, lighting sheen across the
  face, roller base with feet (black on premium), soft floor shadow. Drag/zoom unchanged.

## Changelog — artwork audit + banner artwork studio (this round)
**Task 1 — live-site cross-reference audit.** Every artwork-supply category was checked
against avantiprint.com.au (banners and corflute re-fetched live; the rest against the
original scrape). Findings and fixes are in **AUDIT.md**. Fixed in this round: corflute
thickness + eyelet options on both corflute products, live-parity material combos on the
custom product, and width/height (mm) capture on **all six custom-dimension products**
(corflute and ACM/foamboard enforce the live 1200 × 2400 mm maximum at add-to-cart).

**Task 2 — artwork upload + live preview on the four pull-up banner pages.**
- Drag-and-drop / click upload (JPG, PNG, WebP preview instantly; PDF accepted with a
  "print-ready PDF received" state; 32 MB cap as on the live store)
- Live banner mockup — rail, 850 × 2000 mm print face, pole and roller base (black base
  on premium models) — with drag-to-reposition, zoom slider, fill/fit toggle and a
  dashed "keep text inside" safe-area overlay
- Print-quality check: effective DPI at print size with a badge (140+ excellent · 95+
  good · 70+ acceptable · below 70 too low) and plain-language guidance
- Double-sided models take front/back uploads with a side switcher; one file = printed
  both sides (matches the live FAQ)
- Live-parity supply choice: print-ready files **or** design assistance (Pack 1 free /
  Pack 2 $49 + GST) plus the two artwork-template PDF downloads
- Artwork attaches to the cart line (filename, pixels, DPI verdict, layout) and shows in
  the cart drawer; "order now, supply artwork later" unlocks add-to-cart without a file
- Everything stays client-side (object URLs) — no backend

**Rolling out to other products:** the studio is a reusable component (`artStudioHTML` /
`artStudio` + `BANNER_CFG`); next round points it at A-frames and corflute with a flat
panel mockup (portrait/landscape) instead of the banner rig.

Open `index.html` in any browser. Everything runs client-side, no build step.

## What's in here
- `index.html` — the whole site: home, shop (all products + 14 category pages, search, sort, wallpaper sub-filters), product pages, cart drawer with quantity-tier pricing, about, contact + FAQ, blog, policy page stubs.
- `products.json` — the full catalogue (104 products, 14 categories) pulled from avantiprint.com.au, ready to load into whatever backend comes next.
- `assets/logo-trim.png` — the logo, trimmed for the header.
- `assets/favicon.ico`, `icon-192.png`, `apple-touch-icon.png`, `avanti-favicon-512.png` — the browser/tab and home-screen icons, all generated from the supplied 512px mark.
- `assets/products/` — product photos supplied directly (rather than pulled from the live site).

## Product photos — current coverage
**All 104 products and all 14 category tiles now have real photography.**

Images come from two places:
- **Local files in `assets/products/`** — photos supplied directly. These are bundled in the repo, so they keep working regardless of the old WooCommerce site.
- **Hot-linked from `avantiprint.com.au/wp-content/uploads/...`** — mostly the extra gallery shots (close-ups and artboards) that sit behind the main image.

Any image URL that fails falls back automatically to the branded placeholder tile (see `imgFail` in `index.html`), so a broken image never appears.

### How wallpaper images work
Each wallpaper design on the live site has up to three shots: `Complete-Wall-Design-N`, `Close-Up-Design-N` and `Original-Artboard-Design-N`. Two things to know:
- The trailing `-1` / `-2` is **part of the design identity, not a duplicate marker** — `Design-4`, `Design-4-1` and `Design-4-2` are three completely different artworks. Some numbers carry three separate designs.
- To wire a wallpaper up, add to its row in the `WP` array: the design number as the sixth field, then an array of image paths as the seventh. `WP_TRIO(n, suffix)` builds the three live-site URLs (pass `0` for no suffix).

### Replacing an image later
- **Wallpaper** — edit the seventh field of its `WP` row.
- **Cake topper** — add an entry to the `CT_LOCAL` map; otherwise the filename is derived as `{Name}-Topper.jpg`.
- **Signage / packaging** — edit the relevant `IMGS_*` / `POSTER_IMGS` / `WG_IMGS` constant near the top of the data block.

Then regenerate `products.json` (it's built from the same data) if you're using it.

### A note on image quality
Many of the supplied wallpaper files are the WordPress `480x600` thumbnail rather than the full-size original. They look fine on the shop cards but are a little soft on the large product-page image. Where a thumbnail was supplied, the full-size URL is already included as the next gallery image, so swapping in the originals later is straightforward.

## Deliberately left for the next round
- Real variation pricing (sizes/materials currently show a base price and a "final price by size" note)
- Delivery options and checkout/payment
- Artwork upload on the product page
- Terms, privacy and returns copy (stubs are in place)


## Left for next round
- Roll the artwork studio out to A-frames, corflute and other flat signage (panel mockup)
- Real per-variant pricing for corflute thickness/eyelet combos and other size-priced options
- Delivery options and a checkout/payment flow
- Real policy-page copy; upgrade 480×600 wallpaper thumbnails to full-size originals
- Minor copy fixes (Garden Greens, Grey Artistic Strokes descriptions)
