---
title: 初识 UWP 设备应用
description: 本主题提供的功能，使 UWP 设备应用唯一不同于常规的 UWP 应用的功能的概述。
ms.assetid: 395745E6-7A97-4B26-A82C-0729E7B999C6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3227bcab091c9ba6c7584e12546f661abb47eb42
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370234"
---
# <a name="meet-uwp-device-apps"></a>初识 UWP 设备应用


设备制造商可以创建用作设备配套的 UWP 设备应用。 设备应用程序可以使用外围或内部设备的功能的完整范围，并且可以执行特权的操作，例如固件更新。 本主题提供的功能，使 UWP 设备应用唯一不同于常规的 UWP 应用的功能的概述。

**请注意**  各项功能是可选的。 单个设备应用程序不需要使用所有这些。 所有这些功能都需要设备元数据。

 

有关什么 UWP 设备的应用程序以及如何创建一个详细信息，请参阅[构建 UWP 设备应用](the-workflow.md)。

## <a name="span-iddeviceupdatespanspan-iddeviceupdatespanspan-iddeviceupdatespan-device-update"></a><span id="_Device_update"></span><span id="_device_update"></span><span id="_DEVICE_UPDATE"></span> 设备更新


指定为设备元数据中的特权应用时，UWP 设备应用程序可以在设备的后台任务中执行多步骤设备操作。 即使应用移到背景并挂起，这种特殊类型的后台任务可以运行到完成。 这是允许可靠服务，与对永久设置或固件，而无需用户坐下来并监视进度栏的设备所必需的。

![windows 应用商店设备应用程序可以在后台执行设备更新，如固件更新](images/deviceupdateuserconsent.png)

若要创建服务 （设备更新） 的设备的后台任务，请使用[DeviceServicingTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308965)触发器。 类似触发器[DeviceUseTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308967)，允许使用可靠的内容同步，是适用于所有 UWP 应用。 有关详细信息，请参阅[设备同步和适用于 UWP 的设备应用程序更新](device-sync-and-update-for-uwp-device-apps.md)。

**请注意**  设备后台任务将限制应用程序可以在后台运行，它不用于允许无限期的操作或无限同步的时间量。

 

## <a name="span-idautoplayspanspan-idautoplayspanspan-idautoplayspanautoplay"></a><span id="AutoPlay"></span><span id="autoplay"></span><span id="AUTOPLAY"></span>AutoPlay


你可以配置任何 UWP 应用，包括 UWP 设备应用，在自动播放支持的设备连接到 PC 时自动启动。 但是，该应用必须支持自动播放处理程序，并在应用程序清单中指定体验 ID。 您还可以选择让其他 UWP 应用为你的设备的自动播放处理程序。

![设备的示例自动播放对话框](images/autoplayfordeviceapps.png)

有关自动播放和在 Windows 8.1 中支持哪些设备类的详细信息，请参阅[UWP 设备应用程序的自动播放](autoplay-for-uwp-device-apps.md)。

## <a name="span-iddeviceappsforprintersspanspan-iddeviceappsforprintersspanspan-iddeviceappsforprintersspandevice-apps-for-printers"></a><span id="Device_apps_for_printers"></span><span id="device_apps_for_printers"></span><span id="DEVICE_APPS_FOR_PRINTERS"></span>适用于打印机的设备应用


UWP 的设备应用程序可以突出显示的自定义打印设置浮出控件通过打印机的特殊功能并通知支持。 UWP 的设备应用程序还可以显示打印机状态、 管理的打印作业，并执行打印机的维护。

有关信息，请参阅以下主题：

-   [如何显示打印机状态](how-to-display-printer-status.md)
-   [如何自定义打印设置](how-to-customize-print-settings.md)
-   [使用打印通知](working-with-print-notifications.md)
-   [如何管理打印作业](how-to-manage-print-jobs.md)
-   [如何执行操作的打印机的维护](how-to-do-printer-maintenance.md)
-   [打印机扩展库概述](printer-extension-library-overview.md)

## <a name="span-iddeviceappsforcamerasspanspan-iddeviceappsforcamerasspanspan-iddeviceappsforcamerasspandevice-apps-for-cameras"></a><span id="Device_apps_for_cameras"></span><span id="device_apps_for_cameras"></span><span id="DEVICE_APPS_FOR_CAMERAS"></span>用于相机的设备应用程序


UWP 的设备应用程序还可以突出显示自定义的相机设置和特殊的照相机效果通过照相机的特殊的功能。

有关详细信息，请参阅以下主题：

-   [如何自定义照相机选项](how-to-customize-camera-options.md)
-   [创建一个照相机驱动程序 MFT](creating-a-camera-driver-mft.md)
-   [多针相机上的驱动程序 Mft 的注意事项](driver-mfts-on-multi-pin-cameras.md)
-   [确定内部相机的位置](identifying-the-location-of-internal-cameras.md)

## <a name="span-iddeviceappsforinternaldevicesspanspan-iddeviceappsforinternaldevicesspanspan-iddeviceappsforinternaldevicesspandevice-apps-for-internal-devices"></a><span id="Device_apps_for_internal_devices"></span><span id="device_apps_for_internal_devices"></span><span id="DEVICE_APPS_FOR_INTERNAL_DEVICES"></span>内部设备的设备应用


Oem 和组件供应商可以开发 UWP 应用的内部到 PC 的设备的设备应用程序。 若要访问与系统容器相关联的设备，应用必须指定为设备元数据中的特权应用。 适用于内部设备应用通常预安装在电脑上，并且可以从 Microsoft Store 下载。 有关详细信息，请参阅[UWP 设备应用程序的内部设备](uwp-device-apps-for-specialized-devices.md)。

## <a name="span-idautomaticinstallationspanspan-idautomaticinstallationspanspan-idautomaticinstallationspanautomatic-installation"></a><span id="Automatic_installation"></span><span id="automatic_installation"></span><span id="AUTOMATIC_INSTALLATION"></span>自动安装


当用户将设备连接到其 PC 时，可以自动安装 UWP 设备应用程序。 如果与 Internet 的连接不可用，Windows 将稍后重试。 设备应用程序安装到**所有应用**。

![windows 应用商店设备应用程序可以自动安装](images/autoinstalluserexperience.png)

**警告**  务必要考虑，自动安装功能不提供通知给用户安装应用。 有些用户可能发现这种体验让人困惑和令人沮丧，并为您的应用程序提供错误评级。

 

有关自动安装的详细信息，请参阅[自动安装的打印机和相机](auto-install-for-uwp-device-apps.md)。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[构建 UWP 设备应用程序](the-workflow.md)

[UWP 设备应用的自动安装](auto-install-for-uwp-device-apps.md)

[UWP 设备应用的自动播放](autoplay-for-uwp-device-apps.md)

[UWP 设备应用的设备同步和更新](device-sync-and-update-for-uwp-device-apps.md)

 

 






