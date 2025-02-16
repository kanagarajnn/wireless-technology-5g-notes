# **Search Space in 5G NR**

## **Introduction**
The **Search Space (SS)** in 5G NR defines the **set of resource blocks (RBs) and symbols** where the **UE searches for DCI (Downlink Control Information)** inside a CORESET.

Since **PDCCH blind decoding** is required, the UE does not initially know **where its DCI is located**. The Search Space provides hints to help the UE limit its search and improve efficiency.

---

## **Search Space and CORESET Relationship**
- **CORESET defines PRBs and symbols allocated for PDCCH.**
- **Search Space provides additional details, such as:**
  - **Start symbol of the PDCCH region.**
  - **Aggregation levels (CCE allocations) for the UE.**
  - **PDCCH candidates per aggregation level.**

For example, if **CORESET defines 48 PRBs and 3 symbols**, the Search Space will define the **exact starting symbol** and **CCE locations where the UE should attempt decoding**.

---

## **Blind Decoding and Search Space Role**
### **Challenges in Blind Decoding**
The UE does not know:
1. **The aggregation level (number of CCEs used).**
2. **The exact location of its DCI.**
3. **The number of blind decoding attempts required.**

To reduce search complexity, **Search Space limits the number of decoding attempts** and provides:
- **Max number of monitored PDCCH candidates per slot** (per numerology).
- **Number of candidates per aggregation level.**

### **Example Configuration**
| Aggregation Level | Max PDCCH Candidates |
|------------------|----------------------|
| 1               | 4                      |
| 2               | 2                      |
| 4, 8, 16        | 0                      |

In this case, the UE **knows that its DCI will not be in aggregation levels 4, 8, or 16**, reducing blind decoding attempts.

---

## **Types of Search Space**
There are **two types of search spaces** in 5G:
1. **Common Search Space (CSS)** – Used for common DCI transmissions.
2. **UE-Specific Search Space (USS)** – Used for UE-specific DCI transmissions.

### **1. Common Search Space (CSS)**
Used for system-wide control messages such as:
- **System Information (SI-RNTI).**
- **Random Access (TC-RNTI).**
- **Group-based DCIs (DCI 2_0, 2_1).**

### **2. UE-Specific Search Space (USS)**
Used for individual UE control messages such as:
- **Scheduling Grants (DCI 1_1, 0_1).**
- **Dedicated RNTI-based transmissions.**

---

## **Search Space and CORESET Mapping**
- **A gNodeB can configure up to 40 search spaces.**
- **A gNodeB can configure up to 12 CORESETs.**
- **Each Search Space is mapped to a CORESET.**

### **Example CORESET-Search Space Mapping**
- CORESET **covers a set of RBs and symbols.**
- Search Space defines **specific DCI locations within CORESET.**
- gNodeB maps **different Search Spaces to different CORESETs.**

| CORESET | Search Spaces | Aggregation Levels |
|---------|--------------|-------------------|
| CORESET 0 | SS 0, SS 1  | 1, 2, 4           |
| CORESET 1 | SS 5, SS 6  | 4, 8              |
| CORESET 2 | SS 8        | 2, 8              |

This configuration allows flexible DCI allocation across different bandwidth parts and slots.

---

## **Real-World Example in 5G Modem Software**
- **Smartphones use Search Space to locate PDCCH and decode DCI efficiently.**
- **5G base stations dynamically allocate Search Spaces to UEs based on traffic conditions.**
- **Massive MIMO systems optimize Search Space mapping for reduced interference.**

---

## **Conclusion**
- **Search Space defines where UE should look for DCI inside CORESET.**
- **Reduces blind decoding complexity and improves efficiency.**
- **Two types of Search Spaces: CSS (Common) and USS (UE-Specific).**
- **Mapped to CORESET to define exact DCI locations.**

In the next discussion, we will explore **Blind Decoding and its role in PDCCH detection**.

**Stay tuned for more insights into 5G technology!** 🚀

---
## Next Section
### 35. [PDCCH: Receiver and Blind Decoding](PDCCH_Receiver_Blind_Decoding.md)
