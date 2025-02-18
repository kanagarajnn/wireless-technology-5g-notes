# **Understanding ARFCN in 5G**

## **Introduction**
Absolute Radio Frequency Channel Number (**ARFCN**) is a key parameter in **5G wireless communication** that defines the reference frequency for **uplink and downlink transmissions**. It provides a standardized way to specify channel frequencies within a radio frame.

This document explains **ARFCN, its significance, how it maps to frequency values, and real-world applications in 5G modem software**.

---

## **What is ARFCN?**
- **ARFCN stands for Absolute Radio Frequency Channel Number.**
- It is a **numerical identifier** assigned to specific frequency pairs used for transmission and reception.
- The ARFCN values define **where a signal is positioned within the allocated frequency band.**
- **For FDD (Frequency Division Duplex):** Two ARFCNs are assigned (one for uplink, one for downlink).
- **For TDD (Time Division Duplex):** Only **one ARFCN** is assigned, as uplink and downlink share the same frequency.

### **ARFCN and Synchronization Signal Block (SSB)**
- ARFCN is also used to **define the center frequency of the Synchronization Signal Block (SSB)**.
- Each **SSB center frequency** corresponds to a **valid ARFCN value**, making it essential for initial access and synchronization.

---

## **ARFCN Frequency Ranges in 5G**
The 5G **NR ARFCN values** are categorized based on frequency ranges as per 3GPP specifications:

| **Frequency Range (GHz)** | **ARFCN Range** |
|--------------------|---------------|
| **0 – 3 GHz**      | **0 – 599999** |
| **3 – 24.25 GHz**  | **600000 – 2016666** |
| **24.25 – 100 GHz** | **2016667 – 3279165** |

Each **5G frequency band** has an associated **ARFCN range**, meaning a given ARFCN maps directly to a specific frequency.

---

## **Example: ARFCN Calculation for n78 Band**
One of the most commonly used **5G bands** is **n78** (3.3 GHz – 3.8 GHz TDD band).
- **ARFCN range for n78:** **620000 to 653333** (for 15 kHz subcarrier spacing).
- **This range applies to both uplink and downlink**, as **n78 is a TDD band**.

### **How to Calculate the Frequency for a Given ARFCN?**
Given **ARFCN = 643222**, let's calculate its corresponding frequency using the formula:

```
F(REF) = F(REF-Offs) + ΔF(Global) × (N(REF) - N(REF-Offs))
```
Where:
- **F(REF-Offs) = 3 GHz** (Reference offset frequency for this range)
- **ΔF(Global) = 15 kHz** (Subcarrier spacing)
- **N(REF) = 643222** (Given ARFCN value)
- **N(REF-Offs) = 600000** (Base ARFCN value for this range)

Substituting values:
```
F(REF) = 3 GHz + (15 kHz × (643222 - 600000))
       = 3 GHz + (15 kHz × 43222)
       = 3 GHz + 648.33 MHz
       = 3648.33 MHz
```
Thus, **ARFCN 643222 corresponds to 3648.33 MHz**.

### **Mapping to 5G Bands**
- This frequency falls within **both n77 and n78 bands**.
- This dual mapping ensures **flexibility in network deployment**, allowing operators to optimize coverage and performance.

---

## **Step Size in ARFCN**
ARFCNs are assigned **step sizes** that determine valid frequency increments:
- **Step size 1** → ARFCNs increase by **1 kHz increments**.
- **Step size 2** → ARFCNs increase by **2 kHz increments** (aligned with **30 kHz subcarrier spacing**).
- **Step size 20** → ARFCNs increase by **20 kHz increments**.

For example, in a **30 kHz subcarrier spacing** system:
- **Valid ARFCNs:** 620000, 620002, 620004, etc.
- This ensures **proper alignment of frequency grid** with OFDM subcarriers.

---

## **Why is ARFCN Important in 5G Modem Software?**
### **1. Network Synchronization & Cell Selection**
- When a **UE (User Equipment) starts up**, it scans for **SSB ARFCNs** to detect available networks.
- ARFCN helps the UE **lock onto the correct frequency and establish a connection**.

### **2. Handover & Reselection**
- During mobility, the **UE switches between different ARFCNs**.
- Proper ARFCN mapping ensures **seamless handover between cells**.

### **3. Carrier Aggregation (CA) & Dynamic Spectrum Sharing (DSS)**
- **5G modems dynamically select ARFCNs** to maximize spectral efficiency.
- Operators combine multiple ARFCNs to **increase data rates via Carrier Aggregation (CA).**

### **4. Interoperability Between Frequency Bands**
- Some ARFCNs **overlap multiple bands** (e.g., **n77 & n78**), allowing **flexibility in deployment**.
- This helps optimize network coverage across **low-band, mid-band, and high-band spectrums**.

---

## **Key Takeaways**
- **ARFCN uniquely identifies a frequency in 5G networks.**
- **Different ARFCN ranges are defined for FR1 (Sub-6 GHz) and FR2 (mmWave).**
- **ARFCN helps define the center frequency of SSBs, uplink/downlink transmission, and handovers.**
- **Step size determines valid ARFCN increments and alignment with subcarrier spacing.**
- **5G modems use ARFCN for cell selection, carrier aggregation, and dynamic spectrum sharing.**

---

## **Next Topic: Understanding GSCN in 5G**
- In the next section, we will explore **GSCN (Global Synchronization Channel Number)**, which plays a crucial role in **network synchronization and initial access**.

Thank you for reading!



---
## Next Topic
### 88. [GSCN: Global Synchronization Channel Number](GSCN_Global_Synchronization_Channel_Number.md)
