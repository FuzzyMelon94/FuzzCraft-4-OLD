---
name: project-mechanical-extruder-recipes
description: Mechanical Extruder recipe pass flagged for end-of-pack QoL/config work
metadata:
  type: project
---

Create: Mechanical Extruder recipes need a dedicated pass during the final QoL/config phase.

**Why:** The Extruder is recipe-driven and ships with only basic defaults (water+lava=stone, etc.). There's good opportunity to add compat recipes for other mods in the pack — e.g. renewable ore generation for IE/Thermal/AE2 materials, Silent Gear gem outputs, etc.

**How to apply:** Don't touch Extruder recipes during batch implementation. Flag a dedicated config/recipe pass task at the start of Batch 5 (Building & Questing), when the full mod roster is known and KubeJS is likely in the pack for scripting.
