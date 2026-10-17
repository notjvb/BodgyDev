# bodgy.dev

The portfolio site for bodgy.dev's apps: ProsNCons, ThisOrThat, STRNGTH and
Bell Bearing. Plain HTML and CSS with no build step, served by GitHub Pages
from `main` at https://bodgy.dev.

```
index.html          the home page
<app>/index.html    one page per app, with a screenshot gallery
assets/site.css     the ProsNCons design system, as CSS custom properties
assets/icons/       app icons (512 px, copied from each app's asset catalog)
assets/shots/       screenshots, 800 px wide JPEGs
CNAME               tells GitHub Pages to serve the apex domain
```

## Preview

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000. Paths are root-relative, so open the site from
its root rather than as files.

## Screenshots

STRNGTH's come from its App Store listing. The others were taken in the iOS
Simulator (iPhone 17, status bar overridden to 9:41) with demo data: ProsNCons
and ThisOrThat ran against their local backends (`wrangler dev`) seeded with
made-up decisions, so nothing touched production. Keep new ones at the same
size and name them `<app>-<n>.jpg`.

## Design system

`assets/site.css` mirrors `ios/ProsNCons/Design/Theme.swift`: a cream page
(plum at night), white surfaces with a solid edge underneath instead of a
shadow, and the eight palette colors, each with `edge`, `soft`, `soft-edge` and
`ink` variants for light and dark. Put `tint-<color>` on an element to pick a
palette color for it and its children (`--base`, `--edge`, `--soft`, …).

When the palette changes in the app, regenerate the variants with the same
blends Theme.swift uses: edge mixes 22% black (40% at night), soft mixes 84%
white (78% `#17151F` at night), and so on.

## DNS

`bodgy.dev` is on Cloudflare. The apex points at GitHub Pages with DNS-only
(grey cloud) records so GitHub can issue the HTTPS certificate:

| Type | Name | Content |
| --- | --- | --- |
| A | `@` | 185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153 |
| AAAA | `@` | 2606:50c0:8000::153, 2606:50c0:8001::153, 2606:50c0:8002::153, 2606:50c0:8003::153 |
| CNAME | `www` | `notjvb.github.io` |

`pnc.bodgy.dev` belongs to the ProsNCons Worker (its invite links) and is
unrelated to this site.
