---
title: 创建服务元数据的开发人员指南
description: 创建服务元数据的开发人员指南
ms.assetid: 2d250bce-2dd2-4bd8-aa0f-432dde7783e1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92c9b6b6a78d7aa7724127fd15b1e26af7a725db
ms.sourcegitcommit: 7e4d9508198a30bdc1cb6eda83852dda4e42213e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89304290"
---
# <a name="developer-guide-for-creating-service-metadata"></a>创建服务元数据的开发人员指南

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]


本指南将指导你完成在 Windows 开发人员中心硬件仪表板上创建服务元数据包的过程，以前称为 Sysdev (<https://sysdev.microsoft.com>) 。 将移动宽带应用连接到硬件设备需要服务元数据。 当用户将移动宽带设备插入到计算机时，将下载关联的服务元数据，然后自动下载移动宽带应用。

您可以利用服务元数据来创建更深入的 Windows 体验。 利用服务元数据包，可以包括图标和操作员名称等品牌信息，配置用于访问 SIM 硬件和个人热点的设置和权限，以及预配移动宽带应用以使用移动宽带设备。

**注意**  
即使移动宽带应用自动安装，用户也必须手动将其固定到 "开始" 屏幕。



## <a name="span-idgetting_startedspanspan-idgetting_startedspanspan-idgetting_startedspangetting-started"></a><span id="Getting_started"></span><span id="getting_started"></span><span id="GETTING_STARTED"></span>入门


若要创建成功的服务元数据包，必须完成本部分中包含的步骤。

### <a name="span-idregister_your_company_with_the_windows_dev_center_hardware_dashboardspanspan-idregister_your_company_with_the_windows_dev_center_hardware_dashboardspanspan-idregister_your_company_with_the_windows_dev_center_hardware_dashboardspanregister-your-company-with-the-windows-dev-center-hardware-dashboard"></a><span id="Register_your_company_with_the_Windows_Dev_Center_hardware_dashboard"></span><span id="register_your_company_with_the_windows_dev_center_hardware_dashboard"></span><span id="REGISTER_YOUR_COMPANY_WITH_THE_WINDOWS_DEV_CENTER_HARDWARE_DASHBOARD"></span>向 Windows 开发人员中心硬件仪表板注册公司

-   你的公司在 Windows 开发人员中心硬件仪表板上有一个活动帐户。 如果你的公司在 Windows 开发人员中心硬件仪表板上没有帐户，你可以创建一个新帐户，并将你的用户帐户添加到你的公司。 有关详细信息，请参阅 Windows 开发人员中心硬件仪表板帮助中的 [管理](/windows-hardware/drivers/dashboard/dashboard-administration) 。

-   你的公司有一个 VeriSign 代码签名证书，用于对包进行签名。

### <a name="span-idservice_metadata_wizard_access_and_service_identifiers_registrationspanspan-idservice_metadata_wizard_access_and_service_identifiers_registrationspanspan-idservice_metadata_wizard_access_and_service_identifiers_registrationspanservice-metadata-wizard-access-and-service-identifiers-registration"></a><span id="Service_Metadata_wizard_access_and_service_identifiers_registration"></span><span id="service_metadata_wizard_access_and_service_identifiers_registration"></span><span id="SERVICE_METADATA_WIZARD_ACCESS_AND_SERVICE_IDENTIFIERS_REGISTRATION"></span>服务元数据向导访问和服务标识符注册

在创建服务元数据包之前，Mno 和 Mvno 必须完成以下步骤：

-   请求访问服务元数据向导

-   注册服务标识符

若要完成上述步骤，你必须向发送电子邮件， sysdev@microsoft.com 其中包含以下信息：

-   注册 Windows 开发人员中心硬件仪表板时使用的组织名称。

-   你是移动网络操作员还是移动虚拟网络操作员。

-   你的网站，并论证你需要创建服务元数据包的原因。

包括以下服务标识符（如果适用）：

-   GSM 提供程序 Id 列表

-   GSM 提供程序名称列表

-   CDMA Sid 列表

-   CDMA 提供程序名称的列表

你应收到一封确认电子邮件，其中包含你的请求收到的24小时。 不过，处理请求最多可能需要5个工作日。 如果有冲突，我们将向你发送一封电子邮件，要求提供更多信息。

### <a name="span-idmobile_broadband_appspanspan-idmobile_broadband_appspanspan-idmobile_broadband_appspanmobile-broadband-app"></a><span id="Mobile_broadband_app"></span><span id="mobile_broadband_app"></span><span id="MOBILE_BROADBAND_APP"></span>移动宽带应用

在创建服务元数据包之前，请确保已开发移动宽带应用并将其与 Microsoft Store 相关联。 此应用应提供重要的体验，如计划购买、数据使用、帮助和支持，以及从操作员突出显示增值服务。 有关创建移动宽带应用的详细信息，请参阅以下链接：

-   [移动宽带 WinRT API 概述](list-of-mobile-broadband-windows-runtime-apis.md)

-   [移动运营商硬件概述](mobile-operator-hardware-overview.md)

-   [UWP 移动宽带应用](uwp-mobile-broadband-apps.md)

**注意**  
在对服务元数据进行测试并准备好在外部发布之前，移动宽带应用不必发布到 Microsoft Store。 建议仅在服务元数据包经过预览模式测试后才将应用发布到 Microsoft Store。



## <a name="span-idcreating_service_metadata_packagesspanspan-idcreating_service_metadata_packagesspanspan-idcreating_service_metadata_packagesspancreating-service-metadata-packages"></a><span id="Creating_service_metadata_packages"></span><span id="creating_service_metadata_packages"></span><span id="CREATING_SERVICE_METADATA_PACKAGES"></span>创建服务元数据包


从 Windows 开发人员中心硬件仪表板上提供的服务元数据向导开始创建服务元数据包。 有关服务元数据向导的详细信息，请参阅 [步骤 2-创建服务元数据包](#2-create-the-service-metadata-package)。 您可以使用服务元数据向导来创建新的或编辑现有的服务元数据包。 当你完成向导并填写值时，向导将验证并通知你任何错误或警告。 此验证包括检查缺失或不正确的字段、服务标识符所有权、移动宽带应用是否存在于 Microsoft Store 中，等等。

当你在最后确认页面并准备好提交时，你可以选择以 **开发人员** 模式或 **预览** 模式提交包。

-   **开发人员模式** 在初始阶段中使用，目的是只创建服务元数据包，并将其用于脱机测试目的。 在此模式下，将不会对包进行签名，必须手动将其下载并安装到测试计算机中，以便进行验证。 可以快速快速地查看此模式，以便创建和验证服务元数据包与设备一起工作。

-   **预览模式** 当你确信包已正确编写并且已准备好进行端到端测试时使用。 在此模式下，如果正确设置了测试计算机，则 Windows 开发人员中心硬件仪表板会对包进行签名，并将自动下载到测试计算机。

完成了预览测试并验证了包适用于所有方案后，便可以将包发布到 live。

下图对工作流进行了讨论：

![创建服务元数据包](images/mbae-sxs81-createpackageworkflow.png)

若要创建新的服务元数据包，请参阅 [创建服务元数据包的步骤](#steps-for-creating-a-service-metadata-package)。

若要编辑现有的服务元数据包，请参阅 [编辑服务元数据包的步骤](#steps-for-editing-a-service-metadata-package)。

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

2.  在右侧窗格中，右键单击 **appxmanifest.xml** 文件，然后单击 " **查看代码**"。

3.  从 appxmanifest.xml 文件中收集以下属性：

    -   在 **Identity** 元素中，" **名称** " 属性将用于 "服务元数据" 向导中的 " **包名称** " 字段。

    -   在 " **标识** " 元素中，" **发布服务器** " 属性将用于 "服务元数据" 向导中的 " **发布者** " 字段。

    -   在**应用程序**元素中，**应用程序**子元素的**Id**属性将用于 "服务元数据" 向导中的 "**应用 Id** " 字段。

4.  关闭 appxmanifest.xml 文件。

![代码视图中的 appxmanifest.xml 文件](images/mbae-sxs-appxmanifest.png)

你还可以通过执行以下步骤来完成此操作，而无需使用 Visual Studio 2013：

**在不使用 Visual Studio 2013 的情况下收集移动宽带应用信息**

1.  导航到移动宽带应用的 appxmanifest.xml 文件。

2.  右键单击该文件，然后单击 " **打开方式**"。

3.  清除 " **对所有 appxmanifest.xml 文件使用此应用程序** " 复选框，单击 " **更多选项**"，然后单击 " **记事本**"。

4.  从 appxmanifest.xml 文件中收集以下属性：

    -   在 **Identity** 元素中，" **名称** " 属性将用于 "服务元数据" 向导中的 " **包名称** " 字段。

    -   在 " **标识** " 元素中，" **发布服务器** " 属性将用于 "服务元数据" 向导中的 " **发布者** " 字段。

    -   在**应用程序**元素中，**应用程序**子元素的**Id**属性将用于 "服务元数据" 向导中的 "**应用 Id** " 字段。

5.  保存并关闭 appxmanifest.xml 文件。

### <a name="2-create-the-service-metadata-package"></a>2-创建服务元数据包

服务元数据是通过使用 Windows 开发人员中心硬件仪表板中的服务元数据向导创建的。

**创建服务元数据包**

1.  导航到 <https://sysdev.microsoft.com>。

2.  在 **设备元数据** 标题下，单击 " **创建移动宽带体验**"。

    ![这是仪表板的登录页](images/mbae-sxs81-dashboard.png)

3.  在 " **服务信息** " 页上，填写以下字段，然后单击 " **下一步**"。

    -   **输入用于 windows 网络选择 UI 的网络名称** –将在 Windows 连接管理器中向客户显示的网络的名称。

    -   **输入服务号码** –必须与预配元数据中的 "运营商 ID" 字段匹配的 GUID。 可以通过使用 Visual Studio 2013 来创建 GUID。 有关如何创建 GUID 的详细信息，请参阅 [CREATE guid ( # A0) ](https://go.microsoft.com/fwlink/p/?linkid=330070)。

    -   **上传要在 windows 网络选择 UI 中显示的图标** –单击 " **浏览**"，然后选择向 Windows 连接管理器中的客户显示的图标。

    -   **在应用中输入 Windows 通知事件处理程序 (可选，除非) 下面需要权利检查 ** –这是在移动宽带应用中注册的通知处理程序。

    -   **是否允许用户共享其移动宽带连接 (个人热点) ？** –可能的选项始终为 " **允许**"， **只允许与 " (Windows 通知事件处理程序" 权限检查) **和 " **不允许**"。 默认选项为 "始终允许"。

    -   **是否需要系统管理员权限才能在 Sim 上执行 PIN 解锁？** –如果你希望需要系统管理员特权来锁定 SIM 卡，请单击 **"是"** 选项。

    ![向导的服务信息步骤](images/mbae-sxs81-serviceinfostep.png)

4.  在 " **硬件信息** " 页上，选择应该用于识别你的体验的信息。 选中某个复选框后，可以添加相应的网络范围。 生成的 ID 应该存在于 Windows APN 数据库中，以便标识正确的订阅服务器。 有关 APN 数据库的详细信息，请参阅 [COSA/APN 数据库提交](planning-your-desktop-cosa-apn-database-submission.md)。

    -   如果你是使用国际化 Mobile 订户身份 (IMSI) 的 GSM 提供商，请在 " **GSM** " 标题下选择 " **IMSI** " 复选框。 在 " **提供程序 id** " 框中，输入 GSM 服务提供程序 id。 在 **IMSI/ICCID 范围** 标题下，输入范围，然后单击 " **添加**"。

    -   如果你是使用集成卡标识符 (ICCID) 的 GSM 提供程序，请选中 " **GSM** " 标题下的 " **SIM ICC ID** " 复选框。 在 " **输入提供程序 id 和 ICC id 范围** " 标题下，输入范围，然后单击 " **添加**"。

    -   如果你是使用 home 提供程序名称的 GSM 提供程序，请选中 " **GSM** " 标题下的 "**主提供商名称**" 复选框。 在 " **输入主提供程序名称" 或输入提供程序 id (MCC + MNC) ** "标题中，输入提供程序 id 和提供程序名称，然后单击" **添加**"。

    -   如果你是使用 SID 的 CDMA 提供程序，请选中 " **CDMA** " 标题下的 " **SID** " 复选框。 在 " **输入 sid** " 框中，输入 CDMA SID。

    -   如果你是使用提供程序名称的 CDMA 提供程序，请选中 " **CDMA** " 标题下的 "**提供程序名称**" 复选框。 在 " **输入提供者名称** " 框中，输入 CDMA 服务提供商名称。

    -   单击“配置目录分区”  。

    ![这是向导的 "硬件信息" 步骤](images/mbae-sxs81-hardwareinfostep.png)

5.  在 " **应用程序信息** " 页上，输入在本主题的步骤1中收集的信息。 如果要添加其他特权应用，请单击 " **添加**"，然后输入最多7个其他应用。 输入所有特权应用后，单击 " **下一步**"。

    ![这是向导的 "应用信息" 步骤](images/mbae-sxs81-appinfostep.png)

6.  在 " **确认** " 页上，验证信息是否正确。 选择 " **开发人员模式** " 或 " **预览模式** " 选项，然后单击 " **提交**"。

    -   **开发人员模式** –包未签名，并且必须在每台计算机上手动下载和安装。 如果需要保存该程序包以进行脱机开发，请使用此选项。

    -   **预览模式** –包经过签名，并自动从 Microsoft 下载，以测试配置了适当注册表设置的计算机。 预览模式不会进行检查以确保将移动宽带应用程序发布到 Microsoft Store。

    ![这是向导的 "确认" 步骤](images/mbae-sxs81-confirm.png)

### <a name="3-insert-the-store-manifest-file-into-the-microsoft-store-device-app"></a>3-将商店清单文件插入 Microsoft Store 设备应用

应用商店清单文件必须包含在 UWP 设备应用中。 使用以下步骤从服务元数据包下载应用商店清单文件，并将其插入移动宽带应用项目中。

**插入存储清单文件**

1.  在 Windows 开发人员中心硬件仪表板上，在服务元数据包的 "管理体验" 页上，单击服务元数据包，然后单击 " **StoreManifest.xml** " 下载应用商店清单文件。

    ![下载应用商店清单文件](images/mbae-sxs81-storemanifest.png)

2.  使用 Visual Studio 2013 打开移动宽带应用程序项目。

3.  右键单击该项目，单击 " **添加**"，然后单击 " **现有项**"。

4.  浏览到下载的应用商店清单文件，然后单击 " **添加**"。

5.  重新编译移动宽带应用并再次将其发布到 Microsoft Store。

### <a name="4-test-the-service-metadata-package"></a>4-测试服务元数据包

若要测试服务元数据包，必须有移动宽带设备和服务元数据包文件。 配置测试系统和安装服务元数据包的说明取决于包的模式。

### <a name="span-idtest_a_service_metadata_package_in_developer_modespanspan-idtest_a_service_metadata_package_in_developer_modespanspan-idtest_a_service_metadata_package_in_developer_modespantest-a-service-metadata-package-in-developer-mode"></a><span id="Test_a_service_metadata_package_in_developer_mode"></span><span id="test_a_service_metadata_package_in_developer_mode"></span><span id="TEST_A_SERVICE_METADATA_PACKAGE_IN_DEVELOPER_MODE"></span>在开发人员模式下测试服务元数据包

您必须手动下载包并将其安装在正确的位置，以使方案正常工作。 需要从两个不同的入口点访问开发人员模式包，具体取决于你是创作新包还是现有包。

如果创建了新的包，请在 Windows 开发人员中心硬件仪表板中 **，单击 "** **管理体验**"，然后单击 " (**管理体验**表) 中的第一个条目。 以下代码展示了一个示例：

![下载服务元数据包](images/mbae-sxs81-managedevpackages.png)

如果你编辑了已与某个经验关联的现有服务元数据包，请从 " **管理体验** " 表中选择该体验，然后你将在 " **元包** " 表中看到 "开发人员模式" 包。 单击 " **下载 MBAE Zip 包编辑** " 以下载它。

![下载服务元数据包](images/mbae-sxs81-manageassociatedpackages.png)

下载服务元数据包后，必须启用测试签名，因为服务元数据包未签名。 若要启用测试签名，请 **运行 bcdedit –** 从提升的命令提示符中设置 testsigning，然后重新启动计算机。

启用测试签名后，将 \* devicemetadata-ms 文件从服务元数据包复制到以下位置： **% ProgramData% \\ Microsoft \\ Windows \\ DeviceMetadataStore \\ **<em>区域性</em>，其中*culture*是计算机的当前区域性代码。

### <a name="span-idtest_a_service_metadata_package_in_preview_modespanspan-idtest_a_service_metadata_package_in_preview_modespanspan-idtest_a_service_metadata_package_in_preview_modespantest-a-service-metadata-package-in-preview-mode"></a><span id="Test_a_service_metadata_package_in_preview_mode"></span><span id="test_a_service_metadata_package_in_preview_mode"></span><span id="TEST_A_SERVICE_METADATA_PACKAGE_IN_PREVIEW_MODE"></span>在预览模式下测试服务元数据包

如果服务元数据包处于预览模式，则必须在测试计算机上创建 PreviewKey 注册表项。 有关配置 PreviewKey 注册表项的详细信息，请参阅 [创建预览包](../dashboard/index.yml)。

**注意**  
您无需启用测试签名来测试处于预览模式下的服务元数据包。



创建 PreviewKey 注册表项后，请插入移动宽带设备，并确保它显示在 "网络" 列表中。 如果没有，请参阅 [故障排除](#troubleshooting) 部分了解详细信息。

### <a name="span-idclear_the_existing_service_metadataspanspan-idclear_the_existing_service_metadataspanspan-idclear_the_existing_service_metadataspanclear-the-existing-service-metadata"></a><span id="Clear_the_existing_service_metadata"></span><span id="clear_the_existing_service_metadata"></span><span id="CLEAR_THE_EXISTING_SERVICE_METADATA"></span>清除现有的服务元数据

在 PC 上安装服务元数据时，元数据中包含的值将存储在多个不同的位置，包括注册表、元数据缓存、元数据存储、WWAN 配置文件和开发节点。 这会使重复多个具有相同或不同元数据包的测试变得很困难。 若要确保正确安装服务元数据，应清除任何现有的服务元数据。 可以通过设置测试计算机来运行删除所有跟踪的 PowerShell 脚本，从而清除现有的服务元数据。 首先，必须在测试计算机上设置环境：

**注意**  
这在 Windows RT 设备上不起作用。 使用名为 "在运行 Windows RT 的设备上清除服务元数据" 过程中的步骤。



**设置用于清除服务元数据的环境**

1.  下载 psexec.exe (<https://go.microsoft.com/fwlink/p/?linkid=330071>) ，然后将其解压缩到文件夹。

2.  下载并安装 Windows 驱动程序工具包 Windows 8.1 (<https://go.microsoft.com/fwlink/?LinkId=330072>) 。

3.  导航到 WDK 文件的安装位置。 默认位置为 **C： \\ Program Files (x86) \\ Windows 工具包 \\ 8.1 \\ 工具**。 如果测试计算机运行的是 x86，请将 x86 文件夹 devcon.exe 复制到 psexec.exe 所在的文件夹中。 如果测试计算机运行的是 x64，则从 x64 文件夹中复制 devcon.exe。

4.  将以下脚本作为 MetadataRemovalScript.ps1 保存在与 Devcon.exe 和 PsExec.exe 相同的文件夹中。

    **注意**  
    在 " **保存类型** " 框中，请确保选择 " **所有文件" (" \* \*) ** 保存文件。




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

2.  在提升的命令提示符下，导航到 psexec.exe 提取的文件夹，然后运行 **psexec/s/i powershell**

3.  在 PowerShell 命令提示符中，导航到在其中提取 psexec.exe 的文件夹。

4.  键入 **set-executionpolicy 无限制** ，然后按 enter。

5.  键入 **Y** ，然后输入。

6.  键入 **. \\MetadataRemovalScript.ps1** ，然后按 enter。

7.  出现提示时，请删除移动宽带设备，然后按 Enter。

8.  每次要从测试计算机中清除服务元数据时，请重复这些步骤。

**在运行 Windows RT 的设备上清除服务元数据**

1. 删除 "软件设备" 节点。

   1.  在设备管理器中，单击 " **查看**"，然后单击 " **显示隐藏的设备**"。

   2.  展开 "软件设备"。

   3.  右键单击以下设备节点，然后单击 " **卸载**： **SmsDevice** " 和 " **windows.networking.networkoperators"。 MobileBroadbandAccount**

2. 从所有接口删除所有移动宽带配置文件。

   1. 在提升的命令提示符处，键入**netsh mbn sho pro i \\ =***

   2. 对于每个配置文件，键入**netsh mbn delete profile name = "此处的配置文件名" i = \\ ***，然后按 enter。

3. 禁用所有移动宽带适配器。

   1.  在设备管理器中，展开 " **网络适配器**"。

   2.  右键单击每个移动宽带设备，然后单击 " **禁用**"。

4. 在提升的命令提示符下，通过键入 **sc stop dsmsvc** 停止 DSM 服务，然后按 enter。

5. 通过从 **% ProgramData% \\ Microsoft \\ Windows \\ DeviceMetadataStore**中删除包含服务元数据包的任何文件夹，从设备元数据存储中删除服务元数据包。 您可以通过查找 MobileBroadbandInfo.xml 文件来标识服务元数据包。

6. 删除所有 WWAN SVC MBAE 注册表项。

   1.  在注册表编辑器中，删除以下注册表项和所有子项： HKEY \_ LOCAL \_ MACHINE \\ Software \\ Microsoft \\ WwanSvc \\ MobileBroadbandAccounts。

   2.  如果没有删除注册表项的权限，则必须为自己授予完全控制权限。

7. 启用所有移动宽带适配器。

   1.  在设备管理器中，展开 " **网络适配器**"。

   2.  右键单击每个移动宽带设备，然后单击 " **启用**"。

### <a name="5-publish-the-service-metadata-package"></a>5-发布服务元数据包

确认服务元数据包正确工作后，最后一步是发布包。 可以通过单击 " **发布** " 按钮选择附加到特定体验的包来释放包，如下所示。

![发布服务元数据包](images/mbae-sxs81-releasetolive.jpg)

## <a name="steps-for-editing-a-service-metadata-package"></a>编辑服务元数据包的步骤


可以使用 Windows 开发人员中心硬件仪表板的 "管理体验" 页来编辑服务元数据包。

!["管理体验" 页](images/mbae-sxs81-manageexperience.png)

## <a name="troubleshooting"></a>疑难解答


打开 "网络" 列表，并查找移动宽带网络。 如果使用服务元数据包 **ServiceInfo.xml** 文件中使用的名称和图标列出了网络，则会正确分析包。 如果要更新的服务元数据包具有相同的名称和图标，或者在大约一分钟后名称或图标未显示在列表中，则应执行其他步骤，如此处所述：

-   强制执行元数据刷新

-   检查元数据缓存

-   检查注册表

-   检查 WWAN 日志

### <a name="span-idforcemdrefspanspan-idforcemdrefspanforce-a-metadata-refresh"></a><span id="forcemdref"></span><span id="FORCEMDREF"></span>强制执行元数据刷新

某些部分的元数据和移动宽带应用系统依赖于网络访问，这可能会失败并使计算机处于不一致的状态。 如果发生这种情况，则可能会遇到以下情况：未安装服务元数据，或者未安装移动宽带应用。 系统会定期尝试纠正这种情况，但为了节省电源，重试会在一天) 只 (几次。 你可以手动强制进行刷新，而不是等待下一次重试。 为此，请执行下列步骤：

1.  打开 "桌面 **控制面板"**。

2.  打开 " **设备和打印机**"。

3.  从 " **视图** " 菜单上，单击 " **刷新**"，或按 **F5** 键。 此操作会导致元数据被重新分析，并重新注册后台事件。

重要说明  
如果已成功分析服务元数据包，系统会将此刷新视为元数据更新。 在这种情况下，元数据包的文件名中必须有不同的 GUID，并在**PackageInfo.xml**的[LastModifiedDate](lastmodifieddate.md)元素中包含更新的时间戳。



### <a name="span-idcheckmdcachespanspan-idcheckmdcachespancheck-the-metadata-cache"></a><span id="checkmdcache"></span><span id="CHECKMDCACHE"></span>检查元数据缓存

如果元数据刷新未解决此问题，请确保服务元数据包有效并且具有正确的硬件 Id。 为此，请执行下列步骤：

1. 导航到 **% programdata% \\ Microsoft \\ Windows \\ DeviceMetadataCache \\ dmrccache \\ **<em>culture</em>，其中*culture*是测试计算机的当前区域性的区域性代码 (例如， **en-us**或**es**) 。

2. 查找与元数据包名称相同的文件夹， (没有 **. devicemetadata-ms** extension) 。 如果此目录不存在，则可能表示以下四种情况之一：

   -   服务元数据包已损坏。

   -   服务元数据包没有正确的硬件 Id。

   -   移动宽带设备未处于可下载元数据的状态，或者在复制服务元数据包之前插入设备。

   -   检查元数据包上的数字签名时出现问题。 这通常是由于未在测试计算机上启用测试签名导致的。

如果在复制服务元数据包后确定包未损坏并且第一次插入移动宽带设备，请检查 IMSI 范围。 键入太多或太少的0或9非常简单。 如果确认或更正这些项后问题仍然存在，则必须查看注册表。

### <a name="span-idcheckregspanspan-idcheckregspancheck-the-registry"></a><span id="checkreg"></span><span id="CHECKREG"></span>检查注册表

**警告**  
除非绝对必要，否则不应编辑不属于应用程序的注册表数据。 如果注册表中存在错误，则系统可能无法正常运行。 请勿在任何情况下都删除 **MobileBroadbandAccounts** 注册表项。 Windows 不会重新创建它，并且你将中断此功能。



执行以下步骤以检查注册表：

1.  打开注册表编辑器。

2.  请参阅 **Hklm\ \\ SOFTWARE \\ Microsoft \\ WwanSvc \\ MobileBroadbandAccounts**。

3.  在此注册表项中，查找其他三个密钥： " **帐户**"、" **NetworkInterfaceBindings**" 和 " **数据**"。 默认情况下，这些项不存在;它们是在移动宽带设备首次插入、打开或连接时自动创建的。

4.  如果 **帐户** 或 **NetworkInterfaceBindings** 密钥不存在，并且已插入或打开移动宽带适配器，请检查 WWAN 日志。

5.  如果其中的部分或全部项存在，请在**树**视图中展开 "**帐户**" 键。 其中的一个或多个注册表项的名称与 Guid 类似。 注册表树项应类似于如下所示的注册表树：

    ![已分析帐户的注册表项](images/fig2-registryentries-for-parsedmobilebroadbandaccount.png)

    如果注册表项类似于上图， (值名称将略有不同，具体取决于该帐户是位于 GSM 还是 CDMA 网络) 上，并且如果在 "网络" 列表中看不到该图标，应查看事件日志。

    如果注册表项类似于下图，则意味着移动宽带适配器是在将服务元数据包复制到设备元数据存储区之前插入的，服务元数据包损坏或硬件 Id 不正确。 若要解决在将元数据包复制到元数据存储区之前插入或打开设备的情况，请执行强制执行元数据刷新中的步骤。 否则，请按照检查 WWAN 日志中的步骤进行操作。

    ![未分析帐户的注册表项](images/fig1-registryentries-for-unparsedmobilebroadbandaccount.png)

### <a name="span-idcheckwwanlogsspanspan-idcheckwwanlogsspancheck-the-wwan-logs"></a><span id="checkwwanlogs"></span><span id="CHECKWWANLOGS"></span>检查 WWAN 日志

如果**HKLM \\ SOFTWARE \\ Microsoft \\ WwanSvc \\ MobileBroadbandAccounts**下没有**帐户**或**NetworkInterfaceBindings**注册表项，或者如果有未完全填充的条目，则必须查看 WWAN 日志。 以下步骤会将计算机重置为已知状态：

1.  拔下或关闭移动宽带设备 (如果嵌入了设备，请在 **设备管理器**) 中禁用它。

2.  删除以下注册表项：

    -   **HKLM \\ SOFTWARE \\ Microsoft \\ WwanSvc \\ MobileBroadbandAccounts \\ 帐户**

    -   **HKLM \\ SOFTWARE \\ Microsoft \\ WwanSvc \\ MobileBroadbandAccounts \\ NetworkInterfaceBindings**

    **警告**  
    请勿在任何情况下删除**HKLM \\ SOFTWARE \\ Microsoft \\ WwanSvc \\ MobileBroadbandAccounts \\ **注册表项。 Windows 不会重新创建它，并且你将中断此功能。



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

可以通过在日志中搜索 **帐户管理**来查找这些条目。 在这种情况下，最重要的项是 **数据存储创建/更新已开始** ，并且 **数据存储创建/更新已完成**。 如果这些条目存在并且没有错误消息，则硬件的行为正常。  (引用的数据存储包含 "检查注册表" 中讨论的注册表项。 ) 

与此相反，在删除 SIM 的设备上，条目通常如下所示：

```syntax
[0]02CC.03E4::‎2012‎-‎01‎-‎04 09:29:50.309 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Account updater started for network interface {7a0a0dce-0a51-471a-8c16-6e767cd0b861}. 
[0]02CC.03E4::‎2012‎-‎01‎-‎04 09:29:50.309 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Detected removal of SIM from device bound to network interface {7A0A0DCE-0A51-471A-8C16-6E767CD0B861}. 
[0]02CC.03E4::‎2012‎-‎01‎-‎04 09:29:50.309 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Devnode create/update started. 
[0]02CC.03E4::‎2012‎-‎01‎-‎04 09:29:50.309 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Devnode create/update finished. 
[0]02CC.03E4::‎2012‎-‎01‎-‎04 09:29:50.309 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Account updater finished for network interface {7a0a0dce-0a51-471a-8c16-6e767cd0b861}. 
```

**注意**  
在后一示例中，没有用于 **数据存储创建/更新** 的条目，或者 **数据存储创建/更新已完成**。 由于存储在 SIM 中的信息对于帐户管理过程至关重要，因此没有 SIM 的设备将不具有必要的关联元数据。



如果硬件已成功处理，但你的徽标或名称未显示在 "网络" 列表中，则可能是元数据包有问题。 可以通过在日志中使用分析器任务项来对此进行调查。 若要查找这些条目，请搜索 " **分析器-任务**"。 成功分析的日志条目通常如下所示：

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

这些日志显示已正确分析 **MobileBroadbandInfo.xml** 文件，分析程序任务应用了 wwan 配置文件 (和成功更新配置文件的 wwan 服务日志记录) ，以及分析器任务设置 **MobileBroadbandInfo.xml**中提到的受信任的设置证书。

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

由于分析器任务运行多次是正常的，你可能会看到多个 `[Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]` 日志条目集。 在这种情况下，条目集通常是相同的，如果它们不相同，则可能表示存在间歇问题。

## <a name="span-idadditional_resourcesspanspan-idadditional_resourcesspanspan-idadditional_resourcesspanadditional-resources"></a><span id="Additional_resources"></span><span id="additional_resources"></span><span id="ADDITIONAL_RESOURCES"></span>其他资源


使用以下链接详细了解 Windows 8.1 和 Windows 10 中的移动宽带：

-   [移动宽带概述](overview-of-mobile-broadband.md)

-   [APN 数据库概述](apn-database-overview.md)

-   [服务元数据](service-metadata.md)