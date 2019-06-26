---
title: 步骤 1 创建 UWP 设备应用程序
description: 本主题介绍使用 Microsoft Visual Studio 创建 UWP 设备应用程序的基本过程。 了解有关普遍适用于所有 UWP 设备应用程序的任务。
ms.assetid: 4D8240AD-F589-4623-BC6E-47E304831250
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cdfe2862dba9ec4fe60523d856edfabd1f1b960
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369359"
---
# <a name="step-1-create-a-uwp-device-app"></a>第 1 步：创建 UWP 设备应用


![设备应用工作流，步骤 1](images/1-device-app-workflow.png)

本主题介绍使用 Microsoft Visual Studio 创建 UWP 设备应用程序的基本过程。 了解有关普遍适用于所有 UWP 设备应用程序的任务。

UWP 设备应用程序是一种特殊的设备制造商创建作为其内部或外围设备的配套的 UWP 应用。 使用设备元数据，设备应用程序可以运行特权的操作，并在插入设备时，自动安装。 有关 UWP 的设备应用程序的详细信息，请参阅[满足 UWP 设备应用](meet-uwp-device-apps.md)。

**请注意**  本主题是分步系列的一部分。 请参阅[构建循序渐进的 UWP 设备应用程序](build-a-uwp-device-app-step-by-step.md)引入。

 

## <a name="span-idbeforeyoubeginspanspan-idbeforeyoubeginspanspan-idbeforeyoubeginspanbefore-you-begin"></a><span id="Before_you_begin"></span><span id="before_you_begin"></span><span id="BEFORE_YOU_BEGIN"></span>开始之前的准备工作


此分步指南假定已创建 UWP 应用项目和任何必要的设备驱动程序已存在。

### <a name="span-idcreatingthewindowsstoreappprojectspanspan-idcreatingthewindowsstoreappprojectspanspan-idcreatingthewindowsstoreappprojectspancreating-the-microsoft-store-app-project"></a><span id="Creating_the_Windows_Store_app_project"></span><span id="creating_the_windows_store_app_project"></span><span id="CREATING_THE_WINDOWS_STORE_APP_PROJECT"></span>创建 Microsoft Store 应用项目

在可以开始之前，需要已安装 Visual Studio 并创建 UWP 应用项目。 如果您没有这样做，则可以[下载工具此处](https://go.microsoft.com/fwlink/p/?LinkId=302196)。 若要开始使用 Microsoft Visual Studio，请参阅[使用 Visual Studio 开发 UWP 应用](https://go.microsoft.com/fwlink/p/?LinkID=267230)。

### <a name="span-iddevicedriverrequirementsspanspan-iddevicedriverrequirementsspanspan-iddevicedriverrequirementsspandevice-driver-requirements"></a><span id="Device_driver_requirements"></span><span id="device_driver_requirements"></span><span id="DEVICE_DRIVER_REQUIREMENTS"></span>设备驱动程序要求

某些 UWP 设备应用和 Api 需要你的设备支持 Microsoft 提供的驱动程序或您的驱动程序支持的特定驱动程序模型。 此表列出了某些设备应用程序和 Api 的驱动程序要求。

| 设备应用或 API                      | 驱动程序信息                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|----------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 用于相机的 UWP 设备应用程序   | 照相机的驱动程序必须使用 AvStream 驱动程序模型。 有关 AvStream 驱动程序模型的详细信息，请参阅[AVStream 概述](https://go.microsoft.com/fwlink/p/?LinkId=273032)Windows 驱动程序工具包中。 一个附加组件，称为驱动程序 MFT （媒体基础转换），可以提供与要为相机提供自定义效果的驱动程序安装包。 有关详细信息，请参阅[Windows 应用商店设备应用用于相机](uwp-device-apps-for-webcams.md)。 |
| 适用于打印机的 UWP 设备应用 | 打印机必须使用 v4 打印机驱动程序。 请参阅[开发 v4 打印驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=314231)的详细信息。                                                                                                                                                                                                                                                                                                                                                         |
| USB Api                               | 若要使用 Windows 运行时[Windows.Devices.Usb](https://go.microsoft.com/fwlink/p/?LinkId=306694)Api，你的设备必须符合 Winusb.sys 驱动程序。                                                                                                                                                                                                                                                                                                                                      |
| 人机接口设备 (HID) Api      | HID Api 专供通过 USB、 蓝牙、 蓝牙智能和 I2C 传输。 若要使用 Windows 运行时[Windows.Devices.HumanInterfaceDevice](https://go.microsoft.com/fwlink/p/?LinkId=306697) Api，你的设备必须符合 HIDClass.sys 驱动程序和驱动程序所需的传输。 有关详细信息，请参阅[HID 体系结构](https://docs.microsoft.com/previous-versions/jj126193(v=vs.85))。                                                                                                            |
| 蓝牙 GATT Api                    | 若要使用 Windows 运行时的蓝牙 GATT Api 中， [Windows.Devices.Bluetooth.GenericAttributeProfile](https://go.microsoft.com/fwlink/p/?LinkId=306698)，你的设备必须符合 BthLEEnum.sys 驱动程序。                                                                                                                                                                                                                                                                                   |
| 蓝牙 RFCOMM Api                  | 若要使用 Windows 运行时的蓝牙 RFCOMM Api 中， [Windows.Devices.Bluetooth.Rfcomm](https://go.microsoft.com/fwlink/p/?LinkId=306699)，你的设备必须符合的 Rfcomm.sys 和 BthEnum.sys 驱动程序。                                                                                                                                                                                                                                                                                    |

 

**重要**  设备访问使用自定义驱动程序需要获得 Microsoft 的批准。 Oem 和 Ihv 想要实现使用自定义驱动程序的专用设备的设备访问首先应联系其 Microsoft 联系人讨论其与 Windows 生态系统团队方案。 有关详细信息，请参阅中的自定义驱动程序访问模型部分[UWP 设备应用程序设计指南适用于 PC 的内部专用设备](https://go.microsoft.com/fwlink/p/?LinkId=306693)。

 

## <a name="span-idcreateawindowsstoreaccountspanspan-idcreateawindowsstoreaccountspanspan-idcreateawindowsstoreaccountspancreate-a-microsoft-store-account"></a><span id="Create_a_Windows_Store_account"></span><span id="create_a_windows_store_account"></span><span id="CREATE_A_WINDOWS_STORE_ACCOUNT"></span>创建 Microsoft Store 帐户


Microsoft Store 上的开发人员帐户是必需的。 当您编写应用程序清单和更高版本的步骤中的设备元数据时，将需要发布者名称。 创建存储配置文件后，你也可以保留您的应用程序的名称。

若要创建的 Microsoft Store 帐户，请转到[UWP 应用注册页](https://go.microsoft.com/fwlink/p/?LinkId=302197)然后单击**立即注册**。

当输入**发布者显示名称**，输入应在其下在 Microsoft Store 中列出您的应用程序的名称。 你将无法完成帐户验证之前更改此名称。 谨慎选择名称，客户将会看到此名称时浏览，并且会知道您的应用程序按此名称。

## <a name="span-idassociateyourappwiththewindowsstorespanspan-idassociateyourappwiththewindowsstorespanspan-idassociateyourappwiththewindowsstorespanassociate-your-app-with-the-microsoft-store"></a><span id="Associate_your_app_with_the_Windows_Store"></span><span id="associate_your_app_with_the_windows_store"></span><span id="ASSOCIATE_YOUR_APP_WITH_THE_WINDOWS_STORE"></span>将您的应用程序与 Microsoft Store 相关联


已经创建了一个 Microsoft Store 帐户并选择发布者名称后，将与 Microsoft Store 应用程序相关联。 执行此操作会自动将以下值下载到本地应用程序包清单文件，名为**Package.appxmanifest**。

-   包显示名称

-   程序包名称

-   发布者 ID

-   发布者显示名称

**请注意**  如果您已开发的设备元数据，与 Microsoft Store 将应用程序后，您将需要使用应用程序清单中的值更新设备元数据。

 

**若要将您的应用程序与 Microsoft Store 相关联**

1.  在中**解决方案资源管理器**，右键单击项目，然后选择**应用商店&gt;应用程序与应用商店关联**。

2.  在中**将应用与 Microsoft Store**对话框中，单击**下一步**。 系统将提示您登录到 Microsoft Store。

3.  上**Sign In**页上，登录到 Microsoft Store，然后单击**下一步**。

4.  上**选择此包将应用程序名称**页上，选择**应用名称**已保留。 此外可以单击**保留名称**转到 Microsoft Store 保留其中一个。

5.  选择将应用程序名称，然后单击**下一步**。

6.  在摘要页上查看所选的值。 如果一切正常，请单击**相关联**。 否则，请单击**上一步**以返回并修复任何错误。 单击**相关联**自动下载到应用包清单的发布者显示名称和其他值。

## <a name="span-idreviewtheapppackagemanifestspanspan-idreviewtheapppackagemanifestspanspan-idreviewtheapppackagemanifestspanreview-the-app-package-manifest"></a><span id="Review_the_app_package_manifest"></span><span id="review_the_app_package_manifest"></span><span id="REVIEW_THE_APP_PACKAGE_MANIFEST"></span>查看应用包清单


将您的应用程序与 Microsoft Store 关联后，查看你的应用包清单，若要查看按预期方式已插入发布者显示名称和其他值。 请确保应用程序标题和名称演示紧密连接到设备。 另请注意，只有一个应用程序允许在应用程序包中。

**若要查看应用包清单**

1.  在中**解决方案资源管理器**，双击**package.appxmanifest**文件。 这将打开清单设计器。 清单设计器为基础的 XML 文件的图形用户界面。

2.  清单设计器中打开该文件后，单击**打包**选项卡以查看包和发布服务器信息。

    **请注意**  若要查看在 XML 中相同的信息，请右键单击**package.appxmanifest** ，然后选择**打开&gt;XML （文本） 编辑器**。

     

3.  记下的包名称、 发布者名称和应用程序 id。 您需要将它们的下一步，[步骤 2:创建设备元数据](step-2--create-device-metadata.md)。

## <a name="span-idchooseapublishercertificatespanspan-idchooseapublishercertificatespanspan-idchooseapublishercertificatespanchoose-a-publisher-certificate"></a><span id="Choose_a_publisher_certificate"></span><span id="choose_a_publisher_certificate"></span><span id="CHOOSE_A_PUBLISHER_CERTIFICATE"></span>选择发布服务器证书


尽管您要查看使用清单设计器的应用包清单，选择与匹配的发布服务器证书**发布服务器**名称在清单中。 清单设计器处于打开状态上时**打包**选项卡上，单击**选择证书**来选择相应的证书。

## <a name="span-iddevelopyourwindowsstoredeviceappspanspan-iddevelopyourwindowsstoredeviceappspanspan-iddevelopyourwindowsstoredeviceappspandevelop-your-uwp-device-app"></a><span id="Develop_your_Windows_Store_device_app"></span><span id="develop_your_windows_store_device_app"></span><span id="DEVELOP_YOUR_WINDOWS_STORE_DEVICE_APP"></span>开发 UWP 设备应用程序


当您开始开发 UWP 设备应用程序，请考虑以下几点。

### <a name="span-iddevicecapabilitiesspanspan-iddevicecapabilitiesspanspan-iddevicecapabilitiesspandevice-capabilities"></a><span id="Device_capabilities"></span><span id="device_capabilities"></span><span id="DEVICE_CAPABILITIES"></span>设备功能

若要访问你的设备，你可能需要在应用包清单中指定设备功能。 指定这些选项[DeviceCapability](https://go.microsoft.com/fwlink/p/?LinkId=306696)中应用的项目的 Package.appxmanifest 文件中的元素。 请注意，必须手动指定某些设备功能。 有关详细信息，请参阅[如何在包清单中指定设备功能](https://go.microsoft.com/fwlink/p/?LinkID=306695)。

### <a name="span-idautoplayforwindowsstoredeviceappsspanspan-idautoplayforwindowsstoredeviceappsspanspan-idautoplayforwindowsstoredeviceappsspanautoplay-for-uwp-device-apps"></a><span id="AutoPlay_for_Windows_Store_device_apps"></span><span id="autoplay_for_windows_store_device_apps"></span><span id="AUTOPLAY_FOR_WINDOWS_STORE_DEVICE_APPS"></span>适用于 UWP 设备应用的自动播放

在插入设备时，自动播放默认情况下启动应用。 若要使用此功能，您将需要编辑应用包清单和设备元数据。 有关详细信息，请参阅[UWP 设备应用程序的自动播放](autoplay-for-uwp-device-apps.md)。

### <a name="span-idsyncorupdateyourdeviceinthebackgroundspanspan-idsyncorupdateyourdeviceinthebackgroundspanspan-idsyncorupdateyourdeviceinthebackgroundspansync-or-update-your-device-in-the-background"></a><span id="Sync_or_update_your_device_in_the_background"></span><span id="sync_or_update_your_device_in_the_background"></span><span id="SYNC_OR_UPDATE_YOUR_DEVICE_IN_THE_BACKGROUND"></span>同步，或者在后台将设备更新

可以同步或使用设备后台任务更新你的设备从 UWP 设备应用。 若要使用此功能，您需要为设备元数据中的特权应用指定您的应用程序。 有关详细信息，请参阅[设备同步和适用于 UWP 的设备应用程序更新](device-sync-and-update-for-uwp-device-apps.md)。

### <a name="span-idlearnmorespanspan-idlearnmorespanspan-idlearnmorespanlearn-more"></a><span id="Learn_more"></span><span id="learn_more"></span><span id="LEARN_MORE"></span>了解更多信息

|                                                                                                         |                                                                                                                                                                |
|---------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [打印机的 UWP 设备应用](uwp-device-apps-for-printers.md)                    | 显示打印机状态和扩展的打印设置体验。 从 Windows 8.1，您的应用程序可以还管理打印作业并执行打印机的维护。 |
| [适用于相机的 UWP 设备应用](uwp-device-apps-for-webcams.md)                      | 扩展相机选项体验。 您的应用程序还可以提供与驱动程序 MFT 的自定义效果。                                                              |
| [将集成的设备](https://go.microsoft.com/fwlink/p/?LinkId=533279)                                  | 有关 USB、 HID、 蓝牙、 扫描，和的详细信息，请查阅 Windows 运行时 Api。                                                                                  |
| [适用于内部设备的 UWP 设备应用](uwp-device-apps-for-specialized-devices.md) | 了解如何 Oem 可以编写适用于内部到 PC 的设备的设备应用程序。                                                                                            |

 

## <a name="span-idusethewindowsappcertificationkitspanspan-idusethewindowsappcertificationkitspanspan-idusethewindowsappcertificationkitspanuse-the-windows-app-certification-kit"></a><span id="Use_the_Windows_App_Certification_Kit"></span><span id="use_the_windows_app_certification_kit"></span><span id="USE_THE_WINDOWS_APP_CERTIFICATION_KIT"></span>使用 Windows 应用认证工具包


为了让您的应用程序认证的最大限度地，验证，并在计算机上进行测试，然后才能提交进行认证并在 Microsoft Store 中的列出。 有关详细信息，请参阅[Windows 应用认证工具包](https://go.microsoft.com/fwlink/p/?LinkId=273040)。

## <a name="span-idnextstepspanspan-idnextstepspanspan-idnextstepspannext-step"></a><span id="Next_step"></span><span id="next_step"></span><span id="NEXT_STEP"></span>下一步


[步骤 2：创建设备元数据](step-2--create-device-metadata.md)

 

 





