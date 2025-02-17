# UE Multiplexing for PDSCH and PUSCH in 5G

## Introduction
UE multiplexing in 5G involves allocating **Physical Downlink Shared Channel (PDSCH)** and **Physical Uplink Shared Channel (PUSCH)** resources across different UEs in time, frequency, and space. This ensures **efficient spectrum utilization** and **optimal throughput**.

## Resource Allocation Dimensions
In 5G, resources are allocated across three dimensions:
1. **Time**: Symbols within an OFDM slot (up to 14 symbols per slot).
2. **Frequency**: Physical Resource Blocks (PRBs), up to **273 PRBs** depending on the bandwidth.
3. **Space**: Multiple antennas (MIMO layers) enabling **spatial multiplexing**.

## Basic Rules of UE Multiplexing
- **Rectangular Allocation**: The allocated resource block for a UE must be rectangular (i.e., a continuous block in both time and frequency dimensions).
- **Layer Allocation**: The time and frequency allocations remain **consistent** across all antenna layers allocated to a UE.
- **Independent Scheduling**: Each UE has **independent** parameters such as **Modulation and Coding Scheme (MCS)**, **transport block size (TBS)**, and **DMRS symbols**.
- **UE Isolation**: UEs do not have visibility of other UEs multiplexed in the same slot.

---

## UE Multiplexing in Frequency Domain (FDMA)
**Frequency-division multiplexing** assigns **different PRBs** to different UEs in the same time slot.

### Example Scenarios:
1. **Single UE, Full Bandwidth Allocation**: One UE is allocated **all PRBs** in the slot.
2. **Single UE, Partial Bandwidth Allocation**: One UE is allocated a subset of PRBs.
3. **Multiple UEs in Frequency Domain**: 
   - UE1: PRBs **0-11**
   - UE2: PRBs **12-16**
   - UE3: PRBs **17-273**
4. **High-Density Multiplexing**: Multiple UEs sharing the available PRBs down to the minimum **1 PRB per UE**.

**Limitations:**
- The number of UEs multiplexed in a slot is limited by **PDCCH capacity** (control channel overhead).
- ACK/NACK feedback must fit within **PUCCH resources**.

---

## UE Multiplexing in Time Domain (TDMA)
**Time-division multiplexing** allocates **different time slots** to different UEs while using the same PRBs.

### Example Scenarios:
1. **UE1 occupies first half of slot, UE2 occupies second half**.
2. **UE1 uses Mapping Type A (0-7 symbols), UE2 uses Mapping Type B (8-13 symbols).**

**Practical Considerations:**
- Time multiplexing is **less common** as it introduces additional latency.
- Frequency multiplexing is **preferred** due to better resource efficiency.

---

## UE Multiplexing in Space Domain (MU-MIMO)
UE multiplexing in **spatial domain** occurs when multiple UEs share the **same PRBs and time symbols** but are assigned to **different antenna ports**.

### Example Scenarios:
1. **UE1 uses Antenna Port 0, UE2 uses Antenna Port 1**.
2. **MU-MIMO: UEs are assigned separate spatial layers (e.g., 4 layers to UE1, 2 layers to UE2).**

**Key Benefits:**
- Increases spectral efficiency by allowing **multiple users to share the same frequency resources**.
- Enhances throughput without additional spectrum usage.

**Challenges:**
- Requires accurate **Channel State Information (CSI)**.
- Higher computational complexity at **gNB**.

---

## Example: PDSCH & PUSCH UE Multiplexing in a Slot
| UE | Time Symbols | PRBs | Layers | DMRS Symbols |
|----|-------------|------|--------|--------------|
| UE1 | 0-13 | 10-50 | 2 | 2 |
| UE2 | 0-13 | 51-80 | 4 | 3 |
| UE3 | 0-13 | 81-273 | 1 | 1 |

Each UE has **independent** modulation, coding, and DMRS settings.

---

## Summary
- **Multi-UE per TTI**: Multiple UEs can be multiplexed in a single slot.
- **UEs can be multiplexed in three ways**: **Frequency (FDMA)**, **Time (TDMA)**, and **Space (MU-MIMO)**.
- **Frequency multiplexing** is **most common**.
- **Time multiplexing** is **less preferred** due to latency constraints.
- **MU-MIMO** allows UEs to share PRBs using different antenna ports.
- **Each UE has independent transmission parameters** (MCS, TBS, DMRS allocation).

Understanding these multiplexing methods is crucial for optimizing **5G modem software** to ensure **efficient resource allocation and maximum throughput**. 🚀

---
## Next Section
### 45. [SU-MIMO and MU-MIMO](SU_MIMO_MU_MIMO.md)
