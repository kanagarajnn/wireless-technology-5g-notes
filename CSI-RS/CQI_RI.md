# CQI and RI in 5G NR

## Introduction
**CQI (Channel Quality Indicator)** and **RI (Rank Indicator)** are essential parameters in 5G NR that help the base station (gNB) make efficient decisions regarding **Modulation and Coding Scheme (MCS)** and **MIMO layers**. These indicators ensure optimal resource allocation, enhancing spectral efficiency and data throughput.

## Purpose of CQI and RI
The gNB needs to determine the best MCS and number of MIMO layers for each UE. There are two ways to make these decisions:
1. **Packet Failure-Based Adaptation**: 
   - Start with a certain MCS and single-layer transmission.
   - If the UE successfully decodes the packet (ACK), the MCS is increased.
   - If the packet fails (NACK), the MCS is reduced.
   - The stepping of MCS changes depends on the specific adaptation algorithm.

2. **Channel Quality-Based Adaptation**: 
   - The gNB sends **CSI-RS (Channel State Information Reference Signal)** to the UE.
   - The UE measures the channel quality and reports it back.
   - The gNB uses this feedback to adjust **MCS and MIMO layers dynamically**.

## CQI (Channel Quality Indicator)
### CQI Calculation Process
1. **gNB transmits CSI-RS** → UE receives the reference signal.
2. **UE calculates SINR (Signal-to-Interference-plus-Noise Ratio):**
   - **Signal Power** from non-zero power **CSI-RS**.
   - **Interference + Noise Power** from CSI-IM (Interference Measurement).
   - Formula: `SINR = Signal Power / (Interference + Noise Power)`
3. **UE maps SINR to a CQI value**
   - CQI is an index that corresponds to a specific MCS.
4. **CQI Reporting**
   - **Wideband CQI:** SINR is averaged over the full bandwidth.
   - **Subband CQI:** SINR is calculated per subband and reported separately.

### CQI Tables and MCS Mapping
- The 3GPP specification defines **three CQI-to-MCS mapping tables**:
  - **Table 1 & Table 2:** Designed for a **10% Block Error Rate (BLER)**.
  - **Table 3:** Designed for a **0.001% BLER**, ensuring higher reliability.
- Example:
  - If UE reports **CQI = 12**, the gNB maps it to an MCS that ensures **10% BLER**.

### Dependency on PMI, RI, and Resources
- CQI is linked to:
  - **Precoding Matrix Indicator (PMI)**: Different precoding can change CQI.
  - **Rank Indicator (RI)**: Different MIMO layers impact CQI.
  - **CSI Resources**: Changes in CSI-RS configuration may alter CQI.
- Even if the channel remains the same, different PMI or RI values can lead to different CQI reports.

## RI (Rank Indicator)
### What is RI?
- RI represents the **maximum number of MIMO layers** that a UE can support based on the channel conditions.
- UE signals RI to gNB, which determines how many layers to schedule for **PDSCH (Physical Downlink Shared Channel)** transmission.

### RI Calculation and Reporting
- RI is based on **uncorrelated propagation paths**.
- Example:
  - If **RI = 4**, the UE suggests **4 MIMO layers** can be used.
  - However, if the gNB does not have enough data, it may schedule fewer layers (e.g., **1 or 2 layers**).

## Real-World Application in 5G Modem Software
### Use Case: Adaptive Modulation and MIMO in Smartphones
Modern **5G modems** (e.g., **Qualcomm Snapdragon, MediaTek Dimensity**) utilize CQI and RI feedback for:
- **Adaptive modulation**: Selecting the best MCS to maximize throughput while maintaining reliability.
- **Beamforming and precoding**: Adjusting PMI to optimize signal quality.
- **Multi-layer MIMO**: Dynamically adjusting the number of layers for improved spectral efficiency.

### Example: Enhancing Video Streaming
- A **5G smartphone streaming HD video** in varying signal conditions:
  - In good channel conditions, **CQI = 15**, and **RI = 4**.
  - The gNB assigns **higher MCS (e.g., 256-QAM) and 4 MIMO layers**, boosting throughput.
  - If interference increases, **CQI drops to 8**, and the gNB reduces MCS to ensure reliability.

## Conclusion
- **CQI provides a measure of channel quality, guiding MCS selection.**
- **RI determines the number of MIMO layers for transmission.**
- These parameters enable **adaptive modulation and MIMO** in 5G, improving network performance and user experience.

By leveraging **CQI and RI**, **5G networks dynamically adapt to changing conditions**, optimizing throughput and reliability for **seamless high-speed connectivity**.

---
## Next Topic
### 74. [CSI-RS: PMI](PMI.md) 
