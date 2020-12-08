---
title: 初识 UWP 设备应用
description: 本主题概述了使 UWP 设备应用与常规 UWP 应用程序不同的特性和功能。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73c037436556d4e107a037be8cc12d4b0cec9d58
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815183"
---
# <a name="meet-uwp-device-apps"></a>初识 UWP 设备应用


设备制造商可以创建用作设备配套的 UWP 设备应用。 设备应用能够使用外围设备或内部设备的全部功能，并可以执行特权操作，例如固件更新。 本主题概述了使 UWP 设备应用与常规 UWP 应用程序不同的特性和功能。

**注意**  其中每个功能都是可选的。 单个设备应用不需要全部使用。 所有这些功能都需要设备元数据。

 

有关 UWP 设备应用的定义以及如何创建它的详细信息，请参阅 [构建 uwp 设备应用](the-workflow.md)。

## <a name="span-id_device_updatespanspan-id_device_updatespanspan-id_device_updatespan-device-update"></a><span id="_Device_update"></span><span id="_device_update"></span><span id="_DEVICE_UPDATE"></span> 设备更新


当指定为设备元数据中的特权应用时，UWP 设备应用可以在设备后台任务中执行多步骤设备操作。 这种特殊类型的后台任务可以运行到完成，即使应用程序已移动到后台并挂起也是如此。 这对于允许提供可靠的设备服务（如更改持久的设置或固件）是必需的，无需用户坐下来观看进度栏。

![windows 应用商店设备应用程序可以在后台执行设备更新，如固件更新](images/deviceupdateuserconsent.png)

若要创建用于设备服务的后台任务 () 的设备更新，请使用 [DeviceServicingTrigger](/uwp/api/Windows.ApplicationModel.Background.DeviceServicingTrigger) 触发器。 可用于所有 UWP 应用的类似触发器 [DeviceUseTrigger](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger)（可用于实现可靠的内容同步）。 有关详细信息，请参阅 [UWP 设备应用的设备同步和更新](device-sync-and-update-for-uwp-device-apps.md)。

**注意**  设备后台任务会限制应用可在后台运行的时间量，不允许无限操作或无限同步。

 

## <a name="span-idautoplayspanspan-idautoplayspanspan-idautoplayspanautoplay"></a><span id="AutoPlay"></span><span id="autoplay"></span><span id="AUTOPLAY"></span>功能


你可以配置任何 UWP 应用，包括 UWP 设备应用，以便在自动播放支持的设备连接到电脑时自动启动。 但是，该应用必须支持自动播放处理程序，并在应用程序清单中指定体验 ID。 还可以选择允许其他 UWP 应用充当设备的自动播放处理程序。

![设备的示例自动播放对话框](images/autoplayfordeviceapps.png)

有关自动播放以及 Windows 8.1 中支持的设备类的详细信息，请参阅 [UWP 设备应用的自动播放](autoplay-for-uwp-device-apps.md)。

## <a name="span-iddevice_apps_for_printersspanspan-iddevice_apps_for_printersspanspan-iddevice_apps_for_printersspandevice-apps-for-printers"></a><span id="Device_apps_for_printers"></span><span id="device_apps_for_printers"></span><span id="DEVICE_APPS_FOR_PRINTERS"></span>适用于打印机的设备应用


UWP 设备应用可以通过自定义的打印设置浮出控件和通知支持突出显示打印机的特殊功能。 UWP 设备应用还可以显示打印机状态、管理打印作业和执行打印机维护。

有关信息，请参阅以下主题：

-   [如何显示打印机状态](how-to-display-printer-status.md)
-   [如何自定义打印设置](how-to-customize-print-settings.md)
-   [处理打印通知](working-with-print-notifications.md)
-   [如何管理打印作业](how-to-manage-print-jobs.md)
-   [如何执行打印机维护](how-to-do-printer-maintenance.md)
-   [打印机扩展库概述](printer-extension-library-overview.md)

## <a name="span-iddevice_apps_for_camerasspanspan-iddevice_apps_for_camerasspanspan-iddevice_apps_for_camerasspandevice-apps-for-cameras"></a><span id="Device_apps_for_cameras"></span><span id="device_apps_for_cameras"></span><span id="DEVICE_APPS_FOR_CAMERAS"></span>照相机设备应用


UWP 设备应用还可以通过自定义相机设置和特殊相机效果突出显示相机的特殊功能。

有关详细信息，请参阅以下主题：

-   [如何自定义相机选项](how-to-customize-camera-options.md)
-   [创建相机驱动程序 MFT](creating-a-camera-driver-mft.md)
-   [多针相机上的驱动程序 MFT 的注意事项](driver-mfts-on-multi-pin-cameras.md)
-   [识别内部相机的位置](identifying-the-location-of-internal-cameras.md)

## <a name="span-iddevice_apps_for_internal_devicesspanspan-iddevice_apps_for_internal_devicesspanspan-iddevice_apps_for_internal_devicesspandevice-apps-for-internal-devices"></a><span id="Device_apps_for_internal_devices"></span><span id="device_apps_for_internal_devices"></span><span id="DEVICE_APPS_FOR_INTERNAL_DEVICES"></span>内部设备的设备应用


Oem 和组件供应商可以为 PC 内部的设备开发 UWP 设备应用程序。 若要访问与系统容器关联的设备，必须在设备元数据中将应用指定为特权应用。 内部设备的应用通常预安装在电脑上，并可以从 Microsoft Store 下载。 有关详细信息，请参阅 [内部设备的 UWP 设备应用](uwp-device-apps-for-specialized-devices.md)。

## <a name="span-idautomatic_installationspanspan-idautomatic_installationspanspan-idautomatic_installationspanautomatic-installation"></a><span id="Automatic_installation"></span><span id="automatic_installation"></span><span id="AUTOMATIC_INSTALLATION"></span>自动安装


当用户将设备连接到 PC 时，UWP 设备应用可以自动安装。 如果与 Internet 的连接不可用，则 Windows 稍后将重试。 设备应用安装到 **所有应用**。

![windows 应用商店设备应用可以自动安装](images/autoinstalluserexperience.png)

**警告**  请注意，在安装应用时，自动安装功能不会向用户提供通知。 某些用户可能会发现这种体验令人费解，并使应用程序成为不良评级。

 

有关自动安装的详细信息，请参阅 [打印机和照相机的自动安装](auto-install-for-uwp-device-apps.md)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[构建 UWP 设备应用](the-workflow.md)

[UWP 设备应用的自动安装](auto-install-for-uwp-device-apps.md)

[UWP 设备应用的自动播放](autoplay-for-uwp-device-apps.md)

[UWP 设备应用的设备同步和更新](device-sync-and-update-for-uwp-device-apps.md)

 

