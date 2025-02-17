# PRACH Receiver Processing

## Introduction

The **Physical Random Access Channel (PRACH)** is the first uplink signal sent by a **User Equipment (UE)** to establish initial access with the **gNodeB (gNB)**. The PRACH receiver processing at the **gNB** is crucial in detecting and synchronizing incoming random access requests from multiple UEs.

This document outlines the detailed steps involved in PRACH processing at the gNB, including signal reception, correlation, timing advance calculation, and handling of multiple UEs.

---

## 1. PRACH Signal Reception

### Characteristics of PRACH:
- PRACH **subcarrier spacing** may differ from other uplink channels.
- PRACH signals experience **variable propagation delays** due to different UE distances from the gNB.
- **Multiple UEs** may transmit PRACH simultaneously within the same resource allocation.

### PRACH Sequence Structure:
PRACH consists of:
- **Cyclic Prefix (CP)**
- **Sequence Repetitions (for some formats)**
- **Guard Period (GP)**

The received PRACH signal is processed separately from other uplink channels due to its distinct subcarrier spacing and structure.

---

## 2. PRACH Signal Processing at gNB

### Step 1: Cyclic Prefix Removal
Upon receiving the PRACH signal, the **gNB removes the Cyclic Prefix (CP)** to extract the main sequence. Since the signal may be delayed due to propagation, the system considers the worst-case delay scenario to ensure all useful signal components are retained.

### Step 2: Downsampling
- PRACH subcarrier spacing may be different from **PUSCH (Physical Uplink Shared Channel)**.
- If PRACH subcarrier spacing is **5 kHz**, while **PUSCH uses 30 kHz**, the receiver must adjust sample rates.
- Example:
  - **PRACH Format 3** with **5 kHz subcarrier spacing** results in a symbol time of **200 microseconds**.
  - **PUSCH with 30 kHz subcarrier spacing** has a symbol time of **33.33 microseconds**.
  - The number of received PRACH samples is significantly larger than needed for processing.
  - **Downsampling** is applied to match the required 839 or 139 sequence length (depending on format).

### Step 3: Fast Fourier Transform (FFT) - Frequency Domain Conversion
Once the PRACH signal is extracted and downsampled, it is converted from the **time domain** to the **frequency domain** using an **FFT operation**:
- **839-point FFT** for long PRACH format.
- **139-point FFT** for short PRACH format.
- This step helps extract frequency-domain components for further correlation.

### Step 4: Correlation with Locally Generated PRACH Sequences
- The **gNB generates PRACH Zadoff-Chu (ZC) sequences** corresponding to different **Root Sequence Index (u)** values.
- Each **received PRACH sequence is correlated** with multiple generated sequences.
- The output of this correlation helps determine **which PRACH preamble was transmitted by the UE**.

### Step 5: Peak Detection & Timing Advance Calculation
- The correlated PRACH output is converted **back to the time domain** using **Inverse FFT (IFFT)**.
- The gNB searches for peaks in the correlation output:
  - **A strong peak** indicates a successful detection of a PRACH preamble.
  - **Multiple peaks** may indicate transmissions from different UEs.
  - **Peak shift** from the expected position represents the **timing delay** due to UE distance.

- The **timing advance (TA) is calculated** as follows:
  - The peak delay is measured in terms of **number of samples**.
  - The delay is converted to a **time value** using the sampling rate.
  - The final **TA value** is determined based on system-specific parameters.

Example:
- **UE PRACH transmission delay** = 20 microseconds
- **Round-trip delay** (due to uplink + downlink) = 40 microseconds
- **Timing advance command** = Adjustment required in UE uplink transmission timing to synchronize with gNB.

---

## 3. Handling Multiple UEs
### Scenario: Multiple UEs Transmitting PRACH Simultaneously
When multiple UEs transmit PRACH in the same slot:
1. The gNB **detects multiple peaks** in the correlation output.
2. Each peak corresponds to a **different preamble index**.
3. Timing advance is computed separately for each UE.
4. The gNB schedules **Msg2 (Random Access Response - RAR)** for each detected UE with unique timing advance values.

### Resolving Collisions:
- If **two UEs transmit the same preamble with similar delays**, the gNB might only detect a **single peak**.
- In such cases, **contention resolution is performed** using Msg3 (scheduled uplink message).

---

## 4. Summary

| Step | Description |
|------|------------|
| 1. CP Removal | Extracts PRACH sequence while handling propagation delays. |
| 2. Downsampling | Adjusts PRACH sampling rate to match system bandwidth. |
| 3. FFT Conversion | Converts the PRACH signal to the frequency domain. |
| 4. Correlation | Matches received PRACH sequence with locally generated sequences. |
| 5. Peak Detection | Identifies preamble transmission and computes timing advance. |
| 6. Multi-UE Handling | Detects multiple preambles and assigns Msg2 responses accordingly. |

---

## Conclusion
- PRACH receiver processing is crucial for detecting **UE preambles** and estimating **timing advance**.
- The **gNB processes PRACH independently** from other uplink channels due to different subcarrier spacing.
- **Multiple UEs can transmit PRACH simultaneously**, requiring robust detection and contention resolution.
- Accurate **timing advance calculation** ensures proper uplink synchronization for subsequent transmissions.

Understanding PRACH receiver processing is essential for optimizing **5G NR random access** and ensuring seamless connectivity in diverse network deployments.


---
## Next Section
### To be Added Soon
