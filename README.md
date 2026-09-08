# HOUSE

A series of **HTML apps** that show how a Treasure Coast house actually gets built — every part on a periodic table, a house you build by dragging parts onto it, and the ten county inspectors who decide whether it counts.

Live:

- **Block 3D** — [`apps/cbs3d/index.html`](apps/cbs3d/index.html) — the same house as a **real 3D model you can spin**. Drag to orbit, scroll to zoom; cutaway is a clipping plane through the middle of the building. three.js from a CDN, everything else self-contained. Falls back to a link to the flat version when WebGL will not start.
- **Block** — [`apps/cbs/index.html`](apps/cbs/index.html) (`HOUSE Block`, crew edition) — the flat version: section + elevation, no dependencies, runs on anything.

Both share one engine, one catalog and one set of gates. The only difference is what the middle of the screen draws.

**Play them in order: Block, then Block · Advanced.** Block teaches the *order* of a house — one path, no forks, so a new hire never has to choose before he understands. Advanced (`PLAN.md` §10, not built) teaches the *judgement*: card 2 becomes monolithic-slab-or-stem-wall, and picking stem wall adds two county inspections and renumbers everything after it.

Training model, not a permit. Sister project: [ROOF](../ROOF/README.md) — the dry-in tile in this game is the whole ROOF Shingle game folded into one step.

---

## The one-paragraph version

Most "how a house is built" pictures are twelve cards in a row. A real CBS house is a **partial order with ten gates**: the county inspects the underground plumbing, the slab, the tie beam, the sheathing and straps, the dry-in, the three roughs, the framing, the insulation, the drywall, and the final — and nothing may cover what the inspector has not seen. Between the gates, the order is the house's, not a list's. And the cruel part: a house done wrong looks exactly like a house done right from the street. Toe-nailed trusses and a bare suction line both disappear under stucco and drywall. The only truth is the inspector.

## Repo map

| File | What's in it |
|---|---|
| [`index.html`](index.html) | Series hub |
| [`apps/cbs3d/index.html`](apps/cbs3d/index.html) | **Live.** The 3D model. Same ring, same ten gates; the house is ~1,370 meshes built from the catalog, one unit = one foot. |
| [`apps/cbs/index.html`](apps/cbs/index.html) | **Live.** The flat version. Ring → drag → cutaway / street / inspector → ten gates. One file, no dependencies. |
| [`PLAN.md`](PLAN.md) | Block build plan: what accurate means, the table grammar, the 40-tile catalog, the engine, open decisions |

## Sister projects (same DNA)

- **ROOF** — same shell, same ring, same inspector. Five gates inside this game's one dry-in tile.
- **BODY** — the dark stage, the honest-imaging toggle, the evidence grades.
- **Periodic Table of Frameworks** (RULEROFWISDOM `/forum`) — the tray: families, rows, seats, gaps, complements, *data not code paths*.

## Run HOUSE Block

Open [`apps/cbs/index.html`](apps/cbs/index.html). It needs `<meta charset="utf-8">` (it has it) — without it, `file://` shows mojibake.

1. Drag **Pm — Pull the permit** onto the house. Then try dragging the block. Watch it leak.
2. Work around the ring clockwise. Call each inspection from the paper shelf above the house when its row is done — the gates are tiles.
3. Toggle **Street** after the stucco goes on. Then read the hint.
4. There are two tiles that lie. You will find one at the sheathing inspection and one at the roughs.
5. Checks the engine must still pass:
   - Nothing lands before the permit.
   - The slab refuses to pour before the slab inspection.
   - Trusses refuse to set before the beam is poured; the beam refuses to pour before the tie-beam inspection.
   - Toe-nailed trusses land, then fail the sheathing/strapping gate and come out.
   - A bare line set lands, then fails the roughs and comes out.
   - Drywall refuses to hang before the insulation inspection; attic insulation refuses before the drywall inspection.
   - The final needs all seven of its trades.

## Evidence grades

| Grade | Meaning |
|---|---|
| ✓ **Robust** | In the county schedule or the code table. |
| ~ **Range** | Real, but the number is on your plans (foundation plan, truss sheet, energy form), not in a book. Confirm. |
| ⚠ **Contested** | Builders argue about it. Both shown. |
| ◈ **Model** | Simplified for the sim. |
| ✗ **Cartoon** | The common lie. The trap tiles. |

*Block MVP: 2026-09-07 · Sources: Indian River County / City of Vero Beach residential inspection schedule (BRCOM, 2019) and Required Inspections checklist; FBC 8th Edition (2023) Residential, Energy Conservation; NEC 2020.*
