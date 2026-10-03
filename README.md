# Turo competitive analysis

A worked example of an AI-run competitive research process, applied to [Turo](https://turo.com). 6 competitors surveyed, three taken deep, framed on **New Zealand market entry: competitive tension, cultural fit for peer-to-peer car sharing, and how sports partnerships could build the brand there**.

**Start here: [the dashboard](https://cschubertwork.github.io/Turo-Competitive-Analysis/).** One page: the analysis first, with each competitor's homepage and the exhibits behind every finding, then how the process works. It is a single self-contained HTML file ([`index.html`](index.html)) with the images and fonts embedded and no external requests, so it also works offline if you clone the repo.

The profiles and analysis were produced by running the skills in [`.claude/skills/`](.claude/skills), and the dashboard is rendered from them by the `build-dashboard` skill. You can run the same process on your own company.

## What it found

Turo has no New Zealand presence, so this reads a hypothetical entry against the field. The first version of this analysis argued that Turo's no-fleet model was the answer to the failures of Mevo and Getaround. A full re-check on 3 October 2026 found that Getaround also owned no fleet: it ran the same marketplace model as Turo and failed on losses larger than its revenue and on debt. The finding now is that both of New Zealand's earlier peer-to-peer car platforms (YourDrive and MyCarYourRental) have gone and owning no cars didn't save Getaround, so a Turo launch would start with no hosts in a market where the model hasn't yet lasted for cars. The re-check also found Camplify, a live peer-to-peer campervan marketplace that owns every such platform in the country; showed that Cityhop belongs to Toyota Financial Services, which also owns Ezi Car Rental, the top-rated rental brand; and established that hiring out a car in New Zealand needs a rental-service licence, and that rental cars need a Certificate of Fitness. No competitor uses sports sponsorship, and Turo has done it before, as an official partner of Canada Basketball.

## The competitors, and why these

Six competitors: Mevo, Cityhop, and Zilch (New Zealand's three car-share operators), Camplify (New Zealand's live peer-to-peer campervan marketplace, added after the re-check found it missing), GO Rentals (an NZ-owned traditional rental incumbent, chosen over an international agency brand as the sharper trust comparison), and Getaround (Turo's closest global peer-to-peer rival, kept in the set because it ran Turo's model and still failed, even though it never operated in New Zealand).

[`reference/competitors.md`](reference/competitors.md) also lists who was deliberately left out and why.

## Survey depth, and three taken deep

3 of the 6 profiles are at survey depth: snapshot plus the framing dimensions, from a handful of sources each. **Mevo, Cityhop, and Zilch** got the full treatment together, where a run would usually take one company deep, because all three compete directly with each other in the same local market and the light pass surfaced findings (Mevo's collapse and its shared ownership with Zilch) that were worth triangulating across all three.

Every profile was then re-checked on 2026-10-03, including the claims first marked as inferred, against a verbatim quote from a fetched page, the New Zealand Companies Office register, or SEC filings. The results, including two corrections from the first pass that turned out to be wrong themselves, are in [`analysis/verification-note.md`](analysis/verification-note.md). Claims were re-checked against their citations, not verified true: a vendor figure its own page supports is still a vendor claim, and stays marked as one.

If GO Rentals, Camplify or Getaround matters more to you than this pass suggests, ask. A full profile with the same verification takes the process a few hours.

## How to read the sourcing

Every claim in every profile carries one of two labels:

- `- Observed: [claim] ([URL])` is a fact with a source attached
- `- Inferred (assumption): [claim]` is a judgement that nobody published

106 of the 107 factual claims in the profiles (99%) carry a source checked against the page on 3 October 2026. The other 49 labelled claims are 39 judgements, which can't have a source and stay Inferred however well argued, and 10 negatives backed by logged searches. Counted as labels, that is 106 Observed and 50 Inferred out of 156 (68% and 32%). The deep profiles carry most of the inference (59 to 67% Observed), because their differentiator, risk and opportunity sections are judgement by design. The dashboard shows the same count, and the inferred cells in the comparison matrix are individually marked.

## Layout

```
reference/          product positioning, competitor list, profile template, design system
profiles/            one profile per competitor (3 survey depth, 3 full)
analysis/            the cross-competitor analysis and the verification note
index.html           the dashboard, one self-contained page
.claude/skills/      the skills that produced all of the above
templates/           scaffolding used by /setup for a new company
check.py             the publish gate this repo passed before going public
```

## Running it on your own company

With [Claude Code](https://claude.com/claude-code) in this directory:

```
/setup                          # your product, your competitors, your comparison template
/scan-competitors               # survey-depth pass over every competitor
/competitive-update --competitor <name>   # take one deep
/generate-analysis <topic>      # cross-competitor analysis on any dimension you name
/build-dashboard                # regenerate the dashboard from the current state
```

## Caveats

This is desk research from public sources, produced on 2026-09-22 and re-checked on 2026-10-03. There are no win/loss interviews, customer calls or analyst briefings behind it. Published announcements are a lagging and partial view of what any company has running with customers, so nothing here should be read as an audit of a competitor's internal capability. Fleet and membership figures for the New Zealand competitors are the most recent numbers any public source disclosed and may not be current; Cityhop's latest is from 2022. The dashboard takes its accent from Turo's public brand colour (#593CFB, read from turo.com's own stylesheet) and sets type in Figtree, an open-licence stand-in for Turo's own typeface. Competitor logos and homepage screenshots identify each company and belong to their owners; the screenshots were captured from public homepages on 2026-09-23.

Not affiliated with Turo or any company named here. All trademarks belong to their owners.
