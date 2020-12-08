---
title: Windows 内核模式电源管理器
description: Windows 内核模式电源管理器
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f3fe20081708c766aa233164e731d2e057ae2756
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815047"
---
# <a name="windows-kernel-mode-power-manager"></a>Windows 内核模式电源管理器


Windows 使用电源管理技术来降低计算机的功耗，特别是对于备有电池的便携式计算机。 例如，可以将 Windows 计算机置于睡眠或休眠状态。 计算机设备的复杂电源管理系统经过了发展，因此，当计算机开始关机或降低功耗时，还可以通过适当的方式关闭连接的设备，以便不会丢失数据。 但这些设备需要警告，即电源状态发生变化，并且可能还需要成为通信循环的一部分，通知控制设备等待，直到它们正常关闭。

Windows 内核模式电源管理器管理所有支持电源状态更改的设备的电源状态更改。 这通常通过一种复杂的设备堆栈来控制其他设备。 每个控制设备称为一个 *节点* ，并且必须有一个驱动程序，该驱动程序可以通过设备堆栈处理电源状态更改的通信。

如果你正在编写受电源状态更改影响的驱动程序，你必须能够处理驱动程序代码中的以下类型的信息：

-   系统活动级别。

-   系统电池电量水平。

-   当前要关闭、休眠或休眠的请求。

-   按下电源按钮等用户操作。

-   控制面板设置，如在电池电量达到10% 时自动关闭。

电源管理器使用 Irp 处理这些请求。 有关 Irp 的详细信息，请参阅 [处理 irp](handling-irps.md)。

该电源管理器与策略管理结合使用来处理电源管理并协调电源事件，并生成电源管理 Irp。 Power manager 将收集更改电源状态的请求，决定设备必须将其电源状态更改为哪种顺序，然后发送相应的 Irp 来告知相应的驱动程序进行更改， (这反过来会使更改) 。 策略管理器监视系统中的活动，并将用户状态、应用程序状态和设备驱动程序状态集成到电源策略中。

有关电源管理的更多详细信息，请参阅 [Windows 驱动程序的电源管理](./introduction-to-power-management.md)。

电源管理器被视为 i/o 管理器的子组件。 有关详细信息，请参阅 [Windows I/o 管理器](windows-kernel-mode-i-o-manager.md)。

向电源管理器提供直接接口的例程通常带有 "**Po**" 前缀;例如， **PoSetPowerState**。 有关电源管理器例程的列表，请参阅 [电源管理器例程](/windows-hardware/drivers/ddi/_kernel/#power-management-routines)。

Windows 驱动程序框架 (WDF) 提供一组库以使电源管理变得更加容易。 有关 WDF 的详细信息，请参阅 [内核模式驱动程序框架概述](../wdf/index.md)。

 

