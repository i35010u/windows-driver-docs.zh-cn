---
title: 在 Windows 8.1 中创建设备后台任务
description: 本主题介绍如何创建使用 DeviceUseTrigger 或 DeviceServicingTrigger 的设备后台任务。
ms.assetid: 34263DB8-BB42-480B-AF7F-CC45772E6E84
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdfcdd404a6459877a869c157019ea2dfd5c421e
ms.sourcegitcommit: 68c99026bf38b864867ee3751d05459743ea8e11
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2020
ms.locfileid: "92434678"
---
# <a name="creating-a-device-background-task-in-windows-81-uwp-device-apps"></a>在 Windows 8.1 (UWP 设备应用中创建设备后台任务) 


在 Windows 8.1 中，UWP 应用可以同步外围设备上的数据。 如果你的应用程序与设备元数据相关联，则 UWP 设备应用还可以执行设备更新，例如固件更新。 本主题介绍如何创建使用 [DeviceUseTrigger](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) 或 [DeviceServicingTrigger](/uwp/api/Windows.ApplicationModel.Background.DeviceServicingTrigger)的设备后台任务。 使用这些触发器的设备后台代理需遵守确保用户同意的策略，并在同步和更新设备时帮助保持电池寿命。 有关设备后台任务的详细信息，请参阅 [UWP 设备应用的设备同步和更新](device-sync-and-update-for-uwp-device-apps.md)。

**注意**  本主题对应于 [自定义 USB 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=301975)。 自定义 USB 设备示例演示了使用 DeviceUseTrigger 执行设备同步的后台任务。



尽管 [自定义 USB 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=301975) 中的设备后台任务具有 DeviceUseTrigger，但本主题中讨论的所有内容也可应用于使用 DeviceServicingTrigger 的设备后台任务。 使用这两个触发器的唯一区别是 Windows 进行的策略检查。

## <a name="span-idthe_app_manifestspanspan-idthe_app_manifestspanspan-idthe_app_manifestspanthe-app-manifest"></a><span id="The_app_manifest"></span><span id="the_app_manifest"></span><span id="THE_APP_MANIFEST"></span>应用程序清单


若要使用设备后台任务，你的应用程序必须在前台应用程序的应用程序清单文件中声明它，就像是针对系统触发的后台任务完成的。 有关详细信息，请参阅 [UWP 设备应用的设备同步和更新](device-sync-and-update-for-uwp-device-apps.md)。

在此示例中，从应用程序包清单文件， **DeviceLibrary. SyncContent** 是前台应用的入口点。 **DeviceLibrary. SyncContent** 是使用 [DeviceUseTrigger](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger)的后台任务的入口点。

```XML
<Extensions>
  <Extension Category="windows.backgroundTasks" EntryPoint="DeviceLibrary.SyncContent">
    <BackgroundTasks>
      <m2:Task Type="deviceUse" /> 
    </BackgroundTasks>
  </Extension>
</Extensions>
```

## <a name="span-idthe_device_background_taskspanspan-idthe_device_background_taskspanspan-idthe_device_background_taskspanthe-device-background-task"></a><span id="The_device_background_task"></span><span id="the_device_background_task"></span><span id="THE_DEVICE_BACKGROUND_TASK"></span>设备后台任务


设备后台任务类实现 `IBackgroundTask` 接口，并包含您创建的用于同步或更新外围设备的实际代码。 当后台任务触发时，将执行后台任务类，并从应用程序的应用程序清单中提供的入口点执行。

[自定义 USB 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=301975 )中的 device background 类包含使用[DeviceUseTrigger](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger)后台任务执行到 USB 设备的同步的代码。 有关完整的详细信息，请下载该示例。 有关实现 `IBackgroundTask` 和 Windows 的后台任务基础结构的详细信息，请参阅 [支持应用的后台任务](/previous-versions/windows/apps/hh977056(v=win.10))。

[自定义 USB 设备](https://go.microsoft.com/fwlink/p/?LinkId=301975 )中的设备后台任务的关键部分包括：

1.  `IoSyncBackgroundTask`类实现 `IBackgroundTask` Windows 后台任务基础结构所需的接口。

2.  `IoSyncBackgroundTask`类获取 `DeviceUseDetails` 传递给类的 Run 方法中的类的实例 `IoSyncBackgroundTask` ，并使用此实例向 Microsoft Store 的应用程序报告进度并注册取消事件。

3.  `IoSyncBackgroundTask`类的 Run 方法还 `OpenDevice` `WriteToDeviceAsync` 会调用实现后台设备同步代码的私有方法和方法。

## <a name="span-idthe_foreground_appspanspan-idthe_foreground_appspanspan-idthe_foreground_appspanthe-foreground-app"></a><span id="The_foreground_app"></span><span id="the_foreground_app"></span><span id="THE_FOREGROUND_APP"></span>前景应用


[自定义 USB 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=301975 )中的前台应用会注册并触发使用[DeviceUseTrigger](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger)的设备后台任务。 本部分概述了前台应用注册、触发和处理设备后台任务的进度所需的步骤。

[自定义 USB 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=301975 )中的前景应用执行以下步骤以使用设备后台任务：

1.  创建新的 [DeviceUseTrigger](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) 和 `BackgroundTaskRegistration` 对象。

2.  检查此应用是否之前已注册了任何后台任务，并通过对任务调用 [BackgroundTaskRegistration](/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskRegistration) 方法来取消它们。

3.  私有 `SetupBackgroundTask` 方法注册将与设备同步的后台任务。 在 `SetupBackgroundTask` `SyncWithDeviceAsync` 下一步中，从方法调用方法。

    1.  初始化 `DeviceUseTrigger` 并保存它以供以后使用。
    2.  创建一个新的 `BackgroundTaskBuilder` 对象，并使用其 `Name` 、 `TaskEntryPoint` 和 `SetTrigger` 属性和方法来注册应用程序的 `DeviceUseTrigger` 对象和后台任务名称。 `BackgroundTaskBuilder`对象的 `TaskEntryPoint` 属性设置为触发后台任务时要运行的后台任务类的全名。
    3.  在后台任务中注册完成和进度事件，使前台应用程序可以为用户提供完成和进度更新。

4.  私有 `SyncWithDeviceAsync` 方法将注册将与设备同步的后台任务，并启动后台同步。

    1.  `SetupBackgroundTask`从上一步中调用方法，并注册将与设备同步的后台任务。
    2.  调用私有 `StartSyncBackgroundTaskAsync` 方法，该方法可启动后台任务。 该方法将关闭应用程序的设备句柄，以确保后台任务在启动时能够打开设备。

        **重要提示**  后台任务需要打开设备以执行更新，因此，在调用之前，前台应用程序必须关闭与设备的连接 `RequestAsync` 。




    接下来，该 `StartSyncBackgroundTaskAsync` 方法调用 `DeviceUseTrigger` 对象的 `RequestAsync` 方法，该方法将触发后台任务并返回 `DeviceTriggerResults` 对象，该对象 `RequestAsync` 用于确定后台任务是否成功启动。

    **重要提示**  Windows 将进行检查以确保所有必要的任务启动策略检查已完成。 如果所有策略检查都已完成，则更新操作现在作为前台应用的后台任务运行，从而允许在操作正在进行时安全挂起应用。 如果不再满足这些要求，Windows 还将强制实施任何运行时要求并取消后台任务。



3.  最后，此 `SyncWithDeviceAsync` 方法使用 `DeviceTriggerResults` 从返回的对象 `StartSyncBackgroundTaskAsync` 来确定是否已成功启动后台任务。 Switch 语句用于检查中的结果 `DeviceTriggerResults`


5.  前景应用实现一个专用 `OnSyncWithDeviceProgress` 事件处理程序，该处理程序将使用设备后台任务中的进度更新应用程序 UI。

6.  前台应用实现了一个专用 `OnSyncWithDeviceCompleted` 事件处理程序，用于处理后台任务完成时从后台任务过渡到前台应用的操作。

    1.  使用 `CheckResults` 对象的方法 `BackgroundTaskCompletedEventArgs` 来确定由后台任务引发的任何异常。
    2.  前台应用会重新打开设备供应用使用，现在后台任务已完成，并更新 UI 以通知用户。

7.  前景应用实现专用按钮单击 UI 中的事件处理程序以启动和取消后台任务。

    1.  专用 `Sync_Click` 事件处理程序调用 `SyncWithDeviceAsync` 前面步骤中描述的方法。
    2.  专用 `CancelSync_Click` 事件处理程序调用私有 `CancelSyncWithDevice` 方法来取消后台任务。

8.  私有 `CancelSyncWithDevice` 方法取消注册并取消任何活动设备同步，以便可以使用 [BackgroundTaskRegistration](/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskRegistration) 方法重新打开设备。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[自定义 USB 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=301975 )

[UWP 设备应用的设备同步和更新](device-sync-and-update-for-uwp-device-apps.md)

[Launching, resuming, and multitasking](/previous-versions/windows/apps/hh770837(v=win.10))

[通过后台任务支持您的应用程序](/previous-versions/windows/apps/hh977056(v=win.10))