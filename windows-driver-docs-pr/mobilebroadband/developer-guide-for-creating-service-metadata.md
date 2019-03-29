---
title: 创建服务元数据的开发人员指南
description: 创建服务元数据的开发人员指南
ms.assetid: 2d250bce-2dd2-4bd8-aa0f-432dde7783e1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d85a2cb9294c11c91d0e8235e3c23f6c2670f166
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577400"
---
# <a name="developer-guide-for-creating-service-metadata"></a>创建服务元数据的开发人员指南

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]


本指南逐步讲解如何通过在 Windows 开发人员中心硬件仪表板，以前称为 Sysdev 上创建服务元数据包的过程 (<http://sysdev.microsoft.com>)。 若要连接到硬件设备的移动宽带应用，所需服务元数据。 当用户插入其计算机的移动宽带设备时，下载关联的服务元数据，并自动下载的移动宽带应用，然后。

您可以利用服务元数据以创建具有 Windows 的深度集成的体验。 服务元数据包允许您包括品牌信息，例如图标和操作员姓名、 配置设置和用于访问 SIM 硬件和个人热点的权限和预配移动宽带的应用程序以使用移动宽带设备。

**注意**  
即使移动宽带应用自动安装，用户必须将其固定到开始屏幕手动。



## <a name="span-idgettingstartedspanspan-idgettingstartedspanspan-idgettingstartedspangetting-started"></a><span id="Getting_started"></span><span id="getting_started"></span><span id="GETTING_STARTED"></span>入门


若要创建成功的服务元数据包，必须完成此部分中包含的步骤。

### <a name="span-idregisteryourcompanywiththewindowsdevcenterhardwaredashboardspanspan-idregisteryourcompanywiththewindowsdevcenterhardwaredashboardspanspan-idregisteryourcompanywiththewindowsdevcenterhardwaredashboardspanregister-your-company-with-the-windows-dev-center-hardware-dashboard"></a><span id="Register_your_company_with_the_Windows_Dev_Center_hardware_dashboard"></span><span id="register_your_company_with_the_windows_dev_center_hardware_dashboard"></span><span id="REGISTER_YOUR_COMPANY_WITH_THE_WINDOWS_DEV_CENTER_HARDWARE_DASHBOARD"></span>你的公司注册的 Windows 开发人员中心硬件仪表板

-   你的公司有一个有效的 Windows 开发人员中心硬件仪表板上的帐户。 如果你的公司不具有 Windows 开发人员中心硬件仪表板上的帐户，可以创建新帐户并将您的用户帐户添加到你的公司。 有关详细信息，请参阅[管理](https://msdn.microsoft.com/library/windows/hardware/mt786447)Windows 开发人员中心硬件仪表板帮助中。

-   你的公司有 VeriSign 代码签名证书进行签名的包。

### <a name="span-idservicemetadatawizardaccessandserviceidentifiersregistrationspanspan-idservicemetadatawizardaccessandserviceidentifiersregistrationspanspan-idservicemetadatawizardaccessandserviceidentifiersregistrationspanservice-metadata-wizard-access-and-service-identifiers-registration"></a><span id="Service_Metadata_wizard_access_and_service_identifiers_registration"></span><span id="service_metadata_wizard_access_and_service_identifiers_registration"></span><span id="SERVICE_METADATA_WIZARD_ACCESS_AND_SERVICE_IDENTIFIERS_REGISTRATION"></span>服务元数据向导访问和服务的标识符注册

可以创建服务元数据包之前 Mno 和 Mvno 必须完成以下步骤：

-   请求访问服务元数据向导

-   注册服务标识符

若要完成上述步骤，必须将发送一封电子邮件到sysdev@microsoft.com使用以下信息：

-   为 Windows 开发人员中心硬件仪表板注册时使用的组织名称。

-   你是移动网络运营商或移动虚拟网络的运算符。

-   你的网站和为什么需要创建服务元数据包的理由。

包括以下适用的服务标识符：

-   GSM 提供程序 Id 的列表

-   GSM 的提供程序名称的列表

-   CDMA Sid 列表

-   CDMA 的提供程序名称的列表

应会收到确认电子邮件的 24 小时内收到你的请求。 但是，可能需要最多 5 个工作日来处理该请求。 如果我们有冲突，我们将向你发送一封电子邮件，要求其他信息。

### <a name="span-idmobilebroadbandappspanspan-idmobilebroadbandappspanspan-idmobilebroadbandappspanmobile-broadband-app"></a><span id="Mobile_broadband_app"></span><span id="mobile_broadband_app"></span><span id="MOBILE_BROADBAND_APP"></span>移动宽带应用

创建服务元数据包之前，请确保你的移动宽带应用已开发并与 Microsoft Store 相关联。 此应用程序应提供密钥的体验，例如计划购买、 数据使用情况、 帮助和支持，以及突出显示的运算符的增值服务。 有关创建移动宽带应用程序的详细信息，请参阅以下链接：

-   [移动宽带的 WinRT API 概述](mobile-broadband-winrt-api-overview.md)

-   [移动运营商硬件概述](mobile-operator-hardware-overview.md)

-   [UWP 移动宽带应用程序](uwp-mobile-broadband-apps.md)

**注意**  
移动宽带应用没有服务元数据已经过测试并已准备好从外部发布之前将其发布到 Microsoft Store。 我们建议仅在服务元数据包次预览模式下测试后，应用程序将发布到 Microsoft Store。



## <a name="span-idcreatingservicemetadatapackagesspanspan-idcreatingservicemetadatapackagesspanspan-idcreatingservicemetadatapackagesspancreating-service-metadata-packages"></a><span id="Creating_service_metadata_packages"></span><span id="creating_service_metadata_packages"></span><span id="CREATING_SERVICE_METADATA_PACKAGES"></span>创建服务元数据包


创建服务元数据包开始，可在 Windows 开发人员中心硬件仪表板的服务元数据向导。 服务元数据向导的详细信息，请参阅[步骤 2-创建服务元数据包](#2-create-the-service-metadata-package)。 服务元数据向导可用于创建新的或编辑现有的服务元数据包。 完成向导并填写以下值时，该向导将验证并通知您的任何错误或警告。 此验证包括检查缺失或不正确的字段、 服务标识符所有权、 Microsoft Store 等中的移动宽带的应用程序存在。

当已准备好提交最终确认页上，必须要么提交您的包的选项中**开发人员**模式下或**预览**模式。

-   **开发人员模式**时你的意图就是创建服务元数据包并将其用于脱机测试目的，在初始阶段使用。 在此模式下，包将未签名，但将不得不手动下载并安装到测试计算机以用于验证目的。 此模式可看作是与你的设备工作的快速而快速的方法来创建和验证服务元数据包。

-   **预览模式**使用当你确信包编写正确并已准备好提交的端到端测试。 在此模式下，包将签名的 Windows 开发人员中心硬件仪表板，并且将自动获取下载以测试计算机，提供正确地预配测试计算机。

当完成预览测试，并确认你的包适用于所有方案中，则可以将发布到实时的包。

下图介绍了工作流：

![创建服务元数据包](images/mbae-sxs81-createpackageworkflow.png)

若要创建新的服务元数据包，请参阅[用于创建服务元数据包的步骤](#steps-for-creating-a-service-metadata-package)。

若要编辑现有的服务元数据包，请参阅[编辑服务元数据包的步骤](#steps-for-editing-a-service-metadata-package)。

## <a name="steps-for-creating-a-service-metadata-package"></a>有关创建服务元数据包的步骤


使用以下步骤在 Windows 开发人员中心硬件仪表板上创建服务元数据包：

-   [1-收集所需的信息的服务元数据包](#1-gather-the-required-information-for-the-service-metadata-package)

-   [2-创建服务元数据包](#2-create-the-service-metadata-package)

-   [3-插入存储区清单文件到 Microsoft Store 设备应用](#3-insert-the-store-manifest-file-into-the-uwp-device-app)

-   [4-测试服务元数据包](#4-test-the-service-metadata-package)

-   [5-发布服务元数据包](#5-publish-the-service-metadata-package)

### <a name="1-gather-the-required-information-for-the-service-metadata-package"></a>1-收集所需的信息的服务元数据包

当你完成本主题的第 2 步中的服务元数据向导中的步骤，从你想要与设备关联的移动宽带应用项目在 package.appxmanifest 文件中存储的几个部分是信息的必需的。 使用以下步骤，这样就准备好进行本主题的第 2 步收集的信息。

**警告**  
收集在此步骤中的值之前，移动宽带应用程序必须与 Microsoft Store 相关联。 关联时移动宽带应用程序，包清单文件中的值被更新为使用来自 Microsoft Store 开发人员帐户的信息。 但是，移动宽带应用程序没有要发布到 Microsoft Store。 只有在准备好发布服务元数据包，它可以在本地开发环境。



**若要收集 UWP 设备应用程序信息**

1.  通过使用 Visual Studio 2013 中打开移动宽带的应用程序项目。

2.  在右侧窗格中，右键单击**Package.appxmanifest**文件，，然后单击**查看代码**。

3.  从 package.appxmanifest 文件中收集以下属性：

    -   从**标识**元素，**名称**属性将用于**包名称**字段在服务元数据向导。

    -   从**标识**元素，**发布者**属性将用于**发布服务器**字段在服务元数据向导。

    -   从**应用程序**元素， **Id**属性从**应用程序**子元素将用作**应用 ID**字段中服务元数据向导。

4.  关闭 package.appxmanifest 文件。

![代码视图中的 package.appxmanifest 文件](images/mbae-sxs-appxmanifest.png)

你可以完成这而无需使用 Visual Studio 2013 通过执行以下步骤：

**若要收集而无需使用 Visual Studio 2013 的移动宽带的应用程序信息**

1.  导航到移动宽带应用程序的 package.appxmanifest 文件。

2.  右键单击该文件，然后依次**使用打开**。

3.  清除**用于所有.appxmanifest 文件的此应用**复选框，单击**更多选项**，然后单击**记事本**。

4.  从 package.appxmanifest 文件中收集以下属性：

    -   从**标识**元素，**名称**属性将用于**包名称**字段在服务元数据向导。

    -   从**标识**元素，**发布者**属性将用于**发布服务器**字段在服务元数据向导。

    -   从**应用程序**元素， **Id**属性从**应用程序**子元素将用作**应用 ID**字段中服务元数据向导。

5.  保存并关闭 package.appxmanifest 文件。

### <a name="2-create-the-service-metadata-package"></a>2-创建服务元数据包

在 Windows 开发人员中心硬件仪表板中使用服务元数据向导创建服务元数据。

**若要创建服务元数据包**

1.  导航到 <http://sysdev.microsoft.com>。

2.  下**设备元数据**标题下方，单击**创建移动宽带体验**。

    ![这是在仪表板登录页面](images/mbae-sxs81-dashboard.png)

3.  上**服务信息**页上，需要完成以下字段，然后单击**下一步**。

    -   **输入你要使用 Windows 网络选择 UI 中的网络名称**– 网络的名称，将向客户 Windows 连接管理器中显示。

    -   **输入你的服务号码**– 必须匹配你预配的元数据中的运营商 ID 字段的 GUID。 可以通过使用 Visual Studio 2013 创建一个 GUID。 有关如何创建 GUID 的详细信息，请参阅[创建 GUID (guidgen.exe)](https://go.microsoft.com/fwlink/p/?linkid=330070)。

    -   **上传您是要在 Windows 网络选择 UI 中显示的图标**– 单击**浏览**，然后选择向客户 Windows 连接管理器中显示的图标。

    -   **（除非权利检查需要以下可选） 在应用中输入 Windows 通知事件处理程序**– 这是在你的移动宽带应用中已注册通知处理程序。

    -   **若要允许用户共享其移动宽带连接 （个人热点） 吗？** -可能的选项包括**始终允许**，**只能与权利检查 （Windows 通知事件处理程序所需） 允许**，并**永远不会允许**。 默认选项将始终允许。

    -   **是否需要系统管理员权限来执行 PIN 解锁 SIMs 上？** – 如果你希望要求系统管理员权限才能 PIN 解锁 SIM 卡，单击**是**选项。

    ![向导的服务信息步骤](images/mbae-sxs81-serviceinfostep.png)

4.  上**硬件信息**页上，选择应该用于标识您的体验的信息。 选择复选框后，可以添加相应的网络范围。 生成的 ID 应存在于 Windows APN 数据库，所以标识正确的订阅服务器。 APN 数据库有关的详细信息，请参阅[COSA/APN 数据库提交](cosa-apn-database-submission.md)。

    -   如果您使用国际移动订阅服务器上标识 (IMSI) GSM 提供程序，请选择**IMSI**下的复选框**GSM**标题。 在中**提供程序 ID**框中，输入 GSM 服务提供程序 id。 下**IMSI/ICCID 范围**标题下方，输入范围，并单击**添加**。

    -   如果您使用集成电路卡标识符 (ICCID) GSM 提供程序，请选择**SIM ICC ID**下的复选框**GSM**标题。 下**输入提供程序 ID 和 ICC ID 范围**标题下方，输入范围，并单击**添加**。

    -   如果您使用的家庭的提供程序名称的 GSM 提供程序，请选择**主页提供程序名称**下的复选框**GSM**标题。 下**输入主页提供程序名称或输入提供程序 ID （MCC + mnc 是否）** 标题下方，输入的提供程序 ID 和提供程序名称，然后单击**添加**。

    -   如果您使用 SID CDMA 提供程序，请选择**SID**下的复选框**CDMA**标题。 在中**输入 SID**框中，输入 CDMA SID。

    -   如果您使用的提供程序名称的 CDMA 提供程序，请选择**提供程序名称**下的复选框**CDMA**标题。 在中**输入提供程序名称**框中，输入 CDMA 服务提供程序名称。

    -   单击“下一步” 。

    ![这是向导的硬件信息步骤](images/mbae-sxs81-hardwareinfostep.png)

5.  上**应用信息**页上，输入在本主题的步骤 1 中收集的信息。 如果你想要添加其他特权的应用，请单击**添加**，然后输入最多 7 的详细信息。 当输入的所有特权的应用程序时，单击**下一步**。

    ![这是向导的应用程序信息步骤](images/mbae-sxs81-appinfostep.png)

6.  上**确认**页上，验证信息是否正确。 选择**开发人员模式**或**预览模式**选项，并单击**提交**。

    -   **开发人员模式**– 未签名包和它必须手动下载并安装在每台计算机上。 如果需要保存该程序包以进行脱机开发，请使用此选项。

    -   **预览模式**– 签名和从 Microsoft 测试计算机，使用相应的注册表设置配置自动下载包。 预览模式下不会检查以确保移动宽带应用已发布到 Microsoft Store。

    ![这是向导的确认步骤](images/mbae-sxs81-confirm.png)

### <a name="3-insert-the-store-manifest-file-into-the-microsoft-store-device-app"></a>3-插入存储区清单文件到 Microsoft Store 设备应用

应用商店清单文件必须包含 UWP 设备应用。 使用以下步骤从服务元数据包下载应用商店清单文件并将其插入到移动宽带的应用程序项目。

**插入存储区清单文件**

1.  在 Windows 开发人员中心硬件仪表板中，在服务元数据包，管理体验页上单击服务元数据包，然后依次**StoreManifest.xml**若要下载你的应用商店清单文件。

    ![下载应用商店清单文件](images/mbae-sxs81-storemanifest.png)

2.  通过使用 Visual Studio 2013 中打开移动宽带的应用程序项目。

3.  右键单击该项目中，单击**外**，然后单击**现有项**。

4.  浏览到你下载的应用商店清单文件，然后单击**添加**。

5.  重新编译的移动宽带应用并再次将其发布到 Microsoft Store。

### <a name="4-test-the-service-metadata-package"></a>4-测试服务元数据包

若要测试服务元数据包，必须具有移动宽带设备和服务元数据的包文件。 若要配置你的测试系统和安装的服务元数据包的说明取决于包的模式。

### <a name="span-idtestaservicemetadatapackageindevelopermodespanspan-idtestaservicemetadatapackageindevelopermodespanspan-idtestaservicemetadatapackageindevelopermodespantest-a-service-metadata-package-in-developer-mode"></a><span id="Test_a_service_metadata_package_in_developer_mode"></span><span id="test_a_service_metadata_package_in_developer_mode"></span><span id="TEST_A_SERVICE_METADATA_PACKAGE_IN_DEVELOPER_MODE"></span>在开发人员模式下测试服务元数据包

必须手动下载包并将其安装在正确的位置的情况下才能正常工作。 开发人员模式包将需要从两个不同的入口点，具体取决于您编写的新包或现有的包进行访问。

在 Windows 开发人员中心硬件仪表板中创建新包，则单击**管理体验**，然后单击**未关联的开发人员包**(中的第一个条目**管理遇到**表)。 下图显示了一个示例：

![下载你的服务元数据包](images/mbae-sxs81-managedevpackages.png)

如果编辑已与体验相关联的现有服务元数据包，选择从体验**管理体验**表，您将看到在开发人员模式包**元数据包**表。 单击**下载 MBAE Zip 包编辑**下载它。

![下载服务元数据包](images/mbae-sxs81-manageassociatedpackages.png)

已下载服务元数据包后，你必须启用测试签名因为未签名的服务元数据包。 若要启用测试签名，**运行 bcdedit – 上设置 testsigning**从提升的命令提示符，然后重新启动计算机。

启用测试签名后，将复制\*.devicemetadata ms 文件服务元数据包到以下位置： **%programdata%\\Microsoft\\Windows\\DeviceMetadataStore\\** <em>区域性</em>，其中*区域性*是您的计算机的当前区域性代码。

### <a name="span-idtestaservicemetadatapackageinpreviewmodespanspan-idtestaservicemetadatapackageinpreviewmodespanspan-idtestaservicemetadatapackageinpreviewmodespantest-a-service-metadata-package-in-preview-mode"></a><span id="Test_a_service_metadata_package_in_preview_mode"></span><span id="test_a_service_metadata_package_in_preview_mode"></span><span id="TEST_A_SERVICE_METADATA_PACKAGE_IN_PREVIEW_MODE"></span>在预览模式下测试服务元数据包

如果服务元数据包在预览模式下，必须在测试计算机上创建 PreviewKey 注册表项。 有关配置 PreviewKey 注册表项的详细信息，请参阅[创建一个预览包](https://msdn.microsoft.com/library/windows/hardware/br230780)。

**注意**  
无需启用测试签名来测试服务元数据包的处于预览模式。



创建 PreviewKey 注册表项后，插入你的移动宽带设备，确保它显示在网络列表中。 如果未显示，请参阅[故障排除](#troubleshooting)部分，了解详细信息。

### <a name="span-idcleartheexistingservicemetadataspanspan-idcleartheexistingservicemetadataspanspan-idcleartheexistingservicemetadataspanclear-the-existing-service-metadata"></a><span id="Clear_the_existing_service_metadata"></span><span id="clear_the_existing_service_metadata"></span><span id="CLEAR_THE_EXISTING_SERVICE_METADATA"></span>清除现有的服务元数据

在 PC 上安装服务元数据时，在许多不同的位置，其中包括注册表、 元数据缓存、 元数据存储区、 WWAN 配置文件和适用于开发人员节点存储的元数据中包含的值。 这使得很难重复使用相同或不同，元数据包的多个测试。 若要确保服务元数据已正确安装，应清除任何现有的服务元数据。 可以通过设置测试计算机以运行 PowerShell 脚本，删除所有跟踪清除现有的服务元数据。 首先，必须在测试计算机上设置环境：

**注意**  
这将不适用于 Windows RT 设备。 使用中名为"以清除运行 Windows RT 的设备上的服务元数据"的过程的步骤。



**若要设置用于清除服务元数据环境**

1.  下载 psexec.exe (<https://go.microsoft.com/fwlink/p/?linkid=330071>)，并提取到的文件夹。

2.  下载并安装 Windows 驱动程序工具包 Windows 8.1 (<https://go.microsoft.com/fwlink/?LinkId=330072>)。

3.  导航到安装 WDK 文件。 默认位置是**c:\\Program Files (x86)\\Windows 工具包\\8.1\\工具**。 如果测试计算机运行的 x86，复制 devcon.exe 从 x86 到 psexec.exe 所在的文件夹的文件夹。 如果测试计算机运行的 x64，则将 devcon.exe 复制从 x64 文件夹。

4.  将以下脚本保存为 MetadataRemovalScript.ps1 Devcon.exe 和 PsExec.exe 所在的文件夹中。

    **注意**  
    在中**另存为类型**框中，请务必选择**的所有文件 (\*。\*)** 然后保存文件。




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


设置好环境后，运行以下步骤每次想要清除任何现有的服务元数据：

**若要清除的服务元数据**

1.  请确保移动宽带设备插入测试计算机。

2.  从提升的命令提示符，导航到 psexec.exe，解压缩的文件夹，然后运行**psexec /s /i powershell**

3.  在 PowerShell 命令提示符中，导航到解压缩 psexec.exe 的文件夹。

4.  类型**集-executionpolicy unrestricted** ，然后按 Enter。

5.  类型**Y** ，然后输入。

6.  类型 **。\\MetadataRemovalScript.ps1** ，然后按 Enter。

7.  出现提示时，移动宽带设备中删除，然后按 Enter。

8.  你想要清除的服务元数据从测试计算机每的次重复这些步骤。

**若要清除运行 Windows RT 的设备上的服务元数据**

1. 删除软件设备节点。

   1.  在设备管理器中，单击**视图**，然后单击**显示隐藏的设备**。

   2.  展开软件的设备。

   3.  右键单击下面的设备节点，然后依次**卸载**:**Windows.Devices.Sms.SmsDevice**和**Windows.Networking/NetworkOperators.MobileBroadbandAccount**

2. 从所有接口中删除所有的移动宽带配置文件。

   1. 从提升的命令提示符，键入**netsh mbn 显示 pro i =\\***

   2. 对于每个配置文件中，键入**netsh mbn 删除配置文件名称 ="的配置文件名称下面"我 =\\***，然后按 Enter。

3. 禁用所有的移动宽带适配器。

   1.  在设备管理器中，展开**网络适配器**。

   2.  右键单击每个移动宽带设备，然后依次**禁用**。

4. 从提升的命令提示符，停止 DSM 服务通过键入**sc stop dsmsvc** ，然后按 Enter。

5. 正在删除包含在服务元数据包从任何文件夹从设备元数据存储区中删除你的服务元数据包 **%programdata%\\Microsoft\\Windows\\DeviceMetadataStore**. 可以通过查找 MobileBroadbandInfo.xml 文件确定服务元数据包。

6. 删除所有 WWAN SVC MBAE 注册表项。

   1.  在注册表编辑器中，删除以下注册表项及其所有子项：HKEY\_LOCAL\_MACHINE\\Software\\Microsoft\\WwanSvc\\MobileBroadbandAccounts.

   2.  如果你没有删除注册表项的访问权限，必须为自己提供完全控制权限。

7. 启用所有的移动宽带适配器。

   1.  在设备管理器中，展开**网络适配器**。

   2.  右键单击每个移动宽带设备，然后依次**启用**。

### <a name="5-publish-the-service-metadata-package"></a>5-发布服务元数据包

一旦您已确认服务元数据包工作正常，最后一步是发布包。 可以通过选择附加到特定的体验，通过单击包发布包**释放**按钮，如下所示。

![发布服务元数据包](images/mbae-sxs81-releasetolive.jpg)

## <a name="steps-for-editing-a-service-metadata-package"></a>编辑服务元数据包的步骤


可以通过使用 Windows 开发人员中心硬件仪表板的管理体验页编辑服务元数据包。

![管理体验页](images/mbae-sxs81-manageexperience.png)

## <a name="troubleshooting"></a>疑难解答


打开网络列表，查找你的移动宽带网络。 如果使用的名称和服务元数据包中使用的图标列出网络**ServiceInfo.xml**文件，包的正确分析。 如果要更新服务元数据包的具有相同的名称和图标，或如果名称或图标不出现在列表中之后有关大约一分钟，则应执行其他步骤，此处所述：

-   强制执行元数据刷新

-   检查元数据缓存

-   检查注册表

-   检查 WWAN 日志

### <a name="span-idforcemdrefspanspan-idforcemdrefspanforce-a-metadata-refresh"></a><span id="forcemdref"></span><span id="FORCEMDREF"></span>强制执行元数据刷新

元数据和移动宽带应用系统的某些部分依赖于网络访问，这可以失败，并且使计算机处于不一致的状态。 如果发生这种情况，可能会遇到的情况下未安装服务元数据或未安装的移动宽带应用的位置。 系统将定期尝试弥补这种情况，而是省电，重试次数是相当不频繁 （只需几次一天）。 而不是等待下一步的重试，可以手动强制其立即刷新。 要实现这一点，请执行下列操作：

1.  打开桌面**控制面板**。

2.  打开**设备和打印机**。

3.  从**视图**菜单上，单击**刷新**，或按**F5**密钥。 此操作会导致元数据以进行重新解析和后台事件来重新进行注册。

**重要须知**  
如果服务元数据包已成功地分析，系统会将此刷新作为元数据更新。 在这种情况下，元数据包必须具有在其文件名中不同的 GUID 和更新时间戳[LastModifiedDate](lastmodifieddate.md)的元素**PackageInfo.xml**。



### <a name="span-idcheckmdcachespanspan-idcheckmdcachespancheck-the-metadata-cache"></a><span id="checkmdcache"></span><span id="CHECKMDCACHE"></span>检查元数据缓存

如果刷新元数据未解决此问题，请确保服务元数据包有效，并且它具有正确的硬件 Id。 要实现这一点，请执行下列操作：

1. 导航到 **%programdata%\\Microsoft\\Windows\\DeviceMetadataCache\\dmrccache\\**<em>区域性</em>，其中*区域性*是在测试计算机的当前区域性的区域性代码 (例如， **en-我们**或**es es**)。

2. 查找与您的元数据的包同名的文件夹 (而无需 **.devicemetadata ms**扩展)。 如果此目录不存在，并可以表示四个操作之一：

   -   服务元数据包已损坏。

   -   服务元数据包不具有正确的硬件 Id。

   -   移动宽带设备处于的状态可以下载元数据，或者复制服务元数据包前插入的设备中。

   -   检查元数据包的数字签名时出现问题。 这通常被由于无测试签名在测试计算机上启用。

如果不确定包损坏和，您第一次插入移动宽带设备中复制的服务元数据包后，检查 IMSI 范围。 它是很容易过多或太少 0 秒或 9 中的类型。 如果问题仍然存在确认或更正这些项后，您必须查看注册表。

### <a name="span-idcheckregspanspan-idcheckregspancheck-the-registry"></a><span id="checkreg"></span><span id="CHECKREG"></span>检查注册表

**警告**  
不应编辑不属于你的应用程序除非绝对必要的注册表数据。 如果在注册表中没有错误，您的系统可能不能正常工作。 不，在任何情况下，删除**MobileBroadbandAccounts**注册表项。 Windows 不会重新创建它，并将中断功能。



执行以下步骤来检查注册表：

1.  打开注册表编辑器。

2.  转到**HKLM\\软件\\Microsoft\\WwanSvc\\MobileBroadbandAccounts**。

3.  在此注册表项，查找三个其他键：**帐户**， **NetworkInterfaceBindings**，和**数据**。 这些密钥不存在默认设置。移动宽带设备是插入、 打开，或连接，它们会自动创建第一次。

4.  如果**帐户**或**NetworkInterfaceBindings**密钥不存在并且具有已接通电源或开启你的移动宽带卡，检查 WWAN 日志。

5.  如果某些或所有这些注册表项存在，依次展开**帐户**中的键**树**视图。 一个或多个注册表项的名称类似于 Guid 应存在于其内部。 注册表树条目应类似于注册表树中，如下所示：

    ![已分析的帐户的注册表项](images/fig2-registryentries-for-parsedmobilebroadbandaccount.png)

    如果注册表项看起来类似于上图中 （值名称将略有不同具体取决于该帐户是否 GSM 或 CDMA 网络上），并且如果您看不到网络列表中的图标，您应查看事件日志。

    如果注册表项类似于下图，则意味着移动宽带卡已插入之前服务元数据包复制到设备的元数据存储区中，服务元数据包已损坏或硬件 Id 不正确. 若要更正您接通电源或之前将元数据的包复制到的元数据存储在设备上打开的情况下，执行强制刷新元数据中的步骤。 否则，请按照检查 WWAN 日志中的步骤。

    ![未分析的帐户的注册表项](images/fig1-registryentries-for-unparsedmobilebroadbandaccount.png)

### <a name="span-idcheckwwanlogsspanspan-idcheckwwanlogsspancheck-the-wwan-logs"></a><span id="checkwwanlogs"></span><span id="CHECKWWANLOGS"></span>检查 WWAN 日志

如果有任何**帐户**或**NetworkInterfaceBindings**注册表项下**HKLM\\软件\\Microsoft\\WwanSvc\\MobileBroadbandAccounts**，或如果未完全填充的条目，您必须查看 WWAN 日志。 以下步骤将重置到已知状态计算机：

1.  拔出或关闭你的移动宽带设备 (如果嵌入设备时，将其中禁用**设备管理器**)。

2.  删除以下注册表项：

    -   **HKLM\\SOFTWARE\\Microsoft\\WwanSvc\\MobileBroadbandAccounts\\Accounts**

    -   **HKLM\\SOFTWARE\\Microsoft\\WwanSvc\\MobileBroadbandAccounts\\NetworkInterfaceBindings**

    **警告**  
    不，在任何情况下，删除**HKLM\\软件\\Microsoft\\WwanSvc\\MobileBroadbandAccounts\\** 注册表项。 Windows 不会重新创建它，并将中断功能。



有两种类型的日志中的感兴趣的项： 管理 WWAN 服务条目日志条目和分析器任务项的帐户。 第一种类型可帮助调试问题引起的网络硬件的问题和第二个类型可以帮助调试元数据分析问题。

帐户管理 WWAN 服务条目的日志项已成功处理的网络是类似于下面：

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

搜索的日志可以找到这些条目**帐户管理**。 在这种情况下，最重要的条目都**数据存储创建/更新启动**并**数据存储创建/更新已完成的**。 如果这些条目存在，并且没有错误的消息，硬件行为正确。 （称为此处包含的注册表项中所述的数据存储区检查注册表）。

与此相反，在其中删除 SIM 的设备上的条目通常的外观如下所示：

```syntax
[0]02CC.03E4::‎2012‎-‎01‎-‎04 09:29:50.309 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Account updater started for network interface {7a0a0dce-0a51-471a-8c16-6e767cd0b861}. 
[0]02CC.03E4::‎2012‎-‎01‎-‎04 09:29:50.309 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Detected removal of SIM from device bound to network interface {7A0A0DCE-0A51-471A-8C16-6E767CD0B861}. 
[0]02CC.03E4::‎2012‎-‎01‎-‎04 09:29:50.309 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Devnode create/update started. 
[0]02CC.03E4::‎2012‎-‎01‎-‎04 09:29:50.309 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Devnode create/update finished. 
[0]02CC.03E4::‎2012‎-‎01‎-‎04 09:29:50.309 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Account updater finished for network interface {7a0a0dce-0a51-471a-8c16-6e767cd0b861}. 
```

**注意**  
在后一种示例中，没有为项**数据存储创建/更新启动**或**数据存储创建/更新已完成的**。 由于信息存储在 SIM 中的帐户管理过程的关键，没有 SIM 的设备没有必需的关联元数据。



如果硬件已成功处理，但你的徽标或名称未显示在网络列表中，可能有元数据程序包有问题。 这可以通过在日志中使用的分析器任务项调查。 若要查找这些条目，请搜索**分析器任务**。 为成功分析日志项通常如下所示：

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

这些日志显示**MobileBroadbandInfo.xml**文件已正确解析的分析器任务应用 WWAN 配置文件 （以及的 WWAN 服务日志记录已成功更新配置文件），并且分析器任务设置受信任的预配证书中所述**MobileBroadbandInfo.xml**。

如果过程的任何部分失败，则记录该故障。 例如，如果数字签名检查失败的服务提供程序图标文件上，日志条目通常看起来如下所示：

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

因为它是正常的分析器任务运行一次，可能会看到多个集的`[Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]`日志条目。 在这种情况下，组条目通常都是相同-如果它们不相同，则可以表示间歇性的问题。

## <a name="span-idadditionalresourcesspanspan-idadditionalresourcesspanspan-idadditionalresourcesspanadditional-resources"></a><span id="Additional_resources"></span><span id="additional_resources"></span><span id="ADDITIONAL_RESOURCES"></span>其他资源


使用以下链接详细了解 Windows 8.1 和 Windows 10 中的移动宽带：

-   [移动宽带概述](overview-of-mobile-broadband.md)

-   [APN 数据库概述](apn-database-overview.md)

-   [服务元数据](service-metadata.md)









