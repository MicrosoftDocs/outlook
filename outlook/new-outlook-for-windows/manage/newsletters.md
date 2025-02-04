---
title: Newsletters in Outlook (Preview)
description: Describes how to configure and manage the Newsletters experience in Outlook
author: 
ms.author: 
manager: serdars
audience: ITPro
ms.topic: conceptual
ms.service: outlook
ms.collection:
- Tier3
- deploy-new-outlook
ms.localizationpriority: medium
ms.custom: intro-overview
recommendations: true
ms.date: 2/4/2025
---
# Newsletters in Outlook (Preview)

Newsletters in Outlook helps you create and send structured, professional newsletters quickly and easily from within Outlook. This feature allows you to build momentum and keep your team informed and engaged. While this feature is in Preview, admins can enable for some or all users in an organization, and others will not have access.

End user support documentation: [Newsletters](https://support.microsoft.com/en-us/topic/b35566e6-d319-450d-8930-86e483cda3ee?preview=true)

## Managing access
Access to Outlook Newsletters is managed using the OwaMailboxPolicy.OutlookNewslettersAccessLevel property. This property can be set using the `Set-OwaMailboxPolicy` cmdlet available in the Exchange Management Shell. There are four values for this property:

`ReadWrite` – user has full authoring permissions to create pages and newsletters in the Outlook Newsletters module.  
`ReadOnly` – user can read newsletters and browse pages in the Outlook Newsletters module. (Note: all users can read the email messages generated when publishing a newsletter to mail recipients, regardless of this permission level.)  
`NoAccess` – user cannot access the Outlook Newsletters module in the New Outlook for Windows or Outlook for the Web. They can still read any email messages sent or forwarded to them in Mail.  
`Undefined` – if the value is undefined in a policy (i.e., never explicitly set by your organization’s administrator), the M365 service will default to NoAccess while Outlook Newsletters is still in Preview, and ReadWrite once it has reached Global Availability.  

## Managing features
### Reactions and comments
Outlook Newsletters has several features to allow readers to engage with published newsletters. It introduces the ability for readers to react to each section of a newsletter in addition to reacting to the entire newsletter as with a typical Outlook email. Readers also have to ability to comment on the newsletter via integrated comment controls at the end of a newsletter. These engagement features can be toggled off by authors for their individual newsletters when publishing them, or the administrator can disable these features using the `OwaMailboxPolicy.OutlookNewslettersReactions` property.

### Recommended newsletters
Newsletter editions published with Outlook Newsletters include recommendations to other content published with Outlook Newsletters to encourage greater readership in your organization. Such recommendations are included in the footer of published newsletter editions. Authors can disable these recommendations for each individual newsletter edition they publish, or the administrator can disable these recommendations for a set of users or your entire organization using the `OwaMailboxPolicy.OutlookNewslettersShowMore` property. 

## Other tasks
### Audit logging
As an administrator, you can leverage the audit-logging tools from Microsoft Purview to monitor and audit Newsletters activities in your tenant. The logging tools allow you to filter, search, export, and analyze the log data for various newsletter events.
To access the logging tools, follow these steps:
- Select “Audit” from the Purview tools.
- For Workload, select SharePoint, and add any relevant user, date, or other filters to the search.
- Wait for the search to complete.  This will take a few minutes depending on the volume of logs being pulled and will run in the background.
- When the logs are available, you will see them in a table.  The results can also be exported into a CSV file using the Export button.
- Records that occurred in Newsletters will have a field within the AppAccessContext labelled “ClientAppName”.  The value of this field will be “OutlookNewsletters”.
- If a logging event refers to a SiteCollection, this object type corresponds to a Newsletters page.  Logs referring to a folder correspond to a newsletter in Newsletters.  Events related to specific files correspond to specific sections of a newsletter or images within the newsletter.

### Legal hold and discovery
An administrator with _SharePoint Embedded Administrator_ role and _Compliance data administrator_ role navigate to Microsoft Purview to perform an eDiscovery search.  The admin can perform a search for Outlook Newsletters conent in two ways depending on the location of the Newsletters content they wish to find:
-	Newsletters that have been sent will appear the same as any other email in the inbox of the recipients of the Newsletter. A sent Newsletter is functionally no different from any other email, so the administrator can use the Purview tools to search for these Newsletters in the same way they would any other email.
-	Newsletters that have not been sent yet and are still in Draft format, or comments left on Newsletters can be found in SharePoint Embedded.  These can be found by selecting **Sites** for the data source.
