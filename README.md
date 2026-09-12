# landxland.de — Land × Land

The published site: model-based estimates of political sentiment in all sixteen
German states, for the Landtage and for the Bundestag.

**This repository holds the built site, not its source.** Everything here is
generated — the compiled app in `assets/`, and the data in `data/`, which comes
out of the estimation pipeline. Edits made here are overwritten by the next
publish; the source and the model live in the private pipeline repository.

## What is in it

```
index.html            the app shell
assets/               compiled JS and CSS, content-hashed
data/                 what the model produced — the only part that changes often
  manifest.json       which run this is: vantage date, model, draw count
  meta.json           parties, states, the election calendar and its rules
  unit/<code>.json    one file per unit: "de" plus the sixteen states
  economic.json       ifo, unemployment, inflation (fetched on demand)
  federal_by_state.json   per-state Bundestag medians (fetched on demand)
  polls.json, summary.json
fonts/                Source Serif 4, subset (SIL Open Font License, see OFL.txt)
maps/, brand/         state geometry and the site's mark
CNAME                 landxland.de
.nojekyll             Pages serves the files as they are
```

## How it is published

GitHub Pages, from the `main` branch at the repository root. No build step runs
here: the site arrives already built.

A publish is one command in the pipeline repository:

```
website_draft/publish_site.sh
```

which rebuilds the app, syncs the result into this working tree, commits with
the run's vantage date, and pushes.

## Deploying it the first time

1. Create an empty repository on GitHub (no README, no licence — this tree is
   the initial commit).
2. `git remote add origin git@github.com:<user>/<repo>.git && git push -u origin main`
3. Settings → Pages → Source: *Deploy from a branch*, branch `main`, folder `/`.
4. Settings → Pages → Custom domain: `landxland.de`, then tick **Enforce
   HTTPS** once the certificate is issued.
5. DNS for the apex domain — four A records to `185.199.108.153`,
   `185.199.109.153`, `185.199.110.153`, `185.199.111.153`, and four AAAA
   records to `2606:50c0:8000::153`, `…8001::153`, `…8002::153`, `…8003::153`.
   Optionally a `www` CNAME to `<user>.github.io`.

The app routes on the URL hash (`#/by`, `#/methodik`), so no 404 fallback or
rewrite rules are needed.

## Notes

- About 13 MB on disk, ~2 MB over the wire: Pages compresses the JSON, and the
  app caches it in the browser between visits.
- After a publish, readers can see the previous dataset for up to ten minutes —
  Pages caches responses that long.
- The data is a summary of the model run: quantiles, seat draws and attribution
  components, not the posterior itself.
