---
title: Windows 8.1 中存储设备应用的设备同步和更新
description: 在 Windows 8.1 中，UWP 应用可以使用设备后台任务来同步外围设备上的数据。
ms.assetid: AA6E0760-F048-4BDC-8429-D119A531CED6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72f7650f190f649f42365c91f23b27a4d928fd98
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734469"
---
# <a name="device-sync-and-update-for-store-device-apps-in-windows-81"></a>Windows 8.1 中存储设备应用的设备同步和更新


在 Windows 8.1 中，UWP 应用可以使用设备后台任务来同步外围设备上的数据。 如果应用与设备元数据相关联，则该 UWP 设备应用还可以使用设备后台代理进行设备更新，例如固件更新。 设备后台代理受策略的限制，这些策略可确保用户同意，并有助于在同步和更新设备时保护电池寿命。

若要执行设备同步和更新操作，请分别创建使用 [DeviceUseTrigger](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) 和 [DeviceServicingTrigger](/uwp/api/Windows.ApplicationModel.Background.DeviceServicingTrigger)的设备后台任务。 若要了解如何使用 [自定义 usb 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=301975 ) 和 [固件更新 USB 设备示例](/samples/browse/)来完成此操作，请参阅 [创建设备后台任务](how-to-create-a-device-background-task.md)。

**注意**   Windows 运行时设备 Api 不需要设备元数据。 这意味着你的应用程序无需成为 UWP 设备应用即可使用它们。 UWP 应用可以使用这些 Api 来访问 USB、人体学接口设备 (HID) 、Bluetooth 设备等。 有关详细信息，请参阅 [集成设备](/previous-versions/windows/apps/dn263141(v=win.10))。

 

## <a name="span-iddevice_background_task_overview_spanspan-iddevice_background_task_overview_spanspan-iddevice_background_task_overview_spandevice-background-task-overview"></a><span id="Device_background_task_overview_"></span><span id="device_background_task_overview_"></span><span id="DEVICE_BACKGROUND_TASK_OVERVIEW_"></span>设备后台任务概述


当用户在屏幕上移动 UWP 应用时，Windows 将在内存中挂起应用。 这使另一个应用程序具有前台。 挂起应用程序时，该应用程序驻留在内存中，并且 Windows 已将其停止运行。 发生这种情况时，如果不使用设备后台任务，任何正在进行的设备操作（如同步和更新）都将中断。 Windows 8.1 提供了两个新的后台任务触发器，使你的应用程序在后台安全地执行长时间运行的同步和更新操作，即使你的应用程序已挂起： DeviceUseTrigger 和 DeviceServicingTrigger。 有关应用暂停的详细信息，请参阅 [启动、恢复和多任务](/previous-versions/windows/apps/hh770837(v=win.10))处理。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">后台任务触发器</th>
<th align="left">需要设备元数据</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="https://go.microsoft.com/fwlink/p/?LinkID=308967" data-raw-source="[DeviceUseTrigger](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger)">DeviceUseTrigger</a></td>
<td align="left"></td>
<td align="left">应用挂起时，对外围设备进行长时间运行的同步操作。 在后台同步设备要求用户已批准应用的后台同步。 设备还必须连接到电脑，或与 PC 配对，具有活动 i/o，最多允许10分钟的后台活动。 本主题后面将介绍有关策略实施的更多详细信息。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://go.microsoft.com/fwlink/p/?LinkID=308965" data-raw-source="[DeviceServicingTrigger](/uwp/api/Windows.ApplicationModel.Background.DeviceServicingTrigger)">DeviceServicingTrigger</a></td>
<td align="left"><img src="images/ap-tools.png" alt="DeviceServicingTrigger requires device metadata." /></td>
<td align="left">在应用挂起时，启用长时间运行的设备更新，例如设置传输或固件更新。 在后台更新设备需要在每次使用后台任务时进行用户批准。 与 DeviceUseTrigger 后台任务不同，DeviceServicingTrigger 后台任务允许设备重启和断开连接，并允许最多30分钟的后台活动。 本主题后面将介绍有关策略实施的更多详细信息。</td>
</tr>
</tbody>
</table>

 

DeviceServicingTrigger 需要设备元数据，因为必须将应用指定为特权应用才能执行设备更新操作。

### <a name="span-idapp_privilegespanspan-idapp_privilegespanspan-idapp_privilegespanapp-privilege"></a><span id="App_privilege"></span><span id="app_privilege"></span><span id="APP_PRIVILEGE"></span>应用特权

某些关键设备操作（如长时间运行的设备更新）只能由特权应用执行。 *特权应用*是设备制造商有权执行这些操作的应用。 设备元数据指定已指定为设备的特权应用的应用（如果有）。

当通过设备元数据向导创建设备元数据时，请在 " **指定 UWP 设备应用程序信息** " 页上指定您的应用程序。 有关详细信息，请参阅 [步骤2：创建 UWP 设备应用的设备元数据](step-2--create-device-metadata.md)。

## <a name="span-idsupported_protocolsspanspan-idsupported_protocolsspanspan-idsupported_protocolsspansupported-protocols"></a><span id="Supported_protocols"></span><span id="supported_protocols"></span><span id="SUPPORTED_PROTOCOLS"></span>支持的协议


使用 DeviceUseTrigger 和 DeviceServicingTrigger 的设备后台任务使应用程序可以通过不受 UWP 应用通常使用的系统触发任务不支持的协议与外围设备进行通信。

| 协议         | DeviceServicingTrigger                                                   | DeviceUseTrigger                                                                         | 系统触发器                                                                       |
|------------------|--------------------------------------------------------------------------|------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
| USB              | ![deviceservicingtrigger 支持 usb](images/ap-tools.png)              | ![deviceusetrigger 支持 usb](images/ap-tools.png)                                    | ![系统触发器不支持 usb](images/app-tools-doesnotapply.png)              |
| HID              | ![deviceservicingtrigger 支持 hid](images/ap-tools.png)              | ![deviceusetrigger 支持 hid](images/ap-tools.png)                                    | ![系统触发器不支持 hid](images/app-tools-doesnotapply.png)              |
| Bluetooth RFCOMM | ![deviceservicingtrigger 支持蓝牙 rfcomm](images/ap-tools.png) | ![deviceusetrigger 支持蓝牙 rfcomm](images/ap-tools.png)                       | ![系统触发器不支持蓝牙 rfcomm](images/app-tools-doesnotapply.png) |
| 蓝牙 GATT   | ![deviceservicingtrigger 支持蓝牙 gatt](images/ap-tools.png)   | ![deviceusetrigger 支持蓝牙 gatt](images/ap-tools.png)                         | ![系统触发器不支持蓝牙 gatt](images/app-tools-doesnotapply.png)   |
| MTP              | ![deviceservicingtrigger 支持 mtp](images/ap-tools.png)              | ![deviceusetrigger 不支持 mtp](images/app-tools-doesnotapply.png)              | ![系统触发器不支持 mtp](images/app-tools-doesnotapply.png)              |
| 有线网络    | ![deviceservicingtrigger 支持网络有线](images/ap-tools.png)    | ![deviceusetrigger 不支持网络有线](images/app-tools-doesnotapply.png)    | ![系统触发器不支持网络有线](images/app-tools-doesnotapply.png)    |
| WLAN 网络    | ![deviceservicingtrigger 支持网络 wi-fi](images/ap-tools.png)  | ![deviceusetrigger 不支持网络 wi-fi](images/app-tools-doesnotapply.png)  | ![系统触发器不支持网络 wi-fi](images/app-tools-doesnotapply.png)    |
| IDeviceIOControl | ![DeviceServicingTrigger 支持 IDeviceIOControl](images/ap-tools.png) | ![deviceusetrigger 不支持 ideviceiocontrol](images/app-tools-doesnotapply.png) | ![系统触发器不支持 ideviceiocontrol](images/app-tools-doesnotapply.png) |

 

## <a name="span-idregistering_background_tasks_in_the_app_package_manifestspanspan-idregistering_background_tasks_in_the_app_package_manifestspanspan-idregistering_background_tasks_in_the_app_package_manifestspanregistering-background-tasks-in-the-app-package-manifest"></a><span id="Registering_background_tasks_in_the_app_package_manifest"></span><span id="registering_background_tasks_in_the_app_package_manifest"></span><span id="REGISTERING_BACKGROUND_TASKS_IN_THE_APP_PACKAGE_MANIFEST"></span>在应用程序包清单中注册后台任务


你的应用将在运行后台任务期间以代码的形式执行同步和更新操作。 此代码嵌入在可实现 IBackgroundTask 的 Windows 运行时类中（或 JavaScript 应用的专用 JavaScript 页中）。 若要使用设备后台任务，你的应用程序必须在前台应用程序的应用程序清单文件中声明它，就像它用于系统触发的后台任务一样。

在应用程序包清单文件的此示例中，SyncContent 和**DeviceLibrary**是来自前台应用的入口点。 **DeviceLibrary. UpdateFirmware。** **DeviceLibrary. SyncContent** 是使用 [DeviceUseTrigger](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger)的后台任务的入口点。 **DeviceLibrary. UpdateFirmware** 是使用 [DeviceServicingTrigger](/uwp/api/Windows.ApplicationModel.Background.DeviceServicingTrigger)的后台任务的入口点。

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

## <a name="span-idusing_your_device_with_device_background_tasksspanspan-idusing_your_device_with_device_background_tasksspanspan-idusing_your_device_with_device_background_tasksspanusing-your-device-with-device-background-tasks"></a><span id="Using_your_device_with_device_background_tasks"></span><span id="using_your_device_with_device_background_tasks"></span><span id="USING_YOUR_DEVICE_WITH_DEVICE_BACKGROUND_TASKS"></span>在设备中使用设备后台任务


若要开发应用以利用 DeviceUseTrigger 和 DeviceServicingTrigger 后台任务，请遵循这一基本步骤。 有关后台任务的详细信息，请参阅 [通过后台任务支持应用](/previous-versions/windows/apps/hh977056(v=win.10))。

1.  你的应用在应用清单中注册其后台任务，并在实现 IBackgroundTask 的 Windows 运行时类或 JavaScript 应用的专用 JavaScript 页中嵌入后台任务代码。
2.  当你的应用程序启动时，它会创建并配置适当类型的设备触发器对象，无论是 DeviceUseTrigger 还是 DeviceServicingTrigger，并存储触发器实例供将来使用。
3.  应用检查后台任务是否之前已注册，如果不是，则会将其注册到设备触发器。 请注意，不允许你的应用为与此触发器关联的任务设置条件。
4.  当应用需要触发后台任务时，它会对设备触发器对象调用 RequestAsync 激活方法。
5.  与其他系统后台任务不同，你的后台任务不会受到限制（无 CPU 时间配额），但运行优先级将会降低，从而保证前台应用的及时响应。
6.  然后，在开始执行该后台任务之前，Windows 将根据触发器类型验证是否符合必要的策略，包括是否就该操作请求用户同意。
7.  Windows 监控系统条件和任务运行情况，并在必要时（不再符合所需条件）取消该任务。
8.  当后台任务报告进度或完成时，你的应用将通过该注册任务的进度事件和完成事件接收这些事件。

**重要提示**   使用设备后台任务时，请考虑以下要点：

-   在 Windows 8.1 中引入了使用 DeviceUseTrigger 和 DeviceServicingTrigger 的编程触发后台任务的功能，仅限于设备后台任务。

-   某些策略由 Windows 强制执行，以确保用户在更新其外围设备时得到同意。 此外还会强制执行其他策略，其目的是为了在同步和更新外围设备时维持用户的电池使用寿命。

-   当不再满足某些策略要求时，Windows 可能会取消使用 DeviceUseTrigger 和 DeviceServicingTrigger 的后台任务，包括 (时钟时间) 的最大后台时间量。 使用这些后台任务与外围设备交互时考虑这些策略要求很重要。

 

**提示**   若要查看这些后台任务的工作方式，请下载示例。 [自定义 USB 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=301975 )演示了使用 DeviceUseTrigger 执行设备同步的后台任务。 [固件更新 USB 设备示例](/samples/browse/)演示了使用 DeviceServicingTrigger 执行固件更新的后台任务。

 

## <a name="span-iduser_consentspanspan-iduser_consentspanspan-iduser_consentspanuser-consent"></a><span id="User_consent"></span><span id="user_consent"></span><span id="USER_CONSENT"></span>用户同意


当使用 DeviceUseTrigger 或 DeviceServicingTrigger 时，Windows 8.1 强制实施策略，以确保用户在后台访问其设备以同步和更新内容。 还会实施策略，以便在同步和更新外围设备时帮助保持用户电池寿命。

### <a name="span-iddevice_sync_user_consentspanspan-iddevice_sync_user_consentspanspan-iddevice_sync_user_consentspandevice-sync-user-consent"></a><span id="Device_sync_user_consent"></span><span id="device_sync_user_consent"></span><span id="DEVICE_SYNC_USER_CONSENT"></span>设备同步用户同意

使用 DeviceUseTrigger 的后台任务需要一次性用户同意，以允许应用在后台同步。 此同意存储于每个应用程序和每个设备模型。 用户同意允许应用程序在后台访问设备，就像他们同意允许应用在应用程序处于前台时访问设备。

在以下示例中，名为 Tailspin 的应用在后台同步用户的权限。

!["设备同步用户同意消息" 对话框](images/devicesyncuserconsent.png)

如果用户在以后更改其思想，则他们可以在设置中撤消权限。

!["设备同步权限设置" 对话框](images/devicesyncapppermissions.png)

### <a name="span-iddevice_update_user__consentspanspan-iddevice_update_user__consentspanspan-iddevice_update_user__consentspandevice-update-user-consent"></a><span id="Device_update_user__consent"></span><span id="device_update_user__consent"></span><span id="DEVICE_UPDATE_USER__CONSENT"></span>设备更新用户同意

与使用 DeviceUseTrigger 的任务不同，使用 DeviceServicingTrigger 后台任务的后台任务在每次触发后台任务时都需要用户同意。 此同意并不是存储在 DeviceUseTrigger 中。 这是因为设备固件更新涉及到风险较高的操作，并且需要更长的时间来进行设备更新。 除了获取用户同意外，Windows 还会向用户提供有关设备更新的信息，例如，在整个更新过程中使设备保持连接状态的警告，并确保计算机已计费，并且运行操作的大致运行时间 (如果你的应用程序) 。

!["设备更新用户同意消息" 对话框](images/deviceupdateuserconsent.png)

## <a name="span-idfrequency_and_foreground_restrictionsspanspan-idfrequency_and_foreground_restrictionsspanspan-idfrequency_and_foreground_restrictionsspanfrequency-and-foreground-restrictions"></a><span id="Frequency_and_foreground_restrictions"></span><span id="frequency_and_foreground_restrictions"></span><span id="FREQUENCY_AND_FOREGROUND_RESTRICTIONS"></span>频率和前景限制


您的应用程序可以启动操作的频率并无限制，但您的应用程序一次只能运行一个 DeviceUseTrigger 或 DeviceServicingTrigger 后台任务操作 (这不会影响其他类型的后台任务) ，并且仅当应用程序处于前台时才可启动后台任务。 如果你的应用不在前台，则无法使用 DeviceUseTrigger 或 DeviceServicingTrigger 启动后台任务。 在第一个后台任务完成之前，应用无法启动第二个设备后台任务。

## <a name="span-iddevice_background_task_policiesspanspan-iddevice_background_task_policiesspanspan-iddevice_background_task_policiesspandevice-background-task-policies"></a><span id="Device_background_task_policies"></span><span id="device_background_task_policies"></span><span id="DEVICE_BACKGROUND_TASK_POLICIES"></span>设备后台任务策略


当你的应用程序使用设备后台任务时，Windows 将强制实施策略。 如果不满足这些策略，则可以取消使用 DeviceUseTrigger 或 DeviceServicingTrigger 的后台任务。 使用设备后台任务与外围设备交互时，必须考虑这些策略要求。

### <a name="span-idtask_initiation_policiesspanspan-idtask_initiation_policiesspanspan-idtask_initiation_policiesspantask-initiation-policies"></a><span id="Task_initiation_policies"></span><span id="task_initiation_policies"></span><span id="TASK_INITIATION_POLICIES"></span>任务启动策略

此表指示哪些任务启动策略适用于每个后台任务触发器。

| 策略                                                                                                                                                                                                                               | DeviceServicingTrigger                       | DeviceUseTrigger                                            |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------|-------------------------------------------------------------|
| 当触发后台任务时，UWP 应用处于前台。                                                                                                                                                     | ![策略适用](images/ap-tools.png)       | ![策略适用](images/ap-tools.png)                      |
| 设备连接到系统 (或无线设备) 的范围内。                                                                                                                                                           | ![策略适用](images/ap-tools.png)       | ![策略适用](images/ap-tools.png)                      |
| 当屏幕锁定时，你的后台任务每分钟消耗 400 毫秒的 CPU 时间（假设 1GHz CPU），或者当屏幕未锁定时，每五分钟消耗该时间。 未能满足此策略可能导致任务被取消。 | ![策略适用](images/ap-tools.png)       | ![策略适用](images/ap-tools.png)                      |
| 使用设备外围 Api (适用于 USB、HID、蓝牙等) 的 Windows 运行时 Api，可访问设备。 如果应用无法访问设备，则拒绝访问后台任务。                  | ![策略适用](images/ap-tools.png)       | ![策略适用](images/ap-tools.png)                      |
| 在应用包部件清单中注册该应用提供的后台任务入口点。                                                                                                                                           | ![策略适用](images/ap-tools.png)       | ![策略适用](images/ap-tools.png)                      |
| 用户已向用户提供任务权限以继续。                                                                                                                                                                                  | 每次。                                  | 第一次，然后由应用权限控制。             |
| 应用提供的时间估算小于30分钟。                                                                                                                                                                           | ![策略适用](images/ap-tools.png)       | ![策略不适用](images/app-tools-doesnotapply.png) |
| 应用被指定为设备的特权应用。  (设备容器的设备元数据中的特权应用列表必须与应用程序 ID 完全匹配。 )                                                             | ![策略适用](images/ap-tools.png)       | ![策略不适用](images/app-tools-doesnotapply.png) |
| 计算机的电池容量已超过33% 或处于交流电源上。                                                                                                                                                          | ![策略适用](images/ap-tools.png)       | ![策略不适用](images/app-tools-doesnotapply.png) |
| 每个操作类型只运行一个设备后台任务。                                                                                                                                                                       | ![策略检查适用](images/ap-tools.png) | ![策略适用](images/ap-tools.png)                      |

 

### <a name="span-idruntime_policy_checksspanspan-idruntime_policy_checksspanspan-idruntime_policy_checksspanruntime-policy-checks"></a><span id="Runtime_policy_checks"></span><span id="runtime_policy_checks"></span><span id="RUNTIME_POLICY_CHECKS"></span>运行时策略检查

当你的任务在后台运行时，Windows 将强制执行以下运行时策略要求。 如果不能达到任意一项运行时要求，Windows 将取消你的设备后台任务。

此表指示哪些运行时策略应用于每个后台任务触发器。

| 策略检查                                                                                | DeviceServicingTrigger                                      | DeviceUseTrigger                             |
|---------------------------------------------------------------------------------------------|-------------------------------------------------------------|----------------------------------------------|
| 时钟时间限制 - 你的应用任务可以在后台运行的时间总量。 | 30 分钟                                                  | 10 分钟                                   |
| 设备连接到系统 (或无线设备) 的范围内。                  | ![策略不适用](images/app-tools-doesnotapply.png) | ![策略检查适用](images/ap-tools.png) |
| 任务不断对设备执行常规 I/O （每隔 5 秒执行 1 次 I/O）。                       | ![策略不适用](images/app-tools-doesnotapply.png) | ![策略检查适用](images/ap-tools.png) |
| 应用未取消任务。                                                              | ![策略检查适用](images/ap-tools.png)                | ![策略检查适用](images/ap-tools.png) |
| 应用未退出。                                                                         | ![策略检查适用](images/ap-tools.png)                | ![策略检查适用](images/ap-tools.png) |

 

## <a name="span-idbest_practicesspanspan-idbest_practicesspanspan-idbest_practicesspanbest-practices"></a><span id="Best_practices"></span><span id="best_practices"></span><span id="BEST_PRACTICES"></span>最佳做法


以下是使用设备后台任务的 UWP 设备应用的最佳实践。

### <a name="span-iddevice_background_task_programming_modelspanspan-iddevice_background_task_programming_modelspanspan-iddevice_background_task_programming_modelspandevice-background-task-programming-model"></a><span id="Device_background_task_programming_model"></span><span id="device_background_task_programming_model"></span><span id="DEVICE_BACKGROUND_TASK_PROGRAMMING_MODEL"></span>设备后台任务编程模型

在应用程序中使用 DeviceUseTrigger 或 DeviceServicingTrigger 后台任务可确保从前台应用启动的任何同步或设备更新操作都将继续在后台运行，前提是你的用户切换应用，而前台应用会被 Windows 挂起。 我们建议你按照这个整体模型注册、触发及注销后台任务：

1.  先注册后台任务，然后再请求触发。

2.  将进度事件处理程序和完成事件处理程序连接到你的触发器。 当你的应用从挂起状态恢复时，Windows 将为该应用提供可用于确定后台任务状态的任何排队等候处理的进度事件和完成事件。

3.  触发 DeviceUseTrigger 或 DeviceServicingTrigger 后台任务时，请关闭任何打开的设备对象，以便后台任务可以自由打开并使用这些设备。

4.  注册触发器。

5.  当任务完成时，注销后台任务。 当后台任务完成时，可以取消注册后台任务并重新打开设备，并从 UWP 应用中定期使用该设备。

6.  从你的后台任务类注册取消事件。 注册取消事件后，当 Windows 或你的前台应用取消后台任务时，即可使用后台任务代码完全停止你运行的后台任务。

7.  在应用退出 (不挂起) ，注销并取消任何正在运行的任务。

    -   退出你的应用时，注销并取消所有运行中的任务。

    -   退出你的应用时，将取消你的后台任务并断开所有现有事件处理程序与现有后台任务的连接。 这样你就无需确定你的后台任务的状态。 通过对注销和取消所有后台任务，你即可利用取消代码完全停止后台任务。

**提示**   有关如何使用[自定义 usb 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=301975 )和[固件更新 USB 设备示例](/samples/browse/)来完成此操作的详细说明，请参阅[创建设备后台任务](how-to-create-a-device-background-task.md)。

 

### <a name="span-idcancelling_a_background_taskspanspan-idcancelling_a_background_taskspanspan-idcancelling_a_background_taskspancancelling-a-background-task"></a><span id="Cancelling_a_background_task"></span><span id="cancelling_a_background_task"></span><span id="CANCELLING_A_BACKGROUND_TASK"></span>取消后台任务

若要从前台应用取消后台运行的任务，请在应用中使用的 BackgroundTaskRegistration 对象上使用 "取消注册" 方法，以注册 [DeviceUseTrigger](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) 或 [DeviceServicingTrigger](/uwp/api/Windows.ApplicationModel.Background.DeviceServicingTrigger) 后台任务。 使用 BackgroundTaskRegistration 上的 Unregister 方法注销你的后台任务，将会导致后台任务基础结构取消你的后台任务。

此外，Unregister 方法使用布尔值 true 或 false 指示是否应在任务未完成的情况下取消当前运行的后台任务实例。 有关详细信息，请参阅 [BackgroundTaskRegistration](/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskRegistration)的 API 参考。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[创建设备后台任务](how-to-create-a-device-background-task.md)

[自定义 USB 设备示例](https://go.microsoft.com/fwlink/p/?LinkId=301975 )

[固件更新 USB 设备示例](/samples/browse/)

[Launching, resuming, and multitasking](/previous-versions/windows/apps/hh770837(v=win.10))

[通过后台任务支持您的应用程序](/previous-versions/windows/apps/hh977056(v=win.10))

 

