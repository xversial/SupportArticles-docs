---
title: Support Policy for NIC Teaming
description: Describes the Microsoft Support Policy for Network Adapter Teaming when used in conjunction with Hyper-V.
ms.date: 09/22/2020
author: Deland-Han 
ms.author: delhan
manager: dscontentpm
audience: itpro
ms.topic: troubleshooting
ms.prod: windows-server
localization_priority: medium
ms.reviewer: kaushika
ms.prod-support-area-path: Installation and configuration of Hyper-V
ms.technology: HyperV
---
# Microsoft Support Policy for NIC Teaming with Hyper-V

This article describes the Microsoft Support Policy for Network Adapter Teaming when used in conjunction with Hyper-V.

_Original product version:_ &nbsp; Windows Server 2012 R2  
_Original KB number:_ &nbsp; 968703

## RAPID PUBLISHING

RAPID PUBLISHING ARTICLES PROVIDE INFORMATION DIRECTLY FROM WITHIN THE MICROSOFT SUPPORT ORGANIZATION. THE INFORMATION CONTAINED HEREIN IS CREATED IN RESPONSE TO EMERGING OR UNIQUE TOPICS, OR IS INTENDED SUPPLEMENT OTHER KNOWLEDGE BASE INFORMATION.

## Introduction

Network Adapter Teaming is a third-party Technology that provides fault tolerance for multiple Network Adapters.

## Summary

Since Network Adapter Teaming is only provided by Hardware Vendors, Microsoft does not provide any support for this technology through Microsoft Product Support Services. As a result, Microsoft may ask that you temporarily disable or remove Network Adapter Teaming software when troubleshooting issues where the teaming software is suspect.

If the problem is resolved by the removal of Network Adapter Teaming software, then further assistance must be obtained through the Hardware Vendor.

## More information

Common symptoms exhibited due to improperly configured NIC Teaming software:

- After a live migration of a virtual machine (VM) is performed, the VM loses network connectivity

- Virtual machines intermittently lose network connectivity

- The following event is logged in the System event log on the Hyper-V server:

    > Log Name: System  
    Source: VMSMP  
    Event ID: 28  
    Level: Warning  
    Description: Port '97B1A2BA-D679-4290-AD9B-262DE33C16D6' was prevented from using MAC address '00-15-D5-04-F8-0C' because it is pinned to port 'BFA4D592-1F9D-8484-8ABF-9EDA1534529E'.

## DISCLAIMER

MICROSOFT AND/OR ITS SUPPLIERS MAKE NO REPRESENTATIONS OR WARRANTIES ABOUT THE SUITABILITY, RELIABILITY OR ACCURACY OF THE INFORMATION CONTAINED IN THE DOCUMENTS AND RELATED GRAPHICS PUBLISHED ON THIS WEBSITE (THE "MATERIALS") FOR ANY PURPOSE. THE MATERIALS MAY INCLUDE TECHNICAL INACCURACIES OR TYPOGRAPHICAL ERRORS AND MAY BE REVISED AT ANY TIME WITHOUT NOTICE.

TO THE MAXIMUM EXTENT PERMITTED BY APPLICABLE LAW, MICROSOFT AND/OR ITS SUPPLIERS DISCLAIM AND EXCLUDE ALL REPRESENTATIONS, WARRANTIES, AND CONDITIONS WHETHER EXPRESS, IMPLIED OR STATUTORY, INCLUDING BUT NOT LIMITED TO REPRESENTATIONS, WARRANTIES, OR CONDITIONS OF TITLE, NON INFRINGEMENT, SATISFACTORY CONDITION OR QUALITY, MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE, WITH RESPECT TO THE MATERIALS.