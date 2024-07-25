---
type: docs
title: "Unofficial Azure Adaptive Cloud Lab Kit x Arc Jumpstart"
linkTitle: "Unofficial Azure Adaptive Cloud Lab Kit x Arc Jumpstart"
weight: 1
description: >
---

## Unofficial Azure Adaptive Cloud Lab Kit x Arc Jumpstart

The Unofficial Azure Adaptive Cloud Lab Kit x Arc Jumpstart allows you to test various kinds of Azure Adaptive Cloud solutions for hybrid cloud and edge computing, using technologies such as Azure Arc, Azure Stack HCI, and Azure IoT. It provides a physical compute unit with a virtualization environment specially designed to work with home labs and edge scenarios. It also provides automated zero-to-hero scenarios for Azure Arc and Azure IoT using the Arc Jumpstart.

![Unofficial Azure Adaptive Cloud Lab Kit x Arc Jumpstart](./artifacts/media/Azure-Adaptive-Cloud-Lab-Kit-x-Arc-Jumpstart.jpg#center)

The lab environment provides you with a virtual lab environment, including a physical Hyper-V server running Windows Server 2025 which allows you to run virtual machines. This allows you to leverage this as a platform to run Arc Jumpstart scenarios to try adaptive cloud solutions for hybrid cloud and edge scenarios. It also includes the possibilities to test Azure services such as:

- Arc-enabled servers
- Arc-enabled SQL Server
- Arc-enabled Kubernetes
- Arc-enabled data services
- Arc-enabled app services
- Arc-enabled machine learning
- Arc, Edge, and IoT Operations
- Arc and Azure Lighthouse
- AKS enable by Azure Arc, AKS Edge Essentials
- and more

## Contributors

This Jumpstart Drop was originally written by the following contributors:

- [Thomas Maurer | Principal Program Manager](https://www.linkedin.com/in/thomasmaurer2)

## Getting Started

The Azure Adaptive Cloud Lab Kit x Arc Jumpstart consists of two components: the lab environment and the self-guided Arc Jumpstart scenarios. The Arc Jumpstart scenarios are directly hosted on the Arc Jumpstart website and can be used for creating your labs.

### Things to Know 

- This lab kit contains evaluation software that is designed for IT professionals interested in evaluating Windows Server and Azure solutions and tools on behalf of their organization. We do not recommend that you install this evaluation if you are not an IT professional or are not professionally managing corporate networks or devices.
- Additionally, the lab environment is intended for evaluation purposes only. It is a standalone virtual environment and should not be used or connected to your production environment.
- The Windows Server 2025 Evaluation version expires 180 days after the lab is provisioned.

![Azure Adaptive Cloud Lab Kit Architecture](./artifacts/media/Azure-Adaptive-Cloud-Lab-Kit-Archiecture.jpg#center)

## Prerequisites

To get started with the Azure Adaptive Cloud Lab Kit you need the following:

- Lab Kit Hardware (Intel ASUS NUC or similar)
- Windows Server 2025 Evaluation version
- Azure Subscription
- Internet Connectivity

### Lab Kit Hardware

The Azure Adaptive Cloud Lab Kit x Arc Jumpstart consists of, and is built by using an Intel NUC, NUC stands for Next Unit of Computing and is a line of small-form-factor barebone computer kits designed by Intel. The advantage of this machine is the small formfactor, low power consumption and almost no fan noise.

Note: Also other hardware systems with similar specifications can be used.

- 1x ASUS NUC 13 Pro Kit NUC13ANHi5 (Intel Core i5-1340P)
- 1x WD Black SN850X 1000 GB, M.2 2280
- 2x Corsair Vengeance 32GB, 3200 MHz, DDR4-RAM, SO-DIMM

Note: The Intel ASUS NUC hardware doesn't provide any drivers for Windows Server operating systems. Therefore, networking drivers need to be added with a workaround.

![Lab Kit hardware](./artifacts/media/Lab-Kit-Hardware-Intel-ASUS-NUC-scaled.jpg#center)

 ### System Requirements

- The lab environment used with this lab guide supports the 64-bit editions of Windows Server 2025 or later. 
- The Hyper-V Host on which the lab needs to be imported must meet the following minimum specifications:
- Hyper-V role installed
- Administrative rights on the device
- 500 GB of free disk space (1TB recommended)
- High-throughput disk subsystem
- 32GB of available memory (64 GB recommended)
- High-end processor for faster processing (Intel Core i5 or higher)

### Windows Server 2025 Evaluation version

Download the latest Windows Server 2025 Evaluation version here: [Evaluaton Center](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2025)

### Azure Subscription

To use Azure services, you will need to use an Azure subscription. If you don't have an Azure subscription check out the following links:

[Azure free account](https://azure.microsoft.com/free/)

### Internet Connectivity

Please use a broad bandwidth to download this content to enhance your downloading experience.

## Installation Guide

You can follow these basic steps to set up your unofficial Azure Adaptive Cloud Lab Kit feat. Arc Jumpstart with the following steps.

### Build your NUC hardware

If your hardware is not yet built, you will need to set up SSD storage and memory in your Intel ASUS NUC.

![NUC Hardware](./artifacts/media/Intel-NUC-Windows-Server-LAB.jpg#center)

### Install Windows Server 2025

Install Windows Server 2025 on your Intel NUC. You can create a bootable USB drive to install Windows Server 2025 using the following [guide](https://www.thomasmaurer.ch/2024/07/create-an-usb-drive-for-windows-server-2025-installation/).

To create the USB drive to install Windows Server 2025 on a UEFI (GPT system, you do the following steps:

- The at least an 8GB USB drive has to be formatted in FAT32
- The USB needs to be GPT and not MBR
- You will need to split the wim file using dism since it is larger than 4GB
- Copy all files from the ISO to the USB drive
- This is it, and here is how you do it. First, plug in your USB drive to your computer.

Open a PowerShell using the Run as Administrator option. You will need to change the path of the Windows Server 2025 ISO, and you will need to replace the disk number in the script before running the third command and make sure C:\Temp exists. From previous experiences with users, run the script line by line.

REMINDER: The following commands will wipe the USB Drive completely. Backup everything before you run through the PowerShell.

```sh
# Define Path to the Windows Server 2025 ISO
$ISOFile = "C:\Temp\WindowsServer2025.iso"

# Create temp diectroy for new image
$newImageDir = New-Item -Path 'C:\Temp\newimage' -ItemType Directory

# Mount iso
$ISOMounted = Mount-DiskImage -ImagePath $ISOFile -StorageType ISO -PassThru

# Driver letter
$ISODriveLetter = ($ISOMounted | Get-Volume).DriveLetter

# Copy Files to temporary new image folder 
Copy-Item -Path ($ISODriveLetter +":\*") -Destination C:\Temp\newimage -Recurse

# Split and copy install.wim (because of the filesize)
dism /Split-Image /ImageFile:C:\Temp\newimage\sources\install.wim /SWMFile:C:\Temp\newimage\sources\install.swm /FileSize:4096

 
# Get the USB Drive you want to use, copy the disk number
Get-Disk | Where BusType -eq "USB"
 
# Get the right USB Drive (You will need to change the number)
$USBDrive = Get-Disk | Where Number -eq 2
 
# Replace the Friendly Name to clean the USB Drive (THIS WILL REMOVE EVERYTHING)
$USBDrive | Clear-Disk -RemoveData -Confirm:$true -PassThru
 
# Convert Disk to GPT
$USBDrive | Set-Disk -PartitionStyle GPT
 
# Create partition primary and format to FAT32
$Volume = $USBDrive | New-Partition -Size 8GB -AssignDriveLetter | Format-Volume -FileSystem FAT32 -NewFileSystemLabel WS2025
 
# Copy Files to USB (Ignore install.wim)
Copy-Item -Path C:\Temp\newimage\* -Destination ($Volume.DriveLetter + ":\") -Recurse -Exclude install.wim

# Dismount ISO
Dismount-DiskImage -ImagePath $ISOFile
```

### Install Network Driver

If you are using an Intel NUC, Windows Server will not detect the network driver automatically. You will need to download the Windows 11 network driver from the official support site and follow the following guide to install it.

[Install ASUS Intel NUC Windows Server 2025 Network Adapter Driver](https://www.thomasmaurer.ch/2024/07/install-asus-intel-nuc-windows-server-2025-network-adapter-driver/)

As a workaround you can also use a USB to Ethernet adapter.

### Set up Hyper-V

After you have successfully installed the network driver for your machine, make sure you installed the latest Microsoft Updates.

Now you can enable the Hyper-V role, which will allow you to create virtual machines running on your Azure Adaptive Cloud Lab Kit. You can use the following PowerShell command to [install the Hyper-V role](https://www.thomasmaurer.ch/2017/08/install-hyper-v-on-windows-server-using-powershell/). After running this command you will need to restart your Lab Kit.

```sh
    Install-WindowsFeature -Name Hyper-V -IncludeAllSubFeature -IncludeManagementTools
```

## Jumpstart Scenarios

With the Azure Adaptive Cloud Lab Kit hardware in place, you're now equipped to dive into a variety of Arc Jumpstart scenarios. This setup enables you to thoroughly evaluate hybrid cloud and edge computing environments. Utilizing services like Azure Arc, Azure Kubernetes Service (AKS), Azure Stack HCI, and Azure IoT, you can explore and test the integration and management capabilities of Azure across different infrastructures, ensuring a seamless and scalable deployment of applications and services.

Check out the following Arc Jumpstart scenarios:

## Resources

You can find more information on related topics for the Unofficial Azure Adaptive Cloud Lab Kit x Arc Jumpstart with the following links:

To learn about Microsoft's Azure Adaptive Cloud approach, [get started with our homepage](https://azure.microsoft.com/solutions/hybrid-cloud-app/).

### Azure documentation

- [Azure Arc Documentations](https://learn.microsoft.com/azure/azure-arc/)
- [Azure Stack HCI Documentations](https://learn.microsoft.com/azure-stack/hci/)
- [Azure Kubernetes Service (AKS) enabled by Azure Arc Documentations](https://learn.microsoft.com/azure/aks/hybrid/)
- [Azure IoT Documentations](https://learn.microsoft.com/azure/iot/)

### Addtional assets

- [Arc Jumpstart](https://aka.ms/AzureArcJumpstart)
- [Azure Arc Landing Zone Accelerators](https://aka.ms/ArcLZAcceleratorReady)
