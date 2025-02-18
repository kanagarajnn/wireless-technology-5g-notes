# **Understanding Frequency Bands and Bandwidth in 5G**

## **Introduction**
This document explains the frequency bands used in 5G technology and the concept of bandwidth allocation. It provides a clear understanding of different frequency ranges, their characteristics, and real-world examples related to 5G modem software.

---

## **Frequency Bands in 5G**
Frequency bands in 5G are divided into three main categories:

### **1. Low Band (< 1 GHz)**
- **Pros:**
  - Excellent coverage (signals travel farther and penetrate buildings better).
  - Suitable for rural and suburban areas.
- **Cons:**
  - Limited bandwidth availability (most of these frequencies are already in use).
- **Example in 5G Modem Software:**
  - When designing a modem for rural connectivity, manufacturers prioritize low-band frequencies to ensure better coverage in remote areas.
  
### **2. Mid Band (1 GHz – 6 GHz)**
- **Pros:**
  - Good balance between coverage and speed.
  - Widely adopted for 5G deployments (e.g., around 3.5 GHz).
- **Cons:**
  - Moderate penetration through buildings compared to low band.
- **Example in 5G Modem Software:**
  - Mid-band frequencies are widely used in urban deployments to provide both speed and coverage, ensuring stable performance for applications like video streaming.

### **3. High Band (> 24 GHz, mmWave)**
- **Pros:**
  - High-speed data transmission.
  - Large amounts of spectrum available.
- **Cons:**
  - Very limited coverage (signal degrades quickly and struggles with obstacles).
  - Suitable for dense urban environments and high-traffic areas.
- **Example in 5G Modem Software:**
  - In stadiums or airports, mmWave frequencies are used to provide ultra-high-speed internet access for a large number of users simultaneously.

---

## **5G Frequency Ranges (FR1 and FR2)**
5G bands are defined by the 3GPP specification and are categorized into two frequency ranges:
- **FR1 (Sub-6 GHz)** – Includes both low-band and mid-band frequencies.
- **FR2 (mmWave)** – Includes high-band frequencies for ultra-fast connectivity.

Some common 5G bands:
| Band | Frequency Range | Duplex Mode |
|------|---------------|-------------|
| n1   | 2110-2170 MHz (DL), 1920-1980 MHz (UL) | FDD |
| n78  | 3300-3800 MHz | TDD |
| n257 | 26.5-29.5 GHz | TDD |

---

## **Types of Duplexing in 5G**
Duplexing is the method used to separate uplink (UL) and downlink (DL) transmissions. There are four types:

### **1. Frequency Division Duplex (FDD)**
- **How it works:**
  - Separate frequencies are used for uplink and downlink.
  - Communication occurs simultaneously.
- **Example in 5G Modem Software:**
  - Used in voice call scenarios where continuous bidirectional communication is required.

### **2. Time Division Duplex (TDD)**
- **How it works:**
  - Uplink and downlink share the same frequency but operate at different times.
- **Example in 5G Modem Software:**
  - Mid-band frequencies (e.g., n78) use TDD to optimize bandwidth dynamically based on network traffic.

### **3. Supplementary Downlink (SDL)**
- **How it works:**
  - Provides additional downlink capacity without an uplink pair.
  - Used to enhance download speeds when the primary downlink bandwidth is insufficient.
- **Use Case:**
  - In congested urban networks, SDL is employed to boost downlink speeds for applications like high-definition video streaming.
- **Example in 5G Modem Software:**
  - Network operators can allocate SDL in areas with high download traffic, such as business districts, improving user experience during peak hours.

### **4. Supplementary Uplink (SUL)**
- **How it works:**
  - Provides additional uplink capacity using a separate low-frequency band.
  - Enhances uplink coverage, especially in high-frequency networks.
- **Use Case:**
  - In mmWave networks where uplink coverage is weak due to power constraints, SUL enables better signal transmission by leveraging low-band frequencies.
- **Example in 5G Modem Software:**
  - IoT devices and mobile phones operating in urban areas use SUL to ensure stable uplink connectivity, particularly in environments with high interference or signal blockage.

---

## **Bandwidth Allocation and Guard Bands**
In 5G, not all available bandwidth is used for signal transmission. A portion is left as a **guard band** to prevent interference between adjacent channels.

### **Example: Bandwidth Allocation in n78 (Mid-Band, TDD)**
| Subcarrier Spacing | Channel Bandwidth (MHz) | Used Bandwidth (MHz) | Guard Band (MHz) |
|--------------------|------------------------|----------------------|------------------|
| 30 kHz           | 100 MHz                 | 98.280 MHz          | 1.720 MHz        |

### **Why Are Guard Bands Important?**
- Prevents interference between adjacent frequencies.
- Ensures stable communication.

### **Example in 5G Modem Software:**
- Modems automatically adjust bandwidth usage to comply with 3GPP specifications and avoid signal leakage into adjacent bands.


## **Conclusion**
Understanding frequency bands, duplexing methods, and bandwidth allocation is crucial for optimizing 5G modem software. Different frequency ranges serve different purposes, balancing coverage, speed, and availability based on network requirements.

---
## Next Topic
### 84. [RSRP: Reference Signal Received Power](RSRP_Reference_Signal_Received_Power.md)  
