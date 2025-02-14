# **Limited Buffer Rate Matching (LBRM) vs. Full Buffer Rate Matching (FBRM) in 5G Modem Software**

## **Introduction to LBRM and FBRM**

**Rate Matching** ensures that encoded bits fit within the available transmission resources in 5G NR. In **LDPC-based Rate Matching**, there are two approaches:

1. **Limited Buffer Rate Matching (LBRM)**: Uses a reduced buffer size to minimize memory usage and decoding latency.
2. **Full Buffer Rate Matching (FBRM)**: Uses the entire available buffer for increased flexibility.

These methods are crucial for optimizing **Physical Downlink Shared Channel (PDSCH)** and **Physical Uplink Shared Channel (PUSCH)** transmissions in 5G modems.

---
## **Why is LBRM Needed?**

- **PDSCH (Downlink):** LBRM is **mandatory** to reduce **memory requirements** and **decoding complexity** at the **User Equipment (UE)** side.
- **PUSCH (Uplink):** Can use **both LBRM and FBRM**, depending on the configuration.

By limiting the buffer size, LBRM improves efficiency in memory-constrained environments, ensuring lower power consumption and reduced decoding delays.

---
## **How LBRM and FBRM Work in LDPC Rate Matching**

### **1. Circular Buffer Concept**
- **Encoder Output (N bits)** is placed into a **circular buffer**.
- If **repetition** is needed, bits are **read repeatedly** from the buffer.
- If **shortening** is needed, only a subset of bits is **transmitted**.
- **Puncturing is NOT used in LDPC** (unlike Polar codes).

### **2. Buffer Size Impact**
- **LBRM restricts the buffer size** to a fixed, predefined value.
- **FBRM uses the full buffer size**, typically **50 Zc or 66 Zc**, based on the **Base Graph (BG1/BG2) selection**.

---
## **LDPC Base Graph and Code Rate Impact**

| **Base Graph** | **Input Size** | **Output Size** | **Code Rate** |
|--------------|--------------|---------------|------------|
| **BG1** | 22 Zc | 66 Zc | 1/3 |
| **BG2** | 10 Zc | 50 Zc | 1/5 |

- **High Code Rate:** Less impact of buffer size reduction (shortening is used).
- **Low Code Rate:** Performance is affected since more bits need to be repeated.

---
## **Calculating Buffer Size in LBRM**

The buffer size in LBRM is determined by:
- **Modulation Order (Qm)**
- **Number of Layers**
- **Transport Block (TB) Size**

### **Example Calculation:**
1. **Given Parameters:**
   - **PRBs (Physical Resource Blocks):** 25
   - **Layers:** 2
   - **Modulation Order:** 6 (64-QAM)
2. **Lookup Table:**
   - For PRB **25**, Layer **2**, and Qm **6**, the corresponding buffer size is selected.

Similarly, for **PRBs = 250, Layers = 3, Modulation Order = 8 (256-QAM)**, the buffer size is determined based on fixed table values.

- **LBRM:** Uses the **predefined buffer size** from specifications.
- **FBRM:** Uses the **full buffer size** (50 Zc or 66 Zc).

---
## **Real-World Applications in 5G Modems**

### **1. Optimized Downlink Data Transmission (PDSCH - LBRM Mandatory)**
- In **smartphones**, LBRM ensures minimal memory usage and **fast decoding**.
- Used in **high-mobility scenarios** (e.g., 5G in high-speed trains) where low latency is critical.

### **2. Adaptive Uplink Transmission (PUSCH - LBRM/FBRM Configurable)**
- In **IoT devices**, LBRM reduces **power consumption** and processing overhead.
- In **cloud gaming applications**, FBRM can be used to **enhance throughput and reliability**.

---
## **Conclusion**
- **LBRM is mandatory for PDSCH and optional for PUSCH.**
- **FBRM provides more flexibility but requires higher memory and latency.**
- **5G modem software must optimize buffer selection based on use-case requirements.**

Understanding **LBRM and FBRM** is critical for a **Cellular Modem Software Engineer** working on **5G link-level optimizations**.

---
### **Further Reading & References:**
- [3GPP TS 38.212: LDPC Rate Matching](https://www.3gpp.org)

---
## Next Section
### 12. [RV: Redundancy Version and Bit Selection](RV_Redundancy_Version_and_Bit_Selection.md)

