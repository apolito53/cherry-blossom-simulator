# Cherry Blossom Simulator

A standalone canvas animation of a procedural cherry tree, falling blossoms, wind gusts, and pointer-driven petal interaction. Open `index.html` directly in a browser; there is no build step.

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

The tree is procedural too. Recursive branches generate blossom clusters and spawn points, so petals originate from plausible canopy locations instead of random screen positions.

