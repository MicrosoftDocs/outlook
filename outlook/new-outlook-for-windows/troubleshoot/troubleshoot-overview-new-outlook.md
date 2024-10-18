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
ms.date: 10/17/2024
---

# Overview

Creating a new profile in classic Outlook was a common troubleshooting step to help resolve various issues such as startup problems, synchronization errors, or slow performance. The underlying architecture change in New Outlook means users only need one Outlook profile, and eliminates the need for the profile picker. By removing the ability to create multiple profiles, new Outlook provides a more seamless and less frustrating experience when dealing with email-related issues in Outlook.

The change to the profile experience is part of a broader effort by Microsoft to streamline the user experience and improve the stability and reliability of Outlook. The architecture in new Outlook integrates more robust error-handling mechanisms, offers improved support for modern email protocols, reduces the complexity of maintaining and configuring the application, and eliminates the need to create new profiles.

**In this article**

## System requirements

## Setup issues

## Troubleshoot boot issues

As a modern client, new Outlook includes enhanced built-in supportability and improvements to managing the app. For example, if you or your users have issues when starting new Outlook for Windows, the troubleshooting workflow can assist you in a boot issue scenario.

If the client fails to reach this stage [WHAT STAGE?] after three unsuccessful attempts, regardless of the reason, we'll reset everything, and you'll need to go through the initial setup process to add your accounts again. [WE NEED TO DESCRIBE WHAT THIS IS AND HOW TO DO IT--OR POINT TO CONTENT THAT EXPLAINS THE STEPS.]

Is there a way to force new Outlook for Windows to do this manually? [DO WHAT MANUALLY? START FROM THE BOOT?]

## Sandboxed architecture eliminates need to start in safe mode

Starting new Outlook in safe mode is no longer relevant when troubleshooting new Outlook.  

A frequent troubleshooting approach in classic Outlook was to use the startup switch Outlook.exe /safe. Starting in safe mode was done to prevent COM Add-ins from loading at launch since add-ins were known to trigger problems such as crashes and hangs.

The new sandbox architecture in new Outlook and using web add-ins instead of COM Add-ins means there's no need for a /safe switch. The extensibility architecture is designed to protect new Outlook from crashing if an add-in misbehaves.

For details about add-ins see:

[Use add-ins in Outlook](https://support.microsoft.com/office/use-add-ins-in-outlook-1ee261f9-49bf-4ba6-b3e2-2ba7bcab64c8)
[Office Add-ins platform overview](/office/dev/add-ins/overview/office-add-ins)
[Identify COM add-ins in your organization](../get-started/state-of-com-add-ins.md)
[Migrate from COM add-ins to web add-ins](../get-started/migrate-com-to-web-addins.md)

## Account issues in new Outlook

### Error states

### Reset new Outlook by removing all accounts

Run a command line to reset new Outlook, including all profile information, to return to the initial first-run state.

From Start, run and type:

## Update new Outlook

New Outlook for Windows checks for updates every time it starts, and they're applied automatically.  For more details, check out [Manage updates in new Outlook for Windows](../manage/manage-updates-new-outlook-windows.md). 

There are two primary components to new Outlook: a lightweight Windows integration component and a web interface. 

In theory, one could just refresh the web interface, but since the two components are connected and dependent on each other, restarting new Outlook is the best solution. 

- When new Outlook for Windows starts for the first time, it downloads the latest bits available and then launches. 
- After a few minutes new Outlook checks whether or not an update is available, but as this is the first time – there's nothing new available for us. [THIS IS UNCLEAR] 
- At the next start of new Outlook, we check again if an update is available, and if it is, the update is downloaded in the background. 
- The next time new Outlook starts, the downloaded update installs automatically. 

When troubleshooting, we recommended launching new Outlook and then waiting 5 minutes to make sure all updates are downloaded. [IS THERE ANYTHING THAT TELLS THE USER WHEN A DOWNLOAD IS COMPLETE?] Close and restart new Outlook to ensure the most recent updates are installed.

### New Outlook isn't open in a week

If a user doesn't open new Outlook in a week, they might not have the most recent updates because the downloaded update occurred when new Outlook was last running. A new update might be available and won't be downloaded until new Outlook starts again.

### New Outlook isn't opened in three weeks

If new Outlook wasn't open in three or more weeks, a new download begins. The means the splash screen might show longer before the app completely opens.

### Manually apply an update to new Outlook

You can manually apply updates to new Outlook from the command line. 

1. Select Start and then Run...
1. Type `- olk.exe force-update`.

## Performance

## Troubleshoot web add-ins

