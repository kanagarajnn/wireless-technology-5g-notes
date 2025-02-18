# SRS Receiver Processing in 5G NR

## Introduction
In 5G NR, **Sounding Reference Signal (SRS)** is used to estimate the uplink channel at **gNodeB**. It helps optimize **uplink scheduling, MCS selection, and beamforming**. This document explains how **gNodeB processes the received SRS** to make scheduling decisions.

## System Setup for SRS Reception
- Assume **gNodeB** has **four RX antennas**.
- Assume **UE** has **two TX antennas** sending **SRS**.
- **UE transmits two different Zadoff-Chu sequences** with different **cyclic shifts**.

### Example Configuration
- **KTC = 2** (SRS transmitted on alternate subcarriers).
- **Bandwidth**: 272 PRBs (full band), but simplified to 1 PRB for explanation.

## SRS Transmission and Reception
### Transmission
- **UE TX Antenna 1** sends **SRS sequence 1** (Cyclic Shift = 1).
- **UE TX Antenna 2** sends **SRS sequence 2** (Cyclic Shift = 5).
- Eight cyclic shifts are available (0–7) for **KTC = 2**.

### Reception at gNodeB
- Each **RX antenna** at gNodeB receives **both sequences**.
- The received signal is the **sum of both transmitted signals**.
- Each **RX-TX channel is unique** and modeled as:
  ```
  Received Signal = H_tx1 * SRS_tx1 + H_tx2 * SRS_tx2 + Noise
  ```

## Channel Estimation at gNodeB
Since **SRS sequences are orthogonal**, gNodeB can separate and estimate **each TX-RX channel pair**:
- gNodeB estimates **H_tx1** and **H_tx2** for **each PRB**.
- **SNR (Signal-to-Noise Ratio)** is also computed for each PRB.
- Channel estimation is repeated for **all PRBs (e.g., 272 PRBs)**.

## Scheduling Decisions Based on SRS
### 1. PRB Selection
- gNodeB picks **PRBs with the best SNR** for scheduling **uplink PUSCH**.
- Example: If gNodeB wants to allocate **20 PRBs**, it selects the **20 best PRBs**.

### 2. MCS Selection
- **MCS (Modulation and Coding Scheme)** is chosen based on **SNR**.
- Higher **SNR** → Higher **MCS** → Higher **data rate**.

### 3. TDD Reciprocity for Downlink Beamforming
- In **TDD**, the **uplink channel ≈ downlink channel**.
- gNodeB uses **SRS-based uplink channel estimates** to **precode downlink PDSCH**.
- This is called **TDD Reciprocity**.

## Handling UE with Limited TX Antennas
- **UE may have fewer TX antennas than RX antennas**.
- gNodeB requests UE to send SRS from **different antennas at different times**.
- gNodeB gradually builds a full **TX-RX channel matrix**.

### Challenges
- **Fast-changing channels** may make old SRS estimates invalid.
- **Longer SRS cycles** lead to outdated estimates.
- **Proper scheduling** is required to ensure timely and accurate **channel estimation**.

## Multi-UE Multiplexing for SRS
- **Multiple UEs can transmit SRS simultaneously** using different:
  - **Cyclic shifts** (8 or 12 cyclic shifts based on KTC).
  - **Frequency resources** (Different PRBs for different UEs).
  - **Time-domain symbols** (Different OFDM symbols for different UEs).

### Example Multiplexing Scenario
- **272 PRBs** available.
- **UE1–UE8** use **24 PRBs each**.
- Next **8 UEs use another 24 PRBs**.
- **Multiple OFDM symbols** used to schedule **more UEs**.

## SRS Antenna Switching Feature
- **Antenna switching** allows gNodeB to collect **full TX-RX channel information** over time.
- UE transmits **SRS from different antennas** in different time slots.
- gNodeB requests **antenna switching** to estimate the complete channel.
- This helps improve **beamforming and MIMO scheduling**.

### Example of Antenna Switching
- At **time T1**, UE transmits SRS from **Antenna 1**.
- At **time T2**, UE transmits SRS from **Antenna 2**.
- At **time T3**, UE transmits SRS from **Antenna 3**.
- At **time T4**, UE transmits SRS from **Antenna 4**.

### Benefits
- Allows gNodeB to **estimate full channel matrix**.
- Enables **better precoding and beamforming**.
- Helps in **TDD reciprocity-based scheduling**.

## Conclusion
- **gNodeB estimates uplink channels using SRS** for **better scheduling**.
- **PRB selection and MCS adaptation** optimize uplink efficiency.
- **TDD reciprocity allows downlink precoding using SRS-based estimates**.
- **Multi-UE SRS multiplexing improves spectral efficiency**.
- **Antenna switching provides complete TX-RX channel estimation** for better **beamforming**.

This completes the discussion on **SRS receiver processing in 5G NR**.


---
## Next Topic
### 79. [Phase Noise: What and Why?](PTRS/Phase_Noise_What_and_Why.md)
