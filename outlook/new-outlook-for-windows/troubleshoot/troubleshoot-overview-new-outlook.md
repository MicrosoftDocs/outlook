---
title: "New Outlook for Windows troubleshooting overview"
ms.author: janellem
author: JanelleMcIntosh-MSFT
manager: triciag
audience: ITPro
ms.topic: overview
ms.service: outlook
ms.collection:
- Tier3
- deploy-new-outlook
ms.localizationpriority: medium
ms.custom: intro-overview
recommendations: true
description: "Overview of troubleshooting issues with new Outlook for Windows"
ms.date: 11/22/2024
---

# Changes to troubleshooting steps in new Outlook

Some of the common steps users took to troubleshoot issues in classic Outlook are no longer needed in new Outlook. The architecture changes to new Outlook make actions such as creating a new profile or starting Outlook in safe mode unnecessary.

## Changes to profile experience

Creating a new profile in classic Outlook was a common troubleshooting step to help resolve various issues such as startup problems, synchronization errors, or slow performance. The underlying architecture change in New Outlook means users only need one Outlook profile, and eliminates the need for the profile picker. By removing the ability to create multiple profiles, new Outlook provides a more seamless and less frustrating experience when dealing with email-related issues in Outlook.

The change to the profile experience is part of a broader effort by Microsoft to streamline the user experience and improve the stability and reliability of Outlook. The architecture in new Outlook integrates more robust error-handling mechanisms, offers improved support for modern email protocols, reduces the complexity of maintaining and configuring the application, and eliminates the need to create new profiles.

## Removal of safe mode

Starting new Outlook for Windows in safe mode is no longer relevant when troubleshooting new Outlook. A frequent troubleshooting approach in classic Outlook was to use the startup switch Outlook.exe /safe. Starting in safe mode was done to prevent COM Add-ins from loading at launch since add-ins were known to trigger problems such as crashes and hangs.

The new sandbox architecture in new Outlook for Windows is using web add-ins instead of COM Add-ins means there's no need for a /safe switch. The extensibility architecture is designed to protect new Outlook from crashing if an add-in misbehaves.