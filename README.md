# Cosmic Ages

A single-page, single-file web app by **IncredibleSwipe Studio**.

Live counters for how many days Earth, the Moon, and Mars have existed, plus a
personal comparison: enter your date of birth to see your own day-count next
to theirs, a timeline of real historical events that happened during your
lifetime, and a downloadable share card / 10-second video of the result.

No backend, no database, no build step. It's one static HTML file
(`index.html`) with everything — CSS, JavaScript, canvas rendering — inline.

## Run it locally

Just open `index.html` in a browser. That's it — no install, no server.

If you want a local dev server (some browsers restrict certain features when
opening a file directly via `file://`), any static server works, e.g.:

```bash
npx serve .
```

## Deploy — Cloudflare Pages (recommended, free)

Cloudflare Pages' free tier has no bandwidth cap and allows commercial use,
which is why it's the pick here over Netlify/Vercel.

1. Push this folder to a new GitHub repository.
2. Go to the [Cloudflare dashboard](https://dash.cloudflare.com) → **Workers & Pages** → **Create application** → **Pages** → **Connect to Git**.
3. Select this repository.
4. Build settings: leave the build command **empty** and set the output
   directory to `/` (root) — this is a static file with no build step.
5. Deploy. You'll get a free `*.pages.dev` URL immediately.
6. (Optional) Add a custom domain or subdomain under
   **Custom domains** in the Pages project settings, e.g.
   `cosmicages.incredibleswipe.com`, if you own that domain.

Every future `git push` to the connected branch auto-deploys.

## Project structure

```
.
├── index.html      # the entire app — markup, styles, and script
└── README.md
```

Everything lives in `index.html` on purpose — there's no build tooling to
maintain, no dependency versions to keep in sync. If this grows into
something bigger (payment flow, multiple pages), it's worth splitting out
`styles.css` / `app.js` at that point, but for a single-page share tool this
keeps deployment as simple as possible.

## Roadmap / notes

- **Watermark removal (premium unlock)** — planned once Razorpay is approved.
  The `.watermark` element in `index.html` and the brand text drawn in the
  video export (`drawFrame` function, near the bottom of the `<script>`
  block) are the two places branding is injected — both are the toggle
  points for a paid "remove watermark" tier.
- **Friend-comparison mode** — flagged as the highest-leverage feature
  addition if this needs to support more than one-time use per visitor.
- **`.mp4` export** — current video export produces `.webm` (browser-native,
  no extra libraries). Works on WhatsApp/Android/Chrome; iOS/Instagram
  sharing may need a conversion step, which would require either a small
  server-side encode or a heavier in-browser encoder library.
- **Historical event data** lives in the `EVENTS` array in `index.html` —
  add entries there (format: `['YYYY-MM-DD', "Event title"]`) to expand the
  timeline over time.
