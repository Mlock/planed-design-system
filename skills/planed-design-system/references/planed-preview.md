# "Your system in Planed"

How to fill the last board of the run (SKILL.md step 7): the person's Button page shown as a Screen in Planed's viewer, with two Comment pins and one open thread, then one line and the Join the waitlist button. It shows what their team would see if they shared the system through Planed.

**Two systems on one board.** The Screen inside is theirs and stays on their tokens. Everything around it is Planed and is drawn in **Planed's own values, written as literals**: their file's tokens now hold their colours and fonts, so `var(--color-ink)` would paint Planed's chrome in their palette. Never use `var(…)` in the chrome.

## Planed's values (literal)

| Role | Value |
|---|---|
| Ink (text, primary fill, the mark) | `#17171A` |
| Muted text | `#6C6C70` |
| Quiet text, keys, slashes | `#A8A8AC` |
| Hairline, dividers | `#E3E3E0` |
| Sheet | `#FFFFFF` |
| Table (the canvas) | `#EDEDEB`, dotted: `radial-gradient(circle, #D6D6D2 1.1px, transparent 1.3px) 0 0 / 24px 24px #EDEDEB` |
| Sunken well | `#F5F5F3` |
| Reviewer tints | Jo Kim `#F5CFDD` (rose, first), Ade Bello `#C7DDF4` (sky, second) |
| Font | `"Geist"` for everything (confirm with `get_font_family_info` once; it is on Google Fonts) |
| Float shadow | `#00000010 0 0 0 1px, #0000000A 0 1px 2px, #0000000F 0 12px 32px` |
| Lifted shadow | `#00000010 0 0 0 1px, #0000000A 0 2px 4px, #0000001A 0 24px 56px` |
| Ink lift | `#00000026 0 1px 2px, #00000014 0 8px 24px` |
| Screen shadow | `#00000014 0 0 0 1px, #0000000A 0 2px 4px, #00000014 0 16px 40px` |

The copy is in `copy.md` (`preview.thread`, `preview.line`, `preview.button`). Paste it as written.

## Start from the kit's example

The kit's Start here page already holds this board, named `Your system in Planed`, showing the kit's sample system, Fieldwork: its Button page inside Planed's viewer chrome. **Edit it; don't draw a new one.** Find it by name (IDs differ in a copied file):

1. Inside its `Window`, the `Screen` frame holds a copy of Fieldwork's Button artboard. Delete that child, then put the person's Button artboard in `Screen` with `x-paper-clone`, as "The board", step 4 says.
2. In `Where pill`, replace `Fieldwork` with their system's name (and `Button` if they renamed the page).
3. Move `Pin 1 · Jo Kim · open` and `Pin 2 · Ade Bello · closed` to the exact spots in "The pins" below, then `Thread` beside Pin 1 ("The thread popover"). If their page isn't Button, rewrite the two Comments.
4. Leave the `Mode pill`, `Share` and `Footer` (the line, `Join the waitlist · https://planed.cc/sign-in?ref=design-kit`, the `Waitlist URL` line and the small print) as they are. A Paper board can't carry a working link, so the visible URL line is how the link shows on the board; the closing message carries the clickable one.
5. Run "Before you finish".

Do this last in the run, after every fix to their Button page: the clone is a static copy, so later edits to the page won't reach it. Keep the board where it is, to the right of the `Start here` board. Only if the example is gone, draw the board as below.

## The board

1. **Placement.** On the Start here page, to the right of the moodboard with an 80 gap, top-aligned. Check `get_basic_info` for the page so it overlaps nothing. `create_artboard` ignores `top` and `left`; move it with `update_styles` afterwards.
2. **The artboard.** Name it `Your system in Planed`. 1600 wide, `height: fit-content`, flex column, background `#EDEDEB`, overflow clip.
3. **The window** (first child). A frame 1600 × 1000, `position: relative`, overflow clip, the dotted table background above. Everything in steps 4–8 sits inside it, absolutely positioned.
4. **The Screen.** A viewport frame at left 80, top 84, 1440 × 916, radius 4, overflow clip, background `#FFFFFF`, the Screen shadow. Put the person's Button artboard inside it at 1x:
   - first try `write_html` into the viewport with `<x-paper-clone node-id="<their Button artboard id>" style="position: relative; left: 0; top: 0; translate: 0;" />` (clones keep their absolute position; see `paper-quirks.md`);
   - if the clone doesn't render, `duplicate_nodes` the Button artboard with `parentId` set to the viewport frame, then `update_styles` it to `position: relative; left: 0; top: 0`.
   The viewport cuts the page off at the bottom, the way a viewer scrolls. The header and the Variants and states section must be in view; check with a screenshot. If their strongest page isn't Button, use that page instead and rewrite the two Comments for its components (the deck allows this).
5. **The chrome**, three floating groups 12 off the window's top edge (top 12):
   - **Where pill**, left 12.
   - **Mode pill**, centred on the window (left = (1600 − its width) / 2; read the width with `get_node_info` after writing it).
   - **Share**, right 12.
6. **Pin 1 (open)** on the disabled Primary button and **Pin 2 (closed)** on the default Primary button, positioned over the Screen (below).
7. **The thread popover** beside Pin 1.
8. Nothing else on the window. No Planed editor panels, no Links, no Screens list.
9. **The footer** (second child of the artboard): the line, the button, the URL line and the small print (below).

Write one group per `write_html` call, screenshot after each, and call `finish_working_on_nodes` at the end.

## The where pill

The plane mark, then `<their system name> / Components / Button` with a chevron, a hairline, previous and next.

```html
<div style="position:absolute; left:12px; top:12px; display:flex; align-items:center; gap:2px; height:48px; padding:0 6px; border-radius:999px; background:#FFFFFF; box-shadow:#00000010 0 0 0 1px, #0000000A 0 1px 2px, #0000000F 0 12px 32px;">
  <div style="width:36px; height:36px; display:flex; align-items:center; justify-content:center; flex-shrink:0;">
    <svg width="18" height="15" viewBox="-18 -18 844 716" xmlns="http://www.w3.org/2000/svg"><path d="M807.472 0L600 679.095L369 521L238 658L190 402L0 266L807.472 0ZM48 272L731 48L201 381L48 272ZM214 400L714 73L308 468L249 607L214 400ZM281 583L323 494L351 513L281 583ZM338 472L770 53L587 645L338 472Z" fill-rule="evenodd" clip-rule="evenodd" fill="#17171A" stroke="#17171A" stroke-width="28" stroke-linejoin="round"/></svg>
  </div>
  <div style="display:flex; align-items:center; gap:6px; height:36px; padding:0 10px 0 4px;">
    <span style="font-family:'Geist'; font-size:14px; line-height:18px; color:#6C6C70;">{System name}</span>
    <span style="font-family:'Geist'; font-size:14px; line-height:18px; color:#A8A8AC;">/</span>
    <span style="font-family:'Geist'; font-size:14px; line-height:18px; color:#6C6C70;">Components</span>
    <span style="font-family:'Geist'; font-size:14px; line-height:18px; color:#A8A8AC;">/</span>
    <span style="font-family:'Geist'; font-size:14px; line-height:18px; font-weight:500; color:#17171A;">Button</span>
    <svg width="14" height="14" viewBox="0 0 14 14"><path d="M4 5.5L7 8.5L10 5.5" fill="none" stroke="#6C6C70" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/></svg>
  </div>
  <div style="width:1px; height:20px; background:#E3E3E0; flex-shrink:0;"></div>
  <div style="width:36px; height:36px; display:flex; align-items:center; justify-content:center;"><svg width="16" height="16" viewBox="0 0 16 16"><path d="M10 3.5L5.5 8L10 12.5" fill="none" stroke="#17171A" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"/></svg></div>
  <div style="width:36px; height:36px; display:flex; align-items:center; justify-content:center;"><svg width="16" height="16" viewBox="0 0 16 16"><path d="M6 3.5L10.5 8L6 12.5" fill="none" stroke="#17171A" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"/></svg></div>
</div>
```

`{System name}` is the name from the brief, the Readme's title, on its own ("Tidewater", not "Tidewater design system"; the kit's example reads "Fieldwork"). Use the person's real page name if they renamed Button.

## The mode pill

Navigate, Comment (on, because pins are showing), Hide Nav. The mode that's on is the only ink in the chrome besides the mark.

```html
<div style="position:absolute; top:12px; display:flex; align-items:center; gap:4px; padding:6px; border-radius:999px; background:#FFFFFF; box-shadow:#00000010 0 0 0 1px, #0000000A 0 1px 2px, #0000000F 0 12px 32px;">
  <div style="display:flex; align-items:center; gap:8px; height:40px; padding:0 14px 0 12px; border-radius:999px;">
    <svg width="16" height="16" viewBox="0 0 16 16"><path d="M3.5 2.5L12.5 7L8.3 8.3L7 12.5L3.5 2.5Z" fill="none" stroke="#17171A" stroke-width="1.5" stroke-linejoin="round"/></svg>
    <span style="font-family:'Geist'; font-size:13px; line-height:16px; font-weight:500; color:#17171A;">Navigate</span>
  </div>
  <div style="display:flex; align-items:center; gap:8px; height:40px; padding:0 14px 0 12px; border-radius:999px; background:#17171A;">
    <svg width="16" height="16" viewBox="0 0 16 16"><path d="M8 2.2C4.7 2.2 2.2 4.5 2.2 7.3C2.2 8.6 2.7 9.8 3.6 10.7L2.8 13.8L6.2 12.2C6.8 12.4 7.4 12.4 8 12.4C11.3 12.4 13.8 10.1 13.8 7.3C13.8 4.5 11.3 2.2 8 2.2Z" fill="none" stroke="#FFFFFF" stroke-width="1.5" stroke-linejoin="round"/></svg>
    <span style="font-family:'Geist'; font-size:13px; line-height:16px; font-weight:500; color:#FFFFFF;">Comment</span>
    <span style="font-family:'Geist'; font-size:11px; line-height:14px; color:#FFFFFF; opacity:0.6;">C</span>
  </div>
  <div style="width:1px; height:20px; background:#E3E3E0; flex-shrink:0;"></div>
  <div style="display:flex; align-items:center; gap:8px; height:40px; padding:0 14px 0 12px; border-radius:999px;">
    <svg width="16" height="16" viewBox="0 0 16 16"><path d="M2 8C3.5 5 5.6 3.5 8 3.5C10.4 3.5 12.5 5 14 8C12.5 11 10.4 12.5 8 12.5C5.6 12.5 3.5 11 2 8Z" fill="none" stroke="#17171A" stroke-width="1.5" stroke-linejoin="round"/><circle cx="8" cy="8" r="2" fill="none" stroke="#17171A" stroke-width="1.5"/><path d="M2.5 13.5L13.5 2.5" fill="none" stroke="#17171A" stroke-width="1.5" stroke-linecap="round"/></svg>
    <span style="font-family:'Geist'; font-size:13px; line-height:16px; font-weight:500; color:#17171A;">Hide Nav</span>
    <span style="font-family:'Geist'; font-size:11px; line-height:14px; color:#A8A8AC;">H</span>
  </div>
</div>
```

## Share

A white pill at 48, Float, right 12. Share is a Secondary action, so it stays white: the chrome has no ink button.

```html
<div style="position:absolute; right:12px; top:12px; display:flex; align-items:center; height:48px; padding:0 20px; border-radius:999px; background:#FFFFFF; box-shadow:#00000010 0 0 0 1px, #0000000A 0 1px 2px, #0000000F 0 12px 32px;">
  <span style="font-family:'Geist'; font-size:14px; line-height:18px; font-weight:500; color:#17171A;">Share</span>
</div>
```

## The pins

A pin is a pushpin: round with one sharp corner (bottom-left, radius 4) pointing at the exact spot, filled with its author's tint, initials in ink. Place the sharp corner on the element the Comment is about.

**Find the spots.** Both pins go on the Primary row of the person's Variants and states matrix: Pin 1 on its **Disabled** button, Pin 2 on its **Default** button (the first state column). Read each button's position and size with `get_children` / `get_node_info` on the cloned or duplicated artboard. Window coordinates = the node's position inside the artboard + the viewport's offset (80 across, 84 down).

**Place each pin by its sharp corner** (bottom-left). The sharp corner sits 4px inside the button's top-right corner, so the point touches the button and the pin's body rises above it to the right:

- pin left = button's right edge − 4
- pin top = button's top edge + 4 − the pin's size (30 for Pin 1, 24 for Pin 2)

If the matrix has no Disabled column, put Pin 1 on the Primary row's faintest state and keep the Comments, which are about faintness.

**Pin 1, open** (Jo Kim, on the disabled Primary button), 30, ringed in ink because its thread is open:

```html
<div style="position:absolute; width:30px; height:30px; display:flex; align-items:center; justify-content:center; background:#F5CFDD; border-radius:999px 999px 999px 4px; box-shadow:#FFFFFF 0 0 0 3px, #17171A 0 0 0 5px, #00000026 0 1px 2px, #00000014 0 8px 24px;">
  <span style="font-family:'Geist'; font-size:12px; line-height:16px; font-weight:600; color:#17171A;">JK</span>
</div>
```

**Pin 2, closed** (Ade Bello, on the button row), 24, a white ring and a hairline:

```html
<div style="position:absolute; width:24px; height:24px; display:flex; align-items:center; justify-content:center; background:#C7DDF4; border-radius:999px 999px 999px 4px; box-shadow:#FFFFFF 0 0 0 2px, #00000014 0 0 0 3px, #00000026 0 1px 2px, #00000014 0 8px 24px;">
  <span style="font-family:'Geist'; font-size:10px; line-height:12px; font-weight:600; color:#17171A;">AB</span>
</div>
```

The pins are the only saturated colour on the chrome. No red unread dot: these Comments are the team's example, not news.

## The thread popover

356 wide, radius 24, Lifted, 16 to the right of Pin 1 with its top level with the pin's top. If there's no room on the right inside the window (the Disabled column is usually the last one, so expect this), open it on the left: its right edge 16 left of the pin and its top 16 below the button the Comment is about, so the button stays in view. Either way it must stay 12 clear of the window edges and must not cover that button.

```html
<div style="position:absolute; width:356px; display:flex; flex-direction:column; background:#FFFFFF; border-radius:24px; box-shadow:#00000010 0 0 0 1px, #0000000A 0 2px 4px, #0000001A 0 24px 56px;">
  <div style="display:flex; flex-direction:column; gap:2px; padding:16px 20px 14px; border-bottom:1px solid #E3E3E0;">
    <span style="font-family:'Geist'; font-size:14px; line-height:21px; font-weight:600; color:#17171A;">On the disabled Primary button</span>
    <span style="font-family:'Geist'; font-size:12px; line-height:16px; color:#6C6C70;">Components / Button</span>
  </div>
  <div style="display:flex; flex-direction:column; gap:16px; padding:16px 20px;">
    <!-- one message: repeat for Ade Bello with #C7DDF4, AB, 1h -->
    <div style="display:flex; gap:12px;">
      <div style="width:28px; height:28px; flex-shrink:0; border-radius:999px; background:#F5CFDD; display:flex; align-items:center; justify-content:center;"><span style="font-family:'Geist'; font-size:11px; line-height:14px; font-weight:500; color:#17171A;">JK</span></div>
      <div style="display:flex; flex-direction:column; gap:2px; flex:1 1 0; min-width:0;">
        <div style="display:flex; align-items:baseline; gap:8px;"><span style="font-family:'Geist'; font-size:13px; line-height:16px; font-weight:600; color:#17171A;">Jo Kim</span><span style="font-family:'Geist'; font-size:12px; line-height:16px; color:#A8A8AC;">2h</span></div>
        <span style="font-family:'Geist'; font-size:14px; line-height:21px; color:#17171A;">Is disabled too faint? I can barely tell it apart on my laptop.</span>
      </div>
    </div>
  </div>
  <div style="padding:0 12px 12px;">
    <div style="display:flex; align-items:center; justify-content:space-between; gap:12px; padding:12px 12px 12px 16px; border-radius:12px; background:#F5F5F3; box-shadow:#00000014 0 0 0 1px;">
      <span style="font-family:'Geist'; font-size:14px; line-height:21px; color:#A8A8AC;">Reply…</span>
      <div style="width:32px; height:32px; flex-shrink:0; border-radius:999px; background:#A8A8AC; display:flex; align-items:center; justify-content:center;"><svg width="14" height="14" viewBox="0 0 14 14"><path d="M7 11.5V2.5M7 2.5L3 6.5M7 2.5L11 6.5" fill="none" stroke="#FFFFFF" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"/></svg></div>
    </div>
  </div>
</div>
```

The header names the component the pin is on ("On the disabled Primary button"); if the Comment sits on a differently named variant in their system, use their name. The second line is the page path in the where pill. Build the two messages as two `write_html` calls into the messages column.

## The footer

Under the window, on `#EDEDEB`: a row with 64 padding top and bottom and 80 at the sides, `align-items: center`, `justify-content: space-between`, gap 48.

- **Left:** `preview.line` at 24/30, weight 600, letter-spacing -0.015em, `#17171A`, max 760 wide.
- **Right:** a column, gap 10, aligned to the end:
  - The button `Join the waitlist`: 48 tall, padding 0 24, radius 999, background `#17171A`, Ink lift, label 16/24 weight 500 `#FFFFFF`. Paper boards can't carry a working link, so name the layer `Join the waitlist · https://planed.cc/sign-in?ref=design-kit` and show the URL as text under it (next item). The closing message in chat carries the clickable link.
  - The URL line `planed.cc/sign-in?ref=design-kit`, layer `Waitlist URL`: 13/18, weight 500, `#17171A`, underlined, `width: max-content`.
  - The small print from `preview.button`: 13/18, `#6C6C70`.
- Bottom-left of the footer, under the line: the plane mark at 17 and "Planed" at 16/24 weight 600 `#17171A`, gap 10. This is the only Planed wordmark on the board.

## Before you finish

Screenshot the whole board, then the chrome and the thread at 2x:

- The chrome reads as Planed: grey dotted table, white pills, ink, Geist. Nothing in it took the person's colours or fonts (if anything did, a `var(…)` slipped in).
- The Screen is theirs: their colours, fonts and shapes, exactly as their Button page.
- Pin 1's sharp corner is 4px inside the disabled Primary button's top-right corner, and the thread doesn't cover that button. Pin 2's sharp corner is the same way on the default Primary button.
- The popover clears the window edges by at least 12.
- The copy matches `copy.md` exactly, with `{System name}` filled.
- `finish_working_on_nodes`.
