# **Control Resource Set (CORESET) in 5G**

## **Introduction**
The **Control Resource Set (CORESET)** is a crucial parameter in **PDCCH (Physical Downlink Control Channel)**. It defines the set of **resources** used for **DCI (Downlink Control Information) transmission**.

To understand CORESET better, we first need to understand **Resource Element Groups (REGs)** and **Control Channel Elements (CCEs)**.

---

## **Fundamental Concepts: REG and CCE**
### **Resource Element Group (REG)**
- **REG = 12 subcarriers (1 PRB) × 1 OFDM symbol**
- **Contains 3 DMRS (Demodulation Reference Signals) and 9 data REs**
- **DCI information is mapped to data REs**

### **Control Channel Element (CCE)**
- **1 CCE = 6 REGs**
- **Each CCE contains 54 data REs (6 REGs × 9 data REs per REG)**
- **CCE allocation varies based on the number of OFDM symbols**:
  - **1 OFDM symbol → 1 CCE spans 6 REGs**
  - **2 OFDM symbols → 1 CCE spans 12 REGs**
  - **3 OFDM symbols → 1 CCE spans 18 REGs**

---

## **Aggregation Level and CCE Allocation**
### **Aggregation Levels in PDCCH**
- **Aggregation Level 1 → 1 CCE**
- **Aggregation Level 2 → 2 CCEs**
- **Aggregation Level 4 → 4 CCEs**
- **Aggregation Level 8 → 8 CCEs**
- **Aggregation Level 16 → 16 CCEs**

The total number of bits transmitted depends on the **aggregation level**:
```[ Total Bits = 54 × Aggregation Level × 2 (QPSK) ]```


---

## **CORESET Allocation in Frequency and Time**
### **Frequency Allocation**
- Defined using a **45-bit frequency bitmap**
- **Each bit represents 6 PRBs**
- **Total possible PRBs = 45 × 6 = 270 PRBs**

Example:
- **8 bits set to 1 → 8 × 6 = 48 PRBs allocated for CORESET**
- Defines **which PRBs** are used for CORESET and which are not

### **Time Allocation**
- CORESET defines the **number of OFDM symbols** allocated (1, 2, or 3 symbols)
- CORESET configuration does **not specify the starting OFDM symbol**

---

## **CCE to REG Mapping in CORESET**
### **Types of Mapping**
1. **Non-Interleaved Mapping**
   - Continuous allocation of REGs to CCEs
   - Used for **interference coordination** between neighboring cells
   - Example: One cell transmits on part of the band, another cell transmits on a different part

2. **Interleaved Mapping**
   - REGs are interleaved across the frequency domain
   - Requires **Bundle Size** and **Interleaver Size**
   - Example:
     - **Bundle Size = 3** → REGs are grouped into **bundles of 3**
     - **Interleaver Size = 2** → Data is divided into **2 groups**, then interleaved

### **Shift Index in CCE Mapping**
- Controls the **frequency shift of CCE allocation**
- Helps distribute control channel elements efficiently

---

## **CORESET Configuration in gNB**
- **A gNB can have up to 12 CORESETs**
- **A single UE can have a maximum of 3 CORESETs per active bandwidth part (BWP)**
- **CORESET 0** is always reserved for **SIB1 DCI**

---

## **Real-World Example in 5G Modem Software**
- **Smartphones use CORESET to locate PDCCH and extract scheduling information**
- **5G base stations dynamically configure CORESET based on network load**
- **Massive MIMO systems leverage interleaved CORESET mapping for efficient resource utilization**

---

## **Conclusion**
- **CORESET defines the resources used for PDCCH transmission**
- **CCE consists of 6 REGs, with each REG containing 12 subcarriers × 1 OFDM symbol**
- **Aggregation levels determine the number of CCEs allocated**
- **Mapping can be Non-Interleaved (continuous) or Interleaved (shuffled for interference management)**

In the next discussion, we will explore **Search Space and its impact on PDCCH decoding**.

**Stay tuned for more insights into 5G technology!** 🚀

---
## Next Section
### 34. [PDCCH: Search Space](PDCCH_Search_Space.md)
