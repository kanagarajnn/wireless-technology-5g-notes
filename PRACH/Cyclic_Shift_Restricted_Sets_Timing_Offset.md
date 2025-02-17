# PRACH Cyclic Shift, Restricted Sets, and Timing Offset

## Introduction
Physical Random Access Channel (PRACH) is the first uplink signal transmitted by the User Equipment (UE) to the gNodeB for initial access. To ensure reliable detection of PRACH sequences, the concept of **cyclic shift**, **restricted sets**, and **timing offset** play a crucial role in PRACH signal design.

## PRACH Preamble and Sequence Generation

Each PRACH preamble is generated based on the **Zadoff-Chu (ZC) sequence**, which is defined as:
```text
x_u,v(n) = e^(-j * π * u * n * (n+1) / L_RA)
```
Where:
- `L_RA` = Sequence length (839 for long PRACH, 139 for short PRACH)
- `u` = Root sequence index
- `n` = Sample index

### Root Sequence Mapping
The PRACH sequence depends on the **root sequence index** `u`. Each logical index `I` is mapped to a specific root sequence index, as per predefined tables:
```text
Logical Index 1  -> Root Sequence 138
Logical Index 2  -> Root Sequence 137
Logical Index 3  -> Root Sequence 136
...
```
This ensures that different UEs can use different preamble sequences to avoid collisions.

### Cyclic Shift and Preamble Expansion
To generate additional unique preambles, **cyclic shift (N_CS)** is applied to the base ZC sequence.
```text
Cyclic Shift Size (N_CS) = 209
Total Sequences = L_RA / N_CS = 839 / 209 ≈ 4 cyclic shifts
```
- **Larger cyclic shifts** → Fewer sequences (better separation, but reduced availability)
- **Smaller cyclic shifts** → More sequences (higher availability, but increased collision probability)

The total number of PRACH sequences available is:
```text
Total Preambles = Number of Root Sequences * Cyclic Shifts
```
Example:
- If **838 root sequences** are available with **4 cyclic shifts**, the total preambles are **3352 unique preambles**.

### Preamble Selection by UE
1. The UE is assigned a **starting root sequence index**.
2. Based on the cyclic shift, it derives possible PRACH sequences.
3. The UE **randomly selects** a preamble from the available options.
4. The selected sequence is transmitted to the gNodeB for random access.

## PRACH Timing Offset and Detection
When a PRACH sequence is transmitted, the **timing offset** determines how the signal aligns with the gNodeB’s expected timing.

- **Timing Advance Calculation:**
  - The UE does not initially have a precise timing advance.
  - The gNodeB estimates the timing delay based on received PRACH preamble.
  - The UE is then instructed to adjust transmission timing for future uplink signals.
  
- **Maximum Delay and Cell Size:**
  - The maximum delay supported determines the **cell radius**.
  - If a UE is farther than the maximum supported range, its PRACH signal may be misaligned, causing failure in detection.

## Restricted and Unrestricted Sets
Due to potential **frequency offset** (caused by Doppler shift or oscillator inaccuracies), PRACH sequences may suffer from misalignment. To mitigate this, **restricted sets** are defined.

- **Unrestricted Set:**
  - Used when frequency offset is negligible.
  - Provides maximum preamble availability.

- **Restricted Set Type A:**
  - Used when frequency offset < Subcarrier Spacing (Δf)
  - Reduces the number of cyclic shifts to improve reliability.

- **Restricted Set Type B:**
  - Used when frequency offset < 2 × Subcarrier Spacing
  - Further limits cyclic shifts to minimize false detections.

### Practical Example
If a UE is moving at **high speed**, it introduces a frequency offset due to Doppler shift.
- **High mobility scenarios:** Restricted Set Type B is used.
- **Medium mobility scenarios:** Restricted Set Type A is preferred.
- **Low mobility scenarios:** Unrestricted set can be used.

## Summary
- **Cyclic shifts** help in generating multiple PRACH preambles from a single root sequence.
- **Larger N_CS values** increase cell size but reduce the number of available sequences.
- **Timing offset** determines the PRACH detection and timing advance calculation.
- **Restricted sets** mitigate frequency offset issues for improved PRACH detection.
- **Mobility conditions** influence whether **unrestricted, restricted set A, or restricted set B** is used.

Understanding these factors is critical for optimizing PRACH performance in 5G NR networks and ensuring efficient initial access for UEs.



---
## Next Section
### 52. [PRACH: Long formats](Long_Formats.md)  
