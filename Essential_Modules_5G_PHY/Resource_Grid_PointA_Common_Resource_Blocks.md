# **Understanding Frequency Mapping in 5G Modem Software**

## **Introduction**
In 5G, the **frequency domain structure** is designed to offer flexibility, efficiency, and support for multiple devices with varying bandwidth capabilities. Unlike LTE, where frequency allocations were relatively rigid, 5G introduces a more dynamic approach to **frequency mapping**, enabling a wide range of use cases, from low-latency applications to high-capacity broadband services.

Understanding how the **frequency axis** is structured in 5G is essential for modem software engineers involved in **resource allocation, scheduling, and spectrum efficiency**.

### **Key Concepts in 5G Frequency Mapping**
1. **Reference Point (Point A)**
2. **Common Resource Blocks (CRBs)**
3. **Resource Grid**
4. **Offset to Carrier**
5. **Carrier Bandwidth and Numerology**

These concepts define how frequency resources are allocated and used efficiently in 5G networks.

---

## **1. Reference Point (Point A)**
### **What is Point A?**
In LTE, the reference point for frequency mapping was the **center of the carrier (DC carrier)**. However, in 5G, the new reference point is called **Point A**.

### **Why was Point A introduced?**
- 5G supports **multiple numerologies** (15kHz, 30kHz, 60kHz, 120kHz, etc.), making a common reference necessary.
- A base station (**gNB**) can support a **large bandwidth (e.g., 100MHz)**, but different UEs (**User Equipment**) may only support **smaller bandwidths (e.g., 20MHz, 40MHz, etc.)**.
- By defining **Point A**, even UEs with limited bandwidth can **connect and operate efficiently**.

### **Example**
- A **100MHz base station** transmits data across a wide frequency range, but a UE that supports only **20MHz** can still synchronize and communicate effectively using **Point A as the reference**.

---

## **2. Common Resource Blocks (CRBs)**
### **Definition**
**Common Resource Blocks (CRBs)** are logical resource blocks used to define **frequency allocations** in 5G. These are numbered **starting from Point A** to provide a structured way of identifying frequency resources.

Each **numerology (subcarrier spacing)** has its own set of **CRBs**, ensuring **consistent resource allocation** across different bandwidths.

### **Example of CRB Numbering**
For **15kHz subcarrier spacing**:
```
CRB 0   CRB 1   CRB 2   ...   CRB N
```
For **30kHz subcarrier spacing**:
```
CRB 0   CRB 1   CRB 2   ...   CRB N
```
Even though the subcarrier spacing differs, the CRB numbering **always starts from Point A**.

---

## **3. Resource Grid**
The **resource grid** represents the **actual frequency resources used for data transmission**.

### **Key Points About Resource Grid**
- The **size of the resource grid** depends on the **bandwidth allocated to the device**.
- **Each numerology and each antenna port** has a separate **resource grid**.
- **Multiple numerologies can be used at the same time**, allowing **efficient multiplexing of different users and services**.

### **Example**
A **100MHz base station** may have:
- A **15kHz resource grid** for users needing **wider coverage**.
- A **30kHz resource grid** for users requiring **high-speed data**.
- A **60kHz resource grid** for **low-latency applications**.

The **resource grid does not start at Point A** but is offset based on the **numerology and carrier bandwidth**.

---

## **4. Offset to Carrier**
### **Definition**
The **offset to carrier** is the difference between **Point A** and the actual starting frequency of the **resource grid**.

This offset ensures that **different numerologies** align correctly within the same bandwidth.

### **Special Case: SSB Transmission**
For **Synchronization Signal Blocks (SSB)**, the offset is called **Offset to Point A**, as it determines where SSB is placed within the grid.

- **For FR1 (Frequency Range 1, sub-6 GHz)**: Offset is defined in **15kHz steps**.
- **For FR2 (mmWave, above 24GHz)**: Offset is defined in **60kHz steps**.

---

## **5. Carrier Bandwidth and Numerology**
5G allows **flexible bandwidth allocation** based on **subcarrier spacing (numerology)**.

| Numerology | Subcarrier Spacing | Typical Use Case |
|------------|-------------------|------------------|
| µ = 0      | 15 kHz            | Large coverage, mobility |
| µ = 1      | 30 kHz            | Medium data rates |
| µ = 2      | 60 kHz            | Higher data rates |
| µ = 3      | 120 kHz           | Low latency, mmWave |
| µ = 4      | 240 kHz           | Ultra-low latency, mmWave |

Each numerology defines a **different resource grid**, and devices can use **multiple numerologies simultaneously**.

---

## **Real-World Applications in 5G Modem Software**
### **1. Dynamic Bandwidth Allocation for UEs**
- A **5G smartphone** that supports only **20MHz bandwidth** can still connect to a **100MHz base station** by using the appropriate **CRBs and resource grid**.
- Example: A **video streaming user** gets allocated more bandwidth dynamically, while an **IoT sensor** gets minimal bandwidth.

### **2. Multi-Numerology Scheduling**
- A **base station** can transmit **multiple subcarrier spacings** in the same **time and frequency**.
- Example: A **low-latency gaming application** may use **120kHz numerology**, while **voice calls** use **15kHz** for broader coverage.

### **3. Carrier Aggregation & Massive MIMO**
- Devices can aggregate **multiple carriers** using different numerologies.
- Example: A **5G modem** in a **fixed wireless access setup** uses both **sub-6 GHz and mmWave** frequencies for better throughput.

### **4. Efficient Frequency Allocation for 5G Base Stations**
- Operators dynamically allocate **frequency resources** using CRBs.
- Example: A **5G cell tower** optimizes bandwidth allocation for urban users vs. rural users.

---

## **Conclusion**
- **Point A is the new reference** in 5G, replacing the DC carrier from LTE.
- **Common Resource Blocks (CRBs) define frequency allocations across numerologies**.
- **Resource grids determine actual data transmission areas**.
- **Offset to Carrier aligns different numerologies within the same bandwidth**.
- **Flexible numerology and bandwidth allocation** allow for optimized performance across different use cases.

Understanding **5G frequency mapping** is critical for **modem software engineers**, as it affects **spectrum efficiency, device compatibility, and network optimization**.


---
## Next Section
### 23. [Bandwidth Part (BWP): Concept and Motivation](Bandwidth_Part_BWP_Concept_Motivation.md)
    
