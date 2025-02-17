# **PUCCH in 5G: A Detailed Overview**

## **Introduction**
PUCCH (Physical Uplink Control Channel) is the uplink control channel in 5G NR (New Radio) that carries **Uplink Control Information (UCI)**. This information is crucial for communication between the **User Equipment (UE)** and the **gNB (gNodeB, the 5G base station)**. 
PUCCH ensures 
  >- **Efficient Scheduling**,
  >- **Resource Allocation**,
  >- **Link Adaptation**.

### **Three Main Components of UCI**
1. **HARQ Acknowledgement (ACK/NACK):**
   - HARQ (Hybrid Automatic Repeat Request) feedback consists of **ACK (Acknowledgement)** and **NACK (Negative Acknowledgement)**.
   - ACK indicates that the UE has successfully decoded the **PDSCH (Physical Downlink Shared Channel)**.
   - NACK signals decoding failure, prompting retransmission.
   - Example: In a real-world **5G modem software**, the modem continuously monitors PDSCH transmissions. If a downlink data packet from gNB is corrupted due to interference, the UE sends a **NACK** via PUCCH, requesting a retransmission.

2. **Scheduling Request (SR):**
   - SR is used when the UE wants to transmit **uplink data** but lacks allocated resources.
   - The UE sends an SR via PUCCH to the gNB, which then grants uplink resources.
   - Example: A **5G-enabled smartphone** initiating a video call might need to send an SR when new uplink data arrives but no uplink resources are currently allocated.

3. **Channel State Information (CSI):**
   - CSI reports **channel quality** to the gNB for **adaptive modulation and coding (AMC)**.
   - It helps optimize scheduling and beamforming in **massive MIMO (Multiple Input Multiple Output)**.
   - Example: If a **5G modem** detects a weak signal in a moving vehicle, it reports CSI via PUCCH, prompting gNB to switch to a more robust transmission scheme.

## **PUCCH Formats in 5G**
PUCCH formats determine how UCI is transmitted based on capacity, symbol duration, and multiplexing capability.

### **Two Main Categories of PUCCH Formats**
1. **Short Formats (F0, F2):**
   - Use **1–2 OFDM symbols** in the time domain.
   - Best suited for **low-latency transmission** with minimal overhead.
   - Used for simple HARQ ACK/NACK and SR transmissions.

2. **Long Formats (F1, F3, F4):**
   - Use **4–14 OFDM symbols**.
   - Suitable for higher payload UCI like HARQ, SR, and CSI.
   - Provide better robustness against fading.

### **PUCCH Format Breakdown**
| Format | Time Domain (Symbols) | Frequency Domain (PRBs) | UCI Capacity | UE Multiplexing |
|--------|---------------------|------------------|------------|---------------|
| **F0** | 1–2 | 1 PRB | HARQ, SR | Yes |
| **F1** | 4–14 | 1 PRB | HARQ, SR | Yes |
| **F2** | 1–2 | 1–16 PRBs | HARQ, SR, CSI | No |
| **F3** | 4–14 | 1–16 PRBs | HARQ, SR, CSI | No |
| **F4** | 4–14 | 1 PRB | HARQ, SR, CSI | Yes |

- **Formats F0 & F1**: Used for **low-data UCI**, do not carry CSI.
- **Formats F2, F3, F4**: Used for **higher data UCI**, support CSI reporting.
- **F0, F1, and F4**: Allow **UE multiplexing**, meaning multiple UEs can share the same resources.
- **F2 and F3**: Do not support **UE multiplexing**, making them ideal for dedicated high-capacity UCI transmission.

## **PUCCH Real-World Applications in 5G Modems**
1. **HARQ & ACK/NACK Handling:**
   - In **Qualcomm Snapdragon modems**, HARQ feedback via PUCCH helps **optimize downlink performance** by reducing retransmissions.

2. **Scheduling Request in IoT Devices:**
   - 5G modems in **IoT sensors** use SR to request uplink resources for periodic data transmission.

3. **CSI for Beamforming in mmWave:**
   - **5G mmWave modems** rely on CSI from PUCCH to fine-tune beamforming, ensuring reliable high-speed connectivity in urban areas.

## **Conclusion**
PUCCH plays a crucial role in **5G NR** by enabling efficient uplink control information exchange between **UEs and gNB**. Understanding PUCCH formats helps in optimizing modem software for better performance in real-world **5G deployments**.

---
## Next Section
### 57. [PUCCH Format 0: Signal Generation and Resource Mapping](Format_0_Signal_Generation_Resource_Mapping.md)
