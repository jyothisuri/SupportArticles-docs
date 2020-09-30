---
title: 0xc004f063 when activating an OEM version
description: Provides a solution to an 0xc004f063 error that occurs when you try to validate an OEM version.
ms.date: 09/16/2020
author: Deland-Han 
ms.author: delhan
manager: dscontentpm
audience: itpro
ms.topic: troubleshooting
ms.prod: windows-server
localization_priority: medium
ms.reviewer: kaushika
ms.prod-support-area-path: Activation
ms.technology: Deployment
---
# Error code: 0xc004f063 is displayed when trying to activate or validate an OEM version of Windows 8 or Windows Server 2012

This article provides a solution to an 0xc004f063 error that occurs when you try to validate an OEM version.

_Original product version:_ &nbsp; Windows 8, Windows Server 2012 R2  
_Original KB number:_ &nbsp; 2817024

## Symptoms

When you try to validate an OEM version of Windows 8 or Windows Server 2012, you may receive the following error message:

> Error code : 0xc004f063 The Software Licensing Service reported that the computer BIOS is missing a required license.

Additionally, you may also notice the following events getting logged in the Application event log:

## Cause

This error usually occurs if a hardware is changed or any hardware device malfunctions and Windows is unable to verify the license again. Windows is unable to read the SLIC table in the BIOS that is required to be able to self-activate the OEM_SLP Key that is currently in use. This happens due to one of the following reasons:

1. Service Tag or the Service Number is not updated by the OEM vendor after motherboard replacement.
2. BIOS contains a default or a garbage value for Service Tag.
3. BIOS has incorrect product information

## Resolution

Contact the OEM vendor to update the BIOS that has the updated Serial Number or Service Tag.

## More information

This issue mostly occurs on OEM_SLP machines wherein Windows is bound with the Service Tag of the machine. If an OEM_SLP Windows is validating its license after any hardware change apart from the key, it will also verify the Service Tag number in the BIOS.

Note: To check the Service Tag number on a machine, run the command: *wmic bios get serialnumber*  

Upgrading the BIOS is an effort to put the correct SLIC table on the machine. Software Licensing Description Table (SLIC) is a digital signature placed inside the BIOS by the system manufacturer. The OEM-SLP Key, and an XML formatted OEM certificate (issued by Microsoft to each OEM) will be verified against this OEM-specific SLIC and auto activate if everything is in order.