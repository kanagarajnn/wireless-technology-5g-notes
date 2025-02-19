# 5G Code Block Group (CBG) Based Transmission

## Overview

In 5G, Code Block Group (CBG) based transmission is an optimization technique that enhances data retransmission efficiency. This method improves upon traditional HARQ (Hybrid Automatic Repeat reQuest) by reducing the need to retransmit entire transport blocks when only some parts fail. Instead, **only the failed Code Block Groups (CBGs) are retransmitted**, optimizing network resources and improving performance.

---
## 1. Understanding Code Blocks and Transport Blocks

### **How Data is Processed in 5G Transmission**
- **Transport Block (TB):** A large set of data bits to be transmitted.
- **CRC Attachment:** A **Cyclic Redundancy Check (CRC)** is added to detect errors in transmission.
- **LDPC Encoding:** The TB undergoes **Low-Density Parity Check (LDPC) encoding** for error correction.
- **Segmentation into Code Blocks (CBs):** If the TB is large, it is divided into multiple **Code Blocks (CBs)**.
- **Each CB undergoes CRC, LDPC encoding, and rate matching.**
- The **receiver** follows the reverse process: **LDPC decoding, CRC check, and TB reconstruction.**

### **Traditional HARQ and Its Limitations**
- If **any one CB fails**, the entire **TB is considered failed**, even if the majority of CBs were received successfully.
- This forces retransmission of the entire **TB**, consuming bandwidth unnecessarily.

---
## 2. Code Block Group (CBG) Based Transmission

### **What is CBG?**
- Instead of handling CBs individually, **multiple CBs are grouped together into Code Block Groups (CBGs).**
- Each **CBG has its own CRC**.
- The **ACK/NACK** (Acknowledgment/Negative Acknowledgment) is now reported **per CBG** instead of for the entire TB.

### **How CBG-Based Retransmission Works**
1. **Initial Transmission:**
   - TB is divided into **multiple CBs**, and then **CBs are grouped into CBGs**.
   - Each **CBG is transmitted**.
2. **Error Detection:**
   - The **receiver checks the CRC** for each CBG.
   - If all **CBGs pass**, an **ACK is sent**.
   - If some **CBGs fail**, a **NACK is sent for only those CBGs**.
3. **Retransmission:**
   - The transmitter **only resends the failed CBGs** instead of the entire TB.
   - This reduces bandwidth consumption and improves efficiency.

### **Real-World Example**
- **Scenario:** A user is downloading a **large file** over a 5G network.
- The **TB contains 1,00,000 bits**, divided into **15 CBs**.
- If **only 1 CB fails**, traditional HARQ would require retransmitting all **1,00,000 bits**.
- **CBG-based transmission** retransmits **only the failed CBs**, significantly reducing retransmission overhead.

---
## 3. Trade-Offs and Challenges

### **Increased ACK/NACK Overhead**
- Instead of sending a single **ACK/NACK** for the whole TB, now **one ACK/NACK per CBG is required**.
- For large TBs, this can **increase signaling overhead**.

### **Optimizing the Number of CBGs**
- The number of CBGs **must be chosen carefully** to balance **retransmission efficiency vs. signaling overhead**.
- **3GPP specifications allow 2, 4, 6, or 8 CBGs per TB.**
- Example: A **TB of 3,19,784 bits** can be split into **38 CBs**, which can be **grouped into 8 CBGs**.

---
## 4. Code Block Group Flush Indicator (CBG-FI)

### **What is CBG-FI?**
- A mechanism where the **gNodeB signals the UE** to either:
  - **Keep soft data** from previous failed CBGs (for soft combining).
  - **Flush previous data** and only use new retransmissions.

### **Real-World Example**
- **Streaming a video:**
  - Some packets are lost due to interference.
  - The gNodeB may instruct the UE to **discard old failed packets** (CBG-FI = 1) and only use new data.
  - Or, it may allow **combining of new and old packets** (CBG-FI = 0) for better decoding.

---
## 5. Summary and Benefits

### **Advantages of CBG-Based Transmission**
- ✅ **Reduces retransmission overhead** by only resending failed CBGs.
- ✅ **Optimizes bandwidth usage** in challenging network conditions.
- ✅ **Improves user experience** by lowering latency in retransmissions.
- ✅ **More efficient than traditional HARQ**, especially for large TBs.

### **Key Takeaways**
- **CBG-based HARQ** is a major improvement over **full TB retransmission**.
- Proper **CBG grouping** is essential for **optimal performance**.
- **CBG-FI** adds flexibility by allowing **soft combining or data flushing**.

Understanding and implementing **CBG-based retransmission** can significantly enhance **5G modem performance**, improving both **efficiency and network throughput**.

---
## Next Topic
### 95. [HARQ: Codebooks for PDSCH Ack/Nack](Codebooks_for_PDSCH_Ack_Nack.md)  

