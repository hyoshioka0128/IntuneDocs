---
# required metadata

title: Integrate Jamf Pro with Microsoft Intune for compliance
titleSuffix: Microsoft Intune
description: Use Microsoft Intune compliance policies with Azure Active Directory Conditional Access to help integrate and secure Jamf-managed devices.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/20/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: 4b6dcbcc-4661-4463-9a36-698d673502c6

# optional metadata

#ROBOTS: 
#audience:
#ms.devlang:
ms.reviewer: elocholi
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Integrate Jamf Pro with Intune for compliance

Applies to: Intune in the Azure portal

When your organization uses [Jamf Pro](https://www.jamf.com) to manage macOS devices, you can use Microsoft Intune compliance policies with Azure Active Directory (Azure AD) Conditional Access to ensure that devices in your organization are compliant before they can access company resources. This article will help you configure Jamf integration with Intune.

When Jamf Pro integrates with Intune, you can sync the inventory data from macOS devices with Intune, through Azure AD. Intune's compliance engine then analyzes the inventory data to generate a report. Intune's analysis is combined with intelligence about the device user’s Azure AD identity to drive enforcement through Conditional Access. Devices that are compliant with the Conditional Access policies can gain access to protected company resources.

After you configure integration, you'll then [configure Jamf and Intune to enforce compliance with Conditional Access](conditional-access-assign-jamf.md) on devices managed by Jamf.  


## Prerequisites

### Products and services
You need the following to configure Conditional Access with Jamf Pro:

- Jamf Pro 10.1.0 or later
- [Company Portal app for macOS](https://aka.ms/macoscompanyportal)
- macOS devices with OS X 10.11 Yosemite or later

### Network ports
<!-- source: https://support.microsoft.com/en-us/help/4519171/troubleshoot-problems-when-integrating-jamf-with-microsoft-intune -->
The following ports should be accessible for Jamf and Intune to integrate correctly: 
- **Intune**: Port 443
- **Apple**: Ports 2195, 2196, and 5223 (push notifications to Intune)
- **Jamf**: Ports 80 and 5223

To allow APNS to function correctly on the network, you must also enable outgoing connections to, and redirects from:
- the Apple 17.0.0.0/8 block over TCP ports 5223 and 443 from all client networks.   
- ports 2195 and 2196 from Jamf Pro servers.  

For more information about these ports, see the following articles:  
- [Intune network configuration requirements and bandwidth](../fundamentals/network-bandwidth-use.md).
- [Network Ports Used by Jamf Pro](https://www.jamf.com/jamf-nation/articles/34/network-ports-used-by-jamf-pro) on jamf.com.
- [TCP and UDP ports used by Apple software products](https://support.apple.com/HT202944) on support.apple.com


## Connect Intune to Jamf Pro

To connect Intune with Jamf Pro:

1. Create a new application in Azure.
2. Enable Intune to integrate with Jamf Pro.
3. Configure Conditional Access in Jamf Pro.

## Create an application in Azure Active Directory

1. In the [Azure portal](https://portal.azure.com), go to **Azure Active Directory** > **App Registrations**, and then select **New registration**. 

2. On the **Register an application** page, specify the following details:
   - In the **Name** section, enter a meaningful application name, for example **Jamf Conditional Access**.
   - For the **Supported account types** section, select **Accounts in any organizational directory**. 
   - For **Redirect URI**, leave the default of Web, and then specify the URL for your Jamf Pro instance.  

3. Select **Register** to create the application and to open the **Overview** page for the new app.  

4. On the app **Overview** page, copy the **Application (client) ID** value and record it for later use. You'll need this value in later procedures.  

5. Select **Certificates & secrets** under **Manage**. Select the **New client secret** button. Enter a value in **Description**, select any option for **Expires** and choose **Add**.

   > [!IMPORTANT]  
   > Before you leave this page, copy the value for the client secret and record it for later use. You will need this value in later procedures. This value isn’t available again, without recreating the app registration.  

6. Select **API permissions** under **Manage**. Select the existing permissions and then select **Remove permission** to delete those permissions. Removal of all existing permissions is necessary as you’ll add a new permission, and the application only works if it has the single required permission.  

7. To assign a new permission, select **Add a permission**. On the **Request API permissions** page, select **Intune**, and then select **Application permissions**. Select only the check box for **update_device_attributes**.  

   Select **Add permission** to save this configuration.  

8. On the **API permissions** page, select **Grant admin consent for *\<your tenant>***, and then select **Yes**.  After the app is registered successfully, the API permissions should appear as follows:
   ![Successful permissions](./media/conditional-access-integrate-jamf/sucessfull-app-registration.png)

   The app registration process in Azure AD is complete.


    > [!NOTE]
    > If the client secret expires, you must create a new client secret in Azure and then update the Conditional Access data in Jamf Pro. Azure allows you to have both the old secret and new key active to prevent service disruptions.

## Enable Intune to integrate with Jamf Pro

1. Sign in to [Intune](https://go.microsoft.com/fwlink/?linkid=2090973), and go to **Microsoft Intune** > **Device Compliance** > **Partner device management**.

2. Enable the Compliance Connector for Jamf by pasting the Application ID you saved during the previous procedure into the **Jamf Azure Active Directory App ID** field.

3. Select **Save**.

## Configure Microsoft Intune Integration in Jamf Pro

1. In Jamf Pro, navigate to **Global Management** > **Conditional Access**. Click the **Edit** button on the **macOS Intune Integration** tab.

2. Select the check box for **Enable Intune Integration for macOS**.

3. Provide the required information about your Azure tenant, including **Location**, **Domain name**, the **Application ID**, and the value for the *client secret* that you saved when you created the app in Azure AD.  

4. Select **Save**. Jamf Pro tests your settings and verifies your success.

## Set up compliance policies and register devices

After you configure integration between Intune and Jamf, you need to [apply compliance policies to Jamf-managed devices](conditional-access-assign-jamf.md).


## Disconnect Jamf Pro and Intune 

If you no longer use Jamf Pro to manage Macs in your organization and want users to be managed by Intune, you must remove the connection between Jamf Pro and Intune. Remove the connection by using the Jamf Pro console. 

1. In Jamf Pro, go to **Global Management** > **Conditional Access**. On the **macOS Intune Integration** tab, select **Edit**.
2. Clear the **Enable Intune Integration for macOS** check box.
3. Select **Save**. Jamf Pro sends your configuration to Intune and the integration will be terminated.
4. Sign in to [Intune](https://go.microsoft.com/fwlink/?linkid=2090973). Go to **Microsoft Intune** > **Device Compliance** > **Partner device management** to verify that the status is now **Terminated**. 

   > [!NOTE]
   > Your organization's Mac devices will be removed at the date (3 months) shown in your console. 

## Next steps

- [Apply compliance policies to Jamf-managed devices](conditional-access-assign-jamf.md)
- [Data Jamf sends to Intune](data-jamf-sends-to-intune.md)
