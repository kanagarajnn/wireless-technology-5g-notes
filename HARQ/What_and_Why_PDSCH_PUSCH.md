# **Understanding HARQ in 5G**

## **Introduction**
Hybrid Automatic Repeat Request (**HARQ**) is a key mechanism in **5G networks** that enhances **data transmission reliability** and **error correction**. It ensures that data packets are received **correctly** by retransmitting erroneous packets with redundancy versions.

---

## **Why is HARQ Needed?**
In wireless communication, data transmission is susceptible to **noise, interference, and fading**. If a receiver fails to decode a packet, **retransmission** is needed. HARQ enables this process efficiently by:
- **Detecting errors** via **ACK/NACK** feedback.
- **Retransmitting data** selectively.
- **Improving efficiency** using **soft combining techniques**.

### **Example in 5G Modem Software**
1. **UE receives data from gNB**.
2. **UE decodes and checks errors**.
3. **If correct → Sends ACK (Acknowledgement)**.
4. **If incorrect → Sends NACK (Negative Acknowledgement)**.
5. **gNB retransmits using HARQ process**.

---

## **How HARQ Works?**
### **1. HARQ Process in Downlink & Uplink**
- **Downlink HARQ**: gNB transmits data → UE sends **ACK/NACK** via **PUCCH**.
- **Uplink HARQ**: UE transmits data → gNB sends **ACK/NACK** via **PDCCH**.

### **2. HARQ Mechanism**
- The receiver processes data and **stores soft bits**.
- The sender retransmits **modified redundancy versions** (RV).
- Receiver **combines previous and new transmissions** to enhance decoding success.
- HARQ uses **LDPC coding in 5G** for **efficient error correction**.

---

## **Types of HARQ in 5G**
### **1. Synchronous vs. Asynchronous HARQ**
| Type | Description | Used In |
|------|------------|---------|
| **Synchronous HARQ** | Fixed timing between transmission and retransmission. | FR1 (Low Latency Applications) |
| **Asynchronous HARQ** | Flexible retransmission scheduling based on network conditions. | FR2 (mmWave, CA) |

### **2. Adaptive vs. Non-Adaptive HARQ**
| Type | Description | Used In |
|------|------------|---------|
| **Adaptive HARQ** | Modulation & MCS can change on retransmission. | Dynamic Network Conditions |
| **Non-Adaptive HARQ** | Same modulation & MCS on retransmission. | Time-sensitive applications |

---

## **HARQ Process Example in 5G Modem**
### **1. Initial Transmission**
- gNB transmits **Packet P1**.
- UE receives and **processes it**.
- If successful → Sends **ACK**.
- If failure → Sends **NACK**.

### **2. HARQ Retransmission**
- gNB resends P1 with **redundancy version RV1**.
- UE stores **previous failed bits + new data**.
- UE **combines and decodes** the packet.

### **3. Parallel HARQ Processes**
- **Multiple HARQ processes** (Max 16 in 5G).
- Enables **continuous data flow**.
- Avoids waiting for previous packets before sending new ones.

---

## **HARQ in Different 5G Layers**
### **1. HARQ in Physical Layer (PHY)**
- Uses **LDPC coding** for error correction.
- Retransmissions use **different redundancy versions (RV0, RV1, RV2, RV3)**.

### **2. HARQ in MAC Layer**
- Manages **multiple HARQ processes**.
- Handles **scheduling of retransmissions**.
- Supports **16 parallel HARQ processes**.

### **3. HARQ in RLC Layer**
- Works in **AM (Acknowledged Mode)**.
- Provides **additional retransmission if HARQ fails**.

---

## **HARQ Benefits in 5G**
✅ **Enhances Reliability** → Reduces packet loss.
✅ **Minimizes Latency** → Ensures faster retransmissions.
✅ **Optimizes Power Usage** → Reduces redundant transmissions.
✅ **Improves Spectral Efficiency** → Maximizes data throughput.

---

## **Summary**
- **HARQ ensures reliable data transmission** by handling **retransmissions dynamically**.
- **It works in parallel processes**, avoiding **delays between transmissions**.
- **HARQ uses LDPC coding** to enhance **error correction and throughput**.
- **It is critical for 5G modem software** in managing **PHY, MAC, and RLC layer interactions**.

---
## Next Topic
### 94. [HARQ: CBG Based Transmission](CBG_Based_Transmission.md)

