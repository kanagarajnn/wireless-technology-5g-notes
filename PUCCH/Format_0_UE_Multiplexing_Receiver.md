# **PUCCH Format 0: UE Multiplexing and Receiver Design**

## **Introduction**
PUCCH Format 0 (F0) is a **short format** in **5G NR (New Radio)** used for transmitting **uplink control information (UCI)**, including **ACK/NACK** and **Scheduling Requests (SR)**. This document explores **UE multiplexing**, **receiver design**, and **how different cyclic shifts are used to encode information**.

## **Encoding Information in PUCCH Format 0**

### **Understanding Alpha and Cyclic Shift**
In **PUCCH F0**, the parameter **alpha** determines the **cyclic shift** applied to the **Zadoff-Chu (ZC) sequence**. It is calculated as:

- `alpha = m0 + mcs + Ncs`
  - `m0` → Initial cyclic shift (UE-specific)
  - `mcs` → Encodes UCI information (ACK/NACK, SR)
  - `Ncs` → Function of slot number and symbol number

Since `alpha` ranges from **0 to 11**, the goal is to **maximize the cyclic shift difference** to reduce decoding errors at the receiver.

### **Mapping UCI Information to Cyclic Shift**
- **1-bit HARQ (ACK/NACK)**:
  - `0 → NACK`
  - `6 → ACK`
- **2-bit HARQ (ACK/NACK for two transport blocks)**:
  - `0 → NACK, NACK`
  - `6 → ACK, ACK`
  - `3 → NACK, ACK`
  - `9 → ACK, NACK`
- **HARQ + SR Encoding**:
  - `0 → NACK + No SR`
  - `6 → ACK + No SR`
  - `3 → NACK + SR`
  - `9 → ACK + SR`

### **Minimizing Errors in Detection**
The cyclic shifts are chosen such that **adjacent values have minimal bit difference**. This means:
- **If an error occurs, only one bit is likely to be affected**, reducing decoding errors.
- HARQ has **higher priority than SR**, meaning incorrect detection of SR is acceptable but HARQ errors are minimized.

## **UE Multiplexing in PUCCH Format 0**

### **Assigning Different UEs to Different Cyclic Shifts**
To allow multiple UEs to use the same **PRB** and **symbol resources**, each UE is assigned a **different initial cyclic shift (`m0`)**.

#### **Example: Multiplexing Two UEs**
1. **UE1** → `m0 = 0`
2. **UE2** → `m0 = 1`
3. **ACK/NACK Encoding for Each UE**:
   - `m0 + mcs (UE1) → 0 (NACK), 6 (ACK)`
   - `m0 + mcs (UE2) → 1 (NACK), 7 (ACK)`

This allows multiple UEs to transmit UCI **without requiring additional frequency resources**.

### **Maximum UE Multiplexing Capability**
- **Each bit requires 2 cyclic shifts (e.g., one for ACK, one for NACK).**
- **Up to 6 UEs** can be multiplexed per PRB when transmitting **one-bit HARQ or SR**.
- **For two-bit HARQ + SR, only two UEs** can be multiplexed due to cyclic shift limitations.

## **Receiver Design: How gNB Decodes PUCCH Format 0**

### **Step 1: Correlation with Base Sequence**
The **gNB (5G Base Station)** needs to identify the cyclic shift used by each UE.
- The gNB **generates a local base sequence** based on its knowledge of the transmission parameters.
- It **correlates the received signal with the locally generated sequence**.
- A high correlation at a specific cyclic shift indicates **a detected transmission**.

### **Step 2: Mapping the Detected Cyclic Shift to UCI**
Once the cyclic shift is detected:
- The gNB extracts **mcs** using:
  - `mcs = detected shift - (m0 + Ncs)`
- The gNB then maps `mcs` to the correct **ACK/NACK, SR** values using the predefined encoding table.

### **Example: Detecting Two UEs Simultaneously**
- **Received Signal:** Shows **high correlation** at cyclic shifts **5 and 9**.
- **gNB uses pre-known `m0` values**:
  - `UE1 (m0=0) → 5 - 0 = mcs 5`
  - `UE2 (m0=1) → 9 - 1 = mcs 8`
- **Decoding from Mapping Table**:
  - `mcs 5 → ACK`
  - `mcs 8 → NACK`

## **Resource Optimization in PUCCH Format 0**
Using **UE multiplexing** within the same PRB **saves valuable frequency resources**. Instead of assigning separate PRBs per UE, multiplexing allows:
- **Efficient resource usage** → Multiple UEs can send ACK/NACK/SR in **the same PRB**.
- **Lower PRB consumption** → Reduces **overall bandwidth requirements**.

### **Comparison: Without vs. With Multiplexing**
| Approach | PRB Usage |
|----------|-----------|
| **Without Multiplexing** | Separate PRB for each UE → Higher bandwidth use |
| **With Multiplexing** | Multiple UEs in the same PRB → Efficient resource use |

## **Conclusion**
PUCCH Format 0 **efficiently encodes UCI** using cyclic shifts while enabling **multiple UE transmissions within the same resource block**. The receiver at **gNB** identifies these shifts using **correlation techniques** and maps them back to **ACK/NACK/SR information**.

Understanding **UE multiplexing and receiver design** is crucial for optimizing **5G modem software**, ensuring **efficient uplink resource utilization** and **low-latency feedback mechanisms**.


---
## Next Section
### 59. [PUCCH Format 1: Signal Generation and Resource Mapping](Format_1_Signal_Generation_Resource_Mapping.md)
