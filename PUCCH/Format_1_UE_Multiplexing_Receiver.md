# **PUCCH Format 1: Data Transmission, UE Multiplexing, and Receiver Design**

## **Introduction**
PUCCH Format 1 (F1) in **5G NR (New Radio)** is responsible for transmitting **uplink control information (UCI)** such as **HARQ (ACK/NACK) and Scheduling Requests (SR)**. This document provides an in-depth understanding of:
- **Data encoding**
- **UE multiplexing techniques**
- **Receiver design for decoding transmitted signals**

## **Data Encoding and Modulation**
PUCCH F1 utilizes different **modulation schemes** based on the number of information bits:
- **1-bit HARQ** → **BPSK Modulation**
- **2-bit HARQ** → **QPSK Modulation**

### **Mapping HARQ and SR to Resources**
Each **UE** is assigned two different resource blocks:
- **One for HARQ feedback**
- **One for SR transmission**

| HARQ & SR Combination | Resource Block | Modulation |
|----------------------|----------------|-------------|
| 1-bit HARQ | HARQ PRB | BPSK |
| 2-bit HARQ | HARQ PRB | QPSK |
| SR Only | SR PRB | BPSK |
| HARQ + SR | SR PRB (if SR=1) else HARQ PRB | BPSK/QPSK |

If **SR is positive**, the HARQ data is transmitted **on the SR resources**.
If **SR is negative**, the HARQ data is transmitted **on the HARQ resources**.

### **gNodeB Detection Logic**
- **If data is found in HARQ PRB** → Only HARQ was transmitted.
- **If data is found in SR PRB** → HARQ and SR were both transmitted.

## **UE Multiplexing in PUCCH F1**
To optimize spectral efficiency, **multiple UEs are multiplexed** within the same PRB using:
1. **Orthogonal Cover Code (OCC)**
2. **Cyclic Shift Separation**

### **Multiplexing Example (4 UEs)**
1. **UE1 & UE2** → Separated using **cyclic shift (M0=0, M0=6)**
2. **UE3 & UE4** → Separated using **OCC (w(m)=[1,1] and [1,-1])**

This ensures that:
- **UE1 & UE3** are orthogonal
- **UE2 & UE4** are orthogonal
- **UE1 & UE2** are uncorrelated due to different cyclic shifts

### **Maximum UE Multiplexing Capacity**
| Parameter | Max UEs |
|-----------|---------|
| **Cyclic Shift** | 12 |
| **OCC (7 Data Symbols)** | 7 |
| **Total Theoretical Capacity** | 84 UEs |

In real deployments, the actual number of multiplexed UEs is lower due to **channel conditions**.

## **Receiver Design for PUCCH F1**
### **Signal Processing at gNodeB**
1. **Receive PRB with multiplexed UE signals**
2. **Estimate channel using DMRS**
3. **Separate UE signals using OCC and cyclic shift techniques**

### **Step-by-Step Receiver Processing**
1. **Channel Estimation**
   - Extract **DMRS symbols** from received PRB
   - Remove **OCC sequences** to separate channel estimates for different UE groups
   - Use **Zadoff-Chu (ZC) sequence properties** to identify cyclic shifts

2. **Data Separation**
   - Remove OCC from received data symbols
   - Apply **ZC sequence multiplication** to extract individual UE signals

3. **Equalization & Demodulation**
   - Use estimated channel information to **remove channel effects**
   - Perform **BPSK/QPSK symbol detection**
   - Decode **HARQ/SR information**

### **Key Assumption in Receiver Design**
The receiver assumes **constant channel conditions** across a **PRB** to maintain signal correlation and efficient separation.

## **Real-World Applications in 5G Modem Software**
### **1. HARQ Feedback in Smartphones**
- **Scenario:** A **5G smartphone** acknowledges a downlink packet.
- **PUCCH F1 transmits the HARQ ACK/NACK** efficiently.
- **Example:** Qualcomm Snapdragon modem optimizes PUCCH processing for **low-latency feedback**.

### **2. SR Transmission in IoT Devices**
- **Scenario:** A **smart sensor** requests uplink resources.
- **PUCCH F1 ensures efficient scheduling requests**.
- **Example:** Smart meters use **low-power uplink control signals**.

### **3. UE Multiplexing in Dense Networks**
- **Scenario:** Hundreds of UEs share limited PUCCH resources.
- **PUCCH F1 multiplexing ensures minimal interference**.
- **Example:** 5G base stations in urban environments leverage **OCC and cyclic shifts for efficiency**.

## **Conclusion**
PUCCH Format 1 provides an **efficient uplink control mechanism** in 5G, enabling:
- **Optimized HARQ and SR transmission**
- **Efficient multiplexing of multiple UEs**
- **Reliable receiver decoding with robust signal separation**

This is **crucial for real-world 5G modem implementations**, particularly in **smartphones, IoT devices, and high-density networks**.



---
## Next Topic
### 62. [PUCCH Format 2/3/4: Bit Processing, CSI Part 1 and Part 2](Format_2_3_4_Bit_Processing_CSI.md)
