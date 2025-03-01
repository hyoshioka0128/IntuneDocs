---
# required metadata

title: What info can your company see when you enroll your device?
description: Explains what IT can and can't see on your managed device.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/17/2018
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
ms.assetid: 12655728-a1af-4d89-97bc-925fe36c0dc4
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:
#ms.devlang:
ms.reviewer: esmich
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:
ms.collection: M365-identity-device-management
---

# What information can my organization see when I enroll my device?

Your organization cannot see your personal information when you enroll a device with Microsoft Intune. When you enroll a device, you give your organization permission to view certain pieces of information on your device, such as device model and serial number. Your organization uses this information to help protect the corporate data on the device.

**What your organization can never see:**

- Calling and web browsing history
- Email and text messages
- Contacts
- Calendar
- Passwords
- Pictures, including what's in the photos app or camera roll
- Files

**What your organization can always see:**

- Device model, like Google Pixel
- Device manufacturer, like Microsoft
- Operating system and version, like iOS 12.0.1
- App inventory and app names, like Microsoft Word. On personal devices, your organization can only see your managed app inventory. On corporate-owned devices, your organization can see all of your app inventory.
- Device owner
- Device name
- Device serial number
- IMEI

**What your organization might be able to see:**

- Phone number: For **corporate**-owned devices, your full phone number can be seen. For **personal**-owned devices, just the last four digits of your phone number are visible to your organization. You can see the **Ownership Type** for each individual device  by opening that device's **Device Details** page.
- Device storage space: If you can't install a required app, your organization might look at your device's storage space to figure out if space is too low.  
- Location: Your organization can never see your device's location, unless you need to recover a lost, supervised iOS device. Visit the [Apple iOS documentation](https://go.microsoft.com/fwlink/?linkid=853816) to learn more about supervised devices.  
- App inventory details: If your organization uses Mobile Threat Defense, they will be able to view details about the apps that are on your iOS device. Find out more about [Mobile Threat Defense](you-are-prompted-to-install-mtd-ios.md).
- Network information: Some information about network connections for Android devices may be available to your organization support. For example, if your organization requires devices to remain within a certain building, your device would identify the network where it is connected. 
