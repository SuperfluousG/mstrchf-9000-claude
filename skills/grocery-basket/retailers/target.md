# Target (target.com)

Tested live: no (read-only study, 10 Nov 2026)

| | |
|---|---|
| Market and currency | US, USD |
| Search | `https://www.target.com/s?searchTerm=<phrase>` |
| Add button | Visible text "Add to cart"; accessible label `Add <product name> to cart` |
| Own brand | Good & Gather; also Market Pantry (value) and Favorite Day (treats) |
| Basket | Header cart |
| Access from the UK | The site loaded and showed prices; it picked a default store (Cedar Rapids South, ZIP 52404) |

## Searching and adding

- Find the Add button by its accessible label, which carries the product name. Its test id is `chooseOptionsButton`, so pressing it may open a chooser (size, or Pickup / Same-day Delivery / Shipping) before the item goes in. Pick the option that matches how the user is shopping.
- Results can be filtered by how the order arrives: **Pickup**, **Same-day Delivery**, **Shipping**, **Shop in store**. For fresh food use the user's Pickup or Same-day Delivery choice; skip Shipping-only items.
- A price range ("$2.59 - $5.19") means the product comes in several sizes; choose the size in the chooser.
- Results include sponsored cards (a frozen zucchini fritter topped "zucchini").
- The header shows the store and ZIP. Use what is set; ask before changing it.

## Loose produce

None seen sold by weight. Fresh produce was sold by count or pack, with a unit price: "Fresh Organic Zucchini - 2ct, $3.19 ($1.60/count)", "Zucchini and Yellow Squash - 2ct, $2.99 ($0.15/ounce)". Choose the pack closest to the plan.

## Minimum basket and charges

From older Target and Shipt pages and 2026 guides: Same-day Delivery through Target needs a $35 minimum, with a $9.99 fee for non-members; Target Circle 360 members get free delivery on orders over $35. Same-day Delivery is fulfilled by Shipt. Read the actual fees in the cart.

## Substitutions

Not found. Check the user's existing setting in the cart and leave it.

## Not seen

- What the Add button opens and what it becomes after the first add.
- The cart line format and substitution control.
- The pickup or delivery window flow.
