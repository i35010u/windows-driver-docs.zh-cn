---
title: 支持在多个组件的设备上的空闲状态的电源关闭
description: 支持在多个组件的设备上的空闲状态的电源关闭
ms.assetid: 81C80E30-DAF4-4EE4-AA29-AB40A6827C26
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 984e23f2e2a2fc9d15d4e7b7e4105d12fb1df166
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534261"
---
# <a name="supporting-idle-power-down-on-multiple-component-devices"></a>支持在多个组件的设备上的空闲状态的电源关闭


\[仅适用于 KMDF\]

可以支持多个组件设备的 KMDF 驱动程序[空闲电源关闭](supporting-idle-power-down.md)和正常工作的电源状态。 在这种情况下，驱动程序直接与电源管理框架 (PoFx) 注册，因为该驱动程序必须协调 PoFx 生成 Dx 状态更改。

## <a name="providing-device-power-policy-idle-settings"></a>提供设备电源策略空闲设置


当调用[ **WdfDeviceAssignS0IdleSettings**](https://msdn.microsoft.com/library/windows/hardware/ff545903)，该驱动程序必须设置**IdleTimeoutType**到**DriverManagedIdleTimeout**中[ **WDF\_设备\_POWER\_策略\_空闲\_设置**](https://msdn.microsoft.com/library/windows/hardware/ff551270)结构。 此外，驱动程序必须设置**PowerUpIdleDeviceOnSystemWake**到**WdfTrue**，并**IdleCaps**到[ **IdleCannotWakeFromS0**](https://msdn.microsoft.com/library/windows/hardware/ff552429)，如以下示例所示。

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


在中[ *EvtDeviceSelfManagedIoInit*](https://msdn.microsoft.com/library/windows/hardware/ff540902)，驱动程序调用[ **WdfDeviceStopIdle** ](https://msdn.microsoft.com/library/windows/hardware/ff546921)才能 power 引用，这样可防止从 WDF将设备放在低功耗状态。

该驱动程序通过调用释放 power 参考[ **WdfDeviceResumeIdle** ](https://msdn.microsoft.com/library/windows/hardware/ff546838)从其[ *DevicePowerRequiredCallback* ](https://msdn.microsoft.com/library/windows/hardware/hh450949)回调例程。

该驱动程序通常指定非常简短的空闲超时，以便 WDF 方法将释放所有 power 引用之后立即进入低功耗状态让设备。

## <a name="transitioning-from-low-power-dx-to-working-d0-state"></a>从低功耗 (Dx) 转换为使用 (D0) 状态


在中[ *DevicePowerRequiredCallback*](https://msdn.microsoft.com/library/windows/hardware/hh450949)，驱动程序必须将到其工作 (D0) 状态的设备。 若要执行此操作，它必须遵从工作线程调用[ **WdfDeviceStopIdle** ](https://msdn.microsoft.com/library/windows/hardware/ff546921)与*WaitForD0*参数设置为 TRUE。 对此阻塞调用**WdfDeviceStopIdle**必须*建立*中*DevicePowerRequiredCallback*。

相反，驱动程序必须将推迟到运行在被动级别和保证不进行的工作线程的阻止调用[ **WdfDeviceStopIdle** ](https://msdn.microsoft.com/library/windows/hardware/ff546921)的电源管理队列的 I/O 操作的上下文中调用调度例程。

如果该驱动程序之前已调用[ **WdfDeviceInitSetPowerPageable** ](https://msdn.microsoft.com/library/windows/hardware/ff546766) （这意味着它可以访问 power 转换期间的可分页的数据），该驱动程序可以调用[ **WdfWorkItemCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff551201)创建 framework 工作项。 如果该驱动程序没有设置 power 可分页，驱动程序必须创建自己的系统线程。 有关详细信息，请参阅[ **PsCreateSystemThread**](https://msdn.microsoft.com/library/windows/hardware/ff559932)。

之后[ **WdfDeviceStopIdle** ](https://msdn.microsoft.com/library/windows/hardware/ff546921)返回，即使该方法将返回错误，该驱动程序必须调用[ **PoFxReportDevicePoweredOn**](https://msdn.microsoft.com/library/windows/hardware/hh439526)。

 

 





