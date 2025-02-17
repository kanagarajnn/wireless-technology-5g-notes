# PRACH Overview

## Introduction to PRACH

PRACH stands for **Physical Random Access Channel**. It is the first uplink signal sent by the **User Equipment (UE)** to the **gNodeB (gNB)** for initial access. Before PRACH transmission, the base station does not know about the UE’s presence in the network. PRACH allows the UE to establish an uplink connection and synchronize with the network.

## Purpose of PRACH
PRACH is used in the following scenarios:

1. **Initial Access**: When a UE wants to connect to the network for the first time.
2. **Uplink Resource Request**: If the UE has no allocated uplink resources for PUSCH, PUCCH, or SRS, it initiates PRACH to request them.
3. **Uplink Synchronization**: When the base station loses uplink synchronization with a UE due to movement or environmental factors, it requests the UE to send PRACH again.
4. **Handover Scenarios**: When a UE moves from one cell to another (e.g., from Cell 1 to Cell 2), it sends PRACH to synchronize with the new base station.
5. **Inter-RAT Mobility**: In **Non-Standalone (NSA)** mode, a UE moving from 4G to 5G cells uses PRACH for synchronization.

## PRACH Signal Characteristics
Since a UE can be located at varying distances from the base station (ranging from **150 meters to 100 km**), PRACH signals must be designed to account for different propagation delays. Unlike other uplink signals (PUCCH/PUSCH) that use **Timing Advance (TA)** for synchronization, PRACH does not have pre-aligned timing.

To handle this, different PRACH formats exist:

1. **Long PRACH Format**:
   - Supports **larger cell radius** (up to 100 km)
   - Uses **smaller subcarrier spacing**
   - Designed for high-latency environments
2. **Short PRACH Format**:
   - Supports **smaller cell radius** (4-5 km)
   - Uses **larger subcarrier spacing**
   - Shorter in duration, making it suitable for dense urban deployments

## Timing Advance (TA) Calculation
After PRACH is transmitted, the base station measures the **round-trip delay** and calculates the **Timing Advance (TA)**. The TA value tells the UE how much earlier it should send its uplink signals to align them properly at the base station.

## PRACH Use Cases
PRACH is essential in multiple scenarios:

1. **New Connection Establishment**: When a UE powers on and attempts to connect to the network.
2. **Random Access Requests**: If the UE loses its uplink resources, it initiates PRACH to request new allocations.
3. **Resynchronization**: If a UE moves closer or farther from the gNB, the propagation delay changes, requiring an updated TA value.
4. **Cell Handover**: When moving between cells, the UE sends PRACH to synchronize with the new gNB.

## Conclusion
PRACH is a crucial aspect of 5G networks, allowing UEs to establish and maintain uplink connectivity. It is specifically designed to handle varying propagation delays and ensure seamless communication between the UE and the gNB. Future topics will cover **PRACH signal generation, mapping, different formats, and processing techniques** in more detail.

---
## Next Section
### 50. [PRACH: Signal Generation and Mapping](Signal_Generation_and_Mapping.md)  
