---
title: 设备同步和 Windows 8.1 应用商店设备应用的更新
description: 在 Windows 8.1 中，UWP 应用可以使用设备后台任务来同步外围设备上的数据。
ms.assetid: AA6E0760-F048-4BDC-8429-D119A531CED6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad38e4fc6ca929f5323d0fe6abe064e7096d6431
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391367"
---
# <a name="device-sync-and-update-for-store-device-apps-in-windows-81"></a>设备同步和 Windows 8.1 应用商店设备应用的更新


在 Windows 8.1 中，UWP 应用可以使用设备后台任务来同步外围设备上的数据。 如果应用与设备元数据相关联，则该 UWP 设备应用还可以使用设备后台代理进行设备更新，例如固件更新。 正在同步，并更新，设备后台代理将受到策略，确保用户同意和帮助设备时保持电池寿命。

若要执行设备同步和更新操作，创建一个设备后台任务，使用[DeviceUseTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308967)并[DeviceServicingTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308965)分别。 若要了解如何做到这一点与[自定义 USB 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=301975 )并[固件更新 USB 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=309186)，请参阅[创建的设备后台任务](how-to-create-a-device-background-task.md)。

**请注意**  Windows 运行时设备 Api 不需要的设备元数据。 这意味着您的应用程序不必是一个 UWP 设备应用来使用它们。 UWP 应用可以使用这些 Api 来访问 USB、 人体学接口设备 (HID)、 蓝牙设备和的详细信息。 有关详细信息，请参阅[集成设备](https://go.microsoft.com/fwlink/p/?LinkId=533279)。

 

## <a name="span-iddevicebackgroundtaskoverviewspanspan-iddevicebackgroundtaskoverviewspanspan-iddevicebackgroundtaskoverviewspandevice-background-task-overview"></a><span id="Device_background_task_overview_"></span><span id="device_background_task_overview_"></span><span id="DEVICE_BACKGROUND_TASK_OVERVIEW_"></span>设备后台任务概述


当用户移 UWP 应用屏外时，Windows 将挂起你的应用程序的内存中。 这样就有前景的另一个应用。 当挂起应用程序时，它是驻留在内存和 Windows 已停止，则从正在运行。 当发生这种情况，而无需设备后台任务，帮助将中断任何正在进行设备操作，例如同步和更新。 Windows 8.1 提供两个新后台任务的触发器让应用在后台，安全地执行同步和更新外围设备上进行长时间运行的操作，即使您的应用程序被挂起：DeviceUseTrigger 和 DeviceServicingTrigger。 有关应用程序暂挂的详细信息，请参阅[Launching，resuming，和多任务处理](https://go.microsoft.com/fwlink/p/?LinkId=309316)。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">后台任务触发器</th>
<th align="left">要求设备元数据</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="https://go.microsoft.com/fwlink/p/?LinkID=308967" data-raw-source="[DeviceUseTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308967)">DeviceUseTrigger</a></td>
<td align="left"></td>
<td align="left">长时间运行同步操作到或从外围设备的应用程序被挂起时启用。 同步在后台设备要求您的用户已批准后台同步你的应用。 你的设备还必须连接到或与通过 active I/O 在 PC 配对，并且允许最多 10 分钟的后台活动。 本主题后面将介绍有关策略实施的更多详细信息。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://go.microsoft.com/fwlink/p/?LinkID=308965" data-raw-source="[DeviceServicingTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308965)">DeviceServicingTrigger</a></td>
<td align="left"><img src="images/ap-tools.png" alt="DeviceServicingTrigger requires device metadata." /></td>
<td align="left">启用长时间运行的设备更新，例如设置传输或固件更新，您的应用程序被挂起时。 更新你的设备在后台，需要用户批准每次使用时的后台任务。 与 DeviceUseTrigger 后台任务，不同 DeviceServicingTrigger 后台任务允许设备重启和断开连接并允许最多 30 分钟的后台活动。 本主题后面将介绍有关策略实施的更多详细信息。</td>
</tr>
</tbody>
</table>

 

DeviceServicingTrigger 需要设备元数据，因为该应用程序必须指定为特权的应用，才能执行设备更新操作。

### <a name="span-idappprivilegespanspan-idappprivilegespanspan-idappprivilegespanapp-privilege"></a><span id="App_privilege"></span><span id="app_privilege"></span><span id="APP_PRIVILEGE"></span>应用权限

只能由特权的应用程序，可以执行一些重要的设备操作，如长时间运行的设备更新。 一个*特权的应用*是设备制造商已授权来执行这些操作的应用程序。 设备元数据指定哪些应用程序，如果有，已被指定为特权的应用程序的设备。

如果使用设备元数据向导创建设备元数据，在指定您的应用程序**指定 UWP 设备应用信息**页。 有关详细信息，请参阅[步骤 2:创建 UWP 设备应用的设备元数据](step-2--create-device-metadata.md)。

## <a name="span-idsupportedprotocolsspanspan-idsupportedprotocolsspanspan-idsupportedprotocolsspansupported-protocols"></a><span id="Supported_protocols"></span><span id="supported_protocols"></span><span id="SUPPORTED_PROTOCOLS"></span>支持的协议


设备的后台任务，使用 DeviceUseTrigger 和 DeviceServicingTrigger 让您通过不受系统触发任务通常由 UWP 应用使用的协议与外围设备进行通信的应用程序。

| 协议         | DeviceServicingTrigger                                                   | DeviceUseTrigger                                                                         | 系统触发器                                                                       |
|------------------|--------------------------------------------------------------------------|------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
| USB              | ![deviceservicingtrigger 支持 usb](images/ap-tools.png)              | ![deviceusetrigger 支持 usb](images/ap-tools.png)                                    | ![系统触发器不支持 usb](images/app-tools-doesnotapply.png)              |
| HID              | ![hid deviceservicingtrigger 支持](images/ap-tools.png)              | ![hid deviceusetrigger 支持](images/ap-tools.png)                                    | ![不支持系统触发器 hid](images/app-tools-doesnotapply.png)              |
| 蓝牙 RFCOMM | ![deviceservicingtrigger 支持蓝牙 rfcomm](images/ap-tools.png) | ![deviceusetrigger 支持蓝牙 rfcomm](images/ap-tools.png)                       | ![系统触发器不支持蓝牙 rfcomm](images/app-tools-doesnotapply.png) |
| 蓝牙 GATT   | ![deviceservicingtrigger 支持蓝牙 gatt](images/ap-tools.png)   | ![deviceusetrigger 支持蓝牙 gatt](images/ap-tools.png)                         | ![系统触发器不支持蓝牙 gatt](images/app-tools-doesnotapply.png)   |
| MTP              | ![deviceservicingtrigger 支持 mtp](images/ap-tools.png)              | ![deviceusetrigger 不支持 mtp](images/app-tools-doesnotapply.png)              | ![系统触发器不支持 mtp](images/app-tools-doesnotapply.png)              |
| 有线网络    | ![deviceservicingtrigger 支持有线网络](images/ap-tools.png)    | ![deviceusetrigger 不支持有线网络](images/app-tools-doesnotapply.png)    | ![系统触发器不支持有线网络](images/app-tools-doesnotapply.png)    |
| WLAN 网络    | ![deviceservicingtrigger 支持的 wi-fi 网络](images/ap-tools.png)  | ![deviceusetrigger 不支持的 wi-fi 网络](images/app-tools-doesnotapply.png)  | ![系统触发器不支持网络的 wi-fi](images/app-tools-doesnotapply.png)    |
| IDeviceIOControl | ![DeviceServicingTrigger 支持 IDeviceIOControl](images/ap-tools.png) | ![deviceusetrigger 不支持 ideviceiocontrol](images/app-tools-doesnotapply.png) | ![系统触发器不支持 ideviceiocontrol](images/app-tools-doesnotapply.png) |

 

## <a name="span-idregisteringbackgroundtasksintheapppackagemanifestspanspan-idregisteringbackgroundtasksintheapppackagemanifestspanspan-idregisteringbackgroundtasksintheapppackagemanifestspanregistering-background-tasks-in-the-app-package-manifest"></a><span id="Registering_background_tasks_in_the_app_package_manifest"></span><span id="registering_background_tasks_in_the_app_package_manifest"></span><span id="REGISTERING_BACKGROUND_TASKS_IN_THE_APP_PACKAGE_MANIFEST"></span>注册应用包清单中的后台任务


你的应用将在运行后台任务期间以代码的形式执行同步和更新操作。 此代码将嵌入的 Windows 运行时类中实现 IBackgroundTask （或在专用的 JavaScript 页面适用于 JavaScript 应用中）。 若要使用的设备后台任务，您的应用程序必须将其声明在前台应用程序，像处理系统触发后台任务的应用清单文件中。

在此示例中的应用程序包清单文件， **DeviceLibrary.SyncContent**并**DeviceLibrary.UpdateFirmware**是从前台应用程序的入口点。 **DeviceLibrary.SyncContent**是使用的后台任务的入口点[DeviceUseTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308967)。 **DeviceLibrary.UpdateFirmware**是使用的后台任务的入口点[DeviceServicingTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308965)。

```XML
<Extensions>
  <Extension Category="windows.backgroundTasks" EntryPoint="DeviceLibrary.SyncContent">
    <BackgroundTasks>
      <m2:Task Type="deviceUse" /> 
    </BackgroundTasks>
  </Extension>
  <Extension Category="windows.backgroundTasks" EntryPoint="DeviceLibrary.UpdateFirmware">
    <BackgroundTasks>
      <m2:Task Type="deviceServicing" /> 
    </BackgroundTasks>
  </Extension>
</Extensions>
```

## <a name="span-idusingyourdevicewithdevicebackgroundtasksspanspan-idusingyourdevicewithdevicebackgroundtasksspanspan-idusingyourdevicewithdevicebackgroundtasksspanusing-your-device-with-device-background-tasks"></a><span id="Using_your_device_with_device_background_tasks"></span><span id="using_your_device_with_device_background_tasks"></span><span id="USING_YOUR_DEVICE_WITH_DEVICE_BACKGROUND_TASKS"></span>使用你的设备通过设备后台任务


若要开发应用程序以利用 DeviceUseTrigger 和 DeviceServicingTrigger 后台任务，请执行下面这组基本步骤。 有关后台任务的详细信息，请参阅[支持使用后台任务对应用程序](https://go.microsoft.com/fwlink/p/?LinkID=254337)。

1.  你的应用在应用清单中注册其后台任务，并在实现 IBackgroundTask 的 Windows 运行时类或 JavaScript 应用的专用 JavaScript 页中嵌入后台任务代码。
2.  您的应用程序启动时，它将创建并配置适当的类型，DeviceUseTrigger 或 DeviceServicingTrigger，一个设备触发器对象以及存储触发器实例以供将来使用。
3.  您的应用程序检查后台任务先前已注册，是否没有，请将其注册针对设备触发器。 请注意，不允许你的应用为与此触发器关联的任务设置条件。
4.  当您的应用程序需要触发后台任务时，将设备触发器对象上调用 RequestAsync 激活方法。
5.  与其他系统后台任务不同，你的后台任务不会受到限制（无 CPU 时间配额），但运行优先级将会降低，从而保证前台应用的及时响应。
6.  然后，在开始执行该后台任务之前，Windows 将根据触发器类型验证是否符合必要的策略，包括是否就该操作请求用户同意。
7.  Windows 监控系统条件和任务运行情况，并在必要时（不再符合所需条件）取消该任务。
8.  当后台任务报告进度或完成时，你的应用将通过该注册任务的进度事件和完成事件接收这些事件。

**重要**  时使用设备后台任务，请考虑以下要点：

-   能够以编程方式触发后台任务，从而使用 DeviceUseTrigger 和 DeviceServicingTrigger 在 Windows 8.1 中引入，并仅限于设备后台任务。

-   由 Windows 以确保用户同意的情况下，更新其外围设备时强制执行某些策略。 此外还会强制执行其他策略，其目的是为了在同步和更新外围设备时维持用户的电池使用寿命。

-   不再满足某些策略要求，包括最长背景时间 （时钟时间） 时，Windows 可能会取消使用 DeviceUseTrigger 和 DeviceServicingTrigger 的后台任务。 使用这些后台任务与外围设备交互时考虑这些策略要求很重要。

 

**提示**  若要查看这些后台任务的工作原理，请下载一个示例。 [自定义 USB 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=301975 )演示一个执行 DeviceUseTrigger 与设备同步的后台任务。 [固件更新 USB 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=309186)演示一个执行 DeviceServicingTrigger 的固件更新的后台任务。

 

## <a name="span-iduserconsentspanspan-iduserconsentspanspan-iduserconsentspanuser-consent"></a><span id="User_consent"></span><span id="user_consent"></span><span id="USER_CONSENT"></span>用户同意


使用 DeviceUseTrigger 或 DeviceServicingTrigger 时，Windows 8.1 强制实施策略，以确保在用户给予您应用的权限来访问其设备在后台进行同步和更新内容。 策略也会强制为保护用户的电池使用时间同步和更新外围设备时。

### <a name="span-iddevicesyncuserconsentspanspan-iddevicesyncuserconsentspanspan-iddevicesyncuserconsentspandevice-sync-user-consent"></a><span id="Device_sync_user_consent"></span><span id="device_sync_user_consent"></span><span id="DEVICE_SYNC_USER_CONSENT"></span>设备同步用户同意

使用 DeviceUseTrigger 的后台任务需要一次性用户许可允许您的应用程序在后台同步。 此许可是存储的每个应用，每个设备模型。 用户表示许可后，若要让应用能够访问在后台中的设备，就像他们同意该应用位于前台时让应用访问设备。

在以下示例中，名为 Tailspin Toys 的应用获取用户的权限在后台同步。

![设备同步用户同意的情况下消息对话框](images/devicesyncuserconsent.png)

如果用户稍后改变了主意，它们可以撤消在设置中的权限。

![设备同步的权限设置对话框](images/devicesyncapppermissions.png)

### <a name="span-iddeviceupdateuserconsentspanspan-iddeviceupdateuserconsentspanspan-iddeviceupdateuserconsentspandevice-update-user-consent"></a><span id="Device_update_user__consent"></span><span id="device_update_user__consent"></span><span id="DEVICE_UPDATE_USER__CONSENT"></span>设备更新用户同意

与那些使用 DeviceUseTrigger，使用 DeviceServicingTrigger 后台任务的后台任务需要用户同意的情况下每次触发后台任务。 并且是 DeviceUseTrigger 不存储此许可。 这是时间的因为所涉及的设备固件更新的较高风险操作和段较长所需的设备更新。 除了获得用户同意的情况下，Windows 将向用户提供有关设备更新，例如一条警告，以保持整个更新连接的设备，并确保 PC 收费和操作的近似的运行时间的信息 (如果您的应用程序提供了它）。

![设备更新用户同意的情况下消息对话框](images/deviceupdateuserconsent.png)

## <a name="span-idfrequencyandforegroundrestrictionsspanspan-idfrequencyandforegroundrestrictionsspanspan-idfrequencyandforegroundrestrictionsspanfrequency-and-foreground-restrictions"></a><span id="Frequency_and_foreground_restrictions"></span><span id="frequency_and_foreground_restrictions"></span><span id="FREQUENCY_AND_FOREGROUND_RESTRICTIONS"></span>前景色的频率和限制


没有任何限制的频率与您的应用程序可以启动的操作，但您的应用程序可以只有一个 DeviceUseTrigger 或 DeviceServicingTrigger 后台任务操作一次运行 （这不影响其他类型的后台任务），并可以仅当你的应用位于前台时，请启动后台任务。 当您的应用程序不在前台中时，不能启动与 DeviceUseTrigger 或 DeviceServicingTrigger 的后台任务。 第一个后台任务完成之前，您的应用程序不能启动第二个设备后台任务。

## <a name="span-iddevicebackgroundtaskpoliciesspanspan-iddevicebackgroundtaskpoliciesspanspan-iddevicebackgroundtaskpoliciesspandevice-background-task-policies"></a><span id="Device_background_task_policies"></span><span id="device_background_task_policies"></span><span id="DEVICE_BACKGROUND_TASK_POLICIES"></span>后台任务的设备策略


当你的应用使用设备后台任务时，Windows 强制实施策略。 如果不符合这些策略，可能会取消使用 DeviceUseTrigger 或 DeviceServicingTrigger 的后台任务。 请务必使用设备后台任务与外围设备进行交互时需考虑这些策略要求。

### <a name="span-idtaskinitiationpoliciesspanspan-idtaskinitiationpoliciesspanspan-idtaskinitiationpoliciesspantask-initiation-policies"></a><span id="Task_initiation_policies"></span><span id="task_initiation_policies"></span><span id="TASK_INITIATION_POLICIES"></span>任务启动策略

此表指示策略应用于每个后台任务触发器的任务启动。

| 策略                                                                                                                                                                                                                               | DeviceServicingTrigger                       | DeviceUseTrigger                                            |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------|-------------------------------------------------------------|
| UWP 应用位于前台时触发后台任务。                                                                                                                                                     | ![策略适用](images/ap-tools.png)       | ![策略适用](images/ap-tools.png)                      |
| 你的设备已连接到系统 （或范围中的无线设备）。                                                                                                                                                           | ![策略适用](images/ap-tools.png)       | ![策略适用](images/ap-tools.png)                      |
| 当屏幕锁定时，你的后台任务每分钟消耗 400 毫秒的 CPU 时间（假设 1GHz CPU），或者当屏幕未锁定时，每五分钟消耗该时间。 未能满足此策略可能导致任务被取消。 | ![策略适用](images/ap-tools.png)       | ![策略适用](images/ap-tools.png)                      |
| 你的设备已使用设备的应用可以访问外围设备 Api (Windows 运行时 Api USB HID、 蓝牙，等等)。 如果您的应用程序无法访问设备，为后台任务的访问被拒绝。                  | ![策略适用](images/ap-tools.png)       | ![策略适用](images/ap-tools.png)                      |
| 在应用包部件清单中注册该应用提供的后台任务入口点。                                                                                                                                           | ![策略适用](images/ap-tools.png)       | ![策略适用](images/ap-tools.png)                      |
| 用户已获得的任务权限以继续。                                                                                                                                                                                  | 每次。                                  | 第一次，然后由应用权限控制。             |
| 该应用提供的时间估计值是短于 30 分钟。                                                                                                                                                                           | ![策略适用](images/ap-tools.png)       | ![策略不适用于](images/app-tools-doesnotapply.png) |
| 应用程序指定为特权的应用程序的设备。 （必须有完整的应用 ID 匹配项针对设备容器的设备元数据中的特权的应用列表。）                                                            | ![策略适用](images/ap-tools.png)       | ![策略不适用于](images/app-tools-doesnotapply.png) |
| 计算机有大于 33%电池剩余或者交流电源。                                                                                                                                                          | ![策略适用](images/ap-tools.png)       | ![策略不适用于](images/app-tools-doesnotapply.png) |
| 只有一个设备后台任务正在运行的每个操作类型。                                                                                                                                                                       | ![策略检查适用](images/ap-tools.png) | ![策略适用](images/ap-tools.png)                      |

 

### <a name="span-idruntimepolicychecksspanspan-idruntimepolicychecksspanspan-idruntimepolicychecksspanruntime-policy-checks"></a><span id="Runtime_policy_checks"></span><span id="runtime_policy_checks"></span><span id="RUNTIME_POLICY_CHECKS"></span>运行时策略检查

当你的任务在后台运行时，Windows 将强制执行以下运行时策略要求。 如果不能达到任意一项运行时要求，Windows 将取消你的设备后台任务。

此表指示哪种运行时策略应用于每个后台任务触发器。

| 策略检查                                                                                | DeviceServicingTrigger                                      | DeviceUseTrigger                             |
|---------------------------------------------------------------------------------------------|-------------------------------------------------------------|----------------------------------------------|
| 时钟时间限制 - 你的应用任务可以在后台运行的时间总量。 | 30 分钟                                                  | 10 分钟                                   |
| 你的设备已连接到系统 （或范围中的无线设备）。                  | ![策略不适用于](images/app-tools-doesnotapply.png) | ![策略检查适用](images/ap-tools.png) |
| 任务不断对设备执行常规 I/O （每隔 5 秒执行 1 次 I/O）。                       | ![策略不适用于](images/app-tools-doesnotapply.png) | ![策略检查适用](images/ap-tools.png) |
| 应用未取消任务。                                                              | ![策略检查适用](images/ap-tools.png)                | ![策略检查适用](images/ap-tools.png) |
| 应用未退出。                                                                         | ![策略检查适用](images/ap-tools.png)                | ![策略检查适用](images/ap-tools.png) |

 

## <a name="span-idbestpracticesspanspan-idbestpracticesspanspan-idbestpracticesspanbest-practices"></a><span id="Best_practices"></span><span id="best_practices"></span><span id="BEST_PRACTICES"></span>最佳做法


以下是适用于 UWP 设备应用使用设备后台任务的最佳做法。

### <a name="span-iddevicebackgroundtaskprogrammingmodelspanspan-iddevicebackgroundtaskprogrammingmodelspanspan-iddevicebackgroundtaskprogrammingmodelspandevice-background-task-programming-model"></a><span id="Device_background_task_programming_model"></span><span id="device_background_task_programming_model"></span><span id="DEVICE_BACKGROUND_TASK_PROGRAMMING_MODEL"></span>设备后台任务的编程模型

使用从您的应用程序的 DeviceUseTrigger 或 DeviceServicingTrigger 后台任务可确保任何同步或设备的更新将继续从前台应用程序启动的操作以在后台运行，如果你的用户切换应用程序，并挂起前台应用程序通过 Windows。 我们建议你按照这个整体模型注册、触发及注销后台任务：

1.  先注册后台任务，然后再请求触发。

2.  将进度事件处理程序和完成事件处理程序连接到你的触发器。 当你的应用从挂起状态恢复时，Windows 将为该应用提供可用于确定后台任务状态的任何排队等候处理的进度事件和完成事件。

3.  在触发 DeviceUseTrigger 或 DeviceServicingTrigger 后台任务，以便这些设备可以自由地打开和使用的后台任务时，请关闭任何打开的设备对象。

4.  注册触发器。

5.  完成任务时，取消注册后台任务。 后台任务完成后，可以取消注册后台任务和重新打开设备并使用它定期从 UWP 应用。

6.  从你的后台任务类注册取消事件。 注册取消事件后，当 Windows 或你的前台应用取消后台任务时，即可使用后台任务代码完全停止你运行的后台任务。

7.  在应用程序退出 （未暂停）、 注销并取消任何正在运行的任务。

    -   退出你的应用时，注销并取消所有运行中的任务。

    -   退出你的应用时，将取消你的后台任务并断开所有现有事件处理程序与现有后台任务的连接。 这样你就无需确定你的后台任务的状态。 通过对注销和取消所有后台任务，你即可利用取消代码完全停止后台任务。

**提示**  有关详细说明如何做到这一点与[自定义 USB 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=301975 )并[固件更新 USB 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=309186)，请参阅[创建设备后台任务](how-to-create-a-device-background-task.md)。

 

### <a name="span-idcancellingabackgroundtaskspanspan-idcancellingabackgroundtaskspanspan-idcancellingabackgroundtaskspancancelling-a-background-task"></a><span id="Cancelling_a_background_task"></span><span id="cancelling_a_background_task"></span><span id="CANCELLING_A_BACKGROUND_TASK"></span>正在取消后台任务

若要取消从前台应用程序在后台运行的任务，请使用取消注册方法上 BackgroundTaskRegistration 对象使用应用程序中注册或者[DeviceUseTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308967)或[DeviceServicingTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308965)后台任务。 通过使用 BackgroundTaskRegistration 上取消注册方法来注销后台任务将导致取消后台任务的后台任务基础结构。

取消注册方法另外采用一个布尔值 true 或 false 值，以指示如果当前正在运行的后台任务实例应取消但不允许他们完成。 有关详细信息，请参阅的 API 参考[BackgroundTaskRegistration.Unregister](https://go.microsoft.com/fwlink/p/?LinkId=309315)。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[创建设备后台任务](how-to-create-a-device-background-task.md)

[自定义的 USB 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=301975 )

[固件更新 USB 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=309186)

[启动、 恢复和多任务](https://go.microsoft.com/fwlink/p/?LinkId=309316)

[支持使用后台任务对应用程序](https://go.microsoft.com/fwlink/p/?LinkID=254337)

 

 






