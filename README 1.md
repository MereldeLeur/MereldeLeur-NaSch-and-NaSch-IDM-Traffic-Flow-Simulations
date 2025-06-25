
# NaSch and NaSch+IDM Simulation

This repository contains simulations of traffic dynamics using two models:

- The **NaSch model** (Nagel-Schreckenberg cellular automaton model)
- The **NaSch+IDM hybrid model** (with heterogeneous driver behavior)

Each model simulates car dynamics over a circular track of length `N=1000` for different densities `M/N`.

---

## Code Structure & Simulation Description

The code runs a complete simulation and post-processing pipeline:

### 1. **Position Simulation**
- Each car is initialized with a position (`evenly spaced`) and a velocity (`v_max` or heterogeneous if IDM).
- In each time step (up to 1 million), cars update positions based on:

  #### For NaSch:
  - **Acceleration:** If `v < v_max`, increment speed.
  - **Slowing Down:** Adjust to avoid collisions (gap between cars).
  - **Random Braking:** With probability `p`, reduce speed by 1.
  - **Movement:** Move forward by `v` cells, wrap around circularly.

  #### For NaSch+IDM:
  - Each car has:
    - A driver type (`risk-averse`, `normal`, `risk-seeking`)
    - A personal `desired speed` and `T` (safe time gap)
    - A personal `braking probability`
  - Each step:
    - Attempt to accelerate toward desired speed
    - Compute gap to car ahead and calculate `desired space`
    - If gap too small, reduce velocity accordingly
    - Apply random braking
    - Move car based on final velocity

  - After position updates, **validation checks**:
    - No backward moves
    - No collisions (unique positions)
    - Consistent ID ordering

- Car positions at each time step are saved to CSV (`Data_NaSch_*.csv` or `Data_NaSch_IDM_*.csv`)

---

### 2. **Velocity Extraction**
- From position files, the per-step velocity for each car is computed by the difference in position.
- Handles circular track wrap-around (`modulo N`).
- Results are saved in `car_velocity_*.csv`.

---

### 3. **Fundamental Diagram Analysis**
- From velocity data:
  - Compute **global mean speed** (space-mean) and **global flow** as:  
    `flow = density × speed`
- Plot:
  - Speed vs. Density
  - Flow vs. Density
  - Mark critical density with max flow

---

### 4. **Loop Time Extraction**
- For car 1 (and 25 others), calculate how long it takes to complete one full loop (i.e., travel `N` cells cumulatively).
- Loop time data is saved per car across `M` values.
- Plots generated:
  - Loop time vs. loop index
  - Mean & Std deviation of loop time vs. density

---

### 5. **Delay and Avalanche Analysis**
- Define **delay** as: `actual_loop_time - mean_loop_time` (only if positive).
- Analyze:
  - Delay vs. loop index
  - Sorted delays (for all M)
  - **Avalanche events:** contiguous positive delays between zero delays
    - Extract **duration** (length) and **size** (area under curve)
    - Plot vs. density

---

### 6. **Panel Plots for Thesis**
- 2x3 panels combining:
  - Loop times
  - Delay plots
  - Avalanche statistics
  - All include scientific formatting and annotation of critical density

---

## Output Files
- CSV data: positions, velocities, loop times, delays, avalanche metrics
- PNG plots: speed-density, flow-density, loop times, avalanche behavior
- All output is organized by model and stored under respective folders.

---

## Usage
Each script is modular, but recommended to run in order. Simulations are CPU-intensive and support parallel execution for NaSch+IDM.

---

## Notes
- Models assume 1-based indexing for position to simplify wrap-around math.
- Random seeds fixed for reproducibility.
- Careful validation checks help catch collisions and logical errors during simulation.
