# Dashboard design system

The visual identity for every HTML dashboard this project produces. It was locked during the ProcurePro run and is reused, not reinvented, for each new instance. Per-run decisions are marked; everything else is fixed.

## Concept

A tender comparison sheet, not a SaaS dashboard. The ground is grey-green paper (never cream, never white). Data and machine vocabulary are set in monospace; prose in a tight grotesque. Deliberately avoids SaaS blue and avoids the cream-and-terracotta editorial look.

## Palette

### Fixed neutrals (the system's identity, same in every instance)

- Light: paper `#F2F3EE`, raised `#FBFBF8`, ink `#171A16`, ink-2 `#4A5049`, ink-3 `#757C73`, rule `#D6D9D0`, rule-strong `#B7BCB2`
- Dark: paper `#101310`, raised `#181C18`, ink `#E8EBE4`, ink-2 `#A9B0A6`, ink-3 `#7C8479`, rule `#2A2F29`, rule-strong `#3C433B`
- Inferred steel `#6B7A8F` / dark `#8FA2B8` (state only, never decorative)

### Per-run hues (chosen once per instance, then locked)

Up to four category hues, one per strategic archetype the analysis names. Choose them **subject-native**: borrowed from a color code the subject industry actually uses, then desaturated to ink weight. The ProcurePro run borrowed the construction utility-locate marking code (water blue `#2B6C8F`/`#5FA8CC`, sewer green `#3E7A4E`/`#6FB981`, gas ochre `#9A7415`/`#D6A63C`, marking orange `#D6431B`/`#FF7A4D`). If the new industry has no native code, desaturate the neutrals' temperature range instead; never reach for a generic chart palette. The legend must say where the hues come from.

The **accent** is the target company's own brand color (adjusted to sit on the paper ground in both themes). The target company is the only participant that gets it; competitors stay monochrome.

**The accent is reserved outside the category palette.** If the brand color is not clearly distinguishable from every category hue in both themes, do not use the brand color: fall back to a high-ink neutral accent and say so in the legend. Hue never does double duty. (In the ProcurePro run the accent and the Decision-archetype hue happened to coincide; that was a coincidence of subject, not a rule to reproduce.)

## Encoding rules that must not be broken

- Hue carries archetype only. Strength is ink density, never a second hue.
- Observed vs Inferred is texture, never color: dotted underline, 45-degree hairline hatch, superscript `i`.
- The target company is distinguished by the accent, so competitors stay monochrome.
- Strengths and gaps get no color at all. Glyph and position do the work.

## Type

No webfonts (self-contained, file:// constraint). Display and body: `"Helvetica Neue", Helvetica, "Segoe UI", system-ui, sans-serif`, `letter-spacing: -0.02em` on headings. Everything machine-flavored (eyebrows, axis ticks, scale markers, commands, file paths, matrix figures): `ui-monospace, "SF Mono", Menlo, Consolas, monospace`, 11px uppercase with `letter-spacing: 0.14em` for labels. The mono is where the personality lives.

## Named component patterns

- **Moat bar**: Gantt-shaped range bar; right edge = proximity to margin, width = corpus breadth
- **Archetype cards**: 2x2 grid of cards, not a quadrant chart
- **Sticky-axis matrix** that transposes to a per-dimension accordion below 640px
- **Stepped rail** (rotates vertical below 720px)
- **Strength grid**: ink-density blocks that retain the source's own word
- **Stacked disclosure rows** for competitor detail
- **Numbered priority list** for recommendations

## Deliberately not charted

The comparison matrix, geography (no world map), data confidence (no donut), scale markers (incommensurable units), recommendations (no timeline; no dates exist). No radar charts, no sparklines.

## Hard requirements for any page built from this doc

- One self-contained HTML file: no external requests of any kind, no webfonts, no `@import`; must work opened over `file://`
- Light and dark themes both complete
- Headlines say something specific, never just label a section
- No em dashes anywhere in the copy
