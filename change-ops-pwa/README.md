# Change-Ops

A single-file React PWA that does for business change what **career-ops** does for job offers: a weighted **decision-gate** engine for a portfolio of change initiatives. Same skeleton, retargeted domain.

- **Assess** each change: a canvas, a six-axis technology-readiness rating, and value scores.
- **Prioritise** the portfolio: a weighted 1–5 score with a gate verdict (Proceed now / Proceed / Proceed with caveats / Hold / Reject), plus a RICE lens.
- **Critique**: a constructively-framed red-team that yields a robustness tier (Robust / Caution / Fragile) and surfaces risks and mitigations.
- **Patterns**: portfolio-wide readiness gaps, recurring concerns, and a delivery funnel.

The readiness axes, ownership/delivery-model recommendation and critique signals are grounded in the BT SIMPLIFY and Delivery Framework material (technology readiness, the DigiCo ownership criteria, and Prosci's "people side is the #1 obstacle").

## What's in here

```
index.html               the whole app (React + Babel, editable in place)
manifest.webmanifest     PWA manifest (relative paths)
sw.js                    service worker (offline + installable)
icons/                   app icons (192, 512, maskable, apple-touch, favicon)
README.md                this file
```

## Deploy to GitHub Pages

All paths are **relative**, so it works at the repo root or in any subfolder.

**Option A — at the root of `dlockwood13.github.io`** (served at `https://dlockwood13.github.io/`).
Drop these files into the root of the repo and push. Note this becomes your site's homepage.

**Option B — in a subfolder** (served at `https://dlockwood13.github.io/change-ops/`), which keeps your homepage free.
Put the files under `change-ops/` in the repo and push:

```
git add change-ops
git commit -m "Add Change-Ops PWA"
git push
```

**Option C — a dedicated project repo.** Create a repo, add these files, then Settings → Pages → Deploy from branch → `main` / root.

GitHub Pages serves over HTTPS with correct MIME types, which is all the service worker and manifest need.

## Install it (turn it into an app)

A service worker and manifest only activate when the site is served over HTTPS (i.e. on GitHub Pages, not when opening `index.html` from disk). Once deployed:

- **Desktop Chrome / Edge:** click the install icon in the address bar, or use the **Install app** button in the sidebar.
- **Android Chrome:** menu → *Add to Home screen* (or the install button).
- **iPhone / iPad Safari:** Share → *Add to Home Screen*.

Installed, it opens in its own window and works offline.

## Offline behaviour

On the first online visit the service worker caches the app shell and the React/Babel runtime. After that the app loads and runs with no network. The sidebar shows **Offline ready** once that has happened.

Your data lives in this browser's local storage. Use **Export portfolio** for a portable JSON backup, and **Import portfolio** to load it elsewhere (see the import guide and template if you have them). Import replaces the portfolio; it does not merge.

## Editing

The app is plain React with Babel transforming JSX in the browser, so there is **no build step**. Open `index.html`, edit the JSX inside the `<script type="text/babel">` block, commit, done.

The scoring lives in two functions near the top of that script: `recommendModel` (ownership and delivery-model logic) and `metrics` (readiness, weighted priority, risk penalty, verdict and tier). The readiness axes, priority dimensions, critique signals and default weights are the `READINESS`, `DIMS`, `SIGNALS` and `DEFAULT_WEIGHTS` constants just above them.

## Updating the deployed app

When you change `index.html`, bump the `CACHE` constant at the top of `sw.js` (e.g. `change-ops-v1` → `change-ops-v2`) and push. The new service worker clears the old cache so every client picks up the change on next load.

## What's new in v2 — the four-phase methodology

The per-change workflow now follows four phases (a stepper at the top of **Assess**), with frameworks built into each:

1. **Intake** — Prosci 4 Ps (Project, Purpose, Particulars, People), change label, and current vs future state (gap analysis).
2. **Impact** — a Change Impact Matrix (stakeholder groups × L/M/H severity across processes, technologies, roles, culture), the six-axis technology-readiness radar with the ownership/delivery-model recommendation, and an application disposition using **Gartner TIME** (Tolerate / Invest / Migrate / Eliminate) with the matching cloud **6Rs**.
3. **Readiness** — an **ADKAR** assessment (Awareness, Desire, Knowledge, Ability, Reinforcement) that finds the **barrier point** (first element scoring 3 or below) and auto-generates a targeted mitigation plan (comms cadence, training schedule, leadership coaching, reinforcement).
4. **Prioritise** — the weighted priority dimensions and RICE, plus **MoSCoW** and a **delivery wave**, with the change's position on an **Impact vs Effort** 2×2.

Two new portfolio views support sequencing:

- **Prioritise** adds an Impact/Effort scatter of the whole portfolio and a MoSCoW board, alongside the ranked table.
- **Wave plan** sequences changes into delivery waves and shows a **change-saturation heatmap** (stakeholder groups × waves) so you can spot a department being asked to absorb too much change at once and rebalance.

The decision gate now blends three risk inputs: the red-team signals, ADKAR people-readiness, and impact severity. **Patterns** adds a portfolio-wide ADKAR rollup (your systemic barrier) and a TIME disposition spread.

Note: data from v1 is migrated automatically on first load; the new fields fill in as you work through the phases.
