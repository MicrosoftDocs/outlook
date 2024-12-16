---
title: "Deployment overview for the new Outlook for Windows"
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
description: "Provides an overview of deployment for new Outlook for Windows"
ms.date: 11/13/2024
---

# Deployment overview for the new Outlook for Windows

The new Outlook for Windows client installer is now available either from the Microsoft Store or the Office Content Delivery Network (CDN).

The new Outlook is currently offered as a preview upgrade to classic Outlook for Windows through a toggle. Users can opt in to download the installer and switch to the new experience and can choose to [migrate settings](https://support.microsoft.com/office/b85ce5ff-bef3-45ae-9e95-9d63c514abdc) and [install add-ins](install-web-add-ins.md) from classic Outlook. After users toggle in, they’ll see their supported accounts migrated from classic Outlook for Windows to the new Outlook.

> [!NOTE]
> Users need to sign back in to accounts that can’t automatically authenticate via [Windows Single Sign-On](/microsoft-365-apps/outlook/get-started/supported-account-types).

The toggle experience is the recommended way for users to get the new Outlook for Windows. It’s currently an end-user opt-in mechanism, although admins can control the availability of the toggle in classic Outlook for Windows. In the future, we’re making it easier for organizations to smoothly transition end-users to the new Outlook for Windows. Once switched, users can return to the classic Outlook for Windows.

The new Outlook for Windows is also available as the upgrade from the Windows Mail and Calendar apps through a toggle. Users who toggle in from Mail and Calendar also see their accounts listed for easy sign-in in the new app.

## Prerequisites for target computers

As a requirement, Outlook on the web needs to be enabled for users' mailboxes for whom you're planning to deploy new Outlook for Windows. For more information, see: [OWAEnabled parameter](/powershell/module/exchange/set-casmailbox#-owaenabled).

For the new Outlook client to be successfully installed, computers must meet the minimum requirements listed here.

### System and app requirements

> [!NOTE]
> New Outlook for Windows is not supported on Windows Server 2016 and Windows Server 2019.

Requirement | Version
------------|-------
Windows |- Windows 10 Version 1809 (Build 17763) or higher. The new Outlook for Windows is preinstalled on new Windows devices and devices running Windows 11 version 23H2. </br>- Windows Server 2022 (20348.2402) or higher.
Classic Outlook app | Version 2303 Build 16227.20318 or higher to see the Try the new Outlook toggle. **Important:** Classic Outlook is only a requirement if you want users to be able to switch between classic Outlook and new Outlook. This prerequisite is optional if you only want your users to see the new Outlook client.

## Other deployment options

### Download and install new Outlook for a single computer

For organizations that disable access to the Windows Store, the installer can be directly accessed from the Office CDN.

To install new Outlook on a single computer with many users, follow these steps:

1. Download the [Setup.exe](https://go.microsoft.com/fwlink/?linkid=2207851).
2. Launch PowerShell 7 as an administrator: Right-click the PowerShell icon and choose Run as Administrator.
3. Navigate to where the Setup.exe file is located.
4. Run the following command:

   ```powershell
   .\Setup.exe --provision true --quiet --start-
   ```

### Deploy new Outlook across your organization

To deploy this installer to a group of computers, or your entire organization:

1. Download the [.exe installer](https://go.microsoft.com/fwlink/?linkid=2207851).
2. Distribute the installer to your target computers using [Intune](/mem/intune/fundamentals/what-is-intune), [Microsoft Endpoint Configuration Manager](/mem/configmgr/core/understand/introduction), [Group Policy](/troubleshoot/windows-server/group-policy/use-group-policy-to-install-software), or non-Microsoft distribution software.
3. Run the installer on each computer.

## Non-Administrative Installation Methods

For users without administrative privileges, provided here are several alternatives to install the new Outlook for Windows: Windows Package Manager, Microsoft Intune, or Setup.exe Bootstrapper.

### Windows Package Manager (winget)

The Windows Package Manager (winget) allows for a nonadministrative, per-user installation of the new Outlook for Windows. To use winget, follow these steps:

1. Open PowerShell by pressing Windows + X and select Terminal (PowerShell for Windows 10 users).
2. Enter the following command to install the Microsoft Store version of new Outlook:

   ```powershell
   winget install -i -e --id=9NRX63209R7B --source=msstore --accept-package-agreements
   ```

### Microsoft Intune

Microsoft Intune allows administrators to deploy the Microsoft Store version of Outlook to enrolled devices. This approach doesn't require administrative rights on each device. For more information, see [Deploy apps your organization uses](/mem/intune/fundamentals/manage-apps#deploy-apps-your-organization-uses).

### Setup.exe Bootstrapper for per-user install

A Setup.exe bootstrapper can be used for a straightforward per-user installation:

1. Download the [.exe installer](https://go.microsoft.com/fwlink/?linkid=2207851).
2. Open PowerShell and run the following command:

   ```powershell
   .\Setup.exe --quiet --start-
   ```

## Install new Outlook with a new Microsoft 365 deployment

Starting with Version 2501 (to be updated in January 2025), new deployments of Microsoft 365 desktop client apps on Windows devices will include the new Outlook app by default. Admins might choose to exclude classic or new Outlook, or to have both installed side-by-side.  

The toggle to install both Outlooks is turned on by default to encourage organizations to [run classic and new Outlook side-by-side](https://support.microsoft.com/office/a624c36d-c50f-43bc-9c8b-dd17b5690ffb) for a gradual migration of users to new Outlook. However, admins can choose to install new Outlook or classic Outlook only by toggling the desired app off or on.

To exclude either Outlook, admins can use the [Office Customization Tool](https://config.office.com/deploymentsettings) (recommended) by selecting the toggle to include or exclude **Outlook (classic)** or **Outlook (new)**. Or, admins configure the XML directly. See[Configuration options for the Office Deployment Tool - ExcludeApp element](/microsoft-365-apps/deploy/office-deployment-tool-configuration-options#example-7).

If new Outlook was already installed, admins can always remove it by following the steps in [Control the installation and use of new Outlook](../get-started/control-install.md). Removing new Outlook in this way doesn't affect existing installations.

### Running new and classic Outlook side-by-side ###

There are benefits to running new Outlook and classic Outlook side-by-side such as:

- Depending on your organization policy, users can try new Outlook while still using classic Outlook as needed.
- Outlook behaves according to your organization's existing configuration settings. For example, if the Admin Controlled Migration to the new Outlook policy is enabled, the **Try the new Outlook** toggle appears in classic Outlook and the user experience follows all Admin Controlled Migration policy settings. Learn more about these policy settings in [Policy for Admin-controlled migration to new Outlook](../manage/admin-controlled-migration-policy.md).
- Both **Outlook (classic)** and **Outlook (new)** appear in the Start menu and are available for use based on an organization's policy settings.

**Known issues with new Outlook:**
To customers with configurations using known features such as full .pst support in Outlook and integrated email features such as **Mail merge** in Word, **People picker**, **@ Mentions**, **People cards** in Office apps and **Share To in Windows**, Microsoft recommends installing new Outlook and classic Outlook side-by-side. Until the features are fully available in new Outlook, running the apps side-by-side ensures features that still rely on classic Outlook libraries will continue to work seamlessly in other Office apps.

Learn more about .pst feature progress in new Outlook in: [Work offline in Outlook](https://support.microsoft.com/office/2460e4a8-16c7-47fc-b204-b1549275aac9).

### Download and install new Outlook using an offline installer

Admins can also use a local Outlook MSIX to provision new Outlook to minimize the amount of bandwidth used for the initial installation. For this option, download the MSIX packages for offline situations. Select the MSIX package for your needs:

- [X64 Windows](https://go.microsoft.com/fwlink/?linkid=2195164)
- [X86 Windows](https://go.microsoft.com/fwlink/?linkid=2195278)
- [Arm64 Windows](https://go.microsoft.com/fwlink/?linkid=2195438)

Package info:

- Package Identity/Name: Microsoft.OutlookForWindows
- Package Family Name: Microsoft.OutlookForWindows_8wekyb3d8bbwe

Admins can install the above packages using the appropriate package for their scenario:

- For one user on a machine: [Add-AppxPackage (Appx)](/powershell/module/appx/add-appxpackage?view=windowsserver2025-ps)
- For all users on a machine: [Add-AppxProvisionedPackage (DISM)](/powershell/module/dism/add-appxprovisionedpackage?view=windowsserver2022-ps)

### Control the release of new Outlook

To control the release of new Outlook in your organization, see [Control the installation and use of new Outlook](../get-started/control-install.md).
