# Sun_Moon_lat_lon
Calculate sun and moon latitude and longitude using Python
# Sun and Moon Position Calculation using Quantum State Simulation

This project calculates the positions of the Sun and the Moon using Julian Date formulas and quantum simulation techniques.

## Table of Contents
- [Overview](#overview)
- [Calculation Formulas](#calculation-formulas)
  - [Julian Date Calculation](#julian-date-calculation)
  - [Sun Position Formula](#sun-position-formula)
  - [Moon Position Formula](#moon-position-formula)
- [Quantum State Simulation](#quantum-state-simulation)
- [Predicting Positions for 10,000 Years](#predicting-positions-for-10000-years)
- [Usage](#usage)

## Overview
The project combines classical astronomical calculations with a simulated quantum computing approach to:
1. Predict the Sun and Moon's longitude and latitude over 10,000 years.
2. Leverage a quantum state simulator for state manipulation and measurement.

The calculations use Julian Date as a base for accurate time representation.

---
## Calculation Formulas

### Julian Date Calculation
The **Julian Date (JD)** is used to calculate the number of days elapsed since January 1, 4713 BC (Julian Calendar).

Formula:
```python
if month <= 2:
    year -= 1
    month += 12
A = math.floor(year / 100)
B = 2 - A + math.floor(A / 4)
JD = math.floor(365.25 * (year + 4716)) + math.floor(30.6001 * (month + 1)) + day + B - 1524.5
JD += (hour + minute / 60 + second / 3600) / 24
```
### Explanation:
- **year, month, day**: Input date.
- **A** and **B** are corrections for leap years.
- **hour, minute, second**: Optional time components to improve precision.

### Sun Position Formula
The Sun's position is calculated using the mean longitude and anomaly:

1. **Mean longitude of the Sun (L):**
```math
L = (280.460 + 0.9856474 * n) % 360
```
2. **Mean anomaly of the Sun (g):**
```math
g = (357.528 + 0.9856003 * n) % 360
```
3. **Ecliptic longitude (lambda_sun):**
```math
lambda_sun = (L + 1.915 * sin(g) + 0.020 * sin(2g)) % 360
```

- **n**: Number of days since **JD = 2451545.0**.
- **g**: The mean anomaly, converted to radians.
- **lambda_sun**: Sun's longitude (latitude is 0 for the Sun).

### Moon Position Formula
The Moon's position is determined using its mean longitude and anomaly:

1. **Mean longitude of the Moon (L):**
```math
L = (218.316 + 13.176396 * n) % 360
```
2. **Mean anomaly of the Moon (M):**
```math
M = (134.963 + 13.064993 * n) % 360
```
3. **Argument of latitude (F):**
```math
F = (93.272 + 13.229350 * n) % 360
```
4. **Longitude and latitude of the Moon:**
```math
lambda_moon = (L + 6.289 * sin(M)) % 360
beta_moon = 5.128 * sin(F)
```

- **n**: Number of days since **JD = 2451545.0**.
- **M**: Moon's mean anomaly, converted to radians.
- **lambda_moon**: Moon's longitude.
- **beta_moon**: Moon's latitude.

---
## Quantum State Simulation
This project uses a **QuantumState** class to simulate qubit states for demonstrating quantum gates:
1. **Hadamard Gate (H):** Creates a superposition state.
2. **CNOT Gate:** Applies a controlled NOT operation.
3. **Measurement:** Simulates measuring qubit states in the computational basis.

### Example Quantum State Manipulation
```python
qs = QuantumState(num_qubits=2)
qs.apply_gate(hadamard(), qubit=0)
qs.apply_cnot(control=0, target=1)
qs.measure()
```

---
## Predicting Positions for 10,000 Years
The script predicts the Sun and Moon's positions **for every day** over a span of 10,000 years starting from 2024.

Example prediction:
```python
predict_sun_moon_positions(start_year=2024, years=10000)
```
Output:
```
Date: 2024-01-01, Sun - Long: 280.55°, Lat: 0.00°, Moon - Long: 134.90°, Lat: 5.12°
...
```

---
## Usage
1. Run the script to calculate the Sun and Moon's positions:
```bash
python main.py
```
2. Quantum state manipulations are printed alongside positional data predictions.

---
## Dependencies
- Python 3.10+
- NumPy

---
## Future Enhancements
- Integrate actual quantum computing backends.
- Predict other celestial events (e.g., eclipses).

---
## License
This project is licensed under the MIT License.

