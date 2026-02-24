# CatchEm Landing Page

Static landing page for **[catchem.gg](https://catchem.gg)** — the hub for the CatchEm multi-chain Pokemon catching game.

## Overview

Single-file HTML/CSS/JS landing page that serves as the entry point for CatchEm, directing players to the Solana and ApeChain game clients. Built with a retro pixel-art aesthetic using the Press Start 2P font, CRT scanline effects, and scroll-triggered animations.

## Live URLs

| URL | Description |
|-----|-------------|
| [catchem.gg](https://catchem.gg) | This landing page |
| [sol.catchem.gg](https://sol.catchem.gg) | Solana game client |
| [ape.catchem.gg](https://ape.catchem.gg) | ApeChain game client |

## Sections

1. **Hero** — Animated typewriter tagline, CTA buttons for both chains
2. **Stats Banner** — Animated count-up numbers (chains, ball tiers, wild Pokemon)
3. **About** — What is CatchEm?
4. **How It Works** — 5-step gameplay walkthrough
5. **Choose Your Ball** — 4 ball tiers with pixel art icons, prices, catch rates
6. **Economy** — Revenue split breakdown (96% NFT Pool, 3% Treasury, ~1% Reserves)
7. **Multi-Chain** — Solana and ApeChain feature cards with play links
8. **Community** — Social links (X, GitHub)
9. **Footer** — Copyright, chain links, online status indicator

## Tech Stack

- **Pure HTML/CSS/JS** — No build tools, no frameworks, no dependencies
- **Press Start 2P** + **Outfit** fonts (Google Fonts)
- **Intersection Observer** for scroll-triggered fade-in animations
- **CSS custom properties** for theming
- **Inline SVG** pixel art for ball icons (16x16 grid, `shape-rendering: crispEdges`)

## Development

Serve the directory with any static file server:

```bash
# Using npx serve
npx serve -s .

# Using Python
python -m http.server 3333

# Using PHP
php -S localhost:3333
```

Then open `http://localhost:3333`.

## Deployment

Deployed on **Vercel** as a static site:

1. Import repo at [vercel.com/new](https://vercel.com/new)
2. Framework preset: **Other**
3. No build command needed — serves `index.html` directly
4. Add custom domain `catchem.gg` in project settings

## File Structure

```
├── index.html      # Complete landing page (HTML + CSS + JS, single file)
├── .gitignore      # Git ignore rules
├── CLAUDE.md       # Claude Code instructions
└── README.md       # This file
```

## Design Reference

- Dark theme (`#0a0a0a` background) with yellow (`#ffcc00`) accent
- CRT scanline overlay effect
- Mouse-tracking glow on interactive cards
- Responsive: desktop grid → mobile single-column
- Ball icons match in-game sprite style (colored circle with white center line)
