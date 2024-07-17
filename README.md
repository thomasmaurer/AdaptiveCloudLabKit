---
type: docs
title: "Unofficial Azure Adaptive Cloud Lab Kit x Arc Jumpstart"
linkTitle: "Unofficial Azure Adaptive Cloud Lab Kit x Arc Jumpstart"
weight: 1
description: >
---

## Unofficial Azure Adaptive Cloud Lab Kit x Arc Jumpstart

The Unofficial Azure Adaptive Cloud Lab Kit x Arc Jumpstart allows you to test various kinds of Azure Adaptive Cloud solutions for hybrid cloud and edge computing, using technologies such as Azure Arc, Azure Stack HCI, and Azure IoT. It provides a physical compute unit with a virtualization environment specially designed to work with home labs and edge scenarios. It also provides automated zero-to-hero scenarios for Azure Arc and Azure IoT using the Arc Jumpstart.

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

### Architecture

Azure Adaptive Cloud Lab Kit Architecture

## Prerequisites

To get started with the Azure Adaptive Cloud Lab Kit you need the following:

- Lab Kit Hardware (Intel ASUS NUC or similar)
- Windows Server 2025 Evaluation version
- Azure Subscription
- Internet Connectivity

### Lab Kit Hardware

The Azure Adaptive Cloud Lab Kit x Arc Jumpstart consists of, and is built by using an Intel NUC, NUC stands for Next Unit of Computing and is a line of small-form-factor barebone computer kits designed by Intel. The advantage of this machine is the small formfactor, low power consumption and almost no fan noise.

Note: Also other hardware systems with similar specifications can be used.

- 1x Intel NUCPAHIi5 (Intel Core i5-1135G7)
- 1x Samsung 970 EVO Plus (1000 GB, M.2)
- 2x Kingston ValueRAM (32GB, DDR4-2666, SO-DIMM 260 pin)

Note: The Intel ASUS NUC hardware doesn't provide any drivers for Windows Server operating systems. Therefore, networking drivers need to be added with a workaround.

### Windows Server 2025 Evaluation version

Download the latest Windows Server 2025 Evaluation version here: Evaluaton Center

### Azure Subscription

To use Azure services, you will need to use an Azure subscription. If you don't have an Azure subscription check out the following links:

Azure free account

### Internet Connectivity

Please use a broad bandwidth to download this content to enhance your downloading experience.

## Installation Guide

You can follow these basic steps to set up your unofficial Azure Adaptive Cloud Lab Kit feat. Arc Jumpstart with the following steps.

### Build your NUC hardware

If your hardware is not yet built, you will need to set up SSD storage and memory in your Intel ASUS NUC.

### Install Windows Server 2025

Install Windows Server 2025 on your Intel NUC. You can create a bootable USB drive to install Windows Server 2025 using the following guide.

https://www.thomasmaurer.ch/2024/07/create-an-usb-drive-for-windows-server-2025-installation/
Create an USB Drive for Windows Server 2025 Installation

### Install Network Driver

If you are using an Intel NUC, Windows Server will not detect the network driver automatically. You will need to download the Windows 11 network driver from the official support site and follow the following guide to install it.

https://www.thomasmaurer.ch/2024/07/install-asus-intel-nuc-windows-server-2025-network-adapter-driver/
Install ASUS Intel NUC Windows Server 2025 Network Adapter Driver

As a workaround you can also use a USB to Ethernet adapter.

### Set up Hyper-V

After you have successfully installed the network driver for your machine, make sure you installed the latest Microsoft Updates.

Now you can enable the Hyper-V role, which will allow you to create virtual machines running on your Azure Adaptive Cloud Lab Kit. You can use the following PowerShell command to install the Hyper-V role. After running this command you will need to restart your Lab Kit.

```sh
    Install-WindowsFeature -Name Hyper-V -IncludeAllSubFeature -IncludeManagementTools
```
