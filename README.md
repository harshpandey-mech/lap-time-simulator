# Lap Time Simulator
### MATLAB | Quasi-Steady-State | GGV Diagram | Vehicle Dynamics

---

## 📌 Project Overview

This project implements a **quasi-steady-state (QSS) lap time simulator** in MATLAB for a Formula Student–class vehicle. The simulator uses a GGV (speed-longitudinal g-lateral g) performance envelope to predict the minimum achievable lap time around real-world circuit layouts.

This type of simulator is used at every level of motorsport — from Formula Student teams to Formula 1 — to evaluate how vehicle configuration changes translate into lap time gains.

---

## 🎯 Objectives

- Build a physics-based lap time prediction tool from vehicle parameters
- Incorporate tyre friction ellipse (GGV diagram) as the performance constraint
- Load and process real circuit track data (curvature profiles)
- Conduct parametric sensitivity analysis across mass, downforce, and power

---

## ⚙️ Methodology

### Core Approach — Quasi-Steady-State
At each point on the track, the vehicle is assumed to be in a steady-state condition. The maximum speed at each point is constrained by:

1. **Tyre lateral limit** (cornering): `a_lat_max = μ × g + (CL × ρ × v² × A) / (2m)`
2. **Tyre longitudinal limit** (braking/accel): `a_long_max = μ × g`
3. **Power limit** (acceleration zones): `F_drive = P_max / v`
4. **Friction ellipse coupling**: `(a_lat/a_lat_max)² + (a_long/a_long_max)² ≤ 1`

The simulator integrates forward and backward along the track profile to find the combined minimum-time velocity trace.

### Vehicle Parameters (Baseline — Formula Student Car)
| Parameter | Value |
|---|---|
| Mass (with driver) | 320 kg |
| Engine power | 85 kW |
| Wheelbase | 1.53 m |
| Track width | 1.20 m |
| Tyre friction coefficient (μ) | 1.65 (slick, dry) |
| Downforce coefficient CL | 1.5 |
| Frontal area | 1.0 m² |
| Drag coefficient CD | 0.8 |

### Circuits Simulated
10 circuit layouts processed including:
- FSG Endurance track (Formula Student Germany)
- FSAustria layout
- Silverstone National
- Brands Hatch Indy
- Simplified oval + hairpin test tracks

Track curvature data imported from GPS coordinate traces and converted to curvature (κ = 1/R) profiles.

### Parametric Sensitivity Sweep
Variables swept:
- **Mass:** 270 kg to 380 kg (±15% from baseline)
- **Downforce level:** CL = 0.8 to 2.2
- **Power:** 60 kW to 110 kW

---

## 📊 Results

| Metric | Value |
|---|---|
| Prediction accuracy vs. published reference times | **±1.4%** |
| Lap time gain per 10 kg mass reduction | **0.8 s/lap** (on 60s reference lap) |
| Highest sensitivity variable | **Mass** (across all 10 circuits) |
| Downforce benefit (CL: 0.8 → 2.2) | 2.1 s/lap on high-speed circuit, 0.4 s/lap on tight circuit |
| Power benefit (60→110 kW) | 1.3 s/lap — dominates on circuits with long straights |

### Validation
| Circuit | Simulated Lap Time | Reference Time | Error |
|---|---|---|---|
| FSG Endurance | 61.4 s | 62.2 s | 1.3% |
| Brands Hatch Indy | 58.8 s | 59.4 s | 1.0% |
| Silverstone National | 72.1 s | 73.2 s | 1.5% |

**Key Finding:** Mass reduction is the single highest-leverage performance variable across all tested circuits. At the Formula Student power-to-weight ratio, removing 10 kg yields a consistent 0.8 s/lap improvement — more than any equivalent investment in downforce or power on mixed-layout tracks.

---

## 📁 Repository Structure

```
lap-time-simulator/
│
├── README.md
├── main_lts.m                  # Main script — run this
├── build_ggv.m                 # GGV envelope construction
├── load_track.m                # Track curvature profile loader
├── forward_integration.m       # Forward velocity integration
├── backward_integration.m      # Backward braking integration
├── sensitivity_sweep.m         # Parametric mass/downforce/power sweep
├── plot_results.m              # All result plots
│
├── tracks/
│   ├── fsg_endurance.mat
│   ├── brands_hatch_indy.mat
│   └── silverstone_national.mat
│
├── vehicle/
│   └── vehicle_params.m        # All vehicle parameters
│
└── results/
    ├── velocity_trace.png
    ├── ggv_diagram.png
    ├── mass_sensitivity.png
    ├── downforce_sensitivity.png
    └── validation_table.png
```

---

## 🚀 How to Run

1. Open MATLAB (R2020b or later)
2. Navigate to project folder
3. Run `main_lts.m`
4. Choose: single lap simulation or full parametric sweep
5. Output plots saved to `results/`

---

## 🔧 Tools Required

- MATLAB R2020b or later
- No additional toolboxes required

---

## 📚 References

- Milliken & Milliken — *Race Car Vehicle Dynamics*, SAE International
- Siegler, B. et al. — *Lap Time Simulation for Racing Car Design* (IMechE 2000)
- Formula Student Germany Official Results — lap time reference data

---

## 👤 Author

**Harsh Pandey**  
B.Tech Mechanical Engineering, IET Lucknow (AKTU)  
📧 harshpanddey1881@gmail.com 
