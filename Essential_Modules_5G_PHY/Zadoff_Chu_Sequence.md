# **Zadoff-Chu Sequence in 5G Modem Software**

## **Introduction to Zadoff-Chu (ZC) Sequence**

The **Zadoff-Chu (ZC) sequence** is widely used in **5G NR (New Radio)** due to its unique mathematical properties. It is commonly applied in:
- **Uplink transmission** (e.g., PRACH preamble, DMRS in PUSCH & PUCCH)
- **Scrambling and modulation techniques**
- **Synchronization signals**

It is also referred to as a **low PAPR (Peak-to-Average Power Ratio) sequence**, which makes it efficient for power-constrained devices like **mobile phones and IoT sensors**.

---
## **Key Properties of ZC Sequences**

### **1. Constant Amplitude**
- The sequence is based on an **exponential term**, ensuring the **amplitude remains constant** regardless of values of \( q \) or \( m \).
- This property **reduces signal distortion** and improves transmission efficiency.

### **2. Zero Autocorrelation**
- A ZC sequence of length **N(ZC)** exhibits **zero autocorrelation** when circularly shifted.
- This means that different shifts of the sequence **do not interfere with each other**, making it ideal for **multi-user uplink transmission**.

### **3. Constant Cross-Correlation**
- The **cross-correlation** between two different ZC sequences is always **1/√(N(ZC))**.
- This ensures minimal interference between different users, improving reliability in **massive MIMO and beamforming** scenarios.

### **4. DFT of a ZC Sequence is Another ZC Sequence**
- The **DFT (Discrete Fourier Transform)** of a ZC sequence remains a ZC sequence.
- This makes **frequency domain processing more efficient**, particularly in **OFDM-based transmissions** in 5G NR.

---
## **Mathematical Definition of ZC Sequence**

The base **Zadoff-Chu sequence** is defined as:
```X_q(m) = e^(-j(π q m (m+1) / N(ZC)))```
where:
- \( q \) = sequence root index
- \( m \) = sample index
- \( N(ZC) \) = sequence length (usually a prime number)

### **Example Calculation (N(ZC) = 5, q = 1)**
Using the formula:
```X_1(m) = e^(-j(π × 1 × m (m+1) / 5))```
The generated sequence:
- ```X_1(0) = e^0 = 1```
- ```X_1(1) = e^(-j(2π/5))```
- ```X_1(2) = e^(-j(6π/5))```
- ```X_1(3) = e^(-j(12π/5))```
- ```X_1(4) = e^(-j(4π)) = 1```

---
## **ZC Sequence in 5G Applications**

### **1. Uplink PRACH (Random Access Channel)**
- The PRACH **preamble sequence** is based on **ZC sequences**, allowing unique signal detection across different users.

### **2. DMRS (Demodulation Reference Signal) for PUSCH & PUCCH**
- ZC sequences are used in **Uplink DMRS** to help the receiver estimate the channel efficiently.

### **3. Efficient Frequency Domain Processing in OFDM**
- Since the **DFT of a ZC sequence is also a ZC sequence**, **fast frequency-domain processing** is possible.

---
## **ZC Sequence Variants in 5G NR**

### **1. Standard Base Sequence Generation**
- The **basic ZC sequence** is generated using the formula mentioned above.
- Used when the base sequence length \( N(ZC) \) is **greater than 36**.

### **2. PRB-Aligned Sequence (for M(ZC) < 36)**
- For **subcarrier alignment**, the phase shifts are chosen from a predefined table in **3GPP specifications**.
- Used when \( M(ZC) \) = **6, 12, 18, 24**, aligning with PRBs.

### **3. Special Case for M(ZC) = 30**
- When **N(ZC) = 31** and **M(ZC) = 30**, a specific predefined sequence is used.

---
## **Conclusion**
- **Zadoff-Chu sequences are fundamental to 5G uplink transmissions**.
- Their **low PAPR, zero autocorrelation, and efficient DFT properties** make them ideal for **OFDM-based communications**.
- **Used in PRACH, DMRS, and other key 5G physical layer signals** to ensure **robust performance**.

Understanding **ZC sequences** is essential for a **Cellular Modem Software Engineer** working on **5G physical layer optimizations**.

---
### **Further Reading & References:**
- [3GPP TS 38.211: Zadoff-Chu Sequences](https://www.3gpp.org)

---
## Next Section
### 16. [Scrambling](Scrambling.md)

