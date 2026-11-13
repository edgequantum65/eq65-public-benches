# EQ-I1 — Memory-lean tiled transform

**Citable measurements — version of 2026-11-13.** Every figure is copied from the EQ-I1 executive dossier and its data files, with its date and unit. No figure has been rounded beyond what the dossier states.

## 1. What the method does

The method reduces the working memory needed to transform an image, without producing edge artefacts. The transform is predefined; it is not learned.

This document gives neither the code, nor the implementation recipe, nor the sizing parameters. It describes what was measured, how, and with which limits.

## 2. What is measured and what is not

**Measured.** A long bench of 168 runs over 13 days with data, from 2026-10-18 to 2026-10-31 (14 calendar days), compares the method with the full-image transform on every run, using a single code fingerprint. A complementary bench of 2026-11-04 uses 3 real photographs (public domain; CC BY 2.0, attribution required), upscaled ×2 to ×2.4 with BICUBIC interpolation, then cropped into 30 frames of 1024×1024; memory there is traced image by image with `tracemalloc`, and time there was measured outside `tracemalloc`.

**Not measured.** No measurement on an ASIC or on an embedded target. The long-bench images are simulated. Timings are those of a Python program on a PC.

## 3. Key figures

| Criterion | Result | Date |
|---|---|---|
| Dynamically measured memory (`tracemalloc`, 30 draws) | 33.6 Mo → 8.5 Mo, i.e. ×3.95 | 2026-11-04 |
| Quality (PSNR difference) | −0.0578 dB on average, 95% CI [−0.0784; −0.0372] dB, 168/168 | bench of 2026-10-18 to 2026-10-31 |
| Time, simulated images (criterion ≤ 1.5×) | 4.24× slower, criterion not met 0/168 | bench of 2026-10-18 to 2026-10-31 |
| Real photographs | difference −0.1532 dB, 95% CI [−0.2296; −0.0768] dB; mean time ratio 5.43× over 30 framings (mean of per-framing ratios; the ratio of mean times, 2,290 ms / 428 ms, gives 5.35×), measured outside `tracemalloc` | 2026-11-04 |

*Units as in the dossier: Mo = 10⁶ bytes, Ko = 1,024 bytes.*

## 4. Limits, including unfavourable ones

- **The time criterion fails on every run** (0/168): the method is 4.24× slower. This is the cost of the method on this bench.
- That ×3.95 compares the memory peak of an implementation that keeps a full copy of the image in 64-bit integers (8,388,608 bytes out of 8,512,819 measured); it does not measure the announced memory target.
- There is no "constant image" control in the long bench, and bitrate is not traced there: bitrate equality cannot be verified. The `contours` type gives 100 dB on both sides, a fallback value, not a quality measurement.
- 7 claims are neither implemented nor linked to code, and the system and program-product claims are not realised in hardware.
- The legal status is read from an aggregator page; the third-party search is not conclusive and no legal opinion is provided.

## 5. How to reproduce

The package contains the protocol written on 2026-10-07, the 168 raw data lines of the long bench, the 30 lines of the photo bench and the claim → code → test table. The criteria of the main bench were fixed before the run; those of the photo bench were adjusted after a first pass, and this is stated in the dossier. Every measurement comes with its recomputation command.

## 6. Public page and contact

- Public page: https://edgequantum65.fr/fiches/eq-i1
- Contact: https://edgequantum65.fr/contact
