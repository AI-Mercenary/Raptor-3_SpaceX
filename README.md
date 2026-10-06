# Raptor 3 — Interactive 3D Engine & Live CFD

An interactive, browser-based exploration of **SpaceX's Raptor 3** — the full-flow staged-combustion methane/oxygen engine that powers Starship. Spin it around, cut it open, fire it up, watch the propellants flow through it, and see a real compressible-flow simulation of the exhaust running live in your browser.

**▶ Live demo:** https://ai-mercenary.github.io/Raptor-3_SpaceX/

---

## What it is

This project is an educational visualiser that explains *how* a modern rocket engine works, not just what it looks like. It combines:

- a detailed 3D model of Raptor 3,
- original physically-based materials and a cinematic test-stand scene,
- a real computational-fluid-dynamics (CFD) solver for the chamber, nozzle and plume,
- a narrated guided tour that walks through every major system.

Everything runs client-side — no server, no build step, no install.

## Features

### 🎬 Guided tour
14 narrated chapters that move the camera, highlight parts and switch views automatically:
why methane · the full-flow staged combustion cycle · preburners · turbopumps · regenerative cooling · powerhead & main injector · combustion chamber & throat · nozzle · reading the CFD · shock diamonds · altitude effects · start-up sequence · gimbal & thrust-vector control.

### 🌊 Live CFD (chamber → nozzle → plume)
- 2-D axisymmetric **compressible Euler equations**, finite-volume
- **MUSCL** (minmod) reconstruction + **HLL** Riemann fluxes + **RK2** time stepping
- Runs in a Web Worker on ~26,000 cells along the engine's real inner contour
- Fields: temperature, Mach number, velocity, pressure, **Schlieren** (density gradient)
- Responds live to throttle and altitude
- Result: exit Mach ≈ 3.9, exhaust velocity ≈ 3,200 m/s, ideal Isp ≈ 328 s (published sea-level figure ≈ 327 s)

### 🔥 Exhaust plume
Ray-marched volumetric methalox flame: violet near-exit sheath, Mach-disk "diamonds", turbulent downstream mixing and an orange afterburning layer at sea level. The plume widens and fades with altitude.

### 🛠 Engine controls & views
- Start/shutdown sequence (purge → lead flow → spark-torch ignition → preburners → mainstage)
- Throttle (40–100 %), gimbal pitch/yaw, altitude 0–80 km
- Cutaway, exploded view, part labels, auto-rotate
- **X-ray propellant flow** — animated LOX, methane and hot-gas flow inside the actual ducts, manifolds and cooling jacket
- **Cycle diagram** — animated schematic of full-flow staged combustion
- Click any component for a description and key figures

## Run locally

Open `index.html` in any modern browser (Chrome, Edge, Firefox, Safari). That's it.

Optionally, serve it:

```bash
python -m http.server 8000
```

then visit http://localhost:8000.

## Project structure

```
index.html             app: scene, materials, CFD solver, plume, tour, UI
model/raptor-model.js  compressed engine geometry (decoded at load)
model/ducts.js         duct centre-lines used for the propellant-flow animation
```

## Credits

- **3D model:** ["SpaceX Starship Raptor 3 engine"](https://sketchfab.com/3d-models/none-2d3918a9edcb4eedbf2d180391113e3a) by **VoitAa**, published on [Sketchfab](https://sketchfab.com) (an Epic Games company), licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). The geometry was converted to a compressed format; materials were replaced.
- **Rendering:** [three.js](https://threejs.org)
- Materials, test-stand scene, CFD solver, flame, propellant-flow visualisation, tour and all explanations are original to this project.

## License

Source code is released under the [MIT License](LICENSE).
The 3D model remains under its original **CC BY 4.0** license (see Credits) and is not covered by the MIT License.

## Disclaimer

Educational project. Not affiliated with, endorsed by or connected to SpaceX. Engine figures are approximate and based on publicly available information; the simulation is a simplified inviscid model, not engineering data.
