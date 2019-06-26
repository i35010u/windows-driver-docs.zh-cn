---
title: 支持多组件设备空闲时关闭电源
description: 支持多组件设备空闲时关闭电源
ms.assetid: 81C80E30-DAF4-4EE4-AA29-AB40A6827C26
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9632e4c16702fad90d759cff22beb0aa3c35eac8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384276"
---
# <a name="supporting-idle-power-down-on-multiple-component-devices"></a>支持多组件设备空闲时关闭电源


\[仅适用于 KMDF\]

可以支持多个组件设备的 KMDF 驱动程序[空闲电源关闭](supporting-idle-power-down.md)和正常工作的电源状态。 在这种情况下，驱动程序直接与电源管理框架 (PoFx) 注册，因为该驱动程序必须协调 PoFx 生成 Dx 状态更改。

## <a name="providing-device-power-policy-idle-settings"></a>提供设备电源策略空闲设置


当调用[ **WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)，该驱动程序必须设置**IdleTimeoutType**到**DriverManagedIdleTimeout**中[ **WDF\_设备\_POWER\_策略\_空闲\_设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)结构。 此外，驱动程序必须设置**PowerUpIdleDeviceOnSystemWake**到**WdfTrue**，并**IdleCaps**到[ **IdleCannotWakeFromS0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ne-wdfdevice-_wdf_power_policy_s0_idle_capabilities)，如以下示例所示。

```ManagedCPlusPlus
WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS s0IdleSettings;

WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS_INIT(&s0IdleSettings, 
                                           IdleCannotWakeFromS0);
s0IdleSettings.IdleTimeoutType = DriverManagedIdleTimeout;
s0IdleSettings.PowerUpIdleDeviceOnSystemWake = WdfTrue;
s0IdleSettings.IdleTimeout = 1;
status = WdfDeviceAssignS0IdleSettings(device, &s0IdleSettings);
```

## <a name="transitioning-from-working-d0-to-low-power-dx-state"></a>从工作到低功耗 (Dx) 的状态 (D0) 转换


在中[ *EvtDeviceSelfManagedIoInit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)，驱动程序调用[ **WdfDeviceStopIdle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicestopidle)才能 power 引用，这样可防止从 WDF将设备放在低功耗状态。

该驱动程序通过调用释放 power 参考[ **WdfDeviceResumeIdle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle)从其[ *DevicePowerRequiredCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_device_power_required_callback)回调例程。

该驱动程序通常指定非常简短的空闲超时，以便 WDF 方法将释放所有 power 引用之后立即进入低功耗状态让设备。

## <a name="transitioning-from-low-power-dx-to-working-d0-state"></a>从低功耗 (Dx) 转换为使用 (D0) 状态


在中[ *DevicePowerRequiredCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_device_power_required_callback)，驱动程序必须将到其工作 (D0) 状态的设备。 若要执行此操作，它必须遵从工作线程调用[ **WdfDeviceStopIdle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicestopidle)与*WaitForD0*参数设置为 TRUE。 对此阻塞调用**WdfDeviceStopIdle**必须*建立*中*DevicePowerRequiredCallback*。

相反，驱动程序必须将推迟到运行在被动级别和保证不进行的工作线程的阻止调用[ **WdfDeviceStopIdle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicestopidle)的电源管理队列的 I/O 操作的上下文中调用调度例程。

如果该驱动程序之前已调用[ **WdfDeviceInitSetPowerPageable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpageable) （这意味着它可以访问 power 转换期间的可分页的数据），该驱动程序可以调用[ **WdfWorkItemCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)创建 framework 工作项。 如果该驱动程序没有设置 power 可分页，驱动程序必须创建自己的系统线程。 有关详细信息，请参阅[ **PsCreateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pscreatesystemthread)。

之后[ **WdfDeviceStopIdle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicestopidle)返回，即使该方法将返回错误，该驱动程序必须调用[ **PoFxReportDevicePoweredOn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxreportdevicepoweredon)。

 

 





