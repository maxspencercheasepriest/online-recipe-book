# Recipe Book

A single-page recipe book. Open `index.html` in a browser; no build step or server needed.

- Home page with search and categories (Puddings, Roasts, Indian, Asian, Pasta & Italian, Soups & Stews, Baking & Bread, Sides & Sauces)
- Each recipe has scalable quantities, a g/ml ↔ oz/cups toggle, tick-off ingredients and step timers
- Links use `#hash` routes, e.g. `index.html#char-siu-fried-rice`

## Adding a recipe

Recipes live in the `RECIPES` array near the bottom of `index.html`. Each one looks like:

```js
{
  id: "url-friendly-id",          // used in the #link
  category: "asian",              // one of the CATEGORIES ids
  tags: ["Quick", "Weeknight"],   // optional, any of the TAGS list
  title: "Recipe name",
  photo: "images/url-friendly-id.jpg",   // optional, shown on the card and recipe page
  standIn: true,                  // optional, labels the photo as a stand-in until a real one is added
  cover: true,                    // optional, use this photo on the category tile
  blurb: "One or two sentences.",
  source: ["Site name", "https://..."],   // optional
  serves: 4, unit: "people",      // base quantity the amounts are written for
  chips: [["Serves 4"], ["Chill overnight", "hot"]],  // "hot" highlights a chip
  ingredients: [
    [200, "g", "plain flour"],    // [amount, unit, name] — units: g, ml, tsp, tbsp, cup, pinch, or "" for a count
    [3, "cup", "rice", "plus1"]   // "plus1" = 1 per serving plus 1 extra, instead of straight scaling
  ],
  steps: [
    ["Step title", "What to do.", 600]  // last number is a timer in seconds, 0 for none
  ],
  note: ["Note heading", "Note text."]  // optional
}
```

To add a tag, add it to the `TAGS` list (it shows on the home page once a recipe uses it). To add a category, add an entry to `CATEGORIES` with an `id`, `name`, `blurb` and tile `color`.

## Event lists

`#lists` shows your event lists and the ready-made menus. A list holds recipes and a guest count. It builds a combined shopping list (with a Copy button) and splits the recipes into "Do ahead" (anything tagged Make-ahead) and "On the day". Recipes measured in people, glasses or mugs scale to the guest count, and anything else starts at one batch. Each amount can be changed by hand.

Each list has **Share link** (a link with the whole list packed into it; whoever opens it sees the list and can save their own copy), **Copy as text** (recipes, shopping list and the link, ready to paste into a message) and **Duplicate**. Share links identify recipes by a short code made from the recipe `id`, so changing a recipe's `id` breaks old links to it.

Your own lists are saved in the browser (localStorage), so they stay on the device you made them on. Ready-made menus live in the `MENUS` array in `index.html`: add one with an `id` starting `menu-`, a `name`, `guests`, `blurb` and a list of recipe ids.
