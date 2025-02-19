# **Factors Affecting Uplink Timing in Wireless Communication**

## **Introduction**
In wireless communication, **Timing Advance (TA)** ensures that the **User Equipment (UE)** transmits its **uplink signal** early enough to reach the **gNodeB** at the correct time. However, propagation delay is not the only factor that affects uplink timing. Several other parameters influence when the **UE should transmit**, including **switching delay** and **synchronization errors between base stations**.

This document explains these additional factors with real-world examples related to **5G modem software** to improve clarity and understanding.

---

## **Understanding the Uplink Timing Mechanism**
### **Propagation Delay and Timing Advance**
1. When **gNodeB transmits downlink**, the signal takes time to reach the **UE**.
2. Similarly, when **UE transmits uplink**, the signal takes time to reach the **gNodeB**.
3. If **UE transmits normally**, the **uplink signal arrives late**, causing misalignment and transmission errors.
4. **Timing Advance (TA)** instructs UE to **send its uplink earlier**, ensuring it arrives precisely within the **gNodeB’s reception window**.
5. The required advance transmission time is calculated based on:
   ```
   Time = Distance / Speed of light
   ```
   - Example: For a **2 km distance**, the delay is **6.66 µs**.
   - **Total round-trip delay = 13.33 µs** (uplink + downlink).

---

## **Additional Factors Affecting Uplink Timing**
While **propagation delay** is the primary reason for **timing advance**, other elements influence **when the UE should transmit**:

### **1. Uplink-to-Downlink & Downlink-to-Uplink Switching Time**
- The **radio does not switch instantaneously** between **downlink and uplink** modes.
- When the gNodeB switches from **receiving uplink to transmitting downlink**, it requires **transition time**.
- This **transition period** is known as the **switching delay**.
- Example: In **3GPP specifications (38.104)**, this switching time is defined as:
  - **For FR1:** 10 µs (for sub-6 GHz bands)
  - **For FR2:** 3 µs (for mmWave bands)

### **2. Base Station Synchronization Error**
- In a real-world **5G network**, multiple base stations operate simultaneously.
- If two neighboring base stations (**gNodeB1 and gNodeB2**) are not perfectly synchronized, timing mismatches occur.
- **3GPP allows a maximum synchronization error of 3 µs**.
- This error must be compensated along with **propagation delay and switching delay**.

---

## **Total Uplink Timing Offset Calculation**
Considering all the factors, the **total uplink timing advance (TA)** required by UE is:
```
Total TA = 2 × Propagation Delay + Switching Delay + Synchronization Error
```
### **Example Calculation**
For **FR1 (Sub-6 GHz Bands):**
- **Propagation Delay:** 6.66 µs (for 2 km distance)
- **Switching Delay:** 10 µs
- **Synchronization Error:** 3 µs
- **Total TA = (2 × 6.66) + 10 + 3 = 26.32 µs**

For **FR2 (mmWave Bands):**
- **Propagation Delay:** 6.66 µs (for 2 km distance)
- **Switching Delay:** 3 µs
- **Synchronization Error:** 3 µs
- **Total TA = (2 × 6.66) + 3 + 3 = 19.32 µs**

---

## **Impact on 5G Modem Software**
### **1. Timing Advance Adjustment in 5G Modems**
- **5G modems** (e.g., Qualcomm Snapdragon X65) dynamically adjust TA values in real-time.
- The modem communicates with **gNodeB** to modify **uplink timing** based on:
  - Distance from the base station (propagation delay)
  - Switching time of the radio hardware
  - Base station synchronization errors

### **2. Uplink Transmission Offset (NTA Offset)**
- **3GPP 38.104** defines an offset parameter (**NTA Offset**) that accounts for these delays.
- NTA Offset is calculated as:
  ```
  NTA Offset = (Total TA in µs) × (Sampling Rate in TC)
  ```
- Example:
  - **For FR1 (13 µs delay, 480 kHz sampling rate):**
    ```
    NTA Offset = 13 × 4096 = 53,248 TC
    ```
  - **For FR2 (7 µs delay, 480 kHz sampling rate):**
    ```
    NTA Offset = 7 × 4096 = 28,672 TC
    ```

---

## **Key Takeaways**
1. **Timing Advance (TA)** is **not only based on propagation delay** but also considers:
   - **Switching Delay** (Time taken to switch between uplink and downlink modes)
   - **Base Station Synchronization Errors** (Timing mismatches between neighboring base stations)
2. The **total TA value** is calculated as:
   ```
   Total TA = 2 × Propagation Delay + Switching Delay + Synchronization Error
   ```
3. **5G modems dynamically adjust uplink transmission timing** to ensure that the signal arrives **within the correct reception window**.
4. **NTA Offset** is defined in **3GPP 38.104**, allowing precise compensation for all timing factors.

---

## **Conclusion**
In 5G communication, **uplink transmission timing is influenced by multiple factors**, not just propagation delay.

Modern **5G modem software** ensures **real-time synchronization** by adjusting **Timing Advance dynamically**. This enables **efficient and error-free communication**, even in scenarios where base station synchronization is imperfect.

Understanding these factors helps **optimize 5G modem performance** and ensures a **seamless user experience in high-speed wireless networks**.



---
## Next Topic
### 98. [Timing Advance in TDD vs. FDD – Differences in timing adjustments](TA_in_TDD_vs_FDD.md) 
