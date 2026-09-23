# Competitive analysis: Turo

Public-facing worked example of the competitive research process, applied to Turo (https://turo.com). Framing lens: New Zealand market entry - competitive tension, cultural fit for peer-to-peer car sharing, and how sports partnerships could build Turo's brand there. Started 2026-09-21.

This repo is destined to be **public**. Write everything accordingly.

## Standing rules (these override skill instructions where they conflict)

1. **No git commits until the publish gate passes.** There is deliberately no git repo until phase 8 of the run; skip any commit step a skill instructs, including setup's. History starts clean or not at all.
2. Every claim is labelled: `- Observed: [claim] ([URL])` or `- Inferred (assumption): [claim]`. An Observed claim with no URL is mislabelled.
3. **One claim, one fact.** Split compound bullets so each fact carries its own label and can be verified on its own.
4. Analysis files represent **current state**: regenerate in place, never append dated update sections.
5. Never hand-edit `index.html`; rebuild it with `/build-dashboard`.
6. The `.gitignore` here is publish-mode (four lines, the last being `assets/`). It must never ignore `profiles/`, `analysis/`, or `reference/` content; that content is the product.
7. No em dashes anywhere, whether typed directly or written out as an HTML entity. No absolute local paths. Nothing about any job application or the repo's audience.
8. Verification wording: sourced claims are **re-checked against the pages they cite**, never "verified true".
9. Before anything ships: `python3 check.py` must exit 0. Do not weaken a check to get past it.

## Commands

| Command | What it does |
|---|---|
| `continue the employer demo run` | Resume the run at the phase STATE.md records |
| `/scan-competitors` | Light first-population pass over profile stubs |
| `/competitive-update --competitor <name>` | Full-depth research on one competitor |
| `/generate-analysis <topic>` | Cross-competitor analysis (employer mode: overwrite, no export) |
| `/build-dashboard` | Regenerate the self-contained dashboard |
| `python3 check.py` | The publish gate |

## Going broader on request

Full-depth research on the named competitor, citation check into `analysis/verification-note.md`, **regenerate the analysis**, rebuild the dashboard, run the gate, commit. In that order; skipping the analysis regeneration leaves the dashboard contradicting the profiles.

## Run configuration

- Company: Turo (https://turo.com)
- Framing lens: New Zealand market entry - competitive tension, cultural fit for peer-to-peer car sharing, and how sports partnerships could build Turo's brand there
- Additional depth requested: Turo's unit economics and commercial model (take rate, insurance/protection revenue, host mix) covered as company-background context in the product-info write-up, as a learning interest rather than part of the cross-competitor comparison spine
- Competitor brief: 5 competitors, a mix of global peer-to-peer rivals, traditional rental incumbents, and at least two NZ-specific car-share players, so the NZ read has local grounding
- Markets: New Zealand
- Deep-dive pick: Mevo, Cityhop, and Zilch (formerly Yoogo Share), taken deep together rather than the usual single pick, because all three compete directly in the same local market and the light pass surfaced findings (Mevo's March 2026 collapse, and its shared ownership with Zilch under Carbn Group) that were worth triangulating. GO Rentals and Getaround stayed at survey depth.
- Publish date: 2026-09-22
