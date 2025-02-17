# PUSCH MIMO in 5G Uplink

## Introduction
This document provides an in-depth explanation of **MIMO (Multiple-Input Multiple-Output) for PUSCH (Physical Uplink Shared Channel)** in 5G. It covers **antenna placement, coherence types, and codebook-based MIMO transmission**.

## UE Antenna Placement and Its Impact on Uplink MIMO

UE (User Equipment) can be a **mobile phone, CPE, laptop, or any device** that connects to the gNB (5G Base Station). The way **antennas are placed and how a user holds the phone significantly impact uplink performance**, especially in **mmWave communications**.

### Common Antenna Placements in Mobile Phones
1. **Cross-Polarized Antennas:** Two antennas placed at different angles (e.g., top corners of the device) to optimize reception.
2. **Two-Pair Cross-Polarized Antennas:** Two sets of cross-polarized antennas for better coverage.
3. **Millimeter-Wave Antennas:** 8 or more antennas placed at the **top and side** of the phone for beamforming.
4. **Dual-Antenna Panels:** Two separate panels, each with four antennas for **8T8R (8 Transmit, 8 Receive) MIMO**.

### Key Considerations
- **mmWave Signals are Highly Directional:** UE must determine the best panel for transmission.
- **Hand Placement Matters:** Holding the phone in different ways can block signals, affecting **beamforming and power transmission**.

## Antenna Coherence and UE Classification

UE antennas are categorized based on **coherence**:
1. **Non-Coherent Antennas:** No phase alignment; each stream directly mapped to an antenna.
2. **Partially Coherent Antennas:** Pairs of antennas are phase-aligned, allowing controlled beamforming.
3. **Fully Coherent Antennas:** All antennas phase-aligned, allowing **advanced beamforming and spatial multiplexing**.

## Codebook-Based MIMO for Uplink (PUSCH)

### Step 1: Panel Selection
- UE transmits **SRS (Sounding Reference Signal)** on all antenna panels.
- gNB analyzes the signal and selects the **best antenna panel** for uplink transmission.

### Step 2: Rank and Transmission Configuration
- gNB determines **rank** (number of MIMO layers UE can support).
- UE capability (antenna type, coherence) is **signaled to gNB**.
- gNB selects an appropriate **TPMI (Transform Precoding Matrix Indicator)** for transmission.

### Step 3: Precoding Matrix Selection

#### **Single-Layer Transmission (1 Data Stream)**
- **Two Antennas:** Selects one of two antennas or distributes signal with phase shifts.
- **Four Antennas:** Maps signal to one or multiple antennas with controlled phase shifts.

#### **Two-Layer Transmission (2 Data Streams)**
- **Two Antennas:** Each stream is mapped to a separate antenna.
- **Four Antennas:** Different precoding matrices distribute layers across antennas.

#### **Four-Layer Transmission (4 Data Streams)**
- Each layer mapped to different antennas.
- gNB selects a **precoding matrix** based on coherence and antenna capabilities.

## Practical Considerations for PUSCH MIMO
1. **Transform Precoding:**
   - **Enabled**: Single-layer transmission (low PAPR, better coverage).
   - **Disabled**: Supports multiple layers (higher throughput).
2. **Codebook-based vs. Non-Codebook-Based MIMO:**
   - Codebook-based: gNB controls the **precoding matrix**.
   - Non-Codebook-Based: UE determines **beamforming** dynamically.

## Conclusion
- **Antenna placement and phone holding impact MIMO performance.**
- **UE antennas can be non-coherent, partially coherent, or fully coherent.**
- **Codebook-based MIMO enables controlled uplink transmission.**
- **Transform precoding helps reduce power requirements and enhances signal transmission.**

Understanding these principles is crucial for **5G modem development**, ensuring **efficient uplink transmission and improved coverage.** 🚀

---
## Next Section
### 48. [PUSCH: Non codebook based MIMO](Non_Codebook_Based_MIMO.md)
