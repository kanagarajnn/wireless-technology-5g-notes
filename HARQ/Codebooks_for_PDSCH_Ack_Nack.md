# HARQ CodeBook Based PDSCH ACK/NACK

## Overview

In 5G networks, **code books** define how **Hybrid Automatic Repeat Request (HARQ) acknowledgments (ACK/NACKs)** are mapped to **physical uplink control channel (PUCCH) resources**. These code books are crucial in determining how techniques like **TDD scheduling** and **downlink (DL) acknowledgment** mapping work. Understanding how these code books function allows for **efficient scheduling and resource utilization** in both uplink (UL) and downlink (DL) transmissions.

---
## 1. What are Code Books in 5G?

### **Purpose of Code Books**
- Code books define the mapping of **downlink transmissions to HARQ feedback**.
- They ensure that HARQ feedback is sent at the correct time and on the correct resources.
- They help in deciding whether **semi-static or dynamic HARQ acknowledgment** allocation is used.

### **How Code Books Function**
- In **TDD frame structure**, certain slots are designated for **DL transmissions** and others for **UL transmissions**.
- HARQ acknowledgment (ACK/NACK) can be scheduled in different **UL symbols** depending on processing capabilities.
- **Code books provide a systematic way to map HARQ feedback to PUCCH resources**.

---
## 2. Code Book Implementation in TDD Frames

### **Understanding TDD Frame Structure**
- A **TDD frame** consists of **downlink slots, uplink slots, and guard periods**.
- The placement of HARQ ACK/NACK in **PUCCH depends on UE processing capabilities**.

### **Example of HARQ ACK/NACK Mapping**
Consider a scenario where:
- **Downlink symbols are scheduled** in one slot.
- The UE must process the **PDSCH (Physical Downlink Shared Channel)** and then send HARQ feedback in the next available **PUCCH resources**.
- Depending on **UE processing time**, the HARQ feedback may be mapped to different **uplink slots**.

**Challenges in Mapping HARQ Feedback:**
- **Processing Delay:** The UE must decode the downlink data and generate ACK/NACK within a limited timeframe.
- **Switching Delay:** The transition from DL reception to UL transmission introduces delay.
- **Multiplexing of Multiple UEs:** More than one UE may be scheduled in the same DL slot, requiring efficient HARQ feedback mapping.

---
## 3. Semi-Static vs. Dynamic Code Books

### **Type 1: Semi-Static Code Books**
- HARQ resources are **pre-allocated** in the UL, regardless of whether a **DL transmission occurs**.
- If a **UE fails to decode PDCCH**, it must still send a NACK as per the semi-static resource allocation.
- **Downside:** Wasted UL resources if no DL data was actually transmitted.

### **Type 2: Dynamic Code Books**
- HARQ resources are **allocated dynamically** based on actual **PDCCH decoding success**.
- The **gNodeB can determine if UE failed to decode PDCCH**, eliminating unnecessary NACKs.
- **More efficient** than semi-static, but requires additional signaling overhead.

### **Example: HARQ ACK/NACK Behavior**
#### **Semi-Static Case:**
1. The **gNodeB transmits PDCCH + PDSCH** to the UE.
2. The **UE fails to decode PDCCH**.
3. As per the semi-static rule, the UE must **still send NACK**.
4. The **gNodeB expects HARQ feedback even if the UE did not decode PDCCH**.

#### **Dynamic Case:**
1. The **gNodeB transmits PDCCH + PDSCH** to the UE.
2. The **UE fails to decode PDCCH**.
3. The **gNodeB detects DTX (Discontinuous Transmission) instead of an explicit NACK**.
4. The gNodeB **does not allocate HARQ resources unnecessarily**.

---
## 4. HARQ Feedback Mapping & Resource Allocation

### **HARQ Mapping Process**
- HARQ ACK/NACK feedback is mapped to **PUCCH or PUSCH resources**.
- The mapping depends on:
  - **Downlink slot offset** (time between DL transmission and UL response).
  - **Number of UEs multiplexed in a DL slot**.
  - **MIMO layers** (more layers = more transport blocks, requiring multiple HARQ bits).
  - **Code Block Group (CBG) or non-CBG based feedback**.

### **Example Calculation of HARQ Feedback Bits**
If:
- **6 downlink slots require ACK/NACK feedback**.
- **4 UEs are multiplexed** in one DL slot.
- **Non-CBG based transmission is used** (1 HARQ bit per transport block).
- **Each UE has 2 transport blocks** (MIMO with 2 layers).

Then:
- **Total HARQ bits required = 6 × 4 × 2 = 48 bits**.
- These bits must be mapped efficiently into **PUCCH resources** using code books.

---
## 5. Conclusion: Importance of Code Books in 5G

- ✅ **Code books define systematic HARQ feedback allocation, optimizing resource usage.**
- ✅ **They help overcome processing and switching delays in TDD systems.**
- ✅ **They ensure efficient multiplexing of multiple UEs in a single downlink slot.**
- ✅ **The choice between semi-static and dynamic allocation affects network efficiency.**

Understanding **5G HARQ code books** is essential for optimizing **modem software** and ensuring high-performance, low-latency communication in **real-world 5G deployments**.



---
## Next Topic
## 99. [Introduction to Timing Advance in 5G – What it is and why it matters](../Timing_Advance/Introduction_to_TA.md)
