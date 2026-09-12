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
