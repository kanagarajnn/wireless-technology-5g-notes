# PRACH Long Format

## Introduction

The Physical Random Access Channel (PRACH) long format is designed for scenarios where UEs are farther from the gNodeB and require extended time durations for signal transmission. Compared to short format PRACH, long format PRACH has a longer time duration, which allows it to accommodate larger cell sizes.

## PRACH Long Format Overview

There are **four PRACH long formats** defined in 5G NR:
1. **Format 0**
2. **Format 1**
3. **Format 2**
4. **Format 3**

Each format has a different subcarrier spacing and time duration. Unlike shared channel transmissions, PRACH in long format has subcarrier spacings of **1.25 kHz and 5 kHz**.

## Symbol Duration Calculation

The subcarrier spacing determines the symbol time:
- **1.25 kHz subcarrier spacing:**
  - Symbol time = `1 / 1.25 kHz = 800 µs`
- **5 kHz subcarrier spacing:**
  - Symbol time = `1 / 5 kHz = 200 µs`

These durations are much longer than the **OFDM symbol times** used in PUSCH (e.g., **66.7 µs** for **15 kHz** subcarrier spacing).

## Sequence Time and Cyclic Prefix (CP)

- The sequence time is determined by:
  ```text
  Time = 24576 * 64 * TC
  where TC = 0.509 * 10^(-6) ms
  ```
- The CP time is also specified per format, impacting **cell radius** and **uplink synchronization**.

## PRACH Structure

PRACH transmission consists of three components:
1. **Cyclic Prefix (CP):** Helps manage propagation delay.
2. **Sequence Length (839 symbols):** Defines the main PRACH transmission.
3. **Guard Period (GP):** Ensures time alignment and prevents inter-symbol interference.

## PRACH Long Format Properties

Each long format is defined by its **total duration, CP duration, and cell size**:

| Format  | Subcarrier Spacing | Total Duration | CP Duration | Max Cell Radius |
|---------|--------------------|----------------|-------------|----------------|
| 0       | 1.25 kHz           | 1 ms           | 103 µs      | 14 km         |
| 1       | 1.25 kHz           | 3 ms           | 684 µs      | 100 km        |
| 2       | 1.25 kHz           | 4.3 ms         | 138 µs      | 22 km         |
| 3       | 5 kHz              | 1 ms           | 103 µs      | 14 km         |

## How PRACH CP Defines Cell Size

The CP accounts for **round-trip propagation delay**:
```text
Cell Radius = (Speed of Light * CP Time) / 2
```
Example Calculation for **Format 0**:
```text
Cell Radius = (3 * 10^8 m/s * 103 * 10^(-6) s) / 2
           ≈ 14.5 km
```

## When to Use Each PRACH Long Format

### **Format 0** (Legacy LTE-like Deployment)
- Used for LTE-like **5G installations**.
- Best for standard urban and suburban environments.

### **Format 1** (Large Cell Size, 100 km Coverage)
- Used for large macro cells.
- Suitable for rural areas and **highway deployments**.
- Large CP allows **long propagation delay compensation**.

### **Format 2** (Better Coverage with Repetition Gain)
- Sequences are **repeated four times** for **6 dB signal gain**.
- Best for **coverage-limited scenarios** (e.g., **indoor, remote areas**).
- **Higher reliability**, but **smaller cell size** than Format 1.

### **Format 3** (High-Speed Scenarios)
- Uses **5 kHz subcarrier spacing**.
- Designed for **high-mobility UEs** (e.g., trains, highways).
- Higher subcarrier spacing mitigates **Doppler shifts**.

## Bandwidth and TDD Considerations

The PRACH format selection must align with:
1. **Uplink slot availability in TDD systems**:
   - Format 0 requires **1 ms continuous uplink slots**.
   - Format 1 requires **3 ms continuous uplink slots**.
   - Format 2 requires **4.3 ms continuous uplink slots**.
   - Format 3 requires **1 ms continuous uplink slots**.
2. **Bandwidth Usage**:
   - **Format 0, 1, 2:** Uses **1.048 MHz**.
   - **Format 3:** Uses **4.195 MHz**.

## Summary

- **PRACH long formats** are optimized for various deployment scenarios.
- **CP length defines the maximum cell size**.
- **Higher subcarrier spacing** in Format 3 supports high-speed UEs.
- **Format 2 repetition provides signal gain for weak coverage areas.**

Understanding PRACH long formats allows network engineers to optimize **initial access** and **uplink synchronization** in different environments, ensuring efficient 5G network performance.

---

In the next section, we will explore **PRACH Short Formats** and their deployment scenarios.



---
## Next Section
### 53. [PRACH: Short formats](Short_Formats.md)
