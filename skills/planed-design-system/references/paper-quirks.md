# Paper quirks

Paper behaviours that quietly break a page or make it look generic. Read this once before you touch the first page.

## Tokens and the kit file

- **Copied pages don't bring tokens.** If the person copied the kit's pages into their own Paper File instead of duplicating it, every `var(--…)` resolves to nothing: text can vanish and sheets go transparent. Check `get_tokens` before anything else (`tokens.md`, "First: are the tokens there?").
- **Only colours, font families and radii are token-bound on the boards.** Sizes, gaps, weights and shadows are literal pixels. `set_tokens` restyles colour, type and corners everywhere at once; density and depth change page by page. A literal radius left on a board (in an unprepared copy, or written by hand) won't follow the scale: use the fallback sweep in `tokens.md`.
- **Renaming a token breaks aliases to it in rendering.** After `set_tokens` renames a primitive (say `--color-slate` to `--color-mist`), tokens aliased to it (`--color-foreground-muted: var(--color-slate)`) can render blank or white even though their value reads correctly. Re-setting the same alias does nothing. Set the alias to a literal value once, then back to the `var(...)`, and screenshot an old page to confirm muted text is visible again. Better: don't rename.
- **`var()` inside gradients doesn't resolve.** A `radial-gradient(... var(--color-canvas-dot) ...) var(--color-canvas)` background renders empty. Write gradients and dot grids with literal values from the person's palette, for example `radial-gradient(circle, #D6D6D2 1.1px, transparent 1.3px) 0 0 / 24px 24px #EDEDEB`, and update them by hand when the palette changes.
- **Token-heavy calls.** `get_basic_info` returns the full token list on every call. Call `get_tokens` only when you need tokens it didn't show, and prefer `get_children` of the page root for positions after the first call. `get_font_family_info` can return dozens of styles for one family; call it once per family.
- **Read pages with `get_tree_summary`.** It gives each node's ID, name and a short text preview, which is all a rewrite needs to find its text and sections. `get_jsx` of one section can run to 10k tokens; use it only for the section whose exact styles you need. Every `write_html` also echoes the IDs it created, so write one group at a time and don't re-read what you just wrote.
- **`find_nodes` cuts large results short, silently.** A whole-file query with hundreds of matches returns only part of them, with no warning (a Float shadow sweep found about 180 of about 310). After updating what it found, run the same query again until it returns only what should match. Scope to an artboard whenever you can.

## Type

- **Fonts.** A family name that doesn't resolve falls back to the system sans without any error. Use the font tokens, or confirm the exact family with `get_font_family_info`. Even a confirmed family can draw as a generic face (mono most often), so check a 2x screenshot after setting it (`tokens.md`, "Check that each family renders").
- **Tabular figures work.** `fontVariantNumeric: "tabular-nums"` in `update_styles` (or `font-variant-numeric: tabular-nums` in `write_html`) turns on tabular numerals, so amounts in a column line up. Set it on number columns and totals.
- **Text doesn't inherit `font-family`.** Setting `font-family` on an artboard or frame does nothing for the Text nodes inside it; any text without its own family renders in Inter. Put `font-family: var(--font-sans)` (or `--font-display` for headings) on every text element you write, then check with the font sweep in `lint.md`.
- **Off-scale values.** Text sizes and weights outside the system's scale, and colours that nearly match a palette colour but don't. Measure; don't eyeball.
- **Right-aligned text.** `text-align: right` is turned into flex end and breaks text trim, so right-aligned labels sit about 6px low. Right-align the column with `align-items: flex-end` and give the text `width: max-content`. `overflow: hidden` on a text node breaks trim the same way. For number columns in tables, build every cell as a fixed-width slot with `justify-content: flex-end` from the first write; retrofitting it later means replacing each text node.
- **`white-space: pre` text won't shrink.** A caption with `white-space: pre` keeps its full width and pushes its row wider even with `min-width: 0`. Use `nowrap` with `min-width: 0` on the parent, or shorten the copy.
- **`write_html` wraps padded text.** Text with its own padding is wrapped in an extra frame, which can make sibling columns unequal. Put padding on the parent frame instead.

## Layout

- **Clipping.** A fixed artboard height cuts off content. Every page is `height: fit-content`; keep it that way after edits.
- **`margin` is dropped.** Margins (including `margin-top: auto`) are silently ignored. Use `gap`, padding, or a spacer frame.
- **Negative `gap` is ignored.** Overlapping avatars can't use `gap: -6px` or negative margin. Space them with a 2px gap and a `0 0 0 2px` ring in the surface colour, or position them absolutely.
- **Skew is dropped.** Only `rotate` survives in `transform`, so a skewed shape silently renders flat. Draw angled shapes with rotation, or with an SVG. Scale transforms aren't reliable either: show a big board at 1x inside a clipped frame instead of shrinking it.
- **`position: absolute` sticks on text.** `update_styles` can't clear it on a text node, and replacing the text node may not restore the layout. Delete the block and duplicate the canonical node again.
- **Flex shorthands stick.** A node moved or cloned into a new row can keep its old `flex: 1`, and `update_styles` sometimes can't clear it. If it won't take, replace the node.
- **Zero padding on clones.** `update_styles` sometimes ignores padding shorthands set to `0` on cloned nodes. Set each side separately and confirm with `get_computed_styles`. If it still won't take, rebuild that frame.
- **Heights on inactive pages.** On a page the user isn't viewing, a fit-content board's width, height and position read as `null`. Screenshot it, or export it as a PNG, if you need to measure it.

## Cloning and copying

- **Clone sizes.** A cloned component keeps its specimen size. Check the clone against its slot; pick the smaller variant or rebuild.
- **Specimen frame styling on page-level clones.** Headers and footers cloned from a page often carry the specimen's radius, border or narrow side padding. Strip those and set the page margin.
- **Clones keep absolute positioning and `translate`.** Cloning a floating bar (left `50%`, `translate: -50%`) into a flex row keeps both, so it lands on top of its neighbours. Set `position: relative`, `left`/`top: 0` and `translate: 0` on the clone.
- **Big clones return big results.** A full-artboard `x-paper-clone` returns 60–90k characters of new node IDs. Don't read them; find the clone's root afterwards with `get_children` of its parent.
- **`x-paper-clone` stays in one file.** It can't reach another file. Rebuild from that file's `get_jsx` on this file's tokens instead.
- **Images from another file.** Image fills can cross files. On the source board, run `find_nodes` with `filters: [{styleName: "backgroundImage", styleValue: "*file-assets*"}]`, then reuse the returned `url(...)` as a `background-image`. A `backgroundImage` filter with no value matches every node with a background colour, so always give the value.
- **Copying boards between pages.** `duplicate_nodes` with `parentId: "root_node_<pageId>"` copies a board to another page in the same file. Move it with `update_styles` afterwards.
- **Duplicates land right after their source.** Duplicating a row twice from the same source puts the second copy before the first. Duplicate the newest copy instead, or check the order with `get_children`.

## Artboards and pages

- **`create_artboard` ignores `top` and `left`.** Move the artboard with `update_styles` after creating it, and check its position with `get_basic_info`.
- **Lists stop at 100 artboards.** `get_basic_info` and `get_children` list at most 100 artboards per page. On a bigger page, find boards by text with `find_nodes`.
- **Screenshot scale.** `get_screenshot` caps images to fit size limits, so a tall page comes back small whatever scale you ask for, and scales below 1 aren't reliably honoured. Use a full-page screenshot as a thumbnail of the overall shape, and `get_children` plus 1x or 2x screenshots of sections to read anything.
- **Release only your own boards.** `finish_working_on_nodes` with no arguments releases every agent's working indicators, including running subagents'. Pass your artboard IDs.
- **Exports.** Exports always land in ~/Downloads, whatever you ask. Use the path the export tool returns (Paper appends "(1)" when the name exists), then move the file where it belongs.
- **File size.** Paper sometimes adds "Your file is too large" to calls that aren't about your file; it seems to come from whichever file is open in the app. Check with `get_basic_info` on the person's fileId. If that call returns the warning, stop writing to the file and tell the person, because further edits risk data loss. Either way, mention the warning at the end of the run.
