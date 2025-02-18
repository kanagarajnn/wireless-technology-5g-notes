# **Understanding Sampling Rates in 5G**

## **Introduction**
Sampling rate is a fundamental concept in **5G wireless communication** that determines how frequently a signal is sampled per second. In 5G systems, sampling rate directly influences **signal transmission, bandwidth utilization, and overall system performance**.

This document provides an **easy-to-understand** explanation of **sampling rates**, their dependency on **subcarrier spacing, bandwidth, and FFT/IFFT size**, and their practical applications in **5G modem software**.

---

## **What is Sampling Rate?**
- **Sampling rate refers to the number of samples taken per second** to digitize an analog signal.
- Mathematically, sampling rate is expressed as:
  ```
  Sampling Rate = Number of Samples / Second
  ```
- **Higher sampling rates provide better signal resolution**, but they also increase processing complexity.
- Example:
  - If a **1 Hz signal** is sampled **4 times per second**, the sampling rate is **4 samples per second**.
  - If a **2 Hz signal** is sampled **12 times per second**, the sampling rate is **12 samples per second**.

---

## **Sampling Rate in 5G**
### **Understanding OFDM Transmission in 5G**
- 5G uses **OFDM (Orthogonal Frequency Division Multiplexing)** for signal transmission.
- Each **OFDM symbol** consists of multiple **subcarriers**, each carrying a **complex modulated value**.
- The sampling rate in **5G depends on:**
  - **IFFT/FFT size**
  - **Subcarrier spacing**
  - **Bandwidth**

### **Example: 5G System with 30 kHz Spacing & 100 MHz Bandwidth**
- **Number of subcarriers:** **3276**
- **IFFT/FFT size:** **4096**
- **Symbol duration:** ```1 / 30 kHz = 33.33 μs```
- **Total samples:** ```4096 samples / 33.33 μs```
- **Sampling rate:**
  ```
  4096 * 30,000 = 122.88 Msps (Mega samples per second)
  ```
- This sampling rate is **higher than the Nyquist rate** and ensures accurate signal reproduction.

---

## **Relation Between Nyquist Rate and 5G Sampling Rate**
- The **Nyquist rate** is the **minimum sampling rate required** to reconstruct a signal without aliasing.
- In 5G, the **Nyquist rate is equal to twice the maximum signal bandwidth**.
- **Example:** For a **100 MHz signal**, Nyquist rate = **200 Msps**.
- However, 5G often uses a **sampling rate higher than Nyquist**, such as **122.88 Msps** instead of **100 Msps**.
- This helps in **better filter design, improved synchronization, and signal estimation**.

---

## **How 5G Defines Sampling Rates?**
5G defines sampling rates based on **subcarrier spacing and FFT/IFFT size**. Different configurations are used for **FR1 (Sub-6 GHz) and FR2 (mmWave)**:

### **Sampling Rate Tables in 5G (3GPP Release 15)**
| Subcarrier Spacing | Bandwidth | FFT Size | Sampling Rate |
|-------------------|-----------|---------|--------------|
| 15 kHz  | 50 MHz  | 4096   | 61.44 Msps |
| 30 kHz  | 100 MHz | 4096   | 122.88 Msps |
| 60 kHz  | 200 MHz | 8192   | 245.76 Msps |
| 120 kHz | 400 MHz | 8192   | 491.52 Msps |

- **FR1 (Sub-6 GHz)** supports **15 kHz, 30 kHz, and 60 kHz spacing**.
- **FR2 (mmWave)** supports **60 kHz and 120 kHz spacing**.
- The choice of **FFT size** determines the **sampling rate**.

---

## **Why Higher FFT Size in 5G?**
- **IFFT/FFT size is usually a power of 2** (e.g., 512, 1024, 2048, 4096, 8192).
- However, **non-standard FFT sizes** like **768, 1536, and 3072** are also used.
- Example:
  - For **60 MHz bandwidth & 30 kHz spacing**, the required FFT size is **2048**.
  - However, **3072** is used instead, increasing the sampling rate by **1.5x**.
- **Advantages of using a larger FFT size:**
  - **Easier filter design** (avoids sharp transitions).
  - **Better synchronization and estimation**.
  - **Higher spectral efficiency**.
- **Disadvantage:** Increased computational complexity for **gNB and UE**.

---

## **Can gNB and UE Use Different Sampling Rates?**
- **Yes!** The **gNB (Base Station) and UE (User Equipment) can operate at different sampling rates**.
- **Why?**
  - The gNB transmits at a **higher bandwidth**, but a UE may operate in a **smaller bandwidth part (BWP)**.
  - Example:
    - **gNB transmits at 100 MHz**, but
    - **UE operates at only 40 MHz** → UE **samples at a lower rate**.
- **gNB does not signal the sampling rate to the UE**, as it's unnecessary for reception.

---

## **Practical Impact on 5G Modem Software**
### **1. Signal Processing & FFT Computation**
- 5G modems must **efficiently compute FFT/IFFT** at different sampling rates.
- Hardware accelerators in **Qualcomm Snapdragon, MediaTek, and Samsung modems** optimize FFT processing.

### **2. Adaptive Sampling for Power Efficiency**
- UE can **adjust sampling rate dynamically** based on:
  - **Network conditions** (e.g., lower bandwidth = lower sampling rate).
  - **Battery life optimization** (reducing sampling rate reduces power consumption).

### **3. Bandwidth Part (BWP) Adaptation**
- 5G allows **Bandwidth Part (BWP) switching**, where **UE operates in smaller bandwidths** dynamically.
- Example:
  - If UE supports **100 MHz bandwidth**, but the network is congested,
  - The UE can **switch to a 40 MHz BWP**, reducing sampling rate and power usage.

---

## **Conclusion**
- **Sampling rate in 5G is influenced by FFT size, subcarrier spacing, and bandwidth.**
- **5G typically samples at a rate higher than the Nyquist rate** for better filter design and synchronization.
- **UE and gNB can have different sampling rates**, allowing flexible network adaptation.
- **Optimizing sampling rate is critical for 5G modem software to balance performance and power efficiency.**


---
## Next Topic
### 87. [ARFCN: Absolute Radio-Frequency Channel Number](ARFCN_Absolute_Radio_Frequency_Channel_Number.md)  
