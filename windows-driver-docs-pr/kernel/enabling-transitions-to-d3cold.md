---
title: 启用到 D3cold 的转换
description: 所有版本的 Windows 中都启用设备在计算机处于睡眠状态 （在一个系统低功耗状态 S1 到 S4） 时，要 D3cold。
ms.assetid: C2C6166D-8269-4FCE-81A8-B350626052D4
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 13ce1874616b11a35323b9acce5b247bdaee4f2d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362016"
---
# <a name="enabling-transitions-to-d3cold"></a>启用到 D3cold 的转换


所有版本的 Windows 中都启用设备在计算机处于睡眠状态 （在一个系统低功耗状态 S1 到 S4） 时，要 D3cold。 在计算机退出 S0 之前，功能的驱动程序、 总线驱动程序和筛选器驱动程序协同工作以将设备移到 D3hot。 当计算机进入低功耗 Sx 状态时，此转换具有将设备从 D3hot 移动到 D3cold 的副作用。

从 Windows 8 开始，设备可以进入和退出 D3cold 在计算机仍在 S0 中时。 为设备的电源策略所有者 (PPO) 的驱动程序可以启用和禁用这些转换为 D3cold。 驱动程序不应启用其设备输入 D3cold，除非设备可以如果需要，从 D3cold，唤醒以及然后恢复到 D0 转换后的正常操作。

当设备进入 D3 时，它最初将进入 D3hot D3 子状态。 从 D3hot，D0 或 D3cold，可以输入设备。 在发生唤醒事件或 I/O 请求的响应，则设备将从 D3hot 进入 D0。 否则为设备可能仍处于 D3hot，或者它可能从转为 D3hot D3cold。 有关这些转换的详细信息，请参阅设备电源状态[关系图](device-power-states.md#power-state-diagram)中[设备的电源状态](device-power-states.md)。

该驱动程序不会启动从 D3hot D3cold 到的设备的转换。 相反，此转换发生时与此设备共享通用电源的所有其他设备 D3hot 中，并准备好输入 D3cold。 当这些设备的最后一个输入 D3hot 时，基础总线驱动程序和系统固件删除电源和设备 D3cold 输入更多信息。

设备 PPO 驱动程序通知操作系统是否启用从 D3hot D3cold 到的设备的转换。 该驱动程序可以提供此信息在安装该设备的 INF 文件或驱动程序可以调用[ *SetD3ColdSupport* ](https://msdn.microsoft.com/library/windows/hardware/hh967716)在运行时动态地启用或禁用设备的例程将转换为 D3cold。 有关详细信息，请参阅[使用的 GUID\_D3COLD\_支持\_界面驱动程序接口](using-guid-d3cold-support-interface.md)。

通过启用设备输入 D3cold，驱动程序可保证以下行为：

-   在计算机保留在 S0 中时，设备可以容忍 D3hot 从转换到 D3cold。
-   从 D3cold 恢复 D0 时，设备将正常工作。

设备不能满足任一要求，输入 D3cold 后, 可能不可用之前在计算机重新启动或进入休眠状态。 如果设备必须能够从进入任何低功耗 Dx 状态信号发生唤醒事件，进入 D3cold 必须未启用除非驱动程序为特定设备的唤醒信号，将在 D3cold 中正常工作。

将设备放入 D3cold，已删除的电源与设备的所有源; 并不一定意味着它的意思只允许通过总线设备通信的能力的源都消失了。 设备可能仍将能够绘制足够发出信号将唤醒事件发送到处理器的能力。 例如，删除其主电源源以太网网络接口卡 (NIC) 可能会从以太网电缆消耗电源。

由于 D3cold 是不能用在总线来与设备进行通信的状态，因此驱动程序不能将其设备置于 D3cold 直接。 相反，该驱动程序首先调用[ **PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734)例程以请求 D3 power IRP ( [ **IRP\_MN\_设置\_电源**](https://msdn.microsoft.com/library/windows/hardware/ff551744)请求与目标状态 = **PowerDeviceD3**) 将设备从 D0 移至 D3hot。 输入后 D3hot，设备可能会或可能不从转为 D3hot D3cold。 在设备进入 D3cold 删除时才向总线供电，如果父总线驱动程序将关闭总线出现这种情况，或者如果系统固件关闭电源的硬件平台的一部分。

 

 




