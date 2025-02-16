# **Physical Downlink Control Channel (PDCCH) in 5G**

## **Introduction**
The **Physical Downlink Control Channel (PDCCH)** in 5G is responsible for transmitting **Downlink Control Information (DCI)**. DCI carries configuration details for:
- **PDSCH (Physical Downlink Shared Channel) – Downlink Data Transmission**
- **PUSCH (Physical Uplink Shared Channel) – Uplink Data Transmission**

DCI can include configurations related to:
- Resource allocation
- Power control
- Subframe structure

---

## **PDCCH Transmitter Chain**
### **DCI Bit Structure**
- **Minimum number of bits:** **12** (if less than 12, padded with zeros)
- **Maximum number of bits:** **128**

### **PDCCH Encoding Steps**
1. **CRC Attachment**
   - **CRC24C** is used
   - A 24-bit CRC is appended to the DCI bits
2. **RNTI Masking**
   - The last **16 bits of CRC** are **XORed with RNTI**
3. **Interleaving**
   - Interleaver supports a maximum of **164 bits**
   - Since CRC is 24 bits, maximum **DCI size is 140 bits**
4. **Polar Encoding & Rate Matching**
   - Polar encoding applies to interleaved bits
   - Rate matching techniques include **puncturing, shortening, or repetition**
5. **Scrambling**
   - Uses **m-sequence**
   - Input parameters: **Scrambling ID, Cell ID, or RNTI**
6. **Modulation**
   - **Always QPSK (Quadrature Phase Shift Keying)**
7. **Resource Mapping**
   - Modulated symbols are mapped to **CORESET** (Control Resource Set)

---

## **PDCCH Demodulation Reference Signal (DMRS)**
### **DMRS Generation Process**
1. **Pseudo-random sequence generation using a seed value**
2. **Cinit value based on:**
   - Slot number (**n(s,f)**)
   - Symbol number (**L**)
   - Nid (**Cell ID or scrambling ID**)
3. **QPSK Modulation of DMRS sequence**
4. **DMRS Symbols are mapped to PDCCH resources**

### **DMRS Variability**
- Different **sequence per OFDM symbol inside a frame**
- Ensures proper channel estimation across different symbols

---

## **Blind Decoding of PDCCH**
Unlike other channels, **PDCCH does not have a dedicated configuration channel**. Instead, the UE must **blindly decode PDCCH** to extract DCI.

### **Unknown Parameters for the UE**
- **Aggregation Level**
- **DCI Size**
- **DCI Type (Uplink or Downlink)**
- **DCI Location within CORESET**

To simplify blind decoding, **QPSK is always used**, and the **code rate is adjusted using Aggregation Level**.

---

## **Aggregation Level and Code Rate in PDCCH**
### **Aggregation Levels and Resource Allocation**
| Aggregation Level | Resource Elements (REs) | QPSK Bits |
|------------------|----------------------|----------|
| 1               | 54                   | 108      |
| 2               | 108                  | 216      |
| 4               | 216                  | 432      |
| 8               | 432                  | 864      |
| 16              | 864                  | 1728     |

### **Code Rate Calculation Example**
- Example: **DCI size = 40 bits**
- After CRC addition: **40 + 24 = 64 bits**
- Polar encoding: **64 bits → 512 bits**
- Rate matching to fit aggregation level:
  - Aggregation Level **1** → **108 bits** → Code rate ≈ **0.59**
  - Aggregation Level **2** → **216 bits** → Code rate ≈ **0.3**
  - Aggregation Level **4** → **432 bits** → Code rate ≈ **0.15**
  - Aggregation Level **16** → **1728 bits** → Code rate ≈ **0.04**

As **aggregation level increases, code rate decreases**, leading to **higher redundancy for improved robustness**.

---

## **Real-World Example in 5G Modem Software**
- **Smartphones perform blind decoding of PDCCH** to extract DCI, enabling efficient downlink and uplink scheduling.
- **5G NR base stations adjust Aggregation Level dynamically** based on channel conditions to optimize transmission reliability.
- **Massive MIMO systems rely on PDCCH for dynamic beamforming configuration**.

---

## **Conclusion**
- **PDCCH carries DCI**, which configures PDSCH (Downlink) and PUSCH (Uplink).
- **Encoding steps include CRC attachment, interleaving, polar encoding, and rate matching**.
- **DMRS in PDCCH ensures accurate channel estimation**.
- **UE performs blind decoding to extract control information efficiently**.

In upcoming discussions, we will explore **CORESET, Search Space, and DCI types in greater detail**.

**Stay tuned for more insights into 5G technology!** 🚀

---
## Next Section
### 32. [PDCCH: DCIs](PDCCH_DCIs.md)
