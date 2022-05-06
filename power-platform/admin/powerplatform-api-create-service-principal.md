---
title: "Creating a service principal application using API (preview) | Microsoft Docs"
description: Power Platform API and service principal authentication
author: laneswenka
ms.reviewer: jimholtz
ms.component: pa-admin
ms.topic: reference
ms.date: 03/19/2021
ms.subservice: admin
ms.author: laswenka
search.audienceType: 
  - admin
search.app:
  - Powerplatform
---

# Creating a service principal application using API (preview) 

[!INCLUDE [cc-beta-prerelease-disclaimer](../includes/cc-beta-prerelease-disclaimer.md)]

Authenticating via username and password is often not ideal, especially with the rise of multifactor authentication.  In such cases, service principal (or client credentials flow) authentication is preferred.

## Registering an admin management application
First, the client application needs to be registered in your Azure Active Directory (Azure AD) tenant.  To set this up, review the [Authentication](programmability-authentication.md) article for Power Platform APIs.  

After your client application is registered in Azure AD, it also needs to be registered with Microsoft Power Platform.  Today, there's no way to do this via the Power Platform admin center; it must be done programmatically via Power Platform API or PowerShell for Power Platform administrators.  A service principal can't register itself—by design, the application must be registered by an administrator username and password context.  This ensures that the application is created knowingly by someone who is an administrator for the tenant.

To register a new management application, use the following Request with a bearer token obtained using username and password authentication:

```HTTP
Authorization: Bearer eyJ0eXAiOi...
Host: api.bap.microsoft.com
Accept: application/json
PUT https://api.bap.microsoft.com/providers/Microsoft.BusinessAppPlatform/adminApplications/{CLIENT_ID_FROM_AZURE_APP}?api-version=2020-10-01
```

## Make requests as the service principal 
Now that it has been registered with Microsoft Power Platform, you can authenticate as the service principal itself.  Use the following request to query for your management application list.  This can use a bearer token obtained using client credential authentication flow:

```HTTP
Authorization: Bearer eyJ0eXAiOi...
Host: api.bap.microsoft.com
Accept: application/json
GET https://api.bap.microsoft.com/providers/Microsoft.BusinessAppPlatform/adminApplications?api-version=2020-10-01
```

## Limitations of service principals
Currently, service principal authentication works for environment management, tenant settings, and Power Apps management.  APIs related to Flow are supported for service principal authentication in situations where a license is not required, as it is not possible to assign licenses to service principal identities in Azure Active Directory.
