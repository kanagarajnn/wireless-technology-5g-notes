# **Advanced 5G Throughput Calculation**

## **Introduction**
Throughput calculation in **5G** involves multiple factors beyond basic resource allocation. To achieve accurate throughput estimations, we must account for **reference signal overheads, RRC messages, HARQ process efficiency, and BLER (Block Error Rate).**

This document provides a **detailed step-by-step approach** to calculating exact and maximum throughput in **5G NR**, considering real-world parameters relevant to **5G modem software.**

---

## **Factors Affecting Throughput Calculation**
To accurately calculate **5G throughput**, we must consider:
1. **Resource Elements (REs) available for data transmission.**
2. **Reference Signal Overheads:** DMRS, PTRS, CSI-RS.
3. **RRC Message Overheads:** MIB, SIB1, etc.
4. **BLER Target & HARQ Impact.**
5. **TDD Frame Structure & DL/UL Ratio.**
6. **Maximizing throughput by optimizing layers, PRBs, and modulation order.**

---

## **Step 1: Calculating the Total Resource Elements (REs)**

### **Consideration of Reference Signals**
- REs per **PRB** are reduced by **control signals**:
  - **DMRS:** Dedicated pilot signals for channel estimation.
  - **PTRS & CSI-RS:** Additional reference signals affecting resource availability.
- Example:
  - **PTRS & CSI-RS** occupy **4 REs per PRB on average.**
  - Total REs per PRB available = **124** (instead of 128).

**Total REs Calculation:**
```
Total REs = (Available REs per PRB) * (Total PRBs) * (Number of MIMO Layers)
```
For a **100 MHz channel** with **30 kHz subcarrier spacing**:
```
Total PRBs = 273
Total REs = 124 * 273 * 2 (for 2 MIMO layers)
```

---

## **Step 2: Computing Transport Block Size (TB Size)**

### **Using Modulation and Coding Scheme (MCS)**
- Example: **MCS 15** (64-QAM, Code Rate = 666 / 1024)
- Compute the exact **TB size** using **3GPP-defined formulas.**
- For the given RE allocation, **TB Size = 270,576 bits per slot.**

For **Special Slot (S-Slot)**:
- **Reduced number of PDSCH symbols available.**
- Computed TB size: **172,176 bits per slot.**

**Total Bits in a 2.5ms TDD Frame:**
```
Total Bits = (TB Size for D-Slot * 3) + TB Size for S-Slot
           = (270,576 * 3) + 172,176
           = 983,899 bits
```

---

## **Step 3: Convert to Throughput (Mbps)**
Since these bits are for **2.5 milliseconds**, we compute **throughput per second:**
```
Throughput = (983,899 / 2.5ms) * 10^6
           = 393.56 Mbps
```

---

## **Step 4: Adjusting for RRC & HARQ Overhead**

### **Accounting for RRC Message Overhead**
- **Assumption:** **1 out of 20 slots** in a frame is used for **RRC signaling.**
- **Correction Factor:**
```
Throughput_adjusted = Throughput * (19/20)
                   = 393.56 * 0.95
                   = 373.88 Mbps
```

### **Accounting for HARQ & BLER Impact**
- **Target BLER = 10% (i.e., 90% success rate).**
- **Correction Factor:**
```
Throughput_final = Throughput_adjusted * (9/10)
                 = 373.88 * 0.9
                 = 336.49 Mbps
```

Thus, **Physical Layer Throughput = 336.49 Mbps**.

---

## **Step 5: Uplink Throughput Calculation**
- The **same method applies** to **UL throughput calculations**.
- Considerations:
  - **PUCCH Overhead for ACK/NACK feedback.**
  - **PRACH (Random Access) Resource Dedication.**
- Adjust PRACH overhead based on periodicity:
  - Example: **PRACH once every 20 ms** → Adjust throughput accordingly.

---

## **Step 6: Calculating Maximum Theoretical Throughput**

### **Maximizing Resource Allocation**
- **8 MIMO layers (instead of 2).**
- **256-QAM Modulation (MCS 27, Code Rate = 948 / 1024).**
- **Max REs per PRB: 11 * 12 = 132 (after control overheads).**
- **Total REs with 8 layers:**
```
Max REs = 132 * 273 * 8
```
- **Using MCS 27, compute TB size and apply throughput formula.**

### **Modifying TDD Structure for Maximum DL Throughput**
- **Shift 2 UL symbols in Special Slot to DL.**
- **Ensure PDCCH is shared across all slots to reduce overhead.**

### **Final Maximum Throughput Formula:**
```
Max_Throughput = (TB Size for Max Config) / Slot Duration
```
- If **4 carriers (CA) are used**, multiply by **4.**

---

## **Key Takeaways**
- **Accurate 5G throughput requires considering reference signal overheads, HARQ impact, and BLER targets.**
- **TDD structure significantly affects total throughput.**
- **Max throughput is achieved by maximizing layers, PRBs, modulation order, and optimizing scheduling.**
- **Carrier Aggregation (CA) further increases peak throughput.**

---
## Next Topic
### 92. [PAPR: Peak to Average Power Ratio in OFDM](PAPR_Peak_to_Average_Power_Ratio_in_OFDM.md)

