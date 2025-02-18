# **Understanding RSRP in 5G**

## **Introduction**
RSRP (Reference Signal Received Power) is a key measurement in 5G networks that helps determine the signal strength received by a User Equipment (UE). It is crucial for network performance, signal optimization, and handover decisions in 5G modem software.

---

## **What is RSRP?**
- RSRP stands for **Reference Signal Received Power**.
- It represents the power level of the reference signals received at the UE.
- Unlike other signal measurements, **RSRP does not account for interference or noise**; it purely measures the received signal power.

### **How is RSRP Measured?**
- RSRP is calculated at the **UE side** from the **SSS signal** transmitted by the **gNB (5G base station)**.
- The reference signals used for measurement include:
  - **SS-RSRP**: Derived from Synchronization Signal Block (**SSB**), specifically from **SSS (Secondary Synchronization Signal)**.
  - **CSI-RSRP**: Derived from Channel State Information Reference Signals (**CSI-RS**).
- The measurement does not consider noise or interference but focuses only on the received power.

---

## **How is RSRP Computed?**
- RSRP is the **average received power per Resource Element (RE)** carrying reference signals.
- For **SS-RSRP**, the measurement is performed over **127 Resource Elements (REs)**.
- The calculation follows a linear averaging approach:
  
  ```
  RSRP = (x1 + x2 + ... + x127) / 127
  ```
  
  where `x1, x2, ..., x127` are the received power values in watts.
- The computed value is later **converted to dBm** (decibels per milliwatt) for easier interpretation.

### **Conversion to dBm:**
  ```
  RSRP (dBm) = 10 * log10(RSRP in watts)
  ```

---

## **Why Use dBm Instead of Watts?**
- **Ease of Representation:** Signal power values in watts can be very small (e.g., `0.00000001 W`), making them difficult to interpret. Using dBm provides a more practical scale.
- **Logarithmic Scale Advantage:**
  - Wireless signals experience exponential decay over distance.
  - A logarithmic scale (dBm) helps in better visualization and comparison.
- **Example:**
  - If a UE receives `1 nanowatt (1nW = 0.000000001 W)`, converting to dBm:
    ```
    10 * log10(0.000000001) = -90 dBm
    ```
  - If another UE receives `100 nanowatts (100nW = 0.0000001 W)`, the converted value:
    ```
    10 * log10(0.0000001) = -70 dBm
    ```
  - This shows an easy comparison: -90 dBm is much weaker than -70 dBm.

---

## **RSRP Calculation Example**
### **Step-by-Step Explanation**
Suppose a **User Equipment (UE)** receives **-20 dBm** of power from the **SSB (Synchronization Signal Block)**. The reference signal is spread over **240 subcarriers**. Since RSRP measures the **power per subcarrier**, we need to normalize the total received power across all subcarriers.

### **Formula Used:**
```
RSRP = Total received power - 10 * log10(Number of subcarriers)
```

### **Breaking It Down:**
1. **Total received power:** Given as **-20 dBm** (this is the total power across all subcarriers).
2. **Impact of subcarrier distribution:**
   - The reference signal is spread over **240 subcarriers**.
   - To calculate the per-subcarrier power, we divide the total power by **240** in a logarithmic scale.
   - In dB terms, dividing by **240** is equivalent to subtracting **10 * log10(240)**.
3. **Computing log10(240):**
   ```
   log10(240) ≈ 2.38
   ```
   ```
   10 * log10(240) = 10 * 2.38 = 23.8 dB
   ```
4. **Final Computation:**
   ```
   RSRP = -20 - 23.8
   ```
   ```
   = -43.8 dBm (approximately -44 dBm)
   ```

### **Interpretation:**
- The result means that after adjusting for the **distribution of power across 240 subcarriers**, the **per-subcarrier power** is approximately **-44 dBm**.
- This is the expected **maximum RSRP value**, as it represents the strongest received signal per subcarrier.

---

## **Real-World RSRP Measurement on an iPhone**
- You can check **RSRP values** on an iPhone using **Field Test Mode**:
  1. Dial `*3001#12345#*` and press **Call**.
  2. Navigate to **LTE → Serving Cell Meas**.
  3. Look for **RSRP** value.
  4. If **RSRP > -80 dBm**, you have a strong signal; if **RSRP < -100 dBm**, the signal is weak.

---

## **Conclusion**
- RSRP is a key metric for measuring **signal strength** in 5G networks.
- It helps in **network optimization, handover decisions, and signal quality assessment**.
- Understanding RSRP enables better insights into **5G modem software performance** and network efficiency.

---
## Next Topic
### 85. [RSRQ: Reference Signal Received Quality](RSRQ_Reference_Signal_Received_Quality.md)
