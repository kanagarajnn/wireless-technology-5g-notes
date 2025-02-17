# **PUCCH Format 2: Resource Allocation and Receiver Design**

## **Introduction**
PUCCH Format 2 (F2) in **5G NR (New Radio)** is a **short format** used for **uplink control information (UCI)** transmission. Unlike **PUCCH Format 0 and 1**, **F2 does not support UE multiplexing**, meaning each **UE must use a separate frequency resource** when transmitting using F2.

PUCCH F2 carries:
- **HARQ Acknowledgments (ACK/NACK)**
- **Scheduling Requests (SR)**
- **CSI Part 1** (but **not CSI Part 2**)

This document provides **detailed insights into resource allocation, frequency hopping, and receiver design** for PUCCH F2.

## **PUCCH F2 Characteristics**
- **Modulation:** QPSK only
- **Number of OFDM Symbols:** 1 or 2 (Short Format)
- **PRB Allocation:** 1 to 16 PRBs
- **Coding Rate:** 0.08 to 0.8 (adjustable based on channel conditions)

## **Resource Allocation in PUCCH F2**
### **Basic Resource Allocation**
The smallest PUCCH F2 allocation consists of:
- **1 symbol and 1 PRB** → 8 Resource Elements (REs) → **16 bits (QPSK modulation)**
- **Maximum allocation:** 2 symbols and 16 PRBs → **512 bits**

### **DMRS and Data Interleaving**
- **PUCCH F2 interleaves** **DMRS and data REs** in each PRB.
- **Each PRB contains** **8 data REs** and **4 DMRS REs**.
- **Higher PRB allocations** allow more UCI bits to be transmitted.

### **Example PRB Allocations**
| PRBs | Symbols | Total REs | Modulation | Max Bits |
|------|---------|------------|------------|------------|
| 1    | 1       | 8          | QPSK       | 16         |
| 4    | 2       | 64         | QPSK       | 128        |
| 16   | 2       | 256        | QPSK       | 512        |

## **Frequency Hopping in PUCCH F2**
- **If frequency hopping is enabled**, the second OFDM symbol is transmitted at a **different frequency location**.
- **Example:**
  - **Start PRB = 0, Second hop PRB = 100**
  - **First hop PRB: 0,1** (2 PRBs)
  - **Second hop PRB: 99,100**

If **frequency hopping is disabled**, both symbols remain in the **initial PRB allocation**.

## **Adaptive Resource Allocation for UEs**
- **Poor channel conditions → Lower code rate + Higher PRB allocation**
- **Good channel conditions → Higher code rate + Lower PRB allocation**

## **Receiver Design for PUCCH F2**
### **Step 1: Channel Estimation**
- **DMRS REs** are extracted first.
- Channel estimates are applied for **equalization**.

### **Step 2: Data Processing**
1. **Soft demodulation & descrambling**
2. **De-rate matching based on UCI bits count**
3. **Decoder selection:**
   - **3 to 11 bits** → **Reed-Muller decoder**
   - **12 to 19 bits** → **Polar decoder + CRC-6 removal**
   - **≥ 20 bits** → **Segmentation, Polar decoder + CRC-11 removal**

### **Example: UCI Processing Based on Bit Count**
| UCI Bits | Processing Steps |
|----------|-----------------|
| 3 to 11  | Reed-Muller coding |
| 12 to 19 | CRC-6 → Polar coding |
| ≥ 20     | Segmentation → CRC-11 → Polar coding |

### **Final Decision: Identifying Transmitted UCI Bits**
- Based on **scrambling ID** and **modulation order**, the system determines the **final decoded UCI bits**.

## **Real-World Applications in 5G Modem Software**
### **1. HARQ Feedback in Smartphones**
- **Scenario:** A **5G smartphone** acknowledges received downlink packets.
- **PUCCH F2 ensures accurate HARQ feedback with minimal overhead**.
- **Example:** Qualcomm Snapdragon modems optimize **QPSK-based HARQ signaling**.

### **2. SR Transmission in IoT Devices**
- **Scenario:** A **low-power IoT sensor** requests uplink resources.
- **PUCCH F2 minimizes transmission time while maintaining reliability**.
- **Example:** Smart meters use **low-bandwidth uplink control signaling**.

### **3. Efficient Scheduling in 5G Networks**
- **Scenario:** Multiple UEs require **scheduling requests (SR)**.
- **PUCCH F2 allows quick scheduling without resource conflicts**.
- **Example:** High-density 5G networks use **PUCCH F2 for optimized scheduling**.

## **Conclusion**
PUCCH Format 2 is optimized for **short uplink control signaling**, ensuring:
- **Efficient HARQ and SR transmission**
- **Reliable frequency hopping for interference reduction**
- **Robust receiver processing for accurate UCI decoding**

Understanding **PUCCH F2 resource allocation and receiver design** is essential for **5G modem software development** and **network optimization**.



---
## Next Topic
### 65. [PUCCH Format 3/4: DMRS](Format_3_4_DMRS.md)
