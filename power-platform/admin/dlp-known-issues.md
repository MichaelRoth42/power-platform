---
title: "Known limitations for data loss prevention (DLP) policies | MicrosoftDocs"
description:  DLP policies known limitations.
ms.topic: conceptual
ms.date: 05/06/2022
ms.subservice: admin
author: mikferland-msft
ms.author: miferlan
ms.reviewer: jimholtz
contributors:
  - mikferland-msft
  - mihaelablendea
  - ChrisGarty
ms.custom: "admin-security"
search.audienceType: 
  - admin
search.app:
  - D365CE
  - PowerApps
  - Powerplatform
  - Flow
---

# Known limitations
Below are known limitations to know about when leveraging our suite of data loss prevention (DLP) capabilities:

## General
- There's limited support for DLP actions in the [Power Platform for Admins connector](/connectors/powerplatformforadmins/). The ability to block a connector is only supported in the DLP actions labeled with "V2" (such as "Create DLP Policy V2"). Connector action control, connector endpoint filtering, and DLP for custom connectors can't be configured using the Power Platform for Admins connector.
- Tabular functions in the [Power Apps expression language](/powerapps/maker/canvas-apps/formula-reference) can't be governed with DLP.

## Child flows
- Blocking the [HTTP with Azure AD](/connectors/webcontents/) connector will also block child flows because those child flows are called using the same HTTP connector technology.
- If a child flow violates a DLP policy, it will not result in the parent flow becoming non-compliant.

### Desktop flows
- There's no support for cross checking the categories between a cloud flow and the desktop flows it calls. This will be supported when [DLP for desktop flows](/power-automate/prevent-data-loss#data-loss-prevention-dlp-for-desktop-flows-preview) is generally available.
- There's no support for cross checking the modules that are used between a desktop flow and all its child desktop flows. This will be supported when [DLP for desktop flows](/power-automate/prevent-data-loss#data-loss-prevention-dlp-for-desktop-flows-preview) is generally available.
- There's no support for the "Set default group" for newly added desktop flow modules. This will be supported when [DLP for desktop flows](/power-automate/prevent-data-loss#data-loss-prevention-dlp-for-desktop-flows-preview) is generally available.


[!INCLUDE[footer-include](../includes/footer-banner.md)]

### See also
[DLP for desktop flows](/power-automate/prevent-data-loss#data-loss-prevention-dlp-for-desktop-flows-preview)
