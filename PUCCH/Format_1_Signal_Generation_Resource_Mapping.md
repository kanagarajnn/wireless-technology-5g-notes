# **PUCCH Format 1: Signal Generation and Mapping**

## **Introduction**
PUCCH Format 1 (F1) is used in **5G NR (New Radio)** for transmitting **uplink control information (UCI)** such as:
- **ACK/NACK** (Acknowledgment/Negative Acknowledgment)
- **Hybrid Automatic Repeat Request (HARQ)**
- **Scheduling Request (SR)**

PUCCH F1 utilizes a **Zadoff-Chu (ZC) sequence** for transmission, ensuring efficient and robust signaling. This document provides an in-depth explanation of **PUCCH F1 sequence generation, mapping to resources, and key real-world applications in 5G modem software.**

## **PUCCH F1 Sequence Generation**
### **Mathematical Representation**
The transmitted sequence `Z(n)` is given by:
```
Z(n) = w(m) * y(n)
```
Where:
- `y(n)` = ZC sequence carrying **modulated UCI information**
- `w(m)` = Orthogonal cover code for **UE multiplexing**

### **Modulation Techniques**
- **1-bit information (ACK/NACK, SR)** → **BPSK**
- **2-bit information (e.g., HARQ-ACK, SR)** → **QPSK**

For **one-bit UCI**, one ZC sequence is transmitted.
For **two-bit UCI**, different phase shifts in QPSK are used.

## **Zadoff-Chu (ZC) Sequence in PUCCH F1**
### **Equation**
```
y(n) = ru,v^(alpha, delta)(n)
```
Where:
- `ru,v(n)` = Zadoff-Chu root sequence
- `e^(j*alpha*n)` = **Cyclic shift** providing frequency diversity
- `alpha` = Function of initial cyclic shift (`m0`) and **pseudo-random NCS**

### **Alpha Calculation**
```
alpha = (m0 + NCS) mod 12
```
Where:
- `m0` = Initial cyclic shift (UE-specific)
- `NCS` = Pseudo-random cyclic shift derived from slot and symbol index

### **Group Hopping and Sequence Hopping**
- **Group Hopping (Enabled by default in PUCCH F1)**:
  - Root sequence **u** is computed as:
  ```
  u = (fgh + fss) mod 30
  ```
  - `fgh` = Function of **slot number and frequency hopping**
  - `fss` = Derived from **NID or Cell ID**
- **Sequence Hopping (Disabled in PUCCH F1)**
  - `v = 0` (fixed for PUCCH F1)

## **Resource Mapping in PUCCH F1**
PUCCH F1 spans **one PRB** and utilizes **4 to 14 OFDM symbols**.

### **Structure of PUCCH F1 PRB Allocation**
```
|----|----|----|----|----|----|----|----|
|DMRS|Data|DMRS|Data|DMRS|Data|DMRS|Data|
|----|----|----|----|----|----|----|----|
```
- **DMRS (Demodulation Reference Signal):** Used for **channel estimation**.
- **Data Symbols:** Carry the modulated UCI information.
- **Intra-slot Frequency Hopping:**
  - **Disabled:** All symbols remain in **one PRB**.
  - **Enabled:** Second hop occurs in **another PRB**.

### **Orthogonal Code Covering for UE Multiplexing**
```
w(m) = e^(j*2*pi*phi(m) / NSF_PUCCH-1)
```
Where `phi(m)` provides **four orthogonal sequences**, enabling **UE multiplexing**.

#### **Example UE Assignments**
1. **UE1** → w(0) = [1,  1,  1,  1]
2. **UE2** → w(1) = [1, -1,  1, -1]
3. **UE3** → w(2) = [1,  1, -1, -1]
4. **UE4** → w(3) = [1, -1, -1,  1]

Each UE is assigned a different sequence for **orthogonal multiplexing**.

## **PUCCH F1 Frequency Allocation**
### **Valid Configurations**
- **4 to 14 OFDM symbols**
- **DMRS on first symbol, every alternate symbol thereafter**

| PUCCH Symbols | DMRS Symbols | Data Symbols |
|--------------|--------------|-------------|
| 4           | 2            | 2           |
| 6           | 3            | 3           |
| 8           | 4            | 4           |
| 10          | 5            | 5           |
| 14          | 7            | 7           |

- **Even number of symbols:** DMRS and Data split equally.
- **Odd number of symbols:** DMRS has one extra symbol.

## **PUCCH F1 in Real-World 5G Modem Software**
### **1. ACK/NACK Transmission in Smartphones**
- **Scenario:** UE receives downlink data.
- **PUCCH F1 transmits ACK/NACK back to gNB**.
- **Example:** Qualcomm Snapdragon modem ensures error-free HARQ feedback using **robust ZC sequences**.

### **2. Scheduling Requests in IoT Devices**
- **Scenario:** Low-power IoT sensors periodically send SR to gNB.
- **PUCCH F1 efficiently handles UCI with minimal resource usage**.
- **Example:** Smart meters use **PUCCH F1 to request uplink resources**.

### **3. Frequency Hopping in High-Mobility UEs**
- **Scenario:** A UE in a **fast-moving vehicle** undergoes frequent **channel variations**.
- **PUCCH F1 with frequency hopping improves reliability**.
- **Example:** 5G modems in **autonomous vehicles** leverage intra-slot frequency hopping for stable communication.

## **Conclusion**
PUCCH Format 1 provides **efficient, robust, and flexible uplink control signaling** using:
- **Zadoff-Chu sequences for modulation**
- **Orthogonal multiplexing for multiple UEs**
- **Frequency hopping for enhanced reliability**

This format plays a crucial role in **5G modem software**, ensuring **low-latency feedback**, **optimized resource utilization**, and **error-resilient signaling** for diverse applications in **smartphones, IoT, and autonomous vehicles**.



---
## Next Section
### 60. [PUCCH Format 1: DMRS](Format_1_DMRS.md)
