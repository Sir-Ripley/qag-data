# qag-data — R&R Droids shared research data API

The shared JSON/CSV data backend for R&R Droids research sites. CORS-open (`*`),
versioned, free for research use. Live at **https://qag-data.vercel.app**
(human-readable hub page; raw manifest at `/index.json`).

## Datasets

| Path | Description |
|---|---|
| `carbon-capture/vectors.json` | Pillar 2: 10 QAG-screened viral vectors (f_kill + safety margins) |
| `carbon-capture/evolution-run.json` | Pillar 3: 500-generation evolutionary Monte Carlo |
| `carbon-capture/pillar1-optimum.json` | Pillar 1: acoustic sweep optimum callouts |
| `virology/master-pathogen-index.json` | QAG master pathogen index (30 targets) |
| `virology/research-platform-v2.csv` | QAG research platform dataset |
| `virology/viral-decoherence-index-v2.csv` | Viral decoherence index |
| `virology/virology-database.csv` | QAG virology database |
| `qag/cross_validation.json` | QAG cross-framework validation (Reports 1-8) |

## Consuming sites

- 🌱 [Hybrid Bio-Acoustic Carbon Capture](https://qag-carbon-capture.vercel.app) — Pillars 2 & 3 fetch live (embedded fallback)
- 🦠 [QAG Virology Hub](https://qag-virology-demo-qag-works.vercel.app) — live target count on the Pathogen Indexes card

## Sibling backends

- 🌌 [qag-sparc-data](https://qag-sparc-data.vercel.app/galaxies175.json) — 175-galaxy SPARC kinematics API powering the [Kinetics Lab](https://qag-kinetics-lab.vercel.app) explorer; full v3.0 fit table at `/sparc175-corrected.csv`
- 🗄️ `qag-shared-data` — Vercel Blob store for binary assets (decks, PDFs, large files)

## Usage

```js
fetch('https://qag-data.vercel.app/carbon-capture/vectors.json')
  .then(r => r.json())
  .then(d => console.log(d.vectors.length, 'vectors'));
```

## Data fidelity

Every dataset is checksummed against its source at publish time:

- `virology/*` — byte-identical to `Sir-Ripley/qag-virology/data/` on main
- `carbon-capture/vectors.json` — reproduces `tools/qag_virology_sim.py` output (10 vectors, all SECURE, Δζ ≥ 20 mV)
- `carbon-capture/evolution-run.json` — the 8-generation partition-optimized run (peak 3.820 g CO₂/(g·h))
- `carbon-capture/pillar1-optimum.json` — reproduces `tools/pillar1_acoustic_sweep.py` (P₀*=17.07 MPa, kLa=3.8267 s⁻¹)

## License

Apache 2.0 — R&R Droids, Rodney A. Ripley Jr.
