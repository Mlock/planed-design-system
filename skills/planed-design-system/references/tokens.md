# Tokens

The kit file carries **98 tokens**: 86 primitives with literal values and 12 semantic aliases that point at primitives with `var(…)`. Their values are Fieldwork's, the kit's sample system: paper and bark with moss, IBM Plex Sans with IBM Plex Mono, 6px corners. Boards use the aliases and a few primitives, so changing a primitive's value restyles every page that uses it.

## First: are the tokens there?

A person may have copied the kit's pages into their own Paper File rather than duplicating it. Copied pages don't bring the tokens with them, and every `var(--…)` on the boards then resolves to nothing.

**check get_tokens first; create any missing tokens with create_tokens (primitives before aliases) before setting values**

1. `get_tokens` on their file.
2. If all 98 names below are there, go straight to "What the moodboard sets".
3. If some or all are missing, create the missing ones with `create_tokens`, using the kit's (Fieldwork's) values from the full list at the end of this file. Send the primitives first and the aliases in a second call: an alias created before its primitive points at nothing. Create only the names that are missing; never create a second token with a name that exists.
4. `get_tokens` again and count 98. Then screenshot one page to confirm the boards render (text visible, sheets white, buttons filled) before you set any value.

## What set_tokens does and doesn't restyle

Measured on the kit's boards:

| On the boards | How it's stored | What restyles it |
|---|---|---|
| Colours (text, fills, borders) | `var(--color-…)`, nearly everywhere | `set_tokens` on the primitive. Every page changes at once. |
| Font families | `var(--font-sans)`, `var(--font-display)`, `var(--font-mono)` | `set_tokens`. Every page changes at once. |
| Radii | `var(--radius-…)`: every on-scale radius (10, 8, 6, 4, 2) is bound to the scale. Round things (status dots, pins, radios, toggle knobs, avatars) carry a literal `999px`, and off-scale values stay literal. | `set_tokens` on the seven `--radius-*` values. Every component reshapes at once. A fallback sweep catches any literal left over (see "Set: the radius scale"). |
| Font sizes, weights, line heights, letter-spacing | literal | Per page, only where the brief calls for it. |
| Spacing, padding, gaps | literal | Per page, only for a density change. |
| Shadows | literal recipes | Per page (see "Shadows" below). |

So colour, type and corners change with the token swap. Type sizes, density and shadows change page by page, and only when the brief calls for it.

## What the moodboard sets

### Set: colour primitives

Map the brief's palette roles onto the primitives by **role**, not by name. The names come from the kit's first system and describe neither Fieldwork's values nor the new ones (a token called `--color-sky` can hold the person's teal, `--color-needs-owner` their amber). That mismatch is expected: keep the names, because renaming breaks the aliases (see "Never rename").

| Primitive(s) | Kit value (Fieldwork) | Role on the boards | Set it to |
|---|---|---|---|
| `--color-canvas` | `#F1EFE7` | The ground under every sheet (`--color-background`) | Their page ground |
| `--color-white` | `#FBFAF5` | Sheets, cards, popovers (`--color-surface`); text on primary (`--color-primary-foreground`, `--color-pin-foreground`) | Their raised surface |
| `--color-surface-muted` | `#EEEBE1` | Selected row, segmented track, soft button fill | A step from surface toward ink |
| `--color-surface-sunken` | `#F5F3EC` | Wells inside a sheet: fields, In context canvases, Do and Don't wells | A step below surface |
| `--color-line` | `#E2DED4` | Hairlines and dividers (`--color-border`) | Their divider colour |
| `--color-canvas-dot` | `#D3CEC1` | Disabled primary fill | Their disabled fill |
| `--color-ash` | `#9A9285` | Placeholders, disabled text, planned dots (`--color-foreground-disabled`) | Their quietest legible grey |
| `--color-slate` | `#6B6255` | Secondary text (`--color-foreground-muted`) | Muted text, ≥ 4.5:1 on surface |
| `--color-ink` | `#3E3428` | Text (`--color-foreground`) | Their ink |
| `--color-ink-hover` | `#415A2F` | Primary hover (a darker moss in the kit, because `--color-primary` points at the accent) | One step darker than their primary (lighter on a dark theme) |
| `--color-link`, `--color-link-line`, `--color-link-tint` | `#4F6B3A`, at 50%, at 12% | The accent: the primary action (`--color-primary`), links, focus rings, selection, progress, map contours | Their interactive accent; keep the 50% (`80` alpha) and 12% (`1F` alpha) steps |
| `--color-pushpin` | `#E0662B` | The attention dot (`--color-pin`): a quadrat not logged yet | Their attention colour |
| `--color-pin-green` | `#4F6B3A` | Logged, success, Do (`--color-success`); equal to the accent in the kit | Their success colour, ≥ 4.5:1 at 12px. It may equal the accent when the board uses one colour for both; then every status also carries a word or shape, never colour alone |
| `--color-needs-owner`, `-tint`, `-text`, `--color-coral` | `#E0662B`, `#FBE6D8`, `#8C3A13`, `#F2B896` | "Needs attention" tags, note cards and lines | Their warning family: base, tint, text on tint, a light line colour |
| `--color-oxblood`, `-hover`, `-tint` | `#A63A26`, `#8A2F1E`, `#F7E5DF` | Errors, sync failed, destructive actions, Don't (`--color-error`) | Their danger family |
| `--color-butter`, `--color-rose`, `--color-sky`, `--color-sage` | `#F6E9AE`, `#F3D4C0`, `#D2DFE2`, `#C9D3B0` | Avatar and tag tints, given in order; sage is also the map's lichen ground | Four categorical tints from the moodboard that ink reads on |

**Dark systems.** If the brief says dark, keep the roles and invert the values: `--color-canvas` becomes the darkest ground, `--color-white` the raised dark sheet, `--color-ink` the light text, `--color-primary-foreground` (which points at `--color-white`) then reads dark on a light primary. Literal `#FBFAF5` in focus rings and shadows doesn't follow; the raw-hex sweep in `lint.md` catches it.

**Contrast.** After the swap, check: ink on surface and on background ≥ 4.5; slate on surface ≥ 4.5; the link colour ≥ 3 for lines, ≥ 4.5 where it's text; error, success and `needs-owner-text` on its tint ≥ 4.5 at 12px; ink on each of the four tints ≥ 4.5 at 11px. Fix the primitive, not the page.

### Set: font families

`--font-sans`, `--font-display` and `--font-mono`, to the type pair from the brief, written as a quoted family name (`"Inter"`). Confirm each family with `get_font_family_info` first; a name that doesn't resolve falls back to the system sans with no error. `--font-display` sets every H1 and the large type; `--font-sans` everything else; `--font-mono` addresses and code. If the person's system has no display face, set display and sans to the same family.

Also check weights: the boards use 400, 500 and 600. If the family lacks 500 or 600, set `--font-weight-medium` or `--font-weight-semibold` to the nearest weight it has, and note that the boards' literal weights still need the same change per page.

**Check that each family renders.** `get_font_family_info` finding a family doesn't prove Paper draws it. After `set_tokens`, screenshot a line in each family at 2x (the Typography page has all three) and compare telling glyphs with the family's own: `g`, `a`, `0`, `1`. Mono faces fall back most often: in one dry run IBM Plex Mono resolved by name but drew as a generic monospace (in another it drew correctly, which is what the kit now uses). If a family falls back, pick another confirmed family with the same skeleton, check again, and say in the brief which one you swapped.

### Set: the radius scale

The boards' radii are bound to these tokens, so setting the values reshapes every page at once: buttons, sheets, fields, popovers, avatars. Pick one column from the brief's shape language (or your own values between them), keep the order of the scale from `--radius-none` to `--radius-xl` (each step at least as large as the one before), and set all seven in one `set_tokens` call. `--radius-full` sits outside that order: it's the button, tag and pill radius, so in a square or soft-rectangle system it can be smaller than `--radius-xl` (the kit's 6 under 10, and the Square column's 4 under 8, are deliberate). Round things keep their circle with a literal `999px` ("Round things").

| Token | Kit value (Fieldwork) | Role on the boards | Square system | Soft system |
|---|---|---|---|---|
| `--radius-none` | 0 | Phone sheets' bottom edge | 0 | 0 |
| `--radius-xs` | 2 | Checkbox, inline keys, small marks | 0 | 6 |
| `--radius-sm` | 4 | Tooltip, key chips | 2 | 10 |
| `--radius-md` | 6 | Fields, wells, list rows, In context canvases, Do and Don't wells | 4 | 16 |
| `--radius-lg` | 8 | Section sheets, panels, drawers, cards | 6 | 24 |
| `--radius-xl` | 10 | Popovers, menus, modals, phone sheets' top | 8 | 32 |
| `--radius-full` | 6 | Buttons, tags, pills, tracks (soft rectangles in the kit; round things are literal `999px`, see "Round things") | 4 (buttons go square-ish) | 999 |

- **Pill buttons, square everything else** (a common mix): set `--radius-full` to 999 and the rest from the square column. Round things stay round either way.
- **Nested corners:** where a shape sits close inside another (a thumbnail 8 inside a card, a button 4 inside a well), the outer radius should equal the inner radius plus the gap between them. Check those spots after the swap; a soft scale pinches them most often.
- After `set_tokens`, screenshot Button, Card and Popover to confirm the shapes moved.

**Fallback sweep, if the file isn't prepared.** A file whose boards still carry literal radii (nodes added later, or a copy edited by hand) won't reshape. On each page, run `find_nodes` scoped to the artboard with `filters: [{styleName: "borderRadius", styleValue: "<value>"}]` for each kit value in the table (`10px`, `8px`, `6px`, `4px`, `2px`), and `update_styles` each match to its token (`10px` → `var(--radius-xl)`, `8px` → `var(--radius-lg)`, `4px` → `var(--radius-sm)`, `2px` → `var(--radius-xs)`). `6px` is both `--radius-md` and `--radius-full` in the kit: read the node, then bind buttons, tags and pills to `var(--radius-full)` and fields, rows, wells and canvases to `var(--radius-md)`. Leave scenes you are about to rebuild, off-scale values and the literal `999px` on round things alone.

#### Round things

If round things shared `--radius-full` with buttons, a square system that sets it to 2 or 4 would square radios, status dots, toggle knobs and avatars along with the buttons. In a dry run with every radius at 2, radios became indistinguishable from checkboxes. The kit's `--radius-full` is 6, so its round things already carry a literal `999px`. The rule:

- **Radios, status dots and toggle knobs stay round, always.** Their shape is their meaning.
- **Avatars stay round** unless the moodboard shows square avatars.
- **How:** keep the kit's literal `999px` on those nodes, and give anything round you draw a literal `999px` too (Avatar, Badge and tag, Toggle, Radio, Map pins, and any page whose matrix or scene shows a dot, a radio or an avatar). If the moodboard shows square avatars, set those to a token. Say in the brief what stays round. These literal `999px` radii are the one allowed exception to the Mixed radii lint line (`lint.md`).
- **Deliberately off-system shapes** in a Don't (a round checkbox, a pill button in a square system) also take a literal radius; that's the point of the example.

### Leave unless the brief calls for it

- **Type scale** (`--text-*`, `--leading-*`): 11 sizes from 11 to 72. Change only for a clearly larger or smaller reading size, and then change the boards too.
- **Tracking** (`--tracking-*`): the kit's display tracking is `-0.01em`, set for IBM Plex Sans. A tight grotesque often wants `-0.02em` to `-0.03em`; a serif or wide face `-0.01em` to `0`. The brief names the display value (`moodboard-reading.md`, "Type pair"); set `--tracking-display` to it in step 3. The boards' H1s carry the kit's `-0.01em` as a literal, not the token, so the token alone changes nothing on the pages: each page's H1 gets the brief's value as part of its header (SKILL.md step 4, "Header"; `page-pattern.md`, "The header").
- **Weights** (see above), **opacity** (`--opacity-hidden` 40%, `--opacity-behind-sheet` 64%), **spacing** (`--spacing-2` … `--spacing-128`), **containers** and **breakpoints**.

### Never change

- **The 12 semantic aliases.** `--color-background`, `--color-surface`, `--color-foreground`, `--color-foreground-muted`, `--color-foreground-disabled`, `--color-border`, `--color-primary`, `--color-primary-foreground`, `--color-pin`, `--color-pin-foreground`, `--color-success`, `--color-error` keep pointing at the same primitives. They are why one swap restyles every page. If a role genuinely needs a different primitive, repoint that one alias with `set_tokens`, say so in the brief, and screenshot a page that uses it. In the kit `--color-primary` already points at `var(--color-link)`, so the one primary action is the accent (Fieldwork's moss); if their primary is their ink, point it at `var(--color-ink)`. Repointing `--color-primary` also moves its hover: set `--color-ink-hover` to a darker step of the new primary.
- **Token names.** Don't rename (next section). The primitive names come from the kit's first system (`--color-needs-owner`, `--color-pushpin`, `--color-oxblood`, `--color-sky`) and already don't describe Fieldwork's values (`--color-pushpin` holds signal orange, `--color-white` holds paper); after the swap they'll hold theirs. That mismatch is expected. Leave the names as they are, because renaming a primitive breaks the aliases that point at it (the alias-rename quirk below).

## Shadows

Shadows are literal values on the boards, not tokens. The kit's are Fieldwork's: flat sheets on bark-tinted hairlines, three named recipes, a hairline and no lift on buttons:

| Recipe | Value | Used for |
|---|---|---|
| **Float** | `#3E342814 0 0 0 1px, #3E34280A 0 1px 2px` | Section sheets, panels, drawers, cards |
| **Lifted** | `#3E34281A 0 0 0 1px, #3E342814 0 8px 24px` | Menus, popovers, modals, phone sheets: anything that opens over a sheet |
| **Window** | `#3E342814 0 0 0 1px, #3E34280F 0 8px 24px` | A product window or phone sitting on an In context canvas |
| Hairline | `#3E342817 0 0 0 1px` | Secondary buttons, map buttons and controls inside a sheet |
| Ink lift | none | The kit's primary buttons and pins carry no shadow (pins keep a 2px `var(--color-white)` ring) |

Plus the focus ring, `#FBFAF5 0 0 0 2px, var(--color-link) 0 0 0 4px`, which is a shadow too. Its first part is Fieldwork's paper as a literal: set it to their surface (`var(--color-surface)` works inside a shadow) in the sweep.

**When to raise.** If the brief's shape language is raised (soft cards, buttons that lift), deepen the recipes in the sweep, for example Float `#00000010 0 0 0 1px, #0000000A 0 1px 2px, #0000000F 0 12px 32px`, Lifted `#00000010 0 0 0 1px, #0000000A 0 2px 4px, #0000001A 0 24px 56px`, and add an Ink lift (`#00000026 0 1px 2px, #00000014 0 8px 24px`) to the primary button and pins as each page is rebuilt. Keep exactly one step between "sits on the page" and "opens over it", or popovers stop reading as on top. If the brief is flat, keep the kit's recipes and re-tint them: swap the bark `#3E3428` for their ink at the same alphas. If their ground is dark, black shadows vanish: use the ring (in a light alpha of their ink) and lower the drop.

**The sweep** (SKILL.md step 3). One `find_nodes` per recipe across the whole file (no `pageId`), `filters: [{styleName: "boxShadow", styleValue: …}]`, using the colour-qualified queries so recipes that share offsets don't match each other: Float `*#3E34280A 0px 1px 2px*`, Lifted `*#3E342814 0px 8px 24px*`, Window `*#3E34280F 0px 8px 24px*`, hairline `*#3E342817 0px 0px 0px 1px*`, focus ring `*#FBFAF5 0px 0px 0px 2px*`. Leave every match on Start here alone: the preview board's chrome keeps Planed's literal shadows, and its Button clone is replaced in step 7. `update_styles` the rest.

- **Repeat each query until only Start here matches.** `find_nodes` cuts a large result short without saying so: in a dry run the first whole-file Float query returned about 180 of about 310 nodes, and builders found section sheets still floating on page after page. After each round of updates, run the same query again; stop when every match left is on Start here.
- **New values can match old queries.** If your new recipe keeps a query's colour and offset (you kept the kit's drop and only changed the ring), skip any match already holding your new value.
- **Combined values.** Rings and recipes sit together in longer shadows: a selected pin, a focused button (focus ring plus hairline). Read each match's full value, change only the part the recipe owns, and write the whole value back.
- **Results are long.** A whole-file query can return tens of thousands of characters. Hand the sweep to one subagent if your agent can spawn one, and ask it for the counts, not the node lists.

A node you add later (a rebuilt scene, a new card) takes the settled recipe from the start. Write the new recipes into the Layout page's Shadows section too, so the system documents itself, named in their words (the kit calls its product-window recipe "Window").

## Never rename: the alias-rename quirk

Renaming a primitive with `set_tokens` (`newName`) breaks the aliases that point at it **in rendering**: after `--color-slate` is renamed, `--color-foreground-muted: var(--color-slate)` can render blank or white even though its value still reads correctly, and every muted line on every page disappears. Re-setting the same alias does nothing.

So keep the kit's names and change only values. If a name must change (the person insists their tokens match their code), fix each affected alias by setting it to a literal value once, then back to its `var(…)`, and screenshot an old page to confirm muted text, borders and fills are visible again.

## After the swap

Screenshot three pages to confirm: Color (every primitive and role), Button (primary, secondary, destructive, focus), and one page with an In context scene. Look for invisible text, white-on-white sheets, a fallback font and a primary that no longer reads as the one action.

## The full list

All 98 tokens with the kit's (Fieldwork's) values, in creation order: primitives first, then the semantic aliases. Each block is a ready `tokens` array for `create_tokens`. Use them only to create names that are missing, then set the moodboard's values with `set_tokens`. The values match `get_tokens` on the kit file `01M893XQADCXH6Y0W6JCJZJK2E`.

**Call 1 · primitives (86 tokens).**

```json
[
  {"type": "color", "name": "--color-white", "value": "#FBFAF5"},
  {"type": "color", "name": "--color-canvas", "value": "#F1EFE7"},
  {"type": "color", "name": "--color-line", "value": "#E2DED4"},
  {"type": "color", "name": "--color-ash", "value": "#9A9285"},
  {"type": "color", "name": "--color-slate", "value": "#6B6255"},
  {"type": "color", "name": "--color-ink", "value": "#3E3428"},
  {"type": "color", "name": "--color-ink-hover", "value": "#415A2F"},
  {"type": "color", "name": "--color-surface-muted", "value": "#EEEBE1"},
  {"type": "color", "name": "--color-surface-sunken", "value": "#F5F3EC"},
  {"type": "color", "name": "--color-canvas-dot", "value": "#D3CEC1"},
  {"type": "color", "name": "--color-link", "value": "#4F6B3A"},
  {"type": "color", "name": "--color-link-tint", "value": "#4F6B3A1F"},
  {"type": "color", "name": "--color-link-line", "value": "#4F6B3A80"},
  {"type": "color", "name": "--color-pushpin", "value": "#E0662B"},
  {"type": "color", "name": "--color-pin-green", "value": "#4F6B3A"},
  {"type": "color", "name": "--color-needs-owner", "value": "#E0662B"},
  {"type": "color", "name": "--color-needs-owner-tint", "value": "#FBE6D8"},
  {"type": "color", "name": "--color-needs-owner-text", "value": "#8C3A13"},
  {"type": "color", "name": "--color-coral", "value": "#F2B896"},
  {"type": "color", "name": "--color-oxblood", "value": "#A63A26"},
  {"type": "color", "name": "--color-oxblood-tint", "value": "#F7E5DF"},
  {"type": "color", "name": "--color-oxblood-hover", "value": "#8A2F1E"},
  {"type": "color", "name": "--color-butter", "value": "#F6E9AE"},
  {"type": "color", "name": "--color-rose", "value": "#F3D4C0"},
  {"type": "color", "name": "--color-sky", "value": "#D2DFE2"},
  {"type": "color", "name": "--color-sage", "value": "#C9D3B0"},
  {"type": "fontFamily", "name": "--font-display", "value": "\"IBM Plex Sans\""},
  {"type": "fontFamily", "name": "--font-sans", "value": "\"IBM Plex Sans\""},
  {"type": "fontFamily", "name": "--font-mono", "value": "\"IBM Plex Mono\""},
  {"type": "fontSize", "name": "--text-micro", "value": "11px"},
  {"type": "fontSize", "name": "--text-detail", "value": "12px"},
  {"type": "fontSize", "name": "--text-caption", "value": "13px"},
  {"type": "fontSize", "name": "--text-body-sm", "value": "14px"},
  {"type": "fontSize", "name": "--text-body", "value": "16px"},
  {"type": "fontSize", "name": "--text-title", "value": "18px"},
  {"type": "fontSize", "name": "--text-h3", "value": "24px"},
  {"type": "fontSize", "name": "--text-h2", "value": "32px"},
  {"type": "fontSize", "name": "--text-lead", "value": "36px"},
  {"type": "fontSize", "name": "--text-h1", "value": "48px"},
  {"type": "fontSize", "name": "--text-display", "value": "72px"},
  {"type": "fontWeight", "name": "--font-weight-regular", "value": 400},
  {"type": "fontWeight", "name": "--font-weight-medium", "value": 500},
  {"type": "fontWeight", "name": "--font-weight-semibold", "value": 600},
  {"type": "letterSpacing", "name": "--tracking-display", "value": "-0.01em"},
  {"type": "letterSpacing", "name": "--tracking-tight", "value": "-0.015em"},
  {"type": "letterSpacing", "name": "--tracking-normal", "value": "0em"},
  {"type": "letterSpacing", "name": "--tracking-wide", "value": "0.06em"},
  {"type": "lineHeight", "name": "--leading-micro", "value": "14px"},
  {"type": "lineHeight", "name": "--leading-detail", "value": "16px"},
  {"type": "lineHeight", "name": "--leading-caption", "value": "18px"},
  {"type": "lineHeight", "name": "--leading-body-sm", "value": "21px"},
  {"type": "lineHeight", "name": "--leading-body", "value": "24px"},
  {"type": "lineHeight", "name": "--leading-title", "value": "24px"},
  {"type": "lineHeight", "name": "--leading-h3", "value": "30px"},
  {"type": "lineHeight", "name": "--leading-h2", "value": "36px"},
  {"type": "lineHeight", "name": "--leading-lead", "value": "42px"},
  {"type": "lineHeight", "name": "--leading-h1", "value": "52px"},
  {"type": "lineHeight", "name": "--leading-display", "value": "76px"},
  {"type": "opacity", "name": "--opacity-hidden", "value": "40%"},
  {"type": "opacity", "name": "--opacity-behind-sheet", "value": "64%"},
  {"type": "breakpoint", "name": "--breakpoint-mobile", "value": "390px"},
  {"type": "breakpoint", "name": "--breakpoint-tablet", "value": "768px"},
  {"type": "breakpoint", "name": "--breakpoint-desktop", "value": "1440px"},
  {"type": "container", "name": "--container-drawer", "value": "360px"},
  {"type": "container", "name": "--container-content", "value": "1120px"},
  {"type": "container", "name": "--container-max", "value": "1344px"},
  {"type": "spacing", "name": "--spacing-2", "value": "2px"},
  {"type": "spacing", "name": "--spacing-4", "value": "4px"},
  {"type": "spacing", "name": "--spacing-8", "value": "8px"},
  {"type": "spacing", "name": "--spacing-12", "value": "12px"},
  {"type": "spacing", "name": "--spacing-16", "value": "16px"},
  {"type": "spacing", "name": "--spacing-20", "value": "20px"},
  {"type": "spacing", "name": "--spacing-24", "value": "24px"},
  {"type": "spacing", "name": "--spacing-32", "value": "32px"},
  {"type": "spacing", "name": "--spacing-40", "value": "40px"},
  {"type": "spacing", "name": "--spacing-48", "value": "48px"},
  {"type": "spacing", "name": "--spacing-64", "value": "64px"},
  {"type": "spacing", "name": "--spacing-96", "value": "96px"},
  {"type": "spacing", "name": "--spacing-128", "value": "128px"},
  {"type": "radius", "name": "--radius-none", "value": "0px"},
  {"type": "radius", "name": "--radius-xs", "value": "2px"},
  {"type": "radius", "name": "--radius-sm", "value": "4px"},
  {"type": "radius", "name": "--radius-md", "value": "6px"},
  {"type": "radius", "name": "--radius-lg", "value": "8px"},
  {"type": "radius", "name": "--radius-xl", "value": "10px"},
  {"type": "radius", "name": "--radius-full", "value": "6px"}
]
```

**Call 2 · semantic aliases (12 tokens).** Only after call 1 has succeeded, because each one points at a primitive.

```json
[
  {"type": "color", "name": "--color-background", "value": "var(--color-canvas)"},
  {"type": "color", "name": "--color-surface", "value": "var(--color-white)"},
  {"type": "color", "name": "--color-foreground", "value": "var(--color-ink)"},
  {"type": "color", "name": "--color-foreground-muted", "value": "var(--color-slate)"},
  {"type": "color", "name": "--color-foreground-disabled", "value": "var(--color-ash)"},
  {"type": "color", "name": "--color-border", "value": "var(--color-line)"},
  {"type": "color", "name": "--color-primary", "value": "var(--color-link)"},
  {"type": "color", "name": "--color-primary-foreground", "value": "var(--color-white)"},
  {"type": "color", "name": "--color-pin", "value": "var(--color-pushpin)"},
  {"type": "color", "name": "--color-pin-foreground", "value": "var(--color-white)"},
  {"type": "color", "name": "--color-success", "value": "var(--color-pin-green)"},
  {"type": "color", "name": "--color-error", "value": "var(--color-oxblood)"}
]
```
