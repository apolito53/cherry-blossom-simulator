# Cherry Blossom Simulator

A standalone canvas animation of a procedural cherry tree, falling blossoms, wind gusts, and pointer-driven petal interaction. Open `index.html` directly in a browser; there is no build step.

## Performance Mode

Open the hamburger menu in the upper-left corner and use the `Full mode` / `Light mode` button to trade visual density for smoother performance. The choice is saved in local storage.

Light mode is the default. It lowers the canvas pixel budget, reduces active and settled petals, disables animated fog and tree slice shimmer, refreshes ground caches less often, and caps animation work to roughly 30 FPS.

To force the mode on launch, open `index.html?quality=light` or `index.html?quality=full`.

## Scene Modes

Open the hamburger menu and use the `Sakura scene` / `Fall scene` button to switch the color direction of the tree, particles, sky, hills, mist, and ground. The selected scene is saved in local storage.

To force the mode on launch, open `index.html?scene=sakura` or `index.html?scene=fall`. Scene and performance overrides can be combined, for example `index.html?scene=fall&quality=light`.

## Customizer

Open the hamburger menu in the upper-left corner to tune the scene. It contains the scene/performance toggles plus controls for skybox preset, sky tone, cloud density, and wind strength; changes are saved in local storage.

To force a skybox on launch, open `index.html?skybox=midday`, `index.html?skybox=sunset`, `index.html?skybox=night`, or `index.html?skybox=overcast`.

## Physics Simulation

The simulation is not rigid-body physics. It is an art-directed particle field built from simple forces that combine into believable motion.

Each falling petal carries position, velocity, gravity, terminal velocity, sway, spin, size, opacity, sprite, and depth-layer state. Every animation frame advances those values with simple Euler integration: compute force-like influences, adjust velocity, then move by `velocity * dt`.

The motion comes from several overlapping effects:

- Global wind uses slow sine waves so the whole field breathes instead of drifting linearly.
- Per-petal sway, curve, bob, flutter, and spin make repeated sprites feel individual.
- Gravity pulls petals down, while terminal velocity keeps the fall soft and floating.
- Gusts are temporary circular vortex fields. Petals inside a gust get tangential swirl, uplift, and drift with a soft radial falloff.
- Pointer interaction is another radial force field. Hovering and pressing change the radius, lift, push, orbital force, and drift so the cursor feels like it is stirring the air.

The ground participates in the illusion. A cached terrain curve decides when petals have landed. Some landed petals are converted into ground petals, while the active particle is recycled back near canopy spawn points. That creates visible accumulation without reducing the continuous blossom storm.

The tree is procedural too. Recursive branches generate blossom clusters and spawn points, so petals originate from plausible canopy locations instead of random screen positions. Each page load adds a fresh random tree seed, while resizes reuse that seed so the tree stays stable during the session.
