# PRACH Short Format

## Introduction

The **Physical Random Access Channel (PRACH) Short Format** is designed for rapid initial access and synchronization in **5G NR** networks. Unlike **PRACH Long Format**, which is optimized for large cell deployments, **Short Format PRACH** is compact and suitable for smaller cell sizes with reduced propagation delays.

## Key Characteristics of PRACH Short Format

1. **Short in Time Duration**
   - Sequence length: **139 subcarriers**
   - Optimized for small and medium cell deployments

2. **Supported Subcarrier Spacing**
   - **15 kHz and 30 kHz** for **FR1 (Frequency Range 1)**
   - **60 kHz and 120 kHz** for **FR2 (Frequency Range 2)**

3. **Different PRACH Short Formats**
   - There are **nine different short formats**: A1, A2, A3, B1, B2, B3, B4, C0, and C2.
   - Each format differs in **sequence repetitions, cyclic prefix (CP) length, and supported cell range.**

## PRACH Short Format Table Overview

| Format | Sequence Length | Subcarrier Spacing | CP Length | Number of Repetitions | Cell Radius (Approx.) |
|--------|----------------|--------------------|------------|-----------------|------------------|
| A1     | 139            | 15/30/60/120 kHz  | Small       | 2               | ~900 m           |
| A2     | 139            | 15/30/60/120 kHz  | Medium      | 4               | ~2 km            |
| A3     | 139            | 15/30/60/120 kHz  | Large       | 6               | ~3.5 km          |
| B1     | 139            | 15/30/60/120 kHz  | Small       | 2               | ~350 m           |
| B2     | 139            | 15/30/60/120 kHz  | Medium      | 4               | ~1 km            |
| B3     | 139            | 15/30/60/120 kHz  | Medium      | 6               | ~1.8 km          |
| B4     | 139            | 15/30/60/120 kHz  | Large       | 12              | ~4 km            |
| C0     | 139            | 15/30/60/120 kHz  | Very Large  | 1               | ~5 km            |
| C2     | 139            | 15/30/60/120 kHz  | Largest     | 4               | ~10 km           |

## PRACH Short Format Structure

The PRACH short format consists of the following components:

1. **Cyclic Prefix (CP)**: Provides guard time for synchronization.
2. **PRACH Sequence**: The actual transmission sequence based on Zadoff-Chu (ZC) sequences.
3. **Guard Time (GT)**: Ensures the PRACH sequence does not interfere with the next slot.

Unlike **long PRACH**, some short PRACH formats lack explicit **guard periods** and rely on **multiple PRACH occasions** for coverage.

### PRACH Short Format Transmission Behavior
- **A1, A2, A3**
  - No guard period.
  - Used in **multiple PRACH occasions**.
  - Example: **A1 requires six PRACH occasions.**
  
- **B1, B2, B3, B4**
  - **B1 & B4 are standalone**.
  - **B2 & B3 are paired with A2 & A3, respectively**.
  - **Smaller CP, leading to smaller cell radii.**
  
- **C0 & C2**
  - **Larger CP for extended cell coverage**.
  - **C2 has the longest CP and supports the largest cell size (10 km).**
  
## PRACH Short Format Bandwidth

The bandwidth occupied by short PRACH depends on subcarrier spacing.

```text
PRACH Bandwidth = Sequence Length × Subcarrier Spacing
```

For example, at **30 kHz subcarrier spacing**:

```text
139 × 30 kHz = 4.17 MHz
```

Higher subcarrier spacing results in wider bandwidth usage.

## Use Cases of PRACH Short Format

### **When to Use PRACH Short Format?**
- ✔ **Dense Urban Networks**: Small cells requiring rapid synchronization.
- ✔ **Millimeter-Wave (mmWave) Deployments**: FR2 (60/120 kHz) PRACH for ultra-fast initial access.
- ✔ **Low-Latency Applications**: Shorter PRACH sequences reduce access delay.

### **When NOT to Use PRACH Short Format?**
- ❌ **Large Cell Deployments**: PRACH Long Format is more suitable for macro-cell coverage (>10 km).
- ❌ **High Mobility Scenarios**: PRACH Long Format provides better resilience against Doppler effects.

## Conclusion

PRACH Short Format plays a crucial role in ensuring **efficient and low-latency random access** in 5G networks. The choice of **short PRACH format** depends on factors such as **cell size, subcarrier spacing, latency, and mobility**. Proper selection enhances network performance, reduces access delays, and optimizes UE synchronization with the gNodeB.



---
## Next Section
### 54. [PRACH: More on Resource Allocation](More_on_Resource_Allocation.md)  
