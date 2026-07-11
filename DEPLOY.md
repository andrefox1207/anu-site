# Deploy & configure the ANU site

The site is **live** at **https://andrefox1207.github.io/anu-site/** (GitHub Pages, free).
It's one `index.html` + `/assets` (the demo video + poster) + `sitemap.xml` + `robots.txt`.

## The one config block (top of the `<script>` in `index.html`)
```js
const GUMROAD = {
  template:   "https://andrekingfox.gumroad.com/l/anu-template",   // ← your real URLs
  buildalong: "https://andrekingfox.gumroad.com/l/anu-buildalong",
  dfy:        "https://andrekingfox.gumroad.com/l/anu-dfy",
};
const DISCORD_URL     = "https://discord.gg/hKkSgUZWeQ";
const BRAND           = "ANU";
const USE_OVERLAY     = false;   // true = Gumroad checkout opens as an on-page overlay
const EMAIL_ENDPOINT  = "";      // paste a Formspree URL to turn the waitlist live
const PLAUSIBLE_DOMAIN = "";     // paste your Plausible domain to turn analytics on
```
Change anything here → `git push` → Pages redeploys in ~1 min.

## Redeploy after an edit
```bash
cd /Users/andrefox/TRADING/anu-site
git add -A && git commit -m "update" && git push
```

## Turn on the extras (optional, free tiers)
- **Waitlist:** create a form at formspree.io, paste its `https://formspree.io/f/xxxx` URL into `EMAIL_ENDPOINT`. Until then the form shows a friendly "you're on the list" and just fires an analytics event.
- **Analytics + A/B readout:** add the site as a domain in Plausible, paste the domain into `PLAUSIBLE_DOMAIN`. Events already wired: page + variant, CTA clicks, `begin_checkout`, `discord_join`, `faq_open`, scroll depth, `video_play`, `waitlist_submit`.
- **A/B:** the hero headline auto-splits `?v=a` ("Build your own JARVIS.") vs `?v=b` ("Steal what works."), sticky per visitor, attributed in analytics. Force a variant with `?v=a` / `?v=b`.

## Hard truths
- **Must stay hosted.** The Gumroad script, Google Fonts, Lenis, and analytics are external — they run on Pages/Vercel/Netlify but **not inside a Claude Artifact** (CSP blocks external scripts). A Claude preview is a stripped fallback; the checkout-working site is this hosted file.
- **Buttons degrade gracefully:** if `gumroad.js` fails, CTAs still navigate to the product page.

## The demo video (free)
`assets/demo.mp4` + `.webm` + `demo-poster.jpg` are a real screen-recording of ANU LENS. To regenerate a slicker version later, you *could* use the Motion MCP (`mcp.motion.so`) — brief: *"30s product demo of ANU LENS: paste a reel, it scores the hook, chat returns hooks; dark UI, coral accent, no voiceover."* — but that spends credits and is **unfunded/optional**. The current demo ships free.

## Alternatives to GitHub Pages
- **Netlify Drop:** drag this folder onto app.netlify.com/drop.
- **Vercel:** `npx vercel` in this folder.
