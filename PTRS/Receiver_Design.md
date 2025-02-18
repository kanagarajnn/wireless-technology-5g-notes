# PTRS Receiver Processing in 5G NR

## Introduction

In **5G NR**, **PTRS (Phase Tracking Reference Signal)** is used to mitigate **phase noise** introduced by oscillator imperfections. This document explains **PTRS receiver processing**, focusing on **phase noise correction, signal equalization, and real-world applications** in **5G modem software**.

---

## Understanding Phase Noise Impact on Received Signals

### What Happens When Phase Noise is Added?
Phase noise causes **rotations in constellation points**, which degrades the received signal quality. The effect varies based on the severity of phase noise.

#### Example: 16-QAM Constellation
- **Without phase noise:** The points remain well-aligned.
- **With phase noise:** The points rotate, introducing errors in **demodulation**.
- **Higher Order Modulations (64-QAM, 256-QAM):** More susceptible to phase noise.

### Frequency vs. Time Variations
- **Less variation across subcarriers** → PTRS is **less dense in frequency**.
- **More variation over time** → PTRS is **denser across OFDM symbols**.

---

## PTRS-Based Phase Noise Estimation

### Received Signal Model
Let:
```
Y = X * Hp * Hd + W
```
Where:
- **Y** → Received signal
- **X** → Transmitted signal
- **Hp** → Phase noise effect
- **Hd** → Channel effect (multipath, fading)
- **W** → White noise

### Case 1: Static Channel (No Time-Varying Fading)
- **Hd remains constant across symbols.**
- **Hp varies over time, causing phase shifts per OFDM symbol.**
- **PTRS estimates Hp variations and corrects phase rotation.**

#### Phase Noise Estimation Steps:
1. **Estimate Hd using DMRS on symbol 0**
2. **Remove Hd effect from PTRS symbols**
3. **Calculate phase rotation per symbol**
4. **Interpolate Hp across OFDM symbols**
5. **Apply phase correction to received data**

---

## Advanced Phase Noise Estimation

### Case 2: Time-Varying Channel
- **Hd changes dynamically across symbols.**
- **Use multiple DMRS symbols (e.g., symbol 0, 3, 11) for interpolation.**

#### Updated Equalization Strategy:
1. **Estimate Hd at multiple symbols (e.g., symbol 0, 3, 11)**
2. **Interpolate Hd across the slot**
3. **Remove Hd effects from PTRS symbols**
4. **Estimate phase noise Hp for each PTRS RE**
5. **Interpolate Hp and apply correction**
6. **Equalize received data**

### Example: Phase Correction in High SNR Environment
- **Before correction:** 64-QAM constellation is distorted due to phase noise.
- **After PTRS equalization:** Constellation points are restored, improving **BLER (Block Error Rate)**.

---

## Implementation in 5G Modem Software

### Real-World Considerations
1. **Adaptive PTRS Density:** Adjusted based on **MCS and modulation order**.
2. **Multi-Antenna Scenarios:** Separate phase noise estimation per **Rx antenna**.
3. **TDD Reciprocity:** Utilize **uplink PTRS** to aid **downlink precoding**.
4. **Low-Power UE Optimization:** Efficient phase correction algorithms minimize **power consumption**.

### Software Implementation Steps
1. **Extract PTRS REs from received signal.**
2. **Perform Hd estimation using DMRS.**
3. **Apply initial equalization to PTRS symbols.**
4. **Compute per-symbol phase noise.**
5. **Interpolate phase correction for non-PTRS symbols.**
6. **Apply final equalization to PDSCH/PUSCH data.**

---

## Conclusion

- **PTRS is critical for mitigating phase noise** in **high-order modulation schemes**.
- **Receiver processing involves channel estimation, phase noise tracking, and correction.**
- **Advanced equalization strategies enable reliable 5G communication in high-frequency bands.**
- **Implementation in 5G modem software requires efficient interpolation and correction techniques.**

This concludes the discussion on **PTRS receiver processing in 5G NR**. Let me know if you need **further refinements or additional details**!



---
## Next Topic
### 83. [NR operating bands, bandwidth, SDL and SUL](../Additional_Topics/NR_operating_bands_bandwidth_SDL_SUL.md)  
