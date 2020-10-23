---
title: Add print directory feature
description: Describes how to add the print directory feature, and how to enable printing of the directory listing from within Windows Explorer.
ms.date: 09/14/2020
author: Deland-Han 
ms.author: delhan
manager: dscontentpm
audience: itpro
ms.topic: troubleshooting
ms.prod: windows-client
localization_priority: medium
ms.reviewer: kaushika
ms.prod-support-area-path: 'Management and Configuration: General issues'
ms.technology: PrintFaxScan
---
# How to add the print directory feature to Windows Explorer

This article describes how to add the print directory feature, and how to enable printing of the directory listing from within Windows Explorer.

_Original product version:_ &nbsp; Windows 10 - all editions, Windows Vista  
_Original KB number:_ &nbsp; 272623

## Summary

For more information about How to add the Print Directory feature for folders in Windows XP, in Windows Vista, or in Windows 7, click the following article number to view the article in the Microsoft Knowledge Base: [321379](https://support.microsoft.com/help/321379) How to add the Print Directory feature for folders in Windows XP, in Windows Vista, or in Windows 7  

## More information

To have us add the Print Directory feature for you, go to the [Fix it for me](#fix-it-for-me) section. If you prefer to add the Print Directory feature yourself, go to the [Let me fix it myself](#let-me-fix-it-myself) section.

## Fix it for me

To fix this problem automatically, click the **Fix it** button or link. Click **Run** in the **File Download** dialog box, and follow the steps in the Fix it wizard.

> [!NOTE]
>
> - This wizard may be in English only. However, the automatic fix also works for other language versions of Windows.
> - If you are not using the computer that has the problem, save the Fix it solution to a flash drive or a CD and then run it on the computer that has the problem.
> Then, go to the D[id this fix the problem?](#did-this-fix-the-problem) section.

## Let me fix it myself

To add the print directory feature to Windows Explorer, follow these steps:

### Step 1: Create the Printdir.bat file

To do this, follow these steps:

1. Click **Start**, click **Run**, type notepad, and then click **OK**.
2. Paste the following text into Notepad:
    @echo off  
    dir %1 /-p /o:gn > "%temp%\Listing"  
    start /w notepad /p "%temp%\Listing"  
    del "%temp%\Listing"  
    exit

3. On the **File** menu, click **Exit**, and then click **Yes** to save the changes.
4. In the **Save As** dialog box, type the following text in the **File name** box, and then click **Save**: `%windir%\Printdir.bat`  

> [!NOTE]
> If you receive a dialog box that states that you do not have permission to save in this location, you can save the file to the desktop. Next, you click **Start**, click **Run**, type %windir% , and then click **OK**. Then, you can copy the file from the desktop to the location.

### Step 2: Edit the registry

> [!IMPORTANT]
> This section, method, or task contains steps that tell you how to modify the registry. However, serious problems might occur if you modify the registry incorrectly. Therefore, make sure that you follow these steps carefully. For added protection, back up the registry before you modify it. Then, you can restore the registry if a problem occurs. For more information about how to back up and restore the registry, click the following article number to view the article in the Microsoft Knowledge Base: [322756](https://support.microsoft.com/help/322756) How to back up and restore the registry in Windows  

1. Click **Start**, click **Run**, type **Notepad**, and then click **OK**.
2. Type the following commands in Notepad.

    ```console
    Windows Registry Editor Version 5.00

    [HKEY_CLASSES_ROOT\Directory\Shell]
    @="none"

    [HKEY_CLASSES_ROOT\Directory\Shell\Print_Directory_Listing]
    @="Print Directory Listing"

    [HKEY_CLASSES_ROOT\Directory\shell\Print_Directory_Listing\command]
    @="Printdir.bat \"%1\""

    [HKEY_CLASSES_ROOT\SOFTWARE\Classes\Directory]
    "BrowserFlags"=dword:00000008

    [HKEY_CLASSES_ROOT\SOFTWARE\Classes\Directory\shell\Print_Directory_Listing]
    @="Print Directory Listing"

    [HKEY_CLASSES_ROOT\SOFTWARE\Classes\Directory\shell\Print_Directory_Listing\command]
    @="Printdir.bat \"%1\""

    [HKEY_CURRENT_USER\Software\Microsoft\Windows\Shell\AttachmentExecute\{0002DF01-0000-0000-C000-000000000046}]
    @=""

    [HKEY_CLASSES_ROOT\SOFTWARE\Classes\Directory]
    "EditFlags"="000001d2"
    ```

    On the **File** menu, click **Save As**.
3. In the **Save in** list, click **Desktop**.
4. In the **File name** box, type PrintDirectoryListing.reg, click **All Files** in the **Save as type** list, and then click **Save**.
5. On the desktop, double-click the LoggingOn.reg file to add the registry keys to the Windows registry.
6. Click **OK** in the message box.

### Did this fix the problem?

- Check whether the problem is fixed. If the problem is fixed, you are finished with this section. If the problem is not fixed, you can [contact support](https://support.microsoft.com/contactus/).
- We would appreciate your feedback. To provide feedback or to report any issues with this solution, leave a comment on the [Fix it for me](https://support.microsoft.com/help/2970908) blog or send us an [email](mailto:fixit4me@microsoft.com?subject=kb).