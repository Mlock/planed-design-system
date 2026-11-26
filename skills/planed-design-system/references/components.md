# Pages

One entry per Foundations page (7) and Components page (37) in the kit file `01M893XQADCXH6Y0W6JCJZJK2E`, in page-list order. The kit is a sample system for a made-up product, **Fieldwork**: a survey and field-notes app for ecologists, with an office app (a survey page with a map and a quadrat list) and a field app on a phone. Every page documents Fieldwork. Page IDs are the kit's; in the person's copy they may differ, so match by page name with `get_basic_info` and use their IDs.

Each entry gives:
- **page / board:** the kit's page ID and its main artboard
- **core:** `true` if the page is in the core set a first run does (all 7 Foundations plus 15 components); `false` pages wait for the person's "do the rest" run (see SKILL.md)
- **documents:** what the page shows, section by section, and the states it covers
- **swap:** the Fieldwork-specific parts to replace with the person's
- **remove:** whether the page can be deleted when their product doesn't need it

Every page follows `page-pattern.md`. On every page, also swap the lead, including its last sentence, the status (`In the product <Fieldwork's places>.` → their places, or `Not built yet.`; `page-pattern.md`, "The header"). The kit's pages have no file line or status dot above the title; don't add one.

## Fieldwork's sample data, everywhere

These names and figures recur across the pages. They are the sample's, and none may survive in the person's system. Search for each with `find_nodes` (`textValue: "*<string>*"`) scoped to the page's artboard after you rewrite it (`lint.md`, "Kit leftovers").

| Kind | Fieldwork's | Replace with |
|---|---|---|
| Product and brand | Fieldwork, the lower-case "fieldwork" wordmark and its pin mark (a map pin with a down arrow) | The person's product name, logo (or name set as text) |
| Teams and places | Avon Ecology Trust (the team), Severn Vale Wildlife Group (a second team, Empty state only), Coombe Wood (the site, 51.4816 N, 2.5879 W) | Their customers, accounts or workspaces |
| People | Imogen Pryce (survey lead), Amara Okonkwo and Ruth Hale (observers), Leah Marsh (data manager), Tomasz Nowak (volunteer), Owen Bryant (Empty state); initials IP, AO, RH, LM, TN, OB | Believable names for the person's users and team, in their market |
| Objects | Surveys S-0412 · Transect 4, north slope (In the field, 8 of 12 logged), S-0409 · Transect 2, stream bank (Submitted), S-0405 · Transect 1, meadow edge (Checked), S-0415 · Transect 5, south ridge (Planned); quadrats Q-01 to Q-12 with their names (Bank foot, Hedge margin, Holly gap, Bluebell slope, Coppice stools, Wet flush, Ride edge, Oak edge, Bracken bank, Badger path, Scree) and S-0415's (Ridge gate … Wall foot); species records in italic Latin (*Primula vulgaris*, *Hyacinthoides non-scripta*, *Anemone nemorosa*, *Quercus robur*, *Hedera helix*, *Ficaria verna*) with cover % and counts | The person's own objects (orders, bookings, projects, invoices…) and their parts |
| Figures and times | Thursday 23 April 2026, spring visit 2026; times 08:20 to 10:52 (Q-07's note at 10:46, the office scenes at 10:47, sync failed 10:52); 31 records (29 on the server, 2 on Ruth's phone), 161 records, 312 MB offline map, Team plan 8 seats with 5 used, £12 a seat, Free £0, Organisation £10 | Figures that make sense in their product and add up |
| Nouns | survey, transect, quadrat, visit, record, species, observer, lead, note, site, log, sync, revisit, cover | The nouns from the brief |
| Planed's words, in case any remain | Planed, `planed.cc` | Nothing: the kit's pages shouldn't hold any |

Some Fieldwork-only ideas run through many pages: the office and field split (a survey page in the office, a phone in the field), offline logging and "sync failed", the survey map with contours, pins and a dashed transect line, cover and counts per species, Latin names in italics, one moss action per surface. When a section exists only to show one of these, rebuild it around the closest idea in the person's product, or cut the section and say so.

## Foundations

### Color
- **page / board:** `p-2-0` / `BIK-0`
- **core:** true
- **documents:** Primitives (the neutral ramp and the signal families: moss, signal orange, rust, the warning family, with names and hex). Semantic roles (a table of the roles: swatch, value, what it means). Team tints (butter, rose, sky, sage given to people in the order they joined). Contrast (WCAG ratios for each text pair, with a specimen). On Transect 4 (In context: the survey page and the phone, showing where the few strong colours go). Usage.
- **swap:** every swatch label and hex to the new values (swatches are token fills and recolour on their own; the hex captions are text and don't). Rewrite the role meanings for their product. Recompute every contrast ratio from the new values. Replace "Team tints" with what their four tints mean (avatars, tags, chart series). Rebuild the In context section.
- **remove:** no

### Typography
- **page / board:** `p-3-0` / `ESR-0`
- **core:** true
- **documents:** Scale (11 rows display → micro, each with size/leading/weight/tracking and a line of Fieldwork copy at that size). Mono (IBM Plex Mono for quadrat and survey IDs, times, coordinates and figures). On the survey page (full-bleed: the office window with Q-03 selected). Usage (species names in italic; mono only for IDs and figures).
- **swap:** family names in the header, lead and mono section. Every specimen line to copy from their product at that size. The spec notes (`48/52 · 600 · -0.01em`) if the brief changed sizes or tracking. The mono section to what their product sets in mono, or cut it. Rebuild the scene. Usage examples in their nouns; drop the italic-species rule unless they have one like it.
- **remove:** no

### Layout
- **page / board:** `p-4-0` / `G6N-0`
- **core:** true
- **documents:** The Fieldwork window (the office app at 1440: sidebar 232, survey page with map and quadrat list, quadrat drawer 360; and the phone at 390: the canonical drawings every other scene duplicates). Widths (sidebar, drawer, popover, menu, modal, content, max). Spacing (the 2–128 scale drawn to size with uses). Radius (none → xl and full, each with uses). Shadows (Float, Lifted, Window and the hairline, drawn and written out). Breakpoints (390/768/1440 and the phone). Usage.
- **swap:** rebuild "The Fieldwork window" as their product's main layout: it becomes the canonical shell their later scenes duplicate. Widths to their layout's real widths. Radius specimens and values to the new scale. The Shadows table to the recipes the brief kept, raised or flattened (write the literal values). Breakpoints to theirs if known. Usage pairs about their layout rules.
- **remove:** no

### Motion
- **page / board:** `p-16-0` / `JJ4-0`
- **core:** true
- **documents:** Between views (how one view replaces another in the field app and on a survey page, with A/B diagrams). Speeds and curves (150/250/400 ms; the curves drawn). Interface motion (drawer, sheet, popover, toast, tooltip, toggle, press: motion, time, curve). On Ruth's phone (the quadrat sheet rising over the map). Reduced motion. Usage.
- **swap:** keep the speeds-and-curves and the interface-motion table, retitled for their product, with their components. Rewrite "Between views" for their screen-to-screen or state-change motion, or cut it. Rebuild the scene. Reduced-motion rules stay, in their words.
- **remove:** no (Foundations stay; it may shrink to two or three sections)

### Icons
- **page / board:** `p-5-0` / `NVD-0`
- **core:** true
- **documents:** The set (every icon at 1x and 2x with its name and use: the sidebar's Today, Surveys, Sites, Species, Records, Team; the phone bar's Map, Quadrats, Log, Notes; actions such as flag, note, export, layers, fit to transect). Anatomy and sizes (16px grid, 1.5 stroke; 20 on the phone bar). In context (the office sidebar beside the phone). Usage.
- **swap:** the icon set to the style the brief implies (keep the 16 grid and stroke rules if they fit; a filled or heavier set changes the anatomy notes). Drop Fieldwork-only glyphs (transect, quadrat, species, layers, fit to transect) and add the ones their product needs. Their logo is specced once, on Brand and imagery; if Icons needs to mention it, one line pointing there. Rebuild the scene as their nav.
- **remove:** no

### Brand and imagery
- **page / board:** `p-6-0` / `QBO-0`
- **core:** true
- **documents:** Mark and wordmark (the pin mark and lower-case "fieldwork" at sizes, the app tile, clear space, where it appears). The survey is the imagery (no photographs: the map, the transect and the records are the pictures). Paper and lichen (the grounds, and the map art: the woodland-tint image on the lichen ground, then moss contours). In the office app (full-bleed office scene). Usage.
- **swap:** all of it is Fieldwork's brand. Their logo or name set in their display face ("Mark and wordmark" is the only page that specs the mark: sizes, clear space, where it appears; Icons points here); their imagery rules from the moodboard (photo, illustration, product shots, texture); their ground; a scene in their voice. Keep the Usage format with their own Do and Don't.
- **remove:** no

### Voice and copy
- **page / board:** `p-7-0` / `T9F-0`
- **core:** true
- **documents:** Vocabulary (Fieldwork's words: Say / Meaning / Never: survey, transect, quadrat, visit, record, observer, lead, note, site, log, submit, check, sync). Buttons and names (verbs on buttons, IDs and names, say what changed). Numbers (counts, cover, times, IDs, coordinates: Write vs Not). Empty and wrong (empty-state and error strings). When sync fails (a four-part error card). Usage.
- **swap:** the vocabulary to the brief's nouns (their words, what each means, the synonyms they avoid). Every example string to their product. Numbers rows to the kinds of number their product shows. Empty and error examples from their product; "When sync fails" to the failure their users meet most. Keep the structure; it is the most reusable page in the kit.
- **remove:** no

## Components

### Accordion
- **page / board:** `p-8-0` / `P8N-0`
- **core:** false
- **documents:** Variants and states (a transect row and a help question; closed and open). On the Sites page (full-bleed: Coombe Wood's transects as folds, S-0412 open on its quadrat grid). In help (FAQ folds about offline logging and sync). Usage.
- **swap:** row kinds to the folds their product has (settings groups, FAQ, filters). Rebuild the full-bleed scene from their product. FAQ questions and answers about their product.
- **remove:** yes, if nothing in their product folds

### Avatar
- **page / board:** `p-9-0` / `RZJ-0`
- **core:** true
- **documents:** Tints and sizes (the five people at 20/24/28, each in their team tint, initials 11/600). Stacks and bylines (the observers' stack on a survey header, a record's byline, the account row). On the team page (the Team page inside the office shell). Usage.
- **swap:** every name and initial. The tint rule to theirs (by role, by team, by hash). Sizes to their product's. Rebuild the scene as a place their product shows people (team list, assignee, comments).
- **remove:** no (core)

### Badge and tag
- **page / board:** `p-A-0` / `NVE-0`
- **core:** true
- **documents:** Survey statuses (Planned, In the field, Submitted, Checked, Sync failed: each tone with its meaning). Quadrat dots and counts (logged, not logged, planned as 8px dots that always carry their word; counts in plain words). On the survey list (surveys each with one status). Usage.
- **swap:** tone names and meanings to their statuses (paid, overdue, draft…). Tag text in their nouns. Rebuild the scene as their list of objects with statuses. Keep the "one status per row" and "a dot always comes with its word" rules if they suit; restate them in their words.
- **remove:** no (core)

### Button
- **page / board:** `p-C-0` / `B8T-0` (the gold board; see `page-pattern.md`)
- **core:** true
- **documents:** Variants and states (Primary, Secondary, On the map, Soft, Ghost, Destructive, Destructive text × Default, Hover, Focus, Disabled). Sizes (sm 32, md 40, lg 48, full-width 48 on the phone). Icon button (soft squares at 6: ghost, soft, secondary, on the map, xs). On Transect 4 (the office survey page beside Ruth's phone with Log quadrat). Usage (one moss action per surface; labels that name the result).
- **swap:** every label (Log quadrat, Submit survey, Export CSV, Add note, Mark for revisit…) to their verbs. The variant set to their shape language ("On the map" exists because Fieldwork floats buttons over a map; drop it or make it their floating variant). Sizes to theirs. Rebuild the scene from their product.
- **remove:** no (core). This is the page the "Your system in Planed" board shows by default.

### Button group and segmented
- **page / board:** `p-D-0` / `BZY-0`
- **core:** false
- **documents:** Segmented (Map / List, Cover % / Count and similar two- or three-way switches × Default, Hover, Focus, Disabled). Button groups (joined and spaced, such as Cancel beside Export CSV). In context (the survey page's toolbar with its switch). Usage.
- **swap:** track labels to their choices. Rebuild the scene. If the brief prefers tabs to segmented controls, say so here and point to Tabs.
- **remove:** yes, if their product has no one-of-few choices

### Calendar
- **page / board:** `p-E-0` / `LYN-0`
- **core:** false
- **documents:** Days (Default, Hover, Today, survey day with its transect code, inside the visit window, other month, can't pick). Setting the visit window (a 320 range popover, 14–27 April). Planning S-0415 (its office page with a Visit date field and the popover open). Usage.
- **swap:** the survey-day marker to whatever their dates carry (booking, due date, holiday). Month and dates to a plausible current month. The range to theirs. Rebuild the scene where their product picks dates.
- **remove:** yes, if their product never picks a date

### Card
- **page / board:** `p-F-0` / `BLQ-0`
- **core:** true
- **documents:** Survey card (In the field and Submitted: transect thumbnail, ID and title, status, place line, foot). Planned and sync failed (cards before a visit and after a failed sync, with one action). On Today (the Today page in the office shell). Panel, well and tile. Usage.
- **swap:** the card anatomy to their object's card (thumb, title, status, meta, one action). Card states to theirs (draft, live, failed…). Rebuild the Today scene as their list or dashboard. Keep Panel, well and tile, relabelled.
- **remove:** no (core)

### Charts
- **page / board:** `p-G-0` / `OLF-0`
- **core:** false
- **documents:** Records per quadrat (a column chart summing to 31, Q-08 dashed for records still on a phone). Over the morning (quadrats logged by time; records by observer). Meters (synced 29 of 31, seats 5 of 8). In the quadrat drawer (full-bleed: Q-09's drawer with its cover bars). Usage (one axis, colour only where it means something).
- **swap:** every series, axis and figure to a measure their product shows, drawn to scale. Meters to their limit or quota, or cut. Rebuild the scene.
- **remove:** yes, if their product shows no data

### Checkbox
- **page / board:** `p-I-0` / `EIN-0`
- **core:** true
- **documents:** Values and states (Unchecked, Checked, Indeterminate × Default, Hover, Focus, Disabled). Rows (a quadrat row, a transect with nested quadrats, a column row). In the export (the Export CSV modal ticking quadrats and columns: Species, Cover %, Count, Observer, Logged time, Coordinates, Notes). Usage (ticks wait for a button; square box).
- **swap:** labels to theirs. Row examples to their lists. Rebuild the scene as a multi-select in their product (export, invite, filters).
- **remove:** no (core)

### Chip
- **page / board:** `p-J-0` / `LMB-0`
- **core:** false
- **documents:** Kinds (filters, a species chip, a record tag such as Seedling, a key; default and other state, where each lives). On the Records page (the filter row: Survey, Observer, Quadrat, Species, with "6 of 29 records"). Usage (a chip names one thing).
- **swap:** chip kinds to theirs (filters, mentions, keys, applied tags). Rebuild the scene in their long list.
- **remove:** yes, if their product has no chips; key chips can move to Subcomponents

### Comment thread
- **page / board:** `p-H-0` / `EYB-0`
- **core:** false
- **documents:** Notes on a quadrat (Ruth's note on Q-07 at 10:46 and Imogen's reply at 10:48, on the phone and in the drawer). Composer (writing a note, Add note). In the office (full-bleed: the survey page with the drawer's notes open). Usage.
- **swap:** if their product has comments or messages: the thread to theirs (people, words, where a comment attaches, who resolves), the composer to theirs. If it doesn't, remove the page.
- **remove:** yes, if their product has no comments, threads or messages

### Drawer and sheet
- **page / board:** `p-17-0` / `DZ8-0`
- **core:** true
- **documents:** Anatomy (the quadrat drawer: 360 wide, full height, hairline left edge, flat; header, body, footer with Add note and Mark for revisit). On the survey page (full-bleed: Q-07's drawer beside the map and list). Sheet on a phone (the same content rising over the map, radius xl on top, Lifted, grabber). Usage (dock beside the work).
- **swap:** the drawer's content to a detail panel from their product. Widths, radius and shadow to the shape language. Rebuild both scenes. Keep the phone sheet if their product has a phone view.
- **remove:** no (core)

### Dropdown menu
- **page / board:** `p-K-0` / `JOH-0`
- **core:** false
- **documents:** Items and states (action, action that waits, destructive, already true × Default, Hover or focus, Busy or disabled). Two menus (a quadrat row's ⋯ menu and the account menu). In context (the quadrat list with Q-07's menu open). Usage (safe first, destructive last).
- **swap:** menu items to their actions (account, row actions). Rebuild the scene in their list. Keep the ordering rules.
- **remove:** yes, rarely; most products have a menu

### Empty state
- **page / board:** `p-L-0` / `RES-0`
- **core:** false
- **documents:** A new team (Severn Vale Wildlife Group's first run, with what will fill the space). Kinds (no surveys yet, no species found with "Did you mean", no offline map on the phone yet). Usage (show what will fill the space; one moss step).
- **swap:** each empty state to one their product has (first run, no results, 404, empty inbox), with their next step. The first-run scene to their product.
- **remove:** no in practice; every product has empty states

### Map controls
- **page / board:** `p-1B-0` / `DTK-0`
- **core:** false
- **documents:** Where controls sit (on the office map and the phone map, 12 off the edge). Two heights (hairline on the map; Lifted for what opens from them, such as the 280 Layers popover). Controls (zoom stack, Layers, Fit to transect, Locate, scale). On the survey map (full-bleed: the office window with the controls in place). Usage (controls stay out of the data's way).
- **swap:** this page is Fieldwork's map chrome. If their product has a canvas or map with floating tools (editor, map, board), rebuild it for their chrome and rename the page to suit. Otherwise remove it and fold the two-heights rule into Layout's Shadows.
- **remove:** yes, unless their product floats tools over a canvas or map

### Input
- **page / board:** `p-M-0` / `CFX-0`
- **core:** true
- **documents:** States (Default, Focus, Filled, Error, Disabled, with what changes). Kinds (species search, cover %, count, a note, coordinates). In context (Ruth's phone logging Q-09 at 10:40: species search and the record fields). Usage (label above; errors say how to fix).
- **swap:** every label, placeholder and value (species names, cover and count, coordinates) to their fields. Filled vs outlined, sunken vs white per the brief. Kinds to the fields their product has. Rebuild the scene as a form or search in their product.
- **remove:** no (core)

### Modal
- **page / board:** `p-N-0` / `BUE-0`
- **core:** true
- **documents:** Anatomy (a centred confirm over the survey page: 440 wide, radius xl, Lifted). States (working, couldn't). On the survey page (Mark Q-07 for revisit: "Today, after Q-12" or "Next visit"). Usage (both buttons say what they do; destructive fill only inside the confirm).
- **swap:** the confirm's question, body and buttons to a decision their product asks. Rebuild both scenes. Scrim strength and radius per the brief.
- **remove:** no (core)

### Navigation bar
- **page / board:** `p-O-0` / `BJ2-0`
- **core:** false
- **documents:** Top bar (the phone's top bar at survey level and quadrat level, the log form with ×, pressed, focus). Bottom bar (Map, Quadrats, Log, Notes; the active tab in moss). On Ruth's phone (two phone views: the map and the Quadrats tab). Usage.
- **swap:** rebuild as their top bar or app header: logo, items, account, actions. Fieldwork's office app has only a sidebar; use their structure. Cut the phone bars unless they have a phone app.
- **remove:** no in practice; most products have a top bar (if theirs is only a sidebar, remove and say so)

### Notification
- **page / board:** `p-P-0` / `NF3-0`
- **core:** false
- **documents:** On the phone (notification rows: a new note, a sync failure, a joined teammate, a survey ready to check). In context (Imogen's lock screen at 10:47 beside the quadrat it opens). Kinds (which Fieldwork events notify whom, and which stay in the app as toasts). Ready-to-check email (the "S-0409 is ready to check" email). Usage (one person, one event; no bell).
- **swap:** rows to their events, in their words. Who gets notified to their rule. The email section to their transactional email, or cut it.
- **remove:** yes, if their product sends no notifications

### Number stepper
- **page / board:** `p-T-0` / `LYL-0`
- **core:** false
- **documents:** States (Default, Hover on +, Typing, Lowest step, Error, Saving). Steps (how − and + move a count; units in words). In context (the log form on the phone with a count stepper). Usage (only for counts). Status: New · not built yet.
- **swap:** the counted thing (seedlings, plants) to a count in their product (quantity, seats, guests). Step rules to theirs. Rebuild the scene.
- **remove:** yes, if nothing is counted in steps

### Pagination
- **page / board:** `p-Q-0` / `NPN-0`
- **core:** false
- **documents:** Variants and states (range, show more, previous and next × Resting, Hover, At an end). On the Records page (the last page, 151–161 of 161 records). Usage (say the range in words; feeds grow in place).
- **swap:** the list to a long list in their product. Units in their nouns.
- **remove:** yes, if no list outgrows a page

### Map pins
- **page / board:** `p-1A-0` / `IQ9-0`
- **core:** false
- **documents:** Pins (logged, not logged with a note, planned × on the map, hover, selected in the office, selected on the phone). Sizes, line and labels (14px pins with a 2px paper ring, the dashed transect line, mono labels, a 44 tap target). On the S-0412 map (the office map and the phone, Q-07 selected at 10:47). Usage.
- **swap:** this whole page is Fieldwork's map. Keep it only if their product puts markers on a surface (map pins, annotations, hotspots); then rebuild it for their markers and rename the page to suit.
- **remove:** yes, in most runs; say so in the closing message

### Popover
- **page / board:** `p-18-0` / `GF7-0`
- **core:** true
- **documents:** Kinds (Fieldwork's popovers with widths drawn to scale, such as the observer popover and the 320 date popover, and where each opens). Anchor and placement (beside, flips then clamps, from a button). On the survey page (the observer popover from Q-07's drawer). Usage (keep the anchor in sight; no scrim).
- **swap:** the popover list to their popovers (filters, share, date, profile). Rebuild both scenes. Radius and shadow per the brief.
- **remove:** no (core)

### Pricing and plans
- **page / board:** `p-R-0` / `T9E-0`
- **core:** false
- **documents:** Plan cards (Free £0 for 3 seats, Team £12 a seat a month, Organisation £10 a seat from 21). Seats meter (5 of 8 seats used). On Team › Plan (the plan picker on the Team page). Usage (no countdowns, no "Most popular").
- **swap:** their plans and prices, or remove. The seats meter to their usage limit, or cut.
- **remove:** yes, if they don't sell plans

### Progress
- **page / board:** `p-S-0` / `SG7-0`
- **core:** false
- **documents:** Bars (logged 8 of 12, an offline map 156 of 312 MB, a sync of 2 records: each drawn to its number). Steps and spinner (the CSV export mid-way, 11 of 29 records; spinner sizes; in a button; in a caption). On the survey page (the full quadrat list with its progress). Usage (the number first; no bare spinners).
- **swap:** each bar to a process in their product (upload, onboarding steps, quota). Rebuild the step list and scene.
- **remove:** yes, rarely; most products show progress somewhere

### Radio
- **page / board:** `p-U-0` / `HME-0`
- **core:** false
- **documents:** Values and states (Not picked, Picked × Default, Hover, Focus, Disabled). Options with a field (quadrat size and placement, an option holding its own field). In context (planning S-0415: its quadrat size). Usage (only when options need room; something always picked).
- **swap:** option labels to a one-of-several choice in their product. Rebuild the scene.
- **remove:** yes, if Select and segmented controls cover their choices

### Select
- **page / board:** `p-V-0` / `GJN-0`
- **core:** true
- **documents:** Triggers and states (survey switcher, sort, field select × Default, Hover, Open, Disabled). Open list (each list open, grouped, with a check). On the survey page (the survey switcher open). On Ruth's phone (the list as a sheet). Usage.
- **swap:** triggers and options (survey switcher, quadrat sort, revisit reason) to selects in their product. Rebuild both scenes.
- **remove:** no (core)

### Sidebar
- **page / board:** `p-W-0` / `HJQ-0`
- **core:** false
- **documents:** Office sidebar (232 wide: the mark and team name, Today, Surveys, Sites, Species, Records, Team; resting, hover, current, focus; the account row). On Today (full-bleed: the sidebar beside the Today page at 1440). Usage (no count badges on nav rows).
- **swap:** nav items, icons and the account foot to theirs. Rebuild the full-bleed scene.
- **remove:** yes, if their product has no sidebar

### Slider
- **page / board:** `p-X-0` / `LYM-0`
- **core:** false
- **documents:** States (Default, Hover, Dragging, Typed, Keyboard focus, Disabled). Anatomy (track, fill, knob, band ticks). In the log form (a cover slider on the phone). Usage (for values judged by eye; always show the number). Status: New · not built yet.
- **swap:** the value (cover 0–100%) to a range in their product (price filter, volume, radius). Stops to theirs. Rebuild the scene.
- **remove:** yes, if nothing is set by eye

### Table
- **page / board:** `p-Y-0` / `R2B-0`
- **core:** true
- **documents:** Rows and states (species records: header in a lichen wash, rows, hover, selected). Numbers (cover and counts in fixed right-aligned slots, records per quadrat adding up to 31). On the survey page (full-bleed: the records table). Usage (hairlines between rows; right-aligned numbers).
- **swap:** columns and rows to a table from their product (orders, members, invoices), with numbers that add up. Rebuild the full-bleed scene as their table page.
- **remove:** no (core)

### Tabs
- **page / board:** `p-Z-0` / `MG4-0`
- **core:** true
- **documents:** Variants and states (underlined page tabs in moss and the segmented switch × Default, Hover, Selected, Disabled). Every tab in Fieldwork (Quadrats / Records / Notes / History; By quadrat / By species; People / Plan). On the team page (the Team page's tabs). Usage (page tabs underline; switches stay segmented).
- **swap:** tab sets to theirs. If the brief's shape language uses pill tabs, the underline rule flips: redraw the variants and rewrite the Usage pair. Rebuild the scene.
- **remove:** no (core)

### Text area
- **page / board:** `p-10-0` / `EHB-0`
- **core:** false
- **documents:** States (Empty, Typing, Grown, Didn't save, Read-only). In the office (keys: ⌘ Return, Return, Esc). Two places (the phone sheet and the office drawer). In context (Ruth typing her Q-07 note at 10:46). Usage.
- **swap:** the text area to where their product takes long text (notes, descriptions, messages). The keys to theirs, or cut. Rebuild the scene.
- **remove:** yes, if their product takes no long text (rare)

### Toast
- **page / board:** `p-19-0` / `IX0-0`
- **core:** true
- **documents:** Variants (saved, removed, marked for revisit, after Undo, a failed sync: one ink bar with Undo). Position, timing, stacking (bottom centre, six seconds, never stacked). On Ruth's phone, 10:52 (the sync-failed toast). Usage (only for changes someone might want back).
- **swap:** every message to an event in their product, in past tense with whose it was. Shape per the brief. Rebuild the scene.
- **remove:** no (core)

### Toggle
- **page / board:** `p-11-0` / `JOT-0`
- **core:** true
- **documents:** Values and states (Off, On × Default, Hover, Focus, Saving). Settings rows (Keep the screen on while logging; Email when a survey is submitted; Email when sync fails). When a sync fails (Leah's Today and settings at 10:52). Usage (the flip is the save; destructive things get a button).
- **swap:** settings to theirs. Rebuild the scene as a settings page in their product.
- **remove:** no (core)

### Tooltip
- **page / board:** `p-12-0` / `LOM-0`
- **core:** true
- **documents:** Variants and states (tooltips on Fieldwork's icon buttons × Rest, Hover, Keyboard focus). Placement and delay (below 6 apart; above near the bottom edge). In context (the survey page's map controls and quadrat list). Usage (label the icon only; a few words, verb first).
- **swap:** labels (Zoom in, Fit to transect, Layers…) to their icon buttons. Rebuild the scene in their toolbar.
- **remove:** no (core)

### Subcomponents
- **page / board:** `p-13-0` / `LJD-0`
- **core:** false
- **documents:** Counts and status (counts with units, quadrat status in words). Species name (the Latin name in italic with its common name). Keys (Esc). Copy field (coordinates). On the survey page (Q-09 selected, its drawer showing three records). Usage.
- **swap:** counts and statuses to theirs. Species name to a small part their product repeats, or cut. The copy field's value to something their product copies, or cut. Rebuild the scene.
- **remove:** yes, if the parts are already covered on other pages; merge what's left into Misc

### Misc
- **page / board:** `p-14-0` / `TRD-0`
- **core:** false
- **documents:** Dividers. Focus ring (button, field, row). Loading (map tiles pulse; working buttons such as Exporting CSV). Sync and clock times (how "last synced" and log times read). Behind a sheet (the phone map behind a sheet, no scrim). Usage.
- **swap:** keep Dividers, Focus ring and Loading with their examples. Sync and clock times to how their product writes times, or cut. Behind a sheet only if they use sheets.
- **remove:** no (it carries the focus ring and dividers); it may shrink

## Other pages and boards

- **Readme** (`p-1-0` / `VK4-0`): the kit's Readme, written for Fieldwork as the sample: its title, a lead saying it's a sample the agent restyles, a "Use this kit → Start here" line, the credit line with the licence line under it (keep it as it is), Fieldwork's five rules, the page list and the changelog (`v1.0 · Fieldwork sample generated with the planed-design-system skill`). Rewritten at the end of the run (SKILL.md step 6). Never delete it. The Readme has no eyebrow: its header is the title and the lead column. Its five rules are a plain list (a title at 18/24 semibold, the sentence under it in ink, no index numbers or row rules), and the page list's column heads carry no underline. One part the text sweep misses: the cover under the header, `Cover · S-0412 map` (the transect on the woodland-tint map). Rebuild the cover as their product's signature moment, drawn on their tokens in the same 360-tall band, or remove it if their moodboard gives nothing to show there.
- **Patterns** (`p-15-0`): one board, `Drop your screens here, then run Patterns` (`W93-0`). The kit carries no Patterns boards of its own; the optional Patterns run builds them from the person's screens.
- **Breadcrumbs** (`p-B-0`): an empty page at the end of the page list, after a divider. Fieldwork's own run removed Breadcrumbs (its office app is flat), and the Paper MCP can't delete a page. Don't build on it or count it; tell the person they can delete it in Paper. If their product needs breadcrumbs, document them on Navigation bar.
- **Review logs.** The kit carries none. If a copy has artboards named `… · review log`, delete them; they aren't part of the system.
- **Start here** is the person's page. Don't move their images or write on it. The kit's own boards here are built on the same tokens as every page, so the token swap (SKILL.md step 3) restyles them too: that's expected, leave them. Their moodboard images are literal and don't change. In the kit it holds two boards, found by layer name:
  - `Start here`: the title, the lead (the file is a sample system for a made-up product that the agent restyles into theirs), the steps and the prompt, and the dotted area `Drop your moodboard here`, where the person drops their images. The kit puts six example tiles in that area, named `Example · product screen`, `Example · screenshot`, `Example · logo`, `Example · type you like`, `Example · colour` and `Example · photo` (fernhill and the coffee app). They are not the person's moodboard: skip them when you read it (`moodboard-reading.md`). If the area holds only those six, the board is empty; ask (SKILL.md step 1).
  - `Your system in Planed`: the example of the step 7 board, showing Fieldwork's Button page in Planed's viewer chrome, with "Fieldwork" in the where pill. Step 7 edits it in place rather than drawing a new one (`planed-preview.md`, "Start from the kit's example"). Its chrome uses Planed's literal values, so the token swap doesn't touch the chrome; the shadow sweep skips the whole board.

## Count

7 Foundations + 37 Components = 44 pages, plus Start here, Readme, Patterns and the empty Breadcrumbs page (48 pages and 4 dividers in the kit file). Core: 7 Foundations + 15 components = 22. A first run leaves the other 22 Components pages for "do the rest".
