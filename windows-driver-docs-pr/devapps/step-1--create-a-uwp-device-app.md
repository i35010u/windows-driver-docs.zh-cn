---
title: 步骤1创建 UWP 设备应用
description: 本主题介绍使用 Microsoft Visual Studio 创建 UWP 设备应用程序的基本过程。 了解所有 UWP 设备应用共用的任务。
ms.assetid: 4D8240AD-F589-4623-BC6E-47E304831250
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6485014f4488535208bc81885b5aef79e203662a
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733005"
---
# <a name="step-1-create-a-uwp-device-app"></a>步骤1：创建 UWP 设备应用


![设备应用工作流，步骤1](images/1-device-app-workflow.png)

本主题介绍使用 Microsoft Visual Studio 创建 UWP 设备应用程序的基本过程。 了解所有 UWP 设备应用共用的任务。

UWP 设备应用是一种特殊类型的 UWP 应用，设备制造商可以创建它来充当其内部或外围设备。 通过使用设备元数据，设备应用可以运行特权操作并在设备接通电源时自动安装。 有关 UWP 设备应用的详细信息，请参阅 " [满足 uwp 设备应用](meet-uwp-device-apps.md)"。

**注意**   本主题是分步序列的一部分。 有关简介，请参阅 [构建 UWP 设备应用循序渐进](build-a-uwp-device-app-step-by-step.md) 。

 

## <a name="span-idbefore_you_beginspanspan-idbefore_you_beginspanspan-idbefore_you_beginspanbefore-you-begin"></a><span id="Before_you_begin"></span><span id="before_you_begin"></span><span id="BEFORE_YOU_BEGIN"></span>开始之前


此循序渐进指南假设你已创建一个 UWP 应用项目，并且任何必需的设备驱动程序已经存在。

### <a name="span-idcreating_the_windows_store_app_projectspanspan-idcreating_the_windows_store_app_projectspanspan-idcreating_the_windows_store_app_projectspancreating-the-microsoft-store-app-project"></a><span id="Creating_the_Windows_Store_app_project"></span><span id="creating_the_windows_store_app_project"></span><span id="CREATING_THE_WINDOWS_STORE_APP_PROJECT"></span>创建 Microsoft Store 应用项目

在开始之前，需要安装 Visual Studio 并创建一个 UWP 应用项目。 如果尚未执行此操作，可在 [此处下载工具](https://go.microsoft.com/fwlink/p/?LinkId=302196)。 若要开始使用 Microsoft Visual Studio，请参阅 [使用 Visual Studio 开发 UWP 应用](/previous-versions/windows/apps/br211384(v=win.10))。

### <a name="span-iddevice_driver_requirementsspanspan-iddevice_driver_requirementsspanspan-iddevice_driver_requirementsspandevice-driver-requirements"></a><span id="Device_driver_requirements"></span><span id="device_driver_requirements"></span><span id="DEVICE_DRIVER_REQUIREMENTS"></span>设备驱动程序要求

某些 UWP 设备应用和 Api 要求你的设备支持 Microsoft 提供的驱动程序，或者你的驱动程序支持特定的驱动程序模型。 下表列出了一些设备应用和 Api 的驱动程序要求。

| 设备应用或 API                      | 驱动程序信息                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|----------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 适用于照相机的 UWP 设备应用   | 照相机的驱动程序必须使用 AvStream 驱动程序模型。 有关 AvStream 驱动程序模型的详细信息，请参阅 Windows 驱动程序工具包中的 [AvStream 概述](../stream/avstream-overview.md) 。 其他组件（称为 "驱动程序 MFT" (media foundation 转换) ）可随驱动程序安装包一起提供，以提供照相机的自定义效果。 有关详细信息，请参阅适用 [于照相机的 Windows 应用商店设备应用](uwp-device-apps-for-webcams.md)。 |
| 适用于打印机的 UWP 设备应用 | 打印机必须使用 v4 打印机驱动程序。 有关详细信息，请参阅 [开发 v4 打印驱动程序](../print/v4-printer-driver.md) 。                                                                                                                                                                                                                                                                                                                                                         |
| USB Api                               | 若要使用 Windows 运行时的[Windows Usb](/uwp/api/Windows.Devices.Usb)api，你的设备必须与 Winusb.sys 驱动程序兼容。                                                                                                                                                                                                                                                                                                                                      |
| 人体学接口设备 (HID) Api      | HID Api 设计用于 USB、蓝牙、蓝牙智能和 I2C 传输。 若要使用 Windows 运行时[HumanInterfaceDevice](/uwp/api/Windows.Devices.HumanInterfaceDevice) api，你的设备必须与传输所需的 HIDClass.sys 驱动程序和驱动程序兼容。 有关详细信息，请参阅 [HID 体系结构](/previous-versions/jj126193(v=vs.85))。                                                                                                            |
| 蓝牙 GATT Api                    | 若要使用 Windows 运行时蓝牙 GATT Api， [bluetooth.genericattributeprofile 替换](/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile)，设备必须与 BthLEEnum.sys 驱动程序兼容。                                                                                                                                                                                                                                                                                   |
| 蓝牙 RFCOMM Api                  | 若要使用 Windows 运行时蓝牙 RFCOMM Api， [RFCOMM](/uwp/api/Windows.Devices.Bluetooth.Rfcomm)，你的设备必须与 Rfcomm.sys 和 BthEnum.sys 驱动程序兼容。                                                                                                                                                                                                                                                                                    |

 

**重要提示**   使用自定义驱动程序的设备访问权限需要 Microsoft 的批准。 想要使用自定义驱动程序实现专用设备的设备访问的 Oem 和 Ihv 应该首先联系其 Microsoft 联系人以与 Windows 生态系统团队讨论他们的方案。 有关详细信息，请参阅 [适用于 PC 内部专用设备的 UWP 设备应用设计指南](https://go.microsoft.com/fwlink/p/?LinkId=306693)中的 "自定义驱动程序访问模型" 部分。

 

## <a name="span-idcreate_a_windows_store_accountspanspan-idcreate_a_windows_store_accountspanspan-idcreate_a_windows_store_accountspancreate-a-microsoft-store-account"></a><span id="Create_a_Windows_Store_account"></span><span id="create_a_windows_store_account"></span><span id="CREATE_A_WINDOWS_STORE_ACCOUNT"></span>创建 Microsoft Store 帐户


需要 Microsoft Store 上的开发人员帐户。 在后续步骤中创作应用程序清单和设备元数据时，需要发布者名称。 创建存储配置文件后，还可以为应用保留一个名称。

若要创建 Microsoft Store 帐户，请在 " [UWP 应用注册" 页上](https://go.microsoft.com/fwlink/p/?LinkId=302197) ，单击 " **立即注册**"。

输入 **发布者显示名称**后，请输入应用应在 Microsoft Store 中列出的名称。 在帐户验证完成之前，你将无法更改此名称。 仔细挑选名称，因为客户会在浏览时看到此名称，并将通过此名称来了解你的应用。

## <a name="span-idassociate_your_app_with_the_windows_storespanspan-idassociate_your_app_with_the_windows_storespanspan-idassociate_your_app_with_the_windows_storespanassociate-your-app-with-the-microsoft-store"></a><span id="Associate_your_app_with_the_Windows_Store"></span><span id="associate_your_app_with_the_windows_store"></span><span id="ASSOCIATE_YOUR_APP_WITH_THE_WINDOWS_STORE"></span>将你的应用与 Microsoft Store


创建 Microsoft Store 帐户并选择发布者名称后，将应用程序与 Microsoft Store 相关联。 这样做会自动将以下值下载到本地应用包清单文件中，名为 **appxmanifest.xml**。

-   包显示名称

-   包名称

-   发布者 ID

-   发布者显示名称

**注意**   如果已开发设备元数据，则将应用与 Microsoft Store 相关联后，需要用应用程序清单中的值更新设备元数据。

 

**若要将应用与 Microsoft Store**

1.  在 **解决方案资源管理器**中，右键单击项目，然后选择 **"将 &gt; 应用与应用商店关联"**。

2.  在 "将 **应用与 Microsoft Store 关联** " 对话框中，单击 " **下一步**"。 系统将提示你登录到 Microsoft Store。

3.  在 " **登录** " 页上，登录到 Microsoft Store，然后单击 " **下一步**"。

4.  在 " **为此包选择应用程序名称** " 页上，选择保留的 **应用名称** 。 你还可以单击 " **保留名称** "，以将其保留 Microsoft Store。

5.  选择应用名称后，单击 " **下一步**"。

6.  在 "摘要" 页上，查看您选择的值。 如果看上去不错，请单击 " **关联**"。 否则，单击 " **上一** 步" 返回并修复任何错误。 单击 " **关联** " 会自动将发布者显示名称和其他值下载到应用程序包清单中。

## <a name="span-idreview_the_app_package_manifestspanspan-idreview_the_app_package_manifestspanspan-idreview_the_app_package_manifestspanreview-the-app-package-manifest"></a><span id="Review_the_app_package_manifest"></span><span id="review_the_app_package_manifest"></span><span id="REVIEW_THE_APP_PACKAGE_MANIFEST"></span>查看应用程序包清单


将应用与 Microsoft Store 相关联后，请查看应用的包清单，以查看发布者显示名称和其他值是否已按预期方式插入。 确保应用程序标题和名称演示与设备的强连接。 另请注意，在应用程序包中只允许使用一个应用。

**查看应用程序包清单**

1.  在 **解决方案资源管理器**中，双击 **appxmanifest.xml** 文件。 这将打开清单设计器。 清单设计器是一个图形 UI，适用于基础 XML 文件。

2.  在清单设计器中打开该文件后，单击 " **打包** " 选项卡以查看包和发布服务器信息。

    **注意**   若要查看 XML 中的相同信息，请右键单击**appxmanifest.xml** ，然后选择 "**打开方式 &gt; Xml (文本) 编辑器**"。

     

3.  记下你的包名称、发布者名称和应用 ID。 下一步需要用到它们， [步骤2：创建设备元数据](step-2--create-device-metadata.md)。

## <a name="span-idchoose_a_publisher_certificatespanspan-idchoose_a_publisher_certificatespanspan-idchoose_a_publisher_certificatespanchoose-a-publisher-certificate"></a><span id="Choose_a_publisher_certificate"></span><span id="choose_a_publisher_certificate"></span><span id="CHOOSE_A_PUBLISHER_CERTIFICATE"></span>选择发布者证书


使用清单设计器查看应用程序包清单时，请选择与清单中的 **发布者** 名称匹配的发行者证书。 当清单设计器打开时，在 " **打包** " 选项卡上，单击 " **选择证书** " 以选择相应的证书。

## <a name="span-iddevelop_your_windows_store_device_appspanspan-iddevelop_your_windows_store_device_appspanspan-iddevelop_your_windows_store_device_appspandevelop-your-uwp-device-app"></a><span id="Develop_your_Windows_Store_device_app"></span><span id="develop_your_windows_store_device_app"></span><span id="DEVELOP_YOUR_WINDOWS_STORE_DEVICE_APP"></span>开发 UWP 设备应用


开始开发 UWP 设备应用时，请注意以下几点。

### <a name="span-iddevice_capabilitiesspanspan-iddevice_capabilitiesspanspan-iddevice_capabilitiesspandevice-capabilities"></a><span id="Device_capabilities"></span><span id="device_capabilities"></span><span id="DEVICE_CAPABILITIES"></span>设备功能

若要访问你的设备，你可能需要在应用包清单中指定设备功能。 这些是通过应用程序的项目中的 appxmanifest.xml 文件的 [DeviceCapability](/uwp/schemas/appxpackage/appxmanifestschema/element-devicecapability) 元素指定的。 请注意，必须手动指定某些设备功能。 有关详细信息，请参阅 [如何在包清单中指定设备功能](/uwp/schemas/appxpackage/how-to-specify-device-capabilities-in-a-package-manifest)。

### <a name="span-idautoplay_for_windows_store_device_appsspanspan-idautoplay_for_windows_store_device_appsspanspan-idautoplay_for_windows_store_device_appsspanautoplay-for-uwp-device-apps"></a><span id="AutoPlay_for_Windows_Store_device_apps"></span><span id="autoplay_for_windows_store_device_apps"></span><span id="AUTOPLAY_FOR_WINDOWS_STORE_DEVICE_APPS"></span>UWP 设备应用的自动播放

设备接通电源时，自动播放会默认启动你的应用。 若要使用此功能，你将需要编辑应用包清单和设备元数据。 有关详细信息，请参阅 [UWP 设备应用的自动播放](autoplay-for-uwp-device-apps.md)。

### <a name="span-idsync_or_update_your_device_in_the_backgroundspanspan-idsync_or_update_your_device_in_the_backgroundspanspan-idsync_or_update_your_device_in_the_backgroundspansync-or-update-your-device-in-the-background"></a><span id="Sync_or_update_your_device_in_the_background"></span><span id="sync_or_update_your_device_in_the_background"></span><span id="SYNC_OR_UPDATE_YOUR_DEVICE_IN_THE_BACKGROUND"></span>在后台同步或更新设备

你可以通过使用设备后台任务从 UWP 设备应用同步或更新设备。 若要使用此功能，需要将应用指定为设备元数据中的特权应用。 有关详细信息，请参阅 [UWP 设备应用的设备同步和更新](device-sync-and-update-for-uwp-device-apps.md)。

### <a name="span-idlearn_morespanspan-idlearn_morespanspan-idlearn_morespanlearn-more"></a><span id="Learn_more"></span><span id="learn_more"></span><span id="LEARN_MORE"></span>了解更多信息

**[适用于打印机的 UWP 设备应用](uwp-device-apps-for-printers.md)**：显示打印机状态并扩展打印设置体验。 从 Windows 8.1 开始，你的应用程序还可以管理打印作业并执行打印机维护。

**[适用于照相机的 UWP 设备应用](uwp-device-apps-for-webcams.md)**：扩展相机选项体验。 您的应用程序还可以使用驱动程序 MFT 来提供自定义效果。

**[集成设备](/previous-versions/windows/apps/dn263141(v=win.10))**：了解适用于 USB、HID、蓝牙、扫描等的 Windows 运行时 api。

**[适用于内部设备的 UWP 设备应用](uwp-device-apps-for-specialized-devices.md)**：精益 oem 如何为 PC 的内部设备编写设备应用。


 

## <a name="span-iduse_the_windows_app_certification_kitspanspan-iduse_the_windows_app_certification_kitspanspan-iduse_the_windows_app_certification_kitspanuse-the-windows-app-certification-kit"></a><span id="Use_the_Windows_App_Certification_Kit"></span><span id="use_the_windows_app_certification_kit"></span><span id="USE_THE_WINDOWS_APP_CERTIFICATION_KIT"></span>使用 Windows 应用程序认证工具包


若要为应用程序提供认证，请在提交应用程序进行认证并在 Microsoft Store 中列出之前，在计算机上对其进行验证和测试。 有关详细信息，请参阅 [Windows 应用程序认证包](/previous-versions/windows/apps/hh694081(v=win.10))。

## <a name="span-idnext_stepspanspan-idnext_stepspanspan-idnext_stepspannext-step"></a><span id="Next_step"></span><span id="next_step"></span><span id="NEXT_STEP"></span>下一步


[步骤2：创建设备元数据](step-2--create-device-metadata.md)

