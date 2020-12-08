---
title: UWP 设备应用的新增功能
description: 本部分概述 UWP 设备应用的新增功能。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c96f0aecdba7dcd6938daf0b9e59181b63f12e10
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815158"
---
# <a name="whats-new-for-uwp-device-apps"></a>UWP 设备应用的新增功能


本部分概述 UWP 设备应用的新增功能。 有关设备应用的详细信息，请参阅 " [满足 UWP 设备应用](meet-uwp-device-apps.md)"。

**提示**  Windows 运行时设备 Api 不需要设备元数据。 这意味着你的应用程序无需成为 UWP 设备应用即可使用它们。 UWP 应用可以使用这些 Api 来访问 USB、用户界面设备 (HID) 、蓝牙 GATT、蓝牙 RFCOMM、Wi-Fi 直接设备等。 有关详细信息，请参阅 [集成设备](/previous-versions/windows/apps/dn263141(v=win.10))。

 

## <a name="span-idwhat_s_new_for_windows_10spanspan-idwhat_s_new_for_windows_10spanspan-idwhat_s_new_for_windows_10spanwhats-new-for-windows-10"></a><span id="What_s_new_for_Windows_10"></span><span id="what_s_new_for_windows_10"></span><span id="WHAT_S_NEW_FOR_WINDOWS_10"></span>Windows 10 的新增功能


对于 Windows 10，无 Microsoft Store 设备应用功能的更改。 用于生成、测试和提交 UWP 设备应用的 Windows 8.1 过程将继续使用 Windows 10。 但是，我们建议使用自定义功能开发通用 Windows 平台 (UWP) 应用程序。 有关详细信息，请参阅 [硬件支持应用 (HSA) ：适用于应用开发人员的步骤](hardware-support-app--hsa--steps-for-app-developers.md)。

## <a name="span-iddevice_metadata_wizardspanspan-iddevice_metadata_wizardspanspan-iddevice_metadata_wizardspandevice-metadata-wizard"></a><span id="Device_metadata_wizard"></span><span id="device_metadata_wizard"></span><span id="DEVICE_METADATA_WIZARD"></span>设备元数据向导


Windows 8.1 引入了一个新的设备元数据向导。 轻松为 UWP 设备应用创建设备元数据包，无需编辑原始 XML。 在将应用提交到仪表板之前，新向导还可以本地验证设备元数据。 有关此向导如何适应此过程的详细信息，请参阅分步 [构建 UWP 设备应用](build-a-uwp-device-app-step-by-step.md)。

**注意**  若要获取设备元数据创作向导，在完成本主题中的步骤之前，必须安装 [用于 Windows 8.1 的独立 SDK](https://go.microsoft.com/fwlink/p/?linkid=309209) 。 为 Windows 安装 Microsoft Visual Studio Express 会安装不包括向导的 SDK 版本。

 

## <a name="span-id_background_tasks_for_device_sync_and_updatespanspan-id_background_tasks_for_device_sync_and_updatespanspan-id_background_tasks_for_device_sync_and_updatespan-background-tasks-for-device-sync-and-update"></a><span id="_Background_tasks_for_device_sync_and_update"></span><span id="_background_tasks_for_device_sync_and_update"></span><span id="_BACKGROUND_TASKS_FOR_DEVICE_SYNC_AND_UPDATE"></span> 设备同步和更新的后台任务


在 Windows 8.1 中，UWP 设备应用可以在后台任务中执行多步骤设备操作，使其能够运行到完成，即使应用已移动到后台并挂起也是如此。 这是允许 (更改持久设置或固件) 和内容同步所需的可靠设备，而无需用户坐下来观看进度栏。 将 [DeviceServicingTrigger](/uwp/api/Windows.ApplicationModel.Background.DeviceServicingTrigger) 用于设备服务，将 [DeviceUseTrigger](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) 用于内容同步。 请注意，这些后台任务会限制应用可在后台运行的时间量，不允许无限操作或无限同步。 有关详细信息，请参阅 [UWP 设备应用的设备同步和更新](device-sync-and-update-for-uwp-device-apps.md)。

**注意**  设备同步的 [DeviceUseTrigger](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger)不需要设备元数据。

 

## <a name="span-idautoplay_for_windows_store_device_appsspanspan-idautoplay_for_windows_store_device_appsspanspan-idautoplay_for_windows_store_device_appsspanautoplay-for-uwp-device-apps"></a><span id="AutoPlay_for_Windows_Store_device_apps"></span><span id="autoplay_for_windows_store_device_apps"></span><span id="AUTOPLAY_FOR_WINDOWS_STORE_DEVICE_APPS"></span>UWP 设备应用的自动播放


你可以配置 UWP 设备应用，使其在你的外围设备连接到电脑时自动启动 (在安装该应用后) 。 在 Windows 8.1 中，设备应用的自动播放将添加对人体学接口设备 (HID) 、智能卡和常规端口的支持。 有关详细信息，请参阅 [UWP 设备应用的自动播放](autoplay-for-uwp-device-apps.md)。

## <a name="span-idprinter_capabilitiesspanspan-idprinter_capabilitiesspanspan-idprinter_capabilitiesspanprinter-capabilities"></a><span id="Printer_capabilities"></span><span id="printer_capabilities"></span><span id="PRINTER_CAPABILITIES"></span>打印机功能


在 Windows 8.1 中，UWP 设备应用可以管理打印作业和执行打印机维护任务。 有关详细信息，请参阅 [如何管理打印作业](how-to-manage-print-jobs.md) 和 [如何进行打印机维护](how-to-do-printer-maintenance.md)。

你可以看到这些功能在新示例中突出显示， [打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)。 示例附带的打印机扩展库包装了 COM 接口 PrinterExtensionLib 的 COM 实现。 此库旨在使您能够轻松地在自己的 UWP 设备应用程序中重复使用。

## <a name="span-iduser_experience_changesspanspan-iduser_experience_changesspanspan-iduser_experience_changesspanuser-experience-changes"></a><span id="User_experience_changes"></span><span id="user_experience_changes"></span><span id="USER_EXPERIENCE_CHANGES"></span>用户体验更改


为了提供与 Windows 8.1 上安装的其他 UWP 应用一致的体验，UWP 设备应用在安装时不会被固定为 " **启动** "。 从一 **开始**，用户可从屏幕中心 (向上) ，以查看所有应用，包括最近安装的 UWP 设备应用。

Windows 8.1 内置相机应用不再包含 " **选项** " 按钮。 这意味着，UWP 设备应用中的自定义相机选项飞出不会出现在该应用中。 但是，在安装时，任何其他使用 **CameraCaptureUI** 类的 UWP 应用仍可以公开自 **定义的浮** 出控件。

 

