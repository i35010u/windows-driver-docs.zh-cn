---
title: 电源策略所有权
description: 电源策略所有权
ms.assetid: 8e44eedd-6afe-45c6-bbe8-42cfb6f6a644
keywords:
- 电源管理 WDK KMDF，所有权
- 所有权 WDK KMDF
- 所有权 WDK KMDF，电源策略
- 电源策略 WDK KMDF
- 唤醒功能 WDK KMDF
- 睡眠电源管理 WDK KMDF
- 低功耗状态 WDK KMDF
- 设备电源状态 WDK KMDF
- 工作状态 WDK KMDF
- 电源状态 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40bee4f1284dc702cab39d5b2e153be4903a8cd8
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190345"
---
# <a name="power-policy-ownership"></a>电源策略所有权


对于每个设备，一个 (并且只有一个设备的驱动程序) 必须是设备的 *电源策略所有者*。 电源策略所有者确定设备的相应 [设备电源状态](../kernel/device-power-states.md) ，并在设备的电源状态发生变化时将请求发送到设备的驱动程序堆栈。

基于框架的驱动程序不包含请求设备电源状态更改的代码，因为框架提供了该代码。 默认情况下，每当系统进入 [系统休眠状态](../kernel/system-sleeping-states.md)时，框架会要求设备总线的驱动程序将设备电源状态降低到 D3。  (你的驱动程序可以更改默认行为，以便在设备提供唤醒功能的情况下，框架将设备的睡眠状态设置为 D1 或 D2。 ) 系统电源恢复到其 [工作 (S0) 状态](../kernel/system-working-state-s0.md)时，框架会请求总线驱动程序将设备还原到其工作 (D0) 状态。

电源策略所有者还负责启用和禁用以下设备功能：

-   设备处于空闲状态，并且系统仍处于正常工作状态 (S0) 状态时，设备能够进入[低功耗 (睡眠) 状态](../kernel/device-sleeping-states.md)

-   设备在检测到外部事件时能够从睡眠状态唤醒自身

-   设备在检测到外部事件时能够从系统睡眠状态唤醒整个系统

如果设备支持这些空闲关机和系统唤醒功能，则电源策略所有者还可以调用 [**WdfDeviceInitSetPowerPolicyEventCallbacks**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks) 来注册一组电源策略事件回调功能。

默认情况下，对于基于框架的驱动程序，设备的函数驱动程序是电源策略所有者。  (如果没有函数驱动程序，并且总线驱动程序调用 [**WdfPdoInitAssignRawDevice**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassignrawdevice)，则总线驱动程序为电源策略所有者) 。 如果要更改驱动程序堆栈的电源策略所有者，则默认的电源策略所有者必须调用 [**WdfDeviceInitSetPowerPolicyOwnership**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyownership) 来禁用所有权，并且将作为电源策略所有者的驱动程序必须调用 **WdfDeviceInitSetPowerPolicyOwnership** 以启用所有权。

此框架对电源策略所有者执行以下工作：

-   它处理驱动程序与驱动程序堆栈的其余部分之间的所有电源策略通信。 例如，驱动程序不需要请求总线驱动程序来更改设备的电源状态，因为框架发出请求。

-   如果你的驱动程序注册了电源策略事件回调函数，则当需要启用或禁用设备从低功耗状态唤醒自身的能力时，框架会调用它们。

-   如果你的驱动程序允许用户修改空闲和唤醒设置，则该框架将以设备管理器显示的属性表页面的形式提供用户界面。

有关电源策略所有者责任的详细信息，请参阅以下主题：

-   [支持空闲时关闭电源](supporting-idle-power-down.md)
-   [支持系统唤醒](supporting-system-wake-up.md)
-   [设备空闲和唤醒行为的用户控件](user-control-of-device-idle-and-wake-behavior.md)
-   [支持功能性电源状态](supporting-functional-power-states.md)

 

