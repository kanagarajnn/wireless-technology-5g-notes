# Physical Layer Processing of PDSCH and PUSCH

## Introduction
The processing of PDSCH (Physical Downlink Shared Channel) and PUSCH (Physical Uplink Shared Channel) is quite similar in many ways, as both channels share common physical layer modules. This document outlines the detailed processing of both channels, highlighting key similarities and differences.

## Transport Blocks and CRC Attachment
- PDSCH can process up to **two transport blocks (TBs)**, whereas PUSCH carries only **one transport block**.
- The MAC layer provides the transport block, which can vary significantly in size.
- **Cyclic Redundancy Check (CRC)** is attached to detect errors:
  - **CRC24A** for transport blocks **greater than 3824 bits**.
  - **CRC16** for transport blocks **less than or equal to 3824 bits**.

## Code Block Segmentation
- Large transport blocks are divided into multiple **code blocks (CBs)** to reduce decoding complexity.
- **LDPC Base Graph Selection**:
  - **Base Graph 1** (larger matrix) is used for large TBs.
  - **Base Graph 2** (smaller matrix) is used for small TBs.
- **Code Block Segmentation Criteria**:
  - If **TB + CRC > maximum code block size (Kcb)**, segmentation occurs.
  - **Base Graph 1**: Max CB size = **8448 bits**.
  - **Base Graph 2**: Max CB size = **3840 bits**.
- **Example Calculation**:
  - TB+CRC = 10,000 bits.
  - Max CB size = 8448.
  - Result: The TB is split into **two CBs** of size **5000 bits each**, plus **CRC24B per CB**.

## LDPC Encoding and Rate Matching
- **LDPC Encoding** transforms CBs using LDPC base graphs.
- **Lifting size (ZC)** is chosen to expand the base graph matrix.
- **Rate Matching** is applied to match the coded bits to allocated resources.
- **PUSCH supports both full buffer and limited buffer rate matching**, while **PDSCH always uses limited buffer rate matching**.

## Modulation and Layer Mapping
- **Modulation Schemes**:
  - PDSCH supports **QPSK, 16-QAM, 64-QAM, and 256-QAM**.
  - PUSCH supports **QPSK, 16-QAM, 64-QAM, 256-QAM**, and **π/2 BPSK (if Transform Precoding is enabled)**.
- **Layer Mapping**:
  - **PDSCH:** Supports up to **8 layers**.
  - **PUSCH:** Supports up to **4 layers**.
  - **Example:**
    - 2 Layers: Symbols are mapped as (0,2,4,6) to Layer 0 and (1,3,5,7) to Layer 1.
    - More than 4 Layers: Codewords are distributed among multiple layers.

## Scrambling and Resource Mapping
- **Scrambling** is applied to randomize bit sequences and reduce interference.
  - **Initialization for PDSCH:** `n_RNTI * 2^15 + 9*2^14 + n_ID`.
  - **Initialization for PUSCH:** `n_RNTI * 2^15 + n_ID` (since PUSCH has a single codeword).
- **UCI Bits in PUSCH** (Uplink Control Information) are scrambled differently.
- **Resource Block and Antenna Port Mapping**:
  - Determines the specific resource elements used for transmission.
  - More details are covered in a dedicated section on resource mapping.

## Receiver Processing
- **De-scrambling** and **soft demodulation** are applied to received symbols.
- **Equalization** (Zero Forcing, MMSE, etc.) corrects distortions.
- **LDPC Decoding** recovers original code blocks.
- **Code Block Concatenation** merges CBs into the original transport block.
- **Final CRC Check** determines error-free reception.

## Key Differences Between PDSCH and PUSCH
| Feature | PDSCH | PUSCH |
|---------|-------|-------|
| Number of Transport Blocks | Up to 2 | 1 |
| Maximum Layers | 8 | 4 |
| Modulation | QPSK, 16-QAM, 64-QAM, 256-QAM | QPSK, 16-QAM, 64-QAM, 256-QAM, π/2 BPSK (with Transform Precoding) |
| Rate Matching | Limited Buffer Rate Matching | Full or Limited Buffer Rate Matching |
| Scrambling | `n_RNTI * 2^15 + 9*2^14 + n_ID` | `n_RNTI * 2^15 + n_ID` |

## Conclusion
- PDSCH and PUSCH processing share common steps such as LDPC encoding, modulation, and rate matching.
- Differences exist in transport block structure, modulation, and layer mapping.
- Further details on **resource mapping and antenna port allocation** will be covered in subsequent sections.

This guide provides an in-depth look at the physical layer processing of PDSCH and PUSCH, ensuring clarity and ease of understanding for 5G modem software engineers and researchers.


---
## Next Section
38. [PDSCH/PUSCH: Time and frequency domain resource allocation Part 01](Time_Frequency_Resource_Allocation_Part_01.md)  
