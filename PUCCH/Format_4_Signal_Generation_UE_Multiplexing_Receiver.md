# **PUCCH Format 4: Signal Generation, UE Multiplexing, and Receiver Design**

## **Introduction**
PUCCH Format 4 (F4) is a **long format** in **5G NR (New Radio)** used for transmitting **uplink control information (UCI)**. Unlike PUCCH Format 0 and 1, F4 supports **spreading and multiplexing** of multiple UEs in a single **Physical Resource Block (PRB)**.

This format is primarily used for:
- **Hybrid Automatic Repeat Request (HARQ) feedback**
- **Scheduling Request (SR)**
- **Channel State Information (CSI) feedback**

PUCCH F4 operates with **Pi/2-BPSK or QPSK modulation** and spans **4 to 14 OFDM symbols**.

---
## **Key Features of PUCCH Format 4**
1. **Supports UE Multiplexing**: Up to **4 UEs** can share the same PRB using **spreading factors (SF = 2 or 4)**.
2. **Spreading for UE Multiplexing**: Uses **orthogonal cover codes (OCC)** to distinguish between UEs.
3. **Transform Precoding**: Reduces **Peak-to-Average Power Ratio (PAPR)**, making transmission more power-efficient.
4. **Fixed PRB Allocation**: Always uses **one PRB** but can span **4 to 14 OFDM symbols**.
5. **Supports HARQ, SR, and CSI transmission**.
6. **Maximum Transmission Capacity**: Can send **up to 115 UCI bits** (depending on modulation and code rate).

---
## **Signal Generation Process in PUCCH Format 4**
The PUCCH F4 signal generation consists of **several processing steps**:

### **1. Bit Processing**
Before transmission, **UCI bits** go through several encoding steps:
- **CRC Attachment** (if bits ≥ 12)
- **Polar Encoding**
- **Rate Matching** (adjusts encoded bits to match available REs)
- **Scrambling** (adds security & reduces interference)
- **Modulation** (Pi/2-BPSK or QPSK)

### **2. Spreading and UE Multiplexing**
- **Spreading Factor (SF)**: Determines how many UEs can share a single PRB.
- **SF = 2** → **2 UEs** can be multiplexed.
- **SF = 4** → **4 UEs** can be multiplexed.

Each UE is assigned an **orthogonal spreading sequence (wn)**:
| UE Index | SF = 2 (OCC) | SF = 4 (OCC) |
|----------|-------------|-------------|
| UE 1     | [1, 1]      | [1, 1, 1, 1]|
| UE 2     | [1, -1]     | [1, j, -1, -j]|
| UE 3     | -           | [1, -1, 1, -1]|
| UE 4     | -           | [1, -j, -1, j]|

Each UCI bit is **spread** and **repeated** across **multiple subcarriers**, ensuring separation in the frequency domain.

### **3. Transform Precoding (DFT Spreading)**
- **Purpose**: Reduces **PAPR** and improves power efficiency.
- **Process**:
  - Apply **Discrete Fourier Transform (DFT)** to **spreading output**.
  - The resulting frequency-domain signal is mapped to **PUCCH symbols**.

### **4. Resource Mapping**
PUCCH F4 **allocates symbols** as follows:
- **DMRS symbols**: Used for channel estimation.
- **Data symbols**: Carry actual UCI information.
- DMRS and data **alternate** to ensure robust transmission.

| PUCCH Length | DMRS Positions |
|-------------|----------------|
| 4 symbols   | 1st symbol only |
| 5-9 symbols | 1st & 3rd symbols |
| ≥10 symbols | 1st, 3rd & additional symbols |

**Example:**
- If **PUCCH has 14 symbols**, DMRS is at **symbols 3 & 10**, while data occupies the remaining slots.

---
## **PUCCH F4 Receiver Design**
At the **gNB (5G Base Station)**, the received PUCCH F4 signal is processed as follows:

### **1. Channel Estimation**
- Extract **DMRS symbols**.
- Use known **Zadoff-Chu (ZC) sequences** to estimate **channel response**.

### **2. Equalization**
- Apply **inverse channel response** to received data symbols.
- Helps remove channel distortion.

### **3. Despreading (UE Separation)**
- Since multiple UEs share the same PRB, **orthogonal cover codes (OCC)** are used to separate them.
- **Example**:
  - If **2 UEs** are multiplexed, the receiver applies **[1, -1] & [1, 1]** to extract each UE’s signal.
  - If **4 UEs**, spreading factors **[1, j, -1, -j]** are used for further separation.

### **4. Reverse Processing**
- **Inverse Transform Precoding (IDFT)**
- **Soft Demodulation**
- **Descrambling**
- **Polar Decoding**
- **CRC Removal**

Once all processing is complete, the **UCI bits** are successfully retrieved.

---
## **Real-World Applications in 5G Modem Software**
PUCCH Format 4 is widely used in various **5G applications**, including:

### **1. Smartphone Uplink Control**
- Used in **Qualcomm Snapdragon 5G modems** for transmitting **HARQ feedback** and **CSI reports**.
- Ensures **efficient scheduling** of downlink and uplink transmissions.

### **2. IoT & Low-Power Devices**
- **NB-IoT and LTE-M** devices use PUCCH F4 for **lightweight control signaling**.
- Lower power consumption due to **PAPR reduction via Transform Precoding**.

### **3. Autonomous Vehicles & V2X Communication**
- Ensures **low-latency transmission** of control signals in **connected cars**.
- Used for **reliable HARQ feedback** in safety-critical applications.

---
## **Summary of PUCCH Format 4**
| Feature | Details |
|---------|---------|
| **Symbol Length** | 4 to 14 OFDM symbols |
| **Frequency Allocation** | Always uses **1 PRB** |
| **Multiplexing** | Up to **4 UEs** (using OCC) |
| **Modulation** | Pi/2-BPSK, QPSK |
| **DMRS Type** | Zadoff-Chu sequence |
| **Maximum UCI Bits** | ~115 bits (with high code rate) |
| **Power Efficiency** | **Transform Precoding** reduces PAPR |

---
## **Conclusion**
PUCCH Format 4 is a **highly efficient uplink control channel** in **5G NR**, designed for **multi-UE multiplexing** and **optimized power transmission**. It provides:
- **Orthogonal spreading** for multiple UE transmissions.
- **Efficient modulation** (Pi/2-BPSK & QPSK) for flexible deployments.
- **Robust signal processing** using DMRS and transform precoding.

Understanding **PUCCH F4 signal generation, UE multiplexing, and receiver design** is essential for developing **5G modem software**, ensuring seamless UE-gNB communication in **modern wireless networks**.

---
## Next Topic
### To be Added Soon
