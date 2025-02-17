# Non-Codebook Based MIMO for PUSCH in 5G

## Introduction
Non-codebook based MIMO in **Physical Uplink Shared Channel (PUSCH)** allows **User Equipment (UE)** to determine its own precoding instead of using predefined codebooks. This approach provides **greater flexibility** but requires the UE to estimate and apply its own precoding weights based on the channel conditions.

## Key Considerations for Non-Codebook Based MIMO
For UE to perform **non-codebook MIMO**, the following aspects must be considered:
1. **Antenna Panel Selection**: If multiple antenna panels exist, UE must decide which one to use.
2. **Precoding Weights Calculation**: UE must determine the optimal **precoding weights** based on channel conditions.
3. **Maximum Number of Layers**: UE needs to determine the **maximum rank** (number of spatial layers) that the gNB can support.
4. **Antenna Combination**: UE must choose the most **suitable antenna** combination for uplink transmission.

## UE Capability Signaling
Before using non-codebook MIMO, **UE must signal its capability** to gNB. This includes:
- Maximum supported **rank** (number of layers it can transmit simultaneously).
- Antenna configurations and coherence.
- Support for **non-codebook based MIMO**.

## How gNB Determines Layers and Antenna Combinations
### **Step 1: UE Transmits SRS (Sounding Reference Signal)**
- **UE sends SRS using all available antennas.**
- gNB uses the received SRS to **estimate the channel conditions**.
- gNB determines **which antenna combination** and **how many layers** can be supported.

### **Step 2: gNB Sends Scheduling Information**
- gNB schedules **PUSCH transmission** for UE based on estimated channel conditions.
- It informs UE **how many layers** to use and **which antennas** should be activated.

### **Step 3: UE Determines Precoding Weights**
- UE receives **CSI-RS (Channel State Information - Reference Signal)** from gNB.
- Based on **CSI-RS**, UE calculates **precoding weights** to be applied before transmission.
- UE transmits PUSCH **using calculated weights and selected antenna panel**.

## Can DMRS be Used Instead of SRS?
Yes, **PUSCH DMRS (Demodulation Reference Signal)** can be used **instead of SRS** but with some limitations:
- **DMRS can be used to reduce rank** (e.g., from 4 layers to 2 layers or 2 layers to 1 layer).
- **DMRS cannot be used to increase rank** (e.g., from 1 layer to 2 layers or from 2 layers to 4 layers).

For increasing rank, gNB needs **additional information** about other antennas, which requires **SRS transmission**.

### **Rank Adaptation Using DMRS and SRS**
1. **Initial Transmission with Rank 4**:
   - UE starts with **4 layers** transmission on 4 antennas.
2. **Rank Reduction Using DMRS**:
   - gNB estimates from DMRS that the channel quality is poor.
   - gNB signals UE to **reduce to 2 layers**.
3. **Further Reduction to Rank 1**:
   - gNB determines that only **1 layer** is feasible.
4. **Rank Increase Requires SRS**:
   - To increase from 1 layer back to 2 or 4, **UE must send SRS**.
   - gNB estimates the channel and signals UE about the new rank and antennas to use.

### **Why is SRS Necessary?**
- DMRS **only carries information for active layers**, so it cannot be used for rank increase.
- **SRS provides full channel information** for all antennas, enabling **gNB to determine the best configuration** for increased rank.

## Summary
- **Non-codebook MIMO** allows **UE to determine its own precoding weights** instead of using predefined codebooks.
- **UE must signal its capability** to gNB.
- **SRS is essential** for gNB to determine the best antenna and layer configuration.
- **DMRS can only be used for reducing rank**, but increasing rank requires SRS.
- **This approach enhances flexibility but requires additional signaling and computation.**

Non-codebook based MIMO is **a powerful technique** that enables better adaptability in **5G uplink** by dynamically selecting the best transmission parameters. 🚀

---
## Next Section
### To be Added soon
