---  
title: "Data loss prevention in new Outlook for Windows"   
ms.author: janellem  
author: JanelleMcIntosh-MSFT
manager: triciag
audience: ITPro
ms.topic: overview
ms.service: outlook  
ms.collection: Tier3
ms.localizationpriority: medium 
ms.custom: QuickDraft  
ms.reviewer: janellem  
search.appverid: MET150 
recommendations: true
description: "Learn how to use data loss prevention policy tips in New Outlook for Windows to help manage sensitive information and compliance."
ai-usage: ai-assisted  
ms.date: 1/10/2025 
---  

# Data loss prevention policy tip reference for new Outlook for Windows

New Outlook now supports data loss prevention (DLP) policy tips with commonly used predicates and exceptions, advanced classifiers, and override capabilities.

## Licensing requirements

> [!NOTE]
> Features are enabled based on Licenses and connected experience settings. Review license requirements in [Licensing](/purview/dlp-ol365-win32-policy-tips#licensing).

|License  |These conditions apply  |
|---------|---------|
|E3 and equivalent licenses    |- Content contains Microsoft built-in or custom sensitive information types</br>- Content is shared from Microsoft 365     |
|E5 and equivalent licenses     |- Content contains built-in or custom sensitive information types</br>- Content is shared</br>- Content contains sensitivity labels (works for email and Office and PDF file types)</br>- Sender is</br>- Sender is member of (Only Distribution lists, Azure-based Dynamic Distribution groups, and email-enabled Security groups are supported)</br>- Sender domain is</br>- Recipient is</br>- Recipient is a member of (Only Distribution lists, Azure-based Dynamic Distribution groups, and email-enabled Security groups are supported)</br>- Recipient domain is</br>- Subject contains words     |

> [!NOTE]
> Conditions related to attachments such as Office files, PDF files, messages (.msg), and emails (.eml) are currently not supported. See the [new Outlook roadmap](https://aka.ms/newOutlookforWindows) for details on future updates.

## Actions that support policy tips

Refer to the [Exchange actions support policy tips](/purview/dlp-ol365-win32-policy-tips#actions-that-support-policy-tips) for details on actions that support policy tips.

> [!NOTE]
> Offline evaluation for data loss prevention isn't available for new Outlook.

## Sensitive information types that support policy tips

Refer to the [Sensitive information types](/purview/dlp-ol365-win32-policy-tips#sensitive-information-types-that-support-policy-tips-for-outlook-perpetual-users) for details on sensitive information types that support policy tips for Outlook perpetual users and Microsoft 365 users.

## Oversharing dialog for Outlook for Windows

The oversharing dialog is available in DLP for new Outlook for E5 users. When enabled in a DLP rule, this feature displays popups for warning, override, or block actions to end users who are sharing labeled or sensitive emails in Outlook desktop.

## Wait on send dialog support for oversharing

> [!NOTE]
> Currently, new Outlook only supports default oversharing dialog and not customized over sharing dialog. Learn more about [Customized oversharing dialog](/purview/dlp-ol365-win32-policy-tips#customized-oversharing-dialog)

After you configure the oversharing dialog, you can optionally enable the **Wait on send** dialog feature.

> [!NOTE]
> Wait on send is currently not available in new Outlook. See the [new Outlook roadmap](https://aka.ms/newOutlookforWindows) for details on future updates.
