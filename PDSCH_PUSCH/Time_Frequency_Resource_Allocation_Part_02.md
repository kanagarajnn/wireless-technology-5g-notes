# Frequency Domain Resource Allocation for PDSCH and PUSCH

## Introduction
In this document, we will explore how resource blocks (PRBs) are allocated to UEs in the frequency domain for shared channels such as PDSCH (Physical Downlink Shared Channel) and PUSCH (Physical Uplink Shared Channel). The allocation strategy determines how PRBs are distributed across the available bandwidth to optimize performance and frequency diversity.

## Resource Allocation Strategies
Resource allocation for PDSCH and PUSCH follows structured methods to ensure efficient utilization of bandwidth and provide frequency diversity. There are two primary types of resource allocation:

1. **Resource Allocation Type 0** - Group-based allocation (non-continuous)
2. **Resource Allocation Type 1** - Continuous allocation

Additionally, PDSCH supports **interleaved VRB-to-PRB mapping** to enhance frequency diversity.

## Resource Allocation Type 0
- Uses **group-based transmission** to divide bandwidth into Resource Block Groups (RBGs).
- The group size (P) depends on the **bandwidth part (BWP) size**:
  - If BWP < 36 PRBs: P = 2 or 4
  - If BWP ≥ 36 PRBs: P = 16

### Example
- **BWP size = 36 PRBs**
- Group size **P = 4**
- Number of RBGs = **36 / 4 = 9**

The PRB allocation for a UE may look like:
```
RBGs: 1, 4, 5, 8 (based on bitmap 100110010)
```
This approach provides frequency diversity by spreading the PRBs across different bandwidth locations.

## Resource Allocation Type 1
- **Straightforward, continuous allocation**
- Only requires signaling of **starting PRB index** and **number of PRBs**

### Example
- Start PRB = **6**
- Number of PRBs = **17**

PRB allocation would be:
```
6, 7, 8, ..., 22 (Continuous Allocation)
```
This method is commonly used due to its simplicity.

## Interleaved VRB-to-PRB Mapping (PDSCH Only)
Interleaved mapping introduces frequency diversity by **shuffling PRBs** after initial mapping.

### Example:
- **16 PRBs allocated**
- **Bundle size = 2**
- **Number of bundles = 8**
- **Interleaving factor (R) = 2**

Using interleaving, PRBs are reordered before transmission, ensuring better frequency diversity.

## Differences Between PDSCH and PUSCH Resource Allocation
| Feature                    | PDSCH                                     | PUSCH                          |
|----------------------------|------------------------------------------|--------------------------------|
| **Type 0 Allocation**      | Supported                                | Supported                      |
| **Type 1 Allocation**      | Supported                                | Supported                      |
| **Interleaved Mapping**    | Supported                                | Not supported                  |
| **PRB Grouping**           | Uses RBG-based allocation                | Uses RBG-based allocation      |

## Conclusion
Resource allocation in PDSCH and PUSCH is designed to balance efficiency and frequency diversity. While Type 1 allocation offers simplicity, Type 0 allocation and interleaved mapping (for PDSCH) provide frequency diversity, improving link reliability. Understanding these methods helps in optimizing 5G modem software for enhanced performance.


---
## Next Section
### 40. [PDSCH/PUSCH: MCS tables](MCS_Tables.md) 
