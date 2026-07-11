# Deploy the ANU site (live, with working checkout)

The site is `index.html` — one self-contained file. The 3D hero needs no server,
but **checkout needs the page hosted on a real host** (Gumroad's script can't run
from a `file://` or inside a Claude Artifact). GitHub Pages is free and takes ~5 min.

## Step 1 — Put your real Gumroad links in
Open `index.html`, find the config block near the bottom `<script>`:

```js
const GUMROAD = {
  template:   "https://andrekingfox.gumroad.com/l/anu-template",    // $47
  buildalong: "https://andrekingfox.gumroad.com/l/anu-buildalong",  // $97
  dfy:        "https://andrekingfox.gumroad.com/l/anu-dfy",         // $297
};
const DISCORD_URL = "https://discord.gg/hKkSgUZWeQ";
const USE_OVERLAY = false;   // true = checkout opens as an overlay ON the page
```

Replace the three URLs with your actual Gumroad product links (you get these after
you publish each product). `USE_OVERLAY = false` keeps your button design and sends
buyers to Gumroad's checkout page. Flip to `true` if you want the checkout to pop
up as an overlay without leaving the page (it will use Gumroad's button styling).

## Step 2 — Host it free on GitHub Pages
```bash
cd /Users/andrefox/TRADING/anu-site
git init && git add index.html && git commit -m "ANU site"
gh repo create anu-site --public --source=. --push     # needs the gh CLI, already installed
gh api -X POST repos/andrefox1207/anu-site/pages -f source.branch=main -f source.path=/  # enable Pages
```
Your site is live at: `https://andrefox1207.github.io/anu-site/`
(Give it ~1 minute the first time.)

Prefer clicking? On github.com: new repo → upload `index.html` → Settings → Pages →
Source: `main` / root → Save.

## Step 3 — Point your bio at it
Put `https://andrefox1207.github.io/anu-site/` on `link.me/andrekingfox` (or buy a
custom domain later and point it here). That's your funnel destination.

## Alternatives to GitHub Pages
- **Netlify Drop** — drag the folder onto app.netlify.com/drop. Instant, free.
- **Vercel** — `npx vercel` in this folder.
- **Gumroad only** — skip hosting entirely and just send people to your Gumroad
  product pages. Less slick, zero setup. The site is what makes it premium.

## What's already handled
- The 3D neural-brain hero (self-contained, mobile-safe, respects reduced-motion)
- Live boot terminal, HUD frame, scroll reveals
- All copy, pricing tiers, FAQ, founder note
- `gumroad.js` is already included for overlay checkout
