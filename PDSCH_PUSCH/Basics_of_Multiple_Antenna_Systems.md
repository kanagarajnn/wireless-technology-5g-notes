# Multiple Antenna Systems in 5G

## Introduction
Multiple Input Multiple Output (MIMO) technology plays a crucial role in enhancing the capacity and reliability of 5G networks. This document provides a detailed explanation of various multiple antenna systems, including SISO, SIMO, MISO, and MIMO, with real-world applications in 5G modem software.

## Single Antenna System: SISO
### Single Input Single Output (SISO)
- **Setup**: One transmit antenna, one receive antenna.
- **Channel Impact**: The transmitted signal `x1` undergoes amplitude and phase variations due to the channel `h1`.
- **Received Signal Formula**:
  ```
  y1 = x1 * h1 + w1
  ```
  where `w1` is the noise at the receiver.
- **Limitation**: Limited spectral efficiency, no diversity benefits.

## Multiple Antenna Systems
### MISO (Multiple Input Single Output)
- **Setup**: Two (or more) transmit antennas, single receive antenna.
- **Transmit Diversity**: Same signal is transmitted via multiple antennas with different phase and amplitude modifications using **precoding**.
- **Received Signal Formula**:
  ```
  y1 = h1 * x1 + h2 * x1 + w1
  ```
- **Advantage**: Improved signal quality, higher reliability, effective in overcoming deep fades.
- **Real-World Use Case**: Beamforming in 5G NR (New Radio) to enhance cell-edge user performance.

### SIMO (Single Input Multiple Output)
- **Setup**: Single transmit antenna, multiple receive antennas.
- **Receiver Diversity**: Multiple received copies help in selecting the best signal for improved reception.
- **Received Signal Formula**:
  ```
  y1 = h1 * x1 + w1
  y2 = h2 * x1 + w2
  ```
- **Advantage**: Increased reliability and better reception using techniques like **Maximum Ratio Combining (MRC)**.
- **Real-World Use Case**: Cell phones using two or more antennas to improve reception quality.

### MIMO (Multiple Input Multiple Output)
- **Setup**: Multiple transmit antennas, multiple receive antennas.
- **Spatial Multiplexing**: Different data streams are transmitted simultaneously, leveraging independent channels.
- **Received Signal Formula**:
  ```
  y1 = h1 * x1 + h2 * x2 + w1
  y2 = h3 * x1 + h4 * x2 + w2
  ```
- **Rank of the Channel Matrix**:
  - The ability to separate multiple data streams depends on the channel matrix's **rank**.
  - `Rank = min(transmit antennas, receive antennas)`.
  - In ideal conditions, **4x4 MIMO** can support **4 independent layers**, but in practice, rank is often limited by channel correlation.
- **Real-World Use Case**: 5G Massive MIMO with 32TR/64TR antenna arrays in gNB (Base Stations) to increase spectral efficiency.

## MIMO Configurations in 5G NR
### SU-MIMO (Single User MIMO)
- All layers are assigned to a **single UE**.
- Maximizes individual throughput.
- Used in **high-speed data scenarios** (e.g., streaming, downloads).

### MU-MIMO (Multi-User MIMO)
- Layers are **shared among multiple UEs**.
- Increases overall network capacity.
- Used in **densely populated areas** (e.g., stadiums, urban centers).

## Rank Adaptation in 5G
- **Rank (R)** varies dynamically based on channel conditions.
- **gNB determines the optimal rank** using **CSI-RS (Channel State Information Reference Signal)** feedback.
- If channel correlation is high, **rank is reduced** to prevent interference.
- **Real-World Example**: In high mobility (fast-moving UE), **rank often drops to 1** for robustness.

## Why is 2T1R Practically Not Possible?
- **Channel Limitations**: In a **2T1R** setup (two transmit antennas, one receive antenna), spatial multiplexing is not feasible because there is only one equation to solve for two unknowns (`x1` and `x2`).
- **Signal Overlap Issue**: The receive antenna receives a **superimposed** version of both transmitted signals, making it impossible to separate them without additional information.
- **Requirement for Spatial Multiplexing**: At least **as many receive antennas as transmit antennas** are needed to decode multiple spatial streams.
- **Practical Consideration**: Instead of **2T1R**, **2T2R** or higher configurations are preferred, ensuring proper decoding and diversity gains.

## Summary
| Configuration | Transmit Antennas | Receive Antennas | Use Case |
|--------------|-----------------|-----------------|----------|
| SISO         | 1               | 1               | Basic transmission |
| MISO         | 2+              | 1               | Beamforming, Tx Diversity |
| SIMO         | 1               | 2+              | Improved reception, Rx Diversity |
| MIMO         | 2+              | 2+              | Spatial Multiplexing, High Capacity |

### Key Takeaways
- **Higher antennas enable better performance, but efficiency depends on channel conditions.**
- **Rank adaptation ensures optimal layer usage.**
- **5G leverages MIMO for high spectral efficiency and improved connectivity.**

This document serves as a reference for understanding multiple antenna systems in 5G and their impact on real-world deployments.



---
## Next Section
### 43. [PDSCH: Precoding for MIMO](Precoding_for_MIMO.md)
