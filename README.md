# Lagunitas Brew Ad

> Scroll-driven product ad recreation — GSAP ScrollTrigger pins and scrubs a 3D bottle rotation over 435vh, with multi-layer parallax splats and Locomotive Scroll inertia sync.
---

## What this demonstrates

Scroll-driven product storytelling — the kind used on Apple product pages, Awwwards winners, and luxury brand sites — requires precise coordination between scroll inertia, element pinning, and multi-property animations firing at specific scroll positions. Getting these to work without jitter means understanding how virtual scroll libraries need to be proxied to GSAP's measurement system.

This is a recreation of a premium brand scroll experience built with vanilla JS to understand every mechanic directly.

---

## Techniques

**Pinned bottle with scrubbed rotation and scale**

Two chained `ScrollTrigger` instances on the same `#bottle` element:

- Instance 1: pins the bottle and rotates it to `-15deg` with `scrub: 3` over a trigger range spanning `top 5%` to `top -435%` — the bottle holds its position while the page scrolls past it, slowly rotating.
- Instance 2: scales the bottle to `0.7` as `#page4` enters at `top 70%` — creating the illusion it's being set down as the narrative moves forward.

**Locomotive + ScrollTrigger bridge**

Locomotive Scroll takes over the native scroll container, so `window.scrollY` is always 0 — GSAP reads 0 for every trigger. The fix: `ScrollTrigger.scrollerProxy("#main", {...})` tells GSAP to read scroll position from Locomotive's internal state instead of the window. Without this, nothing fires at the right time.

**Multi-layer parallax**

Splat assets (`splat-red`, `splat-black`) and text layers animate at different rates using independent ScrollTrigger instances — creating foreground/midground/background depth from flat image assets.

---

## Tech Stack

| Tool | Purpose |
|------|---------|
| GSAP 3 + ScrollTrigger | Pin, scrub, and trigger animations at scroll positions |
| Locomotive Scroll | Smooth inertia scroll with virtual container |
| Vanilla JavaScript | Direct animation control, no abstraction layer |

---

## Getting Started

No build step. Serve directly with any static server.

```bash
git clone https://github.com/abhijeet-builds/lagunitas-brew-ad.git
cd gsap-scroll-ad

# Local dev server
npx serve .
# or open index.html directly in a browser
```

---

## Project Structure

```
gsap-scroll-ad/
├── index.html      # Markup + CDN imports (GSAP, Locomotive, ScrollTrigger)
├── style.css       # Layout, section heights, asset positioning
├── index.js        # All ScrollTrigger logic + Locomotive proxy setup
└── img/            # Bottle, logo, splat, and brand assets
```

---

## Deploy

Drag the folder to [Netlify](https://netlify.com). No build command. Publish directory: `/`.

---

## License

MIT
