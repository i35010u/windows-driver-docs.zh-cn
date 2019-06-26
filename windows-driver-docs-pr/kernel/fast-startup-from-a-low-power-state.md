---
title: 从低功耗状态快速启动
description: 从低功耗状态快速启动
ms.assetid: 1091571c-2e30-4ad5-b4b9-0f8633e68288
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d6c6db45818adf93e6daf7c45992f65e6735860f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386601"
---
# <a name="fast-startup-from-a-low-power-state"></a>从低功耗状态快速启动


若要实现低功耗状态从快速启动，叶节点设备的驱动程序应处理 IRP S0 power (即[ **IRP\_MN\_设置\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)的 IRPS0 系统电源状态）。 设备层次结构中的叶节点的设备具有任何子设备。 叶节点设备具有子设备上没有依赖关系，因为设备的功能驱动程序可以重新初始化设备作为后台任务以避免导致不必要的延迟对操作系统或其他驱动程序。 与此相反，总线驱动程序有需要附加的同步逻辑来协调使用其子设备电源的序列的依赖项。

使用以下步骤来实现的低功耗状态从一个叶节点设备快速启动：

1.  设置 S0 power IRP 完成例程。

2.  发送 S0 断电 IRP 设备堆栈。

3.  立即完成 S0 power IRP，而不是等到完成 IRP D0 强大功能。 S0 power IRP 完成例程运行时，请执行以下操作：

    1.  请求 D0 power IRP (即**IRP\_MN\_设置\_POWER** D0 设备电源状态的 IRP)。

    2.  返回状态\_S0 power IRP 完成例程的成功。

4.  驱动程序应收到任何 I/O 请求排队，但延迟处理任何这些请求，直到它完成处理 D0 能力 IRP 为止。

5.  D0 power IRP 完成例程运行时，初始化设备，但限制为需要使设备准备好使用此例程。

6.  完成上述步骤后，可以开始您的驱动程序来处理 I/O 请求，包括任何可能已排队的 I/O 请求。

**请注意**  前面的步骤不适用于任何电源状态而 PowerSystemWorking (S0) 不用于 power Irp 的处理。 这些步骤专门适用于 power Irp 的转换处理从低功耗状态为开机 (S0) 状态。

 

所有设备都已都完成其 S0 power Irp 后，系统启动时已完成。 这些设备不是必需的在系统启动时，已完成其 D0 power Irp 或完全可以正常完成的。 内核电源管理器具有一组有限的 IRP 调度队列，并且必须使用这些队列以通知返回到 S0 状态系统中的所有设备。 驱动程序无法快速完成其 S0 power Irp 的接收其 S0 power Irp 阻止其他设备的驱动程序。 因此，设计欠佳的驱动程序驱动程序执行的操作应同时按顺序执行，从而降低整体系统启动性能。

驱动程序完成其 S0 power IRP 后，它可能会收到从已打开设备的句柄的应用程序的 I/O 请求。 驱动程序必须永远不会使失败这些 I/O 请求，因为这样做可能会导致应用程序停止响应，并生成超时错误消息。 相反，驱动程序必须排队 I/O 请求，直到该设备已准备好处理它们。

总线驱动程序可以使用类似于刚刚介绍的叶节点设备驱动程序的技术实现低功耗状态从快速启动。 总线驱动程序必须满足一个额外的要求，是为了确保来自子设备的任何请求输入 D0 状态被标记为挂起，直到进入 D0 状态总线设备的未完成的总线驱动程序。

例如，当 USB 集线器的总线驱动程序收到 S0 power IRP，驱动程序请求 D0 power IRP，并接收请求的 D0 power IRP 后完成 S0 power IRP。 但是之后 S0 完成 IRP，, 中心的子设备很可能开始接收其 S0 power Irp，并请求 D0 power Irp。 总线驱动程序应防止子设备输入 D0，直到集线器设备输入 D0。 因此，总线驱动程序应将标记为正在等待子设备中的所有 D0 power Irp 和总线驱动程序完成处理 D0 power IRP 为中心并中心设备已完全初始化之前完成这些 Irp 等待。

有关 power Irp 的详细信息，请参阅以下主题：

[处理 IRP\_MN\_设置\_的电源可用于系统的电源状态](handling-irp-mn-set-power-for-system-power-states.md)

[处理 IRP\_MN\_设置\_的电源可用于设备的电源状态](handling-irp-mn-set-power-for-device-power-states.md)

 

 




