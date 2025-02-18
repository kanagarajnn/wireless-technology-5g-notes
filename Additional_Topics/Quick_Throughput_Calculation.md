# **Understanding 5G Throughput Calculation**

## **Introduction**
Throughput calculation in **5G** is an essential metric that helps in evaluating network performance. The process involves determining the total resource elements allocated, converting those into bits, and finally computing the throughput in bits per second.

This document provides a step-by-step explanation of **5G throughput calculation**, considering key parameters, resource allocations, and real-world applications in **5G modem software**.

---

## **Steps to Calculate 5G Throughput**
The **three main steps** in calculating **5G throughput** are:
1. **Find the total number of resource elements (REs) allocated.**
2. **Convert REs into bits using modulation and coding scheme (MCS).**
3. **Convert the total bits to bits per second (bps).**

Each of these steps is elaborated below.

---

## **Step 1: Finding the Number of Resource Elements (REs)**
- The total number of **REs per slot** depends on:
  - **Bandwidth (e.g., 100 MHz, 50 MHz, etc.).**
  - **Number of Physical Resource Blocks (PRBs).**
  - **Slot duration (1 ms, 500 µs, etc.).**
  - **Number of layers (MIMO layers: 1, 2, 4, or 8).**
- **Exclude control REs** (e.g., PDCCH, DMRS, CSI-RS, PTRS, etc.).
- **Example:** For **100 MHz** bandwidth with **30 kHz subcarrier spacing**, we have:
  ```
  Number of PRBs = 273
  Number of subcarriers per PRB = 12
  Number of OFDM symbols per slot = 14
  ```
  
  **For a single PRB:**
  ```
  REs per PRB = 12 * 14 = 168
  REs excluding DMRS (2 symbols) = 12 * (14 - 2) = 144
  ```
  
  **Total REs across all PRBs:**
  ```
  Total REs = 144 * 273 * Number of Layers
  ```

---

## **Step 2: Convert REs into Bits**
Each **RE** carries bits based on the selected **Modulation and Coding Scheme (MCS)**.

### **MCS Table Consideration**
- Example: **MCS = 15** (from 5G NR MCS table).
  - **Modulation Order = 6** (64-QAM → 6 bits per symbol).
  - **Code Rate = 666 / 1024**.

Using these values:
```
Total Bits = Total REs * Modulation Order * Code Rate
```

For **2 layers**, we substitute:
```
Total Bits = (144 * 273 * 2) * 6 * (666 / 1024)
```

---

## **Step 3: Convert Bits to Throughput (bps)**
- The number of bits calculated above is per **slot**.
- To compute **bits per second**, we consider **slot duration**:
  - **Slot duration = 500 µs (2 slots per ms)**
  - **1 second = 1000 ms = 2000 slots**

```
Throughput (bps) = (Total Bits per Slot) * (Number of Slots per Second)
```

For example:
```
Throughput = (207,345 bits per slot) * (2000 slots per second)
= 414.69 Mbps
```

---

## **Accounting for TDD Format in 5G**
- **TDD (Time Division Duplex) networks** allocate specific slots for UL and DL.
- In **DDDSU format**, only **52 out of 70** OFDM symbols are used for DL.
- **Correction factor:**
```
TDD Correction = (Total DL Symbols) / (Total Available Symbols)
= 52 / 70
```
- Adjusted throughput:
```
Throughput = 414.69 * (52 / 70)
= 308 Mbps
```

---

## **Extending to Multiple Carriers (Carrier Aggregation - CA)**
- **If multiple carriers are used, multiply throughput by the number of carriers.**
- Example:
  - **2 carriers:**
  ```
  Total Throughput = 308 Mbps * 2 = 616 Mbps
  ```

---

## **Exact Throughput Considerations**
While the above method gives an approximate throughput, **real-world throughput** considers:
1. **RRC Message Overhead** (e.g., MIB, SIB1, control signaling).
2. **DMRS and Data Interleaving** (impacting actual data allocation).
3. **CRC Overhead** (cyclic redundancy checks reducing payload size).
4. **Additional Reference Signals (CSI-RS, PTRS).**
5. **Block Error Rate (BLER) Target:**
   - BLER influences actual **PHY-layer throughput**.

---

## **Key Takeaways**
- **Three main steps:** Find total REs, convert REs to bits, convert bits to bps.
- **MCS and code rate impact throughput.**
- **TDD slot format affects available DL symbols.**
- **Carrier aggregation increases overall throughput.**
- **Real-world throughput includes additional overhead and BLER adjustments.**


---
## Next Topic
### 91. [Calculating the exact throughput](Calculating_Exact_Throughput.md) 
