# EQ-E1 — Digital compensation of current-sensor phase

**Citable measurements — version of 2026-11-13.** Every figure in this document is copied from the EQ-E1 executive dossier and its data files. Each one carries its date and unit. No figure has been rounded beyond what the dossier states.

## 1. What the method does

The electronic energy meter reads the temperature of its current sensor and the grid frequency, converts each of these two quantities into degrees of phase through a predetermined relation, adds the two corrections, and delays the processor output by the resulting value. The correction is digital and runs inside the meter, not in an analog circuit.

This document gives neither the coefficients, nor the equations, nor the code. It describes what was measured, how, and with which limits.

## 2. What is measured and what is not

**Measured, in simulation.** A Monte-Carlo bench compares two meters: one calibrated only once at the factory, and the same meter with the compensation. Each cell uses 21 seeds × 1,000 sensors, i.e. 21,000 simulated sensors. Sensor imperfections (slope ±10%, non-linearity, offset probe, noise) are assumptions H1–H7, not measurements.

**Not measured.** No standardized IEC test was performed. No measurement on a real current transformer, and none on a physical meter. The throughput benches measure computation time, not metrological superiority.

## 3. Key figures

| Grid · power factor | Factory calibration alone (median worst error) | With compensation (median) | Date / source |
|---|---|---|---|
| 50 Hz · PF 0.5 | 3.36% | 0.281% | recomputed on 21 seeds; dossier revised 2026-11-13 |
| 50 Hz · PF 0.8 | 1.46% | 0.12% | data of 2026-11-05 |
| 60 Hz · PF 0.5 | 3.08% | 0.27% | data of 2026-11-05 |
| 60 Hz · PF 0.8 | 1.34% | 0.12% | data of 2026-11-05 |

- The worst error is divided by at least 7 for 95% of the simulated sensors in all four cells. The multi-seed recount at 50 Hz / PF 0.5 gives × 7.39, with 96.98% of sensors at × 7 or more (dossier revised 2026-11-13).
- "Zero" control: compensation forced to zero, 0% difference over 3,000 sensors per cell, i.e. 12,000 rows, maximum difference 0 (data of 2026-11-05).
- Throughput: 531,025.17 measurements/s on average over 5 runs of 200,000 measurements, variation 0.70% (short bench; the date of the short bench is supplied with the dossier).

## 4. Limits, including unfavourable ones

- Sensor imperfections are assumed. The gain therefore partly depends on the bench assumptions.
- The 2026 addition (individual calibration) divides the error by 5.6 at 50 Hz and 5.3 at 60 Hz: 0.0507% versus 0.2819% at 50 Hz, 0.0504% versus 0.2682% at 60 Hz. But on sensors with no defect of their own it does worse: 0.0506% versus 0.0314% for the compensation alone at 50 Hz. The gain therefore partly comes from the shape of the simulated defect.
- The throughput benches prove no superiority: they are computation times.
- The legal status of the source patent is read from an archived aggregator page and still has to be confirmed at the official register. No legal opinion is provided.

## 5. How to reproduce

The package contains the protocol, the raw data, the recomputation keys and a SHA-256 manifest (`MANIFESTE.sha256`). The executable model passes 71 tests out of 71. Result files and raw data are provided for replay; every figure above points to the corresponding lines of the dossier.

## 6. Public page and contact

- Public page: https://edgequantum65.fr/fiches/eq-e1
- Contact: https://edgequantum65.fr/contact
