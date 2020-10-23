---
title: The system can't find the file specified
description: Discusses errors when you use the Adprep tool together with the /gpprep argument.
ms.date: 09/23/2020
author: Deland-Han 
ms.author: delhan
manager: dscontentpm
audience: itpro
ms.topic: troubleshooting
ms.prod: windows-server
localization_priority: medium
ms.reviewer: kaushika, nedpyle
ms.prod-support-area-path: Group Policy management - GPMC or AGPM
ms.technology: GroupPolicy
---
# "The system cannot find the file specified" Adprep /gpprep error, or tool crashes

This article provides a solution to errors that occur when you use the Adprep tool together with the /gpprep argument.

_Original product version:_ &nbsp; Windows Server 2012 R2  
_Original KB number:_ &nbsp; 2743345

## Symptoms

You use the Adprep tool together with the /gpprep argument on Windows Server 2012. For example, you run the following arguments:  
adprep.exe /domainprep /gpprep

When you do this, you receive the following error:

> Domain-wide information has already been updated.  
[Status/Consequence]  
Adprep did not attempt to rerun this operation.  
>
> Adprep is about to upgrade the Group Policy Object (GPO) information on the Infrastructure Master FSMO dc1.corp.contoso.com.
>
> Gpprep operation 3 failed.  
[Status/Consequence]  
Upgrade of domain Group Policy Objects failed.  
[User Action]  
Check the log file ADPrep.log and gpprep.log in the C:\Windows\debug\adprep\logs\20120809082547 directory for possible cause of failure.  
>
> Adprep encountered a Win32 error.  
Error code: 0x2 Error message: The system cannot find the file specified.
>
> Group policy upgrade failed.  
[Status/Consequence]  
Upgrade of domain Group Policy Objects failed.  
[User Action]  
Check the log file ADPrep.log in the C:\Windows\debug\adprep\logs\20120809082547 directory for possible cause of failure.
>
> Adprep encountered a Win32 error.  
Error code: 0x2 Error message: The system cannot find the file specified.

If you use the Adprep.exe that is included with Windows Server 2008 R2, Adprep.exe crashes, and you receive an error that resembles the following:

> Nt5DS has stopped working
>
> Problem signature:  
Problem Event Name: APPCRASH  
Application Name: adprep.exe  
Application Version: 6.1.7601.17514  
Application Timestamp: 4ce7a045  
Fault Module Name: StackHash_9a46  
Fault Module Version: 6.1.7601.17725  
Fault Module Timestamp: 4ec4aa8e  
Exception Code: c0000374  
Exception Offset: 00000000000c40f2  
OS Version: 6.1.7601.2.1.0.274.10  
Locale ID: 1033  
Additional Information 1: 9a46  
Additional Information 2: 9a46fc9b92ce31eadc29a5f5673559ea  
Additional Information 3: ec6e  
Additional Information 4: ec6ee41ac19ad12f608f0599c2c1bb6f

If you use the Adprep.exe tool that is included with Windows Server 2008, there are no issues.

## Cause

The infrastructure operations master role holder in this domain implements a disjoint namespace. Adprep.exe assumes that computer names will match their domain names because this match is the default behavior in all versions of Windows.

## Resolution

> [!NOTE]
> All steps require membership in the Domain Admins group. Also, run commands at an elevated command prompt.

1. Locate the infrastructure master role holder in the domain. To do this, run the following command: netdom.exe query fsmo  

2. Disable incoming and outgoing (also known as " inbound and outbound") replication on the infrastructure master server. To do this, run the following command:

    repadmin.exe /options **<infrastructure_master_name>** +DISABLE_OUTBOUND_REPL +DISABLE_INBOUND_REPL

3. Log on to the infrastructure master server, and modify its Domain Name System (DNS) suffix. To do this, follow these steps:
    1. Start SYSDM.CPL, select **OK**, select **Change**, and then select **More**  
    2. Set the suffix in the **Primary DNS suffix of this computer** box to match the Active Directory Domain Services (AD DS) domain name instead of the current disjointed name.
4. Restart and log on to the infrastructure master server, and then run the following command:  
adprep.exe /domainprep /gpprep
5. Use SYSDM.CPL, and then follow the steps in step 3, except this time in step 3B, you must set the suffix in the **Primary DNS suffix of this computer** box to match the original disjoint name on the infrastructure master server.
6. Restart and then log on to the infrastructure master server, and enable inbound and outbound replication. To do this, use the following command:  
    repadmin.exe /options *\<infrastructure_master_name>* -DISABLE_OUTBOUND_REPL -DISABLE_INBOUND_REPL  

## More information

Gpprep adds cross-domain planning functionality for Group Policy and Resultant Set of Policy (RSOP) Planning Mode. Adding this functionality requires updating the file system in SYSVOL and AD DS permissions for existing group policies. The environment may already contain custom or delegated permissions that were manually implemented by administrators. In this case, gpprep triggers replication of all Group Policy files in SYSVOL and may deny RSOP functionality to delegated users until their permissions are recreated by administrators. So Administrators should run gpprep only one time in the history of a domain. Gpprep shouldn't be run with every upgrade.

Notes

- Gpprep was introduced in Windows Server 2003.
- Disjoint namespaces aren't a Microsoft best practice.

For more information about Disjoint Namespace support and limitations in AD DS, go to the following Microsoft TechNet website:  
[https://technet.microsoft.com/library/cc731125(v=WS.10).aspx](https://technet.microsoft.com/library/cc731125%28v=ws.10%29.aspx)