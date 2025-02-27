# **Understanding TDD Slot Structure in 5G**

## **Introduction**
Time Division Duplex (**TDD**) slot structure in **5G** defines how transmission alternates between **uplink (UL) and downlink (DL) over time**. This configuration determines when data is sent and received, optimizing network efficiency. Different slot formats provide flexibility to balance latency, throughput, and network coverage.

This document explains **TDD slot structures, key parameters influencing slot selection, and real-world applications in 5G modem software**.

---

## **What is TDD Slot Structure?**
- **TDD (Time Division Duplex) slot structure** determines the distribution of **uplink and downlink transmission slots** over time.
- The structure defines:
  - **When to transmit downlink (DL)**.
  - **When to transmit uplink (UL)**.
  - **When to allocate special symbols (S) for switching between DL and UL.**
- TDD slot configuration impacts **latency, cell coverage, throughput, and interference management**.

### **Common TDD Slot Formats**
Some standard TDD slot structures include:
1. **DDDSU** – Downlink-heavy with special symbols for switching.
2. **DDDDDDD.SUU** – A more balanced approach.
3. **DDSUU** – Uplink-heavy, allowing faster UL transmissions.

Each format has a unique **latency profile** and is selected based on network conditions.

---

## **Key Parameters Affecting TDD Slot Structure**
### **1. Latency Considerations (ACK/NACK Timing)**
- **ACK/NACK feedback delay** is a crucial factor in TDD slot design.
- Example:
  - **Format DDDSU:** ACK/NACK sent in **slot 4**.
  - **Format DDDDDDD.SUU:** ACK/NACK sent in **slot 8**, increasing latency.
  - **Format DDSUU:** ACK/NACK can be sent earlier (slot 3), reducing delay.
- **Lower delay means faster communication and better user experience.**

### **2. Cell Size and PRACH Formats**
- **Physical Random Access Channel (PRACH)** has **long and short formats**:
  - **Long PRACH** (2–3 slots) → Used for **large cells (rural areas).**
  - **Short PRACH** (1 slot) → Used for **small cells (urban areas).**
- Slot structure selection must **accommodate PRACH format**.
- Example:
  - **Format DDDSU** does not support long PRACH.
  - **Format DDDDDDD.SUU** can handle long PRACH.

### **3. SSB Beams and Alignment**
- Synchronization Signal Block (**SSB**) must align with **subcarrier spacing**.
- Example:
  - **8 SSB beams require enough consecutive DL slots.**
  - **Format DDDSU allows only 6 beams, while DDDDDDD.SUU allows all 8.**

### **4. Downlink and Uplink Throughput Balance**
- **Network traffic patterns influence slot allocation.**
- **DL-heavy scenario:** More DL slots (e.g., video streaming).
- **UL-heavy scenario:** More UL slots (e.g., cloud uploads).
- **Format DDSUU provides more UL slots**, while **DDDSU favors DL.**

### **5. Special Symbols (S) for Switching**
- **Special symbols act as a guard period** when switching between DL and UL.
- **The number of S symbols depends on:**
  - **Propagation delay (cell size matters).**
  - **UE and gNB switching time.**
- Example:
  - **FR1 (Sub-6 GHz):** UE switching time < 10 µs, gNB < 10 µs.
  - **FR2 (mmWave):** UE switching time < 5 µs, gNB < 5 µs.
- **More S symbols = More overhead, Less efficiency.**

---

## **TDD Slot Format Representation**
- **Format Structure:** `[Number of DL slots] - [Number of S symbols] - [Number of UL slots]`
- Example: **DDDSU → 3 DL, 1 S, 1 UL**.
- **Example from India:** **Fixed TDD format: DDDSU (10D, 2S, 2U).**

---

## **Guard Period and Switching Delay**
### **Why is Guard Period Needed?**
- **Ensures smooth transition between DL and UL.**
- Factors affecting guard period:
  1. **Propagation Delay (Pd)** – Time for DL signal to reach UE.
  2. **Uplink Propagation Delay (Pu)** – Time for UL signal to reach gNB.
  3. **UE Switching Delay** – Time taken for UE to switch from Rx to Tx.
  4. **gNB Switching Delay** – Time taken for gNB to switch from UL to DL.

### **Timing Constraints for Switching**
| Component | FR1 (Sub-6 GHz) | FR2 (mmWave) |
|-----------|----------------|--------------|
| UE Switching Time | < 10 µs | < 5 µs |
| gNB Switching Time | < 10 µs | < 5 µs |
| Base Station Sync Accuracy | < 3 µs | < 3 µs |

- **Larger cell sizes require larger guard periods due to propagation delay.**
- **Small cells require less guard time, optimizing spectrum usage.**

---

## **Base Station to Base Station Interference**
- **TDD synchronization is crucial when two base stations operate in the same frequency.**
- **Sync accuracy must be better than 3 µs** to avoid interference.
- **Improper slot alignment can degrade network performance.**

---

## **Real-World Impact on 5G Modems**
### **1. Optimizing Latency for Real-Time Applications**
- **Low-latency services (e.g., gaming, VR, remote surgery) require fast ACK/NACK feedback.**
- **Choosing the right slot format ensures minimal delay.**

### **2. Efficient PRACH Planning**
- **Operators choose TDD formats based on PRACH type.**
- **Urban microcells favor short PRACH, while rural macro cells require long PRACH.**

### **3. Balancing Downlink and Uplink for Different Use Cases**
- **Streaming (Netflix, YouTube) needs DL-heavy slots.**
- **Cloud backups (Google Drive, iCloud) need UL-heavy slots.**

### **4. Guard Period Optimization for Small Cells vs Large Cells**
- **Large cells need more guard symbols due to high propagation delay.**
- **Small cells can minimize switching time for better spectral efficiency.**

---

## **Key Takeaways**
- **TDD slot structure determines the distribution of UL/DL transmissions.**
- **Key parameters include latency, PRACH format, SSB beam alignment, throughput balance, and guard periods.**
- **Special symbols ensure smooth switching but add overhead.**
- **Larger cells require more guard time due to higher propagation delay.**
- **5G modems must dynamically adjust TDD slot formats for optimal performance.**


---
## Next Topic
### 90. [Quick throughput calculation](Quick_Throughput_Calculation.md)  
