# Willard Insurance — Account Hub

A self-contained static site that serves as the GOAL reporting hub for **Willard
Insurance** (Account #958). The landing page previews and links to the client
report; the report is a standalone, print-friendly HTML document.

## Structure

```
.
├── index.html                                  # Landing page (Account Hub)
├── reports/
│   └── onboarding-recap-and-launch-plan.html   # Onboarding Recap & Launch Plan report
├── assets/                                     # GOAL brand marks (logos, favicon)
│   ├── goal-mark.png
│   ├── goal-wordmark-white.png
│   └── goal-wordmark-black.png
└── vercel.json                                 # Static hosting config (headers, caching)
```

There is no build step — these are plain HTML files using Google Fonts (Inter)
and inline CSS. Brand assets and report links use relative paths, so the site
works both when served and when opened directly from disk.

## View locally

Open `index.html` in a browser. The landing page embeds a live preview of the
report in an iframe and links to the full document.

> Most browsers allow the iframe preview to load over `file://`. If your browser
> blocks it, run a tiny local server instead:
>
> ```bash
> python3 -m http.server 8000
> # then visit http://localhost:8000
> ```

## Deploy on Vercel (via GitHub)

This repo is ready for a zero-config static deployment.

1. In the [Vercel dashboard](https://vercel.com/new), **Import** the
   `TomsTools11/willard-insurance-reporting` GitHub repository.
2. Leave the defaults:
   - **Framework Preset:** `Other`
   - **Root Directory:** `./`
   - **Build Command:** *(none — leave empty)*
   - **Output Directory:** *(none — leave empty; files are served from the repo root)*
3. Click **Deploy**.

Vercel detects the `index.html` at the repo root and serves the site statically.
After the first import, every push to the connected branch triggers a new
production deploy, and every pull request gets its own preview URL.

Routes once deployed:

- `/` → landing page
- `/reports/onboarding-recap-and-launch-plan.html` → full report

### Configuration notes

`vercel.json` sets long-lived caching for `/assets/*`, a `nosniff` content-type
policy, a `SAMEORIGIN` frame policy (so the landing page can embed the report in
its same-origin preview iframe), and a sensible referrer policy. Clean URLs are
intentionally left **off** so the `.html` links resolve identically whether the
site is served by Vercel or opened straight from disk.

The pages are marked `noindex` because this is a client-specific account hub
rather than public marketing content.
