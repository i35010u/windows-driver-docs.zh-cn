---
title: 与调用 PoCallDriver 调用 IoCallDriver
description: 与调用 PoCallDriver 调用 IoCallDriver
ms.assetid: a47e2310-e89b-4552-bbe3-d4984ae8b564
keywords:
- PoCallDriver
- 活动的电源 Irp WDK 内核
- power Irp WDK 内核，而不是 PoCallDriver IoCallDriver
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed224827b53ea3b1eccd92fb42753c02081981ee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533030"
---
# <a name="calling-iocalldriver-versus-calling-pocalldriver"></a>与调用 PoCallDriver 调用 IoCallDriver





从 Windows Vista 开始，驱动程序应调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)而不是[ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)、 要传递给 power Irp下一步较低的驱动程序。 在 Windows Server 2003、 Windows XP 和 Windows 2000 中，驱动程序必须调用**PoCallDriver**，而非**IoCallDriver**，以将 power Irp 传递给下一个较低驱动程序。 但请注意，使用相同的代码运行在 Windows Vista 和早期 Windows 版本中中的驱动程序必须调用**PoCallDriver**，而非**IoCallDriver**。

从 Windows Vista 开始[ **PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734)并**IoCallDriver**确保电源管理器将在整个系统的电源 Irp 正确同步。 在 Windows Server 2003、 Windows XP 和 Windows 2000 **PoRequestPowerIrp**， **PoCallDriver**，并[ **PoStartNextPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559776)，请确保电源管理器将在整个系统的电源 Irp 正确同步。

系统活动的电源 Irp 数限制，如下所示：

-   多个系统电源 IRP (**IRP\_MN\_设置\_POWER**) 在任意给定时间。

-   不能超过一个设备组的电源 IRP (**IRP\_MN\_设置\_POWER)** 在任何给定时间可以对每个 PDO 处于活动状态。

-   在任何给定时间，不超过一个设备电源要求 power 浪涌 IRP 可以处于活动状态系统中的任意位置。

若要确保两个浪涌设备未尝试同时通电，电源管理器跟踪的活动浪涌 power Irp 跨整个系统，并仅允许一个处于活动状态一次。 其他浪涌 active 浪涌 IRP 已经完成才能启动 IRP。

由于这些限制在浪涌 Irp，IRP 涌入时可能会阻止设备电源 IRP 的另一台设备完成。 调试时，驱动程序编写人员应注意到此行为。

 

 




