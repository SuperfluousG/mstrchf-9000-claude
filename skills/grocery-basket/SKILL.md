---
name: grocery-basket
description: Fill an online grocery basket from a MSTRCHF 9000 basket file or pasted "Order with Claude" instructions, in the user's own signed-in browser. Has guides for Tesco, Sainsbury's, Asda, Ocado, Morrisons (UK), Walmart, Kroger, Amazon Fresh, Target, Albertsons (US), PC Express, Walmart Canada, Voilà and Metro (Canada), and a method for any other online grocer. Use when the user asks to order, shop or fill the basket for a MSTRCHF 9000 week, including instructions that name the older tesco-basket skill. Stops before delivery-slot booking and checkout for the user to confirm.
---

# Grocery basket from a MSTRCHF 9000 plan

MSTRCHF 9000 plans the week and writes a basket: one entry per ingredient with a search phrase, the amount the recipes need, and the packs to buy. Your job is to put those items into the user's basket at their online grocer, in their own browser, then hand back to them.

## Input

Either the pasted "Order with Claude" instructions, or a `mstrchf-basket-<week>.json` file. If the user asks you to order the week without either, ask them to open the planner's Shop page and press **Order with Claude → Copy order instructions**: the pack sizes come from the planner.

The file (version 2) looks like this:

```json
{ "app": "MSTRCHF 9000", "format": "basket", "version": 2,
  "market": "us", "retailer": "walmart", "retailerName": "Walmart", "currency": "USD",
  "weekId": "2026-11-16", "week": "16–22 Nov", "people": 2,
  "meals": ["Smoky chicken fajitas", "Zucchini ribbon pasta"],
  "items": [ { "id": "zucchini", "name": "Zucchini", "search": "zucchini", "aisle": "Produce",
               "need": "1 lb", "buy": [{ "size": "1 lb", "count": 1 }], "estPrice": 1.42,
               "usedIn": ["Zucchini ribbon pasta"] } ],
  "alreadyHave": ["Olive oil"], "estTotal": 61.2, "createdAt": "2026-11-15T18:00:00Z" }
```

- `market` is `uk`, `us` or `ca`. `currency` is `GBP`, `USD` or `CAD`.
- `name`, `search`, `need` and `size` are already in that market's own words and units ("Zucchini", "1 lb" in the US; "Courgette", "500g" in the UK). Search with them as given.
- `retailer` names the shop and its guide (table below). `retailer: null` means the user hasn't picked one: use the grocery site the user has open in their browser, or ask which shop to use.
- **Version 1 files** (`"version": 1`, no `market`) are Tesco-only. Treat them as `market: "uk"`, `retailer: "tesco"`, `currency: "GBP"`.

Pasted instructions name the shop in their first line ("Please fill my Tesco groceries basket…") and list the items as JSON with `name`, `search`, `buy`, `need` and `estPrice`. Older instructions ask for the `tesco-basket` skill; this skill replaces it. Work through the items in the order given: the planner sorts them by aisle.

## Pick the guide

Each shop has a guide in `retailers/<retailer>.md` next to this file. Read it before the first search. If `retailer` is null, match the domain of the user's open grocery tab against the Sites column.

| `retailer` | Shop | Sites | Market | Tested live |
|---|---|---|---|---|
| `tesco` | Tesco | tesco.com | uk | yes, 2 runs, Nov 2026 |
| `sainsburys` | Sainsbury's | sainsburys.co.uk | uk | no |
| `asda` | Asda | asda.com | uk | no |
| `ocado` | Ocado | ocado.com | uk | no |
| `morrisons` | Morrisons | groceries.morrisons.com | uk | no |
| `walmart` | Walmart | walmart.com | us | no |
| `kroger` | Kroger and its banners | kroger.com, ralphs.com, fredmeyer.com, kingsoopers.com and others | us | no |
| `amazon-fresh` | Amazon Fresh | amazon.com | us | no: **read its guide first; do not drive the site** |
| `target` | Target | target.com | us | no |
| `albertsons` | Albertsons and its banners | albertsons.com, safeway.com, vons.com, jewelosco.com and others | us | no (study blocked) |
| `pc-express` | PC Express (Loblaw banners) | loblaws.ca, realcanadiansuperstore.ca, nofrills.ca, zehrs.ca, fortinos.ca, provigo.ca, maxi.ca and others | ca | no |
| `walmart-ca` | Walmart Canada | walmart.ca | ca | no |
| `voila` | Voilà | voila.ca | ca | no |
| `metro` | Metro | metro.ca | ca | no (study blocked) |

"Tested live: no" guides come from a read-only look at the site (signed out, nothing added) and its help pages. Trust what the page in front of you shows over the guide, and tell the user where the guide was wrong. For any other shop, follow **Shop without a guide** below.

## Hard rules

- Use the tab the user is already signed in to. Work in that one tab, one item at a time, with about 3 seconds between actions.
- Never type passwords, card details or loyalty-card numbers (Clubcard, Nectar, PC Optimum, Scene+ and the like). Never create an account. Never press Checkout, Pay, Place order or Confirm order.
- If the site asks for a login or a CAPTCHA, stop and ask the user to do it themselves. Carry on only when they say so.
- If the site blocks you (HTTP 403, "failed some security checks", "confirm you are human" that keeps coming back, "access restricted"), or says automated or AI-agent access is not allowed, **stop the run**. Do not retry, reload, switch tabs or domains, or try to get round it. Report what was added so far (unverified if the basket cannot be read) and the items left, and hand back to the user.
- Never remove or change items that were already in the basket before you started. Note them in your report.
- Don't change the user's store, delivery address, postcode or ZIP, or pickup/delivery choice without asking. Decline optional cookies; accept nothing else on the user's behalf.
- Book a delivery slot (or pickup window) only after the user confirms a specific one in chat.
- If an add might have failed (page error, spinner, timeout), read the basket before retrying so nothing is added twice.

## Procedure

1. Open the basket and record what is already in it (product and quantity).
2. For each item, in the order given:
   1. Search the shop for the `search` phrase.
   2. Choose the product that best matches the `buy` pack size. Prefer the lowest price per kg, lb, litre or each among sensible matches; the shop's own brand is fine. Avoid prepared, marinated or ready-to-eat variants unless the item name says so (e.g. "Cooked puy lentils"). Skip anything sold by a third-party seller or sent separately by courier or mail.
   3. Add the `count` for each pack in `buy`. "single" means one loose or individual item.
   4. If it is unavailable, choose the closest substitute (same ingredient, nearest size; or the nearest equivalent such as cod ↔ haddock) and note it. If nothing sensible exists, skip it and note it.
3. Read the full basket again and compare it with the list: every planned item present at the right count, earlier items untouched.
4. Report back (below).
5. Offer the next three available delivery slots (or pickup windows) and ask which one to book. After booking, remind the user to review the basket and check out themselves.

## What works on every shop

These came from two live Tesco runs (see `retailers/tesco.md`) and hold for any site:

- Find each Add button by its label, which usually contains the product name. **Scroll it into view, then click.** Off-screen clicks can silently do nothing.
- After each add, confirm the basket line or the product's quantity shows the expected count. Second clicks on the same product are the least reliable: use the quantity stepper (+) on the product or the basket page instead.
- When one results page shows several needed items (black beans and kidney beans, ground cumin and cumin seeds), add them all from that page.
- When an item is out of stock, broaden the search (`red peppers` → `peppers`). Make up the count with the nearest sensible alternative, e.g. a mixed 3-pack plus one single.
- If `need` is far below the planned pack (need about 90 g, planned 283 g jar), buy the smaller pack when one exists.
- Always finish by reading the whole basket: line count, unit count and total.
- Loose produce: add by count when the site offers a count, and leave any weight toggle alone. When the plan gives a weight ("1 lb", "500g") and the shop sells by count, use the shop's stated average weight ("about $0.90 each" at "$1.79/lb", "0.3 kg typically") to work out how many, rounding up. Items marked "final cost by weight" are charged on the weight picked, so the basket total is an estimate.

## Shop without a guide

For an online grocer with no guide (a regional chain, or a shop in another country such as Carrefour, E.Leclerc or Auchan in France), work out the site on the first item, then reuse what you learned. The hard rules and stop rules above apply unchanged.

- **Search.** Use the site's search box once, then note the URL it produces (`/search?q=…`, `/recherche?text=…`) and go straight to that URL for later items. If the site is in another language, translate each `search` phrase (red peppers → poivrons rouges) and keep the item's `name` for your report.
- **Product cards.** Each card shows the name, pack size, price and usually a unit price. Ignore cards marked sponsored if they are a worse match, and anything sold by a marketplace seller.
- **Add buttons and steppers.** Look for buttons labelled Add, Add to cart, Add to basket or Add to trolley, or the local equivalent (Ajouter, Ajouter au panier, In den Warenkorb, Añadir). After the first add the button usually becomes a stepper (−, count, +): use + for further units. Some sites ask you to pick a size or a delivery method first; choose what matches the user's current setting.
- **Loose versus packed produce.** Loose items are sold by count ("each", "la pièce", "sold in singles") or by weight ("per kg", "le kg", "au poids"). Packed items have a fixed size ("3 pack", "500 g", "barquette"). Match `buy`: a count plan wants a count; a weight plan can take a pack or loose items that add up to it.
- **Unit prices.** Compare like with like: £/kg, $/lb, ¢/oz, $/100 g, €/kg. Canadian sites often show both $/kg and $/lb.
- **The basket page.** It is behind the basket, cart, trolley or panier icon in the header, which usually shows the item count and total. Read it there at the start and the end.
- **Currency and units.** The site's currency may differ from the plan's (`currency`). Report both totals in their own currency and don't convert unless the user asks. Sites may use other units (metric in Canada and Europe, decimal commas such as "2,49 €"). Convert the plan's amount to the site's unit to choose the pack, rounding up.
- **Slots.** Many sites call slots créneaux, Zeitfenster or windows. Click-and-collect "drive" services (common in France) have collection slots instead of delivery. The same rule applies: book only what the user confirms.

At the end, tell the user the search URL pattern, Add button label and basket location you found, so a guide can be written for that shop.

## Report

- Shop and market used.
- Added: product, quantity, price.
- Substituted: what and why.
- Skipped: what and why.
- Already in the basket before you started.
- Basket total in the shop's currency, and the estimated total from MSTRCHF (`estTotal`, in `currency`) for comparison. Mention any minimum-basket charge if the total is close to the shop's minimum.

## Notes

- Quantities in the file are already scaled to the household and rounded up to whole packs.
- `usedIn` says which meals need the item; use it to judge substitutes (e.g. a curry can take any chicken thighs; a salad needs the leaves it names).
- Prices in the file are estimates, not the shop's live prices.
