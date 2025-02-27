---
# required metadata

title: Add Microsoft Edge to macOS devices using Microsoft Intune
titleSuffix:
description: Learn about adding Microsoft Edge to macOS devices using Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 10/09/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: kellieei
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection: M365-identity-device-management
---

# Add Microsoft Edge to macOS devices using Microsoft Intune

Before you can deploy, configure, monitor, or protect apps, you must add them to Intune. One of the available [app types](~/apps/apps-add.md#app-types-in-microsoft-intune) is Microsoft Edge *version 77 and later*. By selecting this app type in Intune, you can assign and install Microsoft Edge *version 77 and later* to devices you manage that run macOS. This app type makes it easy for you to assign Microsoft Edge to macOS devices without requiring you to use the macOS app wrapping tool. To help keep the apps more secure and up to date, the app comes with Microsoft AutoUpdate (MAU).

> [!IMPORTANT]
> This app type is in **public preview** and offers developer and beta channels for macOS. The deployment is in English (EN) only, however end users can change the display language in the browser under **Settings** > **Languages**. 

> [!NOTE]
> Microsoft Edge *version 77 and later* is available for Windows 10 as well.

## Prerequisites
- The macOS device must be running macOS 10.12 or later before installing Microsoft Edge.

## Add Microsoft Edge to Intune
You can add Microsoft Edge version 77 and later to Intune using the following steps:

1. Sign in to [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
2. In the **Intune** pane, select **Client apps** > **Apps** > **Add**.
3. In the **App type** list under the **Microsoft Edge, version 77 and later**, select **macOS**.

## Configure app information
In this step, you provide information about this app deployment. This information helps you identify the app in Intune, and it helps users find the app in the company portal.

1. Click **App information** to display the **App information** blade.
2. In the **App information** blade, you provide information about this app deployment. This information helps you identify the app in Intune, and it helps users find the app in the company portal.
    - **Name**: Enter the name of the app as it will be displayed in the company portal. Make sure that all names are unique. If the same app name exists twice, only one of the apps is displayed to users in the company portal.
    - **Description**: Enter a description for the app. For example, you could list the targeted users in the description.
    - **Publisher**: Microsoft appears as the publisher.
    - **Category**: Optionally, select one or more of the built-in app categories or a category that you created. This setting makes it easier for users to find the app when they browse the company portal.
    - **Display this as a featured app in the Company Portal**: Select this option to display the app prominently on the main page of the company portal when users browse for apps.
    - **Information URL**: Optionally, enter the URL of a website that contains information about this app. The URL is displayed to users in the company portal.
    - **Privacy URL**: Optionally, enter the URL of a website that contains privacy information for this app. The URL is displayed to users in the company portal.
    - **Developer**: Microsoft appears as the developer.
    - **Owner**: Microsoft appears as the owner.
    - **Notes**: Optionally, enter any notes that you want to associate with this app.
3. Select **OK**.

## Configure Microsoft Edge settings
In this step, configure installation options for the app.

1. In the **Add App** blade, select **App settings**.
2. In the **App settings** blade, the **Beta** Channel is automatically selected and cannot be changed.
    - The **Beta** Channel is the most stable Microsoft Edge preview experience and the best choice for a full pilot within your organization. With major updates every six weeks.

    > [!NOTE]
    > The Microsoft Edge browser logo is displayed with the app when users browse the company portal.
3.	Select **OK**.

## Select scope tags (optional)
You can use scope tags to determine who can see client app information in Intune. For full details about scope tags, see Use role-based access control and scope tags for distributed IT.
1.	Select **Scope (Tags)** > **Add**.
2.	Use the **Select** box to search for scope tags.
3.	Select the check box next to the scope tags you want to assign to this app.
4.	Click **Select** > **OK**.

## Add the app
When you've completed configuring, select **Add** from the **App app** blade. 

The app you've created is displayed in the apps list, where you can assign it to the groups that you select. 

> [!NOTE]
> Currently, Apple does not provide a way for Intune to uninstall Microsoft Edge on macOS devices.

## Next steps
- To learn how to configure Microsoft Edge on macOS devices, see [Configure Microsoft Edge on macOS devices](https://docs.microsoft.com/deployedge/configure-microsoft-edge#configure-microsoft-edge-on-mac).
- To learn about including and excluding app assignments from groups of users, see [Include and exclude app assignments](~/apps/apps-inc-exl-assignments.md).
- [Assign apps to groups](~/apps/apps-deploy.md)

