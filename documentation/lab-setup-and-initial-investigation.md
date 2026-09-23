Lab Setup and Initial Investigation
Overview
This document records the practical steps taken while building my Windows SOC Investigation & Detection Lab.
The goal of this project is to build hands-on experience investigating Windows endpoint activity using native Windows logs, Sysmon, Event Viewer, and PowerShell.
Rather than focusing only on memorizing Windows Event IDs, I am practicing how a SOC analyst would approach endpoint activity:
Activity → Evidence → Timeline → Context → Investigation → Finding**
This document records the lab setup and the first investigations completed so far.
---
1. Lab Environment
The first step was to create an isolated Windows environment that could be used to generate and investigate security-related activity without affecting my main computer.

Host Environment
- Host operating system: Windows 10
- RAM: 8 GB
- Storage: 256 GB SSD
- Virtualization platform: VirtualBox

Windows SOC Lab VM
- Operating system: Windows 10
- RAM: 3 GB
- CPU: 2 cores
- Disk: 50 GB dynamically allocated
- Network mode: NAT

The VM was intentionally configured with limited resources because the lab is being built on a personal machine.
The objective was to keep the environment lightweight while still providing enough resources for Windows security monitoring and investigation.
---

2. Created the SOC Lab Workspace
I created a dedicated workspace inside the Windows VM to keep investigation material organized.
C:\SOC-Lab
│
├── screenshots
├── investigations
├── detections
├── evidence
└── documentation
