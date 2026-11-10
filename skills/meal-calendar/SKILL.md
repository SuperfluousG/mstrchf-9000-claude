---
name: meal-calendar
description: Put a MSTRCHF 9000 week of meals into the user's calendar, one event per meal with the recipe's ingredients and method. Use when the user asks to book, schedule or add their planned meals to a calendar.
---

# Meals into the calendar

## Get the week

In order of preference:

1. The MSTRCHF 9000 planner artifact: read `data/users/me/kitchen` (see the `mstrchf-planner` skill). Use the week the user names; otherwise the current week if it has meals, else next week.
2. A local `data/kitchen.json` from a MSTRCHF 9000 checkout, or a backup file the user gives you. Same `state` shape.
3. A list the user pastes.

A pick's `day` is 0 for Monday to 6 for Sunday, counted from the week id (a Monday, `YYYY-MM-DD`). Recipes are next to this file, by `id`, in the kitchen's own words and measures: `recipes.json` for the UK, `recipes-us.json` for the US and `recipes-ca.json` for Canada. Pick the file from `state.profile.market` (`"uk"`, `"us"` or `"ca"`); if it is missing, use the user's locale, and the UK file when unsure.

## Ask before booking

Confirm in one message, then wait for a yes:

- Which calendar. Use a calendar connector the user has (for example Google Calendar). If there are several calendars or accounts, ask which; suggest their personal one.
- Which meals: all of them, or only dinners.
- Times. Defaults: breakfast 08:00, lunch 12:30, dinner 18:30, in the user's time zone. Each event lasts the recipe's `minutes`, at least 15.
- Skip any day that has already passed.

Before creating anything, list the calendar's events for that week and leave out meals that are already booked (same title and day), so nothing is added twice.

## Each event

- Title: `Dinner: <recipe title>` (or Breakfast, Lunch).
- Description, plain text:

```
<blurb>

<minutes> min · for <people>

Ingredients
• <amount> <name>, <prep>
(plus <cupboard items>)

Method
1. <step>
2. <step>

Planned with MSTRCHF 9000.
```

Scale ingredient amounts from the recipe's `serves` to the household size (`state.profile.people`): multiply `qty`, then write grams and millilitres as whole numbers (US and Canadian files: ounces, pounds and cups, matching how `amount` is written), `each` items as fractions (½, ¼, 1½), and small spice or sauce amounts as teaspoons using `gramsPerTsp` (3 tsp = 1 tbsp). Use `amount` unchanged when the household matches `serves`. Steps are written for the recipe's own servings; when you scale, add one line after the method: "The method is written for <serves>; scale the amounts as above."

Use sentence case headings, never capitals.

## After booking

Report how many events were created, in which calendar, and any meals skipped (already booked or in the past).
