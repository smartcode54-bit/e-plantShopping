# Paradise Nursery

> Where Green Meets Serenity

A single-page houseplant shopping cart built with React and Redux Toolkit. Browse thirty plants across five care categories, add them to a cart, and adjust quantities with totals that update live.

**Live site:** [smartcode54-bit.github.io/e-plantShopping](https://smartcode54-bit.github.io/e-plantShopping/)

## Features

- **Landing page** with a Get Started entry point into the catalogue
- **Product catalogue** of five categories, six plants each, rendered as cards with image, description and price
- **Add to cart** — the button disables and greys out once a plant is in the cart
- **Cart management** — increment, decrement, and delete plants; decrementing the last unit removes the plant entirely
- **Live totals** — per-plant subtotals, overall cart total, and a running item count on the navbar cart icon, all driven from a single Redux store

### Plant categories

| Category | Examples |
| --- | --- |
| Air Purifying | Snake Plant, Spider Plant, Peace Lily |
| Aromatic Fragrant | Lavender, Jasmine, Rosemary |
| Insect Repellent | Marigold, Basil, Catnip |
| Medicinal | Aloe Vera, Echinacea, Chamomile |
| Low Maintenance | ZZ Plant, Pothos, Succulents |

## Tech stack

| Concern | Choice |
| --- | --- |
| UI | React 18 |
| State | Redux Toolkit + React Redux |
| Build | Vite 5 |
| Linting | ESLint |
| Hosting | GitHub Pages via `gh-pages` |

## Getting started

Requires Node.js 18 or newer.

```bash
git clone https://github.com/smartcode54-bit/e-plantShopping.git
cd e-plantShopping
npm install
npm run dev
```

Vite prints a local URL — open it to see the app.

## Available scripts

| Script | What it does |
| --- | --- |
| `npm run dev` | Start the dev server with hot reload |
| `npm run build` | Produce a production build in `dist/` |
| `npm run preview` | Build, then serve the output locally |
| `npm run lint` | Run ESLint across the project |
| `npm run deploy` | Build and publish `dist/` to the `gh-pages` branch |

## Project structure

```text
src/
├── App.jsx           Landing page, toggles through to the catalogue
├── AboutUs.jsx       Blurb shown on the landing page
├── ProductList.jsx   Plant catalogue, navbar, and add-to-cart handling
├── CartItem.jsx      Cart view with quantity controls and totals
├── CartSlice.jsx     Redux slice: addItem, removeItem, updateQuantity
├── store.js          Store configuration, registers the cart reducer
└── main.jsx          Entry point, wraps App in the Redux Provider
```

## How state flows

The cart lives in one Redux slice, so every view reads the same source of truth.

1. `ProductList` dispatches `addItem(plant)` when Add to Cart is clicked.
2. `CartSlice` either pushes the plant with `quantity: 1`, or increments the quantity if it is already in the cart.
3. `CartItem` dispatches `updateQuantity` on the `+` / `-` buttons and `removeItem` on Delete.
4. Subtotals, the cart total, and the navbar count are all derived from store state, so they re-render on any dispatch.

Prices are stored as strings including the currency symbol (`"$15"`), so arithmetic parses them with `parseFloat(item.cost.substring(1))`.

## Deployment

The site deploys to GitHub Pages from the `gh-pages` branch:

```bash
npm run deploy
```

`vite.config.js` sets `base: "/e-plantShopping"` so that asset URLs resolve under the repository subpath. If you fork this project under a different repository name, update that value to match or the deployed page will load blank.

## Credits

Built as the final project for the IBM *Developing Front-End Apps with React* course on Coursera. Plant photography from [Pixabay](https://pixabay.com) and [Unsplash](https://unsplash.com).
