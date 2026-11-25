# Lint: measured checks before review

Run these on each page you rewrote before its set goes to review. They are mechanical faults with a number attached, so a reviewer shouldn't have to spend its notes on them. Passing lint is necessary, not sufficient: a page can pass every line here and still read as Fieldwork (the kit's sample) with new colours, or as generated.

**The person's system wins.** The values in `page-pattern.md` and the brief are the rule; the numbers here only fill the gaps they leave. Measure with `get_computed_styles` (padding, gap, radius, font size, colour) and `get_node_info` (position and size). Don't judge from a screenshot. Scope every search to the page's artboard (`nodeId`), not the whole file.

**Clearing a line by hiding, deleting or shrinking the thing it points at is a bug,** unless the thing really shouldn't be there. Fix the cause.

## The sweeps (every page)

### 1. Kit leftovers

The kit's sample system is Fieldwork, a made-up survey app for ecologists. Its words, names and figures must not survive, and neither may any of Planed's. Run `find_nodes` with `textValue: "*<string>*"`, scoped to the artboard, for:

- Fieldwork's product and places: `Fieldwork`, `fieldwork`, `Coombe Wood`, `Avon Ecology Trust`, `Severn Vale`, `51.4816`
- Fieldwork's people and their initials: `Imogen`, `Pryce`, `Amara`, `Okonkwo`, `Ruth`, `Hale`, `Leah`, `Marsh`, `Tomasz`, `Nowak`, `Owen Bryant`; two-letter text nodes `IP`, `AO`, `RH`, `LM`, `TN`, `OB` in avatars (a search for full names misses them)
- Fieldwork's objects and IDs: `S-04` (S-0405, S-0409, S-0412, S-0415), `Q-0` and `Q-1` (Q-01 to Q-12), `Transect`, `transect`, `quadrat`, `survey`, `species`, `Wet flush`, `Hedge margin`, `Oak edge`, `spring visit`, and the Latin names (`Primula`, `Hyacinthoides`, `Anemone`, `Quercus`, `Hedera`, `Ficaria`)
- Fieldwork's figures and actions: `8 of 12`, `10:47`, `10:52`, `Sync failed`, `Log quadrat`, `Mark for revisit`, `Add note`, `Export CSV`, `cover`, `312 MB`, `161`, `23 April`
- every other person, object and figure in the table "Fieldwork's sample data, everywhere" in `components.md`
- Planed's words, in case any remain: `Planed`, `Prototype`, `Screen`, `Reviewer`, `Owner`, `Paper calls`, `Checkout`, `Priya`, `Mira`, `fernhill`, `planed.cc`

Read each match before you rewrite it. Short strings also match ordinary words and token names: `Ruth` in "truth", `Hale` in "whale", `cover` in "discover", `survey` in a real survey product, `--color-link` in a colour caption, "screenshot". Those are fine. The leftover is Fieldwork's own noun, person or figure where the person's product doesn't have one.

Rewrite every real match. On the Readme, the changelog line (`v1.0 · generated from the Planed design system kit`), the credit line (`Built with the Planed design system kit · planed.cc`) and the licence line under it (`MIT licence · github.com/Mlock/planed-design-system · the Planed name, mark and viewer look are excluded`) are the three expected matches: leave them. Otherwise keep a match only when it's now the person's own word (their product really has surveys or notes), and say so in the brief's nouns.

### 2. The mark

Fieldwork's pin mark (a map pin with a down arrow, beside the lower-case "fieldwork" wordmark) is an SVG, so the text sweep can't see it. Check by eye, with `get_tree_summary` of the artboard and a 1x screenshot, wherever a mark sits: Icons, Brand and imagery, and any In context scene with the office sidebar (its top holds the mark and wordmark). Replace it with their mark (from Brand and imagery), or remove it if they gave none. Planed's paper-plane mark appears only on Start here (the preview board and the eyebrow), the one page where it stays.

**Fieldwork's images.** The text sweep can't see images either. Every map surface in the kit (cards, scenes, pin tiles, the Readme cover) carries Fieldwork's woodland tint as a `background-image` over the `--color-sage` ground. Find them per page with `find_nodes` and `filters: [{styleName: "backgroundImage", styleValue: "*01M89CV0MJN8RYCWFVWES094CK*"}]`. If the person's product has no map, set each match's `backgroundImage` to `none`; the ground falls back to its token colour. If it has a map and their moodboard has a texture or ground that fits, use that image instead. Raster `<img>` nodes are Fieldwork's too, such as the misty-wood stock photo in Brand and imagery's Don't. Rewrite or remove them with the rest of their section. The six example tiles on Start here are the one exception: they stay.

### 3. Fonts

`find_nodes` with `filters: [{styleName: "fontFamily", styleValue: "*<family>*"}]` for each family that isn't the person's: at least `*IBM Plex*` (the kit's), `*Inter*`, `*Geist*`, `*Newsreader*`, `*Helvetica*`, `*system*`. A node whose family reads `var(--font-…)` is fine. A literal family is a fault: text without its own family falls back to Inter (`paper-quirks.md`), and a literal Plex left from the kit won't follow the font tokens. Set it to `var(--font-sans)`, `var(--font-display)` or `var(--font-mono)`. The example tiles on Start here (Inter, Newsreader) and the preview board (Geist) are the kit's own and stay.

**SVGs hide from the sweeps.** `find_nodes` doesn't see text or fills inside an SVG. The kit's diagrams (Motion's curves, Icons, the map art's contours and transect lines, the pin mark) can carry SVG text and literal fills like `#1F261D` (or `#3E3428` in an older copy), `#4F6B3A` or `#000000`. On a page with SVG diagrams you keep, read each SVG with `get_jsx` and set its text and fills to their tokens.

### 4. Raw hex

`find_nodes` with a wildcard hex (`#*`) returns nothing, and a filter with no value matches everything. Instead, read `get_jsx` of the page section by section and look for colour literals outside `var(...)`. Known suspects in the kit:

- Fieldwork's primitives written as literals: `#1F261D` ink, `#5B6157` slate, `#8C9187` ash, `#DCE0D7` line, `#C9CEC4`, `#E8EBE4`, `#F4F5F1`, `#FBFBF9` paper, `#EEF0EB` canvas, `#B03A2E` oxblood, `#7D3A0F`, `#4F6B3A` moss, `#E0662B` signal, `#C9D3B0` lichen
- the same primitives in an older copy of the kit (before 25 November 2026): `#3E3428` bark, `#6B6255`, `#9A9285`, `#E2DED4`, `#D3CEC1`, `#EEEBE1`, `#F5F3EC`, `#FBFAF5` paper, `#F1EFE7`, `#A63A26`, `#8A2F1E`, `#F7E5DF`, `#8C3A13`
- fades and gradients over crops (a literal canvas fade, `#EEF0EB` or `#F1EFE7` in an older copy, on some scenes; gradients can't use tokens, so repaint them from the person's palette, see `paper-quirks.md`)
- `#FBFAF5` in focus rings (older copies; the kit now uses `var(--color-surface)` there), and `#FFFFFF` or `#000000` anywhere

If a match equals one of the person's own token values (check `get_tokens`), swap it for that `var(…)`; it isn't a kit leftover.

Swap each for the matching token. **One exception: gradients.** `var()` doesn't resolve inside a gradient (`paper-quirks.md`), so a gradient takes literal hex from the person's palette. That covers a dot grid kept for a canvas product and a Don't that shows a gradient as the mistake. Use only their palette's values, and note it in your report. Shadow colours (ink at an alpha: `#1F261D14`, `#1F261D0A`, `#1F261D1A`, `#1F261D0F`, `#1F261D17`; bark `#3E3428…` at the same alphas in an older copy) are the recipes and stay literal; the shadow sweep in step 3 re-tints or deepens them (`tokens.md`, "Shadows"), so any left on a page you rewrite is a leftover from the sweep. An In context scene that shows the person's product draws it on their tokens: no literal hex there either.

### 5. Off-scale type

Scenes drawn freehand drift off the type scale (11, 12, 13, 14, 16, 18, 24, 32, 36, 48, 72), and `find_nodes` has no "not in" filter. Sweep for the sizes dry runs kept finding: `find_nodes` scoped to the artboard with `filters: [{styleName: "fontSize", styleValue: "<n>px"}]` for 10, 15, 17, 20, 22, 28 and 44. Move each match to the nearest scale step. Initials in avatars are 11 at the smallest.

## Lines that are never intentional

| Line | What it means | Fix |
|---|---|---|
| **Tight inset** | Words less than 8px from the edge of their card, panel, row or button; 12px or the system's padding is right. | Restore the container's padding. Never let text set the edge. |
| **Tight control** | A button or chip less than 8px below the field, line or card edge above it. | Give it the system's gap, or at least 8px. |
| **Touching** | Text within 4px of a neighbouring box, usually leftover `space-between` with no `gap`. | Set a fixed `gap` of 8–12px. |
| **Tight or loose stack** | A title and its subtitle with less than 3px or more than 10px of visible ink between them. 4–6px reads as one item. | Line height plus a 2–4px gap. |
| **Near-tangent** | Two edges 1–3px apart, which looks like an accident. Check corners too. | Align them exactly, or part them by at least 8px. |
| **Baseline** | Text, links or numbers side by side in one row that don't share a baseline. | `align-items: baseline` on the row, or give them the same line height. |
| **Same figure twice** | A number, date or name stated twice on the page in two places or two forms. | Search the page's text for every key figure; keep it where it drives a decision. |
| **Uneven padding** | A card or tile whose content sits about a third closer to one edge than the opposite one. | Even out the padding, or restructure so the content fills the box. |
| **Nested radius** | An inner shape's radius plus the padding around it doesn't equal the outer radius, so corners look pinched or bloated. This is the line a radius-scale change breaks most often. | Outer radius = inner radius + padding, rounded to the nearest radius token. |
| **Mixed radii** | A literal kit radius survives next to the token-bound ones (a 6 button beside pill buttons; an 8 sheet beside 20 sheets). Not a fault: a literal `999px` on a radio, status dot, toggle knob or avatar kept round on purpose, or an off-system shape drawn as a Don't (`tokens.md`, "Round things"). | Bind it to its token with the fallback sweep in `tokens.md` ("Set: the radius scale"). |
| **Fat row** | A one-line row more than about three times taller than its text (matrix rows of 72 are the pattern, not a fault). | 12px row padding (8px when dense). Never pad a row to fill a pane. |
| **Loose list** | Rows spread apart to fill the height of their pane. | Tighten to the row padding and let the pane end, or add real rows. |
| **Empty pane** | A void under a list or column, or an In context canvas with a scene that fills half of it. | Fill it with real content, resize the canvas, or rebalance. |
| **Clipped** | Text, a button or an icon cut off by its container or a fixed height. | `height: fit-content` on the artboard, or fit the content. |
| **Wrapped unit or amount** | A number on one line and its unit or currency on the next, or an amount that breaks across two lines. | `white-space: nowrap` on the pair, or shorten the copy around it. |
| **Mixed icons** | Filled and outline icons, or two stroke weights, side by side in one nav, list or toolbar. | One family, one stroke, one size per page, as the Icons page says. |
| **Hand-drawn mark** | An icon or logo drawn for this page when the Icons page or the person's assets have one. | Use their icon or asset. If there isn't one, leave it out. |
| **Grey-box product** | An In context scene, thumbnail or preview drawn as grey bars or an empty frame. | Draw a believable scene from their product on their tokens. A skeleton only for a state that is genuinely loading, and the copy says so. |
| **Invented logo** | A letter in a coloured square standing in for a company or product mark. | Use their real mark, or set the name as plain text. |
| **AI shorthand** | Sparkles, wands, stars or purple used to mean "AI". | Show what the feature does, with the product's own icon. |
| **Off-scale** | A font size, weight, radius, spacing or colour that isn't in the system. | Swap it for the nearest token or scale value. |
| **Fallback font** | Text rendering in the system sans because the family didn't resolve. | Use the font tokens, or the exact family from `get_font_family_info`. |
| **Not to scale** | A bar, meter or chart whose size doesn't match its number. | Draw it to the data. |
| **State that doesn't add up** | A count that doesn't match its list, a total that isn't the sum of its rows, a date that contradicts another on the page. | Change both together; recheck every figure in the scene. |
| **Off the ledger** | A person, ID, part, figure, date or status that differs from the ledger in the brief (an invoice with other line items, a different due date, another person's initials). | Use the ledger's. If the page needs something new, add a new object and report it; never change a fact about an existing one. |
| **Dot or badge out of bounds** | A status dot, badge or focus ring outside its row's content edge, or within 4px of the text it marks. | Keep it inside the inset, at least 6px clear of the text. |
| **Status wrong** | The lead's last sentence still names Fieldwork's places (`survey pages, the field app`), says `In the product` for something their product doesn't have, or is missing. | End the lead with `In the product <where>.` or `Not built yet.` (`page-pattern.md`, "The header"). |
| **Eyebrow or status dot** | A file line, a small label or a coloured dot above the H1 or a section title. | Delete it; fold anything it said into the lead or the intro. |
| **Grey running text** | A lead, a section intro or a sentence in a well caption set in `--color-foreground-muted`. | `--color-foreground`. Muted is for captions under specimens and table meta only. |
| **Middle-dot meta** | A doc caption written as `a · b · c` ("Sidebar · 16"). Product strings inside a scene (`S-0412 · Transect 4`) are the product's own and stay. | A plain short phrase with commas, or two lines. |
| **Empty well** | A Do or Don't well much taller than its example, with the example small in the middle. | `height: fit-content`, padding 24, example left-aligned at real size. |

## What you see, what you do

These can't be measured, but you can see them in a 1x screenshot before the reviewer does.

| You see | You do |
|---|---|
| The page reads as Fieldwork with the person's colours: the survey map, quadrats, species records and the phone log form are still the subject | Rebuild the In context scene and the examples from their product. This is the first thing the reviewer checks. |
| The page looks emptier or flatter than the kit's version of it | Match the kit's level of care: as many states, a scene as specific, Do and Don't as carefully drawn. |
| An In context scene that could be any product | Use their nouns, their data, their screen. Name the place in the section title. |
| Every row has the same card, button and chip | Take the card off the rows. Give the strong action only to the row that needs it. |
| A mono or uppercase label over almost every section | Keep labels only where the pattern prescribes them or they carry information. |
| The same art or scene stands for two different things across pages | Use distinct scenes, or a neutral treatment for one of them. |
| A Do and its Don't that differ only in colour | Make the Don't a real mistake someone on their team would make. |
| Two rounds in a row with the same blocking failure mode | Stop polishing; change the composition (see the stall rule in SKILL.md). |
