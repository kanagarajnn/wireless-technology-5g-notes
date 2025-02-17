# PRACH Signal Generation

## Introduction

The Physical Random Access Channel (PRACH) is the first uplink signal transmitted by the UE to initiate communication with the gNodeB. Before transmitting PRACH, the base station (gNodeB) does not recognize the UE. This document explains PRACH signal generation at the UE, covering sequence formation, cyclic shifts, frequency domain mapping, and PRACH format selection.

## PRACH Base Sequence: Zadoff-Chu (ZC) Sequence

PRACH uses Zadoff-Chu (ZC) sequences as the base sequence due to their unique properties:
- **High auto-correlation:** Ensures the signal is easily identifiable.
- **Low cross-correlation:** Reduces interference between different PRACH preambles.
- **Constant envelope:** Ensures a low Peak-to-Average Power Ratio (PAPR), beneficial for UE power efficiency.

The ZC sequence is defined as:
```text
x_u,v(n) = e^(-j * π * u * n * (n+1) / L_RA)
```
Where:
- `L_RA` = Sequence length (139 for short format, 839 for long format)
- `u` = Root sequence index (defines different base sequences)
- `n` = Sample index (0 ≤ n < L_RA)

Different values of `u` generate different sequences, ensuring unique preamble detection at the gNodeB.

## Root Sequence Mapping

Each logical index `I` is mapped to a root sequence index as per predefined tables:
```text
Logical Index 1  -> Root Sequence 138
Logical Index 2  -> Root Sequence 137
Logical Index 3  -> Root Sequence 136
...
```
Similar mappings exist for both long and short PRACH formats, ensuring systematic preamble assignment across UEs.

## Cyclic Shift and Preamble Generation

To increase the number of unique preambles, **cyclic shifts** are applied to the base ZC sequence:
```text
Cyclic Shift Size (CV) = 20
Total Sequences = L_RA / CV = 139 / 20 = 6 sequences
```
- **Larger cyclic shifts** → Fewer sequences (less diversity, but simpler detection)
- **Smaller cyclic shifts** → More sequences (better frequency resolution, but increased complexity)

### Conditions for Cyclic Shift Selection
- **Depends on cell radius:** Larger cells require larger shifts to ensure sufficient diversity.
- **Affects frequency offset:** High-mobility UEs require carefully chosen cyclic shifts to mitigate Doppler effects.
- **Restricted vs. unrestricted sets:** Specified in 3GPP standards to ensure robust preamble allocation.

## Frequency Domain Conversion

Once the base sequence is generated, it is transformed into the frequency domain using FFT:
```text
FFT Size = L_RA (139 or 839)
```
- Converts the time-domain sequence into a frequency-domain signal for efficient OFDM transmission.
- **Multiplication by power factor (`β_Prach`)** ensures appropriate transmission power for various deployment scenarios.

## OFDM Symbol Mapping

PRACH sequences are mapped to the resource grid based on:
- **Start Subcarrier Index:** Determines where PRACH is placed in frequency.
- **Start Symbol:** Determines the timing of PRACH transmission.

For **short PRACH formats**:
```text
Subcarrier Spacing: 15, 30, 60, 120 kHz (aligned with PUSCH)
```
For **long PRACH formats**:
```text
Subcarrier Spacing: 1.25 kHz, 5 kHz (optimized for large cell coverage)
```

### PRACH Resource Grid Representation
```text
| Symbol | Subcarrier Index |
|--------|-----------------|
| 0      | PRACH Data      |
| 1      | PRACH Data      |
| ...    | PRACH Data      |
```

## Cyclic Prefix (CP) and Guard Intervals

Each PRACH format includes a cyclic prefix (CP) to handle different cell sizes:
- **CP Size:** Defines the maximum cell radius supported by PRACH.
- **Guard Intervals:** Ensure alignment with PUSCH symbols.

For **long PRACH formats**, CPs are significantly larger to accommodate UEs farther from the gNodeB.

## PRACH Format Selection: Short vs. Long Format

UE determines whether to use **short** or **long** PRACH formats based on:
1. **gNodeB Configuration**: PRACH configurations, including format type and parameters, are broadcast in System Information Block 1 (SIB1).
2. **Deployment Scenario**:
   - **Long PRACH** is used in large cell deployments where propagation delays are higher (e.g., rural or macro cells).
   - **Short PRACH** is used in small cell environments with low propagation delay (e.g., urban or indoor deployments).
3. **Subcarrier Spacing**:
   - **Long PRACH** uses 1.25 kHz or 5 kHz subcarrier spacing for better delay handling.
   - **Short PRACH** aligns with PUSCH subcarrier spacing (15, 30, 60, 120 kHz) for efficient scheduling.
4. **UE Mobility**:
   - High-mobility UEs may require short PRACH for faster access and synchronization.
   - Low-mobility UEs in large cells may use long PRACH to handle propagation delay variations.

## Summary
- **PRACH uses Zadoff-Chu sequences** for unique preamble detection.
- **Root sequence mapping and cyclic shifts** create multiple PRACH preambles.
- **FFT transformation converts the signal to the frequency domain.**
- **OFDM symbol mapping places PRACH in the resource grid.**
- **Cyclic prefixes and guard intervals ensure proper signal alignment.**
- **UE selects PRACH format based on gNodeB configurations, deployment scenarios, and mobility.**

This understanding of PRACH signal generation is crucial for optimizing initial access and uplink synchronization in 5G NR networks. Properly designed PRACH sequences enhance network efficiency, reduce access delays, and ensure seamless UE connectivity in both small and large cell deployments.

---
## Next Section
### 51. [PRACH: Cyclic Shift, Restricted Sets, and Timing Offset](Cyclic_Shift_Restricted_Sets_Timing_Offset.md)  
