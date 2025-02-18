# **Understanding PAPR in OFDM**

## **Introduction**
Peak to Average Power Ratio (**PAPR**) is a key parameter in **Orthogonal Frequency Division Multiplexing (OFDM)**. High PAPR is a significant issue that impacts **power efficiency and transmission performance** in 5G systems.

This document explains **what PAPR is, why it is a problem in OFDM, and how it affects system performance**, including **real-world applications in 5G modem software**.

---

## **What is PAPR?**
- **PAPR (Peak to Average Power Ratio)** is the ratio of the **peak power** to the **average power** of a signal.
- In mathematical terms:
  ```
  PAPR = 10 * log10 (Peak Power / Average Power)
  ```
- PAPR is measured in **decibels (dB)**.

### **Example Calculation**
- Consider an **OFDM waveform** with:
  - **Peak power = 0.4725**
  - **Average power = 0.125**
- **PAPR Calculation:**
  ```
  PAPR = 10 * log10 (0.4725 / 0.125)
        = 5.78 dB
  ```
- PAPR **varies based on subcarrier allocation** and modulation.

---

## **Why is PAPR a Problem in OFDM?**
- **Power Amplifier (PA) Efficiency Issues**
  - In **OFDM**, signals have **high fluctuations** in power.
  - High PAPR causes **nonlinear distortions** in **power amplifiers (PA)**.
  - This leads to **lower transmission efficiency** and higher energy consumption.

- **Power Amplifier Saturation and Backoff**
  - **PAs operate in a linear region**, providing efficient amplification.
  - If PAPR is **too high**, the amplifier **enters a non-linear region**.
  - To prevent distortion, we must **reduce the input power** (**backoff**), leading to lower output power.

- **Coverage Reduction**
  - A **UE transmitting at 23 dBm** may only transmit **at 20 dBm** due to PAPR.
  - This results in **reduced signal range and weaker coverage**.

### **Graphical Representation of PA Behavior**
- **Linear region:** The **desired** operating range of a PA.
- **Saturation region:** Where the amplifier **distorts** the signal.
- **High PAPR forces operation in a lower power range**, reducing performance.

---

## **Solutions to Reduce PAPR in 5G**
### **1. Use of DFT-S-OFDM (SC-FDMA) in Uplink**
- **DFT-S-OFDM** has a **lower PAPR than conventional OFDM**.
- Reduces power fluctuations, allowing **UE to transmit at higher power levels**.
- Used in **5G NR uplink transmission**.

### **2. π/2 BPSK for Further PAPR Reduction**
- **π/2 BPSK** is introduced in 5G for **even lower PAPR**.
- Helps in **improving UE coverage and reducing power consumption**.

### **3. Clipping and Filtering**
- Removes **high power peaks** at the cost of slight **signal distortion**.

### **4. Peak Windowing**
- Applies **window functions** to smoothen out high peaks.

---

## **Comparing OFDM and DFT-S-OFDM**
### **Complementary Cumulative Distribution Function (CCDF) Comparison**
- **OFDM PAPR:** Higher (~10–12 dB for 99.99% probability).
- **DFT-S-OFDM PAPR:** ~2–3 dB lower than OFDM.
- **Implication:** DFT-S-OFDM enables **higher UE transmission power**, improving **network coverage**.

---

## **Impact of PAPR on 5G Modems**
### **1. PA Design for Higher Efficiency**
- Lower PAPR **improves battery life** in UEs.
- Ensures **better signal strength and reduced power loss**.

### **2. Better Coverage and Uplink Performance**
- **With lower PAPR, UE can transmit at higher power.**
- Extends **coverage area** and **improves reliability**.

### **3. Optimized Carrier Aggregation (CA) and MIMO**
- Lower PAPR **reduces power constraints** in **multi-carrier** and **massive MIMO** scenarios.

---

## **Key Takeaways**
- **High PAPR is a major limitation in OFDM-based wireless systems.**
- **It affects power efficiency and limits PA performance.**
- **5G uplink uses DFT-S-OFDM and π/2 BPSK to reduce PAPR.**
- **Lower PAPR improves UE transmission power and network coverage.**

---

## Next Topic
### 93. [HARQ: What and Why? (PDSCH and PUSCH)](../HARQ/What_and_Why_PDSCH_PUSCH.md) 


