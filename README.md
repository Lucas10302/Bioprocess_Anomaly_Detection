# Real-Time Anomaly Detection in Bioprocessing (Bioreactor)

## Project Context
In the biopharmaceutical industry, losing a batch due to contamination or equipment drift represents a critical financial loss. This project simulates a monitoring system capable of detecting real-time drifts in physical and biological parameters to trigger early warnings before batch failure.

## Objectives
- **Simulate** industrial sensor data (pH, Temperature, Dissolved Oxygen - D0) based on real biological operating ranges.
- **Filter Noise** inherent to physical sensors using a Moving Average smoothing technique to prevent false positives.
- **Automate Detection** of drifts and generate a crisis report with a domain-specific diagnosis (suspected contamination, cooling system failure).

## Tech Stack
- **Python 3**
- **Pandas & NumPy**: Time-series manipulation, data cleaning, and rolling window calculations.
- **Matplotlib / Seaborn**: Data visualization and safety threshold mapping.

## Methodology
1. **Dataset Generation**: Created 500 time-points with Gaussian noise (`np.random.normal`) to mimic field conditions.
2. **Anomaly Injection**: Introduced sudden drops (D0) or progressive drifts (pH, Temperature) at specific timestamps.
3. **Signal Processing**: Applied a 10-minute rolling average to stabilize the signal and increase robustness.
4. **Detection Logic**: Continuous monitoring against strict safety boundaries:
   - pH: [6.8 - 7.2]
   - Temperature: [36.5°C - 37.5°C]
   - Dissolved Oxygen (DO): [30% - 40%]

## Results
The algorithm successfully ignored natural fluctuations (noise) and triggered the alarm at **t = 352 min**, only 2 minutes after the actual anomaly started.

*Sample output from the detection script:*
--- CRISIS REPORT ---
Alert Timestamp: 352 min
Diagnosis: pH Drift (Potential Contamination?)
Values at detection: pH=6.73, Temp=37.02°C
