# **PUCCH Format 3: Detailed Explanation**

## **Introduction**
PUCCH Format 3 (F3) is a **long-format** uplink control channel used in **5G NR (New Radio)** for transmitting **Uplink Control Information (UCI)** efficiently. It supports both **\(π/2\) BPSK** and **QPSK** modulation and uses **Transform Precoding** to reduce the **Peak-to-Average Power Ratio (PAPR)**.

PUCCH F3 is primarily used for transmitting:
- **HARQ (ACK/NACK) bits**
- **Scheduling Request (SR) bits**
- **Channel State Information (CSI) bits**

This format can carry a **large number of UCI bits**, making it suitable for scenarios requiring **high-capacity uplink signaling**.

---
## **PUCCH Format 3: Processing Overview**
### **1. Bit Processing Pipeline**
The bit processing for **PUCCH F3** follows these steps:
1. **CRC Addition**:
   - If UCI bits are **greater than 12**, a **6-bit CRC** is added.
   - If UCI bits are **greater than 19**, a **code block segmentation** and **11-bit CRC** are used.

2. **Channel Coding**:
   - For **3-11 bits**: **Reed-Muller Encoding**
   - For **12-19 bits**: **Polar Encoding**
   - For **\(≥ 20\)** bits: **Polar Encoding with segmentation**

3. **Rate Matching**:
   - Based on available **PUCCH resources** and **modulation scheme**.

4. **Scrambling**:
   - XOR operation with **pseudo-random sequence** for interference avoidance.

5. **Modulation**:
   - **\(π/2\) BPSK** for lower SNR scenarios and **lower PAPR**.
   - **QPSK** for better efficiency in good channel conditions.

---
## **2. Transform Precoding**
Transform Precoding is used to reduce **PAPR** and is applied **after modulation**. It ensures **even power distribution across subcarriers** by applying **Discrete Fourier Transform (DFT)**.

### **DFT Formula**
For each symbol \( L \):
```
z(k) = (1/sqrt(Msc^PUCCH,s)) * sum[y(m) * e^(-j*2π*m*k/Msc^PUCCH,s)]
```
Where:
- **\(Msc^{PUCCH,s}\)** = Number of subcarriers assigned to a symbol.
- **y(m)** = Modulated symbol values.
- **DFT converts time-domain samples into frequency-domain representation**.

---
## **3. Resource Mapping**
Once the **DFT transform precoded data** is obtained, it is mapped to **PUCCH F3 resource elements (REs)**. The mapping follows:
- **First Symbol** → **Symbol 4**
- **Second Symbol** → **Symbol 6**
- **Third Symbol** → **Symbol 8**
- **Remaining symbols** → **Symbols 9, 11, 13, etc.**

The **data is allocated to all OFDM symbols**, **excluding** the ones reserved for **DMRS (Demodulation Reference Signals)**.

#### **PUCCH F3 Symbol Mapping Table**
| PUCCH Symbols | DMRS Symbols | Data Symbols |
|--------------|-------------|--------------|
| 14          | 2 (3,10)     | 12          |
| 10          | 2 (3,7)      | 8           |
| 7           | 2 (2,5)      | 5           |
| 6           | 2 (1,4)      | 4           |

---
## **4. Maximum Data Capacity**
PUCCH F3 supports **maximum** allocation of:
- **14 symbols**
- **16 PRBs**

### **Maximum Bits Calculation**
```
Bits = 2 * 12 (subcarriers) * 12 (data symbols) * 16 (PRBs)
     = 4608 bits (Encoded bits)
```
Using **Code Rate = 0.8**, UCI bits transmitted:
```
UCI Bits ≈ 3600
```
Thus, **PUCCH F3 can carry up to ~3600 UCI bits**.

---
## **5. Frequency Hopping in PUCCH F3**
PUCCH F3 supports **intra-slot frequency hopping**.
- If enabled → Second symbol is **mapped to a different PRB**.
- If disabled → All symbols stay in **same PRB allocation**.

### **Example Allocation with Frequency Hopping**
| Hop Index | Start PRB | PRBs Allocated |
|-----------|-----------|---------------|
| 0         | 0         | 2             |
| 1         | 100       | 2             |

---
## **6. Receiver Processing**
The receiver performs the **inverse operations** of transmission.

### **Steps at gNB Receiver**
1. **Resource Demapping** → Extract DMRS & Data symbols.
2. **Channel Estimation** → Use DMRS to estimate channel.
3. **Equalization** → Apply estimated channel to received data.
4. **Soft Demodulation** → Convert to Log-Likelihood Ratios (LLRs).
5. **Descrambling** → Reverse scrambling process.
6. **Rate Matching & Decoding** → Based on number of UCI bits.
7. **Final UCI Extraction** → Obtain HARQ, SR, and CSI bits.

### **Decoding Path Selection**
| UCI Bits | Decoding Method |
|----------|----------------|
| \(<12\) | Reed-Muller Decoder |
| 12-19   | Polar Decoder with CRC6 |
| \(>19\) | Polar Decoder + CRC11 & Code Block Segmentation |

---
## **7. Real-World Applications in 5G Modem Software**
### **1. Smartphone Uplink Control**
- Qualcomm & MediaTek 5G modems use **PUCCH F3** for **large UCI transmissions**.
- Ensures **reliable CSI reporting** for adaptive scheduling.

### **2. IoT and Industrial 5G**
- Smart factories use **PUCCH F3** for **sensor data transmission**.
- Helps in **low-latency machine-to-machine communication**.

### **3. Autonomous Vehicles (AVs)**
- AVs utilize **PUCCH F3** for **high-precision control feedback**.
- Critical in **real-time vehicle-to-infrastructure (V2I) communication**.

---
## **Conclusion**
PUCCH Format 3 is a **high-capacity** uplink control channel format in **5G NR**, providing:
- **Support for large UCI transmissions (HARQ, SR, CSI)**.
- **Transform Precoding to reduce PAPR**.
- **Flexible modulation (\(π/2\) BPSK and QPSK)**.
- **Intra-slot frequency hopping for reliability**.

Understanding **PUCCH F3 processing, allocation, and reception** is essential for **5G modem software development and optimization**.


---
## Next Topic
### 67. [PUCCH Format 4: Signal Generation, UE Multiplexing and Receiver](Format_4_Signal_Generation_UE_Multiplexing_Receiver.md)
