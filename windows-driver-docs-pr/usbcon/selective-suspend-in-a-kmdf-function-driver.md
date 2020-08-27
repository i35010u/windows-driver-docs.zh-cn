---
description: 本主题介绍 KMDF function 驱动程序如何支持 USB 选择性挂起。
title: USB KMDF 功能驱动程序中的选择性挂起
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 40eacdd13f7b263392aa7470038adb715e871640
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969572"
---
# <a name="selective-suspend-in-usb-kmdf-function-drivers"></a>USB KMDF 功能驱动程序中的选择性挂起


**重要的 API**

-   [**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)
-   [**WdfDeviceAssignSxWakeSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassignsxwakesettings)
-   [**WdfDeviceStopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)

本主题介绍 KMDF function 驱动程序如何支持 USB 选择性挂起。

如果 USB 驱动程序需要不在用户模式下使用的功能或资源，则应提供 KMDF function 驱动程序。 KMDF 驱动程序通过在 KMDF 初始化结构中设置相关值并提供相应的回调函数来实现选择性挂起。 KMDF 处理与较低驱动程序通信的详细信息，以挂起和恢复设备。

## <a name="guidelines-for-selective-suspend-in-kmdf-drivers"></a>KMDF 驱动程序中的选择性挂起指南


支持选择性挂起的 KMDF 驱动程序必须遵循以下准则：

-   KMDF 函数驱动程序必须是其设备堆栈的 PPO。 默认情况下，KMDF 函数驱动程序为 PPO。
-   支持选择性挂起的 KMDF 函数驱动程序可以使用处于电源托管状态的队列或不是电源管理的队列。 默认情况下，PPOs 的队列对象为 "电源管理"。

**电源策略所有权和 KMDF USB 驱动程序**

默认情况下，USB 设备的 KMDF 函数驱动程序是设备堆栈的 PPO。 KMDF 代表此驱动程序管理选择性挂起和恢复。

**KMDF 驱动程序中的 i/o 队列配置**

支持选择性挂起的 KMDF 函数驱动程序可以使用处于电源托管状态的队列或不是电源管理的队列。 通常，驱动程序会将不是电源管理的队列配置为接收传入设备 i/o 控制请求，并将一个或多个电源管理的队列配置为接收读取、写入和其他与电源相关的请求。 当请求到达电源管理队列时，KMDF 确保设备在向驱动程序发出请求之前处于 D0 状态。

如果要编写的 KMDF 筛选器驱动程序在设备堆栈中的 PPO 上方，则不得使用电源管理的队列。 原因与 UMDF 驱动程序相同。 在设备挂起时，框架不会提供来自电源管理队列的请求，因此，使用此类队列可能会使设备堆栈停止。

## <a name="selective-suspend-mechanism-for-kmdf-function-drivers"></a>KMDF 函数驱动程序的选择性挂起机制


KMDF 处理支持 USB 选择性挂起所需的大部分工作。 它跟踪 i/o 活动，管理空闲计时器，并将导致父驱动程序 ( # A0 或 Usbccgp.sys) 的设备 i/o 控制请求发送到挂起和恢复设备。

如果 KMDF 函数驱动程序支持选择性挂起，则 KMDF 跟踪每个设备对象拥有的所有电源管理队列上的 i/o 活动。 每当 i/o 计数达到零时，框架就会启动空闲计时器。 默认超时值为5秒。

如果在空闲超时期限到期之前，i/o 请求到达属于设备对象的电源管理队列，则该框架将取消空闲计时器并且不会挂起设备。

空闲计时器过期时，KMDF 发出请求，要求将 USB 设备置于挂起状态。 如果函数驱动程序在 USB 终结点上使用连续读取器，则读取器的重复轮询不会计入 KMDF 空闲计时器的活动。 但是，在 [*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit) 回调函数中，USB 驱动程序必须手动停止连续读取器以及由不是电源管理的队列馈送的任何其他 i/o 目标，以确保在设备未处于工作状态时，驱动程序不发送 i/o 请求。 若要停止目标，驱动程序将调用 [**WdfIoTargetStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop) ，并将 **WdfIoTargetWaitForSentIoToComplete** 指定为目标操作。 作为响应，框架仅在目标的 i/o 队列中的所有 i/o 请求已完成并且任何关联的 i/o 完成回调都已运行之后，才停止 i/o 目标。

默认情况下，KMDF 会将设备从 D0 上转换到设备电源状态，驱动程序在 "空闲" 设置中指定。 在转换过程中，KMDF 会调用驱动程序的电源回叫功能，其方式与对任何其他关机序列相同。

设备挂起后，当发生以下任何事件时，框架会自动恢复设备：

-   为驱动程序的任何电源管理队列提供 i/o 请求。
-   用户使用设备管理器禁用 USB 选择性挂起。
-   驱动程序调用 [**WdfDeviceStopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)，如 [阻止设备挂起](#preventsusp)中所述。

若要恢复设备，KMDF 会将开机请求发送到设备堆栈中，然后调用该驱动程序的回调函数，其方式与对任何其他开机序列相同。

有关电源关闭和通电顺序中涉及的回调的详细信息，请参阅 " [WDF 驱动程序" 白皮书中的 "即插即用和电源管理](https://download.microsoft.com/download/5/d/6/5d6eaf2b-7ddf-476b-93dc-7cf0072878e6/WDF-pnpPower.docx) "。

## <a name="supporting-usb-selective-suspend-in-a-kmdf-function-driver"></a>支持在 KMDF 函数驱动程序中使用 USB 选择性挂起


在 KMDF 函数驱动程序中实现 USB 选择性挂起：

-   初始化与空闲相关的电源策略设置，包括空闲超时。
-   如果驱动程序确定由于打开的句柄或其他与设备的 i/o 队列无关的原因而不应挂起设备，则可以选择包含逻辑来暂时阻止挂起或恢复操作。
-   在 (HID) 的用户界面设备的 USB 驱动程序中，指示 INF 中支持选择性挂起。

**初始化 KMDF 函数驱动程序中的电源策略设置**

若要为 USB 选择性挂起配置支持，KMDF 驱动程序需要使用 [**WDF \_ 设备 \_ 电源 \_ 策略 \_ 空闲 \_ 设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings) 结构。 驱动程序必须首先初始化结构，然后可以设置字段以提供有关驱动程序及其设备功能的详细信息。 通常，驱动程序会在其 *EvtDriverDeviceAdd* 或 *EvtDevicePrepareHardware* 函数中填充此结构。

**初始化 WDF \_ 设备 \_ 电源 \_ 策略 \_ 空闲 \_ 设置结构**

驱动程序创建设备对象之后，驱动程序将使用 [**WDF \_ 设备 \_ 电源 \_ 策略 \_ 空闲 \_ 设置 \_ INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdf_device_power_policy_idle_settings_init) 函数初始化结构。 此函数采用两个参数：

-   一个指针，指向要初始化的 [**WDF \_ 设备 \_ 电源 \_ 策略 \_ 空闲 \_ 设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings) 结构。
-   一个枚举值，该值指示对选择性挂起的支持。 驱动程序应指定 **IdleUsbSelectiveSuspend**。

如果驱动程序指定了 **IdleUsbSelectiveSuspend**，则该函数将按如下所示初始化结构的成员：

-   在当前5000毫秒或5秒) ， **IdleTimeout**设置为**IdleTimeoutDefaultValue** (。
-   **UserControlOfIdleSettings** 设置为 **IdleAllowUserControl** 。
-   "**已启用**" 设置为 " **WdfUseDefaul**t"，表示已启用选择性挂起，但如果**UserControlOfIdleSettings**成员允许，则用户可以禁用它。
-   **DxState** 设置为 **PowerDeviceMaximum**，它使用设备的已报告电源功能确定要将空闲设备过渡到的状态。

**配置 USB 选择性挂起**

驱动程序初始化 [**WDF \_ 设备 \_ 电源 \_ 策略 \_ 空闲 \_ 设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings) 结构之后，驱动程序可以设置结构中的其他字段，然后调用 **WdfDeviceAssignS0IdleSettings** 将这些设置传递到框架。 以下字段适用于 USB 函数驱动程序：

-   IdleTimeout —在框架认为设备处于空闲状态之前必须经过的时间间隔（以毫秒为单位），而无需接收 i/o 请求。 驱动程序可以指定 ULONG 值，也可以接受默认值。
-   UserControlOfIdleSettings-用户是否可以修改设备的空闲设置。 可能的值为 IdleDoNotAllowUserControl 和 IdleAllowUserControl。
-   DxState-框架挂起设备的设备电源状态。 可能的值包括 PowerDeviceD1、PowerDeviceD2 和 PowerDeviceD3。

    USB 驱动程序不应更改此值的初始设置。 [**WDF \_ 设备 \_ 电源 \_ 策略 \_ 空闲 \_ 设置 \_ INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdf_device_power_policy_idle_settings_init)函数将此值设置为 PowerDeviceMaximum，这可确保框架根据设备功能选择正确的值。

下面的代码段来自 Osrusbfx2 示例驱动程序的设备 .c 文件：

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

在此示例中，驱动程序调用 [**WDF \_ 设备 \_ 电源 \_ 策略 \_ 空闲 \_ 设置 \_ INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdf_device_power_policy_idle_settings_init)，并指定 **IdleUsbSelectiveSuspend**。 驱动程序将 **IdleTimeout** 设置为10000毫秒 (10 秒) 并接受 **DxState** 和 **UserControlOfIdleSettings**的 framework 默认值。 因此，在设备处于空闲状态时，框架会将设备转换为 D3 状态，并创建一个设备管理器属性页，该属性页允许具有管理员权限的用户启用或禁用设备空闲支持。 然后，该驱动程序调用 [**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings) 来启用空闲支持，并将这些设置注册到框架中。

驱动程序可以在创建设备对象之后随时调用 [**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)。 尽管大多数驱动程序最初都是从 *EvtDriverDeviceAdd* 回调调用此方法，但这可能并不总是可能，甚至是理想情况。 如果驱动程序支持多个设备或设备版本，则在查询硬件之前，驱动程序可能不会知道所有设备功能。 此类驱动程序可以推迟调用 **WdfDeviceAssignS0IdleSettings** ，直到 *EvtDevicePrepareHardware* 回调。

在首次调用 [**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)之后，驱动程序可以随时更改空闲超时值和设备空闲的设备状态。 若要更改一个或多个设置，驱动程序只需初始化另一个 [**WDF \_ 设备 \_ 电源 \_ 策略 \_ 空闲 \_ 设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings) 结构（如前文所述），然后再次调用 **WdfDeviceAssignS0IdleSettings** 。

### <a name="preventing-usb-device-suspension"></a><a href="" id="preventsusp"></a>阻止 USB 设备暂停

有时，即使在超时期内没有 i/o 请求，USB 设备也不应关闭，通常是在设备上打开了句柄或设备正在充电。 USB 驱动程序可以通过调用 [**WdfDeviceStopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle) 并调用 [**WdfDeviceResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle) 以使其可被挂起，使框架无法在这种情况下挂起空闲设备。

[**WdfDeviceStopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle) 停止空闲计时器。 如果 **IdleTimeout** 期限尚未过期并且设备尚未挂起，则该框架将取消空闲计时器，并且不会挂起设备。 如果设备已挂起，则框架会将设备返回到工作状态。 当系统更改为 Sx 睡眠状态时， **WdfDeviceStopIdle**不会阻止框架挂起设备。 它的唯一作用是在系统处于 S0 工作状态时阻止设备暂停。 [**WdfDeviceResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle) 重新启动空闲计时器。 这两种方法管理设备上的引用计数，因此，如果驱动程序多次调用 **WdfDeviceStopIdle** ，框架将不会挂起设备，直到驱动程序调用 **WdfDeviceResumeIdle** 的次数相同。 如果没有首先调用**WdfDeviceStopIdle**，驱动程序不得调用**WdfDeviceResumeIdle**。

### <a name="including-a-registry-key-hid-drivers-only"></a>仅 (HID 驱动程序中包含注册表项) 

适用于 USB HID 设备的 KMDF 高层筛选器驱动程序必须在 INF 中指出，它们支持选择性挂起，以便 Microsoft 提供的 HIDClass.sys 端口驱动程序可以为 HID 堆栈启用选择性挂起。 INF 应包含添加 SelectiveSuspendEnabled 键并将其值设置为1的 AddReg 指令，如以下字符串所示：

```cpp
HKR,,"SelectiveSuspendEnabled",0x00000001,0x1
```

有关示例，请参阅 Hidusbfx2 中的 inx% WinDDK% \\ BuildNumber \\ Src \\ Hid \\ Hidusbfx2 \\ sys。

## <a name="remote-wake-support-for-kmdf-drivers"></a>KMDF 驱动程序的远程唤醒支持


与选择性挂起一样，KMDF 支持唤醒，因此 USB 设备在设备处于空闲状态且系统处于工作状态 (S0) 或处于休眠状态 (S1 – S4) 时，可以触发唤醒信号。 在 KMDF 中，这两项功能分别称为 "从 S0 唤醒" 和 "从 Sx 唤醒"。

对于 USB 设备，唤醒只表示设备本身可以启动从较低电源状态到工作状态的转换。 因此，在 USB 术语中，从 S0 唤醒，从 Sx 唤醒是相同的，并且称为 "远程唤醒"。

KMDF USB 函数驱动程序不需要任何代码即可支持从 S0 唤醒，因为 KMDF 将此功能作为选择性挂起机制的一部分提供。 但是，若要支持在系统处于 Sx 时进行远程唤醒，函数驱动程序必须：

-   通过调用 [**WdfUsbTargetDeviceRetrieveInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveinformation)检查设备是否支持远程唤醒。
-   通过初始化唤醒设置并调用 [**WdfDeviceAssignSxWakeSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassignsxwakesettings)来启用远程唤醒。

KMDF 驱动程序通常会配置唤醒支持，同时在 *EvtDriverDeviceAdd* 或 *EvtDevicePrepareHardware* 函数中配置对 USB 选择性挂起的支持。

### <a name="checking-device-capabilities"></a>检查设备功能

在 KMDF USB 函数驱动程序为空闲和唤醒初始化其电源策略设置之前，应验证设备是否支持远程唤醒。 为了获取有关设备硬件功能的信息，驱动程序将 [**初始化 \_ WDF USB \_ 设备 \_ 信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_device_information) 结构并调用 [**WdfUsbTargetDeviceRetrieveInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveinformation)，通常在其 *EvtDriverDeviceAdd* 或 *EvtDevicePrepareHardware* 回调中。

在对 [**WdfUsbTargetDeviceRetrieveInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveinformation)的调用中，驱动程序将句柄传递给设备对象，并将指针传递到已初始化的 [**WDF \_ USB \_ 设备 \_ 信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_device_information) 结构。 成功从函数返回后，结构的特征字段将包含标志，用于指示设备是否是自驱动的，可以高速操作，并且支持远程唤醒。

Osrusbfx2 KMDF 示例中的以下示例演示了如何调用此方法来确定设备是否支持远程唤醒。 运行这些代码行后，如果设备支持远程唤醒，waitWakeEnable 变量将包含 TRUE，否则将返回 FALSE：

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

在 USB 术语中，在设置了 USB 设备的设备 \_ 远程唤醒功能时，会为其启用远程唤醒 \_ 。 根据 USB 规范，主机软件必须在设备上 "只是之前" 设置远程唤醒功能，使设备进入睡眠状态。 KMDF 函数驱动程序只需初始化唤醒设置。 KMDF 和 Microsoft 提供的 USB 总线驱动程序发出 i/o 请求并处理启用远程唤醒所需的硬件操作。

**初始化唤醒设置**

1.  调用 [**wdf \_ 设备 \_ 电源 \_ 策略 \_ 唤醒 \_ 设置 \_ INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdf_device_power_policy_wake_settings_init) ，初始化 [**wdf \_ 设备 \_ 电源 \_ 策略 \_ 唤醒 \_ 设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_wake_settings) 结构。 此函数将结构的 **已启用** 成员设置 **为 WdfUseDefault**，将 **DxState** 成员设置为 **PowerDeviceMaximum**，并将 **UserControlOfWakeSettings** 成员设置为 **WakeAllowUserControl**。
2.  用初始化的结构调用 [**WdfDeviceAssignSxWakeSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassignsxwakesettings) 。 因此，将启用设备以从 D3 状态唤醒，用户可以从设备管理器的设备属性页启用或禁用唤醒信号。

Osrusbfx2 示例中的以下代码片段演示了如何将唤醒设置初始化为其默认值：

```cpp
WDF_DEVICE_POWER_POLICY_WAKE_SETTINGS wakeSettings;

WDF_DEVICE_POWER_POLICY_WAKE_SETTINGS_INIT(&wakeSettings);
status = WdfDeviceAssignSxWakeSettings(Device, &wakeSettings);
if (!NT_SUCCESS(status)) {
    return status;
}
```

对于支持选择性挂起的 USB 设备，基础总线驱动程序会准备要唤醒的设备硬件。 因此，USB 函数驱动程序很少需要 *EvtDeviceArmWakeFromS0* 回调。 当空闲超时过期时，框架会将选择性挂起请求发送到 USB 总线驱动程序。

出于同一原因，USB 函数驱动程序很少需要 *EvtDeviceWakeFromS0Triggered* 或 *EvtDeviceWakeFromSxTriggered* 回调。 相反，框架和基础总线驱动程序会处理将设备返回到工作状态的所有要求。

## <a name="related-topics"></a>相关主题
[USB 驱动程序 (WDF) 中的选择性挂起](selective-suspend-in-usb-drivers-wdf.md)  



