]# NumPy Data Type Memory & Performance Benchmark Lab

A hands-on benchmark showing how NumPy's **dtype** choice (int8 to int64, float16 to float64) changes **memory usage**, **speed** and **numerical precision** on 1-million-element arrays.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/lakadepratik2121-arch/numpy-dtype-benchmark-lab/blob/main/numpy_dtype_benchmark_lab.ipynb)

**Live website:** [lakadepratik2121-arch.github.io/numpy-dtype-benchmark-lab](https://lakadepratik2121-arch.github.io/numpy-dtype-benchmark-lab/)
## Problem

Choosing the wrong dtype wastes memory, slows code down, or silently corrupts results (integer overflow, float rounding). This project measures those trade-offs with real numbers so dtype choice becomes a decision, not a default.

## What I built

1. **Array creation:** the same 1M-element data in int8/16/32/64 and float16/32/64 using `astype()`.
2. **Memory table:** `size`, `itemsize` and `nbytes` for every dtype.
3. **Timing:** `sum` and `multiply` timed with `timeit` (best of 5 runs).
4. **Overflow and precision demos:** int8 wrap-around, float32 losing small increments, float16 overflowing to `inf`, checked with `np.iinfo` / `np.finfo`.
5. **Charts and recommendations:** bar charts for memory and time, a memory-vs-speed scatter plot, and a "which dtype to use" guide.
6. **Extras:** `mean`, `sort` and matrix multiply benchmarks, scaling from 100K to 10M elements, and a real image example (uint8 vs float32 vs float64).

## Key results

| Finding | Detail |
|---|---|
| Memory | int8 uses **8x less memory** than int64/float64 (1 MB vs 8 MB for 1M elements) |
| Speed | Smaller is not always faster. float16 was the slowest dtype because most CPUs lack native float16 arithmetic |
| Overflow | int8 value 200 becomes **-56**; uint8 `230 + 60` becomes 34 |
| Precision | float32 loses `16777216 + 1`; float16 summing 1M values overflows to `inf` |
| Images | A float64 image uses **8x the memory** of the same uint8 image |

> Exact timings depend on your machine. The numbers above are from my runs; see the notebook outputs for the full tables.

## NumPy concepts used

`dtype`, `astype()`, `itemsize`, `nbytes`, `np.arange`, `np.random.default_rng`, `np.iinfo`, `np.finfo`, `np.clip`, 3D arrays, overflow behaviour, performance timing.

## How to run

**On Google Colab (no setup):** click the badge above and run **Runtime > Run all**.

**Locally:**
```bash
pip install -r requirements.txt
jupyter notebook numpy_dtype_benchmark_lab.ipynb
```

## Recommendations

- Use the smallest dtype that safely holds your data range, then measure on your own workload.
- Use `uint8` for image pixels, `float32` for large ML arrays, `float64` for accuracy-critical maths.
- Check ranges with `np.iinfo` before downcasting, because integers overflow silently.
- Avoid `float16` for computation; use it only for storage.

## Tech stack

Python, NumPy, pandas, Matplotlib, Google Colab
