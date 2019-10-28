---
title: UMDF 中的电源策略所有权
description: UMDF 中的电源策略所有权
ms.assetid: cf543259-3401-4f3b-a492-53940cea07f3
keywords:
- 电源策略所有权 WDK UMDF
- 电源策略所有权 WDK UMDF，概述
- 电源管理 WDK UMDF，电源策略所有权
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dab18ddac030c053bf4cc09d21eec508f7db6429
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842245"
---
# <a name="power-policy-ownership-in-umdf"></a>UMDF 中的电源策略所有权


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

对于每个设备，设备驱动程序的一个（且只有一个）必须是设备的*电源策略所有者*。 电源策略所有者确定设备的相应[设备电源状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-power-states)，并在设备的电源状态发生变化时将请求发送到设备的驱动程序堆栈。

基于框架的驱动程序不包含请求设备电源状态更改的代码，因为框架提供了该代码。 默认情况下，每当系统进入[系统休眠状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-sleeping-states)时，框架会要求设备总线的驱动程序将设备电源状态降低到 D3。 （如果设备提供唤醒功能，则驱动程序可以更改默认行为，以便框架将设备的睡眠状态设置为 D1 或 D2。）当系统电源恢复到[工作（S0）状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-working-state-s0)时，框架会请求总线驱动程序将设备还原到其工作（D0）状态。

电源策略所有者还负责启用和禁用以下设备功能：

-   设备处于空闲状态且系统保持正常运行（S0）状态时，进入[低功耗（睡眠）状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-sleeping-states)的能力

-   设备在检测到外部事件时能够从睡眠状态唤醒

-   设备在检测到外部事件时能够从系统睡眠状态唤醒整个系统

如果设备支持这些空闲关机和系统唤醒功能，则电源策略所有者还可以支持该框架的[IPowerPolicyCallbackWakeFromS0](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefroms0)和[IPowerPolicyCallbackWakeFromSx](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefromsx)接口，这些接口定义一组电源策略事件回调函数。

默认情况下，基于 UMDF 的驱动程序不是电源策略所有者。 设备的内核模式功能驱动程序为默认电源策略所有者。 （如果没有内核模式功能驱动程序，并且总线驱动程序调用了[**WdfPdoInitAssignRawDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassignrawdevice)，则总线驱动程序为电源策略所有者）。 如果希望基于 UMDF 的驱动程序成为驱动程序堆栈的电源策略所有者，驱动程序必须调用[**IWDFDeviceInitialize：： SetPowerPolicyOwnership**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setpowerpolicyownership)，并且内核模式默认电源策略所有者必须调用[**WdfDeviceInitSetPowerPolicyOwnership**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyownership)禁用所有权。

此外，如果你要为 USB 设备提供基于 UMDF 的驱动程序，并且你希望驱动程序成为电源策略所有者，则驱动程序[**的 inf 文件必须包含用于在**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)registry. 如果此 REG\_DWORD 大小的值设置为任何非零值，则它将禁用[WinUSB](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)驱动程序的能力作为设备的电源策略所有者。 AddReg 指令必须在[**INF DDInstall 节**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section)中，如下面的示例所示。

```cpp
[MyDriver_Install.NT.hw]
AddReg=MyDriver_AddReg

[MyDriver_AddReg]
HKR,,"WinUsbPowerPolicyOwnershipDisabled",0x00010001,1
```

此框架对电源策略所有者执行以下工作：

-   它处理驱动程序与驱动程序堆栈的其余部分之间的所有电源策略通信。 例如，驱动程序不需要请求总线驱动程序来更改设备的电源状态，因为框架发出请求。

-   如果你的驱动程序注册了电源策略事件回调函数，则当需要启用或禁用设备从低功耗状态唤醒自身的能力时，框架会调用它们。

-   如果你的驱动程序允许用户修改空闲和唤醒设置，则该框架将以设备管理器显示的属性表页面的形式提供用户界面。

有关电源策略所有者责任的详细信息，请参阅以下主题：

-   [支持基于 UMDF 的驱动程序中的空闲电源](supporting-idle-power-down-in-umdf-drivers.md)

-   [支持基于 UMDF 的驱动程序中的系统唤醒](supporting-system-wake-up-in-umdf-drivers.md)

-   [在 UMDF 中控制设备空闲和唤醒行为的用户](user-control-of-device-idle-and-wake-behavior-in-umdf.md)

 

 





