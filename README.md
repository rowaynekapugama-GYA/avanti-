# Avanti Print & Design — new storefront (v1)

Open `index.html` in any browser. Everything runs client-side, no build step.

## What's in here
- `index.html` — the whole site: home, shop (all products + 14 category pages, search, sort, wallpaper sub-filters), product pages, cart drawer with quantity-tier pricing, about, contact + FAQ, blog, policy page stubs.
- `products.json` — the full catalogue (104 products, 14 categories) pulled from avantiprint.com.au, ready to load into whatever backend comes next.
- `assets/logo-trim.png` — the logo, trimmed for the header.

## Adding the remaining product photos
Only the pull-up banners, mailer boxes and shipping cartons have photos wired in (they came from the product pages). Wallpaper, cake toppers and the signage substrates show a placeholder.

Fastest fix: in WooCommerce go to **Products → Export**, tick "Images", and you'll get a CSV with an image-URL column per product. Paste those URLs into the `img` array for each product in `products.json` / the `PRODUCTS` block in `index.html`.

## Deliberately left for the next round
- Real variation pricing (sizes/materials currently show a base price and a "final price by size" note)
- Delivery options and checkout/payment
- Artwork upload on the product page
- Terms, privacy and returns copy (stubs are in place)
