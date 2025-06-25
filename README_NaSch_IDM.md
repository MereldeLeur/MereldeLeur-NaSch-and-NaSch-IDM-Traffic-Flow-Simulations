# Traffic Simulation Models – NaSch and NaSch + IDM

This repository contains the Python code used for the traffic flow simulations in the MSc thesis _"Timeliness Criticality in Supply Chains"_ by Merel de Leur (2025). The simulations explore the dynamics of decentralized systems through two models:

- **NaSch Model**: A classical cellular automaton traffic model
- **NaSch + IDM Model**: A hybrid version incorporating heterogeneous driver behavior based on the Intelligent Driver Model (IDM)

---

## 🚀 Features

- Simulate traffic with varying densities and driver types
- Generate position and velocity data
- Analyze loop times, delays, and avalanche effects
- Create publication-quality plots for thesis figures

---

## 📁 Structure

```
traffic_simulation.py          # Main script: runs both NaSch and NaSch+IDM models
NaSch Data/                    # Output CSVs from NaSch simulation
NaSch Graphs/                  # Plots from NaSch analysis
NaSch + IDM Data/             # Output CSVs from NaSch+IDM simulation
NaSch + IDM Graphs/           # Plots from NaSch+IDM analysis
```

---

## ⚙️ Requirements

Install required Python libraries with:

```bash
pip install numpy matplotlib pandas
```

> Tested with Python 3.10+

---

## ▶️ Running the Code

Make sure to adjust file paths in the script to match your local environment.

To run the full simulation and analysis pipeline:

```bash
python traffic_simulation.py
```

This will:
- Simulate traffic across a range of densities
- Validate simulation correctness at each step
- Save data and plots to the appropriate folders

---

## 📊 Key Outputs

- **Flow-density plots**: `density_vs_flow.png`
- **Speed-density plots**: `density_vs_speed.png`
- **Loop time statistics**: `mean_loop_time_vs_density.png`
- **Delay and avalanche metrics**: `delay_times_car1.png`, `mean_avalanche_duration_vs_density.png`
- **Thesis-ready panel figure**: `panel_2x3_loglog_b_only_with_critical.png`

---

## 🧠 Model Notes

### NaSch Model
- Discrete time, discrete space
- Simple rules for acceleration, braking, and random slowing
- Idealized traffic dynamics for understanding congestion emergence

### NaSch + IDM Model
- Heterogeneous agents with differing risk profiles
- Driver-specific max speeds and time headways
- Models more realistic driver behavior while preserving cellular structure

---

## 📚 Citation

If you use this code, please cite:

> de Leur, M. J. M. (2025). _Timeliness Criticality in Supply Chains_. MSc Thesis.

---

## 📬 Contact

Merel de Leur  
[Your email address]  
[Your LinkedIn or personal site, if applicable]
