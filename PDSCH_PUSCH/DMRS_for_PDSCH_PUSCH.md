# DMRS for PDSCH and PUSCH

## Introduction

In this section, we will discuss the Demodulation Reference Signal (DMRS) for PDSCH (Physical Downlink Shared Channel) and PUSCH (Physical Uplink Shared Channel). Since PDSCH and PUSCH share many similarities in terms of channel processing, the DMRS structure and functionality are also similar.

DMRS is essential for accurate channel estimation, allowing the receiver to decode transmitted data effectively. The DMRS signals can vary in both time and frequency domains, with different configurations optimized for various scenarios.

---

## DMRS Allocation in Frequency Domain

### DMRS Configuration Types

DMRS can be configured in two different types:

1. **Configuration Type 1:**
   - DMRS is transmitted on alternating subcarriers (e.g., 1, 3, 5, 7, 9, 11).
   - High DMRS density, providing better reliability.
   - Used in initial access for robust performance.
   
2. **Configuration Type 2:**
   - DMRS is transmitted on consecutive subcarriers (e.g., 1, 2, 7, 8).
   - Lower overhead compared to Type 1.
   - Provides more Code Division Multiplexing (CDM) groups, allowing better multiplexing of multiple layers.
   
### Configuration Type Selection
- **High DMRS Density (Type 1):** Provides better reliability but higher overhead.
- **Low DMRS Density (Type 2):** Reduces overhead and enables better multi-layer multiplexing.
- **Initial Access:** Type 1 is preferred for its robustness.

---

## DMRS Allocation in Time Domain

### Number of DMRS Symbols in Time
- DMRS symbols can vary between **1 to 4** symbols in a slot.
- Higher Doppler (fast-moving UE) requires more DMRS symbols for accurate channel estimation.
- Fewer DMRS symbols are needed in **FR2 (millimeter-wave)** scenarios due to minimal channel variations.
- Overhead increases as the number of DMRS symbols increases.

### Mapping Types
1. **Mapping Type A:**
   - DMRS reference is the start of the slot.
   - DMRS can be placed on the **2nd or 3rd symbol**.
   - Used in conventional slot-based transmissions.
   
2. **Mapping Type B:**
   - DMRS reference is the start of the PDSCH or PUSCH transmission.
   - DMRS is always in the first symbol.
   - Primarily used for **mini-slot transmissions** (short TTI durations).

---

## Front-Loaded DMRS

- **Purpose:** Enables fast channel estimation at the receiver.
- **How It Works:** DMRS is transmitted in the first symbol of a transmission, allowing the receiver to perform channel estimation before data symbols arrive.
- **Comparison:**
  - **If DMRS is late:** Receiver waits before starting the estimation, increasing latency.
  - **If DMRS is early (front-loaded):** Receiver can estimate the channel immediately and start decoding data symbols sooner.

---

## DMRS Multiplexing

### Single Symbol vs. Double Symbol DMRS
1. **Single Symbol DMRS:**
   - Limited multiplexing capability.
   - Type 1: Supports up to **4 layers per CDM group**.
   - Type 2: Supports up to **6 layers per CDM group**.
   
2. **Double Symbol DMRS:**
   - Enables more orthogonality and better layer multiplexing.
   - Type 1: Supports up to **8 layers**.
   - Type 2: Supports up to **12 layers**.
   
- **Concept:**
  - In **double symbol DMRS**, two consecutive symbols are used for reference signals, assuming the channel remains stable over two symbols.

---

## DMRS Sequence Generation

### Sequence Generation Process
- DMRS sequences are generated using **PN sequences**.
- **Modulation:** QPSK modulation is applied.
- **Scrambling IDs:**
  - `NID^nSCID`: Cell-specific or UE-specific ID.
  - `nSCID`: Can take values **0 or 1**.
  - **Initial Access:** Always set to `0`.
  
- **Orthogonality:**
  - Achieved using **w_f(k') and w_t(l')** factors.
  - These values are predefined in **3GPP specifications**.
  
---

## Transform Precoding and DMRS in PUSCH

- **Transform Precoding Enabled:**
  - Instead of PN sequence-based DMRS, **Zadoff-Chu (ZC) sequences** are used.
  - **Group hopping or sequence hopping** replaces the traditional scrambling ID.
  
- **Purpose of Group Hopping and Sequence Hopping:**
  - Reduces **inter-cell interference**.
  - Ensures different UEs have unique DMRS patterns to avoid collision.
  
---

## Real-World Example: DMRS in 5G Modem Software

### **Scenario:** High-Speed Train Connectivity
- In a high-speed train scenario, **DMRS symbols need to be placed frequently in time** (high Doppler effect).
- **Configuration Type 1** is chosen for higher reliability.
- Front-loaded DMRS ensures **fast channel estimation** before decoding data symbols.
- Multiple DMRS symbols per slot allow **accurate channel tracking** despite the high-speed movement.

### **Scenario:** Fixed Wireless Access (FWA)
- In an FWA scenario, **DMRS overhead must be minimized** (low mobility, stable channel conditions).
- **Configuration Type 2** is used to reduce overhead.
- Fewer DMRS symbols in time to maximize data throughput.
- Double symbol DMRS is used for **higher-layer multiplexing**, supporting MIMO configurations.

---

## Conclusion

- **DMRS plays a crucial role** in accurate channel estimation for PDSCH and PUSCH.
- **Two frequency configurations:**
  - Type 1 (High density, better reliability, used in initial access).
  - Type 2 (Lower density, lower overhead, better layer multiplexing).
- **Time domain variations:**
  - More DMRS symbols in time for high Doppler environments.
  - Fewer DMRS symbols in stable environments to reduce overhead.
- **Transform Precoding in PUSCH:** Uses **ZC sequences** instead of PN sequences.
- **Real-world applications:** DMRS configuration depends on use cases like high-speed mobility or fixed wireless access.

---

In the next section, we will dive deeper into **PDSCH and PUSCH processing** to understand their complete transmission chain.

**Thank you!**

---
## Next Section
### 37. [PDSCH/PUSCH: Physical layer processing](Physical_Layer_Processing.md)  
