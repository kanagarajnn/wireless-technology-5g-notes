# **PRBs in 5G – Detailed Explanation with Examples**

## **📡 What is a PRB (Physical Resource Block) in 5G?**
A **Physical Resource Block (PRB)** is the smallest unit of frequency-time resource allocation in **5G NR (New Radio)**. It is dynamically assigned by the **MAC scheduler** for **data transmission** between the User Equipment (UE) and the 5G base station (gNB).

### **🛠 PRB Structure**
- **Frequency Domain**: 1 PRB = **12 subcarriers**
- **Time Domain**: PRB allocation is done **per slot** (1 ms) based on network demand.

> **💡 PRBs are dynamically assigned every 1ms to optimize bandwidth and throughput.**

---

## **📏 How Big is 1 PRB in 5G?**
The bandwidth of **1 PRB** depends on the **subcarrier spacing (SCS)** defined by 5G **numerology (µ)**:

| **Subcarrier Spacing (SCS)** | **PRB Bandwidth** | **Usage** |
|-----------------------------|------------------|----------|
| **15 kHz**  | **180 kHz** | LTE-like coverage |
| **30 kHz**  | **360 kHz** | Sub-6 GHz mid-band |
| **60 kHz**  | **720 kHz** | High-speed Sub-6 GHz |
| **120 kHz** | **1440 kHz** (1.44 MHz) | Ultra-high-speed mmWave |

### **Example:**
If a user is assigned **10 PRBs** with **30 kHz SCS**, the total bandwidth =

```
10 PRBs × 360 kHz = 3.6 MHz
```

More PRBs = More Bandwidth = Higher Data Rates 🚀

---

## **🔹 How PRBs are Allocated in a 5G Network?**
### **1️⃣ Frequency Domain Allocation**
- PRBs are assigned from **available bandwidth** based on user demand.
- Wider channels (e.g., **100 MHz bandwidth**) allow more PRBs to be allocated.

### **2️⃣ Time Domain Allocation**
- PRBs are scheduled **every 1ms (1 slot)** to different users.
- **Higher QoS users** (e.g., video streaming) may receive **more PRBs**.

### **3️⃣ Dynamic PRB Assignment by MAC Scheduler**
- The **5G MAC Layer** assigns PRBs dynamically based on:
  - **Signal Strength (SINR)**
  - **Network Load**
  - **QoS Priority**
  - **User Bandwidth Demand**

> **Example:** If a cell has **273 PRBs available** in a **100 MHz channel (15 kHz SCS)**, the scheduler distributes PRBs **among multiple users** every slot.

---

## **📝 PRB Calculation Example**
### **Scenario:**
A 5G user is allocated **50 PRBs** in a **100 MHz channel** with **30 kHz SCS**.

### **Step 1: PRB Bandwidth Calculation**
Each PRB with **30 kHz SCS** has **360 kHz bandwidth**.

```
Total Bandwidth Used = 50 PRBs × 360 kHz = 18 MHz
```

### **Step 2: PRB Data Rate Calculation**
PRB capacity depends on the **modulation scheme (MCS - Modulation and Coding Scheme)**:

| **MCS (Modulation Scheme)** | **Bits per Symbol** | **Data Rate per PRB** |
|-----------------|----------------|----------------------|
| **QPSK (2 bits/symbol)** | Low | ~40 Mbps |
| **16-QAM (4 bits/symbol)** | Medium | ~80 Mbps |
| **64-QAM (6 bits/symbol)** | High | ~120 Mbps |
| **256-QAM (8 bits/symbol)** | Very High | ~160 Mbps |

If **256-QAM** is used:
```
Total Data Rate = 50 PRBs × 160 Mbps = 8 Gbps (theoretical max)
```

📌 **In real-world scenarios, actual data rates are lower due to interference, error correction, and network load balancing.**

---

## **📊 Multi-User PRB Scheduling (Example)**
In a **100 MHz 5G cell**, **273 PRBs are available** with **15 kHz SCS**.

| **User** | **PRBs Allocated** | **Bandwidth Used** |
|---------|-----------------|----------------|
| **User 1 (Good Signal, High Priority)** | 120 PRBs | 43 MHz |
| **User 2 (Moderate Signal, Video Streaming)** | 80 PRBs | 28 MHz |
| **User 3 (Weak Signal, Background Download)** | 50 PRBs | 18 MHz |
| **User 4 (VoIP Call, Low Priority)** | 23 PRBs | 8 MHz |

📌 **PRBs are dynamically reassigned every 1ms to balance throughput & QoS.**

---

## **🛠 Real-World PRB Analysis Using QXDM**
To analyze PRB allocation in a live 5G network, we use **Qualcomm QXDM**:

1️⃣ **Connect a 5G device to QXDM.**  
2️⃣ **Start logging network activity.**  
3️⃣ **Analyze DCI (Downlink Control Information) messages** to check PRB allocation.

📌 **QCAT (Qualcomm Commercial Analysis Toolkit) helps post-process logs to analyze PRB usage trends.**

---

## **🚀 Key Takeaways**
✔ **1 PRB = 12 subcarriers in frequency + a time slot in time domain**.  
✔ **PRBs are dynamically allocated by the MAC scheduler every 1ms**.  
✔ **More PRBs = More bandwidth = Higher speeds**.  
✔ **PRB allocation depends on signal quality, network load, and QoS.**  
✔ **PRBs are distributed across multiple users based on demand.**

---
## Next Section
### 23. [Bandwidth Part (BWP): Concept and Motivation](Bandwidth_Part_BWP_Concept_Motivation.md)

