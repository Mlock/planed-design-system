# Reading the moodboard

How to turn the images on Start here into the brief you post in chat (SKILL.md step 2). The brief decides everything after it, so read the board properly before you write a word.

## 1. Look

1. `get_children` of the Start here page root. List what's there: images (fills on frames or rectangles), any text the person typed, any product screens (artboards or large frames that look like UI).
2. Screenshot the whole moodboard once at 1x for the overall feel, then each image or cluster at 1x or 2x so you can read type and see colour. A tall board comes back small; screenshot pieces.
3. Read any text they left. A sentence about the product outranks anything you infer from pictures.
4. Note what kind of thing each image is: their own product, a product they admire, a brand or logo, type specimens, photography, texture, a physical object. Their own product screens weigh the most, then their logo, then everything else.

If the board is empty or has one image, ask (at most three questions, SKILL.md step 1). Don't invent a system from nothing. If no answer can come in this session (you're running unattended), infer, and mark every inferred part of the brief as inferred.

## 2. The brief, part by part

Post it as a short block in chat, in this order. Each part has a rule for how to get it.

### Mood word

One physical condition or register (the Paper guide's list is a good source: mineral, maritime, bookish, alpine, signage, gallery, terminal, candlelit…). Pick the one that the most images share, not the most striking image. Then name the objects in that scene that the colours will come from ("maritime: fog, hull navy, signal-flag yellow"). If you can't name an object for a role, the palette isn't from the board yet.

### Palette with roles

Six to ten colours, each with a hex **and a role** that maps onto the kit's primitives (`tokens.md`, "Set: colour primitives"):

- **Ground** (`--color-canvas`) and **surface** (`--color-white`): from the board's lightest large areas, or darkest if the board is dark. Decide light or dark here; if the board is split, ask.
- **Ink** (`--color-ink`) and **muted text** (`--color-slate`): from the board's text or darkest shape. Pure black only if the board uses it.
- **Accent** (`--color-link` and its 50% and 12% steps): the one colour that does the interactive work. Usually the colour that's on their logo or their product's buttons; otherwise the board's single most saturated recurring colour.
- **Attention** (`--color-pushpin`), **success** (`--color-pin-green`), **warning** (`--color-needs-owner` family), **danger** (`--color-oxblood` family): take them from the board when it has them; otherwise derive them from the same scene so they sit with the palette (a warm board gets a brick red, not a fire-engine red).
- **Four tints** (`--color-butter`, `rose`, `sky`, `sage`): light colours ink reads on, for avatars, tags and chart categories. Pull them from the board's secondary colours, lightened.
- **Neutrals between** (`--color-surface-muted`, `surface-sunken`, `line`, `canvas-dot`, `ash`): derived steps between ground and ink, tinted the way the ground is tinted.

Measure colours from the images; don't guess from memory of a brand. The board outranks general taste rules: if it pairs colours a design guide calls a cliché, it's their brand, so follow it. When the image is a photo, sample a flat area, not a highlight. Then check contrast (`tokens.md`, "Contrast") before you post: a palette that fails contrast gets fixed in the brief, not discovered on the pages.

### Type pair

A display face and a text face (they can be the same), plus a mono if the product shows code, addresses or data.

1. Identify the type in the images: their logo, their product screens, specimens they dropped. Name the closest family you can identify; say when it's a guess.
2. Call `get_font_family_info` with the candidates **before** naming them in the brief. Use the exact family name it returns, and note the weights it has (the boards need 400, 500 and 600, or the nearest).
3. **When a family is missing** (a commercial face that isn't on their machine or Google Fonts): pick the closest available family with the same skeleton (geometric, grotesque, humanist, transitional serif, slab, mono) and similar width and x-height. Compare two or three candidates and choose on those grounds, not because an example here names one. Confirm it with `get_font_family_info`, and say in the brief why it's closest, for example: "Söhne isn't available in Paper here; using Inter Tight, closest in width. Install Söhne and change `--font-sans` to switch." Never set a token to a family that didn't resolve: Paper falls back to the system sans silently.
4. Say where each face goes: display for H1s and big figures, text for everything else, mono for addresses.
5. **Display tracking.** The kit's `-0.01em` is Fieldwork's, set for IBM Plex Sans. A tight grotesque often wants `-0.02em` to `-0.03em`; a serif or wide display face `-0.01em` to `0`. Name the value; it goes into `--tracking-display` and onto every H1 (SKILL.md step 4, "Header").

### Shape language

Decide three things and say them plainly:

- **Corners:** pill, rounded (say the main radius), or square. Read it from their product's buttons and cards first, then from the board's overall feel (soft photography and rounded type → rounder; grids, rules and grotesques → squarer).
- **What stays round:** in a square system, say which round things keep their circle. Radios and status dots always do (a square radio reads as a checkbox); avatars do unless the board shows square ones (`tokens.md`, "Round things").
- **Raised or flat:** do surfaces float on soft shadows, or sit flat with hairlines? This decides whether the four shadow recipes stay or flatten (`tokens.md`, "Shadows").
- **Component anatomy changes:** the specific shifts this causes in the kit (square buttons; outline secondary; underlined tabs instead of segmented; filled or outlined inputs). Name the pages they affect.

### Density

Compact, regular or roomy, from their product screens if they gave any (row heights, padding, type size), otherwise from the board's whitespace. The kit (Fieldwork) is regular: matrix rows 72, table rows 40, list rows 50, body 14–16. Say what changes if not regular (rows 56, body 13; or rows 88, body 16).

### Voice

Two lines: how their product talks (plain or playful, formal or familiar, terse or warm) with one example sentence in that voice, written for their product. Take it from any copy on the board, their sentence about the product, or their product screens. If there's no copy at all, say the voice is inferred and keep it plain.

### The product's nouns

The words their product uses for its main things, replacing Fieldwork's, the kit's sample: survey, transect, quadrat, visit, record, lead, observer, note. List each replacement you'll use ("survey → Project; quadrat → Page; observer → Client"), and drop the ones that have no equivalent. Capitalise them only if their product does. These nouns go into every page's copy, sample data and Usage captions.

### The ledger

The one set of sample data every page draws from, so the system agrees with itself. Twenty pages built by separate builders, and reviewed by separate reviewers, will each invent their own timeline unless one is written down first. In a dry run without it, five of six review sets failed on Made-up data (one invoice with three due dates), and each reviewer proposed a different fix.

Write it before any page is built. It goes into the saved brief in full and into the chat brief as two lines. Make it specific enough that a builder never needs to invent a fact about one of its objects:

- **Today.** The date every page is set on, with the weekday ("Thursday 20 November"). Pick a date that suits the content rather than the real date: the season their data happens in, a point in their cycle (month end, term start).
- **People.** Four to six, with names that fit their market, initials, a role each, and who does what (who sends, who approves, who's new).
- **Objects.** Three to five of their main things (invoices, bookings, orders, projects…), each with its ID or name, its parts with figures (line items, quantities, prices) that add up to its total, its dates (created, due, done), its status today, and who acted on it.
- **Timeline.** Six to ten dated events, in order, that lead to today's state: who did what to which object, and when.
- **In progress.** Any process their product runs (a month-end close, an onboarding, a checkout), its steps, and which are done today.
- **Records.** Secondary records their product lists (bank lines, messages, notifications, payments), each tied to an object and a date on the timeline.
- **Settings and figures.** The plan, limits and counts their product shows, consistent with everything above.
- **Shell.** The app's window as every scene draws it: the nav model (sidebar or top bar, and its items in order), the main view, and the widths of the recurring sheets, drawers and popovers. Also any recurring scene more than one page will show (their booking page, their checkout sheet) with its copy, plus the status colours with the dot size, and the type sizes scenes may use. In a dry run without it, each builder drew its own sidebar and sheet widths, and nearly every review after round 1 failed on pages disagreeing with each other.

Rules for everyone who uses it. The ledger is frozen once Button and Layout pass (SKILL.md step 2):

- A page that shows a ledger object shows it as the ledger says: the same parts, dates, status and people. A page may show a subset.
- A page that needs something the ledger doesn't hold adds a new object or person, never a new fact about an existing one or about the shell, and the builder reports it so you can note it in the ledger as page-local.
- Reviewers check every page against the ledger, not against each other (`reviewer.md`).

## 3. Example

> **Brief: Tidewater (a ferry-booking app)**
> - **Mood:** maritime: fog on the slipway, hull navy, life-ring orange.
> - **Palette:** ground `#F1F3F4` fog, surface `#FFFFFF`, ink `#13233A` hull navy, muted `#5B6B7C`, accent `#1F5FAF` harbour blue, attention `#E8572A` life-ring, success `#2D7A5B`, danger `#B3261E`, tints sand `#EFE3C8`, buoy `#F6D2C4`, sea `#CFE0EE`, kelp `#D4E4D0`.
> - **Type:** display Fraunces 600 (confirmed), text Inter 400/500/600 (confirmed), mono JetBrains Mono for booking refs. Display tracking -0.01em.
> - **Shape:** rounded 10, flat with hairlines; secondary buttons outlined; tabs underlined. Avatars, radios and dots stay round.
> - **Density:** regular.
> - **Voice:** plain and calm, times first. "The 08:40 to Ryde leaves from berth 2. Boarding closes 10 minutes before."
> - **Nouns:** survey → Crossing; quadrat → (none); observer → Passenger; note → Note; visit → Timetable.
> - **Ledger:** today Fri 14 March; Ana Costa and Rob Hale (passengers), Mei Lin and Tom Reyes (desk); bookings TW-2041 Portsmouth → Ryde 08:40, 2 adults × £14.50 = £29.00, paid; TW-2047 Lymington → Yarmouth 10:15, adult and car £62.00, awaiting payment. Full ledger saved with the brief.

The full ledger in the saved brief, for the same product:

```md
## Ledger
Today: Friday 14 March. Timetable: spring, from 1 March.
People: Ana Costa (AC), passenger, travels weekly · Rob Hale (RH), passenger, first booking · Mei Lin (ML), desk at Ryde, handles changes and refunds · Tom Reyes (TR), desk at Lymington.
Bookings:
- TW-2041 · Ana Costa · Portsmouth → Ryde, Fri 14 March 08:40 · 2 adults × £14.50 = £29.00 · paid 10 March by card ··4821 · checked in 08:12 · berth 2
- TW-2047 · Rob Hale · Lymington → Yarmouth, Sat 15 March 10:15 · 1 adult £14.00 + car £48.00 = £62.00 · created 13 March · awaiting payment, link expires 15 March 09:15
- TW-2039 · Ana Costa · Ryde → Portsmouth, Fri 7 March 17:30 · 2 adults × £14.50 = £29.00 · refunded £29.00 on 7 March by Mei Lin (sailing cancelled, wind)
Timeline: 7 Mar 16:05 the 17:30 is cancelled · 7 Mar 16:20 Mei Lin refunds TW-2039 · 10 Mar Ana books TW-2041 · 13 Mar Rob creates TW-2047 · 13 Mar Tom Reyes sends Rob the payment link · 14 Mar 08:12 Ana checks in.
In progress: Rob's booking: details done, vehicle done, payment not yet.
Records: card payment £29.00 on 10 Mar (TW-2041); refund −£29.00 on 7 Mar (TW-2039).
Figures: the 08:40 sailing has 212 of 240 seats booked; car deck 38 of 40.
Shell: top bar (Today, Bookings, Sailings, Refunds; desk name right), the day's sailings list as the main view, booking detail docks right at 360, popovers 320. Status dots 6px: paid success, awaiting payment warning, refunded slate. Scene type: 12, 13, 14, 16, 24 only.
```

Then carry on. The person can redirect while you work.
