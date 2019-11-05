---
title: 创建服务元数据的开发人员指南
description: 创建服务元数据的开发人员指南
ms.assetid: 2d250bce-2dd2-4bd8-aa0f-432dde7783e1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28de135945016ac249a7a0a19951dcb822b72b3a
ms.sourcegitcommit: 724404f7baf0f7f9a8bd3fd3eaf41c09f45a9e60
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445360"
---
# <a name="developer-guide-for-creating-service-metadata"></a>创建服务元数据的开发人员指南

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]


This guide walks you through the process of creating a service metadata package on the Windows Dev Center hardware dashboard, previously known as Sysdev (<https://sysdev.microsoft.com>). Service metadata is required to connect a mobile broadband app to your hardware device. When a user plugs a mobile broadband device into their computer, the associated service metadata is downloaded and then the mobile broadband app is automatically downloaded.

You can leverage service metadata to create a deeply integrated experience with Windows. Service metadata packages allow you to include branding information, such as icons and your operator name, configure settings and permissions for accessing SIM hardware and personal hotspots, and provision mobile broadband apps to work with your mobile broadband device.

**注意**  
Even though the mobile broadband app is automatically installed, the user must pin it to the Start Screen manually.



## <a name="span-idgetting_startedspanspan-idgetting_startedspanspan-idgetting_startedspangetting-started"></a><span id="Getting_started"></span><span id="getting_started"></span><span id="GETTING_STARTED"></span>Getting started


To create a successful service metadata package, you must complete the steps included in this section.

### <a name="span-idregister_your_company_with_the_windows_dev_center_hardware_dashboardspanspan-idregister_your_company_with_the_windows_dev_center_hardware_dashboardspanspan-idregister_your_company_with_the_windows_dev_center_hardware_dashboardspanregister-your-company-with-the-windows-dev-center-hardware-dashboard"></a><span id="Register_your_company_with_the_Windows_Dev_Center_hardware_dashboard"></span><span id="register_your_company_with_the_windows_dev_center_hardware_dashboard"></span><span id="REGISTER_YOUR_COMPANY_WITH_THE_WINDOWS_DEV_CENTER_HARDWARE_DASHBOARD"></span>Register your company with the Windows Dev Center hardware dashboard

-   Your company has an active account on the Windows Dev Center hardware dashboard. If your company does not have an account on the Windows Dev Center hardware dashboard, you can create a new account and add your user account to you company. For more info, see [Administration](https://docs.microsoft.com/windows-hardware/drivers/dashboard/administration) in the Windows Dev Center hardware dashboard help.

-   Your company has a VeriSign code signing certificate to sign the packages.

### <a name="span-idservice_metadata_wizard_access_and_service_identifiers_registrationspanspan-idservice_metadata_wizard_access_and_service_identifiers_registrationspanspan-idservice_metadata_wizard_access_and_service_identifiers_registrationspanservice-metadata-wizard-access-and-service-identifiers-registration"></a><span id="Service_Metadata_wizard_access_and_service_identifiers_registration"></span><span id="service_metadata_wizard_access_and_service_identifiers_registration"></span><span id="SERVICE_METADATA_WIZARD_ACCESS_AND_SERVICE_IDENTIFIERS_REGISTRATION"></span>Service Metadata wizard access and service identifiers registration

MNOs and MVNOs must complete the following steps before you can create a service metadata package:

-   Request access to the Service Metadata wizard

-   Register your service identifiers

To complete the steps above, you must send an email to sysdev@microsoft.com with the following info:

-   The organization name used when you registered for the Windows Dev Center hardware dashboard.

-   Whether you are a mobile network operator or a mobile virtual network operator.

-   Your website and justification on why you need to create a service metadata package.

Include the following service identifiers as applicable:

-   List of GSM Provider IDs

-   List of GSM Provider Names

-   List of CDMA SIDs

-   List of CDMA Provider Names

You should receive an acknowledgement emails with 24 hours that your request was received. However, it could take up to 5 business days to process the request. If we have conflicts, we’ll send you an email asking for additional information.

### <a name="span-idmobile_broadband_appspanspan-idmobile_broadband_appspanspan-idmobile_broadband_appspanmobile-broadband-app"></a><span id="Mobile_broadband_app"></span><span id="mobile_broadband_app"></span><span id="MOBILE_BROADBAND_APP"></span>Mobile broadband app

Before you create your service metadata package, ensure that your mobile broadband app has been developed and associated with the Microsoft Store. This app should provide key experiences, such as plan purchase, data usage, help and support, as well as highlighting value-added services from the operator. For more info about creating the mobile broadband app, see the following links:

-   [Mobile broadband WinRT API overview](mobile-broadband-winrt-api-overview.md)

-   [Mobile operator hardware overview](mobile-operator-hardware-overview.md)

-   [UWP mobile broadband apps](uwp-mobile-broadband-apps.md)

**注意**  
The mobile broadband app doesn’t have to be published to the Microsoft Store until the service metadata has been tested and is ready to be published externally. We recommend that the app is published to the Microsoft Store only after the service metadata package passes preview mode testing.



## <a name="span-idcreating_service_metadata_packagesspanspan-idcreating_service_metadata_packagesspanspan-idcreating_service_metadata_packagesspancreating-service-metadata-packages"></a><span id="Creating_service_metadata_packages"></span><span id="creating_service_metadata_packages"></span><span id="CREATING_SERVICE_METADATA_PACKAGES"></span>Creating service metadata packages


Creating a service metadata package starts with the Service Metadata wizard that is available on the Windows Dev Center hardware dashboard. For more info on the Service Metadata wizard, see [Step 2- Create the service metadata package](#2-create-the-service-metadata-package). You can use the Service Metadata wizard to create a new or edit an existing service metadata package. As you go through the wizard and fill out the values, the wizard will validate and notify you of any errors or warnings. This validation includes checking for missing or incorrect fields, service identifier ownership, mobile broadband app existence in the Microsoft Store, and so on.

When you are on the final confirmation page and ready to submit, you have the option of submitting your package either in **Developer** mode or **Preview** mode.

-   **开发人员模式**在初始阶段中使用，目的是只创建服务元数据包，并将其用于脱机测试目的。 在此模式下，将不会对包进行签名，必须手动将其下载并安装到测试计算机中，以便进行验证。 可以快速快速地查看此模式，以便创建和验证服务元数据包与设备一起工作。

-   **预览模式**当你确信包已正确编写并且已准备好进行端到端测试时使用。 在此模式下，如果正确设置了测试计算机，则 Windows 开发人员中心硬件仪表板会对包进行签名，并将自动下载到测试计算机。

完成了预览测试并验证了包适用于所有方案后，便可以将包发布到 live。

下图对工作流进行了讨论：

![创建服务元数据包](images/mbae-sxs81-createpackageworkflow.png)

若要创建新的服务元数据包，请参阅[创建服务元数据包的步骤](#steps-for-creating-a-service-metadata-package)。

若要编辑现有的服务元数据包，请参阅[编辑服务元数据包的步骤](#steps-for-editing-a-service-metadata-package)。

## <a name="steps-for-creating-a-service-metadata-package"></a>创建服务元数据包的步骤


使用以下步骤在 Windows 开发人员中心硬件仪表板上创建服务元数据包：

-   [1-收集服务元数据包所需的信息](#1-gather-the-required-information-for-the-service-metadata-package)

-   [2-创建服务元数据包](#2-create-the-service-metadata-package)

-   [3-将商店清单文件插入 Microsoft Store 设备应用](#3-insert-the-store-manifest-file-into-the-microsoft-store-device-app)

-   [4-测试服务元数据包](#4-test-the-service-metadata-package)

-   [5-发布服务元数据包](#5-publish-the-service-metadata-package)

### <a name="1-gather-the-required-information-for-the-service-metadata-package"></a>1-收集服务元数据包所需的信息

在完成本主题的步骤2中的 "服务元数据" 向导中的步骤时，需要从要与设备关联的移动宽带应用程序项目中存储的多个信息片段。 使用以下步骤收集信息，使其可用于本主题中的第2步。

**警告**  
在此步骤中收集值之前，移动宽带应用必须与 Microsoft Store 相关联。 关联移动宽带应用时，会更新包清单文件中的值，以使用 Microsoft Store 开发人员帐户中的信息。 但是，移动宽带应用不必发布到 Microsoft Store。 在你准备好发布服务元数据包之前，它可以保留在本地开发环境中。



**收集 UWP 设备应用信息**

1.  使用 Visual Studio 2013 打开移动宽带应用程序项目。

2.  在右侧窗格中，右键单击**appxmanifest.xml**文件，然后单击 "**查看代码**"。

3.  从 appxmanifest.xml 文件中收集以下属性：

    -   在**Identity**元素中，"**名称**" 属性将用于 "服务元数据" 向导中的 "**包名称**" 字段。

    -   在 "**标识**" 元素中，"**发布服务器**" 属性将用于 "服务元数据" 向导中的 "**发布者**" 字段。

    -   在**应用程序**元素中，**应用程序**子元素的**Id**属性将用于 "服务元数据" 向导中的 "**应用 Id** " 字段。

4.  关闭 appxmanifest.xml 文件。

![代码视图中的 appxmanifest.xml 文件](images/mbae-sxs-appxmanifest.png)

你还可以通过执行以下步骤来完成此操作，而无需使用 Visual Studio 2013：

**在不使用 Visual Studio 2013 的情况下收集移动宽带应用信息**

1.  导航到移动宽带应用的 appxmanifest.xml 文件。

2.  右键单击该文件，然后单击 "**打开方式**"。

3.  清除 "**对所有 appxmanifest.xml 文件使用此应用程序**" 复选框，单击 "**更多选项**"，然后单击 "**记事本**"。

4.  从 appxmanifest.xml 文件中收集以下属性：

    -   在**Identity**元素中，"**名称**" 属性将用于 "服务元数据" 向导中的 "**包名称**" 字段。

    -   在 "**标识**" 元素中，"**发布服务器**" 属性将用于 "服务元数据" 向导中的 "**发布者**" 字段。

    -   在**应用程序**元素中，**应用程序**子元素的**Id**属性将用于 "服务元数据" 向导中的 "**应用 Id** " 字段。

5.  保存并关闭 appxmanifest.xml 文件。

### <a name="2-create-the-service-metadata-package"></a>2-创建服务元数据包

Service metadata is created by using the Service Metadata Wizard in the Windows Dev Center hardware dashboard.

**To create a service metadata package**

1.  导航到 <https://sysdev.microsoft.com>。

2.  Under the **Device metadata** heading, click **Create mobile broadband experience**.

    ![this is the landing page for the dashboard](images/mbae-sxs81-dashboard.png)

3.  On the **Service info** page, complete the following fields, and then click **Next**.

    -   **Enter the name for your network that is to be used in the Windows network selection UI** – The name of you network that will be displayed to customers in Windows Connection Manager.

    -   **Enter your service number** – A GUID that must match the carrier ID field in your provisioning metadata. You can create a GUID by using Visual Studio 2013. For more information on how to create a GUID, see [Create GUID (guidgen.exe)](https://go.microsoft.com/fwlink/p/?linkid=330070).

    -   **Upload your icon that is to be shown in the Windows network selection UI** – Click **Browse**, and then select the icon that is shown to customers in Windows Connection Manager.

    -   **Enter the Windows notification event handler in your app (optional unless entitlement check is required below)** – This is the notification handler that was registered in your mobile broadband app.

    -   **Do you want to allow users to share their mobile broadband connection (personal hotspot)?** – The possible options are **Always allow**, **Allow only with entitlement check (Windows notification event handler required)** , and **Never allow**. The default option is to always allow.

    -   **Do you want to require system admin privileges to perform PIN unlock on SIMs?** – If you want to require system administrator privileges to PIN unlock a SIM card, click the **Yes** option.

    ![the service info step of the wizard](images/mbae-sxs81-serviceinfostep.png)

4.  On the **Hardware info** page, select the information that should be used to identify your experience. Once a check box is selected, you can add the appropriate network ranges. The ID generated should exist in the Windows APN database so the right subscriber is identified. For more information about the APN database, see [COSA/APN database submission](cosa-apn-database-submission.md).

    -   If you are a GSM Provider that uses the International Mobile Subscriber Identity (IMSI), select the **IMSI** check box under the **GSM** heading. In the **Provider ID** box, enter the GSM service provider ID. Under the **IMSI/ICCID Ranges** heading, enter the range, and then click **Add**.

    -   If you are a GSM provider that uses the integrated circuit card identifier (ICCID), select the **SIM ICC ID** check box under the **GSM** heading. Under the **Enter the Provider ID and ICC ID range** heading, enter the range, and then click **Add**.

    -   If you are a GSM provider that uses the home provider name, select the **Home provider name** check box under the **GSM** heading. Under the **Enter the Home Provider Name or enter the Provider ID (MCC+MNC)** heading, enter the provider ID and provider name, and then click **Add**.

    -   If you are a CDMA provider that uses the SID, select the **SID** check box under the **CDMA** heading. In the **Enter the SID** box, enter the CDMA SID.

    -   If you are a CDMA provider that uses the provider name, select the **Provider name** check box under the **CDMA** heading. In the **Enter Provider Name** box, enter the CDMA service provider name.

    -   单击**下一步**。

    ![this is the hardware info step of the wizard](images/mbae-sxs81-hardwareinfostep.png)

5.  On the **App info** page, enter the information you gathered in Step 1 of this topic. If you want to add additional privileged apps, click **Add**, and then enter up to 7 more. When all of the privileged apps are entered, click **Next**.

    ![this is the app info step of the wizard](images/mbae-sxs81-appinfostep.png)

6.  On the **Confirm** page, verify that the information is correct. Select the **Developer Mode** or **Preview Mode** option, and then click **Submit**.

    -   **Developer Mode** – The package is not signed and it must be manually downloaded and installed on every computer. 如果需要保存该程序包以进行脱机开发，请使用此选项。

    -   **Preview Mode** – The package is signed and automatically downloaded from Microsoft to test computers with the appropriate registry settings configured. 预览模式不会进行检查以确保将移动宽带应用程序发布到 Microsoft Store。

    ![这是向导的 "确认" 步骤](images/mbae-sxs81-confirm.png)

### <a name="3-insert-the-store-manifest-file-into-the-microsoft-store-device-app"></a>3-将商店清单文件插入 Microsoft Store 设备应用

应用商店清单文件必须包含在 UWP 设备应用中。 使用以下步骤从服务元数据包下载应用商店清单文件，并将其插入移动宽带应用项目中。

**插入存储清单文件**

1.  在 Windows 开发人员中心硬件仪表板上，在服务元数据包的 "管理体验" 页上，单击服务元数据包，然后单击 " **storemanifest.xml** " 下载应用商店清单文件。

    ![下载应用商店清单文件](images/mbae-sxs81-storemanifest.png)

2.  使用 Visual Studio 2013 打开移动宽带应用程序项目。

3.  右键单击该项目，单击 "**添加**"，然后单击 "**现有项**"。

4.  浏览到下载的应用商店清单文件，然后单击 "**添加**"。

5.  重新编译移动宽带应用并再次将其发布到 Microsoft Store。

### <a name="4-test-the-service-metadata-package"></a>4-测试服务元数据包

若要测试服务元数据包，必须有移动宽带设备和服务元数据包文件。 配置测试系统和安装服务元数据包的说明取决于包的模式。

### <a name="span-idtest_a_service_metadata_package_in_developer_modespanspan-idtest_a_service_metadata_package_in_developer_modespanspan-idtest_a_service_metadata_package_in_developer_modespantest-a-service-metadata-package-in-developer-mode"></a><span id="Test_a_service_metadata_package_in_developer_mode"></span><span id="test_a_service_metadata_package_in_developer_mode"></span><span id="TEST_A_SERVICE_METADATA_PACKAGE_IN_DEVELOPER_MODE"></span>在开发人员模式下测试服务元数据包

您必须手动下载包并将其安装在正确的位置，以使方案正常工作。 需要从两个不同的入口点访问开发人员模式包，具体取决于你是创作新包还是现有包。

如果创建了新的包，请在 Windows 开发人员中心硬件仪表板中，单击 "**管理体验**"，然后单击 "未**关联的开发包**（**管理体验**表中的第一项"）。 下图显示了一个示例：

![下载服务元数据包](images/mbae-sxs81-managedevpackages.png)

如果你编辑了已与某个经验关联的现有服务元数据包，请从 "**管理体验**" 表中选择该体验，然后你将在 "**元包**" 表中看到 "开发人员模式" 包。 单击 "**下载 MBAE Zip 包编辑**" 以下载它。

![下载服务元数据包](images/mbae-sxs81-manageassociatedpackages.png)

下载服务元数据包后，必须启用测试签名，因为服务元数据包未签名。 若要启用测试签名，请**运行 bcdedit –** 从提升的命令提示符中设置 testsigning，然后重新启动计算机。

启用测试签名后，\*将 devicemetadata-ms 文件从服务元数据包复制到以下位置： **% ProgramData%\\Microsoft\\Windows\\DeviceMetadataStore\\** <em>区域性</em>，其中*culture*是计算机的当前区域性代码。

### <a name="span-idtest_a_service_metadata_package_in_preview_modespanspan-idtest_a_service_metadata_package_in_preview_modespanspan-idtest_a_service_metadata_package_in_preview_modespantest-a-service-metadata-package-in-preview-mode"></a><span id="Test_a_service_metadata_package_in_preview_mode"></span><span id="test_a_service_metadata_package_in_preview_mode"></span><span id="TEST_A_SERVICE_METADATA_PACKAGE_IN_PREVIEW_MODE"></span>在预览模式下测试服务元数据包

如果服务元数据包处于预览模式，则必须在测试计算机上创建 PreviewKey 注册表项。 有关配置 PreviewKey 注册表项的详细信息，请参阅[创建预览包](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)。

**注意**  
您无需启用测试签名来测试处于预览模式下的服务元数据包。



创建 PreviewKey 注册表项后，请插入移动宽带设备，并确保它显示在 "网络" 列表中。 如果没有，请参阅[故障排除](#troubleshooting)部分了解详细信息。

### <a name="span-idclear_the_existing_service_metadataspanspan-idclear_the_existing_service_metadataspanspan-idclear_the_existing_service_metadataspanclear-the-existing-service-metadata"></a><span id="Clear_the_existing_service_metadata"></span><span id="clear_the_existing_service_metadata"></span><span id="CLEAR_THE_EXISTING_SERVICE_METADATA"></span>清除现有的服务元数据

在 PC 上安装服务元数据时，元数据中包含的值将存储在多个不同的位置，包括注册表、元数据缓存、元数据存储、WWAN 配置文件和开发节点。 这会使重复多个具有相同或不同元数据包的测试变得很困难。 若要确保正确安装服务元数据，应清除任何现有的服务元数据。 可以通过设置测试计算机来运行删除所有跟踪的 PowerShell 脚本，从而清除现有的服务元数据。 首先，必须在测试计算机上设置环境：

**注意**  
这在 Windows RT 设备上不起作用。 使用名为 "在运行 Windows RT 的设备上清除服务元数据" 过程中的步骤。



**设置用于清除服务元数据的环境**

1.  下载 psexec （<https://go.microsoft.com/fwlink/p/?linkid=330071>），然后将其解压缩到文件夹。

2.  下载并安装 Windows 驱动程序工具包 Windows 8.1 （<https://go.microsoft.com/fwlink/?LinkId=330072>）。

3.  导航到 WDK 文件的安装位置。 默认位置为**C：\\Program Files （x86）\\Windows 工具包\\8.1\\工具**。 如果测试计算机运行的是 x86，请将该 x86 文件夹中的 devcon 复制到与 psexec 相同的文件夹中。 如果测试计算机运行的是 x64，请从 x64 文件夹复制 devcon。

4.  将以下脚本作为 MetadataRemovalScript 保存到与 Devcon 和 PsExec 相同的文件夹中。

    **注意**  
    在保存文件之前，请在 "**保存类型**" 框中选择 "**所有文件（\*\*）** "。




```PowerShell
# DEVICE SHOULD BE CONNECTED TO MACHINE

Write-Host "Launching devcon to remove MBAE software device nodes devcon.exe remove @SWD\MBAE\*"
$DevconParameters = ' remove @SWD\MBAE\* '
try
{
   Start-Process devcon.exe -ArgumentList $DevconParameters
}
catch
{
   $Error[0] # Dump details about the last error
   Write-Host "Error running devcon.exe " $DevconParameters
   exit
}

Write-Host "Removing MB Profiles"
$mbprcmd = "mbn sh pr i=*"
$mddelprcmd = "mbn del pr i=* name="

$cmdout = $mbprcmd | netsh | Out-String

$tokens = $cmdout.Split( [String[]] ("`r`n"), [StringSplitOptions]::RemoveEmptyEntries)

if($tokens.Length -gt 3)
{
   for($i=3;$i -lt $tokens.Length-1;$i++)
   {
      $x = $mddelprcmd + '"' + $tokens[$i].trim() +'"'
      Write-Host "Deleting Profile Cmd :" $x
      $x | netsh
   }
}

Write-Host ""
Write-Host "Disabling ALL Mobile Broadband Adapters"
$MBAdapters = Get-Netadapter -Name "Mobile Broadband*"

foreach($MBAdapter in $MBAdapters)
{
   Write-Host "Disabling MB Adapter :"$MBAdapter.Name
   Disable-NetAdapter -Name $MBAdapter.Name -Confirm:$false
}

Write-Host "Stopping Device Setup Manager Service"
Stop-Service DsmSvc

Write-Host "Removing MBAE metadata packages in store"
#Find Package Ids
$MBAEPackageRegKeyHive = "HKLM:\SOFTWARE\Microsoft\WwanSvc\MobileBroadbandAccounts\Accounts\"
if(Test-Path $MBAEPackageRegKeyHive)
{
    $DevMetadataStorePath = join-path -Path $Env:ProgramData -ChildPath "Microsoft\Windows\DeviceMetadataStore"

    $PackageIds = Get-ChildItem $MBAEPackageRegKeyHive | ForEach-Object {Get-ItemProperty $_.pspath} | where-object {$_.MetadataPackageId} | Foreach-Object {$_.MetadataPackageId}
    foreach($PackageId in $PackageIds)
    {
        $PackageStoreFile = $PackageId + ".devicemetadata-ms"        
        $PackageStorePath = Get-ChildItem $DevMetadataStorePath -Recurse -Filter $PackageStoreFile
        if($PackageStorePath -ne $null)
        {
            Write-Host "Deleting Device Metadata Store @" $PackageStorePath.FullName
            Remove-Item -Force $PackageStorePath.FullName
        }
    }
}

Write-Host "Removing all metadata from cache"
$DevMetadataCachePath = join-path -Path $Env:ProgramData -ChildPath "Microsoft\Windows\DeviceMetadataCache\*"
if(Test-Path $DevMetadataCachePath)
{
   Write-Host "Delete All Metadata Packages under "$DevMetadataCachePath
   Remove-Item -Recurse -Force $DevMetadataCachePath
}

Write-Host "Cleanup MBAE registry keys"
$MBAERegKeyPath = "HKLM:\SOFTWARE\Microsoft\WwanSvc\MobileBroadbandAccounts\*"
if(Test-Path $MBAERegKeyPath)
{
    Write-Host "Found MBAE reg keys - deleting"   
    Remove-Item -Path $MBAERegKeyPath -Recurse
}

Write-Host "Enabling all MB Adapters, press any key to continue"
$keypress = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyUp")

$MBAdapters = Get-Netadapter -Name "Mobile Broadband*"

foreach($MBAdapter in $MBAdapters)
{
   Write-Host "Enabling MB Adapter :"$MBAdapter.Name
   Enable-NetAdapter -Name $MBAdapter.Name -Confirm:$false
}


Write-Host "END of Script"

# DEVICE SHOULD BE CONNECTED TO MACHINE

Write-Host "Launching devcon to remove MBAE software device nodes devcon.exe remove @SWD\MBAE\*"
$DevconParameters = ' remove @SWD\MBAE\* '
try
{
    Start-Process devcon.exe -ArgumentList $DevconParameters    
}
catch
{
    $Error[0] # Dump details about the last error
    Write-Host "Error running devcon.exe " $DevconParameters
    exit
}

Write-Host "Removing MB Profiles"
$mbprcmd = "mbn sh pr i=*"
$mddelprcmd = "mbn del pr i=* name="

$cmdout = $mbprcmd | netsh | Out-String

$tokens = $cmdout.Split( [String[]] ("`r`n"), [StringSplitOptions]::RemoveEmptyEntries)

if($tokens.Length -gt 3)
{
    for($i=3;$i -lt $tokens.Length-1;$i++)
    {
        $x = $mddelprcmd + '"' + $tokens[$i].trim() +'"'
        Write-Host "Deleting Profile Cmd :" $x
        $x | netsh
    }
}

Write-Host ""
Write-Host "Please remove the MB device from the system and press any key to continue"
$keypress = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown")


Write-Host "Removing MBAE metadata packages in cache and store"
#Find Package Ids
$MBAEPackageRegKeyHive = "HKLM:\SOFTWARE\Microsoft\WwanSvc\MobileBroadbandAccounts\Accounts\"
if(Test-Path $MBAEPackageRegKeyHive)
{
    $DevMetadataCachePath = join-path -Path $Env:ProgramData -ChildPath "Microsoft\Windows\DeviceMetadataCache"
    $DevMetadataStorePath = join-path -Path $Env:ProgramData -ChildPath "Microsoft\Windows\DeviceMetadataStore"

    $PackageIds = Get-ChildItem $MBAEPackageRegKeyHive | ForEach-Object {Get-ItemProperty $_.pspath} | where-object {$_.MetadataPackageId} | Foreach-Object {$_.MetadataPackageId}
    foreach($PackageId in $PackageIds)
    {
        $PackageCacheFolder = Get-ChildItem $DevMetadataCachePath -Recurse -Filter $PackageId
        if($PackageCacheFolder -ne $null)
        {
            Write-Host "Deleting Device Metadata Cache @" $PackageCacheFolder.FullName
            Remove-Item -Recurse -Force $PackageCacheFolder.FullName
        }
        $PackageStoreFile = $PackageId + ".devicemetadata-ms"        
        $PackageStorePath = Get-ChildItem $DevMetadataStorePath -Recurse -Filter $PackageStoreFile
        if($PackageStorePath -ne $null)
        {
            Write-Host "Deleting Device Metadata Store @" $PackageStorePath.FullName
            Remove-Item -Force $PackageStorePath.FullName
        }
    }
}

Write-Host "Cleanup MBAE registry keys"
$MBAERegKeyPath = "HKLM:\SOFTWARE\Microsoft\WwanSvc\MobileBroadbandAccounts\*"
if(Test-Path $MBAERegKeyPath)
{
    Write-Host "Found MBAE reg keys - deleting"   
    Remove-Item -Path $MBAERegKeyPath -Recurse
}


Write-Host "END"
```


设置环境后，每次要清除任何现有服务元数据时，请运行以下步骤：

**清除服务元数据**

1.  确保将移动宽带设备插入测试计算机。

2.  在提升的命令提示符下，导航到已提取了 psexec 的文件夹，然后运行**psexec/s/i powershell**

3.  在 PowerShell 命令提示符中，导航到已提取 "psexec" 的文件夹。

4.  键入**set-executionpolicy 无限制**，然后按 enter。

5.  键入**Y** ，然后输入。

6.  键入 **.\\MetadataRemovalScript** ，然后按 enter。

7.  出现提示时，请删除移动宽带设备，然后按 Enter。

8.  每次要从测试计算机中清除服务元数据时，请重复这些步骤。

**在运行 Windows RT 的设备上清除服务元数据**

1. 删除 "软件设备" 节点。

   1.  在设备管理器中，单击 "**查看**"，然后单击 "**显示隐藏的设备**"。

   2.  展开 "软件设备"。

   3.  右键单击以下设备节点，然后单击 "**卸载**： **SmsDevice** " 和 " **windows.networking.networkoperators"。 MobileBroadbandAccount**

2. 从所有接口删除所有移动宽带配置文件。

   1. 在提升的命令提示符处，键入**netsh mbn sho pro i =\\** *

   2. 对于每个配置文件，键入**netsh mbn delete profile name = "此处的配置文件名" i =\\** *，然后按 enter。

3. 禁用所有移动宽带适配器。

   1.  在设备管理器中，展开 "**网络适配器**"。

   2.  右键单击每个移动宽带设备，然后单击 "**禁用**"。

4. 在提升的命令提示符下，通过键入**sc stop dsmsvc**停止 DSM 服务，然后按 enter。

5. 通过从 **% ProgramData%\\Microsoft\\Windows\\DeviceMetadataStore**中删除包含服务元数据包的任何文件夹，从设备元数据存储中删除服务元数据包。 您可以通过查找 MobileBroadbandInfo 文件来标识服务元数据包。

6. 删除所有 WWAN SVC MBAE 注册表项。

   1.  在注册表编辑器中，删除以下注册表项和所有子项： HKEY\_本地\_计算机\\软件\\Microsoft\\WwanSvc\\MobileBroadbandAccounts。

   2.  如果没有删除注册表项的权限，则必须为自己授予完全控制权限。

7. 启用所有移动宽带适配器。

   1.  在设备管理器中，展开 "**网络适配器**"。

   2.  右键单击每个移动宽带设备，然后单击 "**启用**"。

### <a name="5-publish-the-service-metadata-package"></a>5-发布服务元数据包

确认服务元数据包正确工作后，最后一步是发布包。 可以通过单击 "**发布**" 按钮选择附加到特定体验的包来释放包，如下所示。

![发布服务元数据包](images/mbae-sxs81-releasetolive.jpg)

## <a name="steps-for-editing-a-service-metadata-package"></a>Steps for editing a service metadata package


You can edit a service metadata package by using the Manage Experiences page of the Windows Dev Center hardware dashboard.

![the manage experiences page](images/mbae-sxs81-manageexperience.png)

## <a name="troubleshooting"></a>“疑难解答”


Open the networks list and look for your mobile broadband network. If the network is listed by using the name and icon that you used in the service metadata package **ServiceInfo.xml** file, the package is correctly parsed. If you are updating a service metadata package that has the same name and icon, or if the name or icon has not appeared in the list after about approximately one minute, you should perform additional steps, as discussed here:

-   Force a metadata refresh

-   Check the metadata cache

-   Check the registry

-   Check the WWAN Logs

### <a name="span-idforcemdrefspanspan-idforcemdrefspanforce-a-metadata-refresh"></a><span id="forcemdref"></span><span id="FORCEMDREF"></span>Force a metadata refresh

Some parts of the metadata and mobile broadband app systems rely on network access, which can fail and leave the computer in an inconsistent state. If this happens, you can encounter a situation where service metadata is not installed or the mobile broadband app is not installed. The system periodically tries to remedy the situation, but to conserve power, retries are fairly infrequent (just a few times a day). Instead of waiting for the next retry, you can manually force a refresh to happen immediately. 要实现这一点，请执行下列操作：

1.  Open the desktop **Control Panel**.

2.  Open **Devices and Printers**.

3.  From the **View** menu, click **Refresh**, or press the **F5** key. This action causes metadata to be reparsed and background events to be re-registered.

**重要须知**  
If a service metadata package has already been successfully parsed, the system will treat this refresh as a metadata update. In this case, your metadata package must have a different GUID in its filename and an updated timestamp in the [LastModifiedDate](lastmodifieddate.md) element of **PackageInfo.xml**.



### <a name="span-idcheckmdcachespanspan-idcheckmdcachespancheck-the-metadata-cache"></a><span id="checkmdcache"></span><span id="CHECKMDCACHE"></span>Check the metadata cache

If a metadata refresh did not fix the problem, make sure that the service metadata package is valid and that it has the correct Hardware IDs. 要实现这一点，请执行下列操作：

1. Navigate to **%programdata%\\Microsoft\\Windows\\DeviceMetadataCache\\dmrccache\\** <em>culture</em>, where *culture* is the culture code for the current culture of your test computer (for example, **en-us** or **es-es**).

2. Look for a folder that has the same name as your metadata package (without the **.devicemetadata-ms** extension). If this directory does not exist, it can mean one of four things:

   -   The service metadata package is corrupt.

   -   The service metadata package does not have the correct Hardware IDs.

   -   The mobile broadband device is not in a state where metadata can be downloaded, or you plugged in the device before you copied the service metadata package.

   -   A problem occurred when checking the digital signature on the metadata package. This is usually caused by not having test signing enabled on your test computer.

If you’re sure that the package is not corrupted and that you first plugged in the mobile broadband device after you copied the service metadata package, check the IMSI ranges. It’s very easy to type in too many or too few 0s or 9s. If the problem persists after confirming or correcting these items, you must look at the registry.

### <a name="span-idcheckregspanspan-idcheckregspancheck-the-registry"></a><span id="checkreg"></span><span id="CHECKREG"></span>Check the registry

**警告**  
You should not edit registry data that does not belong to your application unless it is absolutely necessary. If there is an error in the registry, your system might not function properly. Do not, under any circumstances, delete the **MobileBroadbandAccounts** registry key. Windows 不会重新创建它，并且你将中断此功能。



Perform the following steps to check the registry:

1.  打开注册表编辑器。

2.  Go to **HKLM\\SOFTWARE\\Microsoft\\WwanSvc\\MobileBroadbandAccounts**.

3.  Inside this registry key, look for three other keys: **Accounts**, **NetworkInterfaceBindings**, and **Data**. These keys do not exist by default; they are automatically created the first time that a mobile broadband device is inserted, turned on, or connected.

4.  如果**帐户**或**NetworkInterfaceBindings**密钥不存在，并且已插入或打开移动宽带适配器，请检查 WWAN 日志。

5.  如果其中的部分或全部项存在，请在**树**视图中展开 "**帐户**" 键。 其中的一个或多个注册表项的名称与 Guid 类似。 注册表树项应类似于如下所示的注册表树：

    ![已分析帐户的注册表项](images/fig2-registryentries-for-parsedmobilebroadbandaccount.png)

    如果注册表项类似于上图（值名称将略有不同，具体取决于该帐户是位于 GSM 还是 CDMA 网络上），并且如果在 "网络" 列表中看不到该图标，则应查看事件日志。

    如果注册表项类似于下一个图，则意味着移动宽带适配器是在将服务元数据包复制到设备元数据存储区之前插入的，服务元数据包已损坏，或者硬件 Id 不正确. 若要解决在将元数据包复制到元数据存储区之前插入或打开设备的情况，请执行强制执行元数据刷新中的步骤。 否则，请按照检查 WWAN 日志中的步骤进行操作。

    ![未分析帐户的注册表项](images/fig1-registryentries-for-unparsedmobilebroadbandaccount.png)

### <a name="span-idcheckwwanlogsspanspan-idcheckwwanlogsspancheck-the-wwan-logs"></a><span id="checkwwanlogs"></span><span id="CHECKWWANLOGS"></span>检查 WWAN 日志

如果**HKLM\\SOFTWARE\\Microsoft\\WwanSvc\\MobileBroadbandAccounts**上没有**帐户**或**NetworkInterfaceBindings**注册表项，或者如果有未完全填充的条目，则必须查看 WWAN 日志。 以下步骤会将计算机重置为已知状态：

1.  拔下或关闭移动宽带设备（如果嵌入了设备，请在**设备管理器**中禁用该设备）。

2.  删除以下注册表项：

    -   **HKLM\\软件\\Microsoft\\WwanSvc\\MobileBroadbandAccounts\\帐户**

    -   **HKLM\\软件\\Microsoft\\WwanSvc\\MobileBroadbandAccounts\\NetworkInterfaceBindings**

    **警告**  
    请勿在任何情况下删除**HKLM\\SOFTWARE\\Microsoft\\WwanSvc\\MobileBroadbandAccounts\\** 注册表项。 Windows 不会重新创建它，并且你将中断此功能。



日志中有两种类型的条目：帐户管理 WWAN 服务条目日志条目和分析器任务条目。 第一种类型可帮助调试由网络硬件问题导致的问题，第二种类型可帮助调试元数据分析问题。

帐户管理 WWAN 服务条目已成功处理的网络的日志条目类似于以下内容：

```syntax
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:26.567 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Account updater started for network interface {7a0a0dce-0a51-471a-8c16-6e767cd0b861. 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:26.567 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Getting home provider ID from hardware device for network interface {7A0A0DCE-0A51-471A-8C16-6E767CD0B861}.  Provider ID is "234567". 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:26.567 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Getting home provider name from hardware device for network interface {7A0A0DCE-0A51-471A-8C16-6E767CD0B861}.  Provider name is "MS GSM". 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:26.586 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Network identity not recognized, assigning new network account ID. 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:26.597 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Devnode create/update started. 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:26.617 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Devnode create/update finished. 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:26.617 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Data store create/update started. 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:26.707 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Data store create/update finished. 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:26.707 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Account updater finished for network interface {7a0a0dce-0a51-471a-8c16-6e767cd0b861}.
```

可以通过在日志中搜索**帐户管理**来查找这些条目。 在这种情况下，最重要的项是**数据存储创建/更新已开始**，并且**数据存储创建/更新已完成**。 如果这些条目存在并且没有错误消息，则硬件的行为正常。 （此处提到的数据存储包含检查注册表中讨论的注册表项。）

与此相反，在删除 SIM 的设备上，条目通常如下所示：

```syntax
[0]02CC.03E4::‎2012‎-‎01‎-‎04 09:29:50.309 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Account updater started for network interface {7a0a0dce-0a51-471a-8c16-6e767cd0b861}. 
[0]02CC.03E4::‎2012‎-‎01‎-‎04 09:29:50.309 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Detected removal of SIM from device bound to network interface {7A0A0DCE-0A51-471A-8C16-6E767CD0B861}. 
[0]02CC.03E4::‎2012‎-‎01‎-‎04 09:29:50.309 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Devnode create/update started. 
[0]02CC.03E4::‎2012‎-‎01‎-‎04 09:29:50.309 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Devnode create/update finished. 
[0]02CC.03E4::‎2012‎-‎01‎-‎04 09:29:50.309 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Account updater finished for network interface {7a0a0dce-0a51-471a-8c16-6e767cd0b861}. 
```

**注意**  
在后一示例中，没有用于**数据存储创建/更新**的条目，或者**数据存储创建/更新已完成**。 由于存储在 SIM 中的信息对于帐户管理过程至关重要，因此没有 SIM 的设备将不具有必要的关联元数据。



如果硬件已成功处理，但你的徽标或名称未显示在 "网络" 列表中，则可能是元数据包有问题。 可以通过在日志中使用分析器任务项来对此进行调查。 若要查找这些条目，请搜索 "**分析器-任务**"。 成功分析的日志条目通常如下所示：

```syntax
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.007 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Parser task started. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.030 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Parsing metadata for device container with id "{972238E7-36F4-11E1-BC81-00155DE96B01}" for culture "en-US". 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.297 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Starting parse of mobile broadband service information file. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.297 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Metadata package contains no data for culture "en-US". Using fallback data. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.356 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Finished parse of mobile broadband service information file. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.356 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Starting update of stored network account information. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.377 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]The mobile broadband account now contains service provider information. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.378 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Finished update of stored network account information. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.378 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Applying WWAN profiles for service provider Contoso GSM. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.378 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Starting creation and/or update of WWAN profiles. 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:32.512 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: Profile Update Notification received 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:32.519 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: Complete Scanning 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:32.519 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: WWAN Interface information 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:32.586 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: Profile Update Notification received 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:32.651 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: Profile Update Notification received 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.659 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Finished creation and/or update of WWAN profiles. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.659 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]WWAN profiles applied successfully for service provider Contoso GSM. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.659 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Adding trusted provisioning certificates for service provider Contoso GSM. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.659 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Starting setting of trusted certificates for network provisioning. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:33.016 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Finished setting of trusted certificates for network provisioning. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:33.016 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Trusted provisioning certificates added successfully for service provider Contoso GSM. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:33.017 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Parser task finished. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:33.017 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]MbaeParserTask completed successfully. 
```

这些日志显示**MobileBroadbandInfo**文件已正确分析，分析程序任务应用了 wwan 配置文件（以及成功更新配置文件的 wwan 服务日志记录），并且分析器任务将受信任的预配**MobileBroadbandInfo**中提到的证书。

如果进程的任何部分失败，则记录该失败。 例如，如果 "服务提供程序" 图标文件上的数字签名检查失败，日志条目通常如下所示：

```syntax
[0]0F24.0C70::‎2012‎-‎01‎-‎04 10:09:49.271 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Parser task started. 
[0]0F24.0C70::‎2012‎-‎01‎-‎04 10:09:49.288 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Parsing metadata for device container with id "{97223B34-36F4-11E1-BC81-00155DE96B01}" for culture "en-US". 
[0]0F24.0C70::‎2012‎-‎01‎-‎04 10:09:49.483 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Starting parse of mobile broadband service information file. 
[0]0F24.0C70::‎2012‎-‎01‎-‎04 10:09:49.483 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Metadata package contains no data for culture "en-US". Using fallback data. 
[0]0F24.0C70::‎2012‎-‎01‎-‎04 10:09:49.547 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Finished parse of mobile broadband service information file. 
[0]0F24.0C70::‎2012‎-‎01‎-‎04 10:09:49.547 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Starting update of stored network account information. 
[0]0F24.0C70::‎2012‎-‎01‎-‎04 10:09:49.688 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Digital signature verification failed for file "c:\programdata\microsoft\windows\devicemetadatacache\dmrccache\en-us\B68264FF-E4D1-49B1-AB5F-2B9C1C16EF5D\ServiceInformation\ContosoBroadband.ico". 
[0]0F24.0C70::‎2012‎-‎01‎-‎04 10:09:49.690 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Finished update of stored network account information. 
[0]0F24.0C70::‎2012‎-‎01‎-‎04 10:09:49.692 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Parser task finished. 
[0]0F24.0C70::‎2012‎-‎01‎-‎04 10:09:49.692 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]MbaeParserTask did not complete successfully.  Error is 0x80070306: One or more errors occurred while processing the request. 
```

由于分析器任务需要多次运行，因此可能会看到多个 `[Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]` 日志条目集。 在这种情况下，条目集通常是相同的，如果它们不相同，则可能表示存在间歇问题。

## <a name="span-idadditional_resourcesspanspan-idadditional_resourcesspanspan-idadditional_resourcesspanadditional-resources"></a><span id="Additional_resources"></span><span id="additional_resources"></span><span id="ADDITIONAL_RESOURCES"></span>其他资源


使用以下链接详细了解 Windows 8.1 和 Windows 10 中的移动宽带：

-   [移动宽带概述](overview-of-mobile-broadband.md)

-   [APN 数据库概述](apn-database-overview.md)

-   [服务元数据](service-metadata.md)









