# CSI-RS Resource Mapping Example

## Introduction
CSI-RS (Channel State Information Reference Signal) resource mapping is a complex process due to its support for up to **32 ports**, which is unlike any other channel in 5G NR. In this document, we will break down the mapping process with an example, explaining the different parameters involved and how they contribute to the final allocation of CSI-RS resources.

## Example: CSI-RS Mapping for Row Index 10
We will use **Row 10** from the standard mapping table as our reference and analyze how the CSI-RS allocation takes place step by step.

### Given Parameters:
- **Number of Ports (N):** 12
- **Density (ρ):** 1
- **CDM Type:** CDM4-FD2-TD2
- **CDM Group Size (L):** 4
- **CDM Groups Required:** 3
- **Frequency Indices (k̄):** `{k0, k1, k2}`
- **Time Index (l̄):** `{l0}`

Since **CDM4** is being used, each CDM group contains **4 ports**, requiring **3 CDM groups** to accommodate all **12 ports**.

## Step 1: Assigning CDM Group Locations
The three CDM groups are placed at different subcarrier locations:
- **k0 = 0**
- **k1 = 4**
- **k2 = 8**

For time allocation, **l0 = 3** is assumed. Since it is a **CDM4-FD2-TD2** configuration, the symbol indices will be:
- **l = l0 + l'** where `l'` is `{0,1}`
- This results in symbol indices **{3,4}**

## Step 2: Navigation Inside CDM Groups
Each CDM group contains 4 ports, so we navigate through:
- **k' = {0,1}** (Frequency within CDM group)
- **l' = {0,1}** (Time within CDM group)

Thus, for each CDM group:
- Ports are assigned to `{k0, k0+1}, {k1, k1+1}, {k2, k2+1}`
- Time locations are `{l0, l0+1}`

## Step 3: Bitmap for Mapping
For **Row 10**, a **bitmap of size 6** is used:
```[b5, b4, b3, b2, b1, b0] = [1,0,1,0,1,0]```

Using the formula:
- `k0 = 2 × f(1)`
- `k1 = 2 × f(2)`
- `k2 = 2 × f(3)`

Where `f(i)` is the position of the **set bits** in the bitmap:
- **f(1) = 0** → `k0 = 2 × 0 = 0`
- **f(2) = 2** → `k1 = 2 × 2 = 4`
- **f(3) = 4** → `k2 = 2 × 4 = 8`

Thus, the **final frequency locations** for each CDM group are **{0,4,8}**.

## Step 4: Mapping to Ports
- **Total Ports (N) = 12**
- **Port index (s) varies from 0 to 3**
- **CDM group index (j) varies from 0 to 2**
- **Port indices are assigned sequentially**:
  - `{3000, 3001, 3002, 3003}` → CDM Group 0
  - `{3004, 3005, 3006, 3007}` → CDM Group 1
  - `{3008, 3009, 3010, 3011}` → CDM Group 2

## Step 5: Applying Orthogonal Cover Codes
From the standard **CDM4-FD2-TD2** table:
- `wf(0) = [1,1,1,1]`
- `wt(0) = [1,1,1,1]`
- `wf(1) = [1,-1,1,-1]`
- `wt(1) = [1,-1,1,-1]`

Each CDM group uses the same orthogonality codes to ensure proper signal separation.

## Step 6: Visualizing the Mapping
The final mapping in terms of **subcarriers (k) and symbols (l)**:

| Symbol Index | Subcarrier Indices | CDM Group |
|-------------|-------------------|------------|
| 3, 4       | {0,1}             | CDM Group 0 |
| 3, 4       | {4,5}             | CDM Group 1 |
| 3, 4       | {8,9}             | CDM Group 2 |

Each CDM group consists of 4 ports, spanning across **12 ports in total**.

## Conclusion
In this example, we successfully mapped **12 CSI-RS ports** across 3 CDM groups using the **CDM4-FD2-TD2** scheme. The process involved:
1. **Determining k and l values using bitmap indices.**
2. **Navigating within and across CDM groups.**
3. **Assigning orthogonality codes for interference-free transmission.**
4. **Mapping ports to subcarrier-symbol locations efficiently.**

### Real-World 5G Modem Application
- **5G modems (e.g., Qualcomm Snapdragon, MediaTek Dimensity) use this process for beamforming optimization.**
- **Dynamic adaptation of CSI-RS helps improve MIMO performance.**
- **Efficient CSI-RS allocation leads to better spectral efficiency and throughput.**

This systematic approach ensures **optimized resource allocation** in **5G NR networks**, improving overall communication reliability and performance.



---
## Next Topic
### 72. [CSI-IM: CSI for Interference Measurement](CSI_for_Interference_Measurement.md)  
