# Avanti Print & Design — new storefront (v1)

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
