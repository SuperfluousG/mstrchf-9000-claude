# MSTRCHF 9000 for Claude

A meal planner tuned to your taste, and the skills that do the shopping and the scheduling.

| Skill | What it does |
|---|---|
| `mstrchf-planner` | Sets up your own copy of the planner as a Claude artifact, opens it, and reads your week. Your kitchen is saved privately to your Claude account. |
| `grocery-basket` | Fills your basket at your online grocer from the planner's "Order with Claude" instructions, in your own signed-in browser. Has a guide for each leading shop in the UK (Tesco, Sainsbury's, Asda, Ocado, Morrisons), the US (Walmart, Kroger, Target, Albertsons) and Canada (PC Express, Walmart Canada, Voilà, Metro), and a method for any other online grocer. Stops before the delivery slot and checkout for you. |
| `meal-calendar` | Books each planned meal into your calendar with its ingredients and method. |

## Install

**Claude app (desktop or claude.ai)**

1. Download the `mstrchf-9000-<version>.plugin` file. Don't unzip it.
2. In Claude, go to **Customize → Plugins → Add → Upload plugin** and choose the file.
3. Start a new chat and say: **"Open MSTRCHF 9000."** The first time, Claude sets up your own copy of the planner as an artifact on your Claude account and gives you the link; the recipe photos follow shortly. After that, the same words open it straight away. Your kitchen is saved to your Claude account and is private to you.

If **Upload plugin** isn't there, your organisation's settings don't allow custom plugins.

You can also install from GitHub instead of downloading the file: go to **Customize → Plugins → Add → Add marketplace**, enter `SuperfluousG/mstrchf-9000-claude`, then install MSTRCHF 9000 from it.

**Claude Code**

```
claude plugin marketplace add SuperfluousG/mstrchf-9000-claude
claude plugin install mstrchf-9000@mstrchf-9000
```

**Updating**

Install the new version the same way, then say: "Update my MSTRCHF 9000 planner." Claude updates your planner in place at the same link. Your kitchen is not affected.

## Needs

- A paid Claude plan, with code execution turned on so skills can run.
- The planner: the Claude desktop app or claude.ai (it publishes an artifact).
- The basket: a browser Claude can use (Claude in Chrome, or the desktop app's browser) with you signed in to your grocery shop.
- The calendar: a calendar connector such as Google Calendar.

## Safety

Claude never types passwords, card details or loyalty numbers, never creates accounts, never checks out, and books a delivery slot only after you confirm one. If the shop shows a login, CAPTCHA or security check, Claude stops and hands back to you.

Amazon's Conditions of Use bar unauthorised AI agents, so for Amazon Fresh Claude gives you the list to shop yourself instead of filling the cart.

Recipes are original. Prices are estimates for planning, not the shop's live prices. Diet and allergen labels come from each recipe's ingredients; always check product labels yourself.

## Licence

Free to use for yourself; not to be redistributed. The recipes, photographs and artwork are © 2026 Bayes Ltd. See [LICENSE](LICENSE).
