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
ms.openlocfilehash: f355e1d3dbb4564ea5fed025de60539b08626cbf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555404"
---
# <a name="power-policy-ownership"></a>电源策略所有权


每个设备、 一个 （且只有一个） 的设备的驱动程序必须是设备的*电源策略所有者*。 电源策略所有者确定适当[设备电源状态](https://msdn.microsoft.com/library/windows/hardware/ff543162)的到设备的驱动程序堆栈每当设备的电源状态应更改设备并将其发送请求。

基于框架的驱动程序不包含请求的代码在设备的电源状态下，会更改，因为该框架提供了该代码。 默认情况下，每当系统进入[系统睡眠状态](https://msdn.microsoft.com/library/windows/hardware/ff564575)，框架会要求你的设备的总线，以降低到 D3 的设备电源状态的驱动程序。 （您的驱动程序可以更改默认行为，以便该框架你的设备的睡眠状态设置为 D1 或 D2，如果该设备提供唤醒功能。）当系统电源返回到其[处理 (S0) 状态](https://msdn.microsoft.com/library/windows/hardware/ff564591)，框架请求总线驱动程序，以将设备还原到其工作 (D0) 状态。

电源策略所有者程序还负责启用和禁用以下设备功能：

-   输入你的设备的功能[低功耗 （睡眠） 状态](https://msdn.microsoft.com/library/windows/hardware/ff543186)时处于空闲状态且系统保持在其工作 (S0) 状态

-   你的设备的能力本身从睡眠状态唤醒时检测到的外部事件

-   你的设备的功能唤醒从休眠状态，检测到的外部事件时系统的整个系统

如果你的设备支持这些空闲关机和系统唤醒功能，还可以调用的电源策略所有者[ **WdfDeviceInitSetPowerPolicyEventCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff546774)注册一套电源策略事件回调函数。

默认情况下，基于框架的驱动程序，请在设备的功能驱动程序是电源策略所有者。 (如果没有任何功能驱动程序和总线驱动程序已调用[ **WdfPdoInitAssignRawDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548802)，总线驱动程序是电源策略所有者)。 如果你想要更改驱动程序堆栈的电源策略所有者，必须调用默认电源策略所有者[ **WdfDeviceInitSetPowerPolicyOwnership** ](https://msdn.microsoft.com/library/windows/hardware/ff546776)禁用所有权，并将该驱动程序电源策略所有者必须调用**WdfDeviceInitSetPowerPolicyOwnership**启用所有权。

框架的用途的电源策略所有者的以下工作：

-   它处理您的驱动程序和驱动程序堆栈的其余部分之间的所有电源策略通信。 例如，您的驱动程序无需请求总线驱动程序，若要更改设备的电源状态，因为框架发出请求。

-   如果您的驱动程序注册电源策略事件的回调函数时，框架将调用它们时就可以启用或禁用设备的功能，可以从低功耗状态唤醒本身。

-   如果您的驱动程序允许用户修改空闲状态并唤醒设置，该框架提供的设备管理器中显示的属性表页窗体中的用户界面。

有关电源策略所有者的职责的详细信息，请参阅以下主题：

-   [支持的空闲电源关闭](supporting-idle-power-down.md)
-   [支持系统唤醒](supporting-system-wake-up.md)
-   [设备空闲和唤醒行为的用户控件](user-control-of-device-idle-and-wake-behavior.md)
-   [支持功能的电源状态](supporting-functional-power-states.md)

 

 





