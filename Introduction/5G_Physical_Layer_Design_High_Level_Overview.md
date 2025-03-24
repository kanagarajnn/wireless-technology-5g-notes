# Understanding the Design of 5G Physical Layer

## Introduction

In this topic, we will understand the design of the 5G physical layer at a very high level. 
Later in the course, we will go over each component in detail.

## Communication in 5G

- There is a **cell tower** that provides network coverage.
- Multiple **cell phones (UE - User Equipment)** are connected to the network.
- The goal is to **send data** between mobile and the cell tower in both directions:
  - **Downlink**: From the **cell tower to mobile**.
  - **Uplink**: From **mobile to the cell tower**.

## Example Scenario: Sending a Text Message

- A **cell phone (UE)** wants to send a **text message**.
- The message needs to reach another device, but first, it must reach the nearest **cell tower**.
- To understand the need for different components in the physical layer, we analyze the steps required to transmit this message.

## Finding a Base Station

- The **UE (mobile device)** must determine **which base station to connect to**.
- There are multiple **base stations** in the vicinity: **Base Station 1, Base Station 2, Base Station 3**.
- The UE must decide whether to connect to:
  - **Base Station 1**
  - **Base Station 2**
  - **Base Station 3**

### Checking for 5G Support

- Before connecting, the UE must determine **which base stations support 5G**.
- To achieve this, some signals/messages must be transmitted to identify 5G-supported base stations.

## Synchronization with Base Stations

- The **UE** must synchronize with a base station to:
  - Receive data.
  - Decode transmitted signals from the base station.
  - Identify the network and base station details.
- Synchronization involves:
  - **Matching frequency** between the UE and base station.
  - **Synchronizing time** to ensure proper data decoding.

## Role of Broadcast Signals

- Base stations must transmit **broadcast signals** continuously **even without knowing if a UE is present**.
- These broadcast signals help UEs:
  - Detect and connect to base stations.
  - Synchronize in **time and frequency**.
  - Get more details about the base station.

### Types of Broadcast Signals

- **Primary Synchronization Signal (PSS)** and **Secondary Synchronization Signal (SSS)**:
  - Used for **time and frequency synchronization**.
  - Help decode the **network identity**.
- **Physical Broadcast Channel (PBCH)**:
  - Contains **bare minimum information** required for further data decoding.
  - Helps the UE decode the major chunk of data or information about the cell.
  - Comes bundled with **PSS** and **SSS**.
- **System Information Block 1 (SIB1)**:
  - Stands for **System Information Block 1**.
  - Contains the **major details about the base station**.
  - Helps the UE gain essential network configuration details.

### Broadcast Data Transmission

- **PSS, SSS, and PBCH** are continuously transmitted together by the base station.
- **PSS and SSS** help with **time and frequency synchronization**.
- **PBCH** provides additional data required to locate and decode **SIB1**.
- **SIB1** contains **most of the critical network information**.
- These broadcast signals ensure that any nearby UE can detect and connect to the network.

## Cell Selection by UE

- The **UE** must analyze broadcast signals from multiple base stations.
- It determines **which cell to connect to** by evaluating:
  - **Signal strength** from different towers.
  - **Energy levels** received from base stations.
- The UE selects the base station with the highest signal strength for connection.

## UE Initiating Connection

- Once the UE selects a base station, it attempts to connect.
- However, the **base station does not know** that a UE is trying to connect.
- The UE has synchronized **time and frequency**, but:
  - The base station does not know **how far the UE is**.
  - The UE itself does not know its distance from the base station.
- To resolve this, the **UE must send a signal** to the base station.
- This signal is called **PRACH (Physical Random Access Channel)**.
- **PRACH** is an **uplink message** sent from the **UE to the base station (gNB)**.
- **Purpose of PRACH:**
  - Helps the base station identify that a UE wants to connect.
  - Initiates a group of message exchanges known as **initial access**.

### PRACH Signal Design Considerations

- The PRACH signal must accommodate **randomness**, as the base station does not know if a UE is trying to connect.
- The PRACH must handle:
  - Multiple UEs trying to send PRACH at the same time.
  - UEs at varying distances from the base station (near and far UEs).
- The PRACH signal allows the base station to determine the **distance of the UE**.
  - The base station can estimate whether the UE is **100 meters, 500 meters, or 5 kilometers away**.
  - Based on this estimate, future signals from the UE can be **pre-adjusted** to align with the base station’s timing requirements.

## Base Station as the Master Controller

- The **base station (gNB) manages multiple UEs**.
- It controls resource allocation in terms of:
  - **Time**
  - **Frequency**
  - **Space**
- The base station ensures an efficient connection by coordinating these resources between UEs.

## Data Transmission Configurations

- Data transmission should be optimized based on:
  - **Bit size**: Can vary from small (e.g., 24 bits) to large (e.g., 100,000 bits).
  - **Modulation scheme**:
    - **256 QAM** for close-range UEs (high modulation).
    - **QPSK** for far-range UEs (low modulation).
  - **Layering**:
    - Single layer or multiple layers (e.g., four layers).
  - **Time and frequency resources allocation**.
- Since a **fixed pattern** is not optimal, PDSCH and PUSCH transmissions must be dynamically configured.

### Role of PDCCH (Physical Downlink Control Channel)

- The base station must communicate transmission configurations to the UE.
- **PDCCH** carries this configuration data before PDSCH transmission.
- **Process:**
  1. The base station sends **PDCCH** with configuration details.
  2. The receiver (UE) decodes PDCCH.
  3. The UE applies the received configuration.
  4. The UE decodes PDSCH accordingly.
- The same process is applied for uplink (PUSCH transmission).
- Since the base station is the **master**, it dictates configurations through **PDCCH**.

# Wireless Communication: Data Transfer and Signal Propagation

## Control Channel and Configuration

- The control channel contains different configurations.
- The **User Equipment (UE)** will use this configuration to send uplink data via **Physical Uplink Shared Channel (PUSCH)**.
- The base station already knows the configuration because it assigned the configuration to the UE.
- The base station will use this configuration to decode the **PUSCH** data.

## Data Transfer via Physical Channels

### Downlink Control and Data Transfer
- The **Physical Downlink Control Channel (PDCCH)** carries control information.
- The **Physical Downlink Shared Channel (PDSCH)** carries data.
- The **Physical Uplink Shared Channel (PUSCH)** carries uplink data from the UE to the base station.

**Summary:**
- **PDCCH**: Downlink control information.
- **PDSCH**: Downlink data.
- **PUSCH**: Uplink data.

## Physical Layer Components

The physical layer consists of several essential components:
- **Primary Synchronization Signal (PSS)**
- **Secondary Synchronization Signal (SSS)**
- **Physical Broadcast Channel (PBCH)**
- **PDCCH** (Downlink Control)
- **PUSCH** (Uplink Data)
- **PDSCH** (Downlink Data)

These elements work together to ensure smooth communication between the UE and the base station.

## Signal Propagation and Multi-path Effects

### Wireless Communication vs. Wired Communication
- Unlike wired communication, wireless signals do not travel in a straight line.
- The data or signal can take multiple paths to reach the receiver.

### Factors Affecting Signal Propagation
- **Phase and Amplitude Changes**
  - As the signal travels, both phase and amplitude can change.
  - These changes are inevitable in wireless communication.

- **Mobility and Changing Signal Path**
  - If the **UE is moving** (e.g., on a bike, in a car, or on a train), the path taken by the signal continuously changes.
  - The distance between the UE and the base station also varies.
  - The **speed of movement** affects the signal reception and path variations.

### Dynamic Nature of Wireless Communication
- The receiver must adapt to these dynamic conditions while decoding data.
- The signal may experience:
  - **Doppler effect** due to movement.
  - **Interference** from multiple paths.
  - **Fading** due to obstacles and environmental factors.

## Signal Detection and Decoding

- The signal could be **PBCH data**.
- The signal could be **PDSCH data**.
- It is continuously being decoded by the receiver.
- The detection and decoding of the signal are only possible when some information about the channel is known.

### Impact of Changing Environments
- If the UE is moving at different speeds (faster, slower) or in different environments (lift, parking, indoor rooms), the way the signal travels changes.
- Even if the UE does not move, the channel itself is continuously changing due to environmental factors.
- The receiver must adapt to these changes and understand how the channel affects the signal.

## Reference Signals and Channel Estimation

- To facilitate proper decoding, the transmitter must send **reference signals** along with the data.
- These reference signals help the receiver analyze how the channel has changed the signal in terms of:
  - **Phase shifts**
  - **Amplitude changes**
  - **Rate of variation**

### Demodulation Reference Signals (DMRS)
- **DMRS signals** accompany the data to assist the receiver in decoding.
- The receiver applies corrections based on these signals to mitigate the impact of channel variations.
- Adjustments such as signal rotation and amplitude correction are applied before decoding.

## Packet Transmission and Error Checking

### Data Transfer and Acknowledgment
- These different channels and signals are sufficient to complete data transfer.
- Text messages and other data can be sent using these channels.

### Packet Status Reporting
- When the base station sends a signal to the UE, the receiver must acknowledge whether the packet was successfully received or lost.
- The receiver sends a signal back to the base station to report:
  - **Packet passed** (decoded successfully).
  - **Packet lost** (requires retransmission).

- This acknowledgment allows the transmitter to decide:
  - If the packet was lost, whether to retransmit it.
  - If the packet was received, whether to send the next packet.

### Cyclic Redundancy Check (CRC)
- This mechanism determines whether a packet has passed or failed.
- CRC information helps detect errors in the transmission.

### Uplink and Downlink Feedback
- **PUCCH** is required to transmit acknowledgment (ACK/NACK) for **PDSCH** (downlink data).
- **PDCCH** may also include encoded feedback information regarding the **PUSCH** status.

## 5G Enhancements: Multi-Antenna and Beamforming

### Parallel Data Transmission
- 5G improves efficiency by allowing **multiple antennas** at both transmitter and receiver.
- **Parallel data transmission** is possible, eliminating the need for single-layer transmissions.

### Beamforming
- By using multiple antennas, the base station can **direct signals** towards a specific UE, optimizing signal strength and reducing interference.

### Multi-Layer and Multi-User Transmission
- **Single UE, Multiple Streams**: Multiple data streams can be transmitted to a **single UE** (e.g., four layers of data to one UE).
- **Multiple UEs, Multiple Streams**: Data can be transmitted **simultaneously** to multiple UEs using multiple antennas.

### Channel Estimation for Beamforming
- The base station must know the **current channel conditions** to determine the best transmission strategy.
- A special type of **reference signals** is used to help the UE estimate:
  - How many parallel streams can be supported.
  - The optimal antenna configurations.

### Channel State Information Reference Signals (CSI-RS) and Sounding Reference Signals (SRS)
- **CSI-RS**: Downlink signals transmitted from the base station to the UE to estimate channel conditions.
- **SRS**: Uplink signals transmitted from the UE to the base station for estimating uplink conditions.
- These signals assist in optimizing high throughput, beam steering, and parallel data streams.

## Summary

- Wireless communication involves multiple channels and signals for efficient data transfer.
- Acknowledgment mechanisms ensure reliable transmission through **PUCCH, CRC, and PDCCH feedback**.
- 5G introduces **beamforming** and **multi-antenna** techniques to improve transmission efficiency.
- **CSI-RS and SRS** signals assist in estimating channel conditions, optimizing performance for multiple users and streams.

# 5G Physical Layer Overview

## Frequency Bands in 5G

5G operates in two different frequency bands:

1. **Sub-6 GHz Band**
2. **Millimeter Wave (mmWave) Band**
   - Uses very high frequencies ranging from approximately **24 GHz to 40 GHz**.
   - Due to the high frequency, hardware may not perfectly generate signals.
   - There is a possibility of **phase noise** in the generated signals due to hardware imperfections.
   - This phase noise can occur both on the **User Equipment (UE)** side and the **Base Station** side.

## Phase Noise in mmWave Communication

- If phase noise exists, the **receiver** may not be able to decode the data properly.
- To overcome this issue:
  - The receiver must **identify the phase noise** in the signal.
  - Once detected, the receiver **corrects** the phase noise to properly decode the data.
- This correction is essential for decoding data like **PDCP (Packet Data Convergence Protocol)** and **ACH (Application Control Headers)**.

## Phase Tracking Reference Signals (PTRS)

- A **reference signal** is designed to help the receiver track and correct the phase noise.
- These signals are called **Phase Tracking Reference Signals (PTRS)**.
- PTRS is used exclusively in **millimeter wave communication**.
- PTRS helps track the phase of the signals and apply corrections to ensure accurate data decoding.

## Components of the 5G Physical Layer

In the **physical layer**, the primary goal is to **send data**, primarily through:

1. **PDSCH (Physical Downlink Shared Channel)**
2. **PUSCH (Physical Uplink Shared Channel)**

However, to enable efficient data transmission, many additional signals and channels are required, which act as **overhead**. These include:

### Synchronization Signals
- Helps UE synchronize with the base station.

### Reference Signals
- Includes multiple types of reference signals:
  1. **Phase Tracking Reference Signals (PTRS)** - For phase noise correction.
  2. **Channel State Information Reference Signals (CSI-RS)** - For channel estimation.
  3. **Demodulation Reference Signals (DM-RS)** - Helps UE demodulate received data.

### Broadcast Channel (BCH)
- Used to broadcast **system information** from the base station to all UEs.

### Uplink and Downlink Control Channels
- **PUCCH (Physical Uplink Control Channel)**: Used for sending control information from UE to base station.
- **PDCCH (Physical Downlink Control Channel)**: Used for sending control information from the base station to UE.

### Initial Access and MIMO Support
- Additional reference signals and control information are used for:
  - **Initial access** from UE to the base station.
  - **MIMO (Multiple-Input Multiple-Output) transmission support**.

## Overhead in the Physical Layer

- All control channels, synchronization signals, reference signals, and broadcast channels are categorized as **overhead**.
- The **actual data** is carried by **PDSCH and PUSCH**.
- Overhead signals are essential to:
  - Enable proper decoding.
  - Provide system and control information.
  - Ensure stable and efficient communication.

## Purpose of This Resource

This resource is designed to:
- Provide an in-depth understanding of **5G physical layer channels and signals**.
- Explain **how these signals are designed** and **their specific roles**.
- Cover the **3GPP specifications** that define these signals and their usage.
- Analyze how the **receiver decodes these signals** in real-world scenarios.

We will go over:
- Each channel and signal in detail.
- The rationale behind 3GPP design choices.
- How receivers process and utilize these signals.

## Conclusion

This structured overview of the **5G physical layer** provides insights into the **various signals and channels** that facilitate data transmission. Understanding these elements is crucial to grasp how **modern wireless communication operates efficiently**.

---
## Next Section
### 6. [CRC](../Essential_Modules_5G_PHY/CRC.md)  
