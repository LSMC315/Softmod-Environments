# Storage Architecture: 8TB Multi-System Array Partitioning

This document outlines the engineering specifications and reasoning behind splitting a single 8TB external storage array into two distinct logical volumes to serve mismatched hardware targets (Sony PlayStation 4 and Microsoft Xbox 360).

---

## 📊 Technical Partition Mapping

| Parameter | Volume A (Xbox 360 Target) | Volume B (PlayStation 4 Target) |
| :--- | :--- | :--- |
| **Logical Size** | 2.0 TB (Maximum Native Boundary) | 6.0 TB (Remaining Array Volume) |
| **File System** | FAT32 (File Allocation Table 32) | exFAT (Extended File Allocation Table) |
| **Cluster Size** | 64 KB Allocation Unit Size | 128 KB Allocation Unit Size |
| **Primary Use** | Legacy extraction assets & Dashboard mods | Automated CUSA package deployments |

---

## 🧠 Core Engineering Challenges & Solutions

### 1. Overcoming the 2TB Legacy Volume Constraint
*   **CS Terminology:** Master Boot Record (MBR) vs. GUID Partition Table (GPT) addressing limits.
*   **The Problem:** The Xbox 360's internal operating system utilizes an older format structure that physically cannot read storage spaces larger than 2TB on an external drive. If you plug a raw 8TB drive into it, the console won't recognize it at all.
*   **The Solution:** We restrict Volume A to exactly 2.0 TB using an older partitioning layout style (MBR).
*   **Beginner Explanation:** We slice a 2TB "room" off the massive 8TB drive so it tricks the older Xbox into thinking it is plugging into a standard, fully compatible 2TB drive.

### 2. Overcoming File Size Boundaries (FAT32 vs. exFAT)
*   **CS Terminology:** File Allocation Constraints & Interoperability.
*   **The Problem:** The Xbox 360 requires a traditional format rule called **FAT32**, which has a hard limit: it cannot hold any single file that is larger than **4GB**. This is fine for small retro tools, but modern PlayStation 4 game installation packages (`.pkg`) are massive, often reaching 40GB to 50GB for a single file. They would instantly crash or fail to copy onto a FAT32 partition.
*   **The Solution & Beginner Explanation:** We format Volume B (the remaining 6TB) as **exFAT**. Think of exFAT as a modern upgrade that removes the 4GB file restriction completely. This allows huge PS4 installation images to sit comfortably in a single block of storage while keeping the 2TB partition isolated for the Xbox.

### 3. Allocation Unit Size Optimization (Cluster Optimization)
*   **CS Terminology:** Sector Mapping & Latency Mitigation.
*   **The Problem:** When a console reads data, it fetches it in little chunks called "clusters." If the cluster sizes are unoptimized, the hard drive reader has to work twice as hard, jumping all over the disc platter and slowing down your load times.
*   **The Solution & Beginner Explanation:** 
    *   **Volume A (Xbox 360)** is set to **64 KB clusters** because it deals with thousands of tiny configuration and system files. 
    *   **Volume B (PS4)** is set to a wider **128 KB cluster size**. Because PS4 games are massive files, telling the drive to read larger 128 KB chunks at a exact single time drastically increases performance and limits the mechanical wear and tear on your external drive.
