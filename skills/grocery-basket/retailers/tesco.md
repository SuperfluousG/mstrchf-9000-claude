# Tesco (tesco.com)

Tested live: yes, 2 runs, Nov 2026

| | |
|---|---|
| Market and currency | UK, GBP |
| Search | `https://www.tesco.com/groceries/en-GB/search?query=<phrase>`, which now redirects to `https://www.tesco.com/shop/en-GB/search?query=<phrase>` (read-only check, 10 Nov 2026) |
| Add button | `add 1 <exact product name>` |
| Own brand | Tesco, Tesco Finest. Tesco own-brand is fine. |
| Loyalty | Clubcard. Never type a Clubcard number. |
| Minimum basket | Baskets under £50 carry a £5 minimum-basket charge. Mention it if the total is close. |

## Lessons from the first live run (9 Nov 2026)

- Every Tesco Add button is labelled `add 1 <exact product name>`. Find it by that label, **scroll it into view, then click**. In the first run 4 of 40 off-screen clicks silently did nothing.
- After each add, confirm the product's basket line ("2 Tesco Limes Each for £0.46") shows the expected count. Second clicks on the same product were the least reliable; on the basket page, use that product's own `add 1 …` button.
- Always finish by reading the whole basket: line count, unit count and the guide price. The first run matched 40 lines and 45 units only after a retry pass.
- Loose produce (onions, ginger) is added by count in Quantity mode; leave the weight toggle alone.
- When an item is out of stock, broaden the search (`red peppers` → `peppers`). Make up the count with the nearest sensible alternative, e.g. a mixed 3-pack plus one single.
- If `need` is far below the planned pack (curry paste: need about 90 g, planned 283 g jar), buy the smaller pack when one exists.
- Baskets under £50 carry a £5 minimum-basket charge. Mention it if the total is close.

## Lessons from the second live run (9 Nov 2026)

- **Work in one tab, one item at a time.** On the second run, searching in six tabs at once got the browser blocked by Tesco's security checks after about 20 items. Tesco then returned HTTP 403 "your browser has failed some security checks" on every page, including the basket.
- A single tab with about 3 seconds between actions added 47 items without a block on the same day. Pattern per item: search page, read the top results, `find "add 1"` to get every Add button by product name, then scroll, click, wait and confirm the "N <product> for £x" basket line. When one results page shows several needed items (black beans and kidney beans, ground cumin and cumin seeds), add them all from that page.
- **If Tesco shows a security, CAPTCHA or "failed some security checks" page, stop immediately.** Do not retry, switch tabs or try to get round it. Report what was added so far (unverified if the basket cannot be read) and the remaining items, and hand back to the user.

## Read-only check (10 Nov 2026, signed out)

- Search results mix in **Tesco Marketplace** products. Their cards start "Marketplace ." and say "Sold by Marketplace seller" with "FREE Courier Delivery by <date>". For "red peppers", most of the top results were Marketplace hot sauces and seeds. Skip every Marketplace product: it is not part of the grocery delivery.
- Grocery cards show the price, the unit price ("£38.89/kg") and "Quantity controls Add".
- Signed out, "Tesco Red Peppers Each" showed as out of stock. Stock depends on the user's store, so judge availability only in their signed-in tab.

## Not checked

- The substitution setting and the delivery-slot flow; neither was recorded in the live runs.
- Delivery charges other than the minimum-basket charge.
