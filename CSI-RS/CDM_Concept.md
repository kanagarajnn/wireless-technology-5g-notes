# Code Division Multiplexing (CDM) in CSI-RS

## Introduction
Code Division Multiplexing (CDM) is a technique used in 5G New Radio (NR) for generating orthogonal sequences, ensuring multiple ports can transmit without interference. CDM is utilized in various aspects of 5G, including Demodulation Reference Signal (DMRS) and Channel State Information Reference Signal (CSI-RS). Since CSI-RS supports up to 32 ports, understanding CDM is essential for efficient multiple-port transmission.

## Understanding Orthogonality
Orthogonality is a fundamental concept in CDM. Two sequences are orthogonal if their dot product equals zero. This can be mathematically expressed as:

``` A = (a1, a2) ```
``` B = (b1, b2) ```
``` A ⋅ B = (a1 ⋅ b1) + (a2 ⋅ b2) = 0 ```

### Example 1:
- Sequence A: ``` [+1, +1] ```
- Sequence B: ``` [-1, -1] ```
  - Compute: ``` (+1 × -1) + (+1 × -1) = -2 ``` (Not orthogonal)

- Sequence A: ``` [+1, +1] ```
- Sequence B: ``` [+1, -1] ```
  - Compute: ``` (+1 × +1) + (+1 × -1) = 0 ``` (Orthogonal)

Thus, to generate **N** orthogonal sequences, the sequence length must be at least **N**.

## CDM with Longer Sequences
Extending the sequence length allows for more orthogonal sequences. Consider a length-4 sequence:

- Sequence A: ``` [+1, +1, +1, +1] ```
- Sequence B: ``` [+1, -1, +1, -1] ```
- Sequence C: ``` [+1, +1, -1, -1] ```
- Sequence D: ``` [-1, +1, +1, -1] ```

These sequences are mutually orthogonal, meaning we can use them for different antenna ports without causing interference.

### Key Takeaways:
- **Length-2 sequences:** Support **2 orthogonal sequences**
- **Length-4 sequences:** Support **4 orthogonal sequences**
- **Length-8 sequences:** Support **8 orthogonal sequences**
- **Length-32 sequences:** Support **32 orthogonal sequences**

## Application in 5G Modem Software
Modern 5G modems such as Qualcomm Snapdragon and MediaTek Dimensity use CDM for efficient **MIMO (Multiple-Input Multiple-Output)** transmission. CDM ensures that reference signals across multiple antennas remain orthogonal, preventing interference and improving signal quality.

## Generating Orthogonal Sequences in CSI-RS
CSI-RS ports are assigned orthogonal sequences using **Orthogonal Code Covers**. Given a base sequence ``` [a, b, c, d] ```:

- Sequence A: ``` [+a, +b, +c, +d] ```
- Sequence B: ``` [+a, -b, +c, -d] ```
- Sequence C: ``` [+a, +b, -c, -d] ```
- Sequence D: ``` [-a, -b, +c, -d] ```

If **a, b, c, d** are complex numbers, orthogonality is determined using their conjugates:
``` (a ⋅ p*) + (b ⋅ q*) = 0 ```
where **p, q** are the elements of another sequence.

## CDM Resource Element (RE) Mapping in CSI-RS
CSI-RS resources are mapped using **Frequency Division Multiplexing (FDM)** and **Time Division Multiplexing (TDM)**.

### CDM Configurations:
- **CDM2**: 2 orthogonal sequences per RE
- **CDM4**: 4 orthogonal sequences per RE
- **CDM8**: 8 orthogonal sequences per RE

Each configuration can be applied in different time or frequency domains:
- **CDM2-FD2** (2 in frequency domain)
- **CDM4-FD4** (4 in frequency domain)
- **CDM8-FD4-TD2** (4 in frequency, 2 in time)

## Achieving 32 Orthogonal Sequences for CSI-RS
To maximize spatial multiplexing in 5G MIMO systems, CDM is extended to **32 ports**:
- **CDM8 (FD4-TD2)** is used in four groups to generate **32 orthogonal sequences**.
- UE and gNB can dynamically select the best mapping strategy based on the channel conditions.

## Conclusion
CDM is essential for efficient multi-port transmission in 5G networks. It ensures orthogonality across multiple antennas, allowing CSI-RS and DMRS signals to be transmitted effectively. Understanding CDM helps optimize MIMO performance in 5G modems, leading to improved network efficiency and higher data rates.

This fundamental concept is also utilized in **PDSCH and PUSCH DMRS generation**, making it a cornerstone of 5G modem implementations.



---
## Next Topic
### 70. [CSI-RS: Sequence Generation and Mapping](Sequence_Generation_and_Mapping.md)  
