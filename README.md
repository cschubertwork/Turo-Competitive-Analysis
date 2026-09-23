# Turo competitive analysis

A worked example of an AI-run competitive research process, applied to [Turo](https://turo.com). 5 competitors surveyed, three taken deep, framed on **New Zealand market entry: competitive tension, cultural fit for peer-to-peer car sharing, and how sports partnerships could build the brand there**.

**Start here: [the dashboard](https://cschubertwork.github.io/Turo-Competitive-Analysis/).** One page: the analysis first, with each competitor's homepage and the exhibits behind every finding, then how the process works. It is a single self-contained HTML file ([`index.html`](index.html)) with the images and fonts embedded and no external requests, so it also works offline if you clone the repo.

The profiles and analysis were produced by running the skills in [`.claude/skills/`](.claude/skills), and the dashboard is rendered from them by the `build-dashboard` skill. You can run the same process on your own company.

## What it found

Turo has no current New Zealand presence, so this is a hypothetical entry read against the field, not a market-share snapshot. The standout finding is a pattern rather than a single fact: Mevo, reported as Wellington's car-share leader, collapsed into voluntary administration in March 2026, and Getaround, Turo's closest global peer, is mid-liquidation the same year. One is local and one is global, and both point at the same weakness in fleet-owned or fleet-financed car sharing. New Zealand's car-share field is also more consolidated than five names suggests: Mevo and Zilch now share an owner (Carbn Group), and Cityhop sits inside Toyota NZ. No competitor profiled here, car-share or traditional rental, uses sports sponsorship for brand-building, which reads as open ground rather than contested share.

## The competitors, and why these

Five competitors: Mevo, Cityhop, and Zilch (New Zealand's three car-share operators), GO Rentals (an NZ-owned traditional rental incumbent, chosen over an international agency brand as the sharper trust comparison), and Getaround (Turo's closest global peer-to-peer rival, kept in the set as a live lesson in what breaks this model's economics even though it never operated in New Zealand).

[`reference/competitors.md`](reference/competitors.md) also lists who was deliberately left out and why.

## Survey depth, and three taken deep

2 of the 5 profiles are at survey depth: snapshot plus the framing dimensions, from a handful of sources each. **Mevo, Cityhop, and Zilch** got the full treatment together, rather than the usual single deep dive, because all three compete directly with each other in the same local market and the light pass surfaced findings, Mevo's collapse and its shared ownership with Zilch, that were worth triangulating rather than picking just one.

The deep profiles are also where the verification discipline is on display: every sourced claim in them was re-checked against the page it cites on 2026-09-22, with a verbatim supporting quote recorded in [`analysis/verification-note.md`](analysis/verification-note.md). Claims whose sources could not be reached or did not support them were downgraded to inferred, visibly. Re-checked against their citations, not verified true: a vendor figure its own page supports is still a vendor claim, and stays marked as one.

If GO Rentals or Getaround matters more to you than this pass suggests, ask. A full profile with the same verification takes the process a few hours, not weeks.

## How to read the sourcing

Every claim in every profile carries one of two labels:

- `- Observed: [claim] ([URL])` is a fact with a source attached
- `- Inferred (assumption): [claim]` is a judgement that nobody published

Of the 125 labelled claims in the profiles, 65 (52%) are Observed and 60 (48%) Inferred. The three deep profiles carry most of the inference, at 45 to 49% Observed: their differentiator, risk and opportunity sections are judgement by design, and the citation check downgraded every claim it couldn't re-check. The two survey-depth profiles are 75 to 88% Observed because they only cover the core framing sections. The dashboard shows the same count, and the inferred cells in the comparison matrix are individually marked.

## Layout

```
reference/          product positioning, competitor list, profile template, design system
profiles/            one profile per competitor (2 survey depth, 3 full)
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

This is desk research from public sources, produced on 2026-09-22. There are no win/loss interviews, customer calls or analyst briefings behind it. Published announcements are a lagging and partial view of what any company has running with customers, so nothing here should be read as an audit of a competitor's internal capability. Fleet and membership figures for the New Zealand competitors are, in most cases, the most recent numbers any public source disclosed, not necessarily current; several are from 2020 or earlier. The dashboard takes its accent from Turo's public brand colour (#593CFB, read from turo.com's own stylesheet) and sets type in Figtree, an open-licence stand-in for Turo's own typeface. Competitor logos and homepage screenshots identify each company and belong to their owners; the screenshots were captured from public homepages on 2026-09-23.

Not affiliated with Turo or any company named here. All trademarks belong to their owners.
