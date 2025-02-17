# **PUCCH Format 3 & 4: DMRS Signal Generation and Mapping**

## **Introduction**
Demodulation Reference Signals (**DMRS**) for **PUCCH Format 3 (F3) and Format 4 (F4)** are based on **Zadoff-Chu (ZC) sequences**. The purpose of DMRS is to facilitate **accurate channel estimation** at the **gNB (gNodeB)**, ensuring reliable decoding of **Uplink Control Information (UCI)**.

Since the **DMRS generation and mapping process is similar for both F3 and F4**, they are covered together in this document.

## **DMRS Sequence Generation**
### **Mathematical Representation**
The DMRS sequence is represented as:
```
ru,v^(alpha,delta)(m) = (e^(j*alpha*n)) * (r'u,v(n))
```
Where:
- **ru,v^(alpha,delta)(m)** → The generated ZC sequence
- **alpha** → Cyclic shift applied to the sequence
- **r'u,v(n)** → Base ZC sequence
- **delta** → Always **0** for DMRS in PUCCH

### **Number of Subcarriers for PUCCH F3 & F4**
For **PUCCH F3**, the number of allocated **PRBs (Physical Resource Blocks)** follows:
```
PRBs = 2^alpha2 * 3^alpha3 * 5^alpha5
```
Where **alpha2, alpha3, and alpha5** are non-negative integers.

For **PUCCH F4**, exactly **1 PRB** is allocated.

Thus, the **total subcarriers** used:
- **F3:** Varies depending on PRB allocation (1 to 16 PRBs → 12 to 192 subcarriers)
- **F4:** Fixed at **12 subcarriers**

## **Cyclic Shift Calculation**
### **Alpha Calculation (Cyclic Shift)**
The cyclic shift is determined as:
```
alpha = (2 * pi / 12) * (M0 + NCS) mod 12
```
Where:
- **M0** is the initial cyclic shift (Fixed at **0** for F3, variable for F4)
- **NCS** is derived from the **PN (Pseudo-Random) sequence**

### **PN Sequence for NCS Computation**
```
NCS = sum(2^m * c(slot_number, symbol_number, m)), m = 0 to 7
```
Where **c()** is a PN sequence based on the slot index and symbol number.

## **Group Hopping and Sequence Hopping**
PUCCH DMRS supports **two types of hopping:**
1. **Group Hopping** → Determines **U**, a root sequence index.
2. **Sequence Hopping** → Determines **V**, modifying the ZC sequence.

### **Three Hopping Scenarios**
1. **No Hopping:**
   - `fgh = 0`, `v = 0`
   - Only **fss** determines **U** (derived from `NID mod 30`).

2. **Group Hopping Enabled:**
   - `fgh` is generated from a **PN sequence**
   - `v = 0` (Sequence Hopping Disabled)

3. **Sequence Hopping Enabled:**
   - `v` is generated from a **PN sequence**
   - `fgh = 0` (Group Hopping Disabled)

## **DMRS Resource Mapping**
### **Mapping of Generated Sequence**
1. The DMRS sequence **rl(m)** is mapped **directly** to allocated **PUCCH symbols**.
2. The mapping follows a **bottom-to-top frequency index ordering**.
3. Each **OFDM symbol** has a **unique** DMRS sequence since **alpha** depends on the symbol index.

### **DMRS Symbol Allocation in PUCCH F3 & F4**
- **PUCCH F3:** 1 to 16 PRBs
- **PUCCH F4:** Always **1 PRB**
- **Minimum OFDM symbols:** 4
- **Maximum OFDM symbols:** 14

### **Effect of Frequency Hopping**
| Number of Symbols | Hopping Disabled | Hopping Enabled |
|------------------|----------------|----------------|
| 4               | 1 DMRS Symbol   | 2 DMRS Symbols |
| 5 - 9           | 2 DMRS Symbols  | 2 DMRS Symbols |
| ≥ 10            | 4 DMRS Symbols  | 4 DMRS Symbols |

If **hopping is enabled**, the second DMRS symbol is placed in the **second hop**.

## **Real-World Applications in 5G Modem Software**
### **1. Reliable Channel Estimation for 5G Smartphones**
- **Scenario:** A **5G smartphone** transmits HARQ feedback over PUCCH F3.
- **DMRS ensures accurate channel estimation** for the **gNB**.
- **Example:** Qualcomm Snapdragon modems use **PUCCH DMRS** for efficient control signaling.

### **2. Optimized Resource Utilization in Dense Networks**
- **Scenario:** A **high-density urban 5G network** schedules multiple UEs using **PUCCH F4**.
- **PUCCH F4 DMRS ensures minimal interference while maintaining robust UCI transmission.**
- **Example:** mmWave deployments rely on **PUCCH F4 for short control signals**.

### **3. IoT and Low-Latency Applications**
- **Scenario:** IoT sensors with low-power radios transmit periodic **CSI feedback**.
- **PUCCH DMRS helps the gNB decode control signals from multiple devices.**
- **Example:** Smart meters use **PUCCH F3 DMRS for energy-efficient uplink control.**

## **Conclusion**
PUCCH Formats 3 & 4 **rely on DMRS** for:
- **Accurate channel estimation** using **ZC sequences**
- **Interference mitigation** with **hopping mechanisms**
- **Optimized uplink control signaling** for diverse 5G applications

Understanding **DMRS generation and mapping** in **PUCCH F3 and F4** is crucial for **5G modem software development** and **network optimization**.



---
## Next Topic
### 66. [PUCCH Format 3: Signal Generation, Receiver and More](Format_3_Signal_Generation_Receiver.md)
