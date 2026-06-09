# Moving the Wall — an interactive paper

Coupling detection between two noise-like streams, from baduk to Granger causality.
A static, self-contained site: an interactive board (E1 predicts the next move; the
2016 Lee Sedol vs AlphaGo games are replayable), an animated walk through the paper,
and the full paper in English and Korean.

## Structure
- `index.html` — the interactive scrollytelling site (entry point)
- `PAPER.html` / `PAPER_KO.html` — the paper (EN / KO), math as native **MathML** (no JS)
- `PAPER.pdf` / `PAPER_KO.pdf` — print versions
- `baduk_app.html`, `baduk_moves_3d.html`, `baduk_compare.html`, `baduk_model.html` — interactive explorers
- `vendor/three.min.js`, `vendor/OrbitControls.js` — self-hosted 3D library (pinned three.js r128)

## Deploy (GitHub Pages, HTTPS)
1. Push this folder to the repo's default branch.
2. Repo → **Settings → Pages** → Source: *Deploy from a branch* → **main / (root)** → Save.
3. Wait for the build, then visit `https://<user>.github.io/baduk/`.
4. Settings → Pages → **Enforce HTTPS** (on).

## Security posture
- **Static only** — no backend, no database, no auth, no cookies, no user input read into the DOM → effectively no XSS/injection surface.
- **No third-party scripts** — three.js is self-hosted under `vendor/` (no CDN supply-chain risk); the papers use native MathML (no MathJax CDN). The only third-party origin is Google Fonts (stylesheet + font files), locked down by CSP.
- **Content-Security-Policy** (per-page `<meta>`): `default-src 'none'`, scripts/styles limited to same-origin, fonts to Google Fonts only, images to self + `data:`, `connect-src 'self'`, plus `frame-ancestors 'none'` (anti-clickjacking), `base-uri 'none'`, `form-action 'none'`.
- `X-Content-Type-Options: nosniff` and `referrer: no-referrer` set via meta.
- **HTTPS** enforced by GitHub Pages.
- No secrets, keys, emails, or local paths in any published file (audited).

## Local preview
    python3 -m http.server 8000   # then open http://localhost:8000
