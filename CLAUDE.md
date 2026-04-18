# thirty — Marketing Website

## What This Is
Marketing website for the thirty meditation app. Contains landing page, healthcare workers niche page, privacy policy, and support page.

## Tech Stack
- Plain HTML/CSS (no framework)
- Vite for build/dev server (multi-page config in vite.config.js)
- Static files deployed to Vercel
- GitHub repo: SLMPhatty/thirty-seconds

## Pages
- `index.html` — Main landing page with breathing animation, features, physician credibility section, healthcare workers banner
- `healthcare.html` — Niche landing page for healthcare workers (doctors, nurses, clinical staff) — 6 clinical scenarios, burnout stats, physician-built positioning
- `privacy.html` — Privacy policy
- `support.html` — Support/FAQ page
- `sitemap.xml` — SEO sitemap
- `robots.txt` — Search engine crawler rules

## Build
```bash
npx vite build    # Outputs to dist/
npx vite          # Dev server
```

## Deployment
Push to `main` → Vercel auto-deploys from the repo.

## Key Positioning
- **Physician-built** — Dr. Seth Miller (GP) built this for himself, then for his patients
- **Healthcare workers niche** — dedicated page targeting physicians, nurses, clinical staff
- **$4.99 lifetime** — no subscription, anti-Calm/Headspace positioning
- **Privacy-first** — no analytics, no tracking, all data local

## SEO
- Schema.org SoftwareApplication structured data on index.html
- Schema.org WebPage + author data on healthcare.html
- Sitemap submitted for Google indexing
- Target keywords: meditation app, healthcare worker meditation, physician burnout, 30 second meditation

## 🍎 Apple App Store Review Guidelines
Before submitting to the App Store, READ: /Users/slm/.openclaw/workspace/memory/apple-review-guidelines.md
Contains complete guidelines + pre-submission checklist. Pep Stack Pro was rejected 2026-03-24 for 2.1 + 1.4.1.

## Infrastructure & Decision Log

### Repository layout (verified April 18, 2026)

- This repo (website): github.com/SLMPhatty/thirty-website → local at ~/Projects/thirty-website/
- App lives in a separate repo: github.com/SLMPhatty/thirty-seconds → local at ~/Projects/thirty/
- The two are fully independent — no shared history, no shared build, no shared deployment
- The thirty-website repo was created on April 18, 2026 specifically for this project. Before that, local changes here had been incorrectly pointed at the thirty-seconds remote, which caused divergent-history errors when trying to push.

### How deployment works (current, verified)

- Every push to origin main triggers a Vercel build via GitHub integration
- Vercel runs `npm run build` (which calls `vite build`), producing dist/
- dist/ contains index.html, privacy.html, support.html, healthcare.html, plus assets/ and copied static files from public/
- Vercel serves dist/ at thirty-website.vercel.app
- Vercel Authentication is OFF — site is publicly accessible

### Deprecated tooling

- Manual `vercel deploy` from this folder is deprecated. All deployments now come from git push → Vercel webhook.
- The previous package.json in this folder was a leftover copy of the thirty iOS app's package.json (expo, react-native, react-native-iap, etc.). It had no "build" script and no vite dependency, which meant `npm run build` always failed. Any earlier Vercel builds either deployed an empty or stale dist/. Do not restore that package.json. The current minimal Vite-only package.json is correct.
- The thirty iOS app's src/, App.tsx, and related React Native source files were previously present in this folder as copy artifacts and have been deleted (commit 9c27cf4). They are not used by the website.

### Build commands

- `npm install` — install dependencies (just Vite; ~10 packages)
- `npm run dev` — local dev server at localhost:5173
- `npm run build` — production build to dist/
- `npm run preview` — preview the production build locally

### Key commits

- a2f14c8 (April 18, 2026) — corrected support.html duration list (30s/1m only, removed stale 3m/5m/10m/15m); added breathing patterns bullet under unlock features
- 9c27cf4 (April 18, 2026) — restructured folder as a proper Vite static site: replaced app-leftover package.json with Vite-only config, regenerated package-lock.json (663 packages → 10), deleted App.tsx and src/ (React Native app artifacts), expanded .gitignore, untracked previously-committed node_modules/ and dist/
