# PTRS in 5G NR with Transform Precoding

## Introduction

In **5G NR (New Radio)**, **PTRS (Phase Tracking Reference Signal)** plays a crucial role in mitigating **phase noise**, especially for **high-frequency transmissions** and **high-order modulations** such as **64-QAM and 256-QAM**. In the case of **PUSCH (Physical Uplink Shared Channel)** with **transform precoding (DFT-S-OFDM)**, the **PTRS structure, sequence generation, and resource mapping** differ from the **OFDM case**.

This document provides a detailed explanation of **PTRS for PUSCH with Transform Precoding**, including **signal generation**, **resource mapping**, and **real-world applications in 5G modem software**.

---

## Understanding PTRS in Transform Precoding

### **PTRS in OFDM vs. Transform Precoding**

| Feature               | OFDM-Based PTRS  | Transform Precoding PTRS |
|-----------------------|-----------------|--------------------------|
| **Signal Generation** | Derived from DMRS | Independent PN sequence |
| **Multiplexing**      | Frequency domain mapping | Time domain multiplexing with PUSCH |
| **Purpose**          | Mitigates phase noise in OFDM | Mitigates phase noise in DFT-S-OFDM |
| **Time Density**     | Varies with MCS | Fixed to 1 or 2 |
| **Frequency Density** | PRB-based allocation | Time-domain multiplexed groups |

### **Multiplexing PTRS and PUSCH in Transform Precoding**

In **PUSCH with transform precoding**, **PTRS samples** are **multiplexed in the time domain** **before** they enter the **DFT (Discrete Fourier Transform) module**.

1. **PUSCH and PTRS signals** are **combined in time**.
2. The combined signal is sent through the **DFT** module.
3. The **OFDM modulation** is applied.

### **Group-Based PTRS Multiplexing**

PTRS is formed in **groups**, with:
- **Two possible group sizes:** 2 or 4 samples.
- **Higher PRB allocations → More PTRS groups**.

Example:
- **20 PRBs allocated → 4 PTRS groups**
- **Each group has 2 or 4 PTRS samples**

PTRS follows this **time-domain pattern** before **DFT precoding**:

```
[PUSCH] - [PTRS] - [PUSCH] - [PTRS] - [PUSCH]
```

---

## **PTRS Sequence Generation**

### **Step 1: Generating PN Sequence**
PTRS sequence is generated using a **PN (Pseudo-random Noise) sequence**:

```
S_i = f(n_ID, Slot Number, Symbol Index)
```

where:
- **n_ID** → Cell/UE-specific ID
- **Slot Number** → Slot-dependent sequence
- **Symbol Index** → Ensures uniqueness per symbol

### **Step 2: Pi/2 BPSK Modulation**
The **PN sequence** undergoes **π/2 BPSK (Binary Phase Shift Keying) modulation**:

```
PTRS_Signal = PN_Sequence × exp(j π/2)
```

### **Step 3: Applying Orthogonal Cover Codes**
PTRS symbols are **spread across multiple groups** using **orthogonal cover codes**, which depend on **UE RNTI (Radio Network Temporary Identifier)**:

| Group Size | Orthogonal Sequences |
|------------|----------------------|
| **2 Samples** | `++`, `+-` |
| **4 Samples** | `++++`, `++--`, `--++`, `----` |

Orthogonality ensures **reduced interference** when **multiple UEs** transmit **PTRS** in the **same slot**.

---

## **PTRS Resource Mapping in Transform Precoding**

### **Time-Domain Mapping**
PTRS symbols are **distributed across OFDM symbols** based on **time density**:

- **Time Density = 1:** Every OFDM symbol contains PTRS.
- **Time Density = 2:** Every alternate OFDM symbol contains PTRS.

Example:
```
| Symbol 0 | PTRS  | Symbol 1 | No PTRS  | Symbol 2 | PTRS  | Symbol 3 | No PTRS |
```

### **Frequency-Domain Mapping**
Unlike OFDM-based PTRS, **transform precoding PTRS** follows a **group-based allocation**:

1. **Calculate the number of subcarriers in PUSCH allocation:**

```
M_pusch = PRBs_alloc × 12 (subcarriers per PRB)
```

2. **Determine PTRS placement using the formula:**

```
PTRS_Index = (S × (M_pusch / Group_Size)) + Offset
```

where:
- `S` = Group Index (0 to Total Groups - 1)
- `Group_Size` = 2 or 4 (samples per group)
- `Offset` = Defined offset per UE to avoid collisions

Example:
- **PRBs Allocated:** `20`
- **M_pusch:** `20 × 12 = 240 subcarriers`
- **Group Size:** `4`
- **Calculated PTRS Indices:** `[29, 30], [89, 90], [149, 150], [209, 210]`

```
| PUSCH | PTRS | PUSCH | PTRS | PUSCH |
```

---

## **Impact on Uplink Performance**

### **Why Transform Precoding PTRS Matters?**
- **Mitigates phase noise in DFT-S-OFDM** to ensure **robust uplink transmissions**.
- **Optimized for low-PAPR transmissions** critical in **UE power efficiency**.
- **Enhances reliability** for **256-QAM uplink data transmissions**.

### **Real-World 5G Modem Application**
In a **5G modem**, the **uplink scheduler** dynamically configures **PTRS time/frequency density** based on:
- **Channel conditions** (SNR, interference levels)
- **UE mobility** (fast-moving users → higher time density)
- **Modulation order** (higher MCS → more PTRS symbols)

---

## **Conclusion**

- **PTRS mitigates phase noise**, ensuring **high-performance uplink transmissions**.
- **Transform precoding PTRS differs from OFDM-based PTRS**, using **PN sequences** and **time-domain multiplexing**.
- **Time density and frequency mapping** are dynamically adjusted to optimize **modem performance**.
- **5G modems implement dynamic PTRS allocation** to maximize **data throughput and reliability**.

---

This concludes the discussion on **PTRS in 5G NR with Transform Precoding**. Let me know if you need **further refinements or additional explanations**!


---
## Next Topic
### 82. [PTRS: Receiver Design](Receiver_Design.md)  
