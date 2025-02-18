
# CSI-RS Sequence Generation and Mapping

## Introduction
Channel State Information Reference Signal (CSI-RS) is a critical component in 5G New Radio (NR). It helps in channel estimation, beamforming, and interference measurement. The CSI-RS signal is modulated using **Quadrature Phase Shift Keying (QPSK)**, similar to the **Demodulation Reference Signal (DMRS)**.

This document explains how CSI-RS sequences are generated, mapped, and assigned to resource elements, including real-world applications in **5G modem software**.

## CSI-RS Sequence Generation
### Step 1: Pseudo-Random Sequence (PN Sequence)
- CSI-RS sequences are generated using a **PN sequence**.
- The input to the Pn sequence generator is the **Cinit** value.
- **Cinit** depends on:
  - **Slot number**
  - **Symbol number**
  - **Scrambling ID** (UE-specific ID for UE-specific CSI-RS)

This ensures that the CSI-RS sequence is **unique for every OFDM symbol** in a frame.

### Step 2: QPSK Modulation
- The output of the Pn sequence is QPSK modulated.
- The generated QPSK symbols are then mapped to CSI-RS resource elements.

## CSI-RS Resource Mapping
### Key Parameters:
1. **Alpha(k, l) (p, μ)**
   - `k`: Frequency index
   - `l`: OFDM symbol index
   - `p`: Port index
   - `μ`: Numerology index
   - **β_CSI-RS**: Power scaling factor
   - **wf, wt**: Cover codes for orthogonality in time and frequency

2. **Indices for Mapping:**
   - **k' (Frequency Index in CDM Group)**
   - **l' (Time Index in CDM Group)**
   - **k(bar), l(bar) (CDM Group Navigation Indices)**
   - **ρ (CSI-RS Density in a PRB)**

### Mapping CSI-RS to Resource Elements
- `m'` is used to navigate through the **Pn sequence output**.
- `k'` and `l'` determine the frequency and time position **inside a CDM group**.
- `k(bar)` and `l(bar)` determine movement **between CDM groups**.
- `n` represents the subcarrier index within a **Physical Resource Block (PRB)**.

## CSI-RS Port Allocation and Mapping
### CSI-RS Port Assignments
- CSI-RS supports up to **32 ports**.
- The number of available ports can be **1, 2, 4, 8, 12, 16, 24, 32**.

| Row Index | Ports | Density | CDM Type |
|-----------|-------|---------|----------|
| 1         | 1     | High    | No CDM   |
| 2-18      | 2-32  | 1.5     | CDM2, CDM4, CDM8 |

### CDM Group Navigation
- **k(bar), l(bar)** move across CDM groups.
- **k' (0,1)** navigates within a **CDM2** group.
- **k' (0,1,2,3)** navigates within a **CDM4** group.
- **CDM4 example:**
  - First CDM group at `k0`
  - Second CDM group at `k0 + 2`

## CSI-RS Frequency Domain Allocation
### Bitmap-Based Mapping
- CSI-RS allocation is defined by a **bitmap** in 3GPP specifications.
- Example: For row **4** with a **3-bit bitmap**:
  - `b2, b1, b0` represents the frequency location.
  - `k0 = 4f(0)`, `k1 = 4f(1)`, `k2 = 4f(2)`
  - `f(i)`: Index of the set bit (bit = 1)

### Example:
| Bitmap | Set Bits | Computed k Values |
|--------|---------|-------------------|
| [0 1 0] | `f(0) = 1` | `k0 = 4 × 1 = 4` |
| [1 1 0] | `f(0) = 0`, `f(1) = 1` | `k0 = 4 × 0 = 0`, `k1 = 4 × 1 = 4` |

## CSI-RS Orthogonality and Cover Codes
### w(f) and w(t) (Frequency and Time Cover Codes)
- **w(f) and w(t)** provide orthogonality for **multiple ports** in time and frequency.
- Example: **CDM4-FD2-TD2**
  - `wf = [+1, +1, +1, +1]`
  - `wt = [+1, -1, +1, -1]`

| Port | wf | wt | Final Sequence |
|------|----|----|----------------|
| 0    | +1  | +1  | `+1, +1, +1, +1` |
| 1    | +1  | -1  | `+1, +1, -1, -1` |
| 2    | -1  | +1  | `-1, +1, +1, -1` |
| 3    | -1  | -1  | `-1, -1, +1, +1` |

## CSI-RS Slot Allocation
- **Slot Periodicity & Offset:**
  - Defined by **T(CSI-RS) periodicity**.
  - Slot offset **T** determines slot number for transmission.

## Conclusion
CSI-RS sequence generation and mapping are essential for **beamforming, interference measurement, and channel estimation** in 5G networks. The principles of **orthogonality, cover codes, and frequency-time mapping** ensure efficient CSI-RS transmission across multiple ports.

In **5G modem software**, these concepts are used for **dynamic beam adjustment, MIMO operation, and link adaptation** to improve throughput and reliability.

---
## Next Topic
### 71. [CSI-RS: Sequence Generation and Mapping with Example](Sequence_Generation_and_Mapping_with_Example.md)  
