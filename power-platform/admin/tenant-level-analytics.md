---
title: "Tenant-level analytics (default)" 
description: View tenant-level analytics in a variety of reports
ms.component: pa-admin
ms.topic: conceptual
ms.date: 03/30/2022
author: tjvass
ms.subservice: admin
ms.author: tjvass
ms.reviewer: jimholtz
search.audienceType: 
  - admin
search.app:
  - D365CE
  - PowerApps
  - Powerplatform
  - Flow
---

# Tenant-level analytics (default)

[!INCLUDE [cc-beta-prerelease-disclaimer](../includes/cc-beta-prerelease-disclaimer.md)]

Tenant admins can view reports that apply to all environments in a tenant. 

> [!IMPORTANT]
> - This is a preview feature.
> - Preview features aren’t meant for production use and may have restricted functionality. These features are available before an official release so that customers can get early access and provide feedback.
> - This feature is being gradually rolled out across regions and might not be available yet in your region.

To access these reports, sign in to the Power Platform admin center and select **Analytics** > **Power Apps**. In the upper-right corner, select **Tenant level analytics** from the dropdown list. 

:::image type="content" source="media/select-tenant-level-analytics.png" alt-text="Select tenant level analytics.":::

## Who can view these reports?

Admins with the following roles can view the reports in Power Apps analytics:
- Tenant-level administrator - has access to all environments
- Environment-level admin - environment list is filtered to include only environments where the admin has Contributor or Environment Admin role

For more information on the different roles for managing your tenant across the platform, see [Use service admin roles to manage your tenant](use-service-admin-role-manage-tenant.md).

## How do I enable tenant-level analytics?

Follow these steps to enable the tenant-level analytics preview feature. 

The following admin roles are required:

- Global administrator
- Service administrator
- Delegated admin 

Environment admins are not able to do these steps. The admin doesn't need to be a licensed user. 

1. Select the **Gear** icon (![Gear icon.](media/selection-rule-gear-button.png)) in the upper-right corner of the Microsoft Power Platform site, and then select **Power Platform settings**. 

2. Turn on the option to **Enable tenant level analytics**.

   :::image type="content" source="media/enable-tenant-level-analytics.png" alt-text="Enable tenant-level analytics.":::

3. **Granting consent for tenant-level analytics:** The process of collecting information for tenant-level analytics includes copying service telemetry data from other GEO locations into a central location for reporting.  Customers must explicitly enable this Power Platform operation.  For more information, see [Application and service principal objects in Azure Active Directory](/azure/active-directory/develop/app-objects-and-service-principals).

   Select **Enable** to grant consent for the service to collocate service telemetry data in the location associated with the default environment. 

   :::image type="content" source="media/enable-collocate-service-telemetry-data.png" alt-text="Grant consent for the service to collocate service telemetry data.":::

4. Select **Save** and then close the form. 

5. Select **Environment level analytics**, and then select **Tenant level analytics** to switch viewing modes. 

## How do I disable tenant-level analytics?

Follow these steps to disable the tenant-level analytics preview feature. 

The following admin roles are required:

- Global administrator
- Service administrator
- Delegated admin 

Environment admins are not able to do these steps. The admin doesn't need to be a licensed user. 

> [!IMPORTANT]
> When you disable the tenant-level analytics preview feature, note the following:
> - All the tenant-level aggregation of data from different environments (aggregating metrics, user object IDs, and resource names like app and flow names) will be permanently deleted. 
> - Tenant-level analytics reports will be disabled. 

1. Select the **Gear** icon (![Gear icon.](media/selection-rule-gear-button.png)) in the upper-right corner of the Microsoft Power Platform site, and then select **Power Platform settings**. 

2. Turn off the option to **Enable tenant level analytics**.

   :::image type="content" source="media/enable-tenant-level-analytics.png" alt-text="Enable tenant-level analytics.":::

## Where is this feature available?

The Power Platform admin center tenant-level views are available in all supported regions in the public cloud. This feature is not yet available in other sovereign clouds. 

### See also
[Admin Analytics for Power Apps](analytics-powerapps.md) <br />
[Preview: Tenant-level analytics](tenant-level-analytics.md) 



[!INCLUDE[footer-include](../includes/footer-banner.md)]
