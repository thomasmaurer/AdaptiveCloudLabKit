---
type: docs
title: "Unofficial Azure Adaptive Cloud Lab Kit x Arc Jumpstart"
linkTitle: "Unofficial Azure Adaptive Cloud Lab Kit x Arc Jumpstart"
weight: 1
description: >
---

## Unofficial Azure Adaptive Cloud Lab Kit x Arc Jumpstart

The Unofficial Azure Adaptive Cloud Lab Kit x Arc Jumpstart allows you to test various kinds of Azure Adaptive Cloud solutions for hybrid cloud and edge computing, using technologies such as Azure Arc, Azure Stack HCI, and Azure IoT. It provides a physical compute unit with a virtualization environment specially designed to work with home labs and edge scenarios. It also provides automated zero-to-hero scenarios for Azure Arc and Azure IoT using the Arc Jumpstart.
## Contributors

This Jumpstart Drop was originally written by the following contributors:

- [Thomas Maurer | Principal Program Manager](https://www.linkedin.com/in/thomasmaurer2)

## Prerequisites

- **Operating System:** Windows 11 IoT Enterprise 22H2 Image or later.
- **Administrative Access:** System with administrative privileges.
- **Technical Knowledge:** Familiarity with command-line operations and system configuration.

## Getting Started

The Azure Adaptive Cloud Lab Kit x Arc Jumpstart consists of two components: the lab environment and the self-guided Arc Jumpstart scenarios. The Arc Jumpstart scenarios are directly hosted on the Arc Jumpstart website and can be used for creating your labs.

### Things to Know 

- This lab kit contains evaluation software that is designed for IT professionals interested in evaluating Windows Server and Azure solutions and tools on behalf of their organization. We do not recommend that you install this evaluation if you are not an IT professional or are not professionally managing corporate networks or devices.
- Additionally, the lab environment is intended for evaluation purposes only. It is a standalone virtual environment and should not be used or connected to your production environment.
- The Windows Server 2025 Evaluation version expires 180 days after the lab is provisioned.

### Architecture

Azure Adaptive Cloud Lab Kit Architecture

## Description

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

