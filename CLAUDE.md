# CLAUDE.md — CatchEm Landing Page

## Project Overview

Static landing page for **catchem.gg** — the hub for the CatchEm multi-chain Pokemon catching game. Directs users to Solana (`sol.catchem.gg`) and ApeChain (`ape.catchem.gg`) game clients.

- **Status**: Deployed
- **Domain**: `catchem.gg`
- **Architecture**: Single-file static HTML (no build tools, no frameworks)
- **Hosting**: Vercel (static)

## Quick Start

```bash
npx serve -s .        # Serve locally (any static server works)
# Open http://localhost:3000
```

No build step. No `npm install`. Just serve the directory.

## File Structure

```
├── index.html      # Complete landing page (~800 lines: HTML + CSS + JS)
├── admin.html      # Admin dashboard — password-gated metrics (password: catch3m)
├── .gitignore      # Git ignore rules
├── CLAUDE.md       # This file
└── README.md       # Project documentation
```

Everything lives in single HTML files — styles in `<style>` blocks, scripts in `<script>` blocks at the end.

## Page Sections (in order)

| # | Section ID | Content |
|---|-----------|---------|
| 1 | `#hero` | "Catch 'Em — On Chain" hero with typewriter animation, CTA buttons for Solana + ApeChain |
| 2 | `#stats` | Stats banner with count-up numbers (2 chains, 4 balls, 20 Pokemon, 100% on-chain) |
| 3 | `#about` | "What Is CatchEm?" description paragraph |
| 4 | `#gameplay` | "How It Works" — 5-step card grid |
| 5 | `#balls` | "Choose Your Ball" — 4 ball tier cards with pixel art SVG icons |
| 6 | `#economy` | "Where Your Money Goes" — 96%/3%/~1% revenue split |
| 7 | `#chains` | "Play On Your Chain" — Solana + ApeChain feature cards |
| 8 | `#community` | "Join the Trainers" — X and GitHub placeholder buttons (no URLs yet) |
| 9 | (footer) | Copyright, chain links, online indicator |

## CSS Architecture

### Custom Properties (`:root`)

```
--bg: #0a0a0a          Dark background
--panel: #1a1a1a       Card backgrounds
--border: rgba(255, 204, 0, .75)   Yellow border
--accent: #ffcc00      Yellow accent
--green: #00ff88       Green accent (Solana)
--red: #ff4444         Poke Ball red
--blue: #4488ff        Great Ball blue
--purple: #aa44ff      Master Ball purple
--pixel: 'Press Start 2P'         Pixel font (headings)
--body: 'Outfit'                  Body font (text)
```

### Key Classes

| Class | Purpose |
|-------|---------|
| `.observe` | Intersection Observer target — gets `.visible` class on scroll |
| `.stagger` | Children animate in sequence (stagger delay) |
| `.glow` | Yellow text-shadow glow effect |
| `.sec-label` | Section label with dashes: `— Label —` |
| `.sec-heading` | Section heading (Press Start 2P font) |
| `.btn` | Primary button with yellow border and hover glow |
| `.ball-card` | Ball tier card (`.poke`, `.great`, `.ultra`, `.master` modifiers) |
| `.chain-card` | Chain feature card (`.sol`, `.ape` modifiers) |
| `.step-card` | Gameplay step card |
| `.flow-card` | Economy flow card (`.pool`, `.treasury`, `.reserves` modifiers) |

### Scroll Animations

Uses `IntersectionObserver` with `threshold: 0.15`. Elements with `.observe` start with `opacity: 0; transform: translateY(30px)` and transition to visible on scroll. The `.stagger` class adds incremental delays to children.

### CRT Effects

Two pseudo-elements on `body::before` and `body::after`:
- `::before` — Repeating horizontal scanlines (2px gradient)
- `::after` — Noise texture via randomized radial gradient

Both are `pointer-events: none` and fixed position with low opacity.

### Mouse Glow

Cards track mouse position via `mousemove` listener, setting `--mx` and `--my` CSS variables. A `::before` pseudo-element uses these for a radial gradient glow that follows the cursor.

## JavaScript Features

All JS is in a single `<script>` block at the end of `<body>`:

1. **Intersection Observer** — Adds `.visible` class on scroll, triggers count-up for stats
2. **Count-Up Animation** — Animates numbers from 0 to target with cubic easing (1200ms)
3. **Typewriter Effect** — Cycles through 3 phrases in the hero section with type/delete animation
4. **Card Glow Tracking** — Updates `--mx`/`--my` CSS vars on mousemove for interactive glow

## Ball Tiers (displayed in #balls section)

| Ball | Price | Catch Rate | Flavor Text |
|------|-------|-----------|-------------|
| Poke Ball | $1.00 | 15% | "The classic. Affordable but risky." |
| Great Ball | $10.00 | 35% | "Better odds for serious trainers." |
| Ultra Ball | $25.00 | 60% | "High performance. High reward." |
| Master Ball | $49.90 | **99%** (not 100%) | "The ultimate catch." |

**Important:** Master Ball is 99% catch rate, NOT guaranteed. Do not use words like "guaranteed" or "never fails" when referring to it.

## Solana Payments

Solana chain uses **SolCATCH token** payments (not SOL or USDC directly).

## Ball Icon SVGs

Each ball is a 16×16 pixel art SVG using `<rect>` elements:
- `shape-rendering="crispEdges"` for sharp pixel edges
- `image-rendering: pixelated` on the container
- Design: **solid color circle with white horizontal line through the middle** (matches in-game sprite)

Ball colors:
| Ball | Top/Bottom Color | CSS var |
|------|-----------------|---------|
| Poke Ball | `#ff4444` (red) | `--red` |
| Great Ball | `#4488ff` (blue) | `--blue` |
| Ultra Ball | `#ffcc00` (yellow) | `--accent` |
| Master Ball | `#aa44ff` (purple) | `--purple` |

SVG structure (same pattern for all 4):
```
Rows 1-6:  Ball color (top half, circle shape)
Rows 7-8:  White (#ffffff) horizontal line
Rows 9-14: Ball color (bottom half, circle shape)
```

## External Links

| Link | Destination |
|------|-------------|
| "Launch on Solana" button | `https://sol.catchem.gg` |
| "Launch on ApeChain" button | `https://ape.catchem.gg` |
| "Play on Solana" card button | `https://sol.catchem.gg` |
| "Play on ApeChain" card button | `https://ape.catchem.gg` |
| X button | Placeholder (`#`, no link yet) |
| GitHub button | Placeholder (`#`, no link yet) |

## Fonts

Loaded from Google Fonts:
- **Press Start 2P** — Pixel font for headings and labels
- **Outfit** (400–900) — Clean sans-serif for body text

## Meta Tags & SEO

- Open Graph tags for social sharing (title, description, image, URL)
- Twitter card meta (summary_large_image)
- Inline SVG favicon (PokeBall design)
- `og:image` expects `https://catchem.gg/og-image.png` (needs to be created/uploaded)

## Responsive Breakpoints

| Breakpoint | Layout Change |
|------------|--------------|
| `≤900px` | Grid columns reduce, padding shrinks |
| `≤768px` | Hero buttons stack, cards go single-column |
| `≤600px` | Headings shrink, ball grid 2-column, stats wrap |
| `≤480px` | Maximum compaction, smallest font sizes |

## Deployment

Deployed on Vercel as static site:
- Framework preset: "Other"
- No build command
- Output directory: `.` (root)
- Custom domain: `catchem.gg`
- `vercel.json` enables `cleanUrls` so `/admin` serves `admin.html`

## Related Repositories

| Repo | Description |
|------|-------------|
| [Pokemon-Trader](https://github.com/ZaraC-Codes/Pokemon-Trader) | ApeChain game client (`ape.catchem.gg`) |
| [Pokemon-Trader-Solana](https://github.com/ZaraC-Codes/Pokemon-Trader-Solana) | Solana game client (`sol.catchem.gg`) |

## Coding Conventions

- No build tools — edit `index.html` directly
- CSS custom properties for all colors/fonts (change in `:root`)
- All animations use CSS transitions or requestAnimationFrame (no libraries)
- Inline SVGs for icons (no external icon libraries)
- Semantic HTML sections with descriptive comments
- Mobile-first responsive design via media queries at bottom of `<style>`

## Admin Dashboard (`admin.html`)

Password-gated admin dashboard at `/admin` (password: `catch3m`).

### Features
- **Chain selector**: Solana | ApeChain | Both — filters all metrics
- **Live metrics**: Auto-refreshes every 30 seconds
- **Overview cards**: Total revenue, 24h revenue, throws, win rate, vault NFTs, unique wallets
- **Ball table**: Per-tier counts, revenue, and percentage
- **Mode table**: Placeholder — Adventure vs Encounter not tracked on-chain
- **Charts**: Revenue by tier (bar), ball usage (doughnut), daily revenue (line)

### Configuration (top of `<script>` block in admin.html)
| Constant | Purpose |
|----------|---------|
| `SOLANA_PROGRAM_ID` | Solana program ID (set to `'TODO_SOLANA_PROGRAM_ID'` until deployed) |
| `SOLANA_RPC` | Solana RPC endpoint |
| `APE_CONTRACT` | ApeChain PokeballGame proxy address |
| `APE_RPC` | ApeChain RPC endpoint |
| `APE_DEPLOY_BLOCK` | Block to start event scanning from (0 = last ~1M blocks) |
| `REFRESH_SEC` | Auto-refresh interval in seconds (default 30) |

### Data Sources
- **ApeChain**: ethers.js v6 — contract state reads + `eth_getLogs` event scanning (BallPurchased, ThrowAttempted, CaughtPokemon, FailedCatch)
- **Solana**: @solana/web3.js — PDA account reads (GameConfig, NftVault) + transaction log parsing for Anchor events
- Events are cached in `sessionStorage` for fast incremental refreshes

### CDN Dependencies
- ethers.js v6 (ApeChain)
- Chart.js v4 (charts)
- @solana/web3.js v1 (Solana, loaded dynamically only when configured)

## Common Tasks

### Change ball prices or catch rates
Edit the `.ball-card` sections in HTML. Each card has `.price` and `.rate` divs.

### Add a new chain
1. Add a new `.chain-card` in the `#chains` section
2. Add corresponding CSS for the card's border color
3. Add CTA button in the hero section

### Update social links
Edit the `#community` section — the X and GitHub `<a>` tags. Currently placeholder (`href="#"`).

### Modify animations
- Scroll triggers: Adjust `threshold` and `rootMargin` in the IntersectionObserver config
- Count-up speed: Change `duration` in the `countUp()` function (default 1200ms)
- Typewriter speed: Adjust `setTimeout` values in the typewriter IIFE (30ms type, 16ms delete)

### Change color scheme
Update CSS custom properties in `:root`. All components reference these variables.
