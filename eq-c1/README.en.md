# EQ-C1 — Job placement based on execution history

**Citable measurements — version of 2026-11-05.** Every figure is copied from the EQ-C1 executive dossier and its data files, with its date and unit. No figure has been rounded beyond what the dossier states.

## 1. What the method does

The queue server keeps the history of past jobs, finds a similar job, predicts the required resource, and sends the job only to a server able to absorb it, choosing the least loaded one. If no similar job exists, the method falls back to the server with the lowest utilisation ratio.

This document gives neither the code, nor the similarity measure, nor the parameters. It describes what was measured, how, and with which limits.

## 2. What is measured and what is not

**Measured, in simulation.** A long bench of 348 rows, 330 distinct seeds of which 329 pairable, over 30 days, compares the history-based method with declared memory. A bench with imprecise declarations (scenarios D1 to D4, 30 seeds each) and a 10-seed validation complete the setup.

**Not measured.** No measurement on a real cluster. No measured effect on the rate of jobs interrupted for lack of memory, which is nonetheless the expected benefit. The imprecision levels of scenarios D1 to D4 are chosen by the bench author and are not sourced.

## 3. Key figures

| What is compared | Result | Date |
|---|---|---|
| Dwell time, history versus declared memory | **+3.525 s** on average, 95% CI [+1.983; +5.068]; history wins on **89 of 329** distinct seeds | recounted on 2026-11-01 |
| Memory violations when the declaration is exact | **+1.854** [+1.445; +2.263] violation per seed; 3,903 versus 3,293 cumulative violations over 329 seeds | dossier of 2026-11-05 |
| Memory prediction error, imprecise declaration | from **−7.7 Mo** [−13.6; −1.8] in D1 to **−262.5 Mo** [−276.0; −249.0] in D4 | dossier of 2026-11-05 |
| Memory violations, imprecise declaration | significantly reduced in **one** scenario only, the 50% under-declaration (D3): −8.13 [−10.09; −6.18] | dossier of 2026-11-05 |
| Time versus the least loaded server | −5.8% (5 runs) and −3.8% (10 seeds); better on 6 seeds out of 10 | dossier of 2026-11-05 |

Earlier dwell-time value, kept for the record: +3.020 s, 74/271, 24 days (reading of 2026-10-24).

## 4. Limits, including unfavourable ones

- **The dossier's main criterion is unfavourable**: on dwell time, history does worse than simple declared memory, by 3.525 s on average, and wins on only 89 distinct seeds out of 329.
- **When the user declares correctly, the method causes more memory violations** than declared memory (+1.854 per seed).
- The only measured advantage is a lower prediction error when the declaration is wrong; it translates into fewer violations only in the heavy under-declaration scenario D3. In D1, D2 and D4 the confidence interval crosses zero.
- **The long-bench criterion was fixed after the bench started**: written on 2026-10-09, bench started on 2026-09-30, after a first computation of the differences. The criteria of the "imprecise declaration" bench were written beforehand, on 2026-10-10.
- Seed 1047 has no declared counterpart: it comes from an earlier version of the bench, which leaves 329 pairable seeds out of 330.
- No result on real hardware, and no enforceable right: the application was never granted.
- No legal opinion; the third-party patent survey dates from 2026-09-23 and must be redone at the purchase date.

## 5. How to reproduce

The package contains the executable model of claims 1 to 6, 50 automated tests, a `Dockerfile`, the protocol, the raw data of the long bench and of the declaration benches, and the `declared` ablation. Every figure above points to the corresponding line of the dossier.

## 6. Public page and contact

- Public page: https://edgequantum65.fr/fiches/eq-c1
- Contact: https://edgequantum65.fr/contact
