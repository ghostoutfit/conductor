# conductor — Conductor Simulation

Standalone single-file sim deployed to `ghostoutfit.github.io/conductor/`.
Vanilla HTML + CSS + JS only. No build step — edit `index.html` directly.

To run locally: `python3 -m http.server` in this directory, then open `localhost:8000/`.

## What It Does

Models charge carrier drift in different conducting materials under an applied electric field.
Anode (+) on the left, Cathode (−) on the right. Five material modes selectable via toolbar.

## Modes

| Mode | Particles | Behavior |
|------|-----------|----------|
| Copper | Cu lattice atoms (fixed) + electrons | Electrons drift left toward anode |
| Tin | Sn lattice atoms (fixed) + electrons | Same as copper, different colors |
| NaCl (aq) | H₂O + Na⁺ + Cl⁻ | Na⁺ → cathode, Cl⁻ → anode |
| SnCl₂ (aq) | H₂O + Sn²⁺ + Cl⁻ | Sn²⁺ → cathode (2× drift), Cl⁻ → anode |
| Pure H₂O | H₂O + trace H⁺ + OH⁻ | Near-zero drift (autoionization only) |

## Physics

- E-field points left → right (anode → cathode)
- Each particle: `{ x, y, vx, vy, type, charge, r, thermal, fixed, homeX, homeY }`
- Per frame: `vx += charge * E_STR * eScale` + thermal jitter, then damp, then move
- Lattice atoms: restoring spring toward homeX/homeY + minimal jitter, no drift
- Particles that reach their target electrode respawn at a random position
- Pure water: `eScale = 0.03` (barely perceptible drift)

## Color Palette (distinct from other sims)

- Anode: `#ff6030` (warm red-orange)
- Cathode: `#2288ff` (steel blue)
- Electrons: `#00eeff` (cyan)
- Cu: `#d4782a`, Sn: `#8899bb`, Na⁺: `#ffaa30`, Cl⁻: `#88dd33`, Sn²⁺: `#22ccaa`
- H₂O: semi-transparent pale blue, H⁺: `#ff4488`, OH⁻: `#9966ff`

## Deployment

GitHub Pages from `main` branch root (via GitHub Actions). Push to `origin` to deploy.
Remote: `https://github.com/ghostoutfit/conductor.git`
