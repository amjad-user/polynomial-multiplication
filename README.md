# Polynomial & Big-Integer Multiplication (Problem 7, Part C)

Algorithms and Data Structures, Group 5, SRH University Berlin.

Five ways to multiply two polynomials in Python, plus experiments that compare their
correctness, floating-point precision, runtime and memory.

A polynomial is stored as a list of coefficients, constant term first:
`3x³ + 2x² + 5x + 1  →  [1, 5, 2, 3]`

## The five versions

| Function | Idea | Time |
|---|---|---|
| `poly_mul_v1_schoolbook(a, b)` | every `a[i]` × every `b[j]` | Θ(n²) |
| `poly_mul_v2_dc4(a, b)` | 4 half-size recursive calls | Θ(n²) |
| `poly_mul_v3_karatsuba(a, b, cutoff=16)` | 3 half-size recursive calls | Θ(n^1.585) |
| `poly_mul_v4_fft_recursive(a, b)` | recursive Cooley-Tukey FFT | Θ(n log n) |
| `poly_mul_v5_fft_iterative(a, b)` | in-place bit-reversal FFT | Θ(n log n) |

## How to run

```bash
pip install -r requirements.txt
python part_c_polynomial_multiplication.py
```

The script takes about 4 minutes. It prints all results and saves
`runtime_plot.png` and `memory_plot.png`.

## Results (from `results/`)

- **Correctness:** all 5 versions return identical arrays for n = 8, 64, 512, 2048,
  and the Part A example gives `[3, 19, 27, 24, 24, 7, 6]`.
- **Precision (n = 4096):** the FFT versions are exact up to coefficients of 10⁶ and fail
  from 10⁷, because the results approach 2⁵³ ≈ 9 × 10¹⁵ (the largest integer float64
  stores exactly).
- **Crossovers:** Karatsuba beats Schoolbook from n = 32; Iterative FFT beats Karatsuba
  from n = 512. At n = 32,768: Karatsuba 5.1 s, FFT 0.6 s.
- **Memory:** Schoolbook uses the least; Recursive FFT the most; Iterative FFT about
  40% less than Recursive FFT.

Timings depend on the computer, so your numbers will differ slightly.
