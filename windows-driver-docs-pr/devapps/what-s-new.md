---
title: 什么是 UWP 设备应用程序的新增功能
description: 本部分概述 UWP 设备应用的新增功能。
ms.assetid: AF18ACFD-EA38-4ABD-9369-3974C019E132
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c7c164aa7b7058524141cc7a77f4954a4cc177e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327617"
---
# <a name="whats-new-for-uwp-device-apps"></a>什么是 UWP 设备应用程序的新增功能


本部分概述 UWP 设备应用的新增功能。 有关设备应用程序的详细信息，请参阅[满足 UWP 设备应用](meet-uwp-device-apps.md)。

**提示**  Windows 运行时设备 Api 不需要的设备元数据。 这意味着您的应用程序不必是一个 UWP 设备应用来使用它们。 UWP 应用可以使用这些 Api 来访问 USB、 人体学接口设备 (HID)、 蓝牙 GATT、 蓝牙 RFCOMM、 Wi-Fi Direct 设备和的详细信息。 有关详细信息，请参阅[集成设备](https://go.microsoft.com/fwlink/p/?LinkId=533279)。

 

## <a name="span-idwhatsnewforwindows10spanspan-idwhatsnewforwindows10spanspan-idwhatsnewforwindows10spanwhats-new-for-windows-10"></a><span id="What_s_new_for_Windows_10"></span><span id="what_s_new_for_windows_10"></span><span id="WHAT_S_NEW_FOR_WINDOWS_10"></span>什么是 Windows 10 的新增功能


Windows 10 中，没有到 Microsoft Store 设备应用程序功能更改。 Windows 8.1 处理为生成、 测试，并提交 UWP 设备应用程序将继续适用于 Windows 10。 但是，我们建议开发通用 Windows 平台 (UWP) 应用程序使用自定义功能。 有关详细信息，请参阅[硬件支持应用程序 (HSA):适用于应用开发人员的步骤](hardware-support-app--hsa--steps-for-app-developers.md)。

## <a name="span-iddevicemetadatawizardspanspan-iddevicemetadatawizardspanspan-iddevicemetadatawizardspandevice-metadata-wizard"></a><span id="Device_metadata_wizard"></span><span id="device_metadata_wizard"></span><span id="DEVICE_METADATA_WIZARD"></span>设备元数据向导


Windows 8.1 引入了新的设备元数据向导。 轻松地创建设备元数据包的 UWP 设备应用程序而无需编辑原始 XML。 新向导还可以验证针对您的应用程序本地的设备元数据之前将其提交到仪表板。 有关此向导如何适应该过程的详细信息，请参阅[构建循序渐进的 UWP 设备应用程序](build-a-uwp-device-app-step-by-step.md)。

**请注意**  若要获取设备元数据创建向导，必须安装[独立 SDK 的 Windows 8.1](https://go.microsoft.com/fwlink/p/?linkid=309209)之前完成本主题中的步骤。 安装 Microsoft Visual Studio Express 的 Windows 安装不包括在向导的 sdk 版本。

 

## <a name="span-idbackgroundtasksfordevicesyncandupdatespanspan-idbackgroundtasksfordevicesyncandupdatespanspan-idbackgroundtasksfordevicesyncandupdatespan-background-tasks-for-device-sync-and-update"></a><span id="_Background_tasks_for_device_sync_and_update"></span><span id="_background_tasks_for_device_sync_and_update"></span><span id="_BACKGROUND_TASKS_FOR_DEVICE_SYNC_AND_UPDATE"></span> 后台任务的设备同步和更新


在 Windows 8.1 UWP 设备应用程序可以执行的后台任务中的多步骤设备操作，以便它们可以运行到完成，即使应用移到背景并挂起。 这是必要允许可靠设备服务 （对持久性设置或固件的更改） 和内容同步，而无需用户坐下来并监视进度栏。 将 [DeviceServicingTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308965) 用于设备服务，将 [DeviceUseTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308967) 用于内容同步。 请注意这些后台任务将限制应用程序可以在后台运行，它不用于允许无限期的操作或无限同步的时间量。 有关详细信息，请参阅[设备同步和适用于 UWP 的设备应用程序更新](device-sync-and-update-for-uwp-device-apps.md)。

**请注意**   [DeviceUseTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308967)，不需要设备同步的设备元数据。

 

## <a name="span-idautoplayforwindowsstoredeviceappsspanspan-idautoplayforwindowsstoredeviceappsspanspan-idautoplayforwindowsstoredeviceappsspanautoplay-for-uwp-device-apps"></a><span id="AutoPlay_for_Windows_Store_device_apps"></span><span id="autoplay_for_windows_store_device_apps"></span><span id="AUTOPLAY_FOR_WINDOWS_STORE_DEVICE_APPS"></span>适用于 UWP 设备应用的自动播放


你可以配置 UWP 设备应用以在外围设备插入到 PC （在安装应用） 后自动启动。 在 Windows 8.1 的设备应用程序的自动播放添加人体学接口设备 (HID)、 智能卡和常规端口的支持。 有关详细信息，请参阅[UWP 设备应用程序的自动播放](autoplay-for-uwp-device-apps.md)。

## <a name="span-idprintercapabilitiesspanspan-idprintercapabilitiesspanspan-idprintercapabilitiesspanprinter-capabilities"></a><span id="Printer_capabilities"></span><span id="printer_capabilities"></span><span id="PRINTER_CAPABILITIES"></span>打印机功能


在 Windows 8.1 中 UWP 设备应用程序可以管理打印作业并执行打印机维护任务。 有关详细信息请参阅[如何管理打印作业](how-to-manage-print-jobs.md)并[如何执行打印机维护](how-to-do-printer-maintenance.md)。

您可以看到这些功能在新的示例中，突出显示[打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)。 打印机扩展库，包含与此示例，包装 COM 接口 PrinterExtensionLib COM 的实现。 此库旨在轻松地在 UWP 设备应用中重复使用。

## <a name="span-iduserexperiencechangesspanspan-iduserexperiencechangesspanspan-iduserexperiencechangesspanuser-experience-changes"></a><span id="User_experience_changes"></span><span id="user_experience_changes"></span><span id="USER_EXPERIENCE_CHANGES"></span>用户体验更改


若要提供与 Windows 8.1 上安装其他 UWP 应用一致的体验，UWP 设备应用程序不固定到**启动**安装时。 从**启动**，用户可以往下轻扫向上 （从屏幕的中央） 若要查看所有应用，包括最近安装的 UWP 设备应用程序。

内置相机应用程序不再包括 Windows 8.1**选项**按钮。 这意味着从 UWP 设备应用自定义的照相机选项浮出控件不会显示在该应用。 但是，所使用的任何其他 UWP 应用**Windows.Media.Capture.CameraCaptureUI**类仍然可以提供有关自定义浮出控件**更多选项**，当安装时。

 

 





