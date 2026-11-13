# EQ-S1 — Lowering the cost of exception-handler lookup

**Citable measurements — version of 2026-11-13.** Every figure is copied from the EQ-S1 executive dossier and its data files, with its date and unit. No figure has been rounded beyond what the dossier states.

## 1. What the method does

The system measures exception-path frequency at run time. Only paths judged hot are transformed at compile time to branch directly to the handler; cold paths keep the classic search. Two techniques, separable or combined, are described: compile-time code transformation, and execution profiling with a decision above a threshold.

This document gives neither the code, nor the analysis algorithm, nor the thresholds. It describes what was measured, how, and with which limits.

## 2. What is measured and what is not

**Measured.** A bench of 168 runs over 13 distinct days, from 2026-10-18 to 2026-10-31, with a single code fingerprint and criteria V1 to V6. The bench compares a stack-based Python interpreter equipped with the method against the same interpreter without it.

**Not measured.** No real JVM, no JIT, no machine code. The bench does not measure the performance of an industrial virtual machine; it measures the mechanics of the model in a Python interpreter.

## 3. Key figures

| Criterion | Result | Verdict |
|---|---|---|
| V1 functional equivalence | 0 difference on `result`, `handled`, `uncaught`, `checksum`, all loads, all runs | PASS |
| V2 handler-lookup cost, hot path | 0.000 versus 5.000; ratio 0.000 | PASS |
| V3 time per exception, hot path | median ratio 0.872, 95% CI [0.868; 0.875]; 9,169 ns versus 10,514 ns | **GAIN NOT DEMONSTRATED** (threshold 0.80) |
| V4 non-regression without exception | median ratio 0.996, 95% CI [0.993; 1.000] | PASS |
| V5 selectivity, cold path | 0 optimised site, 0 run with a difference | PASS |
| V6 no-exception control | 0 non-zero value, 0 difference | PASS |

The delivered code has 8 files (6 Python modules) and 17 green tests. The evidence therefore covers equivalence, selectivity and absence of regression, but **not the time gain at the fixed threshold**. In other words: the lookup gain is established, the time gain is not demonstrated.

## 4. Limits, including unfavourable ones

- **The time gain is not demonstrated**: 0.872 against a pass threshold fixed at 0.80. The dossier states this as a gain not demonstrated, not a partial success.
- **The V2 lookup gain holds by construction**: in the simulation, the optimised variant does not query the exception table on the hot path. That figure describes the mechanics of the model, not a performance measured on a virtual machine.
- No transposition to a real JVM, with JIT and machine code, is provided.
- One run out of 168 (the first, seed 229000) carries an earlier criteria fingerprint. Verdicts on the 167 homogeneous runs are identical.
- The dossier's date proof (OTS) has not been placed to date.
- No legal opinion; the third-party patents identified have not been analysed claim by claim.

## 5. How to reproduce

The package contains the protocol, criteria V1 to V6, the bench command, the 168 raw data lines, the code files and their tests. The daily trace is recomputed over the 168 runs, per day, as a median, using the same statistic as the published result.

## 6. Public page and contact

- Public page: https://edgequantum65.fr/fiches/eq-s1
- Contact: https://edgequantum65.fr/contact
