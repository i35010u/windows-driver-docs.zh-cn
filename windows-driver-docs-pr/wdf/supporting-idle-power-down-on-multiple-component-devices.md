---
title: 支持多组件设备空闲时关闭电源
description: 支持多组件设备空闲时关闭电源
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b8ed8281382c49e35092ee0957b6cb64e8f4c55
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834857"
---
# <a name="supporting-idle-power-down-on-multiple-component-devices"></a>支持多组件设备空闲时关闭电源


\[仅适用于 KMDF\]

多组件设备的 KMDF 驱动程序可以支持 [空闲电源关闭](supporting-idle-power-down.md) 和功能电源状态。 因为在这种情况下，驱动程序会直接注册到电源管理框架 (PoFx) ，因此，驱动程序必须将所产生的 Dx 状态更改与 PoFx 进行协调。

## <a name="providing-device-power-policy-idle-settings"></a>提供设备电源策略空闲设置


在调用 [**WdfDeviceAssignS0IdleSettings**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)时，驱动程序必须在 [**WDF \_ 设备 \_ 电源 \_ 策略 \_ 空闲 \_ 设置**](/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)结构中将 **IdleTimeoutType** 设置为 **DriverManagedIdleTimeout** 。 此外，驱动程序必须将 **PowerUpIdleDeviceOnSystemWake** 设置为 **WdfTrue**，并将 **IdleCaps** 设置为 [**IdleCannotWakeFromS0**](/windows-hardware/drivers/ddi/wdfdevice/ne-wdfdevice-_wdf_power_policy_s0_idle_capabilities)，如以下示例中所示。

```ManagedCPlusPlus
WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS s0IdleSettings;

WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS_INIT(&s0IdleSettings, 
                                           IdleCannotWakeFromS0);
s0IdleSettings.IdleTimeoutType = DriverManagedIdleTimeout;
s0IdleSettings.PowerUpIdleDeviceOnSystemWake = WdfTrue;
s0IdleSettings.IdleTimeout = 1;
status = WdfDeviceAssignS0IdleSettings(device, &s0IdleSettings);
```

## <a name="transitioning-from-working-d0-to-low-power-dx-state"></a>从工作 (D0) 转换为 Low-Power (Dx) 状态


在 [*EvtDeviceSelfManagedIoInit*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)中，驱动程序调用 [**WdfDeviceStopIdle**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle) 来进行电源引用，这会阻止 WDF 将设备置于低功耗状态。

驱动程序通过从其 [*DevicePowerRequiredCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_device_power_required_callback)回调例程调用 [**WdfDeviceResumeIdle**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle)来释放电源引用。

驱动程序通常指定非常短的空闲超时，以便在释放所有电源引用后，WDF 会立即将设备置于低功耗状态。

## <a name="transitioning-from-low-power-dx-to-working-d0-state"></a>从 Low-Power (Dx) 转换为工作 (D0) 状态


在 [*DevicePowerRequiredCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_device_power_required_callback)中，驱动程序必须使设备进入工作状态 (D0) 状态。 为此，必须将对 [**WdfDeviceStopIdle**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle) 的调用延迟为工作线程，并将 *WaitForD0* 参数设置为 TRUE。 *不* 能阻止对 **WdfDeviceStopIdle** *的调用。*

相反，驱动程序必须将阻塞调用推迟到在被动级别运行的工作线程，并且保证不会在电源管理队列的 i/o 调度例程的上下文中进行 [**WdfDeviceStopIdle**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle) 调用。

如果驱动程序以前调用了 [**WdfDeviceInitSetPowerPageable**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpageable) (意味着它可以在电源转换) 期间访问可分页的数据，则驱动程序可以调用 [**WdfWorkItemCreate**](/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate) 来创建框架工作项。 如果驱动程序未设置可分页的驱动程序，则驱动程序必须创建自己的系统线程。 有关详细信息，请参阅 [**PsCreateSystemThread**](/windows-hardware/drivers/ddi/wdm/nf-wdm-pscreatesystemthread)。

[**WdfDeviceStopIdle**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)返回后，即使方法返回错误，驱动程序也必须调用 [**PoFxReportDevicePoweredOn**](/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxreportdevicepoweredon)。

 

