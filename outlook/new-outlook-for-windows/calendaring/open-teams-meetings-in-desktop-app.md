---
title: Configure Teams meeting links to open in Teams desktop app
description: How to configure Teams meeting links in Outlook to open in the Teams desktop app.
manager: dcscontentpm
author: Cloud-Writer
ms.author: meerak
audience: ITPro
ms.topic: troubleshooting
ms.custom: 
  - sap:Calendar\Working with meetings or appointments
  - Outlook for Windows
  - CSSTroubleshoot
  - CI 169526
ms.reviewer: tasitae, gbratton, meerak, meshel, tylewis, v-trisshores
appliesto: 
  - Outlook for Microsoft 365
  - Outlook LTSC 2021
  - Outlook 2019
  - Outlook 2016
search.appverid: MET150
ms.date: 03/27/2025
---

# Configure Teams meeting links to open in Teams desktop app

When you select a Microsoft Teams meeting link in Microsoft Outlook to join a meeting, Outlook opens a page in your browser that provides multiple options to join the meeting. If you have the Teams desktop app installed on your computer, and you want to use the app to join all Teams meetings, you can set your meeting preference so that Outlook opens the meeting directly in the Teams app instead of asking for your preference each time.

## Set your Teams meeting preference in the browser

1. Select the **Join Online** button in the Microsoft Outlook meeting reminder or select **Click here to join the meeting** in your email invitation.

2. On the start page for Teams that opens in your browser, select **Always allow teams.microsoft.com to open links of this type in the associated app**, and then select **Open**.

The browser stores your preference and opens the meeting in your Teams desktop app. For all future Teams meetings, Outlook sends your meeting join request to the Teams desktop app when you select the meeting link.

## Set your Teams meeting preference in the Windows registry

Use this method if you can't set your Teams meeting preference in the browser, or if you want to set the preference on behalf of your users.

[!INCLUDE [Important registry alert](../../includes/registry-important-alert.md)]

1. Create a text file named *teams-desktop.reg*.

2. Copy and paste the following text into the file:

   ```notepad
   Windows Registry Editor Version 5.00

   [HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\Teams]

   "currentTeamsDeepLinkUrlProtocolVersion"="1.0.0.0"

   "minStableTeamsDeepLinkUrlProtocolVersion"="1.0.0.0"
   ```

3. Save the *teams-desktop.reg* file.

4. Double-click *teams-desktop.reg*.

5. When prompted for your approval, select **Yes**.

To set the meeting preference for a specific user, replace the second line in *teams-desktop.reg* with the `[HKEY_USERS\<user SSID>\SOFTWARE\Microsoft\Office\Teams]` registry subkey.

The Windows registry stores your preference. For all future Teams meetings, Outlook sends your meeting join request to the Teams desktop app when you select the meeting link.
