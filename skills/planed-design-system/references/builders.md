# Builders and fixers

How to split the page work across subagents (SKILL.md steps 4 and 5) when your agent can spawn them. One page costs 160–270k tokens to rebuild, so the orchestrator can't hold every page in its own context: it writes the brief and the ledger, sets the tokens, coordinates and checks. Builders rebuild pages; reviewers judge sets; fixers apply review notes.

## How it fits the run

1. **Button and Layout first.** Two builders (or you) build Button and Layout. They're linted and reviewed together until they pass or reach the round limit; then their best state is the bar, they go under Worth a look, the ledger freezes and the builders start. Nothing else is built meanwhile: every later builder matches Button's care, and duplicates Layout's canonical window (the ledger's shell) instead of drawing its own.
2. **One page per builder.** Every other page gets its own builder, started once Button and Layout have passed (or reached the round limit). All at once, or in waves of four if your agent limits parallel subagents.
3. **Sets of four for review.** When all four pages of a set are built and linted, a fresh reviewer takes the set (`reviewer.md`), with their passed Button page as the bar.
4. **Fixes.** A handful of mechanical notes you fix yourself. Otherwise one fixer per set takes that set's blocking notes. After a REDESIGN, the set goes back to a fresh reviewer (a confirmation review when every note was mechanical), up to the round limit in SKILL.md step 5.
5. **You keep the ledger, frozen.** Once Button and Layout pass, a builder or fixer may add a new object or person for its own page and report it; you mark it page-local in the ledger. No one changes or adds a shared fact (the shell, statuses, sizes, recurring scenes) after that, and no line applies to a page built before it (SKILL.md step 2).

## The shared builder brief

Write this once to your scratchpad (for example `builder-brief-<system-name>.md`), with the slots filled. Every builder and fixer reads the same file; their prompts carry only its path and their page. That keeps each prompt short and every page on one set of rules.

```md
# Builder brief: <System name>

You rebuild one page of <System name>'s design system in Paper, through the Paper MCP. The file started as the Planed design system kit, a sample system for a made-up product (Fieldwork, a survey app for ecologists); the page you're given still shows Fieldwork and you make it <product name>'s.

- File: <fileId>
- Brief and ledger: <absolute path to brief-<system-name>.md>
- The bar: their Button page, page <pageId>, artboard <artboardId>. It has passed review. Screenshot it once at 1x and match its care.
- The shell: Layout's main-layout scene, node <nodeId> on page <pageId>. When your In context scene shows the app's window, sidebar or nav, duplicate this node (`duplicate_nodes` with your section as parent) or `x-paper-clone` it, then crop or change only what your scene needs. Never redraw the shell from memory. Crop it on a boundary (a row edge, a panel edge, the window edge), never mid-word, through a pin or leaving a sliver of sidebar. What a shell control opens (an Export dialog, a filter, the account menu) is shared too: if the ledger doesn't define it, don't draw it; pick a scene that stays on your page.

## Settled facts

<The decisions you made that every page must share, each in a line: token choices that aren't obvious from the tokens (primary is ink, the accent is for focus and links), what stays round, the ground (plain, no dot grid), status colours and dot size, the type sizes scenes may use, anything the brief inferred. These are instructions for builders, not copy: never write them, or the reasoning behind them, onto a page.>
- Read before you start: <absolute path to the skill>/SKILL.md, step 4 "Each page" only; then, from <absolute path to the skill>/references/:
  - page-pattern.md (the anatomy every page keeps)
  - components.md: your page's entry, and "Fieldwork's sample data, everywhere"
  - paper-quirks.md
  - lint.md
  - tokens.md, "Round things" and "Shadows", if your page has round controls or raised surfaces

## Rules

1. Call get_guide({topic: "paper-mcp-instructions"}) first.
2. Touch only your page's artboard. Never set tokens, never edit another page.
3. Follow SKILL.md step 4, "Each page", items 1 to 6, in order: copy, In context, anatomy, header, Fieldwork-only sections, lint.
4. Every person, figure, date and status comes from the ledger, and so do the shell and the recurring scenes. Never change a fact about an object the ledger holds (its parts, dates, status, who acted). If your page needs something the ledger lacks, add a new object or person, keep it on your page, and report it.
5. Write only text that belongs on the page. The reasons in this brief, the references and your own notes stay off the canvas, and so do example sentences from the references (page-pattern.md's examples are examples, not copy).
6. Scene type uses the type scale only (11, 12, 13, 14, 16, 18, 24, 32, 36, 48, 72). Dry runs kept finding 10, 15, 20, 22, 28 and 44px in scenes; lint.md's off-scale sweep checks for those.
7. Read the page with get_tree_summary. Use get_jsx on one section only when you need its exact styles.
8. One visual group per write_html, a screenshot after each meaningful change, finish_working_on_nodes when you're done.
9. Before you report, run lint.md's sweeps scoped to your artboard and fix what they find.

## Report back (15 lines at most)

- What you rebuilt, section by section, in a few words each.
- New objects or people you added beyond the ledger, with their facts.
- Guesses you made where the brief, the ledger or the references were silent.
- Lint: clean, or what's left and why.
- Anything you couldn't do in Paper.
```

## Prompts

**Builder:**

> Read `<path to builder-brief>` and follow it. Your page: <page name>, page `<pageId>`, artboard `<artboardId>`.

**Fixer** (one per set):

> Read `<path to builder-brief>` and follow it, except rule 3: you don't rebuild, you fix. Your pages: <names, page IDs and artboard IDs>. Fix every blocking note in the review below, in the order SKILL.md step 5 gives ("Fixing"), then the polish notes if they're quick. Where a note contradicts the brief or the ledger, keep the brief and the ledger and say why in your report. <the review>

Reviewers get their own prompt (SKILL.md step 5, `reviewer.md`), not this brief.
