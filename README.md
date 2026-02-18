# ◈ Gravity Assist Trajectory Simulator

An interactive, browser-based simulator that visualizes how spacecraft use planetary gravity assists to travel between planets in our solar system. Built as a single self-contained HTML file — no build tools, no dependencies, no installation required.

**[▶ Try it live here](https://stenjac.github.io/gravity-assist-simulator/)** — or just download `index.html` and double-click it.

<img width="1004" height="610" alt="Screenshot 2026-02-17 at 2 57 01 PM" src="https://github.com/user-attachments/assets/8c30e9d5-564a-4bce-9acd-ffac0ed6667d" />

---

## What is this?

When NASA sends a probe to Jupiter or Saturn, they don't just point it at the planet and fire. They carefully time the launch so the spacecraft can swing past other planets along the way, using each planet's gravity as a free speed boost — like a skateboarder grabbing onto a moving truck.

This simulator lets you experiment with that concept hands-on. You pick a destination, choose your launch parameters, find the right launch window, and watch your rocket trace an orbital path through the solar system.

## The Physics (Explained Simply)

### Why orbits are curved

The Sun's gravity is constantly pulling everything toward it. Earth doesn't fall in because it's moving sideways fast enough — it keeps "missing" the Sun, which is what an orbit is. Your rocket does the same thing. It's always falling toward the Sun, but its sideways speed curves the fall into an ellipse.

### What the trajectory shapes mean

- **Circle** — sideways speed perfectly balances gravity (that's what Earth does)
- **Ellipse (oval)** — the rocket speeds up falling closer to the Sun, slows down climbing away, like a skateboard ramp
- **Open curve** — too much speed, the rocket escapes the solar system entirely

### Why launch timing matters

This is the most important insight the simulator teaches. It's not enough to aim at Mars — Mars has to actually *be there* when your rocket crosses its orbit. If the timing is wrong, the rocket crosses Mars's orbital distance but Mars is on the other side of the Sun.

Real mission planners wait for **launch windows** — specific dates when the angular geometry between Earth and the target planet is just right. For Mars, this window opens roughly every 26 months.

The **phase angle** is what determines this. It's the angle (measured at the Sun) between Earth and the destination planet. Each destination has an ideal phase angle for a minimum-energy transfer:

| Destination | Ideal Phase Angle | Typical Transfer Time | Launch Windows |
|---|---|---|---|
| Mercury | ~109° | ~105 days | Every ~116 days |
| Venus | ~-54° | ~150 days | Every ~584 days |
| Mars | ~44° | ~259 days | Every ~780 days (26 months) |
| Jupiter | ~97° | ~2.7 years | Every ~399 days |
| Saturn | ~106° | ~6.0 years | Every ~378 days |

### How gravity assists work

When a spacecraft flies close to a moving planet, the planet's gravity tugs on it briefly. From the planet's perspective, the spacecraft just swings around and leaves at the same speed it arrived. But relative to the Sun, the spacecraft has gained (or lost) speed because the planet itself is moving.

It's like running alongside a moving train and grabbing a handrail for a second. You didn't gain energy from the train's engine, but you borrowed some of its momentum — and now you're going faster relative to the ground.

NASA's Voyager missions used this trick to visit four planets with barely enough fuel for one.

### Why small angle changes matter so much

Imagine pointing a garden hose at a target 100 feet away. Tilting the nozzle by half a degree barely changes where the water lands at your feet, but shifts the landing spot by several feet at the far end. Same idea — a 5° change at Earth translates to millions of miles of difference by the time the rocket reaches Mars.

## Features

### Controls
- **Destination** — any planet from Mercury to Neptune
- **Boost (Δv)** — percentage of Earth's orbital speed (~29.78 km/s) added at launch
- **Launch Angle** — direction of the boost relative to Earth's position (-180° to 180°)
- **Zoom** — 0.08x to 4x magnification
- **Animation Speed** — 0.01x (slow-motion) to 5x, adjustable mid-flight

### Launch Window Finder
- **Launch Date slider** — scrub through 1,200 days to see planetary positions change
- **Phase angle arc** — visual overlay on the canvas showing the angle between Earth and the target
- **Window quality strip** — color-coded bar showing optimal launch dates at a glance (green = good window, dark = bad timing)
- **Transfer info** — displays ideal phase angle, expected transfer time, and recommended boost for the selected destination

### In-Flight HUD
- **Speed** — current velocity in km/s with a color-coded bar
- **Flight time** — days since launch
- **Distance to target** — in AU, updated in real-time

### Stop Conditions
The simulation tells you exactly why it ended:
- ✓ **ARRIVED** — spacecraft entered the target's sphere of influence
- ✗ **ESCAPED SOLAR SYSTEM** — exceeded 80 AU boundary
- ☀ **CRASHED INTO SUN** — fell below minimum solar distance
- ⏱ **MAX SIM TIME REACHED** — 1.5M calculation steps exhausted

Each stop condition displays a contextual tip for what to adjust.

## Usage

### Option 1: Just open it
```
Download index.html → double-click → it opens in your browser
```
That's it. No server, no terminal, no installs.

### Option 2: GitHub Pages
1. Push this repo to GitHub
2. Go to **Settings → Pages → Source → main branch**
3. Your simulator is live at `https://yourusername.github.io/gravity-assist-simulator/`

### Option 3: Any static file server
```bash
# Python
python3 -m http.server 8000

# Node
npx serve .

# Then visit http://localhost:8000
```

## Quick Start: Reaching Mars

1. Select **Mars** as destination
2. Note the ideal phase angle displayed (~44°)
3. Drag the **Launch Date** slider until the phase angle readout shows ~44° (look for green zones in the strip)
4. Set **Boost** to ~10-12%
5. Set **Launch Angle** to ~0°
6. Hit **▶ LAUNCH**
7. You should arrive in ~260 days

### Quick Start: Reaching Mercury

Mercury is counterintuitive — you need to *slow down* to fall inward:

1. Select **Mercury** as destination
2. Find a launch window with phase angle ~109°
3. Set **Boost** to ~15%
4. Set **Launch Angle** to ~180° (retrograde — firing against Earth's motion)
5. Hit **▶ LAUNCH**

## Technical Details

### Simulation Engine
- **Integration method**: Symplectic Euler (kick-drift) — preserves orbital energy over long timescales
- **Time step**: 0.00008 years (~42 minutes)
- **Max steps**: 1,500,000 (~120 years of simulated time)
- **Boundary**: 80 AU (well past Neptune's orbit at 30 AU)
- **Trail sampling**: Every 15th step stored for rendering

### Physics Model
- **Gravitational constant**: Derived from Kepler's third law: `GM_SUN = 4π² × AU_PX³`, ensuring Earth's orbital speed and the Sun's pull are in balance
- **Planet gravity**: Boosted ~50-100x over real mass ratios so gravity assists produce visually dramatic trajectory bends (this is a teaching tool, not JPL mission software)
- **Orbits**: Circular, coplanar (real orbits are slightly elliptical and tilted)
- **Hohmann transfers**: Phase angles and transfer times calculated from classical orbital mechanics formulas

### What's Simplified
This is an intuition-builder, not a mission planner. Key simplifications:

- All orbits are circular (real orbits are elliptical — Mars's eccentricity of 0.093 matters for real missions)
- All orbits are in the same plane (real orbital inclinations are 1-7°)
- Planet masses are exaggerated for visible gravity assists
- No atmospheric drag, radiation pressure, or relativistic effects
- No multi-body trajectory optimization (real missions use patched conics and numerical optimization)
- Launch is instantaneous (no atmospheric ascent phase)

### Rendering
- HTML5 Canvas 2D with `requestAnimationFrame`
- Real-time animation speed control using `performance.now()` delta timing
- Procedural star field, gradient sun, Saturn rings, trajectory color gradient
- Phase angle arc visualization with Hohmann transfer geometry

## File Structure

```
gravity-assist-simulator/
├── index.html      # The entire simulator (single file, ~500 lines)
├── README.md       # This file
└── LICENSE         # MIT License
```

Yes, the whole thing is one HTML file. No build step, no dependencies, no node_modules folder the size of a black hole.

## Built With

- Vanilla JavaScript
- HTML5 Canvas
- [IBM Plex Mono](https://fonts.google.com/specimen/IBM+Plex+Mono) (loaded from Google Fonts)
- Orbital mechanics textbooks and a lot of trial and error

## License

MIT — do whatever you want with it.

## Acknowledgments

- The core orbital mechanics concepts draw from NASA's [Basics of Space Flight](https://solarsystem.nasa.gov/basics/)
- Phase angle calculations use standard Hohmann transfer formulas from Bate, Mueller & White's *Fundamentals of Astrodynamics*
- Built iteratively with Claude (Anthropic) as a learning project exploring interplanetary trajectory mechanics
