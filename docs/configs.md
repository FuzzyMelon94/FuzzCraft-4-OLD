# FuzzCraft 4 — Config notes

Some notes regarding the configs of various mods as I work through the testing and spot things that might need attention.

### Bosses of Mass Destruction
- No in-game guidebook — boss trigger mechanics are not obvious to new players
- B6 quest pass: BOMD needs dedicated quest coverage explaining how to locate and trigger each boss (locator items, structure hunting, etc.)

### RFTools Dimensions
- No return travel device is placed in the created dimension — players entering a new RFTools dimension have no built-in way back
- B6 quest pass: when the player first crafts a Matter Transmitter, reward them with a charged Porter bound to a Matter Receiver in their base so they always have an escape route

### Almost Unified — Tropicraft Cocktail
- AU tag unification causes JEI to show Pam's HarvestCraft Pina Colada as the output for the Tropicraft cocktail recipe
- Fix: add `tropicraft:cocktail` to the Almost Unified ignored items config so it isn't unified with Pam's drink items
- The portal mechanic works correctly with the crafted item; this is a JEI display issue that would confuse players

### Create Mechanical Extruder
- Balance default recipes
- Add recipes for all the resources Create requires
- Consider adding recipes for other modded resources