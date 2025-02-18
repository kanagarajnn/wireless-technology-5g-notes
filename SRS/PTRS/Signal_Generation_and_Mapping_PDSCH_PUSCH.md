# PTRS in 5G NR: Phase Tracking Reference Signal

## Introduction

In **5G NR (New Radio)**, **PTRS (Phase Tracking Reference Signal)** is a specialized reference signal designed to combat **phase noise** introduced by **oscillator imperfections** in high-frequency transmission. PTRS is especially important in **high-order modulations** (e.g., **64-QAM, 256-QAM**) and **millimeter-wave (mmWave) frequencies** where phase noise is more pronounced.

This document explains **phase noise, PTRS signal generation, and resource mapping** for both **downlink (DL) and uplink (UL) transmissions**.

---

## Understanding Phase Noise

### What is Phase Noise?
Phase noise arises due to imperfections in the **local oscillator (LO)** used to generate the carrier frequency. It results in **frequency fluctuations** that distort the transmitted signal.

### Impact of Phase Noise
- **OFDM Inter-Carrier Interference (ICI):** Causes phase rotation between subcarriers, degrading signal quality.
- **Higher Modulation Sensitivity:** More pronounced in **64-QAM and 256-QAM** than in **QPSK**.
- **Higher Frequency Dependency:** More severe in **mmWave bands (e.g., 28 GHz, 39 GHz)** compared to **sub-6 GHz**.

### Measuring Phase Noise
Phase noise is measured in **dBc/Hz**:
```
Phase Noise (dBc/Hz) = 10log10(Noise Power (W) / Carrier Power (W))
```

For example:
- Carrier frequency: **2.4 GHz**
- Carrier Power: **10 dBm (10⁻² W)**
- Noise Power at 10 kHz offset: **-120 dBm (10⁻¹⁵ W)**
- Phase noise: **-130 dBc/Hz**

---

## PTRS Signal Generation

PTRS is not an independently generated sequence. Instead, it is **derived from DMRS (Demodulation Reference Signal)** and mapped onto select resource elements (REs) in **time and frequency domains**.

### Key Differences Between Downlink and Uplink PTRS
| Feature | Downlink PTRS | Uplink PTRS |
|---------|--------------|-------------|
| **Antenna Ports** | Single port | Two ports |
| **Application** | PDSCH (Data Channel) | PUSCH (Uplink Data Channel) |
| **Oscillator Dependency** | Each panel shares an oscillator | UE may have multiple oscillators |

### Frequency and Time Density of PTRS
#### **Frequency Density (K_PTRS)**
- Defines how frequently PTRS is placed in the **frequency domain**.
- Determined by PRB allocation and defined in the **5G NR specifications**:
  - **No PTRS** if PRBs allocated < **NB0**
  - **K_PTRS = 2** if **NB0 ≤ PRBs < NB1**
  - **K_PTRS = 4** if **PRBs ≥ NB1**

#### **Time Density**
- Determines how often PTRS is placed in the **time domain**.
- Higher **MCS (Modulation and Coding Scheme)** → Higher **PTRS density**.
- **MCS-based mapping:**
  - **Low MCS (QPSK, 16-QAM)** → Sparse PTRS
  - **High MCS (64-QAM, 256-QAM)** → Dense PTRS

---

## PTRS Resource Mapping

### PTRS Resource Elements (REs) Selection
- **Uses DMRS REs**: Selects specific **DMRS subcarriers** for PTRS.
- **Avoids DMRS RE Collisions**: Ensures separate REs for **PTRS and DMRS**.
- **UE-Specific Mapping**: **RNTI (Radio Network Temporary Identifier)** determines **which PRB** is used to prevent collisions between UEs.

### Example of PTRS Mapping
#### **Case 1: Frequency Density = 2, Time Density = 2**
- Selected DMRS REs are repeated every **two PRBs** in frequency.
- Repeated every **two symbols** in time.
- Avoids **collision with DMRS REs**.

#### **Case 2: Frequency Density = 4, Time Density = 1**
- **Every fourth PRB** contains PTRS.
- **Every OFDM symbol** has PTRS REs.
- Used in **high SNR, high-frequency environments**.

---

## Uplink PTRS Considerations

### **Coherent vs. Non-Coherent Antenna Ports**
- **Coherent Antennas:** Single oscillator shared across multiple antennas → **Single-port PTRS**.
- **Non-Coherent Antennas:** Multiple oscillators → **Two-port PTRS required**.

### **Impact on Uplink Scheduling**
- PTRS REs must be **carefully scheduled** to **avoid PUSCH data loss**.
- **Uplink PTRS configuration** is influenced by **UE oscillator stability**.

---

## Conclusion

- **PTRS mitigates phase noise**, ensuring reliable **high-order modulations (64-QAM, 256-QAM)**.
- **PTRS mapping is based on DMRS REs**, avoiding interference while maintaining **minimal overhead**.
- **Time and frequency density of PTRS** is dynamically adjusted based on **MCS and allocated PRBs**.
- **TDD Reciprocity** allows **downlink PTRS** to be used for **uplink estimation** in some scenarios.

PTRS plays a crucial role in ensuring **robust 5G communications**, particularly at **high frequencies** and **high data rates**.

---

This concludes the discussion on **PTRS in 5G NR**. Let me know if you need **further refinements or additions**!


---
## Next Topic
### 81. [PTRS: Signal Generation and Mapping [PUSCH Transform Precoding]](Signal_Generation_and_Mapping_PUSCH_Transform_Precoding.md)  
