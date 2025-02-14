# **Redundancy Versions (RV) in 5G Modem Software**

## **Introduction to Redundancy Versions**

In **5G NR (New Radio)**, **Redundancy Versions (RV)** play a critical role in **Hybrid Automatic Repeat Request (HARQ)** retransmissions. RV determines the **starting position for bit selection** from the **circular buffer** containing the **LDPC encoded bits**.

By choosing different RVs for retransmissions, 5G can improve **decoding efficiency**, enhance **error correction**, and **reduce latency** in high-speed data transmission.

---
## **Understanding Circular Buffer and RV Selection**

1. **Circular Buffer Concept:**
   - After **LDPC encoding**, bits are placed into a **circular buffer** of size **N**.
   - The transmitter picks a **subset of bits** for transmission, based on the **code rate** and **desired number of bits (E)**.
   - Instead of always picking bits from the **beginning (0th bit)**, RV **specifies a different starting point**.

2. **Redundancy Version Values:**
   - There are **four redundancy versions** in **5G NR**: **RV0, RV1, RV2, RV3**.
   - Each **RV defines a specific starting point** in the circular buffer.

---
## **Systematic and Parity Bits in LDPC**

- The **LDPC output** consists of **systematic bits** (original information bits) followed by **parity bits** (error correction bits).
- These bits are stored in the **circular buffer** and selected based on the RV.

### **RV Selection and Systematic Bit Transmission**
- **RV0 and RV3** start **selection from systematic bits**, making them **self-decodable**.
- **RV1 and RV2** start from **parity bits**, requiring additional HARQ transmissions for successful decoding.

| **RV**  | **Starting Position in Circular Buffer** | **Systematic Bits Included?** | **Self-Decodable?** |
|--------|---------------------------------|-------------------|------------------|
| **RV0** | 0 | Yes | ✅ Yes |
| **RV1** | 17 (1/4 buffer) | No | ❌ No |
| **RV2** | 33 (1/2 buffer) | No | ❌ No |
| **RV3** | 56 (3/4 buffer) | Yes | ✅ Yes |

---
## **Self-Decodable Redundancy Versions**

- **RV0 and RV3 are self-decodable**, meaning they contain **enough systematic bits** to allow decoding without requiring additional retransmissions.
- **RV1 and RV2 rely primarily on parity bits**, requiring HARQ retransmissions for successful decoding.

### **Real-World Application in 5G Modem Software**

- **Streaming Video & Gaming (PDSCH - Downlink)**
  - **RV0 is sent first** to maximize the chance of decoding without retransmissions.
  - If needed, **RV1 or RV2** is used for additional error correction.
  
- **Uplink Data Transmission (PUSCH - Uplink)**
  - HARQ retransmissions **use different RVs** to ensure error recovery with minimal overhead.

---
## **Why RV3 is Not Uniformly Distributed?**

- In **5G specifications**, **RV3 is positioned to maximize systematic bit inclusion**.
- Instead of evenly distributing RVs, **RV3 is offset to ensure better decoding performance** in **HARQ retransmissions**.

---
## **Conclusion**

- **Redundancy Versions (RV) define the bit selection starting point** in LDPC rate matching.
- **RV0 and RV3 are self-decodable**, ensuring that the receiver can decode without needing extra transmissions.
- **RV1 and RV2 rely on parity bits**, making them dependent on HARQ retransmissions.
- **Optimized RV selection improves decoding success rate and reduces retransmissions**, improving **5G modem efficiency**.

Understanding **Redundancy Versions in LDPC Rate Matching** is essential for a **Cellular Modem Software Engineer** focusing on **5G link-level optimizations**.

---
### **Further Reading & References:**
- [3GPP TS 38.212: Redundancy Versions for 5G](https://www.3gpp.org)

---
## Next Section
### 13. [Bit Interleaving in LDPC Rate Matching](Bit_Interleaving_in_LDPC_Rate_Matching.md)

