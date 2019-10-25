---
title: 支持多组件设备空闲时关闭电源
description: 支持多组件设备空闲时关闭电源
ms.assetid: 81C80E30-DAF4-4EE4-AA29-AB40A6827C26
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6b25ec8b16be38f1efef6b048b3c87000b1d5b9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831786"
---
# <a name="supporting-idle-power-down-on-multiple-component-devices"></a>支持多组件设备空闲时关闭电源


\[仅适用于 KMDF\]

多组件设备的 KMDF 驱动程序可以支持[空闲电源关闭](supporting-idle-power-down.md)和功能电源状态。 因为在这种情况下，驱动程序会直接注册到电源管理框架（PoFx），因此驱动程序必须与 PoFx 协调产生的 Dx 状态更改。

## <a name="providing-device-power-policy-idle-settings"></a>提供设备电源策略空闲设置


调用[**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)时，驱动程序必须在 WDF\_设备中将**IdleTimeoutType**设置为**DRIVERMANAGEDIDLETIMEOUT** ， [ **\_POWER\_策略\_空闲\_设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)构造. 此外，驱动程序必须将**PowerUpIdleDeviceOnSystemWake**设置为**WdfTrue**，并将**IdleCaps**设置为[**IdleCannotWakeFromS0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ne-wdfdevice-_wdf_power_policy_s0_idle_capabilities)，如以下示例中所示。

```ManagedCPlusPlus
WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS s0IdleSettings;

WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS_INIT(&s0IdleSettings, 
                                           IdleCannotWakeFromS0);
s0IdleSettings.IdleTimeoutType = DriverManagedIdleTimeout;
s0IdleSettings.PowerUpIdleDeviceOnSystemWake = WdfTrue;
s0IdleSettings.IdleTimeout = 1;
status = WdfDeviceAssignS0IdleSettings(device, &s0IdleSettings);
```

## <a name="transitioning-from-working-d0-to-low-power-dx-state"></a>从工作（D0）转换到低功耗（Dx）状态


在[*EvtDeviceSelfManagedIoInit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)中，驱动程序调用[**WdfDeviceStopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)来进行电源引用，这会阻止 WDF 将设备置于低功耗状态。

驱动程序通过从其[*DevicePowerRequiredCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_device_power_required_callback)回调例程调用[**WdfDeviceResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle)来释放电源引用。

驱动程序通常指定非常短的空闲超时，以便在释放所有电源引用后，WDF 会立即将设备置于低功耗状态。

## <a name="transitioning-from-low-power-dx-to-working-d0-state"></a>从低功耗（Dx）到工作（D0）状态转换


在[*DevicePowerRequiredCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_device_power_required_callback)中，驱动程序必须使设备进入工作（D0）状态。 为此，必须将对[**WdfDeviceStopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)的调用延迟为工作线程，并将*WaitForD0*参数设置为 TRUE。 *不*能阻止对**WdfDeviceStopIdle** *的调用。*

相反，驱动程序必须将阻塞调用推迟到在被动级别运行的工作线程，并且保证不会在电源管理队列的 i/o 调度例程的上下文中进行[**WdfDeviceStopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)调用。

如果驱动程序以前调用了[**WdfDeviceInitSetPowerPageable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpageable) （这意味着它可以在电源转换期间访问可分页的数据），则驱动程序可以调用[**WdfWorkItemCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)来创建框架工作项。 如果驱动程序未设置可分页的驱动程序，则驱动程序必须创建自己的系统线程。 有关详细信息，请参阅[**PsCreateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pscreatesystemthread)。

[**WdfDeviceStopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)返回后，即使方法返回错误，驱动程序也必须调用[**PoFxReportDevicePoweredOn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxreportdevicepoweredon)。

 

 





