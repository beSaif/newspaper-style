---
name: newspaper-style
description: Build web UIs, dashboards, reports and A4 PDFs in the "newspaper style" from mutz: a Swiss two-column grid on white paper, black type in Helvetica, hairline rules instead of cards, one thin vertical rule, all black by default with an optional single accent for actions, every claim with a numbered source, and a single small mascot as the only personality. Use whenever the user asks for the newspaper style, the mutz look, a Swiss/editorial/print-like interface, or wants a tool that reads like a well-set broadsheet rather than a SaaS dashboard. Covers tokens, type, layout, components, copy voice, print CSS and a review checklist, with a starter stylesheet and example page in assets/.
---

# Newspaper style

This style came from **mutz**, a research navigator built for the Bern Economic Development Agency. It is a Swiss
editorial look: the page reads like a well-set newspaper. Information is laid out in rows and columns, separated by
rules, and nothing decorates it. Colour does a job or isn't there.

Start from `assets/newspaper.css` (screen) and `assets/print.css` (A4). `assets/example.html` shows every component
on one page. Copy them into the project and adapt the class names to the codebase. Spend your effort on content and
hierarchy, not on decoration.

## The five rules

1. **Palette with roles.** Black, greys and white. All black by default; at most one accent colour, and only if the
   user or brand asks for one. Each colour has a single job.
2. **Type with roles.** One sans family, two weights, a fixed scale.
3. **Two-column grid.** Labels left, content right, flush left, lots of white space. Rows and tables, not cards.
4. **One signature element.** A thin vertical rule between the two columns, on every main screen and down the
   printed page.
5. **One place for personality.** A small mascot (in mutz: a black bear head with a scarf bar) at the bottom right.
   Everything else is quiet.

If a choice breaks one of these, don't make it.

## Tokens

```css
--accent:#111111;   /* actions, the vertical rule, the active tab. Nothing else. Black by default. */
--accent-h:#333333; /* hover on the accent; error accent */
--tint:#F2F2F2;     /* rare: a highlighted row */
--black:#111111; /* text, borders of controls, inverse blocks */
--grey:#5E5E5E;  /* secondary text, labels, metadata (7:1 on white) */
--rule:#D9D9D9;  /* hairlines between rows */
--panel:#FAFAFA; /* sub-bar, hover row, selected row */
--panel2:#F2F2F2;/* button hover, inputs at rest, selected list item */
--paper:#FFFFFF;
--font:"Helvetica Neue",Helvetica,Arial,sans-serif;
```

- No other hues and no gradients. One exception is allowed per product, for one data meaning only (mutz: honey
  `#C68400` fills the coverage pot and nothing else).
- **Default is all black.** Use black for the accent unless the user asks for a colour. To add one, set
  `--accent`/`--accent-h`/`--tint` and keep the rule that it is the only colour. Mutz used the Canton of Bern red
  (`#E30613` / `#B8000F` / `#FCE3E5`).
- When everything is black, the current step and active tab are told apart by **weight** (bold) and the 3 px bar,
  not by colour.
- No shadows except a 1 px offset hard shadow on floating panels (`0 2px 0 var(--black)`), no blur.

## Type

- Family: `"Helvetica Neue", Helvetica, Arial, sans-serif`. Bold (700) for titles and emphasis, regular (400) for
  text. Nothing in between, no italics except quotes.
- Scale in px: **28 / 24 / 21 / 18 / 15 / 13 / 12**. Body 15/1.5. Page title 24–28. Row title 18–21. Metadata and
  labels 12–13 in grey.
- **Kicker**: 11 px, bold, uppercase, `letter-spacing:.06em`, grey. Sits above a heading like a newspaper section
  label ("WHY", "EVIDENCE", "SOURCE").
- Headings `line-height:1.2`. Sentence case everywhere. Never all-caps headings beyond the kicker.
- Numbers in metadata are digits joined by a middle dot: `10 matches · sorted by evidence × recency`.
- German or long compound text: `hyphens:auto`. URLs never hyphenate.

## Layout

- **Masthead** (top bar, white, 1 px black rule below): an accent square and the product name in bold on the left,
  the section nav as plain text with the active item bold and a 3 px accent underline, quiet grey text on the right
  (disclaimer, user).
- **Sub-bar** (panel grey, hairline below): breadcrumb `Leads / Item name` with the item in bold, a boxed chip for
  status, and a step bar on the right. Each step has a 3 px top border: grey = not reached, black = done,
  accent = current (bold).
- **Body**: two columns. Left column 260–300 px for the index, verdict and filters. Right column is the story.
  Between them, the 1 px accent vertical rule, full height. Padding 24–32 px.
- **Rows, not cards.** List items are rows separated by 1 px `--rule` hairlines. The first row of a list gets a
  black top rule instead, like the line under a newspaper section header. Each row is itself a small two-column grid:
  a 110 px grey label column ("Person", "Unit", the affiliation) and the content.
- Square corners. 2 px radius on inputs only. Buttons and controls are 44 px tall (36 px for small ones).
- Lots of white space, flush left, ragged right. No centred body text.
- On phones (< 900 px) the columns stack, the vertical rule disappears, and drawers become bottom sheets.

## Components

All of these are in `assets/newspaper.css` and shown in `assets/example.html`.

| Component | How it looks |
|---|---|
| Button `.b` | white, 1 px black border, bold 14 px, 44 px tall, square |
| Primary `.b.p` | solid accent (black by default), white text. One per view: the action that moves work forward (Accept, Send) |
| Toggle on `.b.on` | solid black, white text. Used for the active filter ("All 10") |
| Segmented filter | a row of `.b.s` buttons with counts: `People 4`, `Units 5`. Active one black |
| Verdict block `.verdict` | black box, white bold 18 px, a small grey label above ("Verdict"). The headline answer |
| Row `.res` | label column + content; title 21 px bold, grey subtitle, body 15–18 px, metadata line in grey |
| Quote `.qt` | italic, 3 px black left bar, 12 px indent. Or inline in grey with curly quotes and a `[n]` ref |
| Source chip `.src` | boxed `[1] example.org`, 1 px black border, 13 px. Clicking opens the page at the quote |
| Ref `sup.ref` | `[1]` after the claim, linked to the source list |
| Chip `.chip` | 12 px, 1 px black border; dashed when tentative |
| Tag `.tg` | 12 px, hairline border, grey text; black border and text when it's the active signal |
| Table `table.t` | header 12 px grey regular with a 1 px black rule under it; hairline rows; no zebra |
| Definition list `dl.pr` | grey 12 px label left, value right |
| Meter `.bar` | 4 px tall hairline track with a black fill, label and `n of N` above. No big numbers, no donuts |
| Tabs `.tb` | boxed group, active tab solid black |
| Steps `.st` | 3 px top border: grey / black / accent as above |
| Timeline `.tl` | 2 px black left line, square markers, a filled marker for the current event |
| Error `.err` | white, 1 px black border, 4 px accent left border, plain sentence of what happened and what to do |
| Empty / no match | say so plainly ("No match · nothing with evidence") and list what was searched. Never a weak guess |
| Links | no underline; a hairline under at rest, a full black line grows from the middle on hover (.15 s) |
| Focus | 2 px solid black outline, 2 px offset |
| Footer | grey 12 px disclaimer, e.g. "Prototype, not an official tool" |
| Mascot | inline SVG, ~72 px, fixed bottom right. Black with white details and one accent bar (a white edge keeps it apart from the head when the accent is black). Poses for idle, searching and sad (error). The only playful thing on the screen |

## Content and voice

The style is as much about how things are written as how they look.

- **Every claim has a source.** A statement shows the quote it rests on and a numbered link to the page. If there
  is no source, the UI says so instead of guessing.
- **Plain, short sentences.** Sentence case. No exclamation marks, no marketing words ("seamless", "powerful",
  "unlock"). No em dashes: use a comma, a full stop or a middle dot.
- **Say what happens.** Button labels are verbs for the actual effect ("Send the clean PDF to the company", "Accept",
  "Undo"). Status reads like a caption: `Active · 2 quotes, 2 pages · strong evidence`.
- **Honest states.** "No match", "Not searched", "The search did not answer." followed by what to try next.
- **Grey for the how, black for the what.** Metadata, counts and provenance are grey; the finding is black.
- The mascot can have a light line ("Bear with me…") in loading states. Nowhere else.

## Print (A4)

`assets/print.css` sets the same look for documents rendered with WeasyPrint or the browser:

- A4, margins 22/18/20/18 mm, 9.5 pt body, 1.45 line height, `hyphens:auto`.
- Cover page: logo, 26 pt title, "For <recipient>", a label/value meta table, a short intro. The disclaimer prints
  once, on the cover footer. Page numbers `n / N` bottom right on the rest.
- Sections start on a new page with a kicker (WHY / WHAT / HOW), an h2 and a grey lede.
- Items are separated by a 0.2 mm hairline at the top, never boxed. `page-break-inside:avoid` on each.
- Superscript `[n]` refs in the accent (grey in the clean copy), and a numbered source list at the end with full URLs.
- A "review copy" variant adds a bordered banner, each quote under its claim, and a running header
  "Review copy. Not for sending."

## Don't

- Cards with rounded corners and drop shadows, gradients, glassmorphism, coloured badges.
- A colour nobody asked for. If there is an accent, it goes only on actions, the rule and the active state, never
  on text for emphasis.
- Big hero numbers, donut charts, KPI tiles. Use a row with a thin meter.
- Icons as decoration. Icons only where they carry meaning, 1.8 px stroke, `currentColor`.
- Centred layouts, multiple accent colours, emoji in UI copy.
- A second mascot moment in the middle of the page.

## Review checklist

Before calling a screen done, check:

- [ ] Only black, greys and white (plus one accent if asked for). The accent appears only on actions, the vertical rule and the active tab/step.
- [ ] One primary button per view.
- [ ] The two columns and the vertical rule are there on main screens.
- [ ] Lists are rows with hairlines; the first row has a black top rule.
- [ ] Font sizes come from 28/24/21/18/15/13/12; only 400 and 700 weights.
- [ ] Square corners except 2 px on inputs; controls ≥ 44 px (36 px small).
- [ ] Every factual statement has a `[n]` source or an explicit "no source".
- [ ] Copy is sentence case, plain, no exclamation marks or em dashes.
- [ ] Empty, loading and error states exist and say what happened.
- [ ] Contrast ≥ 4.5:1 for text, visible focus outline, works at 375 px wide.
- [ ] The mascot (if any) is the only personality on the page.
