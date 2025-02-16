# **Time and Frequency Location of SS Block in 5G**

## **Introduction**
The **Synchronization Signal Block (SS Block)** in 5G is a critical component that aids User Equipment (UE) in detecting and synchronizing with the network. The **time and frequency location** of SS Blocks is governed by several factors, including the **operating band**, **subcarrier spacing**, and **beam index**.

This document provides an in-depth understanding of SS Block positioning in both time and frequency domains.

---

## **Time Domain Location of SS Block**
### **Maximum Number of Beams Based on Operating Band**
- **Below 3 GHz** → Maximum **4 beams** (**Lmax = 4**)
- **Between 3 GHz and 6 GHz** → Maximum **8 beams** (**Lmax = 8**)
- **Above 6 GHz** → Maximum **64 beams** (**Lmax = 64**)

Each **beam corresponds to an SS Block**, and all beams are confined within a **5-millisecond window**.

### **SS Block Periodicity**
The SS Block periodicity can be:
- **5 ms, 10 ms, 20 ms, 40 ms, 80 ms, or 160 ms**.
- The **most commonly used periodicity** is **20 ms**.
- For example, if periodicity = **10 ms**, the SS Blocks are repeated every **10 ms**.

### **Symbol Location of SS Blocks (SSB Cases)**
Each SS Block has a predefined symbol location based on the subcarrier spacing and frequency range.

#### **Case A (15 kHz Subcarrier Spacing - FR1)**
- **SSB Symbol Locations:** 2, 8, 16, 22 (OFDM symbols)
- **Example Transmission in Time Domain:**
  - SSBs at **2, 3, 4, 5** (1st beam)
  - SSBs at **8, 9, 10, 11** (2nd beam)
  - SSBs at **16, 17, 18, 19** (3rd beam)
  - SSBs at **22, 23, 24, 25** (4th beam)

#### **Case B (30 kHz Subcarrier Spacing - FR1)**
- **SSB Symbol Locations:** 4, 8, 16, 20

#### **Case C (30 kHz Subcarrier Spacing - FR1, Alternative Configuration)**
- **SSB Symbol Locations:** 2, 8, 16, 22
- Provides **extra PDCCH symbols** for Ultra-Reliable Low Latency Communication (**URLLC**).

#### **Case D (120 kHz Subcarrier Spacing - FR2)**
- **SSB Symbol Locations:** 4, 8, 16, 20

#### **Case E (240 kHz Subcarrier Spacing - FR2)**
- **SSB Symbol Locations:** 8, 12, 16, 20

---

## **Frequency Domain Location of SS Block**
Unlike LTE, in 5G, the SS Block can be transmitted anywhere in the frequency spectrum.

### **SS Block Frequency Size**
- SS Block occupies **240 subcarriers** (**20 PRBs**).
- It can be positioned anywhere in the spectrum using **two parameters**:
  1. **Offset to Point A** (PRB-based movement)
  2. **kSSB (Subcarrier Offset)** (Subcarrier-based fine tuning)

### **Offset to Point A & kSSB**
- **Offset to Point A:** Defines the starting point in PRBs.
- **kSSB (Subcarrier Offset):** Defines finer movement in subcarriers.
- **Example:**
  - If **Offset to Point A = 30 PRBs** in **15 kHz spacing**, it means **30 PRBs × 15 kHz = 450 kHz offset**.
  - If **kSSB = 10**, it shifts the block **10 × 15 kHz = 150 kHz further**.

### **Frequency Control in FR1 vs FR2**
| Parameter  | FR1 (Subcarrier Spacing: 15 & 30 kHz) | FR2 (Subcarrier Spacing: 60 & 120 kHz) |
|------------|---------------------------------|---------------------------------|
| Offset to Point A | Defined in multiples of **15 kHz** | Defined in multiples of **60 kHz** |
| kSSB | Defined in **15 kHz steps** | Defined in **60/120 kHz steps** |
| kSSB Range | 0 to 23 | 0 to 11 |

---

## **Real-World Example in 5G Modem Software**
- **Smartphones use SS Block scanning to locate the best beam for synchronization.**
- **5G base stations adjust SS Block positions based on network conditions and beamforming needs.**
- **Autonomous vehicles** use SS Block location for **precise and fast synchronization** in **V2X (Vehicle-to-Everything) communication**.

---

## **Conclusion**
- **Time Domain:** SS Blocks are transmitted in a **5 ms window** with a periodicity of **5 to 160 ms**.
- **Frequency Domain:** SS Blocks can be positioned anywhere within the band, controlled by **Offset to Point A** and **kSSB**.
- **Understanding SS Block locations helps optimize network performance and reduce synchronization time in 5G devices.**

In the next discussion, we will explore **GSCN and ARFCN in 5G network deployments**.

**Stay tuned for more insights into 5G technology!** 🚀

---
## Next Section
### 31. [PDCCH: Transmitter Design and DMRS](PDCCH/PDCCH_Transmitter_Design_DMRS.md)
