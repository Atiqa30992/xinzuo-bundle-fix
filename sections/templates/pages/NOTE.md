## What I picked

Bundle Builder — `/pages/bundle-builder` was a completely dead, empty page. Clicking "Build a Bundle" from the navigation led to a blank page with no content.

## Why it's the highest-impact thing here

The Bundle Builder is a direct revenue driver. It encourages customers to buy multiple knives in one order, increasing average order value (AOV). A broken bundle page means:

- Every customer who clicks "Build a Bundle" from the nav hits a dead end
- The store loses its most powerful upsell mechanism
- Tiered discounts (the biggest conversion incentive) are completely inaccessible

Of all the issues on the site, this one has the clearest, most direct impact on sales. A Lighthouse point here or a focus-ring there is nice — a dead revenue page is a bleeding wound.

## What I did

Rebuilt `sections/bundle-builder.liquid` from scratch with:

- **Tabbed series selector** — each block in the section schema maps to one collection, editable from the theme customizer with no code changes needed
- **Product grid per tab** — lazy-loaded images, hover reveal, click-to-select with visual feedback
- **Sticky slide-up cart** — animates in once the first item is selected, stays out of the way otherwise
- **Tiered discount logic** — 2 knives = 5%, 3 = 10%, 4+ = 15%, shown live as items are added
- **Cart API integration** — `/cart/add.js` adds all selected variants in one request, then redirects to `/cart`
- **Accessible markup** — proper `role="tablist"`, `aria-selected`, `aria-controls`, `aria-live` on the cart, focus-visible rings everywhere, all button labels descriptive

Also updated `templates/pages/bundle-builder.json` to wire the section to the page.

## What I'd do next

- Add variant selector (size / handle colour) before adding to bundle — currently defaults to `first_variant`
- Persist bundle selection in `sessionStorage` so refresh doesn't reset it
- Add a maximum bundle size setting (configurable per merchant in schema)
- Integrate a discount code via the Discount API rather than relying on line-item scripts
- Animate the card checkmark on selection for stronger affordance
