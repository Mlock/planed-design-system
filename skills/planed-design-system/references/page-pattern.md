# Page pattern

Every Foundations and Components page in the kit is one 1440-wide artboard built the same way. This file is that anatomy, measured with `get_computed_styles` on the gold board. Keep it when you rewrite a page: the person's system should read as one file, page after page.

**The gold board** is the Button page's artboard, node `B8T-0` on page `p-C-0` (Button) in the kit file `01M893XQADCXH6Y0W6JCJZJK2E`. It shows Fieldwork, the kit's sample system: take its anatomy and care, never its content. In the person's copy the IDs may differ: find it with `get_children` of `root_node_<their Button page id>`. Screenshot it before your first page, and compare each finished page with it.

**Examples here are examples.** The quoted sentences in this file ("Pressed keeps the tint while its confirm is open", "Shown at 40, the size in the office app…") show the kind of thing to write. Never copy one onto a page; write the sentence for their component.

Values below are the kit's, measured with `get_computed_styles` on `B8T-0` (re-measured 25 November 2026, after the eyebrow, the status dot and the sheet drop came out). Colours, font families and radii are tokens (`var(--…)`), so they already follow the person's tokens: a radius of 8 here is `var(--radius-lg)`, 6 on a field, well or canvas is `--radius-md`, 6 on a button or tag is `--radius-full`, and 999 on a dot, pin, radio or avatar is a literal kept round on purpose (the full mapping is in `tokens.md`, "Set: the radius scale"). **Sizes, gaps and shadows are literal pixels on the boards**: when the brief changes density or depth, you change them per page (see `tokens.md`, "What set_tokens does and doesn't restyle"). Anything new you draw uses the radius tokens, never a literal.

## The artboard

| Property | Value |
|---|---|
| Width | 1440 |
| Height | `fit-content` (never a fixed height) |
| Padding | 72 top, 80 left and right, 96 bottom |
| Layout | flex column, gap 32 |
| Background | `var(--color-background)` |
| Overflow | clip |

Children, top to bottom: the page header, then one section per topic (usually three to five), ending with **Usage**.

## The header

A flex column, gap 16, with 32 of padding below it (so the first section starts 64 under the lead: 32 padding + 32 artboard gap). There is no eyebrow above the title: no file line (the Paper page list already names the file and the group) and no status dot.

**Title row.** Flex column, `align-items: flex-start`, gap 16. The lead sits under the H1, not floating on the right.

- **H1:** the page name. 48/52, semibold (600), `--font-display`, `--color-foreground`. Letter-spacing is the kit's `-0.01em`, written as a **literal** on every board (set for IBM Plex Sans). Use the brief's display tracking instead (`tokens.md`, "Leave unless the brief calls for it"): on each page you rewrite, set the H1's `letterSpacing` to that value as part of the header. Where this file says -0.01em, read the brief's value.
- **Lead:** 560 wide, `flex-shrink: 0`. 16/24, regular, `--font-sans`, **`--color-foreground`** (full ink: grey running text reads unfinished). Two or three sentences that state the page's rule in the person's voice: what this component is for in *their* product, and the one thing it never does. Never a definition you could find in any design system.
- **The status is the lead's last sentence.** Every page says whether the thing exists in the product, in the same voice and colour as the rest of the lead:
  - Built: a sentence that starts **`In the product`** and names where it appears, in the person's places. The kit's Button lead ends "In the product on survey pages, in the field app and on every sheet."
  - Not built: a sentence that starts **`Not built yet`**, with any qualifier after it ("Not built yet, apart from the meters." / "Not built yet; it would replace the Count field in the log form.").
  - Rewrite the places every time: Fieldwork's places are a leftover. This sentence is the place to be honest about what exists. Keep it in sans; use `var(--font-mono)` in it only for a real code path they gave you.
  - Later runs and reviewers read the status from this sentence, so always start it with one of those two phrases.

## A section

Every topic is a white sheet:

| Property | Value |
|---|---|
| Layout | flex row, gap 48 |
| Padding | 40 |
| Radius | 8 (`var(--radius-lg)`) |
| Background | `var(--color-surface)` |
| Shadow | the **Sheet** recipe: `#1F261D14 0 0 0 1px`, an ink-tinted hairline ring and no drop. A sheet is a hairline or a drop, never both; only what opens over a sheet lifts (`tokens.md`, "Shadows") |

Inside it, left to right:

1. **The intro column.** 220 wide, `flex-shrink: 0`, flex column, gap 8.
   - Section title: 24/30, semibold, letter-spacing -0.015em, `--font-sans`, `--color-foreground`. Short and specific ("Variants and states", "Sizes", "On Transect 4").
   - Intro: 14/21, regular, **`--color-foreground`** (ink, like the lead). Three to six lines that give the section's numbers and rules in words ("Shown at 40, the size in the office app. Hover darkens or fills; focus adds a 2px ring 2px out").
2. **The content.** `flex: 1 1 0`, `min-width: 0`. One of the three kinds below.

### Content kind 1: the matrix

The states table. Used for "Variants and states", "Values and states", "Tones", "Kinds" and similar.

- Container: flex column.
- **Head row:** 32 tall, flex, centred, a 1px bottom border in `--color-border`. Labels 12/16, regular, `--color-foreground-muted`.
- **Body rows:** 72 tall each, flex, centred, a 1px bottom border in `--color-border`.
- **First column** (the row label): 200 wide, flex column, gap 2. Name 14/18 medium `--color-foreground`; a note under it, 12/16 regular muted, giving the size, the fill or the token as a plain short phrase with commas ("The one moss action, no lift"). Never a middle-dot string (`a · b · c`).
- **State columns:** fixed-width slots (170 each on Button), `flex-shrink: 0`, so the lanes line up down the table. A column for each state the component really has, usually Default, Hover, Focus, Disabled; add Pressed, Loading, Error, Selected only where the component has them.
- A cell that has nothing to show holds a short muted sentence saying why ("Pressed keeps the tint while its confirm is open"), never an empty slot.
- **`New` markers on column heads.** The kit marks states Fieldwork hasn't built with `New` in the column head (12/16, `--color-foreground-disabled`). Drop the marker unless the brief says that state isn't built in the person's product. If the whole page is not built (its lead ends "Not built yet"), drop them all: the lead already says it.
- **Numbers line up.** Amounts, counts and IDs in a column take tabular figures: `font-variant-numeric: tabular-nums` (`update_styles` with `fontVariantNumeric: "tabular-nums"`) works in Paper. Set it on every number column and total.

### Content kind 2: specimens

A row or grid of examples with a caption under each: name and size 13–14 medium ("md, 40"), then a muted line saying where it's used, as a plain phrase ("Office app, 14 text, the default"). Muted grey is only for these captions and table meta; running text is ink. Used for Sizes, Icon button, anatomy callouts. Spacing between specimens is a fixed gap (48–56 on Button), aligned on the baseline or the bottom.

### Content kind 3: In context

The section that shows the component in the person's real product. It is what makes the page theirs, so it gets the most care.

- **In a section:** a canvas frame, `flex: 1 1 0`, `min-width: 0`, a fixed height that fits the scene (820 on Button, which holds the office survey page beside a phone; 480–720 elsewhere), radius 6 (`var(--radius-md)`), overflow clip, `position: relative`, on a plain `var(--color-surface-sunken)` ground. Product windows and phones sit on it with the **Window** recipe. A dot grid suits only a product with a working canvas; gradients can't use `var()` (see `paper-quirks.md`), so any gradient takes literal values from the person's palette.
- **Full-bleed variant:** some pages (Table, Typography, Charts, Brand and imagery, Accordion, Map controls, Sidebar and others) break out of the sheet for a window scene. The section is 1440 wide, `position: relative; left: -80px`, flex column, gap 28, 16 top padding. Its intro is a row (120 side padding, gap 48): the title at 220 and a 560-wide paragraph in ink. The canvas below is 1440 wide, `height: fit-content`, with inset hairlines top and bottom (`#1F261D14 0 1px 0 inset, #1F261D14 0 -1px 0 inset`) on `var(--color-background)`.
- **Crop to the subject.** A scene shows the part of the product the page is about, at 1x where it can be read, not the whole window again. In the kit, Typography, Charts and Brand and imagery put the office window in a **window crop**: a frame with a fixed width and height, `overflow: clip`, radius 8 (`var(--radius-lg)`) and the Window recipe, with the full window inside it at `position: absolute` and a negative `left`/`top` (Typography and Charts: 744 wide at `left: -696`, showing the quadrat list and the drawer; Brand: 704 wide at `left: 0`, the sidebar and the map). On the full-bleed canvas the crop lines up with the intro paragraph (`padding-left: 388`, 48 above, 56 below). Card's Today scene drops the sidebar instead and shows the main panel whole. A crop edge falls between rows or past the last word, never through a word, a row or a pin label.
- **What goes in it:** a scene from the person's product with this component doing its job: a real screen of theirs if they dropped one on Start here, otherwise a small believable scene drawn on their tokens. Name the scene in the section title (Fieldwork's "On Transect 4" becomes "In the cart", "On the booking page"…). Use their nouns and believable sample data that adds up.
- In the kit, the scenes show Fieldwork's own product: the office survey page, the quadrat drawer, the phone with its map and log form. They are drawn on the kit's tokens, so after the token swap they already wear the person's colours and fonts and can look finished. They aren't: the subject is still Fieldwork's surveys and quadrats. In the person's system **the product is theirs**. Delete the kit scene and rebuild it from their product; never just recolour or relabel it.

### The Usage section: Do and Don't

The last section on every page. The content is a flex column of **pairs**, gap 32; each pair is a row of two columns, gap 24.

- Each column: flex column, gap 12, `flex: 1 1 0`.
- **The well:** sized to its content. `height: fit-content`, padding 24, radius 6 (`var(--radius-md)`), `var(--color-surface-sunken)`, flex, gap 8, `justify-content: flex-start` (a column well also takes `align-items: flex-start`). The example sits **left-aligned at real size**, never small in the middle of a big empty well: two buttons, a field and a button, a row. Real components on the person's tokens, never grey bars. A well whose example is absolutely positioned (a popover over a field, a scrim) keeps a fixed height that shows it whole.
- **Pairs line up.** When the Do and the Don't show the same thing, build them from the same parts in the same place, so the mistake is the only difference you can see.
- **The caption:** flex row, gap 8. The verdict, 44 wide: `Do` in `--color-success` or `Don't` in `--color-error`, 13/18 semibold. Then the reason, 13/18 regular `--color-foreground`: one sentence saying what goes right or wrong for the *user*, in the person's nouns.
- Two pairs is the norm. The Don't must be a mistake someone on the person's team could plausibly make, drawn as carefully as the Do.

## Status, names and nouns

- Layer names follow the kit: `Page header`, `Title row`, `Lead`, `Section · <Title>`, `Section intro`, `Matrix`, `Head`, `Row · <State>`, `Pairs`, `Pair · <Topic>`, `Do`, `Don't`. Keep them; later runs and reviewers find sections by name.
- The page's H1 is the component's generic name (Button, Select). A page the person's product calls something else may say so in the lead ("Called Switch in code").
- Every visible word is in the person's voice and nouns from the brief. Fieldwork's nouns (survey, transect, quadrat, visit, record, observer, lead, note) only stay where they are also the person's words.

## Checks before a page is done

1. Screenshot the page beside the gold. Same header rhythm, same section sheet, same intro width, same matrix row heights. No running text in grey, no eyebrow or status dot, no well that is mostly empty.
2. Nothing clipped: the artboard is `fit-content`, and no In context canvas cuts its own scene off mid-element unless the crop is deliberate.
3. Run the sweeps in `lint.md` (fonts, raw hex, specimen leftovers) scoped to the page's artboard.
