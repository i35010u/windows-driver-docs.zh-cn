---
title: 支持空闲时关闭电源
description: 系统仍在其工作 (S0) 状态时，某些设备可以进入低功耗 (Dx) 状态。
ms.assetid: d0ce51db-eeb7-45ef-b823-248cd03ee2a9
keywords:
- 空闲关闭 WDK KMDF
- 电源管理 WDK KMDF、 空闲关机
- 唤醒功能 WDK KMDF
- 睡眠电源管理 WDK KMDF
- 低功耗状态 WDK KMDF
- 系统睡眠状态 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fad731308be63be77cd3b6a978bad81ce30ed92
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377385"
---
# <a name="supporting-idle-power-down"></a>支持空闲时关闭电源


系统仍在其工作 (S0) 状态时，某些设备可以进入低功耗 (Dx) 状态。 从 Windows 8 开始，设备可以转换到低功耗正常工作的电源状态 (Fx) 进入 Dx 状态之前。 对于此类设备，框架将启动降低电源的设备或组件的后该设备处于空闲状态 （未使用） 预先确定的 （且可设置的） 的时间量。

检测到任何外部事件，这些设备的一些还可以触发总线上的唤醒信号。 总线驱动程序响应此信号，并驱动程序堆栈将设备还原到其工作状态。 （未检测到外部事件的设备仍保留在低功耗状态直到框架要求总线驱动程序以启动设备还原到其工作状态。）

如果您的设备或组件，可以关闭电源时处于空闲状态， [ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)中的回调函数[电源策略所有者](power-policy-ownership.md)必须执行以下两个步骤：

1.  调用[ **WdfDeviceAssignS0IdleSettings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)指定：

    -   设备将进入低功耗状态
    -   时间的设备[必须保持空闲状态](#idle-conditions)降低其电源状态之前
    -   设备是否可以检测的外部事件，并触发总线上的唤醒信号
    -   用户是否可以控制设备的空闲状态设置
    -   设备的空闲关机功能是启用还是禁用
    -   是否设备系统返回到其工作 (S0) 状态时将返回到其工作 (D0) 状态
    -   是否在设备的空闲超时值确定的电源管理框架 (PoFx)
    -   是否框架可以将设备置于 D3cold 电源状态的空闲超时期限过期时

    有关这些设置的详细信息，请参阅[ **WDF\_设备\_POWER\_策略\_空闲\_设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)结构，作为以及[支持功能的电源状态](supporting-functional-power-states.md)。

2.  调用[ **WdfDeviceInitSetPowerPolicyEventCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks)注册以下事件回调函数，如果需要为你的设备：
    -   [*EvtDeviceArmWakeFromS0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0)，可让设备硬件 （而不在总线），以响应外部的唤醒事件
    -   [*EvtDeviceDisarmWakeFromS0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_s0)，它表示禁用外部唤醒事件响应设备的功能 （不在总线功能）
    -   [*EvtDeviceWakeFromS0Triggered*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_wake_from_s0_triggered)，它告诉总线检测到唤醒信号驱动程序。


## <a name="idle-conditions"></a>空闲条件

框架认为设备不处于空闲状态，并开始计数空闲时间，当满足所有以下条件：

-   无此设备实例创建的电源管理队列已在队列中等待的任何请求或分派给该驱动程序。 如果请求被调度到驱动程序，该驱动程序将其发送到的 I/O 目标，请求仍与队列。 设备将不被视为处于空闲状态，除非该驱动程序使用，否则[**发送和忘记选项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/ne-wdfrequest-_wdf_request_forward_options_flags)将请求发送。 中非电源管理的队列的请求都不会计入设备空闲。
-   如果该驱动程序之前调用[ **WdfDeviceStopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicestopidle)，随后调用驱动程序，具有[ **WdfDeviceResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle)。
-   如果电源策略所有者是总线驱动程序，没有任何子设备的总线驱动程序都在 D0。

如果您的驱动程序 （或用户） 启用空闲关闭设备，你可能必须使用[ **WdfDeviceStopIdle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicestopidle)方法。 如果设备在其工作 (D0) 状态，此方法将阻止设备驱动程序调用直到空闲[ **WdfDeviceResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle)。 如果设备处于低功耗状态时，驱动程序调用**WdfDeviceStopIdle**，并且该框架的系统是在其工作 (S0) 状态，如果请求总线驱动程序，以将设备还原到其工作 (D0) 状态。 每次成功调用**WdfDeviceStopIdle**必须通过调用匹配**WdfDeviceResumeIdle**。 在调试器中查看 power 引用计数的信息，请参阅[WDF 中调试 Power 引用泄漏](debugging-power-reference-leaks-in-wdf.md)。

详细了解您的驱动程序可能需要调用[ **WdfDeviceStopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicestopidle)，请参阅该方法的参考页。

如果设备可以唤醒本身从低功耗状态，为设备的总线驱动程序参与了唤醒设备。 总线驱动程序通常提供[ *EvtDeviceEnableWakeAtBus* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_enable_wake_at_bus)并[ *EvtDeviceDisableWakeAtBus* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus)回调函数。 这些函数会尽一切所上启用和禁用设备的功能，可以从低功耗状态唤醒的总线适配器。

控制设备的空闲状态功能的注册表项的信息，请参阅[用户控件的设备空闲和唤醒行为](user-control-of-device-idle-and-wake-behavior.md)。

 

 





