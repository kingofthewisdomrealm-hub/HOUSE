# HOUSE — Block (CBS) build plan

**Goal:** the most visual working model of a Treasure Coast concrete-block house that still tells the truth — and that a new hire can *play* until the order is in his hands.

Not twelve cards in a row. A **Periodic Table of House Parts** as the data, a **ring** of tiles around a **living house** you build by dragging parts onto it, and **ten inspectors** who each see the house once. Order is not a line. It is a set of gates with work between them, and the house looks identical from the street whether you did it right or not.

This is the plan for app 1 (Block). Frame, Elevated and Addition reuse the same shell.

Sister projects, same DNA:

- **ROOF** — same shell, same ring, same inspector figure. The whole ROOF Shingle game is one tile here (*Dr — Dry in the roof*) plus one more (*Rc — Roof covering*). Decided 6 Sep: **the roof is three tiles in the house ring (trusses, sheathing, dry-in), and the tile links out to ROOF.**
- **BODY** — dark stage, honest imaging, evidence grades.
- **Periodic Table of Frameworks** (RULEROFWISDOM `/forum`) — the tray grammar. *Data not code paths.*

---

## 1. What "accurate" means here

Three views of the same house. The user can switch instantly.

| Mode | What it shows | What it must not fake |
|---|---|---|
| **Cutaway** | The house cut down the middle: ground, shell, systems, skin. Every layer you placed is visible — pipes under the slab, steel in the cells, straps on the trusses, the line set in the wall. | A house that is one flat color per step. Drywall that hides nothing. |
| **Street** | The front of the same house: slab, block, roof, stucco, windows, the condenser, the sod. Everything that holds it together is invisible. | A "finished" glow. A toe-nailed roof and a strapped roof **look identical** from the street — the view says so. |
| **Inspector** | Only what the open gate checks, lit. Everything else dimmed. | Inspecting things the inspector cannot see anymore (straps after the drywall). |

The killer honesty: **a wrong house looks like a right house.** The only people who ever know are the ten inspectors, and the owner in the first named storm. That is why the game refuses to let you cover anything before its gate.

Sources: Indian River County / City of Vero Beach Building Division **residential inspection scheduling sheet** (BRCOM, 2019 — the priority order) and **BRCOM Required Inspections checklist** (the notes: "check for plans, permit, NOC and sub contractor affidavits", "entire suction line must be insulated", "vertical vents through roof per code", "check structure layout with plans"); FBC 8th Edition (2023) Residential and Energy Conservation; NEC 2020 as adopted.

---

## 2. Product: one HTML app

Single page, no login, GitHub Pages, like ROOF and BODY.

```
index.html                 ← series hub (Block live; Frame / Elevated / Addition "soon")
apps/cbs/index.html        ← the app (MVP is one self-contained file, no dependencies)
```

Rule carried over: **if you write `if (part.id === 'block')` the engine is dead.** Hue lives on the family. Order lives on `needs`. What a gate checks lives on the gate (`lit`, `failsIf`). What a part draws lives on `layer`.

---

## 3. Visual architecture

### 3.0 The ring (the ROOF rules, kept)

1. **The table is the DATA, the screen is a RING.** 29 house parts on one ellipse around the house, clockwise by `z` from 12 o'clock; the ten gate rows drawn as arcs (grey → gold when open → green PASS → red FAIL). Ready tiles wear a gold ring. The card is a peek anchored to the tile. The table is one click away, read-only. **No scroll at 1440×900, 1024×700, 390×780** (verified 7 Sep).
   *New in HOUSE:* tiles are spaced by **arc length**, not by angle — 29 tiles on a phone's tall ellipse crowd the flat top otherwise. Same clockwise order.
2. **Paper is a SHELF above the house.** Permit + ten inspections in inspection order. *New in HOUSE:* eleven tiles do not fit one row on a laptop, so the shelf **wraps** — one row at 1440, two at 1024, three on a phone — and the house box shrinks to make room. Still above the house, still in order, left to right, top to bottom.
3. **Pictures, not letters, for paper.** Inspector with the magnifying glass, gate number in the lens (1–10). Permit = document with the red stamp; placed, it becomes a sign on a post in the front yard.

### 3.1 The table (the data)

| Family | Symbol | The question | Block |
|---|---|---|---|
| Paper | Pp | Is it legal, and who signed? | 1 |
| Ground | Gd | What is it standing on? | 2 |
| Concrete | Cn | What carries the load? | 2 |
| Frame | Fr | What is the wind holding onto? | 2 |
| Roof | Rf | What keeps the rain out? | 2 |
| Pipe | Pi | Where does water come in and go out? | 3 |
| Wire | Wi | Where does the power go? | 3 |
| Air | Ai | What cools it, and where does the water drip? | 3 |
| Warm | Wm | What keeps the heat out? | 4 |
| Cover | Cv | What does the owner see? | 4 |

Gutters: Paper | the Shell (Ground, Concrete, Frame, Roof) | the Systems (Pipe, Wire, Air) | the Skin (Warm, Cover).

| Row (gate) | County code | Label | What the inspector must see |
|---|---|---|---|
| 1 | 301 | Underground | Every pipe under the slab, open, capped, holding a test. |
| 2 | 503 | Slab | Steel on chairs, poly, forms — and the formboard survey and density report already approved. |
| 3 | 119 | Tie beam | Steel in the forms, steel in the cells, a strap wherever a truss will land. |
| 4 | 123 · 126 · 118 | Sheathing & straps | Every truss strapped, braced, nailed down — before anything covers it. |
| 5 | 603 | Dry-in | A roof that survives tonight's rain with nothing on top. |
| 6 | 203 · 311 · 403 | Roughs | Pipe, wire and duct in the open walls — and an insulated suction line. |
| 7 | 124 | Framing | Layout matches the plans. Furring, blocking, holes and notches within limits. |
| 8 | 510 | Insulation | The R-value on the energy form, in the wall, before the drywall. |
| 9 | 135 (+193) | Drywall | Screws at the spacing, bare, before tape. Shutters n/a with impact glazing. |
| 10 | 999 | Final | Every trade final, the blower door, the certificates — then the CO. |

The rows are the county's own **priority order** from the scheduling sheet (priorities 1–5, 7–11; there is no priority 6 on the sheet). Where the county groups three inspections under one priority (4: sheathing, strapping, bracing; 7: the three roughs) the game does too — one gate, three codes on the card.

### 3.2 The house (center)

**Section**, cut through the middle: ground at y=440, slab 150–650, block walls cut at each end, a far wall with a window and a door, tie beam, one truss with webs and bracing, ridge at (400,58). A face-on interior partition (the hallway wall) so the roughs have somewhere to live. Outside: permit sign left, condenser right, sewer tie-in under the right footing.

Each placed part draws a real layer (§5 has the full list). The trap tiles draw too — toe-nails instead of wrapped straps, bare copper instead of wrapped copper — and from the street, nothing.

**Front** (street view): the eave side of the same house. Slab edge, block face with openings, beam band, a hip-view roof plane that goes plywood → grey-blue → shingles, stucco over all of it, windows and door, meter, condenser, sod, driveway, the address numbers.

Wrong drop = a **leak**: blue drips, the tile shakes back, the card says why in the inspector's words. Score = leaks + failed gates. Three stars at zero.

### 3.3 The card

Same as ROOF: symbol, name, family · gate (and the county code on gate tiles); **Law** (one sentence); **Spec** (the numbers, or *on your plans*); **Fails when** (the inspector's reason); **Grade + source**. The two roof tiles carry a link to ROOF Shingle (`↗` on the tile).

---

## 4. The engine

Unchanged from ROOF except the count: a partial order, **ten** gates, **two** traps.

```
parts[]   {id, z, sym, name, short, fam, row, needs[], altOf?, trap?, gate?, failsIf?, lit?, layer, law, spec, fail, grade, src, link?}
gates     are parts with gate:n — placed like any other part, because calling the inspection IS a step
state     placed:Set, burned:Set, passed:Set, failedRows:Set, leaks, fails, view
```

- A part can be placed when every id in `needs` is placed (`a|b` = either).
- Placing a part whose needs are not met is a **leak**. It does not land.
- A gate runs `failsIf`: a trap present → FAIL, the trap comes out and is burned (✗); else PASS opens the next arc.
- `altOf` pairs complements (straps ↔ toe-nail; wrapped ↔ bare line set): place one and the other greys out.
- Rows are not locked as a whole — real crews run parallel. Windows, partitions and the roof covering can go on early; the gate is what is strict.

Critical truths cartoons get wrong, and we will not:

1. **The paper gates the concrete.** The county will not book the slab inspection until the formboard survey and the density report are approved. So the survey and the report live on the *Forms & footings* tile, and the slab gate's card says why.
2. **Pour after the stamp.** Slab and beam each have a separate *pour* tile that needs its inspection. That is the whole lesson in two tiles.
3. **The straps go in before the pour.** In a CBS house the hurricane straps are cast into the tie beam. Forgetting them is a drill-and-epoxy retrofit plus an engineer's letter — so straps are on the tie-beam steel tile, and *wrapping* them is the row-4 tile the trap replaces.
4. **Right and wrong look the same.** Toe-nailed trusses and a bare line set both land, both vanish under drywall and stucco, both fail their gate. From the street, the same house.
5. **The county's order, not ours.** Ten priorities, in their sequence.

---

## 5. The catalog — 40 tiles (MVP)

`z` = first possible placement. Gates in bold. Ring tiles are everything not in Paper.

| z | Sym | Part | Fam | Gate | Needs | Draws | Grade |
|---|---|---|---|---|---|---|---|
| 1 | Pm | Pull the permit | Pp | 1 | — | permit sign | ✓ |
| 2 | Fp | Layout, forms and footings (survey, fill, density report) | Gd | 1 | Pm | trench, fill, steel, forms, stakes | ✓ |
| 3 | Up | Underground plumbing | Pi | 1 | Fp | pipes under the slab, capped | ✓ |
| 4 | **I1** | **Underground plumbing inspection (301)** | Pp | 1 | Up | inspector at the trench | ✓ |
| 5 | Tv | Termite treatment and vapor barrier | Gd | 2 | I1 | blue poly, green dots | ✓ |
| 6 | St | Slab steel | Cn | 2 | Tv | mesh on chairs | ~ |
| 7 | **I2** | **Slab inspection (503)** | Pp | 2 | St | inspector on the forms | ✓ |
| 8 | Po | Pour the slab | Cn | 3 | I2 | the slab | ✓ |
| 9 | Bk | Lay the block, lintels and sills | Cn | 3 | Po | walls, far wall, openings, cell steel | ✓ |
| 10 | Tb | Tie beam forms, steel and straps | Cn | 3 | Bk | beam forms, bars, straps standing | ~ |
| 11 | **I3** | **Tie beam inspection (119)** | Pp | 3 | Tb | inspector on the wall | ✓ |
| 12 | Pb | Pour the beam and fill the cells | Cn | 4 | I3 | solid beam, grouted cells | ✓ |
| 13 | Tr | Set and brace the trusses | Fr | 4 | Pb | truss, webs, bracing | ✓ |
| 14 | Sp | Wrap the straps over every truss | Fr | 4 | Tr | gold straps, nails | ✓ |
| 14 | Sp | Toe-nail the trusses — **trap** | Fr | 4 | Tr | three slanted nails | ✗ |
| 15 | Sh | Roof sheathing, nailed | Fr | 4 | Sp | plywood line | ~ |
| 16 | **I4** | **Sheathing, strapping, bracing (123 · 126 · 118)** — fails if toe-nailed | Pp | 4 | Sh | inspector in the attic | ✓ |
| 17 | Dr | Dry in the roof → *ROOF Shingle* | Rf | 5 | I4 | underlayment, drip edge | ✓ |
| 18 | **I5** | **Roof dry-in (603)** | Pp | 5 | Dr | inspector on the roof | ✓ |
| 19 | Pt | Interior partitions | Fr | 6 | Pb | the hallway wall, studs | ✓ |
| 19 | Wd | Bucks, impact windows and doors | Cv | 6 | Pb | bucks, glass, door | ✓ |
| 20 | To | Plumbing top-out | Pi | 6 | Pt, I5 | vent through the roof, supply | ✓ |
| 20 | Er | Electrical rough | Wi | 6 | Pt, I5 | panel can, cable, boxes | ✓ |
| 20 | Ar | A/C rough, suction line insulated | Ai | 6 | Pt, I5 | air handler, ducts, wrapped line set | ✓ |
| 20 | Ar | A/C rough, line set bare — **trap** | Ai | 6 | Pt, I5 | bare copper | ✗ |
| 21 | **I6** | **Roughs (203 · 311 · 403)** — fails if bare | Pp | 6 | To, Er, Ar | inspector inside | ✓ |
| 22 | Fb | Furring, fire blocking, draft stops | Fr | 7 | I6 | furring strips, blocking | ✓ |
| 23 | **I7** | **Framing (124)** | Pp | 7 | Fb | inspector inside | ✓ |
| 24 | Wn | Wall insulation | Wm | 8 | I7 | foil board | ~ |
| 25 | **I8** | **Insulation (510)** | Pp | 8 | Wn | inspector inside | ✓ |
| 26 | Dw | Hang the drywall | Cv | 9 | I8 | board, bare screws | ~ |
| 27 | **I9** | **Drywall (135)** | Pp | 9 | Dw | inspector inside | ✓ |
| 28 | At | Attic insulation (511) | Wm | 10 | I9 | pink band on the ceiling | ~ |
| 28 | Fx | Fixtures, water heater, sewer tie-in (303/313) | Pi | 10 | I9 | toilet, heater, cleanout | ✓ |
| 28 | Dv | Panel, devices and power (211) | Wi | 10 | I9 | panel cover, meter | ✓ |
| 28 | Eq | Set the condenser and air handler | Ai | 10 | I9, Dv | condenser on its pad | ✓ |
| 28 | Rc | Roof covering (609) → *ROOF Shingle* | Rf | 10 | I5 | shingles, ridge | ✓ |
| 29 | Fn | Stucco, paint, floors, cabinets (136 lath) | Cv | 10 | Dw, Wd | stucco, tile, cabinets, paint | ◈ |
| 29 | Gr | Final grade, driveway, address | Gd | 10 | I9 | sod, driveway | ✓ |
| 30 | **Fn** | **Final (999)** | Pp | 10 | At, Fx, Dv, Eq, Rc, Fn, Gr | inspector in the driveway | ✓ |

Facts on the cards, by source:

- **County scheduling sheet (2019):** the priority order; "Formboards, Stem Wall Surveys, Density (compaction) reports be submitted, reviewed, and approved before a slab inspection is allowed." ✓
- **County BRCOM checklist:** 102 Footing "check for plans, permit, NOC and sub contractor affidavits"; 152 Sheathing "check reviewed plan for fastening and sheathing size"; 311 Top-out "vertical vents through roof per code"; 403 A/C rough "entire suction line must be insulated"; 124 Framing "check structure layout with plans"; 136 Metal lath; 211 Temp-perm power; 303/313 sewer/septic; 511 attic insulation; 609 roof covering. ✓
- **FBC Residential 8th Ed.:** R318 termite, R506 slab and 6-mil vapor retarder, R403 footings, R606 masonry, R802.11 uplift, R803 sheathing, R302.11 fire blocking, R317 PT plate on concrete, R301.2.1.2 wind-borne debris, R401.3 grade, R319 address. ✓ / ~ where the number is on the plans.
- **FBC Energy Conservation:** R401.3 certificate at the panel; R402.4.1.2 blower door ≤ 7 ACH50. ✓
- **The plans:** foundation steel, tie-beam bars, strap type, sheathing nail spacing, R-values (Form R405), drywall fastener schedule — all graded ~ *on your plans*.

---

## 6. Evidence grades

| Grade | Meaning |
|---|---|
| ✓ **Robust** | In the county schedule or the code table. Build the game on it. |
| ~ **Range** | Real, but the number is on your plans (foundation plan, truss sheet, energy form). Card says *confirm*. |
| ⚠ **Contested** | Builders argue about it. Show both. |
| ◈ **Model** | Simplification for the sim (one truss, one partition, one window). |
| ✗ **Cartoon** | Common lie. The trap tiles. We let you place it, then the gate refuses it. |

---

## 7. Decided: the basic model stays simple

**7 Sep, Josias: "these things should go on an advanced model."** Right. The six open questions were all *"which way does Covenant do it"* — and the answer for the beginner level is **don't ask, don't fork, teach one clean path.** A man learning the order of a house should not be choosing between two foundations on card 2.

So the basic Block model is **closed**, and it teaches one house:

| Question | The basic model teaches | Grade |
|---|---|---|
| Foundation | **Monolithic** — footing and slab in one pour, thickened edge | ◈ Model — one of two real ways |
| Air handler | **Attic** | ◈ Model |
| Wall insulation | **Foil board between PT furring** on the block | ◈ Model |
| Interior studs | **Wood**, PT bottom plate on the slab | ◈ Model |
| Traps | **Two** — toe-nailed trusses, bare suction line | — |
| ROOF link | **Closed.** Relative path works because the repos are named `ROOF` and `HOUSE`; verified live | ✓ |

Those five cards carry a **◈ Model** grade now instead of a **~ confirm** — an honest change. *~ confirm* meant "go find the number." *◈ Model* means "this is one real way, simplified on purpose; the other ways are in Advanced." Nothing pretends to be the only way, and nothing sends a new hire off to read plans he does not have yet.

**Everything that was a fork moves to §10.**

---

## 8. The 3D level (`apps/cbs3d/`) — added 7 Sep 2026

Josias: *"make it a 3d model"* → **real 3D you can spin**, **added alongside the flat one** (both live; the flat one is the fallback for a phone that will not run WebGL).

Same data, same engine, same ring, same ten gates. **Only the middle of the screen changed.** The SVG section/elevation is replaced by a three.js scene (r134 UMD from cdnjs, the one external file; hand-rolled orbit, no OrbitControls dependency).

- **One unit = one foot.** House 40 × 28, walls 8.5 ft of block, 1.5 ft tie beam, 4:12 gable, 2 ft overhangs. ~1,370 meshes.
- **Every part still owns a `layer`**; the builder makes all layer groups once at load and `redraw()` only flips `.visible`. Adding a part is still a data row plus one builder line — never a code path.
- **Cutaway is a real clipping plane** at z = 0: it slices the whole building in half, so you see the wall sandwich — block, furring, foil board, drywall — in section, which the flat version could only imply. Site objects (ground, driveway, condenser, meter, the inspectors) carry no clipping plane, so the yard stays whole.
- **Street** turns clipping off. **Inspector** drops every layer the open gate does not check to 7 % opacity and puts a warm emissive on the ones it does.
- **The inspectors are in the model**, standing where they checked, each under a gold numbered badge. The dry-in man stands on the shingles.
- **Leaks are 3D**: the drop point is raycast onto a plane through the house and blue drops fall from it.
- **Openings are real holes.** One `segs()` function splits a wall into the rectangles an opening leaves, and every shell — block, furring, insulation, drywall, stucco — is built from the same hole list at a different inset. That is why the section reads correctly at a window.
- **Textures are drawn in a canvas at load** (block coursing, stucco, shingles, plywood, board, foil, sod, soil) and each mesh gets a texture repeat matched to its real size, so a 40-ft wall shows 30 blocks, not one stretched one.
- **Wall-layer thicknesses are exaggerated** (furring, insulation and drywall read at ~1.5 in instead of ~0.5–0.75 in) so the sandwich is legible at building scale. Grade ◈ Model.
- Falls back to a link to the flat version if `window.THREE` never arrives.

Geometry the first render caught and the second fixed, worth remembering for Frame: roof planes and truss top chords tilt by **+s·pitch**, not −s·pitch; truss webs must be placed by **endpoints** (`strut(x, z1,y1, z2,y2)`), never by a guessed rotation; the stucco shell must sit *outside* the block's outer face (inset −0.475, not −0.14); and a soffit hangs **below** the truss tails, with a frieze board closing the eave — otherwise tails and hurricane straps poke through a "finished" house.

### 8.1 Reverse (added 7 Sep, both levels)

Josias: *"have a reverse button, it reverses the last step."* A **Reverse** button sits left of *Start over*; **Ctrl+Z / Cmd+Z** does the same. Press it repeatedly to walk the whole house back down to bare dirt.

- Every action that **changes the house** pushes one snapshot (`placed`, `passed`, `burned`, `failedRows`, `leaks`, `fails`) onto a stack before it runs. Reverse pops and restores.
- A **leak is not a step** — a refused drop changes nothing, so it never enters the stack and Reverse never "undoes" something invisible.
- Reversing a **passed gate** un-stamps it. Reversing a **failed gate** un-burns the trap and puts the tile back on the house, with the fail count returned. The stamps panel is rebuilt from state, never patched.
- The button disables itself when the stack is empty; *Start over* clears the stack.
- **The cards still tell the truth.** Reversing a gate says so out loud: *"In the field a stamp is a stamp."* Reversing a part: *"On a real job that step is a demo crew and a change order."* The button is a training convenience, not a claim about the job.

### 8.2 The cards speak in the imperative (7 Sep)

Josias: *"word them as instructions, instead of events… Pull the permit — this is the first thing you do, you go to the building dept, you get…"*

All 40 cards rewritten. The **Spec** block is now headed **What you do** and every one of them is second person, present tense, marching orders: *"You call the surveyor and he sets your corners. You fill and compact the pad in lifts, and you send the density report to the county."* Gate cards are instructions too — *"You call in a 503 — Slab, and you call it before you order concrete"* — so the act of calling the inspection reads as the step it is.

**Fails when** stayed a warning, but moved to second person as well: *"Order the truck for 7 and the inspector for 9 and you pay standing time while everybody watches."*

Rules for anyone writing new tiles (Frame, Elevated, Addition):

- **Law** stays an aphorism — it is the thing you repeat on the ladder, not an instruction.
- **What you do** starts with a verb aimed at the reader. No noun-phrase inventories ("Beam forms set on top of the wall"), no passive voice. Say who does it: *you* set it, *he* checks it, *the surveyor* sets the corners.
- **Every number survives the rewrite.** 6 in. o.c., two #5 continuous, 1/4 in. per foot, 7 ACH50, R405. Instruction voice is a change of grammar, not of content.
- **Straight apostrophes are forbidden in card text** — the strings are single-quoted JavaScript. Use a curly ’. The rewrite script enforces this; so should you.

### 8.3 The deck, the card faces, and Covenant branding (7 Sep)

Josias: *"instead of the tiles surrounding the house, collapse them into a convenient place, like cards in a deck, and pull them out sequentially… make each card represent their step by how it looks… SAY how many cards there are and how many steps… have an option to see them all at once surrounding the house… make the number and the STEP big enough to see at first glance."* And: *"put covenant builders branding on the model."*

**Two layouts, one engine.** `state.mode` is `deck` (default) or `ring`.

- **Deck** — all 40 cards in one stack in the top-left, in `z` order, drawn one at a time. The top card is big (186×250) and is the drag source. `◀ ▶` (or the arrow keys) walk the deck; after every placement `deckSeek()` jumps to the lowest-`z` card that is actually ready. A stack of card edges sits behind it so it reads as a deck. The house gets the rest of the screen — roughly **2.4× the area** the ring left it.
- **Ring** — the old layout, unchanged, one button away: *See all 40 around the house*. That button lives in the corner row, **not** in the deck panel, because the panel is hidden in ring mode.
- **The count is stated, not implied:** `Card 9 of 40 · Step 3 of 10`, plus `21 left in the deck`, plus a row of **ten pips** — one per gate, grey / gold (open) / green (pass) / red (fail).

**The card face** (same markup small on the ring and big in the deck, `cardFace(p, big)`):

- the **`z` number** huge in the top-left (40px on the big card, 13px on a ring tile)
- the **step** in the top-right — `Step 3` over `Tie beam`
- **a picture of the step**, not a letter. `ART` is a table of ~30 inline-SVG glyphs keyed off **`p.layer`** — the field the 3D scene already uses — so a new tile still needs no code path, only a layer name and a glyph. Gate cards keep the numbered inspector, the permit keeps its stamped document.
- the name, and the family question underneath.

**Covenant Builders branding.** Lockup in the corner: the crown traced from `covenantbuilders.org/images/logo.png` as an SVG path (`M11,116 L2,55 L45,66 L73,3 L101,66 L145,55 L136,116 Z`, stroke 13, no fill, verified against the pixels at five heights), flanked by rules, over `COVENANT BUILDERS` / `WE DELIVER`. **Colours come from his site repo, not from sampling the PNG** — navy `#12182B`, sand `#c4a574`, wordmark `#e9e7e2`, the same tokens ROOF ships. (Sampling the logo gives `#af9d80`/`#e9e9e9`; close, wrong, and it made HOUSE disagree with ROOF for about an hour.) The functional gold `#d4a24c` is deliberately kept for *state* (ready, open gate, action) so brand and signal do not fight. Footer carries CBC1253676, (772) 473-7115 and the service area. **And the model itself carries a job sign**: in the 3D level the permit tile now plants a Covenant yard sign — crown, wordmark, licence and phone drawn into a 640×400 CanvasTexture, text auto-fitted to the board, posts set behind the face.

Traps worth remembering: an old phone media query hid `.tile .nm`, which silently blanked the *name* on the big deck card too; and the step **name** collides with the number at phone card size, so narrow shows `Step 4` alone.

## 10. HOUSE Block · Advanced — the level that forks

**BUILT — 8 Sep 2026 — `apps/adv/index.html`.** Everything the basic model refuses to fork on lives here, and the difference between the two levels is the whole point: **the basic model teaches the ORDER. Advanced teaches the JUDGEMENT.**

### What shipped

| | Block | Block · Advanced |
|---|---|---|
| Decisions | none | **5** — foundation, roof covering, air handler, studs, insulation |
| Gates | 10 | **10 or 12**, depending on the foundation |
| Cards | 40 | **42–52**, depending on every choice |
| Traps | 2 | **8** — 4 of them only exist on a road you chose |
| Score | gates, leaks, failed gates | **+ days and dollars, including rework** |

**How the fork is built — data, not code paths.** No row and no card carries a hard number any more. Each carries a `seq` (where it falls in the job) and an optional `only:['tag']`. Choosing an option switches its tag on; `rebuild()` filters both lists by the live tags, sorts by `seq`, and *then* hands out the numbers 1..N. So "pick a stem wall and every step after it renumbers" is not a feature anyone wrote — it is what happens when the numbers are given out after the filter instead of before it. `needs` gained one form, `'?choiceId'`, which means *this decision has to be made first* — that is what stops a man ordering trusses before he has decided what is going on top.

**Measured, both roads played to a Certificate of Occupancy:**

- Monolithic · shingle · closet air handler · wood studs · spray foam → 10 gates, 42 cards, **day 142, $377,700**, no rework.
- Stem wall · tile · attic air handler · steel studs · foil board → 12 gates, 52 cards, **day 179, $469,400**.

**The days and dollars are ◈ Model** — Treasure Coast ballparks for a 40×28 CBS house, in the file so the trade-offs have a size. They are not a bid. Replace them with Covenant's real numbers and the level becomes an estimating trainer as well as a sequencing one.

### The one thing still open

Advanced now *shows* what a stem wall costs. It does not yet say **when a Covenant lot gets one.** That rule is Josias's, not a book's — flood elevation, a lot that falls, a slab that has to sit above a road. Until he writes it, the foundation card presents both roads evenhandedly and lets the player find out the hard way.

### The original spec follows


A man who finishes Block knows what comes after what. He still does not know why this lot got a stem wall and that one did not. That is Advanced.

### What Advanced adds

**1. The foundation fork — the headline.** Card 2 becomes a choice, not an instruction. Two cards sit side by side and the man picks:

- **Monolithic** — footing and slab in one pour. Flat, dry, well-drained lot. Stays at ten gates.
- **Stem wall** — pour the footing, lay block on it to get up out of the dirt, fill and compact inside, then pour the slab on top. For a lot with fall to it, or one that has to come up to grade. **The county inspects this as two more steps: 102 Footing and 137 Stem Wall.** Picking it grows the game to **twelve gates**, and every step after renumbers.

That renumbering is the lesson. A man watches the whole inspection schedule change because of one decision made on day one — which is exactly what happens on a real job, and exactly what nobody tells him.

Each card carries the **lot conditions** that make it the right answer, so the choice is judged, not guessed. The game does not fail you for picking either one; it fails you for picking one and then building the other one's sequence.

**2. Variant cards, not fixed ones.** Air handler (attic / garage / closet), wall insulation (foil board between furring / spray foam / furring-less), interior studs (wood / metal track). Each is a small fork with its own downstream consequence — the metal-track card kills the pressure-treated-plate instruction, the garage air handler moves the line set and the drain, spray foam changes what gate 8 is looking at.

**3. More traps, and meaner ones.** Basic has two. Advanced should carry six-plus, including the two candidates already written:

- **A vent stack that dead-ends in the attic** — fails top-out. County checklist: *vertical vents through roof per code*.
- **Mesh laid flat on the poly with no chairs** — fails the slab. Steel on the ground does nothing.

And the trap that only Advanced can hold: **the right work in the wrong sequence.** Not a bad part — a good part, placed in an order that makes a later inspection impossible.

**4. A scored run.** Basic counts leaks and failed gates. Advanced should count **days and dollars**: a failed inspection is a re-inspection fee and a crew standing around, and the score should say so in money, because that is the number a superintendent actually feels.

### What Advanced must NOT do

- It must not be the first thing a new hire opens. The hub orders them: **Block → Block 3D → Advanced.**
- It must not replace the basic model. Two levels, one engine, same catalog underneath.
- It must not turn a fork into a trap. Picking stem wall is not wrong. Picking stem wall and then calling the slab inspection before the stem wall inspection is wrong.

### What it needs from Josias before it can be built

Only one thing, and it is not a code question: **when does a Covenant lot get a stem wall instead of a monolithic slab?** One or two sentences of his own rule — fall across the lot, fill depth, flood elevation, whatever he actually uses to decide — goes on the fork card as the judgement being taught. Everything else in §10 can be built from the code and the county schedule.

---

## 9. Series

1. **Block** — this plan. Built 7 Sep 2026: flat + 3D, deck layout, Covenant branded.
2. **Block · Advanced** — §10. The forks, the variants, the meaner traps, a score in days and dollars.
3. Frame — stick walls on the slab: sheathing, wrap, the nailing schedule, the strap-at-every-stud detail.
4. Elevated — stem wall and pilings; the flood-zone house; the FEMA elevation certificate as a Paper tile.
5. Addition — tying new to old: the dowel, the beam, the roof that has to meet. The remodel funnel.

Later: manager mode replay; Spanish strings (all card text is data); email gate → CRM lead; a *superintendent* mode where the ring is scrambled and you sort it.

---

*Plan written 2026-09-07; 3D level added the same day. County facts from the Indian River County / City of Vero Beach residential inspection scheduling sheet and BRCOM Required Inspections checklist; code references FBC 8th Edition (2023). A training model, not a permit.*
