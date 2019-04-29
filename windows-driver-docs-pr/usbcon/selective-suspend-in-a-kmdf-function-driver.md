---
Description: 本主题介绍如何 KMDF 函数驱动程序支持 USB 选择性挂起。
title: USB KMDF 功能驱动程序中的选择性挂起
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 04fc0d1cce9a9609e846c4fcbe2729b5c529f212
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379513"
---
# <a name="selective-suspend-in-usb-kmdf-function-drivers"></a>USB KMDF 功能驱动程序中的选择性挂起


**重要的 Api**

-   [**WdfDeviceAssignS0IdleSettings**](https://msdn.microsoft.com/library/windows/hardware/ff545903)
-   [**WdfDeviceAssignSxWakeSettings**](https://msdn.microsoft.com/library/windows/hardware/ff545909)
-   [**WdfDeviceStopIdle**](https://msdn.microsoft.com/library/windows/hardware/ff546921)

本主题介绍如何 KMDF 函数驱动程序支持 USB 选择性挂起。

如果 USB 驱动程序不需要功能或不是在用户模式下可用的资源，则应提供 KMDF 功能驱动程序。 通过设置 KMDF 初始化结构中的相关值，然后提供相应的回调函数 KMDF 驱动程序实现选择性挂起。 KMDF 处理与低级驱动程序挂起和恢复该设备进行通信详细的信息。

## <a name="guidelines-for-selective-suspend-in-kmdf-drivers"></a>指导原则的选择性挂起 KMDF 驱动程序中


支持选择性挂起的 KMDF 驱动程序必须遵循以下准则：

-   KMDF 功能驱动程序必须为其设备堆栈 PPO。 默认情况下，KMDF 函数驱动程序都是 PPO。
-   支持选择性挂起 KMDF 功能驱动程序可以使用电源管理的队列或队列不电源管理的。 默认情况下，PPOs 的队列对象是电源管理。

**电源策略所有权和 KMDF USB 驱动程序**

默认情况下，USB 设备的 KMDF 函数驱动程序是设备堆栈 PPO。 KMDF 管理选择性挂起和继续代表此驱动程序。

**KMDF 驱动程序中的 I/O 队列配置**

支持选择性挂起 KMDF 功能驱动程序可以使用电源管理的队列或队列不电源管理的。 通常情况下，驱动程序配置不是电源管理以接收传入设备 I/O 控制请求和配置用于接收读取、 写入和其他依赖于电源的请求的一个或多个电源管理队列的队列。 当请求到达时在电源管理的队列时，KMDF 可确保设备是 D0 之前它将提供对该驱动程序的请求。

如果你正在编写中设备堆栈 PPO 上进行分层 KMDF 筛选器驱动程序，您必须使用电源管理队列。 原因是与 UMDF 驱动程序相同。 框架没有显示从电源管理队列的请求时挂起设备，因此使用此类队列可能安装设备堆栈。

## <a name="selective-suspend-mechanism-for-kmdf-function-drivers"></a>选择性挂起 KMDF 函数驱动程序的机制


KMDF 句柄的大部分工作所需支持 USB 选择性挂起。 它跟踪的 I/O 活动、 管理空闲计时器，并将设备发送会导致父驱动程序 （Usbhub.sys 或 Usbccgp.sys） 暂停和恢复设备的 I/O 控制请求。

如果 KMDF 函数驱动程序支持选择性挂起，KMDF 跟踪每个设备对象拥有的所有电源管理的队列上的 I/O 活动。 每当 I/O 计数达到零时，框架将开始一个空闲计时器。 默认超时值为 5 秒。

如果 I/O 请求到达时所属的设备对象的空闲超时期限过期之前的电源管理的队列，框架将取消的空闲计时器，并不会挂起设备。

空闲计时器过期时，KMDF 发出请求所需将 USB 设备放在挂起状态。 如果功能驱动程序使用 USB 终结点上的连续读取器，则读取器的重复的轮询不能算作 KMDF 空闲计时器活动。 但是，在[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)回调函数的 USB 驱动程序，必须手动停止持续读取器和任何其他队列不是电源管理，确保通过填充的 I/O 目标设备不处于工作状态时，驱动程序不发送 I/O 请求。 若要停止的目标，驱动程序调用[ **WdfIoTargetStop** ](https://msdn.microsoft.com/library/windows/hardware/ff548680) ，并指定**WdfIoTargetWaitForSentIoToComplete**作为目标操作。 在响应中，该框架目标的 I/O 队列中的所有 I/O 请求已都完成和任何相关的回调已运行的 I/O 完成后，仅停止 I/O 目标。

默认情况下，KMDF 转换 D0 带到空闲的设置中指定驱动程序的设备电源状态的设备。 为转换的一部分，KMDF 调用驱动程序的 power 回调函数，相同的方式就像任何其他电源关闭序列。

已挂起设备后，框架将自动恢复设备时出现任何以下事件：

-   I/O 请求到达的任何驱动程序的电源管理队列。
-   通过使用设备管理器用户禁用 USB 选择性挂起。
-   驱动程序调用[ **WdfDeviceStopIdle**](https://msdn.microsoft.com/library/windows/hardware/ff546921)，如中所述[阻止设备挂起](#preventsusp)。

若要恢复设备，KMDF 发送设备堆栈的下层的增益道具请求，并就像任何其他强化序列相同方式调用驱动程序的回调函数。

有关电源关闭和启动序列中涉及的回叫的详细信息，请参阅[插和 WDF 驱动程序中的电源管理](http://download.microsoft.com/download/5/d/6/5d6eaf2b-7ddf-476b-93dc-7cf0072878e6/WDF-pnpPower.docx)白皮书。

## <a name="supporting-usb-selective-suspend-in-a-kmdf-function-driver"></a>KMDF 功能驱动程序中支持 USB 选择性挂起


若要实现 USB 选择性挂起 KMDF 功能驱动程序中：

-   初始化与空闲状态，其中包括空闲超时的电源策略设置。
-   根据需要包含逻辑以暂时防止挂起或恢复操作时，驱动程序确定设备不应由于开放句柄或与设备的 I/O 队列不相关的其他原因而挂起。
-   在 USB 驱动程序 INF 中指示的人机接口设备 (HID)，它支持选择性挂起。

**初始化 KMDF 功能驱动程序中的电源策略设置**

若要配置支持的 USB 选择性挂起，KMDF 驱动程序将使用[ **WDF\_设备\_POWER\_策略\_空闲\_设置**](https://msdn.microsoft.com/library/windows/hardware/ff551270)结构。 驱动程序首先必须初始化该结构，然后，可以设置字段提供有关驱动程序和其设备的功能的详细信息。 通常情况下，该驱动程序填充此结构中其*EvtDriverDeviceAdd*或*EvtDevicePrepareHardware*函数。

**若要初始化 WDF\_设备\_电源\_策略\_空闲\_设置结构**

该驱动程序创建的设备对象后，驱动程序将使用[ **WDF\_设备\_POWER\_策略\_空闲\_设置\_INIT**](https://msdn.microsoft.com/library/windows/hardware/ff551271)函数初始化结构。 此函数采用两个参数：

-   一个指向[ **WDF\_设备\_POWER\_策略\_空闲\_设置**](https://msdn.microsoft.com/library/windows/hardware/ff551270)结构初始化。
-   一个枚举值，指示支持的选择性挂起。 该驱动程序应指定**IdleUsbSelectiveSuspend**。

如果指定了该驱动程序**IdleUsbSelectiveSuspend**，该函数初始化结构的成员，如下所示：

-   **IdleTimeout**设置为**IdleTimeoutDefaultValue** （当前 5000 毫秒或 5 秒）。
-   **UserControlOfIdleSettings**设置为**IdleAllowUserControl** 。
-   **已启用**设置为**WdfUseDefaul**t，指示的选择性挂起已启用，但如果用户可以禁用它**UserControlOfIdleSettings**成员允许它。
-   **DxState**设置为**PowerDeviceMaximum**，它使用设备的报告的电源功能以确定要转换的空闲状态的设备的状态。

**若要配置 USB 选择性挂起**

该驱动程序初始化后[ **WDF\_设备\_POWER\_策略\_空闲\_设置**](https://msdn.microsoft.com/library/windows/hardware/ff551270)结构，该驱动程序可以设置结构，然后调用中的其他字段**WdfDeviceAssignS0IdleSettings**将这些设置传递到框架。 以下字段适用于函数的 USB 驱动程序：

-   IdleTimeout — 以毫秒为单位，而不会收到的 I/O 请求，该框架将设备视为空闲之前必须等待的间隔。 该驱动程序可以指定 ULONG 值，也可以接受默认值。
-   UserControlOfIdleSettings — 用户是否可以修改设备的空闲设置。 可能的值为 IdleDoNotAllowUserControl 和 IdleAllowUserControl。
-   DxState，框架将设备挂起的设备电源状态。 可能的值为 PowerDeviceD1、 PowerDeviceD2 和 PowerDeviceD3。

    USB 驱动程序不应更改此值的初始设置。 [ **WDF\_设备\_POWER\_策略\_空闲\_设置\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff551271)函数将此值设置为PowerDeviceMaximum，这样可以确保框架选择正确的设备功能的值。

以下代码片段摘自 Osrusbfx2 示例驱动程序 Device.c 文件：

```cpp
WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS idleSettings;
NTSTATUS    status = STATUS_SUCCESS;
//
// Initialize the idle policy structure.
//
WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS_INIT(&idleSettings, 
     IdleUsbSelectiveSuspend);
idleSettings.IdleTimeout = 10000; // 10 sec

status = WdfDeviceAssignS0IdleSettings(Device, &idleSettings);
if ( !NT_SUCCESS(status)) {
     TraceEvents(TRACE_LEVEL_ERROR, DBG_PNP,
                 "WdfDeviceSetPowerPolicyS0IdlePolicy failed %x\n", 
                 status);
    return status;
}
```

在示例中，该驱动程序调用[ **WDF\_设备\_POWER\_策略\_空闲\_设置\_INIT**](https://msdn.microsoft.com/library/windows/hardware/ff551271)，指定**IdleUsbSelectiveSuspend**。 驱动程序集**IdleTimeout**为 10000 毫秒 （10 秒），并接受的 framework 默认值**DxState**并**UserControlOfIdleSettings**。 因此，框架将转换到 D3 状态设备时它处于空闲状态，并创建允许具有管理员权限的用户启用或禁用设备空闲支持的设备管理器属性页。 然后，该驱动程序调用[ **WdfDeviceAssignS0IdleSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff545903)启用空闲支持并向框架注册这些设置。

驱动程序可以调用[ **WdfDeviceAssignS0IdleSettings**](https://msdn.microsoft.com/library/windows/hardware/ff545903)任何时候，只要之后创建的设备对象。 尽管大多数驱动程序调用此方法从最初*EvtDriverDeviceAdd*回调，这可能不始终是无法或甚至不适合。 如果驱动程序支持多个设备或设备版本，该驱动程序可能不会知道所有设备功能，直到它查询硬件。 此类驱动程序可以延迟调用**WdfDeviceAssignS0IdleSettings**直到*EvtDevicePrepareHardware*回调。

在其首字母后随时调用[ **WdfDeviceAssignS0IdleSettings**](https://msdn.microsoft.com/library/windows/hardware/ff545903)，驱动程序可以更改空闲超时值和在其中空闲设备的设备状态。 若要更改一个或多个设置，该驱动程序只需初始化另一个[ **WDF\_设备\_POWER\_策略\_空闲\_设置**](https://msdn.microsoft.com/library/windows/hardware/ff551270)如前面所述的结构和调用**WdfDeviceAssignS0IdleSettings**试。

### <a href="" id="preventsusp"></a>阻止 USB 设备挂起

有时，USB 设备应不关闭电源即使没有 I/O 请求的超时期限内，通常当句柄是打开到设备或设备正在充电。 USB 驱动程序可以防止在 framework 挂起空闲设备在这种情况下通过调用[ **WdfDeviceStopIdle** ](https://msdn.microsoft.com/library/windows/hardware/ff546921)并调用[ **WdfDeviceResumeIdle**](https://msdn.microsoft.com/library/windows/hardware/ff546838)时可以被再次挂起的设备。

[**WdfDeviceStopIdle** ](https://msdn.microsoft.com/library/windows/hardware/ff546921)停止空闲计时器。 如果**IdleTimeout**期尚未过期和尚未挂起设备，该框架取消空闲计时器，并不会挂起设备。 如果设备已被暂停，框架会将设备返回到工作状态。 **WdfDeviceStopIdle**不会阻止该框架系统更改为 Sx 睡眠状态时挂起设备。 其唯一的影响是为了防止设备挂起，当系统处于 S0 工作状态。 [**WdfDeviceResumeIdle** ](https://msdn.microsoft.com/library/windows/hardware/ff546838)重新启动空闲计时器。 这两种方法管理引用计数在设备上，因此，如果驱动程序调用**WdfDeviceStopIdle**几次，该框架不会挂起设备驱动程序已调用之前**WdfDeviceResumeIdle**同样次数。 驱动程序不能调用**WdfDeviceResumeIdle**而无需第一个调用**WdfDeviceStopIdle**。

### <a name="including-a-registry-key-hid-drivers-only"></a>包括一个注册表项 （仅限 HID 驱动程序）

KMDF 上层筛选器驱动程序 USB HID 设备必须指示 INF 中，它们支持选择性挂起，以便 Microsoft 提供 HIDClass.sys 端口驱动程序可以启用选择性暂停的 HID 堆栈。 INF 应包括将 SelectiveSuspendEnabled 密钥添加一个 AddReg 指令并将其值设置为 1，如下所示的字符串：

```cpp
HKR,,"SelectiveSuspendEnabled",0x00000001,0x1
```

有关示例，请参阅位于 %winddk%WDK 中的 Hidusbfx2.inx\\BuildNumber\\Src\\Hid\\ Hidusbfx2\\sys。

## <a name="remote-wake-support-for-kmdf-drivers"></a>用于 KMDF 驱动程序的远程唤醒支持


使用选择性挂起，如 KMDF 集成了对唤醒，支持，以便在设备处于空闲状态和系统不处于工作状态 (S0) 或处于休眠状态 (S1-S4) 时，USB 设备可以触发唤醒信号。 在 KMDF 术语中，这两个功能称为"从 S0 唤醒"和"从 Sx，唤醒"分别。

USB 设备的唤醒只是指示设备本身可以启动从省电状态转换到工作状态。 因此，在 USB 术语中，从 S0 唤醒从 Sx 唤醒是相同的并称为"远程唤醒"。

KMDF USB 函数驱动程序不需要任何代码，以支持从 S0 唤醒，因为 KMDF 提供了此功能，如一部分的选择性挂起机制。 但是，若要支持远程唤醒 Sx 系统时，功能驱动程序必须：

-   检查设备是否支持通过调用远程唤醒[ **WdfUsbTargetDeviceRetrieveInformation**](https://msdn.microsoft.com/library/windows/hardware/ff550100)。
-   通过初始化唤醒设置，然后调用启用远程唤醒[ **WdfDeviceAssignSxWakeSettings**](https://msdn.microsoft.com/library/windows/hardware/ff545909)。

KMDF 驱动程序通常它们为 USB 选择性挂起中配置支持的同时配置唤醒支持*EvtDriverDeviceAdd*或*EvtDevicePrepareHardware*函数。

### <a name="checking-device-capabilities"></a>检查设备功能

KMDF USB 功能驱动程序初始化之前为其电源策略设置空闲和唤醒，应该验证设备支持在远程唤醒。 若要获取有关设备的硬件功能的信息，该驱动程序初始化[ **WDF\_USB\_设备\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff552592)结构和调用[ **WdfUsbTargetDeviceRetrieveInformation**](https://msdn.microsoft.com/library/windows/hardware/ff550100)，通常在其*EvtDriverDeviceAdd*或者*EvtDevicePrepareHardware*回调。

在调用[ **WdfUsbTargetDeviceRetrieveInformation**](https://msdn.microsoft.com/library/windows/hardware/ff550100)，该驱动程序将一个句柄传递给设备对象和一个指向初始化[ **WDF\_USB\_设备\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff552592)结构。 在从该函数成功返回时，结构的特征字段包含标志，指示设备是否自供电，可以运行在高速度、 和支持远程唤醒。

下面的示例摘自 Osrusbfx2 KMDF 示例演示如何调用此方法来确定设备是否支持远程唤醒。 运行以下代码行后，waitWakeEnable 变量将包含 TRUE，如果设备支持远程唤醒和 FALSE，如果不是：

```cpp
    WDF_USB_DEVICE_INFORMATION          deviceInfo;
// Retrieve USBD version information, port driver capabilities and device
// capabilites such as speed, power, etc.
//

WDF_USB_DEVICE_INFORMATION_INIT(&deviceInfo);

status = WdfUsbTargetDeviceRetrieveInformation(
                            pDeviceContext->UsbDevice,
                            &deviceInfo);
waitWakeEnable = deviceInfo.Traits & WDF_USB_DEVICE_TRAIT_REMOTE_WAKE_CAPABLE;
```

### <a name="enabling-remote-wakeup"></a>启用远程唤醒

在 USB 术语中，USB 设备可用于远程唤醒时其设备\_远程\_唤醒功能设置。 根据 USB 规范中，主机软件必须在"仅只是之前"将设备置于睡眠状态的设备上设置远程唤醒功能。 KMDF 功能驱动程序仅需初始化唤醒设置。 KMDF 和 Microsoft 提供的 USB 总线驱动程序发出 I/O 请求并处理启用远程唤醒所需的硬件操作。

**若要初始化唤醒设置**

1.  调用[ **WDF\_设备\_POWER\_策略\_唤醒\_设置\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff551279)初始化[**WDF\_设备\_POWER\_策略\_唤醒\_设置**](https://msdn.microsoft.com/library/windows/hardware/ff551277)结构。 此函数将该结构的**已启用**成员添加到**WdfUseDefault**，设置**DxState**成员添加到**PowerDeviceMaximum**，和设置**UserControlOfWakeSettings**成员添加到**WakeAllowUserControl**。
2.  调用[ **WdfDeviceAssignSxWakeSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff545909)与初始化结构。 结果是，启用了设备，以从 D3 状态中唤醒，用户可以启用或禁用从设备管理器中的设备属性页的唤醒信号。

下面的代码段从示例演示如何初始化的 Osrusbfx2 唤醒设置为其默认值：

```cpp
WDF_DEVICE_POWER_POLICY_WAKE_SETTINGS wakeSettings;

WDF_DEVICE_POWER_POLICY_WAKE_SETTINGS_INIT(&wakeSettings);
status = WdfDeviceAssignSxWakeSettings(Device, &wakeSettings);
if (!NT_SUCCESS(status)) {
    return status;
}
```

对于支持选择性挂起的 USB 设备，基础总线驱动程序准备用于唤醒的设备硬件。 因此，函数的 USB 驱动程序很少需要*EvtDeviceArmWakeFromS0*回调。 空闲超时过期时，框架会将选择性挂起请求发送到 USB 总线驱动程序。

出于相同原因，USB 函数驱动程序很少需要*EvtDeviceWakeFromS0Triggered*或*EvtDeviceWakeFromSxTriggered*回调。 相反，该框架和基础总线驱动程序处理返回到工作状态的设备的所有要求。

## <a name="related-topics"></a>相关主题
[USB 驱动程序 (WDF) 中的选择性挂起](selective-suspend-in-usb-drivers-wdf.md)  



