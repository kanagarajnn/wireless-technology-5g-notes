# DFT-s-OFDM (Transform Precoding) in PUSCH

## Introduction

In 5G NR, the **Physical Uplink Shared Channel (PUSCH)** supports two types of modulation schemes:
- **DFT-spread-OFDM (DFT-s-OFDM)**, also known as **Transform Precoding**
- **CP-OFDM (Cyclic Prefix-Orthogonal Frequency Division Multiplexing)**

DFT-s-OFDM is used to **reduce Peak-to-Average Power Ratio (PAPR)** in uplink transmissions, thereby improving power efficiency and enhancing signal coverage for User Equipment (UE).

---

## Why Use Transform Precoding?

**DFT-s-OFDM** introduces an additional Discrete Fourier Transform (DFT) stage before the OFDM processing to reduce **PAPR**. This is particularly useful because:

1. **Improves Power Efficiency**: Lower PAPR enables UE to transmit with higher power, enhancing coverage.
2. **Better Performance in High Mobility Scenarios**: Reduces power amplifier distortion, which is critical for high-speed users.
3. **Used for Low-Capacity Devices**: Suitable for IoT and mMTC (massive Machine Type Communication) applications.

However, **DFT-s-OFDM is limited to a single layer**, making **CP-OFDM** preferable for **higher throughput scenarios**.

---

## Transform Precoding Process

### **PUSCH Transmission Chain with DFT-s-OFDM**

1. **Layer Mapping**: Data symbols are mapped to layers.
2. **Transform Precoding (DFT Stage)**: Each OFDM symbol undergoes a Discrete Fourier Transform (DFT) to spread the frequency components.
3. **Resource Grid Mapping**: The transformed data is mapped onto subcarriers.
4. **Antenna Port Mapping**: The data is mapped to the appropriate antenna port for transmission.

### **Mathematical Representation**
Each PUSCH symbol undergoes a DFT operation:
```
x'[k] = (1 / sqrt(M_sc^PUSCH)) * SUM_{i=0}^{M_sc^PUSCH-1} x[i] * e^(-j*2*pi*i*k/M_sc^PUSCH)
```
Where:
- `x[i]` → Input data symbols
- `M_sc^PUSCH` → Number of subcarriers allocated to PUSCH (12 * PRBs allocated)
- `k` → Subcarrier index
- `i` → Index in the PUSCH samples

After DFT, the transformed symbols are mapped to the subcarriers before being sent through the **Inverse Fast Fourier Transform (IFFT)** process in OFDM transmission.

---

## PRB Allocation and Constraints

- **DFT-s-OFDM requires specific PRB allocation**:
  - PRBs must follow the condition:
    ```
    2^α_2 * 3^α_3 * 5^α_5
    ```
  - This constraint ensures efficient **DFT computation** and **low complexity**.
- Unlike **CP-OFDM**, PRBs **cannot** be arbitrarily selected.

---

## Resource Grid Mapping

- Data symbols are first arranged in resource elements.
- **When PTRS (Phase Tracking Reference Signals) is enabled**, PUSCH symbols avoid **PTRS REs**.
- Data is **spread across subcarriers** before passing through the antenna port mapping.

### Example: PUSCH Transmission with Transform Precoding
1. **Without PTRS**:
   - Data symbols (120 total) are mapped into **5 symbols per PRB**.
   - DFT is applied to each set of **24 samples**.
2. **With PTRS**:
   - Data symbols (100 total) avoid PTRS locations.
   - DFT is still applied across **remaining subcarriers**.

---

## Comparison: DFT-s-OFDM vs CP-OFDM in PUSCH

| Feature | DFT-s-OFDM | CP-OFDM |
|---------|------------|---------|
| **Layers** | 1 | Up to 4 |
| **PAPR** | Low (better power efficiency) | High (needs linear PA) |
| **Coverage** | Better | Lower |
| **Throughput** | Lower | Higher |
| **Interleaving** | No DMRS-Data interleaving | DMRS-Data interleaving allowed |
| **Usage** | Uplink scenarios requiring better power efficiency | High-throughput uplink scenarios |

---

## Practical Applications

### **When to Use DFT-s-OFDM?**
- ✅ Low-power devices like IoT (NB-IoT, LTE-M) for better energy efficiency.
- ✅ Scenarios where **UE transmission power is limited**.
- ✅ Coverage-limited deployments like rural areas.
- ✅ UE with single-layer uplink transmission.

### **When NOT to Use DFT-s-OFDM?**
- ❌ High-throughput applications (eMBB) that require **multi-layer transmissions**.
- ❌ mmWave bands where **high spectral efficiency** is required.
- ❌ Scenarios where flexible PRB allocation is needed.

---

## Summary

- **DFT-s-OFDM** is used in PUSCH for **lower PAPR and better power efficiency**.
- Uses **DFT before OFDM processing** to spread the signal and reduce peak power variations.
- **PRB allocation must follow constraints** (multiples of 2, 3, or 5).
- **Only single-layer transmission** is supported.
- **Preferred in coverage-limited and power-sensitive scenarios**.
- **CP-OFDM is used when higher throughput is required**.

Understanding DFT-s-OFDM is crucial for optimizing **5G modem uplink performance** while balancing **coverage, power, and efficiency**. 🚀



---
## Next Section
### 47. [PUSCH: MIMO, Codebook, Beamforming and more](MIMO_Codebook_Beamforming.md)
