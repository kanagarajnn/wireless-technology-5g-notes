# **Timing Advance Range and Cell Distance in 5G Networks**

## **Introduction**
In wireless communication, the **Timing Advance (TA)** parameter helps the **User Equipment (UE)** determine the correct uplink transmission time to ensure that signals arrive at the **gNodeB (base station)** precisely when expected. The **TA value** is sent from the **gNodeB to the UE** and has a range from **0 to 3846**.

This document explains how to calculate the approximate distance of a **UE from a cell tower** based on the **TA value**, using real-world **5G modem software examples** for better clarity.

---

## **Understanding the TA Value and Distance Calculation**
### **Formula for NTA Calculation**
For a given TA value (T):
```
NTA = (T × 16 × 64) / 2^μ
```
where:
- **μ** is the numerology index corresponding to **subcarrier spacing (SCS)**.
- For **30 kHz SCS (μ = 1)**, the formula simplifies to:
  ```
  NTA = (T × 16 × 64) / 2
  ```
- This gives **NTA in terms of TC (basic time unit in 5G networks).**

### **Propagation Delay in Nanoseconds**
The **TA value (T)** is directly related to the signal travel time:
```
Propagation Delay = (T × 16 × 64) / (480 × 10³ × 4096) seconds
```
For **T = 1**, using **30 kHz subcarrier spacing**:
```
Propagation Delay = 260.42 nanoseconds (round-trip)
```
- **Single-side distance** (from UE to gNodeB):
  ```
  Distance = 39.06 meters
  ```
- **Round-trip distance** (UE → gNodeB → UE):
  ```
  78.13 meters
  ```

---

## **Quick Reference Table for TA and Distance**

| Subcarrier Spacing | TA = 1 Distance (m) | TA = 2 Distance (m) | TA = 50 Distance (km) | TA = 3846 Max Distance (km) |
|-------------------|-------------------|-------------------|------------------|------------------|
| **15 kHz**       | 80 m              | 160 m             | ~2 km           | ~150 km         |
| **30 kHz**       | 40 m              | 80 m              | ~1 km           | ~75 km          |
| **60 kHz**       | 20 m              | 40 m              | ~500 m          | ~37.5 km        |
| **120 kHz**      | 10 m              | 20 m              | ~250 m          | ~18.75 km       |

- **For TA = 1 at 30 kHz**, UE is **~39 meters** from the base station.
- **For TA = 50 at 30 kHz**, UE is approximately **~2 km** from the base station.
- **For TA = 3846 (max value),** UE is at **~150 km** from the base station.

---

## **Practical Application in 5G Modem Software**
### **1. Distance Estimation Using TA in 5G Modems**
- **5G modems (e.g., Qualcomm Snapdragon X65)** use **TA values** to determine the estimated distance of the UE from the **gNodeB**.
- The **TA value is continuously updated** based on **PRACH signals** to ensure synchronization.
- By knowing **TA**, network operators can estimate the **cell radius** and optimize resource allocation.

### **2. Impact of Subcarrier Spacing on TA Quantization**
- **Higher subcarrier spacing (e.g., 120 kHz)** reduces **TA resolution**, meaning a **TA = 1** covers a **shorter physical distance**.
- **Lower subcarrier spacing (e.g., 15 kHz)** provides **better granularity** for TA-based distance measurement.

### **3. Deployment Considerations**
- **Urban areas** use **higher subcarrier spacing (30 kHz, 60 kHz, or 120 kHz)** for **dense networks and small cells**.
- **Rural areas** use **lower subcarrier spacing (15 kHz)** for **wider coverage and better range estimation**.

---

## **Key Takeaways**
1. **TA Value (T) is a key parameter** in determining **UE distance from the base station**.
2. **TA values range from 0 to 3846**, with each **increment corresponding to a fixed distance**.
3. **Distance calculation depends on subcarrier spacing (SCS)**; higher spacing means shorter distances per TA step.
4. **5G modems continuously update TA values** to maintain accurate uplink synchronization.
5. **Operators use TA values to estimate cell range and optimize network performance.**

---

## **Conclusion**
By understanding **TA values and their impact on distance estimation**, 5G networks can effectively manage uplink synchronization and optimize coverage. **Timing Advance is a fundamental parameter** in modern **5G modem software**, ensuring seamless connectivity and efficient network planning.




---
## Next Topic
### 104. [TA Procedures and Reporting in 5G – How UE and gNB handle it](TA_Procedures_and_Reporting.md)  
