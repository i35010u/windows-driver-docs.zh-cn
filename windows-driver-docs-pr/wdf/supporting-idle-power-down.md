---
title: 支持空闲时关闭电源
description: 某些设备在系统保持正常运行（S0）状态时可以进入低功耗（Dx）状态。
ms.assetid: d0ce51db-eeb7-45ef-b823-248cd03ee2a9
keywords:
- 空闲的关闭 WDK KMDF
- 电源管理 WDK KMDF、空闲关机
- 唤醒功能 WDK KMDF
- 睡眠电源管理 WDK KMDF
- 低功耗状态 WDK KMDF
- 系统睡眠状态 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7c792e5a00a79e2fb69531ba45cabffecb5d558
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831790"
---
# <a name="supporting-idle-power-down"></a>支持空闲时关闭电源


某些设备在系统保持正常运行（S0）状态时可以进入低功耗（Dx）状态。 从 Windows 8 开始，设备可以在进入 Dx 状态之前过渡到低功耗功能电源状态（Fx）。 对于此类设备，框架在设备处于空闲（未使用）状态的情况下启动设备或组件的功能，以确定（且可设置）的时间。

其中一些设备还可以在检测到外部事件时在总线上触发唤醒信号。 总线驱动程序会响应此信号，驱动程序堆栈会将设备还原到其工作状态。 （未检测到外部事件的设备仍处于低功耗状态，直到框架要求总线驱动程序启动将设备还原到其工作状态。）

如果设备或组件处于空闲状态，则[电源策略所有者](power-policy-ownership.md)中的[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数必须执行以下两个步骤：

1.  调用[**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)指定：

    -   设备将进入的低功耗状态
    -   设备在电源状态降低之前[必须保持空闲](#idle-conditions)的时间量
    -   设备是否可以检测外部事件，并在总线上触发唤醒信号
    -   用户是否可以控制设备的空闲设置
    -   设备的空闲关机功能是已启用还是已禁用
    -   当系统恢复到工作（S0）状态时，设备是否将恢复为其工作（D0）状态
    -   设备的空闲超时值是否由电源管理框架（PoFx）确定
    -   当空闲超时期限过期时，框架是否可以将设备置于 D3cold 电源状态

    有关这些设置的详细信息，请参阅[**WDF\_设备\_POWER\_策略\_空闲\_设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)结构，以及[支持功能电源状态](supporting-functional-power-states.md)。

2.  如果你的设备需要，请调用[**WdfDeviceInitSetPowerPolicyEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks)来注册以下事件回调函数：
    -   [*EvtDeviceArmWakeFromS0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0)，可使设备硬件（而不是总线）响应外部唤醒事件
    -   [*EvtDeviceDisarmWakeFromS0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_s0)，用于对外部唤醒事件禁用设备功能（而不是总线的能力）
    -   [*EvtDeviceWakeFromS0Triggered*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_wake_from_s0_triggered)，它通知驱动程序总线检测到唤醒信号。


## <a name="idle-conditions"></a>空闲条件

当满足以下所有条件时，框架会将设备视为处于空闲状态，并开始计算空闲时间：

-   为此设备实例创建的任何电源管理队列都没有在队列中等待的任何请求，或已将其分派给驱动程序。 如果请求已分派给驱动程序，并且驱动程序将其发送到 i/o 目标，则请求仍与队列相关。 除非驱动程序使用 "[**发送并忘记" 选项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ne-wdfrequest-_wdf_request_forward_options_flags)发送请求，否则不会将设备视为空闲。 非电源管理队列中的请求不计入设备空闲。
-   如果驱动程序之前调用[**WdfDeviceStopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)，则驱动程序随后称为[**WdfDeviceResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle)。
-   如果电源策略所有者是总线驱动程序，则总线驱动程序的任何子设备都不是 D0。

如果你的驱动程序（或用户）对你的设备启用了空闲电源，则可能必须使用[**WdfDeviceStopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)方法。 如果设备处于工作（D0）状态，此方法会阻止设备置于空闲状态，直到驱动程序调用[**WdfDeviceResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle)。 当驱动程序调用**WdfDeviceStopIdle**时，如果设备处于低功耗状态，并且系统处于正常工作（S0）状态，则框架将请求总线驱动程序将设备还原到其工作（D0）状态。 对**WdfDeviceStopIdle**的每次成功调用都必须通过调用**WdfDeviceResumeIdle**进行匹配。 有关在调试器中查看 power reference 计数的信息，请参阅[在 WDF 中调试 Power Reference 泄漏](debugging-power-reference-leaks-in-wdf.md)。

有关驱动程序何时需要调用[**WdfDeviceStopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)的详细信息，请参阅该方法的参考页。

如果设备可以从低功耗状态唤醒，则设备总线的驱动程序将参与唤醒设备。 总线驱动程序通常提供[*EvtDeviceEnableWakeAtBus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_enable_wake_at_bus)和[*EvtDeviceDisableWakeAtBus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus)回调函数。 这些函数在总线适配器上执行任何必要的操作，以启用和禁用设备从低功耗状态唤醒的能力。

有关控制设备的空闲功能的注册表项的信息，请参阅[用户控制设备空闲和唤醒行为](user-control-of-device-idle-and-wake-behavior.md)。

 

 





