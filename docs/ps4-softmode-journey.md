# 🎮 PlayStation 4 Softmod & Hardware Restoration Guide

This document outlines my hands on engineering workflow for restoring, isolating, and configuring two PlayStation 4 consoles to run homebrew software, retro console emulators, and localized game backups.

---

## 🔧 Phase 1: Hardware Inventory & Drive Restoration

### Node 1: Primary Working Console (Firmware 13.52) [Status: Completed]
* **Computer Science Concept (Kernel & WebKit Attack Surface):** My primary PS4 operates on system software version **13.52**, which exposes an exploitable vulnerability in the WebKit browser engine that allows arbitrary userland code execution and subsequent kernel privilege escalation.
* **Beginner Explanation:** Because this console was kept on an older software version instead of updating to the newest Sony firmware, I can run a browser based tool to unlock the system without opening the case or soldering any chips.

### Node 2: Drive Less Console SSD Upgrade & OS Initialization [Status: Planned / In Progress]
* **Computer Science Concept (SATA III Storage Provisioning & Recovery Bootloader):** To restore my second PS4 console (which currently lacks a working internal drive), I selected a **500GB PNY CS900 2.5 inch SATA III SSD** (7mm height, fitting well within Sony's 9.5mm bay tolerance). Because the PS4 operating system resides partially on the internal drive, I staged the **1.05GB firmware 13.52 recovery image (`PS4UPDATE.PUP`)** inside a strict directory hierarchy (`PS4/UPDATE/`) on a **32GB SanDisk Ultra Flair USB 3.0** drive formatted to **exFAT**. Once installed, booting into **Safe Mode Option 7 (Initialize PS4 / Reinstall System Software)** will partition the new solid state drive and flash the base OS cleanly.
* **Beginner Explanation:** Think of a brand new SSD like an empty house with no furniture. I already prepared the PlayStation operating system file on my USB flash drive, and my next step is installing the new SSD inside this second console and running Safe Mode to load the system software onto it.

---

## 🛡️ Phase 2: Network Isolation & GoldHEN Execution

### 1. Blocking Telemetry & Firmware Updates
* **Computer Science Concept (Network Layer Filtering & Air Gapping):** Before launching any exploit payloads, I disabled automatic system downloads and isolated the network interface on Node 1 to prevent unauthorized over the air (OTA) firmware patches from closing the kernel vulnerability.
* **Beginner Explanation:** If the PS4 connects to Sony's servers and updates itself, the softmod stops working. Turning off automatic updates and keeping the console offline protects the setup.

### 2. Volatile Memory Payload Injection (GoldHEN)
* **Computer Science Concept (RAM Resident Homebrew Enabler):** Using a **64GB SanDisk Cruzer Glide 3.0** exFAT USB drive and the offline browser cache, I execute the exploit chain on Node 1 to load **GoldHEN** directly into volatile system memory (RAM). GoldHEN patches kernel restrictions on the fly, unlocking **Debug Settings** for custom package (`.pkg`) installation. Because RAM is volatile, a full power down clears the payload, so I utilize **Rest Mode** to keep memory powered and preserve the active environment between sessions.
* **Beginner Explanation:** This softmod lives in the console's temporary memory rather than permanently changing the motherboard. Putting the PS4 into Rest Mode instead of turning it completely off keeps the softmod active so I do not have to reload it every time I play.

---

## 🕹️ Phase 3: Legacy Emulation & Package Conversion

To consolidate multiple retro consoles onto a single living room node, I configured specialized emulators and binary conversion pipelines:

* **PlayStation 2 (`PS2-FPKG` Pipeline):** Raw single disc PS2 `.iso` and `.bin/.cue` optical disc images are packaged on my Windows workstation using **PS2-FPKG** into signed fake package (`.pkg`) containers, transferred to the root directory of my 64GB USB drive, and installed natively via GoldHEN Debug Settings.
* **Sega Dreamcast (`Resonance`):** Extracted multi track disc images are organized into dedicated game folders on external exFAT storage for hardware accelerated playback.
* **PlayStation 1 & Sega Saturn (`RetroArch`):** Configured core dependencies and required system BIOS binaries (including `sega_101.bin` and `mpr-17933.bin` for Beetle Saturn) alongside `.chd` and `.bin/.cue` game archives.
* **GameCube & Wii (`DolphinPS4`):** Staged compatible ISO backups for cross platform testing.

---

## 💾 Phase 4: Storage Architecture & Account Security

* **Master Vault Integration:** All large PS4 `.pkg` archives are cataloged on my PC using my custom Python deduplication scripts (`track_games.py` and `vault_manager.py`) and stored on the **6TB exFAT partition** of my 8TB external Master Vault drive before staging onto USB for installation.
* **Offline Profile Isolation:** To prevent account bans on official networks, I operate all softmodded sessions exclusively on a dedicated **offline local user profile** with zero PlayStation Network credentials linked.


## 🔗 Referenced Tools & Original Sources

Rather than duplicating external emulator codebases, I star and reference the original open source repositories used in this environment while documenting my own configuration, hardware restoration, and Python automation workflows inside this repository:

* **Computer Science Concept (External Dependency Attribution):** Referencing canonical upstream repositories directly keeps my repository tree focused on original engineering artifacts while maintaining clear attribution and version traceability for external dependencies.
* **Beginner Explanation:** Think of starring and linking a repository like citing a source in a research paper. Instead of copying someone else's entire book onto my shelf, I point directly to their original work and focus my own page on how I set everything up.

* **Sega Dreamcast Runtime:** [iHaiDeeZ/Resonance](https://github.com/iHaiDeeZ/Resonance) *(Original Repository)*
* **GameCube & Wii Runtime:** [iHaiDeeZ/DolphinPS4](https://github.com/iHaiDeeZ/DolphinPS4) *(Original Repository)*
* **Classic Package Conversion Utility:** [SvenGDK/PS-Classics-fPKG-Builder](https://github.com/SvenGDK/PS-Classics-fPKG-Builder) *(Original Repository)*

---

*Note: This technical portfolio documentation utilizes AI design formatting to present computer science concepts alongside clear, accessible explanations.*
