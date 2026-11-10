# Metro (metro.ca)

Tested live: no (read-only study, 10 Nov 2026: blocked)

The study's first page, `https://www.metro.ca/en/online-grocery/search?filter=zucchini`, returned **HTTP 403** with a Cloudflare "Almost there: please confirm that you are human" page (in French and English). The study stopped there.

In the user's own signed-in browser in Canada the site may load normally. If this check appears during a run, ask the user to complete it themselves and carry on only when they say so. If it keeps coming back, or the site returns 403 pages, stop the run (see the hard rules). Never try to complete the check yourself.

## What is known without the site

| | |
|---|---|
| Market and currency | Canada (Ontario and Quebec), CAD |
| Search | `https://www.metro.ca/en/online-grocery/search?filter=<phrase>` (pattern only; results not seen). The site is bilingual; French pages are under `/fr/`. |
| Own brand | Irresistibles; Selection. Not checked on the site. |
| Loyalty | Moi. Never type a Moi number. |

From metro.ca pages: the Unlimited Delivery pass needs a $50 minimum per delivery order. Express Delivery (under 2 hours, where available) runs through Uber Eats and is not covered by the pass. Older sources give delivery fees of $4 to $8 by day and time, and a $50 minimum. Read the actual fees in the cart.

## Not seen

Everything on the site: search results, product cards, Add buttons, loose produce, the cart, substitutions and the delivery slot flow. On the first live run, record the Add button label, how loose produce is sold and the cart line format, and add them here.
