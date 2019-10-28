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
ms.openlocfilehash: 6a1d1ae68c608648d512dd879d6f5983af947bb4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842243"
---
# <a name="power-policy-ownership"></a>电源策略所有权


对于每个设备，设备驱动程序的一个（且只有一个）必须是设备的*电源策略所有者*。 电源策略所有者确定设备的相应[设备电源状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-power-states)，并在设备的电源状态发生变化时将请求发送到设备的驱动程序堆栈。

基于框架的驱动程序不包含请求设备电源状态更改的代码，因为框架提供了该代码。 默认情况下，每当系统进入[系统休眠状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-sleeping-states)时，框架会要求设备总线的驱动程序将设备电源状态降低到 D3。 （如果设备提供唤醒功能，则驱动程序可以更改默认行为，以便框架将设备的睡眠状态设置为 D1 或 D2。）当系统电源恢复到[工作（S0）状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-working-state-s0)时，框架会请求总线驱动程序将设备还原到其工作（D0）状态。

电源策略所有者还负责启用和禁用以下设备功能：

-   设备处于空闲状态且系统保持正常运行（S0）状态时，进入[低功耗（睡眠）状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-sleeping-states)的能力

-   设备在检测到外部事件时能够从睡眠状态唤醒自身

-   设备在检测到外部事件时能够从系统睡眠状态唤醒整个系统

如果设备支持这些空闲关机和系统唤醒功能，则电源策略所有者还可以调用[**WdfDeviceInitSetPowerPolicyEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks)来注册一组电源策略事件回调功能。

默认情况下，对于基于框架的驱动程序，设备的函数驱动程序是电源策略所有者。 （如果没有函数驱动程序，并且总线驱动程序调用了[**WdfPdoInitAssignRawDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassignrawdevice)，则总线驱动程序为电源策略所有者）。 如果要更改驱动程序堆栈的电源策略所有者，则默认电源策略所有者必须调用[**WdfDeviceInitSetPowerPolicyOwnership**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyownership)来禁用所有权，并且将作为电源策略所有者的驱动程序必须调用**WdfDeviceInitSetPowerPolicyOwnership**以启用所有权。

此框架对电源策略所有者执行以下工作：

-   它处理驱动程序与驱动程序堆栈的其余部分之间的所有电源策略通信。 例如，驱动程序不需要请求总线驱动程序来更改设备的电源状态，因为框架发出请求。

-   如果你的驱动程序注册了电源策略事件回调函数，则当需要启用或禁用设备从低功耗状态唤醒自身的能力时，框架会调用它们。

-   如果你的驱动程序允许用户修改空闲和唤醒设置，则该框架将以设备管理器显示的属性表页面的形式提供用户界面。

有关电源策略所有者责任的详细信息，请参阅以下主题：

-   [支持空闲关机](supporting-idle-power-down.md)
-   [支持系统唤醒](supporting-system-wake-up.md)
-   [设备空闲和唤醒行为的用户控制](user-control-of-device-idle-and-wake-behavior.md)
-   [支持功能电源状态](supporting-functional-power-states.md)

 

 





