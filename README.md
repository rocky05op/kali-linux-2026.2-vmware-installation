# Kali Linux 2026.2 VMware Installation

## Week 1 Internship Task

This repository documents my Week 1 internship task: installing and configuring **Kali Linux 2026.2** as a virtual machine using **VMware Workstation**.

> **Note:** This repository documents my actual setup process. Installation screenshots are not included because I did not capture screenshots at every installation step. I have intentionally not used fabricated screenshots.

---

## Table of Contents

- [Objective](#objective)
- [Environment](#environment)
- [Requirements](#requirements)
- [Why a Pre-Built VMware Image](#why-a-pre-built-vmware-image)
- [Installation Procedure](#installation-procedure)
- [VMware Configuration](#vmware-configuration)
- [First Boot](#first-boot)
- [Verification](#verification)
- [Useful Commands](#useful-commands)
- [What I Learned](#what-i-learned)
- [Troubleshooting](#troubleshooting)
- [Repository Structure](#repository-structure)
- [References](#references)
- [Conclusion](#conclusion)

---

## Objective

The objective of this task was to:

1. Obtain the official Kali Linux 2026.2 VMware image.
2. Extract and import the pre-built virtual machine into VMware Workstation.
3. Configure the virtual machine's hardware and networking.
4. Boot Kali Linux successfully.
5. Verify the operating system, kernel, and network connectivity.
6. Document the process in a GitHub repository.

---

## Environment

| Component | Details |
|---|---|
| Host OS | Windows 11 |
| Virtualization Software | VMware Workstation |
| Guest OS | Kali Linux 2026.2 |
| Architecture | AMD64 / x86_64 |
| VM Type | Pre-built VMware virtual machine |
| Network Mode | NAT (recommended for a simple internet-connected VM) |

Kali provides official pre-built VMware images for users who want to run Kali as a guest virtual machine.

---

## Requirements

### Hardware

- 64-bit processor
- Hardware virtualization enabled in BIOS/UEFI
- Sufficient RAM for the VM
- Sufficient free storage
- Internet connection

### Software

- Windows 11 or another supported host OS
- VMware Workstation
- 7-Zip or another application capable of extracting `.7z` archives
- Official Kali Linux 2026.2 VMware image

---

## Why a Pre-Built VMware Image?

For this setup I used the **pre-built VMware image** instead of performing a fresh ISO installation.

The pre-built image is convenient because Kali provides a VMware-ready virtual machine. After extracting the archive, VMware can open the `.vmx` configuration file and boot the VM.

Official Kali documentation describes this workflow as:

1. Extract the VMware archive.
2. Open VMware Workstation.
3. Select **Open a Virtual Machine**.
4. Locate the `.vmx` file.
5. Review the VM settings.
6. Start the VM.

---

## Installation Procedure

### 1. Download the Official Kali VMware Image

I used the official Kali Linux 2026.2 VMware image:

```text
kali-linux-2026.2-vmware-amd64.7z
```

The file is an AMD64 VMware virtual machine archive.

**Important:** Kali recommends obtaining images from official sources and verifying downloaded images where practical.

---

### 2. Extract the Archive

I extracted the `.7z` archive using 7-Zip.

After extraction, the VMware virtual machine directory contains the VM configuration and virtual disk files.

Important file types include:

```text
.vmx
.vmdk
.nvram
```

The `.vmx` file is the VMware virtual machine configuration file.

The `.vmdk` file is the virtual hard disk.

---

### 3. Open the VM in VMware Workstation

I opened VMware Workstation and selected:

```text
Open a Virtual Machine
```

I then navigated to the extracted Kali directory and selected the `.vmx` file.

---

### 4. Review Virtual Machine Settings

Before booting, I reviewed the VM hardware configuration.

The main settings to check are:

- Memory (RAM)
- Processors
- Virtual disk
- Network adapter
- CD/DVD device
- USB controller
- Display settings

The exact resource allocation should depend on the host computer's available hardware.

---

### 5. Configure Network

For a basic internet-connected Kali VM, I used:

```text
Network Adapter → NAT
```

NAT allows the guest VM to access the internet through the host's network connection without requiring a separate physical network connection.

---

### 6. Start Kali Linux

After reviewing the settings, I powered on the virtual machine.

Kali Linux then booted into the desktop environment.

---

## First Boot

After the first successful boot, I logged into the Kali Linux desktop.

The official pre-built Kali VMware image uses:

```text
Username: kali
Password: kali
```

For security, the default password should not be treated as a permanent credential.

---

## Verification

After Kali started successfully, I verified the installation.

### Check Kali Version

```bash
cat /etc/os-release
```

This displays information about the installed operating system.

### Check Kernel

```bash
uname -a
```

This displays kernel and system information.

### Check Current User

```bash
whoami
```

Expected result:

```text
kali
```

### Check IP Address

```bash
ip addr
```

### Test Network Connectivity

```bash
ping -c 4 google.com
```

A successful response confirms basic network connectivity.

---

## System Update

After confirming that networking worked, the package information can be refreshed with:

```bash
sudo apt update
```

The system can then be upgraded with:

```bash
sudo apt full-upgrade -y
```

After major system updates, reboot when appropriate:

```bash
sudo reboot
```

---

## Useful Commands

| Command | Purpose |
|---|---|
| `cat /etc/os-release` | Display OS information |
| `uname -a` | Display kernel information |
| `whoami` | Display current user |
| `ip addr` | Display network interfaces and addresses |
| `ping -c 4 google.com` | Test basic network connectivity |
| `sudo apt update` | Refresh package information |
| `sudo apt full-upgrade -y` | Upgrade installed packages |
| `sudo reboot` | Restart the system |

---

## Troubleshooting

### VM boots to network/PXE boot

If VMware displays something similar to:

```text
Network boot from AMD ...
DHCP...
```

the VM is attempting network boot instead of booting from its virtual disk.

For a pre-built VMware VM, check that:

- The `.vmx` file was opened.
- The virtual disk (`.vmdk`) is present.
- The virtual disk is attached in **VM Settings → Hard Disk**.
- The VM is not accidentally configured to boot from the network first.

---

### Package manager installation failure

A package-manager error during an ISO installation can be caused by networking, repository, or mirror problems.

This repository uses the pre-built VMware image, so the normal workflow does not require going through the ISO installer package-selection screens.

---

### No Internet in Kali

Check:

```bash
ip addr
```

Then test:

```bash
ping -c 4 google.com
```

If there is no network connection, check the VMware network adapter and confirm that it is connected.

---

## What I Learned

During this task I learned:

- The basic purpose of virtualization.
- How VMware Workstation runs a guest operating system.
- The difference between a VM configuration file and a virtual disk.
- How to import a pre-built VMware virtual machine.
- How NAT networking works at a basic level.
- How to verify a Linux installation from the terminal.
- How to update a Debian-based Linux system with APT.
- How to document a technical task using GitHub and Markdown.
- The importance of downloading operating-system images from official sources.

---

## Repository Structure

```text
kali-linux-2026.2-vmware-installation/
│
├── README.md
├── LICENSE
├── .gitignore
│
├── notes/
│   └── installation-notes.md
│
└── screenshots/
    └── README.md
```

The `screenshots/` directory is intentionally kept empty of fabricated evidence. Genuine screenshots can be added later.

---

## Screenshots

I did not capture screenshots during every installation step.

Instead of creating misleading or fabricated screenshots, I recommend adding genuine screenshots of the completed environment, such as:

```text
screenshots/
├── vmware-settings.png
├── kali-desktop.png
├── kali-version.png
└── network-test.png
```

These can be captured from the actual VM after installation.

---

## References

- Kali Linux official website: https://www.kali.org/
- Kali Linux download page: https://www.kali.org/get-kali/
- Kali Linux VMware documentation: https://www.kali.org/docs/virtualization/
- Import Pre-Made Kali VMware VM: https://www.kali.org/docs/virtualization/import-premade-vmware/
- Kali Linux image documentation: https://www.kali.org/docs/introduction/download-official-kali-linux-images/

---

## Conclusion

Kali Linux 2026.2 was successfully installed and configured as a virtual machine using VMware Workstation.

The completed setup provides an isolated Linux environment that can be used for learning Linux administration, networking, and cybersecurity concepts in a controlled virtual machine.

---

**Author:** Rocky  
**Task:** Week 1 Internship  
**Project:** Kali Linux 2026.2 VMware Installation
