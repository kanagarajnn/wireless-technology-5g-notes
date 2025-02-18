# **Understanding RSRQ in 5G**

## **Introduction**
Reference Signal Received Quality (**RSRQ**) is a crucial metric in **5G networks** that helps determine the quality of the received signal. It is an **extension of RSRP (Reference Signal Received Power)** but provides additional information about **interference and network congestion**. 

RSRQ plays a significant role in **cell selection, cell reselection, and handover decisions** in 5G modem software.

---

## **What is RSRQ?**
- **RSRQ stands for Reference Signal Received Quality**.
- Unlike **RSRP**, which only measures the received signal power, **RSRQ also accounts for interference and overall network quality**.
- RSRQ is used to **determine the usability of a network cell**, especially in congested environments.

### **Key Difference Between RSRP and RSRQ**
| Metric  | Measurement Source | Purpose |
|---------|-------------------|---------|
| **RSRP** | Measures power from **SSS (Secondary Synchronization Signal)** | Indicates signal strength |
| **RSRQ** | Can be measured from any resource, including **SSBurst, PDCCH, or PDSCH** | Indicates signal quality (accounts for interference) |

---

## **How is RSRQ Measured?**
### **RSRQ Formula**
``` 
RSRQ = RSRP / (RSSI / N) 
```
Where:
- **RSRP** = Reference Signal Received Power (measured per RE - Resource Element)
- **RSSI** = Received Signal Strength Indicator (total received power over multiple PRBs)
- **N** = Number of PRBs (Physical Resource Blocks) over which RSSI is measured

### **Explanation of Terms**
- **RSRP** measures the received signal power per **single resource element (RE)**.
- **RSSI** is the total received power across **multiple PRBs**, including noise and interference.
- **RSRQ normalizes RSRP by dividing it by the per-PRB RSSI**, giving a better quality measurement.

---

## **Understanding RSRQ Calculation**
### **Scenario 1: Measuring RSRQ from SSS (Synchronization Signal Block)**
- RSRP is measured from **SSS** (Secondary Synchronization Signal).
- RSSI is calculated as:
  ```
  RSSI = RSRP * 12 * N  (where 12 is the number of subcarriers per PRB)
  ```
- RSRQ formula simplifies to:
  ```
  RSRQ = RSRP / (RSSI / N)

  RSRQ = RSRP / (RSRP * 12 * N / N)

  RSRQ = 1/12
  ```
- Since **RSSI is directly proportional to RSRP in this case**, the result is always:
  ```
  RSRQ = 1/12 ≈ -11 dB
  ```
- This means that **RSRQ calculated from SSS alone is not useful for evaluating interference**, as it remains constant.

### **Scenario 2: Measuring RSRQ from Other PRB Resources**
- Instead of using only SSS, we measure **RSRQ from another set of PRBs**.
- Assume **100 PRBs** are used for RSSI measurement.
- If interference from another gNB (base station) is present, it affects **RSSI**.
- The formula now considers this interference:
  ```
  RSRQ = RSRP / (12 * x)
  ```
  where **x** is the received power per RE from interfering gNBs.
- In dB scale:
  ```
  RSRQ (dB) = RSRP - 10 * log10(12) + 10 * log10(x)
  ```
  - **10 * log10(12) ≈ 11 dB**
  - **10 * log10(x)** depends on interference levels.

---

## **Example RSRQ Calculation**
Let's assume:
- **RSRP = -80 dBm**
- **Interference (10log10(x)) = -100 dBm**
- Applying the formula:
  ```
  RSRQ = -80 - 11 + 100
  ```
  ```
  RSRQ = +9 dB
  ```

### **What Does This Mean?**
- **RSRQ can be positive**, indicating very low interference.
- If interference was higher (e.g., `10log10(x) = -90 dBm`), then:
  ```
  RSRQ = -80 - 11 + 90 = -1 dB
  ```
- A **negative RSRQ** means the network is experiencing high interference and poor quality.

---

## **Why is RSRQ Important in 5G?**
- **RSRP alone does not indicate interference**, but RSRQ does.
- **Used in cell selection and reselection**: Higher RSRQ means better network quality.
- **Helps optimize handovers**: Ensures users switch to a higher-quality cell, not just a stronger signal.

### **Use Cases in 5G Modem Software**
- **Handover Decisions** → A UE will switch to a new cell if **RSRQ is poor**, even if RSRP is strong.
- **Load Balancing** → Operators use RSRQ to distribute traffic efficiently among base stations.
- **Interference Management** → If RSRQ is low, interference mitigation techniques like beamforming are applied.

---

## **RSRQ Value Interpretation**
| **RSRQ (dB)**  | **Signal Quality**        |
|---------------|-------------------------|
| > -3 dB      | Excellent Quality        |
| -3 to -10 dB | Good to Fair             |
| -10 to -15 dB | Poor                     |
| < -15 dB     | Very Poor (High Interference) |

- **Higher RSRQ means better signal quality and lower interference.**
- **Lower RSRQ suggests a congested or noisy network environment.**

---

## **Conclusion**
- **RSRQ provides critical information about network quality beyond just signal strength.**
- **RSRP measures power, while RSRQ evaluates power relative to interference.**
- **5G modem software uses RSRQ for network selection, handovers, and interference management.**
- **A strong RSRP does not always mean good network quality; RSRQ must also be considered.**

---
## Next Topic
### 86. [Sampling Rates in 5G](Sampling_Rates_in_5G.md)
