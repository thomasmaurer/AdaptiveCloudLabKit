## Unofficial Azure Adaptive Cloud Lab Kit x Arc Jumpstart Overview

The Unofficial Azure Adaptive Cloud Lab Kit x Arc Jumpstart allows you to test various kinds of Azure Adaptive Cloud solutions for hybrid cloud and edge computing, using technologies such as Azure Arc, Azure Stack HCI, and Azure IoT. It provides a physical NUC compute unit running Windows Server 2025 with a virtualization environment specially designed to work with home labs and edge scenarios. It also provides automated zero-to-hero scenarios for Azure Arc and Azure IoT using the Arc Jumpstart.

![Unofficial Azure Adaptive Cloud Lab Kit x Arc Jumpstart](./artifacts/media/Azure-Adaptive-Cloud-Lab-Kit-x-Arc-Jumpstart.jpg#center)

The lab environment provides you with a virtual lab environment, including a physical Hyper-V server running Windows Server 2025 which allows you to run virtual machines. This allows you to leverage this as a platform to run Arc Jumpstart scenarios to try adaptive cloud solutions for hybrid cloud and edge scenarios. It also includes the possibilities to test Azure services such as:

- Arc-enabled servers
- Arc-enabled SQL Server
- Arc-enabled Kubernetes
- Arc-enabled data services
- Arc-enabled app services
- Arc-enabled machine learning
- Arc, Edge, and Azure IoT Operations
- Arc and Azure Lighthouse
- AKS enable by Azure Arc, AKS Edge Essentials
- and more

> [!NOTE]
> The unofficial Adaptive Cloud Lab Kit is **not** supported by Microsoft and only has community support. This project is **not** sponsored by any third-party.

## Contributors

This Jumpstart Drop was originally written by the following contributors:

- [Thomas Maurer | Principal Program Manager](https://www.linkedin.com/in/thomasmaurer2)

- [Contribute to the Azure Adaptive Cloud Lab Kit](https://github.com/thomasmaurer/AdaptiveCloudLabKit/)

## Getting Started

The Azure Adaptive Cloud Lab Kit x Arc Jumpstart consists of two components: the lab environment and the self-guided Arc Jumpstart scenarios. The Arc Jumpstart scenarios are directly hosted on the Arc Jumpstart website and can be used for creating your labs.

![Azure Adaptive Cloud Lab Kit Architecture](./artifacts/media/Azure-Adaptive-Cloud-Lab-Kit-Archiecture.jpg#center)

### Important things to know 

- This lab kit contains evaluation software that is designed for IT professionals interested in evaluating Windows Server and Azure solutions and tools on behalf of their organization. We do not recommend that you install this evaluation if you are not an IT professional or are not professionally managing corporate networks or devices.
- Additionally, the lab environment is intended for evaluation purposes only. It is a standalone virtual environment and should not be used or connected to your production environment.
- The Windows Server 2025 Evaluation version expires 180 days after the lab is provisioned.
- This project is a community project and is **not** sponsored by any third-party.
- The unofficial Adaptive Cloud Lab Kit is **not** supported by Microsoft and only has community support.
- You are welcome to [support and contirbute to the project](https://github.com/thomasmaurer/AdaptiveCloudLabKit/).
- Windows Server 2025 Evaluation licenses should only be used for evaluation porpuses.
- By enabling additional Azure services, additional costs may apply.

## Prerequisites

To get started with the Azure Adaptive Cloud Lab Kit you need the following:

- Lab Kit Hardware (Intel ASUS NUC or similar)
- Windows Server 2025 Evaluation version
- USB flash drive
- Azure Subscription
- Internet Connectivity

### Lab Kit Hardware

The Azure Adaptive Cloud Lab Kit x Arc Jumpstart consists of, and is built by using an Intel NUC, NUC stands for Next Unit of Computing and is a line of small-form-factor barebone computer kits designed by Intel. The advantage of this machine is the small formfactor, low power consumption and almost no fan noise.

> [!NOTE]
> Also other hardware systems with similar specifications can be used.

| Amount| Hardware | 
| ------- | -- | 
| 1x | ASUS NUC 13 Pro Kit NUC13ANHi5 (Intel Core i5-1340P) | 
| 1x | WD Black SN850X 1000 GB, M.2 2280 | 
| 2x | Corsair Vengeance 32GB, 3200 MHz, DDR4-RAM, SO-DIMM |

> [!NOTE]
> The Intel ASUS NUC hardware doesn't provide any drivers for Windows Server operating systems. Therefore, networking drivers need to be added with a workaround.

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

Download the latest Windows Server 2025 Evaluation version here: 

[Evaluaton Center](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2025)

### Azure Subscription

To use Azure services, you will need to use an Azure subscription. If you don't have an Azure subscription check out the following links:

[Azure free account](https://azure.microsoft.com/free/)

### Internet Connectivity

Please use a broad bandwidth to download this content to enhance your downloading experience.

## Installation Guide

You can follow these basic steps to set up your Azure Adaptive Cloud Lab Kit feat. Arc Jumpstart with the following steps.

### Build your NUC hardware

If your hardware is not yet built, you will need to set up SSD storage and memory in your Intel ASUS NUC.

![NUC Hardware](./artifacts/media/Intel-NUC-Windows-Server-LAB.jpg#center)

### Install Windows Server 2025

Install Windows Server 2025 on your Intel NUC. You can create a bootable USB drive to install Windows Server 2025 using the following guide.

To create the USB drive to install Windows Server 2025 on a UEFI (GPT system, you do the following steps:

- The at least an 8GB USB drive has to be formatted in FAT32
- The USB needs to be GPT and not MBR
- You will need to split the wim file using dism since it is larger than 4GB
- Copy all files from the ISO to the USB drive
- This is it, and here is how you do it. First, plug in your USB drive to your computer.

Open a PowerShell using the Run as Administrator option. You will need to change the path of the Windows Server 2025 ISO, and you will need to replace the disk number in the script before running the third command and make sure *C:\Temp* exists. From previous experiences with users, run the script line by line.

> [!NOTE]
> The following commands will wipe the USB Drive completely. Backup everything before you run through the PowerShell.

```powershell
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

Download the latest Networking Drivers for Windows 11 on the ASUS Intel NUC (Intel Ethernet (LAN) Driver for Windows 11 for Intel NUC 13 Pro Kit / Mini PC) [support site](https://www.asus.com/us/displays-desktops/nucs/nuc-mini-pcs/asus-nuc-13-pro/helpdesk_download?model2Name=ASUS-NUC-13-Pro).

> [!NOTE]
> This driver can also be forced to use with Windows Server 2025. Keep in mind it is not recommended to do this with production systems.

![Download ASUS Intel NUC Network Adapter NIC driver](./artifacts/media/Download-ASUS-Intel-NUC-Network-Adapter-NIC-driver-scaled.jpg#center)

Copy the drivers to your ASUS Intel NUC and extract driver zip file and you will see the following files:

![Intel NIC drivers](./artifacts/media/Intel-NIC-Drivers.jpg#center)

Open Device Manager right click on **Ethernet Controller** and select **Update Driver**.

![Update Network Driver](./artifacts/media/Update-Network-Driver.jpg#center)

Select **“Browe on my computer for driver software”**, and select **“Let me pick from a list of available drivers on my computer”**, now you can select **Network Adapter**.

![Let me pick from a list of available drivers on my computer](./artifacts/media/Let-me-pick-from-a-list-of-available-drivers-on-my-computer.jpg#center)

Click on **“Have Disk…”** enter the following path where you extracted the drivers to.

![Driver Location](./artifacts/media/Driver-Location.jpg#center)

Now select Intel Ethernet Connection I219-LM

![Intel Ethernet Controller I225-LM](./artifacts/media/Intel-Ethernet-Controller-I225-LM.jpg#center)

Now you are done and you will be able to use the network adapter of the Asus Intel NUC with Windows Server 2025.

> [!NOTE]
> As a workaround you can also use a USB to Ethernet adapter. [Original Guide: Install ASUS Intel NUC Windows Server 2025 Network Adapter Driver](https://www.thomasmaurer.ch/2024/07/install-asus-intel-nuc-windows-server-2025-network-adapter-driver/)

### Set name of your Azure Adaptive Cloud LabKit

Run the following command to change the server name of your Adaptive Cloud Lab Kit:

```powershell
Rename-Computer -NewName "AdaptiveCloudLabKit01"
```

### Set up Hyper-V

After you have successfully installed the network driver for your machine, make sure you installed the latest Microsoft Updates.

Now you can enable the Hyper-V role, which will allow you to create virtual machines running on your Azure Adaptive Cloud Lab Kit. You can use the following PowerShell command to [install the Hyper-V role](https://www.thomasmaurer.ch/2017/08/install-hyper-v-on-windows-server-using-powershell/). After running this command you will need to restart your Lab Kit.

```powershell
Install-WindowsFeature -Name Hyper-V -IncludeAllSubFeature -IncludeManagementTools
```
### Onboard Azure Adaptive Cloud Lab Kit to Azure using Azure Arc

You can start the Azure Arc Setup wizard in different ways on a Windows Server machine. One way is to click on the system tray icon at the bottom of the screen. This icon appears when the Azure Arc Setup feature is turned on, which is the default setting. Another way is to open the pop-up window in the Server Manager. A third way is to go to the Windows Server Start menu and select the wizard from there.

![Get Started with Azure Arc Setup on Windows Server](./artifacts/media/Get-Started-with-Azure-Arc-Azure-Arc-Setup-on-Windows-Server.jpg#center)

Follow the wizard to onboard your Adaptive Cloud Lab kit with Azure Arc. If you need more information check out the following [page](https://www.thomasmaurer.ch/2023/12/azure-arc-setup-on-windows-server/).

![Installing Azure Arc on Winodws Server](./artifacts/media/Installing-Azure-Arc-on-Winodws-Server.jpg#center)

Your Adaptive Cloud Lab Kit is now ready to run virtual machines, Kubernetes clusters and other workloads and connect them using Azure Arc and deploy Arc Jumpstart scenarios.

## Jumpstart Scenarios

With the Azure Adaptive Cloud Lab Kit hardware in place, you're now equipped to dive into a variety of Arc Jumpstart scenarios. This setup enables you to thoroughly evaluate hybrid cloud and edge computing environments. Utilizing services like Azure Arc, Azure Kubernetes Service (AKS), Azure Stack HCI, and Azure IoT, you can explore and test the integration and management capabilities of Azure across different infrastructures, ensuring a seamless and scalable deployment of applications and services.

Check out the following Arc Jumpstart scenarios:

- [Arc-enabled servers](https://azurearcjumpstart.io/azure_arc_jumpstart/azure_arc_servers)
- [Arc-enabled Kubernetes](https://azurearcjumpstart.io/azure_arc_jumpstart/azure_arc_k8s)
- [Arc-enabled SQL Server](https://azurearcjumpstart.io/azure_arc_jumpstart/azure_arc_sqlsrv)
- [Arc, Edge, and Azure IoT Operations](https://azurearcjumpstart.io/azure_arc_jumpstart/azure_edge_iot_ops)
- [Arc and Azure Lighthouse](https://azurearcjumpstart.io/azure_arc_jumpstart/azure_arc_lighthouse)
- [Arc-enabled data services](https://azurearcjumpstart.io/azure_arc_jumpstart/azure_arc_data)
- and more on [ArcJumpstart.com](https://arcjumpstart.com/)

## Resources

You can find more information on related topics for the Azure Adaptive Cloud Lab Kit x Arc Jumpstart with the following links:

- [Contribute to the Azure Adaptive Cloud Lab Kit](https://github.com/thomasmaurer/AdaptiveCloudLabKit/)

To learn about Microsoft's Azure Adaptive Cloud approach, [get started with our homepage](https://azure.microsoft.com/solutions/hybrid-cloud-app/).

### Azure documentation

- [Azure Arc Documentations](https://learn.microsoft.com/azure/azure-arc/)
- [Azure Stack HCI Documentations](https://learn.microsoft.com/azure-stack/hci/)
- [Azure Kubernetes Service (AKS) enabled by Azure Arc Documentations](https://learn.microsoft.com/azure/aks/hybrid/)
- [Azure IoT Documentations](https://learn.microsoft.com/azure/iot/)

### Addtional assets

- [Arc Jumpstart](https://aka.ms/AzureArcJumpstart)
- [Azure Arc Landing Zone Accelerators](https://aka.ms/ArcLZAcceleratorReady)
