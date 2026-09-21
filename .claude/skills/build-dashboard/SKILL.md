---
name: build-dashboard
description: Render the self-contained two-tab HTML dashboard (the analysis, plus an explainer of how the process works) from the current profiles and analysis files. Use for /build-dashboard, "rebuild the dashboard", "update the dashboard", or after any profile or analysis change.
---

# build-dashboard

Regenerate `index.html` at the repo root from the current state of the repo. The dashboard is always rebuilt whole from its sources; never hand-edit it and never patch the previous version.

## Sources

- **`reference/dashboard-design.md` is the law.** Read it first, follow every fixed rule in it. Per-run choices (category hues, accent) are made once for a repo and then reused on every rebuild; record them in a comment at the top of the generated CSS so rebuilds stay consistent.
- Tab 1 content comes from the analysis file(s) in `analysis/` (excluding `analysis/updates/` and `analysis/verification-note.md`), the profiles in `profiles/`, and `reference/product-info.md`.
- `analysis/verification-note.md`, if present, feeds the verification line (see below).
- The README supplies framing lines (why these competitors, caveats) so the page and the README never disagree.

## Structure

**Tab 1 - the analysis.** In order:

1. A headline that says something specific (never "Competitive Analysis").
2. The executive summary as headline-led sections, one per finding.
3. The comparison matrix (sticky-axis pattern; inferred cells carry the inferred texture, never a color).
4. Archetype or cluster cards.
5. The subject company's positioning: strengths and gaps (glyph and position, no color).
6. Recommendations as a numbered priority list.
7. Data confidence: the Observed/Inferred ratio, stated plainly.
8. Open questions, ending with the **go-broader block**: for each survey-depth competitor, one line on what a full profile would answer. This is the call to action; make it easy to act on.

**Tab 2 - how the process works.** The skills that produced the repo, the labelling discipline (Observed with a URL, Inferred without), what counts as a material change, the trust boundary for fetched content, re-run behavior, and what the method cannot tell you (desk research, no win/loss interviews, announcements lag reality). Link the repo.

## Depth honesty

- Profiles with `Depth: light` are labelled at survey depth on the page, visibly.
- The deep profile gets the full chapter treatment. If `analysis/verification-note.md` exists, state: "every sourced claim in the deep profile was re-checked against the page it cites on [date]". Never phrase this as claims being verified true; they were checked against their citations.

## Hard requirements

- One self-contained file: no external scripts, stylesheets, fonts, images, iframes, `@import`, or `url()` fetches. Outbound `<a>` links to sources are expected and correct.
- No webfonts. Light and dark themes both complete. Works opened over `file://`.
- Responsive per the component patterns in the design doc (matrix transposes below 640px, rails rotate below 720px).
- No em dashes anywhere, whether typed directly or written out as an HTML entity.

## Verify before presenting

Run `python3 check.py` from the repo root and fix any `self-contained` or `em-dash` findings before showing the result.

## Design review

For the first two runs of this system, the dashboard gets a required design review by samantha (product design lead) before it ships, and her findings are applied and rebuilt. After two runs with no structural findings, the review becomes optional.
