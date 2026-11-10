# Albertsons (albertsons.com and banners)

Tested live: no (read-only study, 10 Nov 2026: blocked)

The study's first page, `https://www.albertsons.com/shop/search-results.html?q=zucchini`, returned **HTTP 403** with an empty page from a UK connection. The study stopped there and did not try other domains. A US visitor in their own signed-in browser may see the site normally; if they also get a 403, stop the run (see the hard rules).

Albertsons Companies runs one shop site under many banners, each on its own domain: Safeway, Vons, Jewel-Osco, Acme, Shaw's, Star Market, Tom Thumb, Randalls, Pavilions and others. Use this guide for whichever banner the user is signed in to. Do not switch domains to get round a block.

## What is known without the site

| | |
|---|---|
| Market and currency | US, USD |
| Search | `https://www.<banner domain>/shop/search-results.html?q=<phrase>` (pattern only; results not seen) |
| Own brand | Signature Select, Signature Farms, O Organics, Open Nature, Lucerne (dairy). Not checked on the site. |
| Loyalty | Never type a phone or loyalty-card number. |

From an Albertsons FAQ and Safeway promotion pages: delivery in most areas costs $9.95, varying by store and window. A $30 minimum applies, with a minimum-order fee below it. A FreshPass subscription removes delivery fees on qualifying orders. Where a third party such as Instacart does the delivery, its own terms may apply. Read the actual fees in the cart.

## Not seen

Everything on the site: search results, product cards, Add buttons, loose produce, the cart, substitutions and the delivery-window flow. On the first live run, record the Add button label, how loose produce is sold and the cart line format, and add them here.
