---
title: UMDF 中的电源策略所有权
description: UMDF 中的电源策略所有权
ms.assetid: cf543259-3401-4f3b-a492-53940cea07f3
keywords:
- 电源策略所有权 WDK UMDF
- 电源策略所有权 WDK UMDF 概述
- 电源管理 WDK UMDF，电源策略所有权
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ed7ed3743b28425952a5b59cbd948671867d927
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371105"
---
# <a name="power-policy-ownership-in-umdf"></a>UMDF 中的电源策略所有权


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

每个设备、 一个 （且只有一个） 的设备的驱动程序必须是设备的*电源策略所有者*。 电源策略所有者确定适当[设备电源状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-power-states)的到设备的驱动程序堆栈每当设备的电源状态应更改设备并将其发送请求。

基于框架的驱动程序不包含请求的代码在设备的电源状态下，会更改，因为该框架提供了该代码。 默认情况下，每当系统进入[系统睡眠状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-sleeping-states)，框架会要求你的设备的总线，以降低到 D3 的设备电源状态的驱动程序。 （您的驱动程序可以更改默认行为，以便该框架你的设备的睡眠状态设置为 D1 或 D2，如果该设备提供唤醒功能。）当系统电源返回到其[处理 (S0) 状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-working-state-s0)，框架请求总线驱动程序，以将设备还原到其工作 (D0) 状态。

电源策略所有者程序还负责启用和禁用以下设备功能：

-   输入你的设备的功能[低功耗 （睡眠） 状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-sleeping-states)时处于空闲状态且系统保持在其工作 (S0) 状态

-   你的设备能够唤醒本身从睡眠状态，检测到的外部事件时

-   你的设备的功能唤醒从休眠状态，检测到的外部事件时系统的整个系统

如果你的设备支持这些空闲关机和系统唤醒功能，电源策略所有者还可以支持的框架[IPowerPolicyCallbackWakeFromS0](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefroms0)和[IPowerPolicyCallbackWakeFromSx](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefromsx)接口，定义一组的电源策略事件的回调函数。

默认情况下，基于 UMDF 驱动程序不是电源策略所有者。 设备的内核模式功能驱动程序是默认电源策略所有者。 (如果没有任何内核模式功能驱动程序和总线驱动程序已调用[ **WdfPdoInitAssignRawDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitassignrawdevice)，总线驱动程序是电源策略所有者)。 如果您希望基于 UMDF 驱动程序是驱动程序堆栈的电源策略所有者，该驱动程序必须调用[ **IWDFDeviceInitialize::SetPowerPolicyOwnership**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setpowerpolicyownership)，和内核模式下默认电源策略所有者必须调用[ **WdfDeviceInitSetPowerPolicyOwnership** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyownership)禁用所有权。

此外，如果你要为 USB 设备提供基于 UMDF 驱动程序，并且如果您希望您的驱动程序是电源策略所有者，驱动程序的 INF 文件必须包含[ **INF AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive) ，用于设置WinUsbPowerPolicyOwnershipDisabled 注册表中的值。 如果此 REG\_DWORD 大小的值设置为任何非零数字，它会禁用[WinUSB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)驱动程序的能力是设备的电源策略所有者。 AddReg 指令必须在[ **INF DDInstall.HW 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section)，如下面的示例所示。

```cpp
[MyDriver_Install.NT.hw]
AddReg=MyDriver_AddReg

[MyDriver_AddReg]
HKR,,"WinUsbPowerPolicyOwnershipDisabled",0x00010001,1
```

框架的用途的电源策略所有者的以下工作：

-   它处理您的驱动程序和驱动程序堆栈的其余部分之间的所有电源策略通信。 例如，您的驱动程序无需请求总线驱动程序，若要更改设备的电源状态，因为框架发出请求。

-   如果您的驱动程序注册电源策略事件的回调函数时，框架将调用它们时就可以启用或禁用设备的功能，可以从低功耗状态唤醒本身。

-   如果您的驱动程序允许用户修改空闲状态并唤醒设置，该框架提供的设备管理器中显示的属性表页窗体中的用户界面。

有关电源策略所有者的职责的详细信息，请参阅以下主题：

-   [在基于 UMDF 驱动程序中支持空闲电源关闭](supporting-idle-power-down-in-umdf-drivers.md)

-   [在基于 UMDF 驱动程序中支持系统唤醒](supporting-system-wake-up-in-umdf-drivers.md)

-   [设备的用户控制空闲和唤醒 UMDF 中的行为](user-control-of-device-idle-and-wake-behavior-in-umdf.md)

 

 





