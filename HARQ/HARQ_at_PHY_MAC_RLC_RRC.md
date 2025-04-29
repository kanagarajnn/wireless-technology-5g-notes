# 5G HARQ in Different Layers: Layer 1, Layer 2, and Layer 3

## Overview
**Hybrid Automatic Repeat reQuest (HARQ)** is a key mechanism in 5G networks that ensures data reliability across different layers of communication. It operates at multiple layers: **Physical Layer (Layer 1), Medium Access Control (MAC) Layer (Layer 2), and Radio Resource Control (RRC) Layer (Layer 3).** Each layer plays a specific role in the retransmission process, improving overall efficiency, throughput, and reliability in 5G networks.

---
## 1. HARQ in Layer 1 (Physical Layer)
The **Physical Layer (L1)** is responsible for actual transmission and reception of radio signals. HARQ at this layer ensures efficient use of wireless spectrum by handling data encoding, decoding, and retransmissions at a low latency.

### **Functions of HARQ in Layer 1:**
- **LDPC Encoding & Rate Matching:** The transmitted transport blocks (TBs) go through **Low-Density Parity Check (LDPC) coding** for error correction.
- **Redundancy Versions (RV):** HARQ retransmits failed data using different redundancy versions (RV0, RV1, RV2, RV3) for error correction without resending the entire transport block.
- **Soft Combining:** When a retransmission occurs, the receiver combines new redundancy version data with previously received soft bits to improve decoding success.
- **HARQ Timing:** The Physical Layer handles synchronous and asynchronous HARQ transmissions depending on whether it operates in **Frequency-Division Duplex (FDD)** or **Time-Division Duplex (TDD).**

### **Real-World Example:**
- A user is streaming a 4K video, and the **gNodeB** (base station) transmits data blocks.
- Some blocks fail due to poor signal conditions.
- Instead of retransmitting the entire block, the base station sends a new redundancy version.
- The user’s device (UE) combines the old and new data to recover the lost information without requiring a complete retransmission.

---
## 2. HARQ in Layer 2 (MAC Layer)
The **Medium Access Control (MAC) Layer (L2)** is responsible for managing HARQ retransmissions and scheduling data transmissions efficiently. It plays a critical role in ensuring that retransmissions do not cause excessive delays.

### **Functions of HARQ in Layer 2:**
- **HARQ Process Management:** Up to **16 parallel HARQ processes** can run simultaneously, ensuring continuous data flow while awaiting ACK/NACK responses.
- **HARQ Retransmission Handling:** If a NACK is received, MAC Layer triggers a HARQ retransmission with a new redundancy version.
- **Scheduling Interactions:** The **MAC scheduler** prioritizes data retransmissions to minimize latency and optimize spectral efficiency.
- **Adaptive Modulation and Coding (AMC):** Based on **Channel Quality Indicator (CQI)** feedback, MAC Layer can adjust modulation and coding schemes to improve transmission performance.

### **Real-World Example:**
- A user is in a crowded area, experiencing **network congestion**.
- The MAC Layer decides to delay some HARQ retransmissions due to limited resources.
- The scheduler optimizes bandwidth allocation, ensuring the most critical data gets transmitted first.
- The device (UE) stores soft bits from previous failed transmissions and waits for the next retransmission attempt.

---
## 3. ARQ in Layer 2 (RLC Sub-Layer)
The **Radio Link Control (RLC) Sub-Layer**, a part of Layer 2, provides an additional level of error correction and retransmission above the MAC Layer. While HARQ operates at the MAC Layer, **RLC Automatic Repeat reQuest (ARQ)** complements it by handling retransmissions at a higher layer.

### **Functions of HARQ in RLC:**
- **Error Correction Beyond HARQ:** If HARQ fails multiple times at the MAC Layer, the RLC sub-layer ensures additional retransmissions using ARQ.
- **Segmented Data Retransmissions:** Unlike HARQ, which retransmits entire code blocks, RLC retransmits specific missing segments of the packet, reducing overhead.
- **Buffering and Reordering:** RLC buffers received segments and reorders them before passing complete packets to higher layers.

### **Real-World Example:**
- A user is on a high-speed train moving between different network coverage areas.
- HARQ at the MAC Layer attempts retransmissions, but some packets still fail.
- The RLC layer identifies the missing segments and requests retransmission, ensuring data integrity without retransmitting the entire transport block.

---
## 4. Role of Layer 3 (RRC Layer)
The **Radio Resource Control (RRC) Layer (L3)** handles higher-level retransmission strategies, focusing on persistent errors and overall radio link quality.

### **Functions of HARQ in Layer 3:**
- **Radio Link Control (RLC) and HARQ Coordination:** The RRC Layer monitors persistent HARQ failures and decides when to escalate retransmission requests to a higher level.
- **HARQ Failure Recovery:** If multiple HARQ retransmissions fail, the RRC Layer may trigger a **Radio Link Failure (RLF)** and initiate re-establishment procedures.
- **Interference Management:** The RRC Layer ensures HARQ retransmissions do not interfere with other users in the network by dynamically adjusting power levels and scheduling strategies.
- **Inter-RAT (Radio Access Technology) Coordination:** If HARQ failures persist, RRC may decide to hand over the connection to another RAT, such as LTE, ensuring seamless connectivity.

### **Real-World Example:**
- A user is driving through a tunnel and loses the signal.
- HARQ in **Layer 1 and Layer 2** attempts multiple retransmissions, but they fail.
- The **RRC Layer** detects the failure and initiates a **handover to an LTE network** to maintain connectivity.
- The network switches back to 5G once a stronger signal is detected.

---
## 5. Comparison of HARQ in Different Layers

| Layer  | Function | Key Responsibilities |
|--------|----------|----------------------|
| **L1 (Physical Layer)**  | Fast retransmissions at low latency | LDPC encoding, soft combining, redundancy version selection |
| **L2 (MAC Layer)**  | Manages multiple HARQ processes & scheduling | HARQ process management, adaptive retransmissions, scheduler interaction |
| **L2 (RLC Sub-Layer)**  | Provides additional retransmissions if HARQ fails | Segmented retransmissions, buffering, error correction |
| **L3 (RRC Layer)**  | Handles persistent errors and link recovery | Radio link control, failure handling, inter-RAT handovers |

---
## 6. Conclusion
HARQ operates across different layers in 5G to enhance reliability and efficiency:
- **Layer 1 (Physical Layer):** Manages **fast retransmissions** and soft combining for efficient error correction.
- **Layer 2 (MAC Layer):** Oversees **HARQ process management** and scheduling, ensuring optimal resource utilization.
- **Layer 2 (RLC Sub-Layer):** Provides **higher-level retransmissions** when HARQ at MAC Layer fails.
- **Layer 3 (RRC Layer):** Handles **persistent failures, link recovery, and network handovers** to maintain seamless connectivity.

---
## Next Topic
### 97. [HARQ: CBG Based Transmission](CBG_Based_Transmission.md)

