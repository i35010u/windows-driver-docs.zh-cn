---
title: 支持功能的驱动程序中的 PnP 和电源管理
description: 支持功能的驱动程序中的 PnP 和电源管理
ms.assetid: 487d4a69-a8a8-406c-8572-688388deabe3
keywords:
- 即插即用 WDK KMDF，功能的驱动程序
- 插 WDK KMDF，功能的驱动程序
- 电源管理 WDK KMDF，功能的驱动程序
- 函数的 WDK KMDF 驱动程序
- 电源策略 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3097fd14a14bafcf9f618984b6f8e9b5ad404c48
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554934"
---
# <a name="supporting-pnp-and-power-management-in-function-drivers"></a>支持功能的驱动程序中的 PnP 和电源管理


*函数的驱动程序*控制设备的操作，因此它们访问的设备硬件。 这些驱动程序必须支持的即插即用和电源管理操作，并通常注册多个事件回调函数时它们[创建设备对象](creating-a-framework-device-object.md)。

通常情况下，功能驱动程序的[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)事件回调函数调用[ **WdfDeviceInitSetPnpPowerEventCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff546135)来注册以下回调函数：

-   [*EvtDevicePrepareHardware*](https://msdn.microsoft.com/library/windows/hardware/ff540880)，它向驱动程序提供了鼠标设备的系统分配的资源。 该驱动程序可以执行使硬件驱动程序可以访问的操作，例如设备的总线相对内存映射到处理器的虚拟地址空间。

-   [*EvtDeviceD0Entry*](https://msdn.microsoft.com/library/windows/hardware/ff540848)，其执行操作，如加载固件的所需每次的驱动程序的设备将进入其工作 (D0) 状态。

-   [*EvtDeviceD0Exit*](https://msdn.microsoft.com/library/windows/hardware/ff540855)，驱动程序的设备会使其工作 (D0) 状态，并进入低功耗状态执行操作所需每次。

-   [*EvtDeviceReleaseHardware*](https://msdn.microsoft.com/library/windows/hardware/ff540890)，以释放任何系统资源的[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)分配。

所有框架定义的回调函数，如前面的列表中是可选的。 您必须提供这些值仅在您的驱动程序需要的时候。

功能的驱动程序可以调用[ **WdfDeviceSetPnpCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff546898)并[ **WdfDeviceSetPowerCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff546901)以报告设备的即插即用和对操作系统的电源管理功能。

通常情况下，将使用的框架*电源管理的 I/O 队列*对于大部分 I/O 请求。 如果 I/O 队列，电源管理框架提供给驱动程序请求的仅当其设备已在其工作 (D0) 状态。 有关电源管理 I/O 队列的详细信息，请参阅[I/O 队列的电源管理](power-management-for-i-o-queues.md)。

通常情况下，设备的功能驱动程序是*电源策略所有者*的驱动程序堆栈。 电源策略所有者确定适当[设备电源状态](https://msdn.microsoft.com/library/windows/hardware/ff543162)的到设备的驱动程序堆栈每当设备的电源状态应更改设备并将其发送请求。 有关基于 framework 的驱动程序，该框架将处理此职责，因此不需要提供您请求设备的电源状态更改的驱动程序中的代码。

电源策略所有者具有两个额外的职责： 控制设备的功能时处于空闲状态，并且系统保持在进入低功耗状态及其[处理 (S0) 状态](https://msdn.microsoft.com/library/windows/hardware/ff564591)，及其控制的设备的功能生成检测到低功耗状态中的外部事件时唤醒信号。 如果你的设备具有空闲或唤醒功能，功能驱动程序可以提供其他回调函数。 电源策略所有者的职责的详细信息，请参阅[电源策略所有权](power-policy-ownership.md)。

 

 





