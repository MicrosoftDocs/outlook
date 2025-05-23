---
title: Synchronization monitor in Microsoft Outlook
description: Describes the Synchronization monitor in Outlook and how it affects mail synchronization.
author: cloud-writer
ms.author: meerak
manager: dcscontentpm
audience: ITPro
ms.topic: troubleshooting
ms.custom: 
  - sap:Exchange Mailbox Accounts\.ost file synchronization
  - Outlook for Windows
  - CSSTroubleshoot
ms.reviewer: gbratton
appliesto: 
  - Outlook for Microsoft 365
  - Outlook 2021
  - Outlook 2019
  - Outlook 2016
search.appverid: MET150
ms.date: 03/25/2025
---

# Synchronization monitor in Microsoft Outlook

_Original KB number:_ &nbsp; 3197761

Microsoft Outlook includes a feature that is informally known as the synchronization monitor or sync monitor. The sync monitor is a continuous background check of local folders in the Outlook .ost file to verify that they are in sync with their related server folders. If the sync monitor's logic concludes that a folder isn't in sync, the program runs a series of repairs to resolve the problem. The [October 4, 2016, Update for Outlook 2016](https://support.microsoft.com/help/3118375) changes the detection and repair logic, and also add some diagnostic logging to the sync monitor feature.

> [!NOTE]
> By default, this updated detection and repair logic isn't enabled. To enable this new functionality, see the registry information that is provided in the More Information section.

The sync monitor runs a series of detection and repair actions based on the synchronization state health of every folder. For example, the sync monitor checks the unread items in the local copy of a folder, and then compares those items to the unread items in the server copy of the folder. If the number of items in each group don't match, a repair is necessary.

The repair process is a series of steps that try to restore the sync state of the folders. The steps are performed in order from least-intrusive to most-intrusive. If all other repairs fail, the sync monitor schedules a full resync of the folder.

Sometimes, the original problem detection logic that is used by the sync monitor is too aggressive. In this case, folders that are in a good sync state are incorrectly identified as broken. If the repair on these folders can't be successfully completed by using one of the nonintrusive steps, a full folder resync will eventually be scheduled. This can cause an unexpected resync of a folder. If the folder contents are large, this can also create unexpected network traffic and a poor user experience while you wait for the full resync of the folder to finish.

The October 4, 2016, updates for Outlook 2016 add the following important changes to the sync monitor logic:

- The algorithm for detecting folders that are out-of-sync is adjusted to be less aggressive.
- Diagnostic logging is added to help the Outlook product team understand future problems in this area.
- Registry value options are added to enable control of the repair process steps.

## Sync monitor repair process

The sync monitor repair process includes the following steps:

1. Run a simple sync of the folder.
2. Find and fix known problems that affect the local binary information that is used to track sync status.
3. Run an integrity check scan on the .ost file to repair integrity problems in the data file.
4. Clear the offline items.

> [!NOTE]
> This step causes a complete folder resync of all data from the server.

## Registry Information

> [!IMPORTANT]
> Follow the steps in this section carefully. Serious problems might occur if you modify the registry incorrectly. Before you modify it, [back up the registry for restoration](https://support.microsoft.com/help/322756) in case problems occur.

To enable the synchronization monitor feature, use one of the following registry subkeys.

`HKEY_CURRENT_USER\Software\Microsoft\Office\x.0\Outlook\Cached Mode`

Or

`HKEY_CURRENT_USER\Software\Policies\Microsoft\Office\x.0\Outlook\Cached Mode`

> [!NOTE]
>
> - _x.0_ in the registry key path represents the version of Outlook (16.0 = Outlook 2016, Outlook 2019, Outlook 2021, Outlook for Microsoft 365).
> - You might have to manually create the `Cached Mode` registry key if it doesn't already exist.

## Controlling the repair process

Use the following registry settings to control the repair process.

Value (DWORD): SyncMonitorLevel  
Data:

The data for this registry setting controls the repair process in a cumulative manner. To do this, it starts by using the better logic detection methods, and then it uses the repair options from least-intrusive to most-intrusive. The following chart describes the behavior that is associated with the repair option settings.

| Data| Behavior |
|---|---|
|0|No change or improvement. This is the same as not applying the update for sync monitor.|
|1|Use improved detection logic related to read/unread counts.|
|2|Use improved detection logic related to read/unread counts.<br/>Use improved detection logic for decisions about whether items have changed between local/server.|
|3|Use improved detection logic related to read/unread counts.<br/>Use improved detection logic to decide whether items have changed between local/server.<br/>Never clear offline items repair.<br/><br/>**NOTE** This setting enables the sync monitor to try to repair the sync problems by using steps 1, 2, and 3 in the sync monitor repair process.|
|4|Use improved detection logic related to read/unread counts.<br/>Use improved detection logic to decide whether items have changed between local/server.<br/>Never try the integrity check scan.<br/>Never clear offline items repair.<br/><br/> **NOTE** This setting enables the sync monitor to try to repair the sync problems by using steps 1 and 2 in the sync monitor repair process.|
|5|Use improved detection logic related to read/unread counts.<br/>Use improved detection logic to decide whether items have changed between local/server.<br/>Don't fix problems with the local binary information that is used to track sync state.<br/>Never try the integrity check scan.<br/>Never clear offline items repair.<br/><br/>**NOTE** This setting enables the sync monitor to try to repair the sync problems by using step 1 in the sync monitor repair process.|

Diagnostic logging

Value (DWORD): SyncMonitorLogging  
Data: 1

If diagnostic logging is enabled and the sync monitor engine decides that a folder is out-of-sync, it runs the repair options and adds a message to the **Sync Issues** folder that contains the diagnostic information. This information can be provided to a Microsoft Support professional if additional troubleshooting is required to understand a sync monitor problem. The subject of the diagnostic log message is **Sync Monitor**.

Recommended settings

The registry and diagnostic options that are added by the update are provided to help isolate and correct problems that affect the sync monitor. There's no one particular "right" setting to use to resolve all problems. Use the following guidelines for the new settings:

- If you suspect that you're experiencing folder resyncs although there's no problem, set the `SyncMonitorLevel` value to **2**. This turns on the better detection logic and provides the best first step to fix the problem.
- If you're experiencing full folder resyncs and the folders are so large that the network traffic or user experience is problematic, set the `SyncMonitorLevel` value to **3**. This should prevent Outlook from performing the full folder resync. If you use this option but your local folder is out-of-sync, the problem won't be repaired.
- If the folder resyncs are frequent enough to cause problems for more than one user, consider adding the diagnostic logging so that there's data to help Microsoft diagnose the problem and make future improvements to the sync monitor feature.
- If you decide to turn off some repair options such as the **clear offline items** choice, you should enable the diagnostic logging and check for problem folders occasionally. If a particular folder is problematic and you want to repair the folder manually, you can clear the folder manually. To do this, use the **Clear Offline Items** on the **General** tab of the folder properties. To access the folder properties, right-click the folder in the folder list, and then select **Properties**.
