# **Physical Broadcast Channel (PBCH) and PBCH DMRS in 5G**

## **Introduction**
The **Physical Broadcast Channel (PBCH)** in 5G carries the **Master Information Block (MIB)**, which contains critical system information needed for a **User Equipment (UE)** to access the network and decode further channels such as **SIB1 (System Information Block 1)**.

### **Key Information in PBCH**
- **MIB (Master Information Block)** is **24 bits long** and contains:
  - System Frame Number (SFN)
  - SSB (Synchronization Signal Block) beam index
  - kSSB (Subcarrier offset for SSB)
  - Information required to decode SIB1
- **PBCH payload is 32 bits**, consisting of **24 bits from MIB** + **8 additional bits**.

## **PBCH Payload Generation**
1. **MIB (24 bits) + Additional 8 bits:**
   - 6 bits from SFN (out of total 10 bits)
   - 4 LSB bits of SFN are added separately
   - Half Frame Number
   - MSB of SSB index
   - kSSB (subcarrier offset)
2. **Scrambling (First Level)**: Uses **2nd and 3rd bits of SFN**
3. **CRC Attachment (24-bit CRC-24)**: Generates **56 bits (32 + 24)**
4. **Polar Encoding**: Expands **56 bits** to **512 bits**
5. **Polar Rate Matching**: Matches **512 bits** to **864 bits**
6. **Scrambling (Second Level)**: Based on **SSB index**
7. **QPSK Modulation**: Converts **864 bits** into **432 QPSK symbols**
8. **Resource Mapping**: Distributes **PBCH symbols across 3 OFDM symbols**

## **PBCH Modulation and Rate Matching**
- **Modulation Scheme:** **QPSK (Quadrature Phase Shift Keying)**
- **Code Rate:** **56/864 ≈ 0.16** (very low for robustness)
- **Mapping:**
  - **3 OFDM symbols** allocated to PBCH
  - **127 subcarriers** used alongside **PSS and SSS**
  - **432 QPSK symbols distributed within PBCH resource blocks**

## **Demodulation Reference Signal (DMRS) in PBCH**
- **DMRS is used for channel estimation** during PBCH decoding.
- **Location of DMRS is not fixed**, but is determined using:
  - **DMRS position = (Cell ID) mod 4**
  - Example:
    - If Cell ID = 3 → DMRS positions = {3, 7, 11, …}
    - If Cell ID = 10 → DMRS positions = {2, 6, 10, …}
- **DMRS sequence generation** is a function of **SSB index and Cell ID**.

## **UE Processing for PBCH Reception**
### **Step-by-Step Decoding Process**
1. **UE decodes PSS and SSS to determine Cell ID**.
2. **Cell ID is used to find DMRS locations**.
3. **SSB Index is unknown** at first, so UE must blindly decode it.
4. **Blind Decoding of SSB Index:**
   - Try **SSB index values (0,1,2,3)**
   - Perform **CRC check**
   - If CRC passes, correct SSB index is found.
5. **Once SSB index is determined, UE gets:**
   - **Full SFN (System Frame Number)**
   - **Slot number, OFDM symbol number, and SSB location**
6. **Extract MIB and decode essential network parameters.**

## **Real-World Example in 5G Modem Software**
- **Smartphones use PBCH to establish an initial connection with a 5G cell.**
- **IoT devices** decode PBCH for low-power synchronization with the network.
- **Autonomous vehicles** rely on PBCH for ultra-reliable and low-latency communication (URLLC).
- **PBCH ensures reliable and fast handovers** between 5G cells for uninterrupted connectivity.

## **Conclusion**
The **Physical Broadcast Channel (PBCH) is essential for initial synchronization and system information decoding in 5G**. By understanding **PBCH structure, scrambling, modulation, and decoding techniques**, we can see how **UEs efficiently acquire network parameters** to establish a reliable connection.

In the next discussion, we will explore **frequency location of PBCH and its impact on network deployment**.

---
## Next Section
### 30. [SSBurst Time and Frequency Locations](SSBurst_Time_Frequency_Locations.md)



