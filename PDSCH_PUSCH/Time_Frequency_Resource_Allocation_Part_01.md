# Physical Layer Resource Mapping for PDSCH and PUSCH

## Introduction
In this document, we will explore how data from PDSCH (Physical Downlink Shared Channel) and PUSCH (Physical Uplink Shared Channel) are mapped to resource blocks in the 5G physical layer. While both channels share similar processing steps, there are minor differences which will be highlighted.

## Data Mapping Process
Data is mapped to resource blocks (RBs) and symbols within the allocated frequency and time domain. Let’s consider data symbols as:

```
d0, d1, d2, d3, ..., dn
```

Each data symbol is mapped to subcarriers and OFDM symbols as follows:

1. **Starting Symbol and Number of Symbols**
   - The PDSCH/PUSCH start symbol is defined, along with the number of symbols allocated.
   - The first allocated symbol is determined by the control channel (PDCCH) which carries the Downlink Control Information (DCI).

2. **Mapping Strategy**
   - Data is mapped sequentially across subcarriers and symbols.
   - Interleaving of DMRS (Demodulation Reference Signal) and data may or may not be allowed.
   - The presence of additional signals like CSI-RS (Channel State Information Reference Signal) or PTRS (Phase Tracking Reference Signal) affects mapping.
   
## Layer and MIMO Considerations
In MIMO (Multiple Input Multiple Output) scenarios:
- Different layers (L1, L2, etc.) are mapped separately.
- UEs may be spatially multiplexed, meaning one UE’s DMRS locations are not used for another UE’s data transmission.
- The mapping follows a fundamental rule: **leave all non-allocated REs (Resource Elements) and map data in increasing order.**

## PDSCH and PUSCH Mapping Differences
| Feature               | PDSCH                          | PUSCH                          |
|----------------------|--------------------------------|--------------------------------|
| **Mapping Type A**  | Starts from symbol 0, 1, 2, or 3 | Always starts from symbol 0 |
| **Mapping Type B**  | Can start from any symbol (0-12) | Can start from any symbol (0-12) |
| **Symbol Lengths**  | Defined as 2, 4, 7 for normal CP | Flexible symbol length allocation |
| **Interleaving**    | DMRS interleaving allowed      | DMRS interleaving allowed      |

## Slot Offset (k0 and k2)
Slot offsets indicate the timing difference between the DCI allocation and the corresponding data transmission.
- **k0 (for PDSCH):** Determines the slot offset for the downlink transmission relative to the DCI.
- **k2 (for PUSCH):** Determines the slot offset for the uplink transmission relative to the DCI.

For example:
- If the DCI is in slot 0 and the PDSCH is in slot 1, then k0 = 1.
- If the DCI is in slot 0 and the PUSCH is in slot 2, then k2 = 2.

**Formula for slot offset with different numerologies:**
```
Offset = (n * 2^μ_PDSCH / 2^μ_PDCCH) + k0  (for downlink)
Offset = (n * 2^μ_PUSCH / 2^μ_PDCCH) + k2  (for uplink)
```

## SLIV (Start Symbol and Length Indicator Value)
SLIV is a compact way to communicate start symbols and length for PDSCH/PUSCH. Instead of explicitly signaling both values, SLIV is used:

**Formula:**
```
If L-1 ≤ 7: SLIV = 14 * (L-1) + S
If L-1 > 7: SLIV = 14 * (14 - L) + (14 - S)
```

For example, if:
- Start symbol S = 3
- Length L = 7

Then SLIV calculation is:
```
SLIV = 14 * (7-1) + 3 = 87
```

### Extracting S and L from SLIV
At the receiver, the UE extracts **S (start symbol)** and **L (length)** from the received SLIV value. This is computed as follows:

1. Compute `L`:
   - If `SLIV / 14 < 7`, then `L = (SLIV / 14) + 1`
   - Otherwise, `L = 14 - (SLIV / 14)`

2. Compute `S`:
   - If `SLIV / 14 < 7`, then `S = SLIV % 14`
   - Otherwise, `S = 14 - (SLIV % 14)`

**Example Computation:**
Given `SLIV = 87`:
- `L = (87 / 14) + 1 = 6 + 1 = 7`
- `S = 87 % 14 = 3`

Thus, the UE correctly extracts `S = 3` and `L = 7` from `SLIV = 87`.

## Conclusion
Resource mapping in PDSCH and PUSCH follows a structured approach where symbols are allocated based on predefined rules, ensuring efficient transmission. The interplay between DMRS, CSI-RS, PTRS, slot offsets (k0, k2), and SLIV ensures optimal scheduling and minimal interference in 5G networks.

By understanding these concepts, modem software engineers can optimize implementations for real-world deployments, ensuring robustness and efficiency in 5G communication systems.

---
## Next Section
### 39. [PDSCH/PUSCH: Time and frequency domain resource allocation Part 02](Time_Frequency_Resource_Allocation_Part_02.md)
