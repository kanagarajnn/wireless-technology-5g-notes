# Sounding Reference Signal (SRS) in 5G

## Introduction
**SRS (Sounding Reference Signal)** is an uplink signal transmitted by the **UE (User Equipment)** to the **gNB (Base Station)** in **5G NR**. It helps in estimating the uplink channel conditions, optimizing resource allocation, and improving overall network efficiency.

## Why Do We Need SRS?
Although **DMRS (Demodulation Reference Signal)** exists in **PUSCH (Physical Uplink Shared Channel)**, it is limited to the allocated resources. SRS provides additional benefits:
- **Full-band Channel Estimation:** Helps gNB determine the best frequency resources.
- **MIMO Layer Optimization:** Assists in determining the **best number of layers** for transmission.
- **Uplink Scheduling:** Determines the best **PRBs (Physical Resource Blocks)** and **MCS (Modulation and Coding Scheme)**.
- **TDD Reciprocity:** Used for **downlink scheduling** in **Time Division Duplex (TDD) mode**.

## How SRS Works
1. **UE Transmits SRS:**
   - SRS is sent separately in the uplink for **channel estimation**.
   - gNB measures the SRS to **schedule uplink transmission** efficiently.
2. **gNB Estimates Channel Conditions:**
   - Determines the best **PRBs** and **MIMO layers**.
   - Can use SRS for **downlink scheduling in TDD mode**.

## SRS for TDD Reciprocity
- **TDD Mode:** gNB assumes the uplink and downlink channel conditions are similar.
- **SRS helps estimate the downlink channel** for scheduling **PDSCH (Physical Downlink Shared Channel)**.
- **Limitation:** Cannot measure downlink interference, affecting scheduling accuracy in high-interference scenarios.

## SRS Transmission Types
SRS can be scheduled in three ways:
1. **Periodic SRS:** Sent at fixed intervals.
2. **Aperiodic SRS:** Sent only when requested by gNB.
3. **Semi-Persistent SRS:** Configured for repeated transmission but can be modified dynamically.

## SRS Resource Allocation
- **Last OFDM symbols** in a slot are allocated for SRS.
- Can take **up to 4 OFDM symbols**.
- Can be transmitted in **any of the last 6 symbols** (symbol index: **8 to 13**).
- Supports **full-band transmission** (up to **272 PRBs**).

## SRS Signal Generation
- SRS is based on the **Zadoff-Chu (ZC) sequence**.
- Uses **cyclic shift multiplexing** to enable **multiple UEs or antenna ports** to transmit on the same resource.

## Multiplexing Multiple UEs in SRS
- Multiple UEs can transmit SRS in **the same resource block** using different **cyclic shifts**.
- Example:
  - **UE1** transmits in a certain SRS resource.
  - **UE2** transmits using a different cyclic shift in the same resource.
  - Up to **8 UEs** can share the same resource.

## SRS Frequency Hopping
**Problem:**
- A UE at the **cell edge** has limited power.
- If the UE transmits **full-band SRS**, the **power per subcarrier is weak**, making channel estimation inaccurate.

**Solution:**
- **Frequency Hopping:** Concentrates power in fewer PRBs.
- **Two Types of Frequency Hopping:**
  1. **Intra-Slot Frequency Hopping:** SRS is transmitted in different PRBs within the same slot.
  2. **Inter-Slot Frequency Hopping:** SRS is transmitted in different PRBs across multiple slots.

## Limitation: Channel Aging
- If the channel varies rapidly, **inter-slot frequency hopping** may cause outdated channel estimates.
- **Fast-changing channels** make **inter-slot SRS** less effective.

## Conclusion
- **SRS is crucial for uplink scheduling, rank estimation, and MIMO optimization.**
- **It helps in TDD mode for downlink scheduling but cannot measure downlink interference.**
- **Multiplexing and frequency hopping techniques enhance SRS performance, especially for cell-edge users.**

In the next discussion, we will explore **SRS signal generation, resource mapping, and advanced scheduling techniques.**



---
## Next Topic
### 76. [SRS: Sequence Generation](Sequence_Generation.md) 
