---
name: employer-demo-run
description: Continue an employer-facing competitive-analysis demo run from where STATE.md says it is - setup, light scan, deep dive with citation check, analysis, dashboard, README, publish gate. Run from inside the instance repo (the one scaffolded by employer-demo-scaffold). Use for "continue the employer demo run" or "/employer-demo-run".
---

# employer-demo-run

Drives phases 2-8 of the employer demo. Read `STATE.md` first and resume at the phase it records; update its `Phase:` line after completing each phase. If `STATE.md` is missing and the repo is already published, you are probably being asked for the go-broader loop (bottom of this file).

Standing rules for the whole run (also in this repo's CLAUDE.md):

- **No git commits until phase 8.** There is deliberately no git repo yet. Skip any commit step another skill instructs, including setup's.
- Every claim labelled Observed (with URL) or Inferred. One claim, one fact: never pack a date, a product list, and a person into one bullet.
- No em dashes anywhere, including HTML entities.
- This repo will be public. Nothing about any job application, no internal notes, no absolute local paths.

## Phase 2: setup

Follow the `setup` skill's quick-start path against the URL in STATE.md, with three overrides:

1. When proposing the profile template (setup Phase 3), derive the custom sections from the **framing lens** in STATE.md and mark the 2-3 lens sections `(core)` in `reference/guidelines.md` - the light pass populates only those.
2. Propose competitors per the **competitor brief** in STATE.md, using web search; the user approves the list. Record who was deliberately left out and why in `reference/competitors.md` - the README uses it.
3. **Skip setup's post-setup CLAUDE.md overwrite and commit steps.** The employer CLAUDE.md already exists, and there is no git repo yet by design.

## Phase 3: light pass

Run the `scan-competitors` skill across all competitors.

## Phase 4: deep dive

1. From the light pass, propose ONE competitor for the deep dive with a **written justification** - why this one matters most to the company right now. The justification goes into the analysis and onto the dashboard, not just into chat. The user approves or redirects the pick.
2. Research the pick at full depth: follow the `competitive-update` skill's research method (its Steps 1-2) against every section of the profile template, writing as first population with a single batched approval. Set the header to `Depth: full`.
3. **Citation check** - this is what the demo demonstrates, so do it exactly:
   - First split any remaining compound Observed bullets (one claim, one fact).
   - For each Observed claim in the deep profile, WebFetch the cited URL.
   - A claim **passes** only if you can copy a **verbatim quote** from the fetched page that supports the specific fact, into `analysis/verification-note.md` next to the claim. If it cannot be quoted, it fails.
   - A fetch that returns a 404, a paywall, a consent wall, a robots block, or an empty JS shell is **unverifiable**. Unverifiable means downgrade, never silent retention: relabel the claim `- Inferred (assumption): [claim] (cited URL unverifiable on YYYY-MM-DD)`.
   - `analysis/verification-note.md` format: date, counts (checked / passed / downgraded), then one entry per claim: the claim, the verbatim quote, the URL.
   - Wording rule everywhere this is described: claims were **re-checked against the pages they cite**, not verified true. A vendor's marketing figure that its own page supports is still a vendor claim; keep it marked as one.

## Phase 5: analysis

Follow the `generate-analysis` skill's method on the framing lens, with employer-mode overrides:

- **Overwrite in place.** The analysis file represents current state; no dated update sections, no append log.
- **Decline the HTML export step.** The dashboard is the export; `exports/` is not on the publish allowlist.
- Scope honestly: the matrix works at snapshot level with inferred cells marked; deep cross-competitor claims are only made where the deep profile supports them.
- End with a **"What going broader adds"** section: one entry per survey-depth competitor naming the specific questions a full profile would answer. This is the reader's call to action.

## Phase 6: dashboard

Run the `build-dashboard` skill end to end: asset capture and the look at every image, brand tokens, the build, `assets.py embed`, check.py, the rendered-pixel checks, and the samantha design review (required for the first two runs on the v2 design system). Capture needs Google Chrome installed and network access.

## Phase 7: README

Write `README.md` from `templates/employer-readme.md.template`, filling every placeholder. Keep the sourcing wording rule from phase 4 and the not-affiliated line. Read it once as prose before moving on: headlines must say something, no em dashes, no intensifier tics.

## Phase 8: gate, then git, then publish checklist

1. Fold the run configuration from `STATE.md` into CLAUDE.md's "Run configuration" section, then **delete `STATE.md`**.
2. Run `python3 check.py` from the repo root. Fix findings and re-run until it exits 0. Do not weaken a check to get past it; if a check is wrong, that is a conversation, not an edit.
3. Only now: `git init`, `git add -A`, and a single commit describing the analysis.
4. Present the manual publish checklist. **Never create the remote or push yourself:**
   - Create a **private** GitHub repo named `<Company>-Competitive-Analysis`; push `main`.
   - Review the repo on GitHub as the employer would: README, every profile, the dashboard file, no strays.
   - Flip to public. Enable Pages (deploy from `main`, root).
   - Verify the live URL: dashboard renders with every screenshot and logo, both themes, phone width, README links resolve.

## The go-broader loop

When the reader asks for depth on another competitor:

1. Research that competitor at full depth (competitive-update method), set `Depth: full`.
2. Citation check per phase 4; extend `analysis/verification-note.md`.
3. **Regenerate the analysis** (phase 5 rules). Skipping this leaves the dashboard rendering an analysis that contradicts the profiles.
4. Rebuild the dashboard.
5. `python3 check.py`, then commit.
