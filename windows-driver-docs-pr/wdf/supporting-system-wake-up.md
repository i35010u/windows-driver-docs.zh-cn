---
title: 支持系统唤醒
description: 支持系统唤醒
keywords:
- 系统唤醒 KMDF
- 电源管理 WDK KMDF、唤醒功能
- 唤醒功能 WDK KMDF
- 睡眠电源管理 WDK KMDF
- 低功耗状态 WDK KMDF
- 电源管理事件 WDK KMDF
- PME WDK KMDF
- 电源管理功能 WDK KMDF
- PMC WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc5d1bc7aa9c667ef7f2291122f816392eafe745
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836589"
---
# <a name="supporting-system-wake-up"></a>支持系统唤醒


当系统处于低功耗状态时，某些设备可以检测到外部事件，例如传入网络数据包，并唤醒系统。 例如，如果 PCI 设备具有系统唤醒功能，如设备的电源管理功能 (PMC) 寄存器中所示，则会通过在 PCI 总线上的 PME) 信号 (PME 发出电源管理事件来唤醒系统。

如果设备可以将系统从系统范围内的低功耗状态唤醒，则 [电源策略所有者](power-policy-ownership.md)中的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数必须执行以下两个步骤：

1.  调用 [**WdfDeviceAssignSxWakeSettings**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassignsxwakesettings) 指定：

    -   设备将进入的低功耗状态
    -   用户是否可以控制设备的空闲设置
    -   设备的唤醒功能是已启用还是已禁用

    有关这些设置的详细信息，请参阅 [**WDF \_ 设备 \_ 电源 \_ 策略 \_ 唤醒 \_ 设置**](/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_wake_settings) 结构。

2.  如果你的设备需要，请调用 [**WdfDeviceInitSetPowerPolicyEventCallbacks**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks) 来注册以下事件回调函数：
    -   [*EvtDeviceArmWakeFromSx*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx) 或 [*EvtDeviceArmWakeFromSxWithReason*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx_with_reason)，使设备硬件能够响应外部唤醒事件。
    -   [*EvtDeviceDisarmWakeFromSx*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_sx)，用于禁用设备对外部唤醒事件的响应能力。
    -   [*EvtDeviceWakeFromSxTriggered*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_wake_from_sx_triggered)，它通知驱动程序总线检测到唤醒信号。

总线驱动程序还参与了对系统的唤醒。 设备总线的驱动程序通常提供 [*EvtDeviceEnableWakeAtBus*](/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_enable_wake_at_bus) 和 [*EvtDeviceDisableWakeAtBus*](/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus) 回调函数。 这些函数在总线适配器上执行任何必要的操作，以启用和禁用设备从低功耗状态唤醒的能力。

当总线驱动程序确定设备触发了唤醒信号时，它必须调用 [**WdfDeviceIndicateWakeStatus**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceindicatewakestatus) 来通知框架应还原设备的电源。 然后，框架将此信息传递给驱动程序堆栈中的其余驱动程序。

有关控制设备的唤醒功能的注册表项的信息，请参阅 [用户控制设备空闲和唤醒行为](user-control-of-device-idle-and-wake-behavior.md)。

 

