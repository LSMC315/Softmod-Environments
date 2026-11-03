# Softmod & Infrastructure Environments

This repository tracks my local development environments, automation deployment logic, hardware verification logs, and storage architecture splits.

## Repository Architecture

```text
├── README.md               # The main portfolio page (Project overview & summary)
├── docs/
│   ├── hardware-validation.md # Motherboard, MFR date, and amperage cross-checks
│   ├── flash-dump-logic.md   # Step-by-step reading/writing the NAND flash memory
│   └── partition-splitting.md # Technical layout of the 8TB multi-system split array
└── configuration/
    └── aurora_scan_paths.json # Mock example of your custom storage tracking paths
```

## System Targets & Storage Blueprint
- **PS4 Slim Host:** Firmly locked onto firmware **13.52** via WebKit pathing. Employs an internal 500GB PNY CS900 SSD.
- **Xbox 360 Host:** Slim iteration provisioned for storage testing and pipeline automation.
- **8TB Storage Array Platform Split:** 
  - **2TB FAT32 Partition:** Exclusively map-routed for native Xbox 360 dashboard storage utility limits.
  - **6TB exFAT Partition:** Allocated strictly for automated PS4 package deployment packages.
  
docs: initialize master repository layout documentation
