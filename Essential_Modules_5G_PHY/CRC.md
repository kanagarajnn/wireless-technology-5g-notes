# **Cyclic Redundancy Check (CRC) in 5G Modem Software**

## **Introduction to CRC**
Cyclic Redundancy Check (CRC) is an error-detecting code commonly used in digital networks and storage devices to detect accidental changes to raw data. In a 5G modem, CRC plays a crucial role in ensuring data integrity during transmission across various communication channels.

The CRC process is divided into two main parts:
1. **CRC Generation & Attachment** (at the transmitter)
2. **CRC Checking & Removal** (at the receiver)

## **How CRC Identifies Errors**
When data is transmitted over a communication channel, it undergoes CRC encoding before transmission. The steps involved in CRC generation and checking are as follows:

### **Step 1: CRC Generation at Transmitter**
- A sequence of bits (data to be transmitted) is given.
- A specific CRC polynomial (a predetermined sequence of bits) is used.
- The data is divided using **Modulo-2 Binary Division** by the CRC polynomial.
- Unlike conventional division, **XOR operation replaces subtraction**.
- The remainder from this division is the **CRC checksum**, which is appended to the data.
- The final transmitted sequence consists of the original data plus the CRC checksum.

### **Step 2: CRC Checking at Receiver**
- The received data undergoes the same **Modulo-2 Binary Division** using the same CRC polynomial.
- If the remainder is **zero**, the data is error-free.
- If the remainder is **non-zero**, an error is detected.
- CRC does not indicate which bit is incorrect, only that an error exists.

## **Example of CRC Calculation**
Consider a 5-bit polynomial **11001** used for CRC computation:
- Data: **10101111**
- CRC polynomial: **11001** (degree = 4, so the remainder will have at most 4 bits)
- Perform Modulo-2 division (XOR-based binary division)
- Append remainder to the data before transmission

At the receiver:
- Perform the same division
- Check the remainder (zero for correct data, non-zero for errors)

## **CRC in 5G Modem Software**
In **5G New Radio (NR)**, different CRC polynomials are used for various physical layer channels. The CRC length determines the error-detection capability and is chosen based on the channel characteristics.

### **Common CRC Polynomials in 5G NR**
| CRC Type  | Polynomial (Binary) | Polynomial (Hex) | Used In |
|-----------|------------------|------------------|---------|
| CRC-6    | 1100001          | 0x61             | Downlink Control Information (DCI) |
| CRC-11   | 100000000101     | 0x805           | Uplink Control Information (UCI) |
| CRC-16   | 11000000000000101 | 0xC0005         | Transport Blocks (TB) |
| CRC-24A  | 110000000000000000001011 | 0xC0000B | Physical Downlink Shared Channel (PDSCH) |
| CRC-24B  | 110000000000000000001110 | 0xC0000E | Physical Uplink Shared Channel (PUSCH) |
| CRC-24C  | 110010011000000000001101 | 0xC9800D | Used in Radio Link Control (RLC) |

## **Real-World Application in 5G Modems**
1. **Physical Layer Error Detection**
   - CRC-24 is used in **PDSCH and PUSCH** to ensure correct packet reception.
   - If CRC fails, **Hybrid Automatic Repeat Request (HARQ)** is triggered.

2. **Channel Coding in 5G**
   - CRC is appended before **LDPC/Turbo coding** to improve error correction.
   - Helps in detecting **incorrect blocks before decoding** to save processing power.

3. **5G NR Uplink & Downlink Transmission**
   - CRC-6 is used in **Downlink Control Information (DCI)** to detect control message errors.
   - CRC-11 is used in **Uplink Control Information (UCI)** to check for scheduling errors.

4. **Efficient Packet Transmission**
   - In 5G **millimeter-wave (mmWave) communication**, CRC is crucial to handle **high packet loss rates**.
   - CRC ensures **error-free decoding in high-mobility scenarios** (e.g., 5G in high-speed trains or autonomous vehicles).

## **Conclusion**
CRC is a fundamental technique for **error detection** in 5G modem software. It helps ensure the integrity of transmitted data and plays a key role in various physical layer channels of 5G NR. Understanding how different CRC types are used in 5G can help optimize modem performance and improve communication reliability.

---
For more details on **channel-level CRC usage**, we will discuss them in future notes!

## Next Section
 ### 7. [Channel Coding](Channel_Coding.md)

