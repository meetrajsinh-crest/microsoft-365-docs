---
title: Onboard your organization's devices to Microsoft Defender for Business
description: Onboard your organization's devices to Microsoft Defender for Business
search.appverid: MET150
author: denisebmsft
ms.author: deniseb
manager: dansimp 
audience: Admin
ms.topic: how-to
ms.service: o365-administration
ms.localizationpriority: high
ms.reviewer: shlomiakirav
f1.keywords: NOCSH 
ms.collection: 
- SMB
- M365-security-compliance
---

# Onboard enrolled devices to Microsoft Defender for Business

Microsoft 365 Business Premium includes [Microsoft Defender for Business](../security/defender-business/mdb-overview.md), an endpoint security solution for small and medium-sized businesses. Defender for Business provides next-generation protection (antivirus, antimalware, and cloud-delivered protection), firewall protection, web content filtering, and more for your company's devices. Protection is applied when you onboard devices and apply security policies to those devices.

To onboard devices to Defender for Business, you can choose from several options:

- [Automatic onboarding for Windows devices that are already enrolled in Microsoft Intune](#use-automatic-onboarding-for-windows-devices-that-are-already-enrolled-in-intune)
- [A local script to onboard Windows and Mac devices to Defender for Business](#use-a-local-script-to-onboard-windows-and-mac-devices-to-defender-for-business) (for devices that are not already enrolled in Intune)
- [Intune for enrolling new devices, including mobile devices](#use-intune-to-enroll-devices) (Windows, Mac, iOS, and Android) and then apply Defender for Business policies to those devices

This article also includes:

- [What about servers?](#what-about-servers) (NEW!)
- [How to run a detection test on a Windows device](#run-a-detection-test-on-a-windows-device)
- [How to onboard devices gradually](#onboard-devices-gradually)
- [How to offboard a device](#offboard-a-device) if a device is replaced or someone leaves the organization

> [!IMPORTANT]
> If something goes wrong and your onboarding process fails, see [Microsoft Defender for Business troubleshooting](../security/defender-business/mdb-troubleshooting.yml).

## Use automatic onboarding for Windows devices that are already enrolled in Intune

You can onboard Windows client devices to Defender for Business automatically if those devices are already enrolled in Intune. Defender for Business detects Windows client devices that are already enrolled in Intune, and prompts you to choose whether to onboard those devices automatically. Security policies and settings in Defender for Business are then applied to those devices. We call this process *automatic onboarding*. 

Automatic onboarding helps get your devices protected almost immediately. 
Note that the automatic onboarding option applies to Windows client devices only, if the following conditions are met:

- Your organization was already using Intune or Mobile Device Management (MDM) in Intune before you got Defender for Business (Microsoft 365 Business Premium customers already have Microsoft Intune and MDM).
- You already have Windows client devices enrolled in Intune.

> [!TIP]
> If you're prompted to use automatic onboarding, we recommend selecting the "all devices enrolled" option. That way, when Windows devices are enrolled in Intune later on, they'll be onboarded to Defender for Business automatically.

To learn more about automatic onboarding, see [Use the wizard to set up Microsoft Defender for Business](../security/defender-business/mdb-use-wizard.md).

## Use a local script to onboard Windows and Mac devices to Defender for Business

You can use a local script to onboard Windows and Mac devices. When you run the onboarding script on a device, it creates a trust with Azure Active Directory (if that trust doesn't already exist), enrolls the device in Intune (if it isn't already enrolled), and then onboards the device to Defender for Business. You can onboard up to 10 devices at a time using the local script.

See [Onboard devices to Microsoft Defender for Business](../security/defender-business/mdb-onboard-devices.md) for detailed instructions.

## Use Intune to enroll devices

To enroll a device, you can enroll it yourself, or have users sign in to the company portal app, enroll their devices, and then install any apps that are needed. 

If you were already using Intune or Mobile Device Management before you got Defender for Business, you can continue to use Intune to onboard your organization's devices. With Intune, you can onboard computers, tablets, and phones, including iOS and Android devices.

See [Device enrollment in Microsoft Intune](/mem/intune/enrollment/device-enrollment). 

## What about servers?

Servers are not supported by default in Microsoft 365 Business Premium and Defender for Business. However, the ability to onboard a server, such as an endpoint running Windows Server or Linux Server, is now in preview. Make sure to review the requirements before onboarding a server:

- You have a server license for each server instance in either Microsoft 365 Business Premium or Defender for Business (standalone).
- The **Preview features** setting is turned on. In the Microsoft 365 Defender portal ([https://security.microsoft.com](https://security.microsoft.com)), go to **Settings** > **Endpoints** > **General** > **Advanced features** > **Preview features**.
- The enforcement scope for Windows Server is turned on. Go to **Settings** > **Endpoints** > **Configuration management** > **Enforcement scope**. Select **Use MDE to enforce security configuration settings from MEM**, select  **Windows Server**, and then select **Save**.

See the **servers** tab in [Onboard devices to Microsoft Defender for Business](../security/defender-business/mdb-onboard-devices.md) for detailed instructions.

## Run a detection test on a Windows device

After you've onboarded Windows devices to Defender for Business, you can run a detection test on a Windows device to make sure that everything is working correctly.

1. On the Windows device, create a folder: `C:\test-MDATP-test`.

2. Open Command Prompt as an administrator.

3. In the Command Prompt window, run the following PowerShell command:

   ```powershell
   powershell.exe -NoExit -ExecutionPolicy Bypass -WindowStyle Hidden $ErrorActionPreference = 'silentlycontinue';(New-Object System.Net.WebClient).DownloadFile('http://127.0.0.1/1.exe', 'C:\\test-MDATP-test\\invoice.exe');Start-Process 'C:\\test-MDATP-test\\invoice.exe'
   ```

After the command has run, the Command Prompt window closes automatically. If successful, the detection test is marked as completed, and a new alert appears in the Microsoft 365 Defender portal ([https://security.microsoft.com](https://security.microsoft.com)) for the newly-onboarded device in about ten minutes.

## Onboard devices gradually

If you prefer to onboard devices in phases, which we call *gradual device onboarding*, follow these steps: 

1. Identify a set of devices to onboard.

2. Go to the Microsoft 365 Defender portal ([https://security.microsoft.com](https://security.microsoft.com)), and sign in.

3. In the navigation pane, choose **Settings** > **Endpoints**, and then under **Device management**, choose **Onboarding**.

4. Select an operating system (such as **Windows 10 and 11)**, and then choose an onboarding method (such as **Local script**). Follow the guidance provided for the method you selected.

5. Repeat this process for each set of devices you want to onboard. 

> [!TIP]
> You don't have to use the same onboarding package every time you onboard devices. For example, you can use a local script to onboard some devices, and later on, you can choose another method to onboard more devices.

## Offboard a device

If you want to offboard a device, use one of the following procedures:

1. In the navigation pane, choose **Settings**, and then choose **Endpoints**.

2. Under **Device management**, choose **Offboarding**.

3. Select an operating system, such as **Windows 10 and 11**, and then, under **Offboard a device**, in the **Deployment method** section, choose **Local script**. 

4. In the confirmation screen, review the information, and then choose **Download** to proceed.

5. Select **Download offboarding package**. We recommend saving the offboarding package to a removable drive.

6. Run the script on each device that you want to offboard. Need help with this task? See the following resources:   

   - Windows devices: [Offboard Windows devices using a local script](../security/defender-endpoint/configure-endpoints-script.md#offboard-devices-using-a-local-script) 
   - Mac: [Uninstalling on Mac](../security/defender-endpoint/mac-resources.md#uninstalling)

> [!IMPORTANT]
> Offboarding a device causes the devices to stop sending data to Defender for Business. However, data received prior to offboarding is retained for up to six (6) months.

## Next objective

[Set up protection for your Windows devices](m365bp-protection-settings-for-windows-10-devices.md).
