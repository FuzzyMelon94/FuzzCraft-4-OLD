# FuzzCraft 4 — Batch 6 Testing: Building & Decoration

## Summary
**Pack version:** 0.6.1
**Test date:** <tester fills in>
**Tester:** <tester fills in>
**Play mode:** Single player

## Known Issues
- Supplementaries version tag has a minor inconsistency in the Modrinth version numbering (cosmetic only — correct jar was pulled: 3.6.8).
- Every Compat (Wood Good) and Every Compat (Stone Zone) will significantly expand JEI item count. Use mod-filter or search to navigate. No fix needed — expected behaviour.
- Twigs NeoForge port is very new (v3.1.2, June 2026, ~3K downloads). Watch for crashes or missing textures and report if found.

---

## 1. Launch & Stability

- [ ] Pack launches to main menu with no crash
- [ ] No missing texture spam in log on launch
- [ ] Create new world and load in — no world gen crash
- [ ] Log shows no `ERROR` or `WARN` entries for B6 mods (Macaw's, Chipped, Rechiseled, Supplementaries, etc.)

---

## 2. Regression — Prior Batches

- [ ] Create: place a mechanical press, confirm it operates
- [ ] AE2: open ME Terminal, confirm items display
- [ ] Farmer's Delight: craft a Cutting Board, confirm recipe viewer shows FD recipes
- [ ] Twilight Forest: craft the portal frame, confirm portal activates
- [ ] JEI: open recipe viewer, confirm it loads and search works

---

## 3. Macaw's Suite

- [ ] Open creative menu — Macaw's tabs appear (Furniture, Roofs, Bridges, Windows, Doors, Fences & Walls, Lights & Lamps, Paintings, Trapdoors, Paths & Pavings)
- [ ] Place a Macaw's Furniture item (e.g. a sofa) — no crash, renders correctly
- [ ] Place a Macaw's Roof block — slopes render and connect correctly
- [ ] Place a Macaw's Bridge segment — connects to adjacent segments
- [ ] Place a Macaw's Window — renders, opens/closes if applicable
- [ ] Place a Macaw's Door — opens with right-click
- [ ] Place a Macaw's Fence — connects to adjacent fence and vanilla fence
- [ ] Place a Macaw's Light — emits light, no flicker
- [ ] Place a Macaw's Painting — hangs on wall correctly
- [ ] Place a Macaw's Trapdoor — opens/closes
- [ ] Place a Macaw's Path block — renders correctly underfoot

---

## 4. Let's Do Additions

- [ ] Beachparty: creative tab appears — place a beach chair or cocktail table, confirm render
- [ ] Beachparty: craft a cocktail (or find in creative) — no crash, item exists
- [ ] [Let's Do] Furniture: creative tab appears — place curtains (try a colour or two), confirm they hang correctly
- [ ] [Let's Do] Furniture: place a terrarium or gramophone — renders with no missing model

---

## 5. Block Reskinning (Chipped + Rechiseled)

- [ ] Craft/find a **Carpenter's Workbench** (Chipped) — open GUI, confirm block variants appear for at least one block type (e.g. Stone Bricks)
- [ ] Craft/find a **Chisel** (Rechiseled) — right-click a supported block, confirm variant selection appears
- [ ] Place a Rechiseled: Create block variant — renders correctly with Create's texture set
- [ ] JEI: search "chipped" — large number of variants appears, no crash

---

## 6. Framed Blocks

- [ ] Craft a **Framing Hammer** and a **Framed Block** — place the framed block, use hammer to apply a texture from another block
- [ ] Build a sloped/angled shape using Framed Blocks — renders correctly, no z-fighting
- [ ] Break a Framed Block — drops correctly, no crash

---

## 7. Decoration Mods

### Supplementaries
- [ ] Creative tab appears — place a **Jar** on a surface, confirm it renders
- [ ] Place a **Rope** block — extends downward, climbable
- [ ] Place a **Sign Post** (directional sign) — renders and can be written on
- [ ] Place a **Pedestal** — can hold an item display

### Decorative Blocks Reborn
- [ ] Creative tab appears — place a **Lattice**, a **Rocky Dirt** block, and a **Support Beam** — all render correctly

### Dusty Decorations
- [ ] Creative tab appears — place a **Hanging Fish**, a **Food Barrel**, and a **Buoy** — confirm randomised texture variants appear (place several of the same block, they should look slightly different)
- [ ] Place a **Rope** (Dusty) — confirm it is climbable

### Twigs ⚠️
- [ ] Creative tab appears — no crash loading the tab
- [ ] Place a **Pebble** on the ground — renders as small decoration
- [ ] Place a **Stone Lamp** — emits light, no crash
- [ ] Place a **Bundled Log** — renders correctly
- [ ] Check log for any Twigs-related ERROR entries

### Handcrafted
- [ ] Creative tab appears — place a **Sofa** and a **Chair** — renders with correct model and texture
- [ ] Place a **Bookshelf** variant — renders correctly

### Cluttered
- [ ] Creative tab appears — browse tab, no crash
- [ ] Place a **Kitchen Counter** — renders correctly
- [ ] Place a **Wallpaper** block — applies texture correctly
- [ ] Use **Hand Drill** on a supported block to change variant — confirm GUI opens and applies change

---

## 8. Diagonal Rendering

- [ ] Place vanilla **Oak Fences** in an L-shape — confirm diagonal corner connects visually (Diagonal Fences)
- [ ] Place **Stone Walls** in an L-shape — confirm diagonal visual connection (Diagonal Walls)
- [ ] Place **Glass Panes** in an L-shape — confirm diagonal visual connection (Diagonal Windows)
- [ ] Confirm no visual glitching on straight runs of these blocks

---

## 9. Every Compat (Wood Good + Stone Zone)

- [ ] JEI: search "everycomp" or "every compat" — large number of entries appears, no crash
- [ ] Confirm at least one Macaw's block appears in a modded wood type (e.g. search "acacia" + "macaw" — should find Every Compat variants)
- [ ] Confirm at least one Chipped or Rechiseled variant appears in a modded stone type via Stone Zone

---

## 10. Utility & Display

### Armor Statues
- [ ] Place an **Armor Stand** — right-click with an empty hand to open the Armor Statues GUI
- [ ] Apply a pose and rotate a limb — confirm it saves and persists after leaving/rejoining the area
- [ ] Confirm this works in survival without needing server-side mod (test on a vanilla server or single-player with server auto-hosting)

### Dramatic Doors
- [ ] Find/craft a **Dramatic Door** (tall door) — places as 3-block-tall door
- [ ] Open/close it — animates correctly
- [ ] Confirm you can walk through without dismounting a horse (the selling point!)

### MmmMmmMmmMmm (Target Dummy)
- [ ] Craft/find a **Target Dummy** — place it in the world
- [ ] Hit it with a weapon — damage numbers display above it
- [ ] Equip it with armour pieces — armour applies, damage numbers reflect the mitigation
- [ ] Break it — drops correctly, no crash

---

## 11. Deferred — Requires Server / Multiplayer

- Verify Every Compat Wood + Stone don't cause TPS issues with large builds (many variant blocks in view)
- Verify Framed Blocks performance — complex framed builds with many texture lookups
- Verify Diagonal block visuals are consistent between clients on the same server
- Armor Statues: confirm poses set by one player are visible to others correctly

---

## Tester Notes

<!-- Free-form: crashes, surprises, visual issues, mods that feel wrong, anything worth feeding back -->
