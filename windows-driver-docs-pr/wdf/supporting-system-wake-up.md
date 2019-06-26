---
title: 支持系统唤醒
description: 支持系统唤醒
ms.assetid: 519dcd1a-9975-48b1-a032-04348b903ac5
keywords:
- 系统唤醒 WDK KMDF
- 电源管理 WDK KMDF，唤醒功能
- 唤醒功能 WDK KMDF
- 睡眠电源管理 WDK KMDF
- 低功耗状态 WDK KMDF
- 电源管理事件 WDK KMDF
- PME WDK KMDF
- 电源管理功能 WDK KMDF
- PMC WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0304cd242e940e01eff0122f52cb3f76b23b5c5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368021"
---
# <a name="supporting-system-wake-up"></a>支持系统唤醒


低功耗状态系统时，某些设备可以检测外部事件，例如传入的网络数据包，并将系统然后唤醒。 例如，如果 PCI 设备具有系统唤醒功能，则设备电源管理功能 (PMC) 注册中所示，它通过引发 PCI 总线上的电源管理事件 (PME) 信号唤醒系统。

如果你的设备可以从系统范围内低功耗状态，将系统唤醒[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)中的回调函数[电源策略所有者](power-policy-ownership.md)必须执行以下两个步骤：

1.  调用[ **WdfDeviceAssignSxWakeSettings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassignsxwakesettings)指定：

    -   设备将进入低功耗状态
    -   用户是否可以控制设备的空闲状态设置
    -   设备的唤醒功能是启用还是禁用

    有关这些设置的详细信息，请参阅[ **WDF\_设备\_POWER\_策略\_唤醒\_设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_wake_settings)结构。

2.  调用[ **WdfDeviceInitSetPowerPolicyEventCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks)注册以下事件回调函数，如果需要为你的设备：
    -   [*EvtDeviceArmWakeFromSx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx)或[ *EvtDeviceArmWakeFromSxWithReason*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx_with_reason)，它实现了设备硬件对外部唤醒事件作出响应。
    -   [*EvtDeviceDisarmWakeFromSx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_sx)，它表示禁用设备的外部唤醒事件响应的能力。
    -   [*EvtDeviceWakeFromSxTriggered*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_wake_from_sx_triggered)，它告诉总线检测到唤醒信号驱动程序。

总线驱动程序还参与唤醒系统。 适用于设备的总线驱动程序通常提供[ *EvtDeviceEnableWakeAtBus* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_enable_wake_at_bus)并[ *EvtDeviceDisableWakeAtBus* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus)回调函数。 这些函数会尽一切所上启用和禁用设备的功能，可以从低功耗状态唤醒的总线适配器。

当总线驱动程序确定设备已触发唤醒信号时，它必须调用[ **WdfDeviceIndicateWakeStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceindicatewakestatus)以通知框架应还原设备的电源。 然后，框架会将此信息传递给驱动程序堆栈中的驱动程序的其余部分。

控制设备的唤醒功能的注册表项的信息，请参阅[用户控件的设备闲置，唤醒行为](user-control-of-device-idle-and-wake-behavior.md)。

 

 





