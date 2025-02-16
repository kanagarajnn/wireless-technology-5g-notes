# Modulation and Coding Scheme (MCS) Tables for PDSCH and PUSCH

## Introduction
In this document, we will explore MCS (Modulation and Coding Scheme) tables for both PDSCH (Physical Downlink Shared Channel) and PUSCH (Physical Uplink Shared Channel). MCS is crucial in 5G networks as it determines the modulation order and coding rate used for data transmission, balancing throughput and reliability.

## Why Different MCS Indices?

In a 5G network, the channel conditions vary for each UE (User Equipment). Several factors affect the selection of an appropriate MCS:

1. **Signal-to-Noise Ratio (SNR):**
   - A UE close to the gNodeB will experience high SNR, allowing the use of higher modulation orders (e.g., 256-QAM) for maximum throughput.
   - A UE far from the gNodeB or in an obstruction-filled environment will experience low SNR, requiring lower modulation orders (e.g., QPSK) to ensure reliable communication.

2. **Trade-off Between Throughput and Reliability:**
   - Higher modulation orders (e.g., 256-QAM) provide higher throughput but lower reliability.
   - Lower modulation orders (e.g., QPSK) provide higher reliability but lower throughput.

3. **Maintaining a Target Block Error Rate (BLER):**
   - The network aims to keep BLER within a predefined range (e.g., 10%).
   - The gNodeB dynamically selects the optimal MCS to achieve this BLER target while maximizing throughput.

## Structure of MCS Tables

Each entry in an MCS table specifies:
- **Modulation Order (Q):** Determines how many bits are mapped to a symbol (e.g., Q=2 for QPSK, Q=6 for 64-QAM).
- **Target Code Rate:** Defines the proportion of transmitted bits that contain useful data.
- **Spectral Efficiency:** Measures the number of bits transmitted per second per Hz (bits/s/Hz).

### Formula:
```
Spectral Efficiency = Modulation Order (Q) * Code Rate (CR)
```

### Example:
If the spectral efficiency is **2.5703** and the bandwidth is **100 MHz**, the theoretical maximum throughput is:
```
Throughput = 2.5703 * 100 MHz = 257.03 Mbps
```
(Note: Real-world throughput is lower due to overheads such as cyclic prefix, DMRS, and control signaling.)

## MCS Tables for PDSCH

### Three Tables in 3GPP Specifications:

1. **Table 1:**
   - Supports up to 64-QAM.
   - Used when the UE or gNodeB does not support 256-QAM.

2. **Table 2:**
   - Supports 256-QAM.
   - Provides higher spectral efficiency (up to 7.4063 bits/s/Hz) and a higher code rate (up to 948/1024).
   - Used when both UE and gNodeB support 256-QAM.

3. **Table 3:**
   - Also supports up to 64-QAM but has lower spectral efficiency compared to Table 1.
   - Used for ultra-reliable low-latency communications (URLLC) where high reliability is required.

## MCS Tables for PUSCH

For PUSCH, MCS selection depends on whether **transform precoding** is enabled or disabled.

1. **Transform Precoding Disabled:**
   - Uses the same MCS Tables as PDSCH (Tables 1, 2, and 3).

2. **Transform Precoding Enabled:**
   - Uses two special MCS tables:
     - One with 64-QAM.
     - One with lower spectral efficiency for increased reliability.
   - Pi/2-BPSK modulation is included, where Q=1 (one bit per symbol) for robust transmission.

## Special Considerations in MCS Tables

1. **Reserved MCS Entries:**
   - Some MCS indices (e.g., 29, 30, 31) are marked as **reserved**.
   - These are used for retransmissions in HARQ (Hybrid Automatic Repeat Request).

2. **Spectral Efficiency Differences:**
   - In some tables, the spectral efficiency differences between consecutive MCS values are small, allowing finer granularity in adapting to changing channel conditions.

3. **Usage of Pi/2-BPSK in Uplink:**
   - Pi/2-BPSK is used in PUSCH when transform precoding is enabled.
   - Provides robust transmission in low SNR conditions.

## Conclusion
MCS tables in 5G allow for dynamic adaptation to changing channel conditions, ensuring a balance between throughput and reliability. Selecting the right MCS index based on real-time channel feedback is critical for efficient communication. Understanding these tables is essential for optimizing 5G modem software, scheduling algorithms, and link adaptation strategies.



---
## Next Section
### 41. [PDSCH/PUSCH: Transport Block (TB) size calculations](Transport_Block_Size_Calculations.md)  
