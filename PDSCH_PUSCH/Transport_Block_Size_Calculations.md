# Transport Block Size (TBS) Calculation for PDSCH and PUSCH

## Introduction
In 5G, the Transport Block Size (TBS) is not explicitly signaled to the UE. Instead, the UE must compute it based on the allocated resources, MCS, and other parameters derived from the Downlink Control Information (DCI). This document explains how the TBS is calculated for PDSCH (Physical Downlink Shared Channel) and PUSCH (Physical Uplink Shared Channel).

## Why Should UE Calculate TBS?
The transport block size is not directly signaled to the UE because of the dynamic nature of resource allocation in 5G. Instead, the UE calculates the TBS for the following reasons:
- **Efficient Resource Utilization**: The base station dynamically assigns resources to UEs based on network conditions. By computing the TBS locally, the UE adapts to varying bandwidth allocations without requiring additional signaling.
- **Reduced Control Overhead**: Explicitly signaling the TBS would require additional bits in the DCI, leading to higher overhead. Instead, the UE can derive it from existing parameters.
- **Flexibility for Different Numerologies**: 5G supports multiple numerologies (subcarrier spacings). The UE calculates the TBS based on its assigned numerology, ensuring compatibility with different network configurations.
- **Minimized Latency in Adaptive Modulation**: MCS and resource allocations can change dynamically. The UE computing TBS locally allows rapid adaptation to new transmission conditions.

## Steps to Calculate Transport Block Size

### Step 1: Compute Number of Resource Elements (REs) per PRB
Each Physical Resource Block (PRB) consists of **12 subcarriers** across multiple OFDM symbols. The total REs per PRB are:

```
REs_per_PRB = 12 * (Number_of_Symbols) - DMRS_REs - Overhead_REs
```

- **Number of Symbols**: The allocated symbols in the time domain.
- **DMRS REs**: REs used for the Demodulation Reference Signal (DMRS).
- **Overhead REs**: Additional overhead such as PTRS or CSI-RS.

Example Calculation:
- Assume 14 symbols allocated.
- Two DMRS symbols (each occupying 12 REs across all subcarriers → 12 * 2 = 24).
- No additional overhead.

```
REs_per_PRB = (12 * 14) - 24 - 0 = 144
```

### Step 2: Compute Total Allocated REs
```
Total_REs = REs_per_PRB * Total_PRBs
```

If **Total_REs per PRB exceeds 156**, it is limited to 156 due to specification constraints.

Example:
- Assume **10 PRBs allocated**
-
```
Total_REs = 144 * 10 = 1440
```

### Step 3: Compute Intermediate Information Bits (N_info)

The approximate transport block size before coding is given by:

```
N_info = Total_REs * Number_of_Layers * Modulation_Order * Code_Rate
```

Where:
- **Number of Layers (V)**: 1 to 8.
- **Modulation Order**: BPSK (1), QPSK (2), 16-QAM (4), 64-QAM (6), 256-QAM (8).
- **Code Rate**: Given as a fraction (e.g., 308/1024).

Example:
- **Layers = 1**, **Modulation = QPSK (2)**, **Code Rate = 308/1024**
```
N_info = 1440 * 1 * 2 * (308/1024) = 866.25
```

### Step 4: Determine Final Transport Block Size
#### Case 1: If **N_info < 3824**
Use the following formula to compute **N_info'**:
```
N_info' = max(24, 2^n * floor(N_info / 2^n))
```
Where:
```
n = max(3, floor(log_2(N_info)) - 6)
```
Example Calculation:
```
n = floor(log_2(866.25)) - 6 = 3
N_info' = max(24, 2^3 * floor(866.25 / 2^3)) = 864
```
The transport block size (TBS) is the closest **higher** value in the TBS lookup table.
- Looking at the TBS table, **888** is the next closest value.
```
TBS = 888
```

#### Case 2: If **N_info > 3824**
For larger transport blocks where code block segmentation is required, use:
```
N_info' = max(3840, 2^n * round((N_info - 24) / 2^n))
```
For code block segmentation:
- **If Code Rate < 1/4**, use **3816** for segmentation.
- **If Code Rate > 1/4**, use **8424** for segmentation.

Final Transport Block Size Calculation:
```
TBS = 8 * C * ceil((N_info' + 24) / (8 * C)) - 24
```
Where **C** is the number of code blocks, ensuring **TBS is a multiple of 8 and C**.

## Summary
- **UE must compute the TBS based on allocated resources, MCS, and overhead.**
- **N_info gives an initial estimate, which is adjusted using 3GPP-defined rules.**
- **TBS values are always rounded up to the nearest valid entry in the TBS lookup table.**

Understanding TBS calculations is essential for optimizing 5G modem performance and ensuring efficient resource allocation in real-world deployments.


---
## Next Section
### 42. [MIMO: Basics of Multiple Antenna Systems](Basics_of_Multiple_Antenna_Systems.md)
