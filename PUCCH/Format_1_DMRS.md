# **PUCCH Format 1: DMRS Generation and Mapping**

## **Introduction**
PUCCH Format 1 (F1) in **5G NR (New Radio)** plays a crucial role in transmitting **uplink control information (UCI)**, such as **ACK/NACK and Scheduling Requests (SR)**. **Demodulation Reference Signal (DMRS)** is essential for accurate decoding of the transmitted signal at the receiver.

In this document, we will explore **DMRS generation, mapping to resources, and its real-world applications in 5G modem software**.

## **DMRS Generation in PUCCH F1**
### **Mathematical Representation**
DMRS follows a **Zadoff-Chu (ZC) sequence**, similar to the data sequence in PUCCH F1. The transmitted sequence is:
```
z(m) = w(m) * y(n)
```
Where:
- `y(n)` = ZC sequence with parameters **u, v, alpha, and delta**
- `w(m)` = **Orthogonal code cover** for UE multiplexing
- `z(m)` = Final sequence mapped to **time-frequency resources**

### **Key Parameters in ZC Sequence Generation**
- **Group Hopping**: Enabled to avoid inter-cell interference
- **Sequence Hopping**: Disabled for PUCCH F1 (`v=0`)
- **Cyclic Shift**: Different values for each symbol

### **Power Scaling in DMRS**
```
A(K, L) = Beta_DMRS * z(m)
```
Where:
- `A(K, L)` = DMRS signal mapped to frequency index `K` and time index `L`
- `Beta_DMRS` = Power scaling factor
- `L` = Symbol index (DMRS appears in symbols `0, 2, 4, …` within PUCCH allocation)

## **DMRS Mapping in PUCCH F1**
### **DMRS vs. Data Symbol Allocation**
PUCCH F1 consists of **alternating DMRS and data symbols**, ensuring **accurate channel estimation**.

#### **Example: PUCCH with 10 Symbols (No Frequency Hopping)**
- **DMRS takes 5 symbols** (index: `0, 2, 4, 6, 8`)
- **Data takes 5 symbols** (index: `1, 3, 5, 7, 9`)

```
| S0 | S1 | S2 | S3 | S4 | S5 | S6 | S7 | S8 | S9 |
|----|----|----|----|----|----|----|----|----|----|
|DMRS|Data|DMRS|Data|DMRS|Data|DMRS|Data|DMRS|Data|
```

### **Effect of Intra-Slot Frequency Hopping**
When **intra-slot frequency hopping is enabled**, symbols are relocated within the allocated PRB.

- **Example: PUCCH with 10 Symbols (Hopping Enabled)**
  - **First half (Symbols 0-4)**: DMRS → `Symbols 0, 1, 2`
  - **Second half (Symbols 5-9)**: DMRS → `Symbols 4, 5`

```
| S0 | S1 | S2 | S3 | S4 | S5 | S6 | S7 | S8 | S9 |
|----|----|----|----|----|----|----|----|----|----|
|DMRS|DMRS|DMRS|Data|DMRS|DMRS|Data|Data|Data|Data|
```

This structure ensures **frequency diversity** and improves **reception accuracy in varying channel conditions**.

## **Real-World Applications in 5G Modem Software**
### **1. Uplink Signal Decoding in Smartphones**
- **Scenario:** A **5G smartphone** sends ACK/NACK feedback for downlink data.
- **PUCCH F1 DMRS** ensures **error-free detection** by **5G base stations (gNB)**.
- **Example:** Qualcomm Snapdragon modems use optimized DMRS structures for **high-speed uplink processing**.

### **2. IoT Devices Using PUCCH F1**
- **Scenario:** Low-power IoT sensors periodically send **Scheduling Requests (SR)**.
- **PUCCH F1 DMRS aids in accurate signal decoding** despite **low transmission power**.
- **Example:** Smart home devices efficiently transmit **uplink control signals** over long distances.

### **3. High-Mobility UEs (Autonomous Vehicles, Drones)**
- **Scenario:** A **moving vehicle** sends uplink control messages while changing cell towers.
- **DMRS with intra-slot frequency hopping** improves **link reliability**.
- **Example:** 5G modems in autonomous vehicles utilize **PUCCH F1 for seamless handovers**.

## **Conclusion**
PUCCH Format 1 DMRS is **critical for accurate uplink signal detection**, utilizing **Zadoff-Chu sequences, orthogonal multiplexing, and frequency diversity**. Its efficient **mapping strategy** ensures **robust control signaling in 5G networks**, particularly in **smartphones, IoT, and high-mobility applications**.




---
## Next Topic
### 61. [PUCCH Format 1: UE Multiplexing and Receiver](Format_1_UE_Multiplexing_Receiver.md)  
