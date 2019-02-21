---
title: 在 Windows 8.1 中创建设备后台任务
description: 本主题介绍如何创建使用 DeviceUseTrigger 或 DeviceServicingTrigger 设备后台任务。
ms.assetid: 34263DB8-BB42-480B-AF7F-CC45772E6E84
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f47e173582c5007bb8ac90310926fd19ff49a2d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541405"
---
# <a name="creating-a-device-background-task-in-windows-81-uwp-device-apps"></a>在 Windows 8.1 （UWP 设备应用） 中创建设备后台任务


在 Windows 8.1，UWP 应用可以同步外围设备上的数据。 如果你的应用程序与设备元数据，该 UWP 设备应用还可以执行设备更新，例如固件更新。 本主题介绍如何创建使用的设备后台任务[DeviceUseTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308967)或[DeviceServicingTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308965)。 正在同步，并更新，设备使用这些触发器的后台代理将受到策略，确保用户同意和帮助保留的电池使用寿命，在设备时。 有关设备后台任务的详细信息，请参阅[设备同步和适用于 UWP 的设备应用程序更新](device-sync-and-update-for-uwp-device-apps.md)。

**请注意**本主题对应于[自定义 USB 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=301975 )。 自定义 USB 设备示例演示一个执行 DeviceUseTrigger 与设备同步的后台任务。 若要查看执行 DeviceServicingTrigger 的固件更新的后台任务的示例，请下载[固件更新 USB 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=309186)。



尽管设备背景中的任务[自定义 USB 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=301975 )功能 DeviceUseTrigger，本主题中介绍的所有内容也应用于设备的后台任务，使用 DeviceServicingTrigger。 使用两个触发器的唯一区别是所做的 Windows 策略检查。

## <a name="span-idtheappmanifestspanspan-idtheappmanifestspanspan-idtheappmanifestspanthe-app-manifest"></a><span id="The_app_manifest"></span><span id="the_app_manifest"></span><span id="THE_APP_MANIFEST"></span>应用程序清单


若要使用的设备后台任务，您的应用程序必须在前台应用程序的应用清单文件中声明，如完成的系统触发后台任务。 有关详细信息，请参阅[设备同步和适用于 UWP 的设备应用程序更新](device-sync-and-update-for-uwp-device-apps.md)。

在此示例中的应用程序包清单文件中，从**DeviceLibrary.SyncContent**是从前台应用程序入口点。 **DeviceLibrary.SyncContent**是使用的后台任务的入口点[DeviceUseTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308967)。

```XML
<Extensions>
  <Extension Category="windows.backgroundTasks" EntryPoint="DeviceLibrary.SyncContent">
    <BackgroundTasks>
      <m2:Task Type="deviceUse" /> 
    </BackgroundTasks>
  </Extension>
</Extensions>
```

## <a name="span-idthedevicebackgroundtaskspanspan-idthedevicebackgroundtaskspanspan-idthedevicebackgroundtaskspanthe-device-background-task"></a><span id="The_device_background_task"></span><span id="the_device_background_task"></span><span id="THE_DEVICE_BACKGROUND_TASK"></span>设备后台任务


设备后台任务类实现`IBackgroundTask`接口并包含到任一同步创建或更新外围设备的实际代码。 触发后台任务时，从你的应用的应用程序清单中提供的入口点执行后台任务类。

中的设备背景类[自定义 USB 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=301975 )包含用于执行同步到 USB 设备使用的代码[DeviceUseTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308967)后台任务。 有关完整详细信息，下载的示例。 有关实现详细信息`IBackgroundTask`，请参阅 Windows 的后台任务基础结构[支持使用后台任务对应用程序](https://go.microsoft.com/fwlink/p/?LinkID=254337)。

密钥部分中的设备后台任务[自定义 USB 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=301975 )包括：

1.  `IoSyncBackgroundTask`类实现`IBackgroundTask`Windows 后台任务基础结构所需的接口。

2.  `IoSyncBackgroundTask`类获取`DeviceUseDetails`实例传递给中的类`IoSyncBackgroundTask`类的 Run 方法，并使用此实例与报表进行备份到 Microsoft Store 应用，以及如何取消事件注册。

3.  `IoSyncBackgroundTask`类的 Run 方法还会调用私有`OpenDevice`和`WriteToDeviceAsync`方法来实现后台设备同步的代码。

## <a name="span-idtheforegroundappspanspan-idtheforegroundappspanspan-idtheforegroundappspanthe-foreground-app"></a><span id="The_foreground_app"></span><span id="the_foreground_app"></span><span id="THE_FOREGROUND_APP"></span>前台应用程序


在前台应用程序[自定义 USB 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=301975 )注册，并触发使用的设备后台任务[DeviceUseTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308967)。 本部分概述了前台应用程序进行注册，触发器并将处理设备后台任务的进度的步骤。

在前台应用程序[自定义 USB 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=301975 )将执行以下步骤以使用设备后台任务：

1.  创建新[DeviceUseTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308967)和`BackgroundTaskRegistration`对象。

2.  检查以确定的任何后台任务之前是否已注册此应用，并通过调用取消它们[BackgroundTaskRegistration.Unregister](https://go.microsoft.com/fwlink/p/?LinkId=309315)任务方法。

3.  私有`SetupBackgroundTask`方法与设备注册将同步的后台任务。 `SetupBackgroundTask`方法从调用`SyncWithDeviceAsync`下一步中的方法。

    1.  初始化`DeviceUseTrigger`并将其保存以供将来使用。
    2.  创建一个新`BackgroundTaskBuilder`对象，并使用其`Name`，`TaskEntryPoint`并`SetTrigger`属性和方法来注册应用程序的`DeviceUseTrigger`对象和后台任务名称。 `BackgroundTaskBuilder`对象的`TaskEntryPoint`属性设置为触发后台任务时都会运行的后台任务类的全名。
    3.  注册的完成和从后台任务的进度事件，以便前台应用程序可以向用户提供完成和正在进行更新。

4.  私有`SyncWithDeviceAsync`方法注册的后台任务，将设备与同步启动后台同步。

    1.  调用`SetupBackgroundTask`前一步骤中的方法，并注册该设备将同步的后台任务。
    2.  调用私有`StartSyncBackgroundTaskAsync`启动后台任务的方法。 方法关闭设备以确保后台任务的应用程序的句柄可以在启动时打开设备。

        **重要**后台任务将需要打开设备以执行更新，因此前台应用程序必须关闭其连接到设备之前，调用`RequestAsync`。




    下一步，`StartSyncBackgroundTaskAsync`方法调用`DeviceUseTrigger`对象的`RequestAsync`方法，这将启动触发后台任务，并返回`DeviceTriggerResults`对象从`RequestAsync`用于确定是否已成功启动后台任务。

    **重要**Windows 进行检查以确保所有必需的任务启动策略检查已完成。 如果所有策略都检查都已完成更新操作现在作为后台任务之外前台应用程序，可通过应用程序安全地挂起操作正在进行时运行。 Windows 还将强制执行任何运行时要求，并取消后台任务，如果不再满足这些要求。



3.  最后，`SyncWithDeviceAsync`方法使用`DeviceTriggerResults`从返回的对象`StartSyncBackgroundTaskAsync`以确定是否已成功启动后台任务。 Switch 语句用于检查的结果 `DeviceTriggerResults`


5.  前台应用程序实现私有`OnSyncWithDeviceProgress`事件处理程序将从设备后台任务的进度更新应用程序 UI。

6.  前台应用程序实现私有`OnSyncWithDeviceCompleted`事件处理程序以处理从后台任务转换为前台应用程序时的后台任务已完成。

    1.  使用`CheckResults`方法的`BackgroundTaskCompletedEventArgs`对象，以确定是否的后台任务引发任何异常。
    2.  现在，后台任务已完成并更新 UI 以通知用户，前台应用程序重新打开适用于使用的设备应用程序的情况。

7.  前台应用程序实现专用按钮单击事件处理程序从用户界面来启动和取消后台任务。

    1.  私有`Sync_Click`事件处理程序调用`SyncWithDeviceAsync`上一步骤中所述的方法。
    2.  私有`CancelSync_Click`事件处理程序调用私有`CancelSyncWithDevice`方法来取消后台任务。

8.  私有`CancelSyncWithDevice`方法中注销，并取消任何活动设备同步，因此可以通过重新打开该设备[BackgroundTaskRegistration.Unregister](https://go.microsoft.com/fwlink/p/?LinkId=309315)方法。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[自定义的 USB 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=301975 )

[固件更新 USB 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=309186)

[设备同步和 UWP 的设备应用程序的更新](device-sync-and-update-for-uwp-device-apps.md)

[启动、 恢复和多任务](https://go.microsoft.com/fwlink/p/?LinkId=309316)

[支持使用后台任务对应用程序](https://go.microsoft.com/fwlink/p/?LinkID=254337)










