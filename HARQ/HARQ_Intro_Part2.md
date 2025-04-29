# Understanding HARQ in 5G Modem Software

## Overview
In 5G wireless communication, **Hybrid Automatic Repeat reQuest (HARQ)** plays a crucial role in ensuring reliable data transmission. This document provides a structured explanation of HARQ, how redundancy versions (RV) work, and how parallel HARQ processes improve efficiency in both uplink and downlink communications.

---
## 1. Data Transmission Chain in 5G Modem
### **Downlink and Uplink Chains**
Data transmission follows a well-defined process at the physical layer. When a packet is transmitted, it goes through a series of encoding and modulation steps at the **transmitter** side. On the **receiver** side, the same steps occur but in reverse order for decoding.

### **Code Blocks and Transport Blocks**
- A **transport block** is the complete set of bits that need to be transmitted.
- This transport block is divided into **code blocks** for more efficient transmission and error correction.
- Each transport block undergoes **LDPC (Low-Density Parity Check) encoding**.
- After LDPC encoding, **rate matching** is applied.

---
## 2. Understanding Rate Matching and Redundancy Versions
Rate matching is an essential step in 5G communication to ensure the right amount of data fits within the allocated radio resources.

### **What is Redundancy Version (RV)?**
- The **LDPC encoder** generates systematic and parity bits, which are stored in a **circular buffer**.
- The **rate matching module** picks bits from the circular buffer for transmission based on:
  - **Code rate** (how much redundancy is needed)
  - **Resources allocated** (how many symbols can be used)
  - **Redundancy version (RV)** (which part of the buffer to pick bits from)

| Redundancy Version (RV) | Starting Point in Circular Buffer |
|-------------------------|---------------------------------|
| RV0                    | Start of the buffer            |
| RV1                    | Somewhere after the start      |
| RV2                    | Middle of the buffer          |
| RV3                    | End of the buffer             |

- **RV0 is always used in the first transmission.**
- If decoding fails, a retransmission occurs using RV2, RV3, and then RV1 in a sequence.
- This technique ensures different portions of the encoded data are used for retransmissions, improving decoding success rates at the receiver.

---
## 3. HARQ Process and Soft Combining
### **How HARQ Works**
HARQ allows a receiver to store incorrectly received data and combine it with future retransmissions for better error correction.

- **Initial Transmission (RV0)**: The transmitter sends data with RV0.
- **Receiver Decodes Data**:
  - If successful → Sends an **ACK (Acknowledgment)** to stop further retransmissions.
  - If unsuccessful → Sends a **NACK (Negative Acknowledgment)** to request retransmission.
- **Retransmission with New RV**:
  - The transmitter sends new redundancy bits (RV2, RV3, etc.).
  - The receiver combines the new data with previously received soft bits (stored data) to improve decoding chances.

### **Self-Decodable vs. Non-Self-Decodable RVs**
- **RV0 and RV3 are self-decodable**, meaning they contain enough information to be decoded independently.
- **RV1 and RV2 are not self-decodable**, meaning they need to be combined with previous transmissions.

### **Real-World Example**
- **Scenario**: A user is streaming a 4K video on a 5G network.
- **Transmission**:
  - The base station (gNodeB) transmits packets with RV0.
  - If some packets are lost or corrupted, a retransmission is requested using RV2.
  - The receiver combines the old RV0 data with the new RV2 data for improved decoding.
- **Benefit**: This process prevents re-sending the entire packet, reducing latency and improving efficiency.

---
## 4. Parallel HARQ Processes for Efficient Transmission
### **Why Multiple HARQ Processes?**
- In 5G, **gNodeB (base station) and UE (user equipment)** use up to **16 parallel HARQ processes**.
- This means **16 packets can be transmitted simultaneously** before waiting for ACK/NACK.
- **Benefit**: **Higher throughput and reduced waiting time** for each packet.

### **Handling Delays in HARQ Processing**
- In **Time-Division Duplex (TDD) mode**, there are limited uplink slots.
- The gNodeB may have to wait for an **uplink slot** to receive the ACK/NACK.
- Instead of waiting, it can transmit **new packets (P2, P3, etc.)** in available slots.
- **This increases spectral efficiency and reduces transmission delays.**

### **Example: HARQ in a Video Call**
- **Multiple packets (P1, P2, P3...)** are sent in parallel.
- If P1 fails but P2 and P3 succeed, the receiver stores P2 and P3 while waiting for P1’s retransmission.
- When P1 is successfully received, the entire data is reassembled and passed to higher layers.
- **This approach ensures a smoother and more efficient communication experience.**

---
## 5. Conclusion
HARQ is a critical feature in **5G modem software** that significantly improves data reliability and efficiency. By using **redundancy versions, soft combining, and parallel HARQ processes**, 5G networks ensure:
- **Higher throughput** by allowing multiple parallel transmissions.
- **Lower latency** by avoiding unnecessary retransmissions.
- **Better reliability** by enabling soft combining of failed packets.

Understanding these concepts is crucial for modem software engineers working on 5G implementations, as they directly impact **performance, power consumption, and user experience** in real-world applications.

---
## Next Topic
### 96. [HARQ: HARQ at PHY MAC RLC RRC](HARQ_at_PHY_MAC_RLC_RRC.md)
