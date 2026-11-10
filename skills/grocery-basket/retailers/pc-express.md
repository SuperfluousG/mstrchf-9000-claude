# PC Express (Loblaw banners)

Tested live: no (read-only study, 10 Nov 2026)

PC Express is Loblaw's online ordering, run on each banner's own site. pcexpress.ca only asks the user to choose a store, then sends them to a banner: loblaws.ca, realcanadiansuperstore.ca (superstore.ca), nofrills.ca, zehrs.ca, fortinos.ca, provigo.ca, maxi.ca, atlanticsuperstore.ca and others. Use this guide on whichever banner the user is signed in to.

| | |
|---|---|
| Market and currency | Canada, CAD |
| Search | `https://www.<banner domain>/en/search?search-bar=<phrase>` (studied on loblaws.ca; the site adds `storeId` and `cartId` to the URL). French pages use `/fr/`. |
| Add button | `Add <product name> to cart`, where the label **leaves out the brand** |
| Own brand | President's Choice (PC); No Name (value) |
| Loyalty | PC Optimum. Never type a PC Optimum number. |
| Basket | "N items in cart, click to review cart" in the header |
| Access from the UK | loblaws.ca loaded and showed prices; it picked a default store (Loblaws Ogilvie Road) |

## Searching and adding

- The Add label drops the brand: the card "No Name Naturally Imperfect Zucchini" has the button `Add Naturally Imperfect Zucchini to cart`. Two cards can share a short label (loose "Zucchini" and another brand's "Zucchini"), so check the card's brand, size and price before clicking.
- Results include sponsored cards (peanut butter and rice topped "zucchini").
- The header shows the store and the next delivery and pickup times. Use what is set; ask before changing it.

## Loose produce

Loose produce shows an estimated price and both metric and imperial unit prices: "about $1.85 — Zucchini — $6.61/1kg, $3.00/1lb". Add by count. Packs show a count price instead: "Organic Green Zucchini 2x1.0 ea, $3.00/1ea".

## Prices and units

Packed goods show the size and a price per 100 g ("1.02 kg, $0.78/100g"). Plans in metric or imperial both work: Canadian pages show both for produce.

## Minimum basket and charges

Each banner has a fees page at `https://www.<banner domain>/pc-express-fees` (linked from pcexpress.ca). Third-party guides report no order minimum, with pickup and delivery fees by slot, and a PC Express Pass that waives fees on orders of $35 or more. Read the actual fees in the cart.

## Not seen

- Signed-in behaviour: what the Add button becomes after the first add, and the cart line format.
- The substitution setting (not found in help pages either).
- The pickup or delivery slot flow.
