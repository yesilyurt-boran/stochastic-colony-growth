# PA Colony Growth — Branching Tip Simulation

A stochastic simulation of bacteria colony morphology using a branching random walk framework.

---

## Overview

This project explores a phenomenological stochastic model for branching bacterial colony growth using biased random walks, probabilistic branching/death dynamics, and environment-dependent growth modulation.

Rather than modeling individual particles or cells explicitly, the colony is represented through effective propagating growth tips whose collective behavior generates emergent colony morphology.

The goal is to investigate how simple local stochastic rules can produce realistic large-scale growth patterns, including branching structures, anisotropic expansion, and self-limiting colony size.

---
## Model Components

The model combines:

- Biased random walk dynamics for directional tip propagation
- Survival, branching, and death probabilities for stochastic tip evolution
- Branching penalties to reduce effective motion after bifurcation
- Environmental nutrient fields (uniform and non-uniform) that modulate growth rates
- Symmetry-based daughter branch generation following branching events

These ingredients define an effective colony-growth process without imposing explicit macroscopic growth laws.


---
## Nutrient Environments

| Type | Description |
|---|---|
| `uniform` | spatially homogeneous |
| `half-plane` | Anisotropic: rich below y=0, poor above |
| `red` | Radial exponential decay from origin |

Each tip at every step:
- **Survives** — continues moving with current speed
- **Dies** — trajectory ends
- **Splits** — records a branch point; a daughter tip is spawned with reduced speed and a diverging bias direction

Nutrient at each location modulates survival, splitting probability, and speed via a sigmoid scaling function. Daughter tips inherit a bias frame computed from the parent's trajectory, ensuring approximate radial outward motion and preventing collision with the parent branch.

---

## Monte Carlo Analysis

To characterize ensemble behavior, multiple independent colony realizations are generated under fixed parameters.

Statistical observables
- Mean colony radius vs. time
- Standard deviation across realizations
- Spatial density / colony occupancy maps
- Estimated colony boundary and morphology


---

## Key Findings
The ensemble-averaged colony radius exhibits three distinct growth regimes:

1. Initial ballistic expansion:

    Rapid approximately linear growth driven by unconstrained tip propagation.
    
2. Progressive growth slowdown:

    Expansion decelerates as branching accumulation and environmental penalties reduce effective mobility.
3. Late-time saturation:

    The colony approaches an effective maximum size, where continued activity primarily contributes to internal densification rather than further outward expansion.

These results suggest that self-limiting colony growth can emerge naturally from simple stochastic branching dynamics without explicitly imposing a carrying capacity.

---

## Structure
```
stochastic-colony-growth.ipynb          # full simulation and analysis
```

| Section | Content |
|---|---|
| 1. Motivation | Biological background and modelling rationale |
| 2. Model Definition | From single walker to multi-tip ensemble |
| 3. Simulation Algorithm | Full implementation with nutrient coupling and branching |
| 4. Monte Carlo Experiments | Mean radius, variance, density map, colony boundary |
| 5. Parameter Sweep | Interactive sliders across environments and turn counts |
| 7. Key Findings | Interpretation of results |
| 8. Future Directions | Nutrient depletion, antibiotic environments |

---

## Dependencies

```
numpy
matplotlib
scipy
alphashape
ipywidgets
```

---

## Key Parameters

| Parameter | Role |
|---|---|
| `tipn` | Number of tips (controls statistical convergence) |
| `m_turns` | Steps per tip (controls colony extent) |
| `survival_rate` | Base probability of surviving each step |
| `splitting_rate` | Base probability of branching each step |
| `k` | Sigmoid sharpness for nutrient response |

---

## Future Directions

- Nutrient depletion: dynamic field updated as tips consume
- Tip-Tip interactions and competition
- Antibiotic environments: death rate as a function of external agent distribution
- Connection to individual-scale dynamics
- Calibration against experimental colony-growth data

---
### Acknowledgements

We would like to thank Emrah Simsek for the helpful conversations and especially for bringing this topic to our attention. This project was developed as an independent exploratory modeling study to demonstrate stochastic simulation, scientific computing, and emergent behavior analysis.
