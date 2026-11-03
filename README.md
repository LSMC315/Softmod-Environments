# Integrated Softmod & Infrastructure Environments

Welcome! This repository serves as an open-source engineering blueprint for my local development ecosystem. It acts as an educational guide and functional portfolio showing how a custom workstation, segmented homelab network, and targeted legacy console environments interface with one another. 

Whether you are a developer looking at project orchestration or a hobbyist setting up your first console environment, this documentation breaks down the architecture line by line.

---

## 🖥️ 1. Workstation Node (Custom PC Build)
*   **CS Terminology:** Centralized Development Environment & Asset Orchestration Server.
*   **Beginner Explanation:** This is my primary custom-built computer where I write scripts, manage my code files, and prepare packages before sending them over the network to my consoles.
*   **Key Pipeline:** Uses local integrated development environments (IDEs) like PyCharm to build automation flows, safely containing all raw code assets in an isolated local container.

---

## 🌐 2. Homelab Network Infrastructure
*   **CS Terminology:** Segmented Network Routing & Intranet Subnets.
*   **Beginner Explanation:** Setting up an isolated sub-network (Intranet) inside my home router. This keeps the consoles disconnected from the public internet (preventing forced system updates) while letting them talk to my main computer to transfer files.
*   **Key Pipeline:** Implements static IP routing protocols to ensure reliable, high-throughput server-to-client handshakes.

---

## 🎮 3. Target Environments (Consoles)

### Sony PlayStation 4 Slim
*   **CS Terminology:** Payload Injection Vector & Hardware Abstraction.
*   **Beginner Explanation:** A test console kept safely on a specific system firmware (**13.52**) so it can read local files via an exploit path in its web browser (WebKit). 
*   **Storage Upgrade:** Upgraded to an internal **500GB PNY CS900 SSD** to replace the old mechanical hard drive, drastically reducing file system read/write latency (load times) during deployment tests.

### Microsoft Xbox 360 Slim
*   **CS Terminology:** Legacy Storage Provisioning & File System Analysis.
*   **Beginner Explanation:** A hardware testing node used to explore dashboard modifications, file extraction pipelines, and automated asset storage structures.

---

## 💾 4. Storage Architecture Blueprint (8TB Array Split)
*   **CS Terminology:** Data Array Partitioning & File System Interoperability.
*   **Beginner Explanation:** Consoles have strict storage limits. The Xbox 360 cannot naturally read a massive 8TB drive. To solve this, a single 8TB hard drive is split into two logical "rooms" (partitions) formatted with different file rules:
    *   **2TB FAT32 Partition:** Allocated to respect the legacy Xbox 360 dashboard volume ceiling, enabling native file system discovery.
    *   **6TB exFAT Partition:** Allocated for massive PS4 package storage files, supporting individual file sizes larger than 4GB with optimal performance.

---

## 📂 Repository Architecture

```text
├── README.md               # Master portfolio dashboard (This page)
├── 6-Personal-Tech-Projects/
│   ├── custom_pc_build/     # Workstation specs, benchmarking, and environment scripts
│   └── console_restoration/ # Hard drive configuration maps and console diagnostic logs
├── 7-Network-Infrastructure/
│   └── homelab_configs/     # Router subnets, network mapping, and static routing files
├── docs/
│   ├── hardware-validation.md # Motherboard, MFR date, and amperage cross-checks
│   ├── flash-dump-logic.md   # Step-by-step reading/writing the NAND flash memory
│   └── partition-splitting.md # Technical breakdown of the 8TB multi-system split array
└── configuration/
    └── aurora_scan_paths.json # Storage map schema tracking path automation
```
