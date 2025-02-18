# Mapping of Zadoff-Chu (ZC) Sequence to SRS Resources in 5G

## Introduction
**Sounding Reference Signal (SRS)** in **5G NR** is mapped to resources based on a structured mathematical approach. The Zadoff-Chu (ZC) sequence, previously generated, is allocated to the appropriate **time-frequency grid** based on multiple parameters.

This document explains how the **ZC sequence** is mapped to **SRS resources**, covering **frequency-domain and time-domain mapping**, cyclic shifts, comb structures, and real-world applications.

## Key Parameters for SRS Mapping
The SRS mapping equation is:
```af,l^(pi) = (1 / sqrt(Nap)) * beta_SRS * r^(pi)(k', l')```
Where:
- `Nap` = Number of SRS antenna ports.
- `beta_SRS` = Power scaling factor for SRS.
- `r^(pi)(k', l')` = ZC sequence generated.
- `Pi` = Antenna port index.
- `k'` = Frequency index within ZC sequence.
- `l'` = Time index within ZC sequence.

## Understanding Frequency-Domain Mapping
The **frequency location** where the SRS sequence is mapped is given by:
```f = KTC * k' + k_o^(pi)```
Where:
- `KTC` = Comb size (`2` or `4`).
- `k_o^(pi)` = Offset calculated from SRS resource allocation.

### ZC Sequence Length and PRB Allocation
The **length of the ZC sequence** is determined by:
```Msc,b^SRS = msrs,b * 12 / KTC```
- `msrs,b` = Number of PRBs allocated for SRS.
- `12` = Number of subcarriers per PRB.
- `KTC` = Comb size (`2` or `4`).

Example:
- If `msrs,b = 1 PRB` and `KTC = 2`:
  ```Msc,b^SRS = (1 * 12) / 2 = 6 subcarriers```
- If `msrs,b = 1 PRB` and `KTC = 4`:
  ```Msc,b^SRS = (1 * 12) / 4 = 3 subcarriers```

## Understanding Time-Domain Mapping
SRS symbols are allocated in the **last 6 OFDM symbols** of a slot (`8` to `13`). The mapping follows:
```L' = L_o + l'```
Where:
- `L_o` = Offset determining symbol start position.
- `l'` = Index within allocated SRS symbols.

Example:
- If `L_o = 10` and `l' = 0, 1`:
  - SRS is mapped to symbols `10` and `11`.

## Frequency Offset Calculation
The frequency offset is given by:
```k_o^(pi) = k_o'^(pi) + Σ (KTC * Msc,b^SRS * NB)```
Where:
- `k_o'^(pi)` = Initial frequency shift.
- `NB` = Parameter adjusting hopping.
- `KTC * Msc,b^SRS` = Total frequency span covered by SRS.

## Frequency Hopping in SRS
**Frequency hopping** is enabled based on:
- **Inter-slot hopping**: Changes frequency allocation across slots.
- **Intra-slot hopping**: Changes frequency allocation within a slot.

Frequency hopping enables SRS to improve **power efficiency** and **channel estimation** in fading environments.

### Real-World Applications in 5G Modems
1. **Uplink Scheduling Optimization**:
   - 5G modems such as **Qualcomm Snapdragon, MediaTek Dimensity** use SRS mapping to optimize **uplink beamforming** and **PRB allocation**.

2. **Interference Avoidance in TDD Systems**:
   - **Different cells** allocate distinct **SRS hopping sequences** to reduce interference.

3. **Power Efficiency at Cell Edge**:
   - **Low-power UEs** use **frequency hopping** to transmit SRS efficiently over **smaller PRB allocations**.

## Conclusion
- **SRS mapping ensures optimal resource allocation for uplink transmissions.**
- **Zadoff-Chu sequence mapping considers comb structure, frequency shifts, and hopping strategies.**
- **5G modems leverage SRS mapping to optimize beamforming, interference management, and power efficiency.**

Next, we will explore **advanced SRS configurations and their impact on multi-user scheduling in 5G networks.**



---
## Next Topic
### 78. [SRS: Receiver Processing, TDD Reciprocity and Antenna Switching](Receiver_Processing_TDD_Reciprocity_Antenna_Switching.md)  
