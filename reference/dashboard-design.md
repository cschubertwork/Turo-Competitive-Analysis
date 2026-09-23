# Landscape dashboard design system (v2)

The visual law for every landscape repo's `index.html`. It replaces the v1 "tender comparison sheet" system (fixed grey-green paper, monochrome competitors, no imagery). Everything here is **fixed** unless it is marked **derived**, and derived values are produced by a procedure, never by taste on the day. Copy follows `reference/dashboard-voice.md`; this doc only governs what the words sit in.

Companion files:
- `derive_tokens.py`: turns one brand colour into the complete light and dark token set, contrast-checked. Run it; never hand-pick a hex.
- `assets.py`: implements section 8. `capture` takes the screenshots (consent dismissal, lazy-load scroll, and gates 1, 2 and 4 automated) and collects logo candidates and brand signals; `exhibit` takes crops; `font` fetches the typefaces; `embed` inlines everything. Gates 3 and 5 and the logo choice stay a visual check by the builder.
- `templates/dashboard.html`: the reference implementation (the Turo run). Start from it.
- The per-run block (section 12) is written once per repo as a comment at the top of the CSS and reused on every rebuild.

---

## 1. Who this is for, and the 10-second test

**Reader.** A product or leadership person at the target company who opens a link cold, from a message or a LinkedIn post, usually on a laptop and sometimes on a phone. They didn't ask for it. They are asking themselves two things: does this person understand our business, and is the work real?

**The page's job.** Answer both before the reader scrolls, then reward the reader who does scroll with evidence they can check.

**The 10-second test.** At 1440x900, with no scrolling, the reader must be able to see:
1. That this is independent work by a named person, about their company.
2. The headline finding, stated as a specific sentence.
3. The real market: every competitor's actual homepage and logo, with the ones in trouble visibly marked.
4. How far to trust it: the Observed/Inferred ratio and the re-check date.

If a build fails any of the four at the fold, it isn't finished.

## 2. Concept: the frame is the author's, the ink is the target's

Every landscape page is built from two layers, and keeping them apart is what makes the page read as tailored and independent at once.

- **The frame is fixed, and it's the author's.** Layout, grid, type scale, the mono annotation face, exhibit frames, capture captions, encoding textures, the byline. This stays the same across every company, so the series reads as one person's body of work, and so the page never looks like the target's own collateral.
- **The ink is derived, and it's the target's.** One accent from the target's brand colour, neutrals tinted toward that hue, a dark ground borrowed from the brand where it has one, and an open-licence typeface matched to the brand's type. That is what makes a Turo page feel made for Turo.
- **The evidence is theirs too.** Competitor homepages and logos appear as labelled exhibits, in full colour, inside the author's frame. Colour in imagery identifies companies. Colour in data marks is reserved (section 5).

The register is an analyst's briefing with exhibits. Real screenshots do the visual work that v1 tried to get from typography alone.

## 3. Page architecture

**One page, two parts, no tabs.** v1 hid the method behind a second tab, which meant the "why this compounds" pitch was the least-seen part of the page. v2 is a single scroll. Part 2 opens with a full-width band that changes register, and the masthead links straight to it. Deep links are plain anchors. The only script left is the theme toggle.

Order and anchors:

| # | Section | Anchor | Content source |
|---|---|---|---|
| 0 | Masthead (sticky) | | fixed |
| 1 | Hero: eyebrow, headline, standfirst, trust panel, cast strip | `#top` | analysis summary, counts, asset manifest |
| 2 | Findings, each paired with at most one exhibit | `#findings` | executive summary |
| 3 | The field: clusters, each holding player cards | `#field` | clusters + profiles |
| 4 | Comparison matrix | `#compare` | analysis matrix |
| 5 | Where the target stands: strengths, gaps, open ground | `#position` | positioning section |
| 6 | Lens deep-dive (optional; only when the analysis has one) | `#options` | e.g. "what a sports partnership could look like" |
| 7 | Recommendations | `#recommendations` | analysis |
| 8 | Evidence: confidence bars, per-profile bars, verification line | `#evidence` | label counts + verification note |
| 9 | Open questions and going broader (the call to action) | `#next` | analysis |
| 10 | Part 2 opener band | `#method` | fixed + repo state |
| 11 | Process rail, why this compounds, labelling, material change, trust boundary, limits | `#process`, `#compounds`, `#labels`, `#material`, `#trust`, `#limits` | skills + README |
| 12 | Footer and colophon | `#colophon` | fixed + per-run block |

Every piece of content the v1 structure covered is still here. Merges: v1's archetype cards and competitor-detail disclosures become section 3 (cards grouped by cluster). v1's confidence bar grows into section 8.

**Cut from v1, on purpose:**
- **Category hues.** Screenshots and logos already bring six or more foreign colours onto the page, so four chart hues on top would make a carnival. The hue-collision fallback was also the most fragile rule in v1. Clusters are now shown by grouping and position.
- **Tabs and their JS.**
- **CSS-counter section numbers.** Numbering now appears only where order is real (section 5, rule 8).
- **The ink-density strength grid.** The position board (section 9.13) is easier to read.

## 4. Fixed foundations

### 4.1 Grid and breakpoints

- Content max width `1280px`, centred. Side gutter `clamp(16px, 4vw, 56px)`, set once on the page wrapper with `padding-inline`.
- Desktop (at least 1100px): 12 columns, 24px column gap.
- Tablet (720 to 1099px): 6 columns, 20px gap.
- Phone (under 720px): 4 columns, 16px gap. Nothing may cause horizontal page scroll. Only the matrix, the presence grid and the nav row scroll sideways, each inside its own `overflow-x: auto` container.
- Full-bleed elements (Part 2 opener band only) break out with `margin-inline: calc(50% - 50vw)`.

### 4.2 Spacing scale

4, 8, 12, 16, 20, 24, 32, 40, 48, 56, 72, 96. No other values.

- Between top-level sections: `padding-block: 96px` desktop, 72 tablet, 56 phone.
- Section heading to section body: 40 desktop, 32 tablet, 24 phone.
- Between sibling blocks inside a section: 24. Between findings: 72.
- Use grid/flex `gap` for sibling spacing, not margins.

### 4.3 Typefaces

Two families per page:
- **Brand match** (derived, section 6.6). Used for display, headings and body. Embedded as base64 `@font-face`, variable weight where available. Token `--font-brand`, with fallback `ui-sans-serif, system-ui, -apple-system, "Segoe UI", sans-serif` (serif matches fall back to `Georgia, serif`).
- **IBM Plex Mono** (fixed, every run; SIL OFL). Used for labels, eyebrows, captions, URLs, dates, commands, figures in tables and chips. Weights 400 and 500. Token `--font-mono`, fallback `ui-monospace, "SF Mono", Menlo, Consolas, monospace`. Plex Mono is the author's constant voice across every target; it is never used for headings or running prose.

### 4.4 Type scale

| Token | Size / line-height | Weight | Tracking | Use |
|---|---|---|---|---|
| `display-xl` | `clamp(38px, 3.2vw + 12px, 60px)` / 1.05 | 750 (700 if the family lacks it) | -0.025em | hero headline only |
| `display-l` | `clamp(32px, 2.4vw + 10px, 46px)` / 1.1 | 700 | -0.02em | Part 2 opener headline |
| `h2` | `clamp(26px, 1.4vw + 14px, 34px)` / 1.18 | 700 | -0.015em | section headlines (sentences), max width 30ch |
| `h3` | 22px / 30px (phone 20/28) | 650 | -0.01em | finding, cluster and recommendation headlines |
| `h4` | 18px / 24px | 650 | -0.005em | card titles, company names in cards |
| `lede` | `clamp(17px, 0.6vw + 13px, 21px)` / 1.5 | 400 | 0 | hero standfirst, Part 2 standfirst, max 58ch |
| `body` | 16px / 26px | 400 | 0 | running text, max 66ch |
| `body-s` | 15px / 24px | 400 | 0 | card summaries, cluster text |
| `small` | 13px / 20px | 400 | 0 | exhibit annotations, fallbacks |
| `label` | 11.5px / 16px, Plex Mono, uppercase | 500 | 0.1em | eyebrows, exhibit labels, row headers |
| `data` | 13px / 20px, Plex Mono | 400 | 0 | figures, URLs, dates, commands; `tabular-nums` |
| `figure` | 44px / 48px, brand face | 700 | -0.02em | the E6 figure only, `tabular-nums` |

Headings take `text-wrap: balance`, paragraphs `text-wrap: pretty`. Bold inside body copy is 600, used at most once per paragraph.

### 4.5 Shape, borders, elevation

- Radii: `--r-s: 4px` (chips, code chips), `--r-m: 8px` (screenshots, small panels), `--r-l: 12px` (cards, exhibit frames). Identity tiles use their own radius (9.4). Nothing else is rounded; text blocks never sit in containers.
- Borders are 1px `--rule` by default and 1px `--rule-strong` for screenshot edges and interactive boundaries. The target's card gets 2px `--accent-fill`.
- No drop shadows anywhere. Separation comes from border, surface step and space.
- Hatch (the Inferred texture), defined once:
  `--hatch: repeating-linear-gradient(135deg, color-mix(in oklab, var(--ink) 34%, transparent) 0 1px, transparent 1px 6px);`
  `--hatch-accent`: the same with `var(--accent-fill) 60%`.

### 4.6 Motion and interaction

- No load animation. The page is fully visible at rest.
- Hover on links and cards: colour and border changes only, `transition: 120ms ease-out`. Removed under `prefers-reduced-motion: reduce`.
- Focus: `outline: 2px solid var(--ink); outline-offset: 2px` on every interactive element. Never removed.
- Links in prose: `--ink` text, 1px underline in `--rule-strong` with 3px offset. On hover the underline turns `--ink`. Links are not accent-coloured, because accent is reserved (section 5).
- Theme toggle: default follows the system. The button stamps `data-theme` on `<html>` and remembers the choice in `localStorage` (inside try/catch). A `?theme=dark` or `?theme=light` query forces a theme on load, for review captures.

## 5. Encoding rules (these carry the page's honesty; never break them)

1. **Accent means the target.** Its card, row, column, marks, chip, and the moves this analysis recommends it make. Nothing else gets accent, including links, nav and focus.
2. **Alert means an ending or restructuring event.** Administration, liquidation, dissolution, market exit, shutdown. Always text plus glyph plus colour, so colour is never the only carrier. Nothing else gets alert.
3. **Observed versus Inferred is texture, never colour.** Texture has a size floor: hatch only reads on a mark at least 6px thick and 24px long (bars, ranges, confidence segments). Anything smaller (dots, rings, cell edges, single-line table cells) carries inference on its text instead: a dotted underline plus a superscript `i`, the same treatment as inline prose. Never try to hatch a 12px glyph or a 4px strip; at 1x they read as a stray chevron. The legend sits above or beside the exhibit, never only in a footer.
4. **Competitors never get a hue in data marks.** Their marks are ink. Their colour lives only inside their logo tile and their screenshot.
5. **Strengths and gaps get no colour.** Glyph and column position carry them.
6. **Judgement axes are ordinal.** Worded end labels, no numbers, no gridlines implying a scale.
7. **Dashed means not done yet.** Survey-depth chips, go-broader cards and "not in market" chips use dashed borders. Full profiles use solid.
8. **Numbers mark real order only.** Findings (ranked), exhibits (referenced by number in the text), recommendations (priority) and process steps (sequence) are numbered. Nothing else is.
9. **Every ratio on the page comes from one count.** Observed/Inferred figures are computed by counting `- Observed:` and `- Inferred` label lines in `profiles/*.md` at build time. The hero, the evidence section and the README must all quote that same count. If prose elsewhere disagrees, the prose is wrong.
10. **Wording is fixed.** "Re-checked against the pages they cite." Never "verified" as a claim about truth.

## 6. Derived per run: brand intake to tokens

### 6.1 Brand signals the capture step supplies

For the target (competitors optional): `theme-color`, chromatic colours from its CSS ranked by frequency, font-family stacks, near-black candidates (OKLCH L 0.12 to 0.22, C under 0.03), and the logo. The target's homepage screenshot is used to confirm by eye.

### 6.2 Picking the brand colour (one colour; the rest are recorded, not used)

In order, take the first that exists:
1. `theme-color`, if chromatic (OKLCH C of 0.04 or more) and not `#FFFFFF`/`#000000`.
2. The most frequent chromatic colour in the site's own CSS, excluding default link blues (`#0000EE`, `#1A0DAB`, `#0645AD`, `#3898EC`, the Webflow default) and colours that only appear in third-party widgets.
3. The dominant chromatic colour of the logo.
4. None: the brand is achromatic, so use neutral mode (6.4).

Then check it against the screenshot. It should be the colour the company uses for its primary action or its mark. If the screenshot contradicts the pick, record why and take the next candidate.

**One accent, even when the brand has more.** Secondary brand colours are recorded in the per-run block and not used. A second brand hue makes the page read as the company's own collateral, and it competes with alert.

### 6.3 The dark ground

If the brand signals include a near-black (L 0.12 to 0.22, C under 0.03) from the target's own CSS, pass it to `derive_tokens.py --dark`. The dark theme then sits on the company's own black. Otherwise the script derives a dark ground at L 0.17 on the brand hue.

### 6.4 Running the derivation

```
python3 derive_tokens.py '<brand hex>' [--dark '<near-black hex>']          # contrast report
python3 derive_tokens.py '<brand hex>' [--dark '<near-black hex>'] --css    # paste-ready token blocks
```

What it does, so a reviewer can check it:
- **Neutrals** keep fixed OKLCH lightness and chroma and borrow only the brand's hue. Every page gets its own tint, and contrast stays identical from run to run. Light ink-3 is at least 4.7:1 on every surface, and dark ink-3 at least 5.9:1.
- **Accent (text).** It starts at the brand colour and moves lightness (darker in light theme, lighter in dark) until it reaches 4.5:1 on `--bg`, `--surface`, `--surface-2` and `--accent-wash`. Hue is kept, and chroma is reduced only to stay in gamut. If the brand already passes, the accent is the exact brand colour.
- **Accent fill** (solid marks: bars, the target card border, chip fill, active markers) is the exact brand colour if it reaches 3:1 on the grounds; otherwise it is stepped until it does. `--on-accent` is white or ink, whichever reads on the fill, and must reach 4.5:1.
- **Wash and line.** `--accent-wash` is a pale tint (light) or deep tint (dark) for the target's column, row and card highlights. Ink and ink-2 stay at 7.5:1 or better on it. `--accent-line` is for decorative rules inside target areas only, never a boundary that has to be seen.
- **Modes**, recorded as `--accent-mode`:
  - `ink`: the normal case. The accent is used as text colour and as fill.
  - `highlighter`: neon or pale brands (lime, yellow, cyan) whose text-safe version would lose its identity (lightness moved more than 0.22, or chroma below 45% of the original). The brand colour then acts only as a fill behind ink: marker behind the headline phrase, chip fill, bar fill, card border. Text "accent" becomes `--ink`. **Every filled accent mark gets a 1px `--ink` outline in this mode**, because the fill itself doesn't reach 3:1 on the ground. Dark theme usually stays in `ink` mode for these brands.
  - `neutral`: achromatic brands (C under 0.04). The accent is `--ink`. The target is marked by a solid ink fill, 700-weight names and the "Subject" label. Neutrals take hue 250 at 60% chroma.
- **Alert** is fixed at hue 28 (red-orange) and stepped to 4.5:1 on every surface and on its own wash. If the brand hue is within 35 degrees of 28 (reds and oranges), alert switches to ink-inverse: `--alert` becomes `--ink` and `--alert-wash` becomes `--surface-2`, and the glyph and text carry the meaning.

Tested cases, with their modes (light / dark): Turo `#593CFB` ink/ink; Spotify-like `#1DB954` ink/ink; Netflix-like `#E50914` ink/ink plus alert clash; lime `#C6FF00` highlighter/ink; yellow `#FFCC00` highlighter/ink; cyan `#00D1FF` highlighter/ink; black `#000000` neutral/neutral. Every text pairing lands at 4.5:1 or better.

### 6.5 Token reference

| Token | Role |
|---|---|
| `--bg` | page ground; `body` background |
| `--surface` | cards, exhibit frames |
| `--surface-2` | caption bars, fallbacks, Part 2 band, code specimens, the "gap" column band |
| `--rule` / `--rule-strong` | hairlines / screenshot edges and interactive boundaries |
| `--ink` / `--ink-2` / `--ink-3` | headings and key text / body / labels and captions |
| `--accent` | target text: labels, first recommendation numeral, headline phrase (ink mode) |
| `--accent-fill` / `--on-accent` | target solid marks / text on them |
| `--accent-wash` / `--accent-line` | target highlight ground / decorative rule inside target areas |
| `--alert` / `--alert-wash` | ending-event chips and markers |

All tokens are declared in bare `:root` first. The dark blocks only redefine them (the script prints all three blocks). Components use tokens only, never literals, apart from logo plate colours, which are the logo's own ground and stay constant across themes (9.4).

### 6.6 Matching the typeface

Never embed the target's own font, even when it can be downloaded. Pick the open-licence match by class:

| The brand's face looks like (by name, or by the site's own fallback stack, or by eye) | Use (Google Fonts, SIL OFL) | Request |
|---|---|---|
| Geometric sans: Avenir, Futura, Circular, Gilroy, Gotham, Cera, Product Sans, Euclid, custom geometrics | **Figtree** | `Figtree:wght@400..800` |
| Neo-grotesque: Helvetica, Neue Haas, Graphik, Aktiv, SF Pro, Suisse, Söhne, Roboto | **Instrument Sans** | `Instrument+Sans:wght@400..700` |
| Humanist sans: Frutiger, Myriad, FF Meta, Gill Sans, Segoe, Calibri | **Source Sans 3** | `Source+Sans+3:wght@400..800` |
| Rounded sans: VAG Rounded, Gotham Rounded, Arial Rounded | **Nunito** | `Nunito:wght@400..800` |
| Serif: Tiempos, Publico, GT Sectra, Canela, Georgia | **Newsreader** (display and body) | `Newsreader:opsz,wght@6..72,400..700` |
| Industrial or condensed: DIN, Eurostile, Tungsten, Knockout | **Barlow** | `Barlow:wght@400;500;600;700` |
| Can't classify | **Instrument Sans** | as above |

If the site's stack names a family that is itself open-licence (for example it self-hosts a Google font), use that exact family, even if it's a common one. Tailoring outranks the "avoid default fonts" instinct here, because the choice is derived, not defaulted.

**Sourcing, with no subsetting tools required.** At build time, request `https://fonts.googleapis.com/css2?family=<request>&display=swap` with a desktop Chrome user agent. Keep only the `/* latin */` `@font-face` blocks, download each `woff2`, and embed it as `url(data:font/woff2;base64,...)` with the same `unicode-range` and `font-display: swap`. Do the same for `IBM+Plex+Mono:wght@400;500`. Budget: 150 KB of font binary in total.

The colophon names the match and says it stands in for the brand's own typeface (section 10).

## 7. Independence cues (all required, every run)

1. The masthead's left slot is the author ("Chris Schubert", with the label "Independent landscape"). The target's name or logo never appears there.
2. The hero eyebrow begins with `INDEPENDENT ANALYSIS`.
3. "Not affiliated with {Target}." is visible at 1440x900 without scrolling (trust panel) and again in the footer.
4. The target's logo tile is the same size as every competitor's. It is never enlarged, never used in a heading, never a background.
5. The brand colour never fills the page ground, the masthead, or any full-bleed band. The largest accent-filled shape allowed is a chip, a bar, a 3px rule or a 2px card border. `--accent-wash` may fill only the target's own column, row or card.
6. Every screenshot sits inside the caption-bar frame (domain, capture date, locale served if not the target market).
7. The target is written about in the third person ("Turo would"), never "we" or "our".
8. Nothing is lifted from the target's site except the labelled screenshot and the unaltered logo: no taglines, product photos, illustrations or icon sets.
9. The colophon states how the accent was derived and that the typeface is an open stand-in.

## 8. Assets: capture, selection, processing, budget

### 8.1 What imagery appears where

| Place | Asset | Size |
|---|---|---|
| Hero cast strip | screenshot (16:10, top of homepage) + identity tile S | about 200px wide per shot |
| Findings exhibits | E1/E2/E3 use tiles; E4 uses an exhibit crop | full exhibit width |
| The field, player cards | screenshot (16:10) + identity tile M | about 400px wide |
| Matrix header, evidence rows, event rail, presence grid | identity tile S | 24px |
| Go-broader cards | identity tile M | 40px |

Mobile captures are not used. On a phone, the 16:10 desktop capture still reads as "their homepage", and a second image per company would double the weight for a small-screen nicety. The capture step can stop producing them.

### 8.2 Screenshot capture (per company, including the target)

- Viewport 1440x900 at DPR 1 (or DPR 2 downscaled). Wait for load plus 1.5s of network idle. Scroll to the bottom in 600px steps, return to the top, and wait 1s, so lazy-loaded images fire. Hide consent overlays by injecting `display:none` on fixed or sticky elements whose id, class or aria-label matches `cookie|consent|gdpr|onetrust|cmp|privacy`. Then capture.
- **Gates.** Reject the capture, retry once with doubled waits, then fall back to a manual recapture in an isolated browser (never a signed-in one: a logged-in session can put a name or personalised content on a public page) or to the fallback frame:
  1. **Blocked or challenge page.** The title or visible text matches `just a moment|attention required|access denied|verify you are human|captcha|request blocked|are you a robot|waf`, or the title contains unrendered `{{`. (curl and plain headless Chrome both hit Turo's Cloudflare block page from this machine.)
  2. **Broken imagery.** Any `<img>` in the first viewport with `complete && naturalWidth === 0`, or visible alt text. (Turo's first pass failed this: the hero showed its alt text "Rental reinvented" and three of four car photos were blank.)
  3. **Blank.** More than 92% of pixels within 6 levels of the modal colour.
  4. **Fonts not loaded.** Capture only after `await document.fonts.ready` and `document.fonts.status === 'loaded'`, then 500ms more. (Cityhop's recapture shipped with its headline in Times because the webfont hadn't arrived; a fallback-font screenshot misrepresents the company.)
  5. **Consent modal still covering more than 20% of the viewport.** (Getaround's and Zilch's first passes.)
- `assets.py capture` renders at 1200px wide and steps JPEG quality down 72, 64, 56, 48 to stay under the cap. A manual recapture is normalised with `sips -Z 1200 -s format jpeg -s formatOptions 72 in.png --out assets/<slug>/home.jpg`.
- Record per company: URL after redirects, the locale served (a Sydney machine gets turo.com's Australian site), capture date (Sydney date), status `ok | unavailable`, and a reason.

### 8.3 Exhibit crops (for E4 only)

When a finding's evidence is visible on a page but sits below the fold, capture at 1440x1600 (or full page) and crop to the part that carries the claim. **Aspect ratio between 16:10 and 3:1**, never wider: a 6:1 band scaled into a 7-column exhibit renders its content at about half size, and at phone width it is illegible. If the evidence runs across a wide band (a row of review scores and badges), crop the portion the finding cites and leave the rest out. Test: the key text in the crop must be at least 9px tall when rendered at 358px wide. Store it as `exhibit-<slug>.jpg`, 1200px wide, under the same cap. Record the crop rectangle and the source URL. At most two per page.

### 8.4 Logos: the identity tile system

The captures produce a mix: app-icon squares, transparent wordmarks in any colour, og tiles, and sometimes nothing. **Every company is shown as a square identity tile** of fixed size, radius and border, with its name always set beside it in the page's own type. Uniform squares make the mix look deliberate, and because the name is always adjacent, the tile never has to be legible as a word.

**Selection order** (take the first that passes the checks):
1. A square app icon (`apple-touch-icon`, manifest icon) at least 80px.
2. A square mark from the site (inline SVG or image) inside the header's homepage link, or with `logo` or the company name in its class, id, alt, aria-label or title.
3. A transparent wordmark from the same places.
4. `og:image`, when it's a flat logo tile rather than a photo.
5. A favicon of at least 80px.
6. Otherwise: monogram.

**Mandatory visual check.** Render each chosen asset on white and on near-black and look at it. It must show the company's name or its known mark. Reject:
- Other companies' logos. Review, social, payment and app-store badges turn up constantly: GO Rentals' candidates included the Google and Facebook review logos.
- UI icons and decoration. Turo's first "inline SVG logo" was an AI-sparkle icon (`IconAiSparkleBrand`), and Getaround's was a rating star.
- Photos, mascots and broken files.

**Fill modes** (recorded in the manifest):
- `bleed`: the asset is an opaque square app icon or tile. It fills the tile with `background-size: cover`, centred. Two exceptions, both seen on the Turo run: an icon with transparent rounded corners goes on a plate of its own edge colour (GO Rentals' icon on `#E21266`), and a non-square og tile carrying a wordmark is fitted with `contain` on a plate of its own sampled background colour, never centre-cropped (a crop clipped Getaround's wordmark).
- `plate`: the asset is transparent. It sits centred on a plate colour, with 18% padding each side, at `background-size: contain`. **The plate is the ground the company itself puts behind that logo.** Dark logos go on `#FFFFFF`. Light logos go on the site's header or brand colour, sampled from the screenshot behind the logo, or on `#1A1A1A` if nothing can be sampled. The plate colour is constant across both themes, so the logo is never recoloured or inverted.
- `monogram`: no acceptable asset. The tile is filled `--surface-2` with the initials in `--ink` (the target: `--accent-fill` with `--on-accent`). Initials are the first letter of the first two words, or one letter for a one-word name, in the brand face at weight 700 and 42% of the tile height. The manifest records why.

**Tile spec.**
- Sizes: S = 24px (radius 6), M = 40px (radius 9). There is no larger size. Screenshot fallbacks use M.
- Border: `box-shadow: inset 0 0 0 1px color-mix(in oklab, var(--ink) 14%, transparent)`, so a white plate still has an edge on a light ground.
- Sharpness, measured against the rendered size at M: a `bleed` raster needs a native short side of at least 60px (1.5x of 40). A `plate` raster needs a native width of at least 1.5x its rendered width inside the padded tile (a 154x47 wordmark renders about 26px wide, so it passes easily). An asset that fails at M is not used at S either; take the next candidate, so one company never shows two different marks.
- Rasters are kept as PNG. If over 30 KB, downscale to 160px with `sips -Z 160`. SVGs are sanitised (strip `<script>`, `on*` attributes and external `href`s; keep `viewBox`; remove width and height) and embedded as `data:image/svg+xml;base64`.
- Tiles are `aria-hidden="true"`, because the adjacent name carries the meaning.

### 8.5 Embedding

- Every image is declared **once**, as a CSS custom property in a single `<style id="asset-data">` block placed just before `</body>`:
  `:root{--shot-mevo:url("data:image/jpeg;base64,...");--tile-mevo:url("data:image/png;base64,...");}`
- Components reference them with an inline custom property, for example `<div class="shot" style="--img:var(--shot-mevo)" role="img" aria-label="Mevo homepage, mevo.co.nz, captured 23 September 2026"></div>`, where `.shot{background:var(--img) top center/cover no-repeat}`.
- This keeps the markup readable and makes reuse free: the hero strip and the player card share one copy of each screenshot.
- `check.py` passes `data:` URIs. Still no external `url()`, `src` or `href` fetches of any kind.

### 8.6 Page-weight budget

- `index.html`: hard limit **2.5 MB**, warning at 2.0 MB (add both to `check.py`).
- Per screenshot: `min(180 KB, 1100 KB / number of companies)` of JPEG binary. Per exhibit crop: 180 KB.
- Per tile: 30 KB. Fonts: 150 KB in total. Markup, CSS and JS: 200 KB.
- Base64 adds about 34%. Six companies plus two crops comes to roughly 2.1 MB.

### 8.7 Manifest fields the builder reads

`assets/manifest.json`, keyed by slug: `name`, `domain`, `url_captured`, `locale_served`, `captured`, `shot {file, status, reason, notes}`, `exhibit_crops [{file, source_url, rect, finding}]`, `tile {file, mode, plate, native_short_side, reason}`, `chip {label, variant}`, and for the target `brand {primary, secondaries, near_black, fonts, font_class, font_match}`.

## 9. Components

Each component lists anatomy, then sizes, then states, then responsive behaviour. Sizes are CSS px.

### 9.1 Masthead

- Sticky, `top: env(safe-area-inset-top, 0px)`, height 64 (phone 56), `--bg` fill, 1px `--rule` bottom border, z-index above the matrix's sticky header.
- Left: "Chris Schubert" in the brand face, 15px, 650, `--ink`, followed by the `label` "INDEPENDENT LANDSCAPE" in `--ink-3`, 12px gap. It links to the repo.
- Right: nav anchors (Findings, The field, Compare, Recommendations, Evidence, How it was built) in 14px, 500, `--ink-2`, 24px apart; hover `--ink`. Then the theme toggle: 32px tall, 12px horizontal padding, `label` text naming the theme it switches to ("DARK"/"LIGHT"), 1px `--rule-strong` border, `--r-s`.
- Phone: the nav moves into a second row that is not sticky. It is 44px tall, scrolls sideways inside its own container, uses 16px gaps, and fades out over 24px on the right with a mask. The sticky row keeps the author mark and the toggle.

### 9.2 Hero

- `padding-block: 72px 48px` desktop, `40px 32px` phone.
- Grid at desktop: headline block in columns 1 to 8, trust panel in columns 10 to 12, aligned to the top of the headline. Tablet: trust panel below, full width, with its `label` spanning the full width on top and the bar plus figures on the left, the fact lines on the right. Phone: stacked.
- **Eyebrow**: `label`, `--ink-3`: `INDEPENDENT ANALYSIS · {TARGET} × {LENS, 2 TO 4 WORDS} · {DD MON YYYY}`. 16px above the headline.
- **Headline**: `display-xl`, `--ink`, at most 3 lines at 1440 (about 85 characters). One phrase, the part about the target's move or advantage, is marked: in `ink` mode it is `--accent` text; in `highlighter` mode it is ink on a brand-fill marker (`background: linear-gradient(transparent 55%, var(--accent-fill) 55%)`, `box-decoration-break: clone`); in `neutral` mode it gets a 3px ink underline. Mark only a phrase about the target. Never mark a competitor's failure in accent.
- **Standfirst**: `lede`, `--ink-2`, 2 or 3 sentences, 24px below.
- **Trust panel**: 1px `--rule` left border, 24px left padding, no fill.
  - `label` "HOW FAR TO TRUST THIS".
  - Confidence bar, compact version (9.16): height 10.
  - `data`: "{o}% observed · {i}% inferred" on one line and "{n} claims" on the next, so a wrap never strands a separator at a line end.
  - Three to four `small` lines: "{n} competitors, {k} profiled in full"; "Deep profiles re-checked against the pages they cite on {date}"; "Desk research. No interviews or customer calls."
  - A link, "How this was built", to `#method`.
  - Last line, 13px `--ink-3`: "Not affiliated with {Target}."
- **Cast strip**: 48px below the text block (phone 32). Header row: `label` "THE FIELD" on the left, and `data` "Homepages captured {date}" in `--ink-3` on the right. Then the cast cards (9.3).

### 9.3 Cast card (hero)

- The whole card is an `<a href="#player-{slug}">`.
- Anatomy: screenshot (16:10, `--r-m`, 1px `--rule-strong` border, `.shot`). 12px below it, a row with tile S, 8px gap, and the name (15/20, 650, `--ink`). 8px below that, the status chip.
- Grid: up to 6 companies in one row at desktop (`repeat(n, 1fr)`, 16px gap); 7 or 8 companies go 4-up in two rows. Tablet 3-up, phone 2-up. More than 8: show the 8 most relevant, then a `small` line "and {n} more in The field".
- **Target placement encodes the truth.** If the target already operates in the lens market, it goes first. If the lens is a market entry (the target isn't there yet), it goes last, set apart by a 1px `--rule` vertical divider with 24px either side (phone: a full-width divider row). Its chip reads "Not in {market} yet".
- States: hover turns the screenshot border `--ink-3` and underlines the name. Focus gets the outline. The target's screenshot border is 2px `--accent-fill`.
- Screenshot unavailable: the fallback frame (9.10) at thumbnail scale, with the tile and domain only.

### 9.4 Identity tile

See 8.4. Class `.tile.tile-s` or `.tile.tile-m`, background from `--tile` and `--plate`. It never stretches, and `flex: none` keeps it square.

### 9.5 Status chip

- Height 22, padding 0 8px, `--r-s`, `label` type at 11px with 0.06em tracking, `white-space: nowrap`, **at most 20 characters** (the cast card is about 176px wide at six across, and a chip that wraps breaks the strip's baseline). For an ending event, the chip names the event and its date ("COLLAPSED MAR 2026", "LIQUIDATING 2026"); what happened next (a relaunch, a sale) goes in the role line and the card summary, never in the chip.
- Variants:
  - `neutral` (owner or model, e.g. "TOYOTA NZ"): 1px `--rule-strong` border, `--ink-2` text, no fill.
  - `alert` (e.g. "ADMINISTRATION · MAR 2026", "LIQUIDATING · 2026"): `--alert-wash` fill, `--alert` text, 1px border in `color-mix(in oklab, var(--alert) 45%, transparent)`, and a 6px square rotated 45 degrees in `currentColor` before the text, with a 6px gap.
  - `subject` ("NOT IN NZ YET", or "SUBJECT"): `--accent-wash` fill, `--accent` text, 1px `--accent-line` border. In `highlighter` mode: `--accent-fill` fill, `--on-accent` text, 1px `--ink` border.
  - `depth` ("SURVEY DEPTH"): 1px dashed `--rule-strong`, `--ink-3`. ("FULL PROFILE"): 1px solid `--rule-strong`, `--ink-2`.
- One status chip per company per context. Its wording is fixed in the manifest so it reads the same everywhere.

### 9.6 Section head

- `label` eyebrow (what the section is, e.g. "FINDINGS"), 12px gap, then the `h2` headline, which is a sentence that says something, max 30ch. Optionally, 16px below, a one-sentence `body` intro in `--ink-2`, max 60ch.
- It sits in columns 1 to 8. Nothing sits beside it.

### 9.7 Finding block

- `<article id="finding-{n}">`. Desktop grid: text in columns 1 to 5, exhibit in columns 6 to 12, both aligned to the top. Findings are separated by 72px of space, with no rules.
- Text column, top to bottom:
  - `label` "FINDING {n} OF {total}" in `--ink-3`.
  - `h3` headline sentence, 12px below.
  - `body` in `--ink-2`, 2 to 5 sentences (at most about 110 words), 12px below.
  - "What it means for {Target}": a `label` "FOR {TARGET}" in `--accent`, then one or two `body` sentences in `--ink`, 16px below.
  - Sources line: `data` 12px `--ink-3`, e.g. "Observed · 3 sources · Mevo and Getaround profiles", with the profile names as links to `#player-{slug}`.
- **No exhibit available.** The text runs across columns 1 to 7. The "For {Target}" line moves to columns 9 to 12 as a pull line: 20/30, `--ink`, with a 2px `--accent-fill` left border and 16px padding. Never invent an exhibit to fill the space.
- Tablet and phone: text first, then the exhibit at full width, 24px apart.

### 9.8 Exhibit frame

- `<figure id="exhibit-{n}">`: `--surface` fill, 1px `--rule` border, `--r-l`, padding 24 (phone 16).
- Header: `label` "EXHIBIT {n}" in `--ink-3`, then the title (15/22, 650, `--ink`) on the next line, 20px above the body.
- `<figcaption>`: 20px above, 12px top padding, 1px `--rule` top border, `data` 11.5/18 in `--ink-3`. It holds the source(s), the Observed/Inferred status, and the legend if the exhibit uses a texture.
- Exhibits are numbered in order of appearance across Part 1, and the text refers to them by number.
- At most one exhibit per finding and six in total (the matrix and player cards don't count).
- **Only the six exhibit types below exist.** A builder may not invent a new chart type. If none fits, the finding runs without one.

### 9.9 Exhibit types

**E1 Event rail**: for findings driven by what happened when.
- Only Observed, dated events. Day or month precision is placed; month-only goes at mid-month with a label like "MAR 2026"; year-only events are not placed and belong in the text.
- Horizontal time axis: 1px `--rule-strong`, from the start of the first event's quarter to the end of the last one's. Quarter ticks 6px tall, labelled in `label` `--ink-3` ("Q1 2026"). Positions are on a true time scale.
- Markers, 10px: alert events are a rotated square in `--alert`; other events are a circle in `--ink-2`; target events are a circle in `--accent-fill`.
- Labels alternate above and below the axis, with a 16px connector in `--rule-strong`. Each label is at most 180px wide: date (`data` 11px `--ink-3`), then tile S and company name (13/18, 650), then the event (13/18 `--ink-2`, at most 60 characters). Body height 260.
- **Choose the mode before drawing.** Use horizontal only if every pair of adjacent events is at least 12% of the axis range apart; otherwise use vertical mode from the start. Real event sets cluster (four of Turo's five events fall within ten weeks), so vertical will be the common case, and horizontal is the exception for evenly spread histories.
- Vertical mode (also used under 720px): a vertical line on the left, markers on it, labels to the right, evenly spaced in date order. Where an interval between adjacent events is more than three times the median interval, insert a gap note between them (`label` `--ink-3`, e.g. "13 MONTHS"), so the even spacing doesn't hide the time that passed. The caption adds "Spacing not to scale."

**E2 Ownership map**: for findings about who owns whom.
- A row of groups. Each group has a parent box: `--surface-2` fill, 1px `--rule-strong`, `--r-m`, padding 10px 14px, `label` "OWNER", and the name in 15/20, 650.
- Below it, a bracket: a 12px vertical line from the parent's centre, a horizontal line across the children's centres, and 12px drops to each child, all 1px `--rule-strong` (drawn with CSS borders or pseudo-elements).
- Children: tile M, the name (14/20, 650), and a `data` 11px detail (e.g. "since 2018", "acquired 2026").
- Independent companies sit under a parent box with a dashed border and the label "INDEPENDENT".
- The target, if relevant, sits at the far right, 32px apart, inside a 1px dashed `--accent-line` outline, with its parent (e.g. "IAC · 31% STAKE") and its subject chip.
- Group widths are proportional to child count (`grid-template-columns` in `fr` equal to child count), with a minimum of 152px per group so no parent name wraps.
- **All parent boxes share one height, and all children share one top line.** Build it as one grid with two rows (parents, then children) across every group, or give parent boxes a fixed height of 64px, so a two-word parent name can't push its children below the others.
- An inferred link uses a dotted connector and a superscript `i` on the child.
- Under 720px, groups stack and each bracket becomes a left rule with the children indented 20px.

**E3 Presence grid**: for findings about who does or doesn't have something.
- A table. The first column holds tile S and the name (14/20). Header cells are `label`, at most 6 categories, each at least 88px wide.
- Cell glyphs, 12px:
  - Observed present: a filled `--ink-2` dot, with an optional 12px `--ink-2` name beside it ("AA").
  - Looked, none found: a 1.5px `--ink-3` ring.
  - Inferred present: the same filled `--ink-2` dot as Observed (the thing is claimed to be there), with its name label in dotted underline plus superscript `i` (rule 3: glyphs this small can't carry hatch). Present and absent must never look alike.
  - Not researched: an en dash in `--ink-3`.
- **The column the finding is about comes first**, immediately after the company column, at every width, so it is never scrolled off-screen on a phone. It gets a `--surface-2` band plus 1px `--rule-strong` borders on both sides (the fill alone is only a 3-point lightness step in dark theme and disappears), and a `label` in `--ink` naming the finding ("THE GAP"), set as its own line above the header row, separated from the column's own header by 4px. No accent, because accent is the target's.
- The target's row: `--accent-wash` ground, glyphs in `--accent-fill`.
- The legend is in the figcaption. "None found" is always worded as absence of evidence, never as proof of absence.
- Phone: the table scrolls sideways in its container, with the first column sticky.

**E4 Screenshot exhibit**: for findings where the page itself is the evidence.
- A caption bar (as in 9.10) over an exhibit crop (8.3) or the homepage capture, at full exhibit width, `--r-m`.
- Optional: one verbatim quote from the captured page below it (17/26, `--ink`, in curly quotes), plus a `data` source line.
- No drawn callouts or arrows on the image.
- At most two per page.

**E5 Ordinal band**: for findings about where companies sit on a judgement scale. This generalises v1's moat bar.
- One row per company, 36px tall. The label column is 168px wide (tile S and name). The track spans the rest: `--surface-2`, 12px tall, `--r-s`.
- Range bar: 12px, radius 3, filled `--ink-2` (the target: `--accent-fill`). A wholly or partly inferred range uses `--hatch` with a 1px `--ink-3` outline (the target: `--hatch-accent` with a 1px `--accent-fill` outline).
- Axis: worded ends only ("Minutes", "Weeks") in `label` `--ink-3`, with optional evenly spaced ordinal category ticks (Minutes, Hours, Days, Weeks). Never numbers.
- Bars are clamped inside the track.
- The caption states: "Positions are ordinal judgements. Hatched ranges are inferred."
- Phone: the label sits above the track.

**E6 Figure pair**: for a finding that rests on one or two numbers.
- One or two figures side by side, 40px apart: `figure` type, unit in 16px `--ink-2`, label in 14/20 `--ink-2` (at most 2 lines), source in `data` 11px.
- An inferred figure is prefixed "est.", with a 2px dotted underline and a superscript `i`.
- A pair is allowed only when the two numbers are in the same unit and mean the same kind of thing.

### 9.10 Player card and screenshot frame

- `<article id="player-{slug}">`: `--surface`, 1px `--rule` border, `--r-l`, `overflow: hidden`. The target's card: 2px `--accent-fill` border.
- **Caption bar**: height 32, padding 0 12px, `--surface-2`, 1px `--rule` bottom border. `data` 11px `--ink-3`: the domain on the left; the capture date on the right (plus the locale served, e.g. "AU SITE", when it isn't the lens market). The target's bar adds "SUBJECT" in `--accent` before the date. The bar never clips: the date keeps `flex: none`; the left item takes `min-width: 0; overflow: hidden; text-overflow: ellipsis`; and below 480px any descriptor between domain and date ("BELOW THE FOLD", "AU SITE") is dropped.
- Screenshot: 16:10 `.shot`, top-anchored. **A screenshot always renders at its captured 16:10 aspect.** `.shot` never gets `aspect-ratio: auto`, `min-height` or a flex-stretched height, because `cover` into a box of any other shape crops the company's logo and headline off the sides.
- **Fallback frame** (screenshot unavailable): the same 16:10 box in `--surface-2`, centred column: tile M, the domain (`data`), and a `small` `--ink-3` line at most 30ch wide, e.g. "Homepage not captured on 23 Sep 2026: the site blocked automated access." It never looks broken, and it never pretends.
- Body, padding 20 (phone 16), top to bottom:
  - A header row: tile M, 12px gap, the name (`h4`), then the status chip on the right (wrapping below on narrow cards).
  - The role line, 8px below: `label` `--ink-3`, e.g. "NZ CAR-SHARE · FREE-FLOATING · WELLINGTON".
  - The summary, 12px below: `body-s` `--ink-2`, 2 to 4 sentences.
  - The depth row, 16px below: the depth chip, then a mini confidence bar (120 by 6, 9.16), then `data` "{o} observed · {i} inferred".
  - A disclosure, 16px below, with a 1px `--rule` top border and 12px padding: `<details>`, whose `<summary>` is "Key facts and sources" (14px, 600) with a CSS chevron. Inside is a list of 4 to 8 facts in `body-s`. Observed facts end with their source domain as a `data` link. Inferred facts get the dotted underline and a superscript `i`. The last line reads "Full profile: profiles/{slug}.md" and links to the GitHub blob.
- **Wide variant** (a cluster with one card, or the last card of an odd set): a two-column card, with the screenshot column on the left at 58% and the body on the right. The screenshot column holds the caption bar and a 16:10 `.shot`, aligned to the top. Any height the body adds below the image is filled with `--surface-2` in the screenshot column, never by stretching the image. Under 1100px it becomes the normal stacked card.

### 9.11 The field: cluster groups

- Clusters appear in the analysis's order. Each cluster: a 1px `--rule` top border with 24px padding above, and 72px between clusters.
- Desktop grid: cluster text in columns 1 to 4, cards in columns 5 to 12 (2-up, 20px gap). One card uses the wide variant. An odd number above one: the last card goes wide.
- Cluster text: the name (`h3`), then how it works (`body-s` `--ink-2`, 2 to 3 sentences, 12px below), then the `label` "FOR {TARGET}" in `--accent` and a `body-s` `--ink` sentence, 16px below.
- Every company appears in exactly one cluster, its current one. Past membership (e.g. "Mevo, before its relaunch") is mentioned in the cluster text, not shown as a second card.
- The target's own cluster (for example "Outlier") is last.
- Tablet: the cluster text sits above its cards, which stay 2-up. Phone: 1-up.

### 9.12 Comparison matrix

- Wrapped in an `overflow-x: auto` container with the legend above it: `data` 11px, e.g. "Dotted underline and i mean inferred. A dash means not researched at this depth."
- Table: the first column is 180px, with a `--bg` fill, sticky left only while its own container is scrolled sideways. The header row is **not** sticky: `position: sticky` inside an `overflow-x` container sticks to the container, not the page, so it can't work here.
- Header cells: tile S and the name (13/18, 650), aligned to the bottom, padding 12. The target's header has a 3px `--accent-fill` top border, with the `label` "SUBJECT" in `--accent` above the name.
- Row headers: `label` `--ink-3`, wrapping.
- Body cells: 14/21 `--ink`, padding 12px 14px, 1px `--rule` bottom border, each column at least 150px.
- The target's column: `--accent-wash` ground from top to bottom.
- Inferred cell: the cell text gets a dotted underline (1px, `--ink-3`, 3px offset) plus a superscript `i` in `--ink-3`, per rule 3. No hatch strip: a 4px strip sits on the column boundary and reads as belonging to the neighbouring cell.
- Not researched: an en dash in `--ink-3`, with `title="Not researched at this depth"`.
- Under 720px it transposes to one `<details>` per dimension. The summary is the dimension name; the content lists each company (tile S, name, value), with the target's row on `--accent-wash`. Generate both markups and switch between them with CSS.

### 9.13 Position board (strengths, gaps, open ground)

- Three columns at desktop, separated by 1px `--rule` vertical lines with 32px padding; stacked on phone.
- Column headers: `label` "STRENGTHS", "GAPS", "OPEN GROUND", each preceded by its glyph (+, −, ○) in the brand face at 20px, `--ink`.
- Items are 20px apart: a 24px glyph gutter (the same glyph in 16px `--ink-3`), a title that is a short sentence (16/24, 650), and detail (15/23 `--ink-2`, 1 to 2 sentences).
- No colour, no cards. Item shapes vary as the voice doc requires.

### 9.14 Option comparison (lens deep-dive, optional)

- Two or three option cards side by side: `--surface`, 1px `--rule`, `--r-l`, padding 24.
- Each card: the option name (`h4`), then rows of a `label` plus `body-s` for "WHAT IT BUYS", "WHAT IT COSTS" and "WHO IT REACHES", then a one-sentence verdict at the bottom above a 1px `--rule`.
- The option the analysis recommends: 2px `--accent-fill` border plus a subject-variant chip, e.g. "SHARPER FIRST MOVE". Costs stay qualitative unless a source gives a figure.
- Phone: stacked.

### 9.15 Recommendations

- An `<ol>`. Each item is a two-column grid: a 64px numeral (brand face, 40/44, 700, `tabular-nums`, `--ink-3`; the first item's numeral is `--accent`), then the content.
- Content: the headline (`h3`), the body (`body`, `--ink-2`, at most 70 words), and a `data` 11px "Rests on" line with links to `#finding-{n}` and `#exhibit-{n}`.
- Items are separated by 1px `--rule` lines and 28px vertical padding.
- Order is the analysis's priority. The count is whatever the analysis gives.

### 9.16 Confidence bars (Evidence section)

- **Main bar**: 16px tall, radius 3, as a flex row. Each segment has `flex: {count} 1 0` (flex-basis 0, so the ratio is exact). Observed is solid `--ink-2`. Inferred is `--hatch` on `--surface-2` with a 1px `--rule-strong` outline. Below each segment, a `data` 12px label: "{o}% OBSERVED · {n} CLAIMS" and "{i}% INFERRED · {m} CLAIMS".
- **Per-profile rows**: tile S and name (168px), the depth chip (112px), a bar (8px tall, same construction), and `data` "{o} / {i}". Full profiles are listed first, then survey depth, alphabetical within each group.
- **Verification line**: a `--surface-2` box, `--r-m`, padding 20, `body-s`, with the fixed wording: "Every sourced claim in the deep profiles was re-checked against the page it cites on {date}. Claims whose sources couldn't be reached or didn't support them were downgraded to inferred."
- **Compact variant** (hero trust panel and player cards): the same construction at 10px or 6px, without the labels under the segments.
- The section headline states the ratio as a sentence.

### 9.17 Open questions and going broader

- Open questions: an unnumbered list in `body`, at most 6.
- **Going broader**: an `h3` sentence, then one card per survey-depth competitor: a 1px **dashed** `--rule-strong` border (dashed means not done yet), `--r-l`, padding 20. Each card: tile M, the name, and a depth chip; then "A full profile would answer:" with a `body-s` list.
- Close with a `body` line: "A full profile with the same citation check takes a few hours. Ask: {contact}". The contact is shown as selectable text and also linked.

### 9.18 Part 2 opener band

- Full bleed, `--surface-2` fill, `padding-block: 96px` (phone 64), 1px `--rule` top and bottom.
- Contents: the `label` "PART 2 · HOW THIS WAS BUILT", a `display-l` headline (a sentence about the process as an asset), and a `lede` standfirst.
- This is the one register change on the page.

### 9.19 Process rail

- A horizontal stepped rail (a real sequence, so numbered): one column per skill that ran, with a 1px `--rule-strong` connector running through the step numbers.
- Each step:
  - The number (`data` `--ink-3`).
  - The command in a code chip (`data` 13px, `--surface` fill, 1px `--rule`, `--r-s`, padding 4px 8px), only when the step is a real command the reader could run. A step that happens inside another command (the citation check runs within `/competitive-update`) gets a plain `label` instead, e.g. "INSIDE /COMPETITIVE-UPDATE".
  - What it does (15/22, 650).
  - What it produced in this repo, with real counts ("5 profiles written, 3 taken deep"), in 14/20 `--ink-2`.
- Under 720px it turns vertical, with the connector on the left.

### 9.20 Why this compounds

- An `h2` sentence, then a 2x2 grid (phone: 1 column) of four blocks with a 32px gap. Each block: a `label`, an `h4` sentence, and `body-s` text.
- The blocks cover:
  - Living profiles and diffs.
  - Additive depth.
  - Regeneration from source.
  - Commits as a market timeline.
- The first block carries a small inline specimen: the three diff sorts ("MATERIAL", "MINOR", "NO CHANGE") as neutral chips.
- Use this repo's real state (counts, dates, commands), never generic language.

### 9.21 Label specimen and plain documentation sections

- **Labelling discipline**: two rows. On the left, the profile line exactly as it appears in the markdown (`data` 13px, `--surface-2`, `--r-m`, padding 16): one Observed line with its URL and one Inferred line. On the right, how that claim renders on this page: the solid versus hatched bar segment, the matrix edge, the dotted underline and `i`. This ties the method to the visuals.
- **Material change, trust boundary and limits** use plain documentation layout: columns 1 to 8, `h2` labels allowed as plain labels (per the voice doc), `body` text.

### 9.22 Footer and colophon

- 1px `--rule` top border, `padding-block: 48px`. Desktop: two columns; phone: stacked.
- Left, `body-s` `--ink-2`: "Independent analysis by Chris Schubert. Not affiliated with {Target} or any company named here. Logos and screenshots identify each company and belong to their owners; screenshots were captured from public homepages on {date}."
- Right, `data` 11px `--ink-3`: "Accent derived from {Target}'s public brand colour {hex}. Type: {Font} (SIL Open Font License), an open stand-in for {Target}'s own typeface, which is not used here. Data and labels in IBM Plex Mono. Built {date} from {repo link}."

## 10. Deliberately not charted, and banned

- Not charted: geography (no maps), incommensurable scale markers, recommendation timelines (no dates exist), radar charts, sparklines, donuts or any angle-encoded proportion, and scatter plots of inferred positions on numeric axes.
- Banned styling: gradients on grounds, glassmorphism or backdrop blur, drop shadows, emoji, decorative icons, centred hero layouts, accent bars on rounded cards, and full-bleed brand colour.
- Banned content moves: invented exhibits, callouts drawn onto screenshots, recoloured or inverted logos, and taglines or imagery lifted from the target.

## 11. Build and verify

1. `python3 check.py`: the self-contained and em-dash gates, plus the size gate (warn at 2.0 MB, fail above 2.5 MB).
2. Capture and look at: 1440x900 light, 1440x900 dark (the 10-second test, both themes); a full page at 1440 light; a full page at 1024; and a full page at 390 in light and dark. Use `?theme=` to force the theme.
3. On the captures, check that nothing overlaps (event-rail labels, ownership brackets, chips wrapping), that every tile is square and sharp, that no screenshot shows a blocked page or broken image, and that the target column's wash reads in dark.
4. Confirm the Observed/Inferred numbers in the hero, the evidence section and the README are the same count.
5. Read the Part 1 copy straight through against `dashboard-voice.md`.

## 12. Per-run block (top of the generated CSS)

```
/* LANDSCAPE PER-RUN BLOCK
   target:        {name} ({domain})
   lens:          {lens}
   brand primary: {hex}  (source: theme-color | css-frequency | logo; confirmed against screenshot)
   secondaries:   {hexes} (recorded, not used)
   near-black:    {hex or none} (source)
   accent mode:   light {ink|highlighter|neutral} / dark {...}; alert clash: {yes|no}
   font class:    {class} -> {OFL family} (brand face: {name}, not embedded)
   target slot:   {first | last, divided}  (operates in lens market: yes|no)
   tiles:         {slug: mode/plate} ...
   exhibits:      F1 {type}, F2 {type}, ...
   captured:      {date}, locale served per company if not the lens market
*/
```

Tokens are pasted below this block from `derive_tokens.py --css`, and rebuilds reuse them unchanged unless the brand colour changes.
