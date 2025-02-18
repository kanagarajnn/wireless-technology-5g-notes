# SRS Sequence Generation in 5G

## Introduction
**Sounding Reference Signal (SRS)** in **5G NR** is used to estimate uplink channel conditions. It is generated based on the **Zadoff-Chu (ZC) sequence**, which provides good auto-correlation and cross-correlation properties, making it suitable for multi-user multiplexing and minimizing interference.

This document explains **how SRS sequences are generated**, including key parameters such as **cyclic shift, group hopping, sequence hopping**, and how they contribute to efficient uplink transmission.

## Why is SRS Sequence Generation Important?
- Enables **accurate uplink channel estimation**.
- Allows **multiple UEs and antenna ports to share the same resources**.
- Supports **frequency hopping** for better power efficiency.
- Facilitates **MIMO scheduling and beamforming** in uplink transmission.

## Base Formula for SRS Sequence Generation
The **SRS sequence** is generated using:
```ru,v^(alpha_i,delta)(n) = e^(j*alpha*n) * r'(u,v)(n)```
Where:
- `alpha_i` = Cyclic shift parameter.
- `delta` = Determines sequence length.
- `u, v` = Group hopping and sequence hopping indices.
- `n` = Sequence index, ranging from `0` to `Msc,b^srs`.
- `L'` = Number of OFDM symbols allocated for SRS.
- `Pi` = Antenna port index (1, 2, or 4 ports).

## SRS Resource Mapping Based on Comb Size
**Comb Size (KTC)** determines the frequency density of SRS resources:
- **KTC = 2**: SRS is allocated in every **alternate** subcarrier (density = 1/2).
- **KTC = 4**: SRS is allocated in **every fourth** subcarrier (density = 1/4).

This affects the length of the **ZC sequence** used for SRS transmission.

## Cyclic Shift Assignment
Cyclic shifts enable **multiple UEs and antenna ports** to use the same resource block without interference.
- Cyclic shift formula:
  ```alpha_i = 2 * pi * (nsrs^(cs,i) / nsrs^(cs,max))```
- Maximum cyclic shifts:
  - **12 shifts** for `KTC = 4`
  - **8 shifts** for `KTC = 2`
- Example:
  - For `KTC = 4`, the cyclic shifts are `2*pi*(ni / 12)`, where `ni` varies between `0` to `11`.
  - Different shifts ensure **orthogonality** between UE transmissions.

## Group and Sequence Hopping (U and V)
Hopping improves frequency diversity and minimizes interference across cells:
- **Group Hopping (U):** Alters the base sequence for different slots/symbols.
- **Sequence Hopping (V):** Alters sequence **within a group**.
- **U Values:** 0 to 29 (30 possible sequences).
- **V Values:** 0 or 1 (two possible sequence variations).

## Interference Mitigation Across Cells
To avoid **inter-cell interference**, different UEs and cells use unique sequence IDs (`nID^SRS`).
Example:
- **Cell 1:** `nID^SRS = 20`
- **Cell 2:** `nID^SRS = 21`
- **Cell 3:** `nID^SRS = 22`

This ensures that each cell generates **orthogonal sequences** for SRS, reducing interference.

## Real-World Applications in 5G Modems
### 1. **Beamforming and MIMO Scheduling**
- **5G modems (Qualcomm Snapdragon, MediaTek Dimensity)** use SRS to optimize **beamforming** and **multi-layer MIMO transmission**.

### 2. **Uplink Power Optimization**
- **Cell-edge UEs** can use **frequency hopping** to focus power on fewer PRBs, improving reception at the base station.

### 3. **Adaptive Resource Allocation**
- gNB dynamically schedules PRBs based on **SRS-based channel estimates**.

## Conclusion
- **SRS sequence generation** enables **multi-user uplink transmission** with minimal interference.
- **Zadoff-Chu sequences**, **cyclic shifts**, and **hopping techniques** ensure efficient **resource sharing**.
- **Real-world 5G modems** rely on SRS for **beamforming, MIMO scheduling, and power-efficient transmissions**.

Next, we will explore **SRS resource mapping and its implementation in 5G networks**.


---
## Next Topic
### 77. [SRS: Resource Mapping](Resource_Mapping.md)
