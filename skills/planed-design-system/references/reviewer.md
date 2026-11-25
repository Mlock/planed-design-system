# Reviewer brief

You're reviewing a set of pages (up to four) in a design system someone has just generated in Paper. The file started as the Planed design system kit, a sample system for a made-up product called Fieldwork (a survey and field-notes app for ecologists: surveys, transects, quadrats, species records, an office survey page and a phone), and an agent has rewritten it for the person's own product from their moodboard. You did not build it. Look at it the way the most exacting design lead you know would on a first review: the one who screenshots a single wrong thing and sends it back with "what is this?". Only what's on the canvas counts.

You answer three questions, in this order:

1. **Theirs, not the kit's?** Does each page read as the person's own product's design system, or as Fieldwork's with their colours poured in? This outranks everything else.
2. **Does it feel human-designed?** Would an experienced product designer believe a person with a point of view made it, not a generator filling in a template?
3. **Is it on-system?** Their tokens, their type, the shape language from the brief, and the page pattern every page follows.

You are read-only. Don't edit, move or create anything in the file.

## What your prompt gives you

- the file ID, and the page and artboard IDs in this set
- the path to the brief (mood, palette with roles, type pair, shape language, density, voice, the product's nouns) and its **ledger**: the one set of sample data every page draws from (today's date, the people, the objects with their parts, dates and status, the timeline)
- the paths to this skill's `references/page-pattern.md`, `references/lint.md` and `references/components.md`
- the bar: their Button page once it has passed review (its page and artboard ID), or, before it has, `page-pattern.md` alone
- earlier rounds' reviews for this set and the builder's responses, if any
- whether this is a default review (pass at 8) or `--thorough` (pass at 9)

## The evidence rule

**The bar for a finding is a screenshot or a node you looked at.** Every blocking note cites one: the screenshot (its scale and the region) or the node ID with the value you read. A problem you predict from the brief is not a finding, and neither is a pass you predict. If you need a view you don't have, take it before you write the note.

## How to look

1. **Read the brief and the ledger first.** Note the nouns, the shape language and the ledger; you will check every page against them.
2. **Theirs, not the kit's.** For each page:
   - Run the leftover sweep from `lint.md` ("Kit leftovers") with `find_nodes`, scoped to the artboard. Any match that isn't now the person's own word is a blocking note.
   - Screenshot the In context section at 1x. Is the scene from *their* product, with their nouns and data, drawn on their tokens? Or is it still Fieldwork's (the survey page with its map and quadrat list, the quadrat drawer, the phone log form, contour maps with pins) in new colours? The kit's scenes are drawn on tokens, so they recolour themselves and can pass a glance: read the words and the subject, not the palette. Fieldwork's concepts surviving as the subject of a page is the most important finding you can make, unless the brief says their product genuinely has them.
   - Read the lead and the Usage captions. Are they rules for their product in their voice, or Fieldwork's rules reworded?
   - Check the status: the lead's last sentence reads `In the product <their places>.` or `Not built yet.`, never Fieldwork's places. There is no eyebrow, file line or status dot above the title.
3. **Thumbnail.** Screenshot each artboard whole. A tall board comes back small; that's your thumbnail. Note where the weight sits and whether each section has real content or chrome.
4. **First read.** Screenshot each page's sections at 1x (use `get_children` of the artboard to find them). Write down what the eye lands on first, second and third. Does that order match what the page is for?
5. **Against the pattern and the bar.** Compare with `page-pattern.md` (header rhythm, 220 intro column, section sheets, matrix rows, Do and Don't wells) and, if you were given one, the passed Button page. Name the **one biggest difference** in quality: is this page the emptier, flatter, more boxed or more generic of the two?
6. **Dense areas at 2x.** Matrices, tables, captions, small labels. Read the copy and the numbers. Check that the numbers add up, nothing is clipped or wrapped where it shouldn't be, and charts and bars are drawn to their numbers.
   - **Against the ledger.** Every person, object, part, figure, date and status on the page matches the ledger. A page may show a subset, or a new object the ledger lacks, but never a different fact about a ledger object. A contradiction is a Made-up note, wherever it sits; cite the ledger line it breaks. Because every set is checked against the same ledger, this is also the check across sets.
   - **The shell.** The ledger's shell (the app's window, nav, sheet and popover widths, recurring scenes, status dot size, scene type sizes) is checked the same way: a sidebar, width or scene that differs from the ledger's is a Made-up note. A ledger line marked page-local applies only to its page.
   - **Never propose a timeline of your own.** If a page shows something the ledger doesn't cover, write a polish note ("add to the ledger: …") rather than inventing the fact for the builder.
7. **Measure, don't eyeball.** Run `get_computed_styles` on a few representative nodes per page: the H1, a body line, a button, a matrix row, a section sheet. Look for:
   - colours outside `var(--color-…)` that aren't shadow recipes (raw hex left from the kit)
   - literal font families that aren't the brief's (the font sweep in `lint.md`)
   - radii that don't follow the brief's shape language, or a kit radius left beside the new ones
   - sizes off the type scale
   - nested corners that don't add up
8. **Across the set.** Do the pages look like one designer made them? Same In context care, same caption voice, same ledger, same shape language.
9. **Earlier rounds.** Mark each earlier blocking note fixed, partly fixed or not fixed. Don't reverse an earlier note without saying why.

**Confirmation reviews.** If your prompt says this is a confirmation, check only the changed nodes it lists and whether the page still reads as theirs. Return PASS, or one blocking note.

## Failure modes

Name one in every blocking note. Put the main one first when a note fits two.

- **Kit's.** The page still documents the kit's sample product, Fieldwork (its scenes, nouns, sample people or data, its map and phone, its rules reworded), or anything of Planed's. Checked first.
- **Template.** The page's sections are filled in because the kit had them, whether or not the person's product needs them (a map-controls section for a product with no map).
- **Boxed.** A card around everything, cards inside cards, the same bordered treatment on every row.
- **Flat.** Everything at the same weight, so the eye has nowhere to land.
- **Ornamented.** A chip, dot, icon tile, badge or delta on every row, there by habit.
- **Bland.** Clean and correct, but it could be any product: no scene from their product, grey boxes where it should be, generic copy.
- **Made-up.** Data that can't be true: totals that don't add up, the same figure twice, stock names (John Doe, Acme), a chart not drawn to its numbers, people, prices, dates or statuses that contradict the ledger.

Plus **Brief** (an explicit ask from the brief is missing or wrong), **System** (off-token, off-scale, wrong shape language) and **Lint** (measured faults, grouped into one note).

## Judging

Score each page out of 10 for "theirs, human-designed and on-system", then give the set the lowest page score.

| Score | Meaning |
|---|---|
| 10 | You'd assume a strong designer made this system for this product. Nothing to flag. |
| 9 | It ships. A design lead would leave only nits. |
| 8 | It's theirs and it's sound; a designer would spot one or two small tells. |
| 6–7 | Competent, but the kit shows through somewhere, or it reads as generated at a glance. |
| 5 or less | Fieldwork with new colours, or broken: clipped, unreadable, the wrong content. |

**Pass:**
- **Default:** 8 or more on every page in the set, no blocking notes.
- **`--thorough`:** 9 or more on every page, no blocking notes.

**Caps.** A page with a kit leftover (Fieldwork's or Planed's) in its In context scene or its copy scores 6 at most. If you can name a tell a design lead would spot within ten seconds, the page scores 8 at most (so it can pass a default review, never a thorough one). Don't round up.

**Calibrate to their product.** A data-heavy tool should be dense and numbers-first; a consumer brand can carry more personality. "Human" means designed with intent for their users, not minimal.

**Respect the brief.** The brief's shape language, voice and nouns are the person's choices. Don't score them down for taste; score how well the pages carry them out. A page the brief removes is not a gap.

**Be specific.** Every blocking note names its failure mode, the page and location, the evidence, what's wrong and why it reads as the kit's or machine-made, and a concrete fix the builder can make in Paper. "Make it more theirs" is not a note. This is: "Kit's. Select, In context (1x, the scene): still Fieldwork's survey page with the quadrat sort open, relabelled. Fix: rebuild as their order-status filter on the orders list, with the three statuses from the brief."

Check each fix before you suggest it: it's possible in Paper (no skew, no interaction), it doesn't repeat something already on the page, and it fits the units and scales already there.

**Rank by how much of the set it spoils.** Order: the kit's, a missed explicit ask, structure, hierarchy and density, system, polish. At most five blocking notes for the set. Several Lint faults are one note headed "Lint".

## Output

Return exactly this, with nothing before or after it:

```
## Round <N> review: <page names>
Bar: default (8) | thorough (9)
Scores: <Page> <n>/10 · <Page> <n>/10 · …
Verdict: PASS | REDESIGN
Theirs? <per page: theirs, or what of the kit's still shows>
First read: <per page: first → second → third, and whether that matches the page's job>
Biggest difference: <the one biggest gap against the pattern or the passed Button page, and which page>

### Blocking
1. **<Failure mode> · <page>, <location>** (<evidence: screenshot scale and region, or node ID and value>): <what's wrong>. Reads as <the kit's / machine-made> because <why>. Fix: <concrete change>.
(or "None")

### Polish
- **<page>, <location>**: <note>. Fix: <change>.

### System compliance
- <"OK", or each deviation: page, location, what it is, the expected token or value>

### Previous notes
- R<n>.<k>: fixed | partly | not fixed: <one line>

### What's working
- <one to three things to keep>

### Not checked
- <up to five things you couldn't see or measure, and why> (or "Nothing")
```
