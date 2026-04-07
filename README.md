# QuantStream

A high-velocity integer compression engine leveraging **SIMD-BP128** and **AVX2** vectorization. QuantStream is designed to saturate memory bandwidth by dynamically quantizing sensor telemetry to its minimal bit-representation.

## Scholarly Foundation
QuantStream is an implementation of vectorized integer compression techniques detailed in:
QuantStream is built upon the foundational work of:
* **Lemire, D. & Boytsov, L. (2015):** *Decoding billions of integers per second through vectorization.* (SIMD-BP128/FastPFor)
* **Afroozeh, A. (2023):** *FastLanes: A Next-Gen File Format.* (Data-parallel encodings and transposition logic)

## Technical Architecture
* **Bit-Width Analysis:** Uses hardware-accelerated `clz` instructions to determine block-level entropy.
* **Vectorized Packing:** Implements 32x32 bit-transposition for 256-bit register alignment.
* **Parallel Pipeline:** Multi-threaded execution via OpenMP to maximize vCPU utilization.

## Hardware Benchmarks
*Platform: Intel(R) Xeon(R) @ 2.20GHz*

| Metric | Baseline | QuantStream |
| :--- | :--- | :--- |
| **Throughput** | 9.13 GB/s | **13.47 GB/s** |
| **Peak Burst** | -- | **24.1 GB/s** |
| **Latency (1GB)** | 0.109s | **0.074s** |

## Requirements & Environment
### Hardware
* **Architecture:** x86_64 (Intel Core 4th Gen+ or AMD Zen+).
* **Instruction Sets:** Must support **AVX2** and **BMI2** (for high-speed bit manipulation).
* **Memory:** Minimum 2GB RAM (optimized for Dual-Channel bandwidth).

### Software
* **Operating System:** Linux (Ubuntu 20.04+ recommended) or WSL2.
* **Compiler:** GCC 9.0+ or Clang 10.0+ (Must support OpenMP 4.5+).
* **Dependencies:** * `libomp-dev` (for multi-threading support).
    * `python3` with `pandas` and `matplotlib` (only for telemetry visualization).

