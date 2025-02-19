# **Timing Advance Quantization in Wireless Communication**

## **Introduction**
In previous discussions, we learned that the **User Equipment (UE)** must send the **uplink signal in advance** to compensate for **propagation delay**, **uplink-to-downlink switching delay**, and **BTS-to-BTS synchronization error**. This advance timing is precisely calculated and communicated to the **UE** by the **gNodeB (base station)**.

However, the actual **Timing Advance (TA) value is not sent directly** from the gNodeB to the UE. Instead, it is **quantized** before transmission, and this quantization depends on the **subcarrier spacing (SCS)**. This document explains how TA quantization works, its impact on 5G modems, and real-world applications.

---

## **Understanding Timing Advance Calculation**
### **Total Uplink Advance Time Formula**
The total advance time that the **UE** applies to its uplink transmission is:
```
Total TA = 2 × Propagation Delay + NTA Offset (Switching & Sync Error)
```
This timing is computed based on **subcarrier spacing** and represented in terms of **TC** (time unit used in 5G).

### **Breaking Down the Formula**
- **NTA (Normalized Timing Advance):**
  ```
  NTA = (2 × Delay) / TC + NTA Offset
  ```
- Expressing in **TC units**:
  ```
  NTA = 13.33 µs / (1 / 480 kHz × 4096) ≈ 262
  ```
- Instead of sending **NTA** directly, gNodeB **quantizes** this value and transmits **ToTA (Timing Advance Index)**:
  ```
  ToTA = (NTA × 64 × 16) / 2^μ
  ```
- Where **μ** is the numerology index related to **subcarrier spacing**.

---

## **Example Calculation: 5G Modem Implementation**
### **Scenario**
- **UE is 2 km from the gNodeB.**
- **Round-trip propagation delay = 13.33 µs.**
- **Subcarrier Spacing = 30 kHz (μ = 1).**

### **Step-by-Step Calculation**
1. Compute **NTA**:
   ```
   NTA = 13.33 µs × (480 kHz × 4096) = 262
   ```
2. Convert **NTA to ToTA**:
   ```
   ToTA = (262 × 64 × 16) / 2^1
        = 262 × 64 × 8
        ≈ 51
   ```
3. **gNodeB sends ToTA = 51 to UE.**
4. UE **recomputes NTA** from ToTA when received:
   ```
   NTA = ToTA × (16 × 64) / 2^μ
        = 51 × (16 × 64) / 2^1
        = 262
   ```
5. **Final Advance Time** applied by the UE:
   ```
   Total TA = (NTA + NTA Offset) × TC
   ```

---

## **Why Is Quantization Needed?**
### **1. Dependency on Subcarrier Spacing (SCS)**
- Different **subcarrier spacings (SCS)** affect **symbol duration** and **cyclic prefix**.
- Higher **SCS means shorter symbol duration**, requiring finer **timing adjustments**.
- Quantization ensures that **TA adjustments are proportionate to the SCS**.

### **2. Impact on Modem Performance**
- **5G modems (e.g., Qualcomm Snapdragon X65)** receive **quantized TA values**.
- The modem **computes precise NTA values** based on the received **ToTA**.
- The UE then **synchronizes uplink transmissions precisely**, ensuring:
  - **Low latency**
  - **Reduced transmission errors**
  - **Efficient power consumption**

---

## **Real-World Implementation in 5G Networks**
### **1. How gNodeB Computes Timing Advance**
- The **gNodeB measures propagation delay** using **PRACH signals** sent by the UE.
- Based on this delay, it computes **NTA** and **quantizes it into ToTA**.
- The **gNodeB transmits ToTA** to the UE in a **MAC control element (TA Command).**

### **2. How UE Uses Timing Advance**
- Upon receiving **ToTA**, the **UE computes NTA** and applies the **correct uplink timing shift**.
- Every subsequent uplink transmission (**PUCCH, PUSCH, SRS**) is **aligned correctly** to avoid:
  - **Interference**
  - **Missed slots**
  - **Synchronization errors**

---

## **Key Takeaways**
1. **Timing Advance ensures uplink transmission synchronization** by compensating for **propagation delay, switching delay, and synchronization errors.**
2. **gNodeB does not send raw NTA values**; it sends **quantized ToTA**, which depends on **subcarrier spacing (SCS)**.
3. **Quantization is necessary** because different **SCS values affect symbol time and cyclic prefix**, requiring tailored TA adjustments.
4. **5G modems dynamically compute the exact TA offset** from the received **ToTA value**, ensuring efficient and precise uplink transmission.
5. **Real-world 5G networks rely on PRACH signals** to measure propagation delay, enabling **adaptive and accurate uplink synchronization**.

---

## **Conclusion**
Timing Advance quantization is a critical feature in **5G networks**, ensuring accurate **uplink synchronization** while optimizing **modem performance**. By **adjusting TA dynamically based on deployment conditions**, 5G modems can **maintain low-latency and high-efficiency communication**, even in challenging network environments.



--- 
## Next Topic
### 103. [Timing Advance - A quick and easy check](Quick_and_Easy_Check.md)
