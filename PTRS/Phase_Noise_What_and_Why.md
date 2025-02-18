# Phase Noise and PTRS in 5G NR

## Introduction
In 5G NR, **Phase Tracking Reference Signal (PTRS)** is used to mitigate the impact of **phase noise** in high-frequency communication. Understanding **phase noise** is essential to grasp the necessity of PTRS. This document explains **what phase noise is, its impact on wireless communication, and how PTRS mitigates its effects**.

---

## What is Phase Noise?
**Phase noise** is a deviation in the phase of a signal caused by imperfections in the **local oscillator (LO)** at the transmitter and receiver. Since **LOs generate carrier frequencies** (e.g., 2.4GHz, 3.5GHz, 28GHz, etc.), any instability in the oscillator results in phase noise.

### How Phase Noise is Generated
- A **perfect LO** produces a pure sinusoidal signal, resulting in a **single peak** in the frequency spectrum.
- A **non-ideal LO** introduces **phase variations**, leading to **spectral spreading** around the carrier frequency.
- This results in **inter-carrier interference (ICI)** in **OFDM** systems, degrading system performance.

### Measuring Phase Noise
Phase noise is measured in **dBc/Hz**, which represents the power of phase noise relative to the carrier power at a specific frequency offset. It is defined as:
```
Phase Noise (dBc/Hz) = Noise Power (dBm) - Carrier Power (dBm)
```
For example:
- Carrier Power = **10 dBm**
- Noise Power at 10kHz offset = **-120 dBm**
- **Phase Noise = -130 dBc/Hz**

---

## Impact of Phase Noise on 5G NR
1. **OFDM Signal Distortion**
   - Phase noise leads to **constellation rotation** in higher-order modulations like **64-QAM and 256-QAM**.
   - It introduces **random phase errors**, affecting the accuracy of received signals.

2. **Higher Impact in Millimeter-Wave (mmWave) Bands**
   - **Higher carrier frequencies (28GHz, 39GHz, etc.)** suffer more from phase noise.
   - **Sub-6GHz** bands (e.g., 700MHz, 3.5GHz) have **negligible phase noise**.

3. **Effect on Modulation Schemes**
   - **QPSK**: Minimal phase noise impact.
   - **16-QAM**: Some distortion, but manageable.
   - **64-QAM / 256-QAM**: High susceptibility to phase noise, leading to increased **Block Error Rate (BLER)**.

4. **Impact on TDD Systems**
   - In **Time Division Duplexing (TDD)**, phase noise affects both **uplink and downlink**, leading to degraded performance in **beamforming**.

---

## Need for PTRS (Phase Tracking Reference Signal)
**PTRS** is introduced in 5G NR to **estimate and correct phase noise** in the received signal. It helps improve the **demodulation accuracy of high-order modulations**.

### Key Characteristics of PTRS
1. **Higher Density in Time-Domain**
   - Since phase noise varies more in **time** than in **frequency**, **PTRS is placed densely in time** but sparsely in frequency.
2. **PTRS in High Modulation Schemes**
   - Only used when **higher MCS (e.g., 64-QAM, 256-QAM)** is used for **PDSCH/PUSCH**.
3. **PTRS in mmWave Bands**
   - Essential for **mmWave (28GHz, 39GHz)** due to increased phase noise at higher frequencies.

---

## Real-World Examples in 5G Modem Software
### **1. Handling Phase Noise in 5G Smartphones**
- In **mmWave-enabled smartphones**, **PTRS is dynamically enabled** when UE switches to **256-QAM**.
- The **5G modem firmware** corrects the phase noise **before decoding PDSCH data**.

### **2. Network Base Station (gNB) Adaptation**
- **gNodeB measures phase noise from UE transmissions** and applies **adaptive PTRS density**.
- In high phase noise conditions, **PTRS is increased** dynamically to maintain performance.

### **3. Carrier Aggregation (CA) and Phase Noise Compensation**
- In **multi-carrier setups**, different carriers have different **phase noise profiles**.
- PTRS is used to align phase across **aggregated carriers** for **seamless data transmission**.

---

## Conclusion
- **Phase noise** is a significant impairment in 5G NR, especially in **mmWave bands**.
- **PTRS is designed to estimate and correct phase noise**, ensuring **higher-order modulations work efficiently**.
- **Modern 5G modems dynamically enable PTRS** based on **MCS, frequency bands, and phase noise conditions**.

By effectively implementing **PTRS**, 5G systems ensure **higher spectral efficiency, lower BLER, and improved data throughput**.

---

This concludes the discussion on **Phase Noise and PTRS in 5G NR**.



---
## Next Topic
### 80. [PTRS: Signal Generation and Mapping [PDSCH & PUSCH]](Signal_Generation_and_Mapping_PDSCH_PUSCH.md)  
