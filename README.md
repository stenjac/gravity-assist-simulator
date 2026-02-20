# ◈ Gravity Assist Trajectory Simulator

An interactive, browser-based simulator that visualizes how spacecraft use planetary gravity assists to travel between planets in our solar system. Built as a single self-contained HTML file — no build tools, no dependencies, no installation required.

**[▶ Try it live here](https://stenjac.github.io/gravity-assist-simulator/)** — or just download `index.html` and double-click it.

<img width="1372" height="631" alt="Screenshot 2026-02-20 at 9 25 40 AM" src="https://github.com/user-attachments/assets/89f60a64-a840-4dbd-b1a9-dc8941f4277a" />

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

### How often is gravity assist actually used?

It depends on the destination. For short trips to Mars or Venus, most missions skip it entirely — a direct Hohmann transfer gets you there with manageable fuel costs, and adding a gravity assist would mean a longer, more complex route. Mars Perseverance, Curiosity, InSight, and most Mars orbiters all took direct shots. It's like driving across town: you don't need to draft behind a semi truck to save gas.

For anything past Mars, it's a different story. The fuel math gets brutal for outer planets. A direct shot to Jupiter requires about 9 km/s of delta-v; a Venus-Earth gravity assist path gets you there for about 6 km/s. That 3 km/s difference translates to exponentially more fuel thanks to the tyranny of the rocket equation — saving a little velocity at the top means dramatically less fuel at the bottom.

Notable real missions and their assist chains:

| Mission | Destination | Gravity Assists |
|---|---|---|
| Voyager 1 | Interstellar | Jupiter → Saturn |
| Voyager 2 | Interstellar | Jupiter → Saturn → Uranus → Neptune |
| Cassini | Saturn | Venus → Venus → Earth → Jupiter |
| Galileo | Jupiter | Venus → Earth → Earth |
| New Horizons | Pluto | Jupiter |
| Messenger | Mercury | Earth → Venus → Venus → Mercury → Mercury → Mercury |
| BepiColombo | Mercury | Earth → Venus → Venus → Mercury → Mercury → Mercury → Mercury → Mercury → Mercury |

**See these trajectories visualized:**

- 🪐 **Voyager 2 Grand Tour** — [NASA Scientific Visualization Studio](https://svs.gsfc.nasa.gov/4140/) has a full animated visualization of Voyager 2's trajectory from Earth through Neptune and beyond, showing each gravity assist bending the path. Also see [The Planetary Society's detailed breakdown](https://www.planetary.org/articles/20130926-gravity-assist) with vector diagrams showing how speed changes at each flyby, plus a chart of Voyager 2's velocity vs. distance proving it was below solar escape velocity until Jupiter's assist boosted it past the threshold.

- 🪐 **Cassini's VVEJGA trajectory** — [NASA's Cassini trajectory page](https://science.nasa.gov/resource/cassini-trajectory/) shows the full Venus-Venus-Earth-Jupiter-Saturn path diagram. The [VVEJGA Trajectory Lithograph (PDF)](https://solarsystem.nasa.gov/system/downloadable_items/1946_trajectory.pdf) is a beautifully illustrated one-page explainer of how each flyby added velocity. Also see the [interactive Cassini flight path](https://www.theplanetstoday.com/cassini_flight_path.html) showing the spacecraft's real position over time.

- 🪐 **MESSENGER's reverse slingshots to Mercury** — [Johns Hopkins APL mission design page](https://messenger.jhuapl.edu/About/Mission-Design.html) has an interactive trajectory viewer where you can highlight each leg of the journey. NASA's [15th anniversary retrospective](https://www.nasa.gov/history/15-years-ago-messenger-launched-to-orbit-mercury/) includes the full trajectory diagram showing all six gravity assists. The [interactive flight path animation](https://www.theplanetstoday.com/messenger_flight_path.html) lets you scrub through the entire mission timeline.

- 🪐 **NASA's Gravity Assist Primer** — [Basics of Space Flight](https://science.nasa.gov/learn/basics-of-space-flight/primer/) is NASA's own explainer with vector diagrams showing how a flyby adds velocity in the Sun's reference frame even though the spacecraft's speed doesn't change relative to the planet.

Messenger and BepiColombo are interesting because they fly to an *inner* planet. Getting to Mercury is counterintuitively hard — you need to shed a huge amount of speed, so they use repeated planetary flybys to gradually slow down instead of burning enormous amounts of fuel.

Roughly 30-40% of all interplanetary missions have used gravity assists, but that number is skewed by the fact that we've sent a *lot* of missions to Mars. If you filter to missions going past the asteroid belt, the figure is essentially 100%.

**A note on this simulator's planet masses:** In reality, a gravity assist from Jupiter changes your speed by 10-20 km/s relative to the Sun, but this happens over a subtle, wide curve spanning millions of kilometers. At the scale of this simulator's canvas, that curve would be nearly invisible. The planet masses in the sim are inflated ~50-100x so the trajectory bends are dramatic enough to see and learn from. The concept is identical, just the visual scale is exaggerated.

### Why small angle changes matter so much

Imagine pointing a garden hose at a target 100 feet away. Tilting the nozzle by half a degree barely changes where the water lands at your feet, but shifts the landing spot by several feet at the far end. Same idea — a 5° change at Earth translates to millions of miles of difference by the time the rocket reaches Mars.

## Features

### Controls
- **Destination** — any planet from Mercury to Neptune
- **Rocket Class** — determines your Δv budget (see below)
- **Boost (Δv)** — departure velocity added at launch, auto-capped to your rocket's budget
- **Launch Angle** — direction of the boost relative to Earth's orbital motion (see below)
- **Zoom** — 0.08x to 4x magnification
- **Animation Speed** — 0.01x (slow-motion) to 5x, adjustable mid-flight

### Rocket Classes & Fuel Budget

The simulator models real propulsion constraints through a **Δv budget** system. Delta-v (Δv) is the total velocity change a rocket can produce — think of it as the "mileage" of a spacecraft. Once you've burned through your budget, you're coasting on momentum and gravity alone.

Four rocket classes are available:

| Class | Δv Budget | Max Boost | Real-World Equivalent | Cost |
|---|---|---|---|---|
| Scout (Small) | 4.0 km/s | ~13% | Rocket Lab Electron, PSLV | ~$7-8M |
| Workhorse (Medium) | 7.0 km/s | ~23% | Falcon 9, Atlas V, Ariane 5 | ~$60-100M |
| Heavy Lift | 11.0 km/s | ~37% | SLS, Falcon Heavy + kick stage | ~$150M-2B |
| Unlimited | ∞ | 60% | (No constraint — for exploration) | — |

**Why this matters:** The boost slider is physically capped to your selected rocket's Δv budget. A Scout physically cannot produce more than 4 km/s of departure Δv — the slider won't go higher, just like a real Scout rocket's fuel tanks won't get bigger mid-flight.

The **reachability strip** below the rocket selector shows which planets are within range:
- 🟢 **Green** — reachable with a direct shot (Δv budget ≥ direct cost)
- 🟡 **Orange (★)** — unreachable directly, but reachable *with gravity assists* (the whole point!)
- ⬛ **Dim** — out of range even with assists

Hover over any planet pill to see exact Δv costs for direct vs. assisted routes.

**The key demonstration:** Select "Workhorse" and look at Jupiter. Direct cost is 8.8 km/s (over budget), but an assisted route via Venus-Earth-Earth costs only 4.0 km/s (within budget). That's not a small savings — the rocket equation is exponential, so that 4.8 km/s difference means roughly 4-5x more fuel mass. Without gravity assists, Jupiter would require a Heavy Lift rocket costing 10-20x more. The Juno mission to Jupiter actually did exactly this — launched on an Atlas V (Workhorse class), used an Earth gravity assist two years later, and reached Jupiter on a budget that would have been impossible with a direct shot.

Δv costs used in the simulator (km/s of departure Δv from Earth):

| Destination | Direct Cost | With Gravity Assists | Assist Route |
|---|---|---|---|
| Mercury | 5.5 | 3.5 | via Venus |
| Venus | 2.5 | 2.5 | Direct is optimal |
| Mars | 2.9 | 2.9 | Direct is optimal |
| Jupiter | 8.8 | 4.0 | via Venus-Earth-Earth |
| Saturn | 10.3 | 4.5 | via Venus-Venus-Earth-Jupiter |
| Uranus | 11.3 | 5.5 | via Jupiter |
| Neptune | 11.7 | 6.0 | via Jupiter |

Notice Venus and Mars don't benefit from assists — they're close enough that a direct Hohmann transfer is already cheap. But past Mars, the savings are dramatic and grow with distance.

**The Rocket Equation — Why Δv Is So Expensive:**

The Tsiolkovsky rocket equation says: `Δv = exhaust_velocity × ln(full_mass / empty_mass)`. That natural logarithm is the villain. To double your Δv, you don't need double the fuel — you need exponentially more. It's like packing for a hiking trip: every extra pound of water means extra food to carry it, which means a bigger pack, which means sturdier boots, which means more energy and more food... Each addition cascades. A rocket that needs 11 km/s instead of 4 km/s doesn't carry 3x more fuel, it carries something like 10-15x more fuel by mass. This is why gravity assists aren't just a nice optimization — for outer planet missions, they're the difference between "mission exists" and "no rocket on Earth can do it."

**In-flight fuel gauge:** During flight, the HUD shows a fuel bar — orange for Δv spent on launch, green for remaining budget. When the rocket receives a gravity assist, a yellow label shows the free Δv gained from the flyby.

### Launch Angle

The launch angle controls *which direction* the rocket fires relative to Earth's orbital motion around the Sun. It's measured in degrees from Earth's velocity vector (the direction Earth is currently traveling).

<img width="1146" height="571" alt="Screenshot 2026-02-20 at 9 33 16 AM" src="https://github.com/user-attachments/assets/5eb5c940-f0a9-4c57-ac6f-c638a26deb26" />




Think of Earth as a car driving in a circle around the Sun. The launch angle determines which direction you throw a ball out the window:

- **0° (Prograde)** — throw the ball forward, in the direction the car is moving. This *adds* to Earth's orbital speed, pushing the rocket into a wider orbit that reaches outer planets. **Use 0° for Mars, Jupiter, Saturn, and all outer planets.**

- **180° (Retrograde)** — throw the ball backward, against the car's motion. This *subtracts* from Earth's orbital speed, causing the rocket to fall into a tighter orbit closer to the Sun. **Use 180° for Mercury and Venus.**

- **90° / -90°** — throw the ball out the side window. This mostly changes the orbit's tilt rather than its size. Rarely useful for reaching planets (since all planets orbit in roughly the same plane), but real missions sometimes use slight angle offsets for fine-tuning.

**Recommended settings by destination:**

| Destination | Recommended Angle | Why |
|---|---|---|
| Mars | 0° | Add speed to reach a wider orbit |
| Jupiter | 0° | Add speed to reach a much wider orbit |
| Saturn+ | 0° | Same principle, more speed needed |
| Venus | ~180° | Subtract speed to drop inward |
| Mercury | ~180° | Subtract speed to drop much further inward |

In practice, small deviations from 0° or 180° (say, ±10-20°) can fine-tune your arrival geometry, but the big picture is simple: outer planets = 0°, inner planets = 180°. The simulator auto-sets the boost amount to the Hohmann ideal when you switch destinations, but the angle is left for you to experiment with — try wildly different angles and watch how the trajectory shape changes.

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
- ✓ **ORBITAL CAPTURE** — spacecraft is slow enough to be captured by the planet's gravity
- ↗ **FLYBY (TOO FAST)** — spacecraft reached the planet but is moving too fast to be captured, it'll swing past and keep going
- ✗ **ESCAPED SOLAR SYSTEM** — exceeded 80 AU boundary
- ☀ **CRASHED INTO SUN** — fell below minimum solar distance
- ⏱ **MAX SIM TIME REACHED** — 1.5M calculation steps exhausted

### Capture vs Flyby
When the spacecraft reaches the destination, the simulator compares its **approach speed** (velocity relative to the planet) against the planet's **escape velocity**. If your approach speed is below escape velocity, the planet's gravity is strong enough to hold onto you — like rolling a marble slowly enough into a bowl that it stays. If you're above escape velocity, you fly right through — like that same marble going so fast it rolls up one side and out the other.

A visual panel shows the comparison after arrival:
- A colored bar for your approach speed
- A white marker line for escape velocity
- The margin (how much under or over you are)

Real escape velocities used:

| Planet | Escape Velocity |
|---|---|
| Mercury | 4.25 km/s |
| Venus | 10.36 km/s |
| Mars | 5.03 km/s |
| Jupiter | 59.5 km/s |
| Saturn | 35.5 km/s |
| Uranus | 21.3 km/s |
| Neptune | 23.5 km/s |

In real missions, even a "flyby" spacecraft can achieve capture with a braking burn (firing engines to slow down). The Δv required equals the excess speed shown by the simulator.

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
2. Select **Scout** or **Workhorse** as rocket class (Mars is reachable even on a Scout — it's a short trip)
3. Note the ideal phase angle displayed (~44°)
4. Drag the **Launch Date** slider until the phase angle readout shows ~44° (look for green zones in the strip)
5. **Boost** will auto-set to ~10% — leave it there
6. Set **Launch Angle** to **0°** (prograde — firing in the direction Earth is moving)
7. Hit **▶ LAUNCH**
8. You should arrive in ~260 days

### Quick Start: Reaching Mercury

Mercury is counterintuitive — you need to *slow down* to fall inward:

1. Select **Mercury** as destination
2. Select **Workhorse** or higher (Mercury's direct cost of 5.5 km/s is too high for a Scout — notice it shows as orange "needs assist" on Scout!)
3. Find a launch window with phase angle ~109°
4. **Boost** will auto-set to ~15%
5. Set **Launch Angle** to **~180°** (retrograde — firing against Earth's motion to shed speed)
6. Hit **▶ LAUNCH**

### Quick Start: The Gravity Assist Argument

This is the "aha moment" scenario:

1. Select **Jupiter** as destination
2. Select **Scout** (4 km/s budget) — notice Jupiter shows as **dim/unreachable**. A Scout can't get there at all.
3. Switch to **Workhorse** (7 km/s) — Jupiter turns **orange (★ needs assist)**. Direct cost is 8.8 km/s (over budget), but with a gravity assist chain it's only 4.0 km/s (within budget!)
4. Switch to **Heavy Lift** (11 km/s) — Jupiter turns **green**. You can brute-force it, but you're spending $2 billion instead of $67 million.
5. Switch back to **Workhorse** — now try launching toward Jupiter with a trajectory that passes near Venus or Earth for a free speed boost. That's how Juno, Galileo, and Cassini actually reached their destinations.

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
├── index.html                  # The entire simulator (single file, ~1100 lines)
├── launch-angle-diagram.svg    # Visual explainer for launch angle concept
├── README.md                   # This file
└── LICENSE                     # MIT License
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
