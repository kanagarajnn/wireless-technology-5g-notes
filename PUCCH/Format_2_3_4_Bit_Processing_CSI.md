# **PUCCH Format 2, 3, and 4: Bit Processing**

## **Introduction**
PUCCH Formats 2, 3, and 4 in **5G NR (New Radio)** are designed for transmitting **more than two bits** of **uplink control information (UCI)**. These formats primarily carry:
- **HARQ Acknowledgments (ACK/NACK)**
- **Scheduling Requests (SR)**
- **Channel State Information (CSI)**

Bit processing involves handling **UCI bits from generation to modulation**, including **coding, scrambling, and mapping**. Since this process is similar for all three formats, they are discussed together.

## **Bit Processing Overview**
Bit processing is categorized based on the **number of UCI bits**:
1. **Small block lengths (3 to 11 bits)** → **Reed-Muller coding**
2. **Medium block lengths (12 to 19 bits)** → **Polar coding with CRC-6**
3. **Large block lengths (≥ 20 bits)** → **Code block segmentation with CRC-11**

Each case undergoes:
1. **Encoding**
2. **Rate matching**
3. **Scrambling**
4. **Modulation**

---
## **Bit Processing Steps**
### **1. Small Block Lengths (3 to 11 bits)**
- **No CRC added**
- **Reed-Muller coding** is applied
- Rate matching and modulation (**QPSK**) are performed

### **2. Medium Block Lengths (12 to 19 bits)**
- **CRC-6 is added** to the UCI bits
- **Polar coding** is applied
- Rate matching and modulation (**QPSK**) are performed

### **3. Large Block Lengths (≥ 20 bits)**
- **Code block segmentation** is performed
- **CRC-11 is added** to each code block
- **Polar coding** is applied
- **Rate matching and modulation (QPSK or pi/2-BPSK)**
- **Code block concatenation** is performed before scrambling

---
## **CSI Part 1 and Part 2 Handling**
Channel State Information (CSI) is divided into **two parts:**
- **CSI Part 1** (High-priority information)
- **CSI Part 2** (Lower-priority information)

### **Bit Prioritization**
CSI Part 1 is given priority over CSI Part 2 during bit allocation.
- **If resources are limited**, **only CSI Part 1 is transmitted**.
- **Remaining resources** are allocated to CSI Part 2.

### **Bit Allocation Formula**
```
O_CSI1 = Available Bits for CSI Part 1
O_ACK = Bits for HARQ-ACK
O_SR = Bits for Scheduling Request
R_max = Maximum Code Rate
Q_M = Modulation Order (1 or 2 for QPSK/pi/2-BPSK)
```
The number of bits allocated to CSI Part 1 is calculated as:
```
E_CSI1 = (O_CSI1 + O_ACK + O_SR + L) * R_max * Q_M
```
Remaining bits are allocated to CSI Part 2.

---
## **Resource Allocation and Rate Matching**
The number of modulated bits depends on the **PUCCH format and resource allocation**.

### **PUCCH Format 2 (QPSK Only)**
| Modulation | Symbols | PRBs | Max Bits |
|------------|---------|------|---------|
| QPSK       | 1-2     | 1-16 | 16 bits |

### **PUCCH Format 3 (QPSK or pi/2-BPSK)**
| Modulation | Symbols | PRBs | Max Bits |
|------------|---------|------|---------|
| QPSK       | 4-14    | 1-16 | 168 bits |

### **PUCCH Format 4 (QPSK or pi/2-BPSK)**
| Modulation | Symbols | PRBs | Max Bits |
|------------|---------|------|---------|
| QPSK       | 4-14    | 1-16 | 288 bits |

---
## **Scrambling and Modulation**
After rate matching, bits undergo **scrambling and modulation**:
1. **Scrambling**:
   - Initialization: `C_INIT = nRNTI ⊕ NID`
   - Ensures **randomized bit distribution**
2. **Modulation**:
   - **QPSK or pi/2-BPSK** depending on the format
   - Higher efficiency for larger PUCCH durations

---
## **Bit-to-Resource Mapping**
### **DMRS-Based Prioritization**
UCI symbols are categorized into **three sets**:
1. **Set 1** → Symbols **adjacent to DMRS** (best channel estimates)
2. **Set 2** → Symbols **one step away** from DMRS
3. **Set 3** → Symbols **farther from DMRS**

### **Example: 10-Symbol PUCCH Allocation**
| Symbols | Set | Allocation |
|---------|-----|------------|
| 0, 4, 5, 9 | Set 3 | Lowest priority bits |
| 1, 3, 6, 8 | Set 2 | Medium priority bits |
| 2, 7 | Set 1 | Highest priority bits |

---
## **Real-World Applications in 5G Modem Software**
### **1. High-Priority CSI Reporting in Smartphones**
- **Scenario:** A **5G smartphone** reports CSI to optimize downlink scheduling.
- **PUCCH Format 3/4** enables **large CSI reports with HARQ feedback**.
- **Example:** Qualcomm Snapdragon modems prioritize **CSI Part 1 for optimal scheduling**.

### **2. Low-Latency HARQ Feedback in IoT Devices**
- **Scenario:** An **IoT sensor** transmits HARQ ACK/NACK over **limited uplink resources**.
- **PUCCH Format 2** efficiently delivers **low-latency HARQ feedback**.
- **Example:** Smart meters use **QPSK-based Format 2 for quick uplink signaling**.

### **3. Multi-UE CSI Reporting in Dense Networks**
- **Scenario:** A **5G base station** receives **CSI feedback from multiple UEs**.
- **PUCCH Format 3 multiplexing** ensures **efficient CSI reporting**.
- **Example:** High-density urban networks use **Format 3 for scalable feedback**.

---
## **Conclusion**
PUCCH Formats 2, 3, and 4 handle **larger UCI payloads** efficiently using **bit prioritization, advanced coding, and rate matching**. These formats ensure **reliable uplink signaling**, crucial for:
- **Smartphones (CSI reporting, HARQ feedback)**
- **IoT applications (low-power HARQ/SR transmission)**
- **High-density 5G networks (multi-UE reporting)**

A strong understanding of **bit processing and resource mapping** is essential for optimizing **5G modem software** and ensuring **efficient spectrum utilization**.



---
## Next Topic
### 63. [PUCCH Format 2: DMRS](Format_2_DMRS.md)
